---
title: aaaReplicate Hyper-V virtuele machines in VMM-clouds met Azure Site Recovery en PowerShell (Resource Manager) | Microsoft Docs
description: Hyper-V virtuele machines in VMM-clouds met Azure Site Recovery en PowerShell repliceren
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>Hyper-V virtuele machines in VMM-clouds tooAzure met PowerShell en Azure Resource Manager repliceren
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Klassieke portal](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Klassiek](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>Overzicht
Azure Site Recovery draagt bij aan tooyour zakelijke continuïteit en noodherstel (BCDR) strategie door replicatie, failovers en herstel van virtuele machines in een aantal implementatiescenario's te organiseren. Voor een volledige lijst van de implementatie van scenario's Hallo Zie [Azure Site Recovery-overzicht](site-recovery-overview.md).

Dit artikel laat zien hoe toouse PowerShell tooautomate algemene taken moet u tooperform bij het instellen van Azure Site Recovery tooreplicate Hyper-V virtuele machines in System Center VMM-clouds tooAzure opslag.

Hallo artikel bevat vereisten voor Hallo scenario en laat zien u

* Hoe tooset van een Recovery Services-kluis
* Hello Azure Site Recovery Provider installeren op de bronserver VMM Hallo
* Hallo-server registreren in de kluis hello, Azure storage-account toevoegen
* Hello Azure Recovery Services agent op Hyper-V-host-servers installeren
* Configureer beveiligingsinstellingen voor VMM-clouds die toegepast tooall beveiligde virtuele machines worden
* Schakel de beveiliging voor deze virtuele machines.
* Test Hallo failover-toomake controleren of dat alles werkt zoals verwacht.

Als u problemen bij het instellen van dit scenario, stel uw vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo Resource Manager-implementatiemodel.
>
>

## <a name="before-you-start"></a>Voordat u begint
Zorg ervoor dat u deze vereisten hebt voldaan:

### <a name="azure-prerequisites"></a>Vereisten voor Azure
* U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig. Als u niet hebt, beginnen met een [gratis account](https://azure.microsoft.com/free). U kunt bovendien lezen over Hallo [prijzen van Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Als u uit Hallo tooa CSP abonnement replicatiescenario probeert, hebt u een CSP-abonnement nodig. Meer informatie over Hallo CSP programma in [hoe tooenroll Hallo CSP programma](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).
* U moet een tooAzure toostore gerepliceerde gegevens van Azure v2-opslag (Resource Manager)-account. Hallo-account moet geo-replicatie is ingeschakeld. Deze moet in dezelfde regio bevinden als hello Azure Site Recovery-service hello, en worden gekoppeld aan Hallo hetzelfde abonnement of Hallo CSP-abonnement. toolearn meer informatie over het instellen van Azure-opslag, Zie Hallo [tooMicrosoft inleiding Azure Storage](../storage/common/storage-introduction.md) ter referentie.
* U moet zorgen dat virtuele machines die u wilt dat tooprotect aan Hallo voldoen toomake [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

> [!NOTE]
> Er zijn momenteel alleen VM niveau bewerkingen mogelijk via Powershell. Ondersteuning voor niveau herstelbewerkingen plan zal binnenkort worden gesteld.  Nu bent u beperkt tooperforming failovers van datacenters alleen op een granulatie 'beveiligde virtuele machine' en niet op een herstelplan-niveau.
>
>

### <a name="vmm-prerequisites"></a>VMM-vereisten
* U moet de VMM-server waarop System Center 2012 R2.
* De VMM-servers die virtuele machines bevat die u wilt, tooprotect hello Azure Site Recovery Provider moet worden uitgevoerd. Dit wordt geïnstalleerd tijdens de implementatie van Azure Site Recovery Hallo.
* U moet ten minste één cloud op Hallo gewenste tooprotect VMM-server. Hallo cloud moet bevatten:
  * Een of meer VMM-hostgroepen.
  * Een of meer Hyper-V-hostservers of -clusters in elke hostgroep.
  * Een of meer virtuele machines op Hallo bron Hyper-V-server.
* Meer informatie over het instellen van VMM-clouds:
  * Meer informatie over VMM-privéclouds in [What's New in een Privécloud met System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) en in [VMM 2012 en Hallo clouds](http://go.microsoft.com/fwlink/?LinkId=324956).
  * Meer informatie over [configureren Hallo VMM fabric cloud](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * Nadat uw cloud fabric-elementen voldaan zijn informatie over het maken van privéclouds in [maken van een privécloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) en in [overzicht: privéclouds maken met System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).

### <a name="hyper-v-prerequisites"></a>Hyper-V-vereisten
* Hallo Hyper-V-hostservers moeten ten minste draaien **Windows Server 2012** met Hyper-V-rol of **Microsoft Hyper-V Server 2012** en hebben Hallo nieuwste updates zijn geïnstalleerd.
* Als u Hyper-V in een cluster uitvoert, wordt die clusterbroker niet automatisch gemaakt als u een cluster op basis van een statisch IP-adres hebt. U moet tooconfigure hello clusterbroker handmatig. voor
* Zie voor instructies [hoe tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).
* Alle Hyper-V-hostserver of het cluster waarvoor u de toomanage beveiliging moet worden opgenomen in een VMM-cloud.

### <a name="network-mapping-prerequisites"></a>Vereisten voor netwerktoewijzing
Wanneer u virtuele machines in Azure beveiligt, toegewezen netwerktoewijzing Hallo Hallo virtuele-machinenetwerken op Hallo bron-VMM-server en doel-Azure-netwerken tooenable Hallo volgende:

* Alle machines die een failover op Hallo dezelfde netwerk verbinding kan maken van andere, ongeacht welk herstelplan ze tooeach.
* Als een netwerkgateway ingesteld op Hallo Azure-doelnetwerk is, kunnen virtuele machines verbinding tooother on-premises virtuele machines maken.
* Als u geen netwerktoewijzing configureert, alleen virtuele machines met failover in Hallo dezelfde Hallo herstelplan kunnen tooconnect tooeach andere worden na de failover-tooAzure.

Als u wilt dat de netwerktoewijzing toodeploy moet u de volgende Hallo:

* Hallo virtuele machines die u wilt dat tooprotect op Hallo bron-VMM-server moet zijn verbonden tooa VM-netwerk. Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud.
* Een Azure-netwerk toowhich gerepliceerde virtuele machines verbinding kunnen maken na failover. U selecteert dit netwerk op Hallo moment van failover. Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als uw Azure Site Recovery-abonnement.

Meer informatie over de netwerktoewijzing in

* [Hoe tooconfigure logische netwerken in VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Hoe tooconfigure VM-netwerken en gateways in VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [Hoe tooconfigure en monitor virtuele netwerken in Azure](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a>PowerShell-vereisten
Zorg ervoor dat u Azure PowerShell gereed toogo hebt. Als u al van PowerShell gebruikmaakt, moet u tooupgrade tooversion 0.8.10 of hoger. Zie voor informatie over het instellen van PowerShell Hallo [tooinstall te leiden en configureer Azure PowerShell](/powershell/azureps-cmdlets-docs). Zodra u hebt ingesteld en geconfigureerd PowerShell, kunt u alle beschikbare Hallo-cmdlets voor Hallo service weergeven [hier](/powershell/azure/overview).

toolearn over tips waarmee u Hallo-cmdlets, zoals hoe parameterwaarden, in- en uitgangen doorgaans worden uitgevoerd in Azure PowerShell gebruiken kunt Zie Hallo [tooget slag met Azure-Cmdlets begeleiden](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Stap 1: Stel Hallo-abonnement
1. Van Azure powershell, aanmelding tooyour Azure-account: met behulp van de volgende cmdlets Hallo

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. Een lijst van uw abonnementen ophalen. Dit worden Hallo subscriptionIDs voor elk Hallo abonnementen vermeld. Noteer Hallo abonnements-id van het Hallo-abonnement waarmee u toocreate Hallo recovery services-kluis wenst

        Get-AzureRmSubscription
3. Hallo-abonnement in welke Hallo recovery services-kluis gemaakt is door de vermelding Hallo abonnements-ID toobe instellen

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>Stap 2: Maak een Recovery Services-kluis
1. Een resourcegroep maken in Azure Resource Manager als u nog niet hebt

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Een nieuwe Recovery Services-kluis maken en opslaan van Hallo ASR kluis object is gemaakt in een variabele (later worden gebruikt). U kunt ook Hallo ASR kluis post maken van het object met de cmdlet Get-AzureRMRecoveryServicesVault Hallo ophalen:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Stap 3: Hallo Recovery Services-kluis context instellen

Hallo kluis context instellen door te voeren Hallo onder opdracht.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Stap 4: Hello Azure Site Recovery Provider installeren
1. Maak een map door het uitvoeren van de volgende opdracht Hallo op Hallo-VMM-machine:

       New-Item c:\ASR -type directory
2. Hallo-bestanden met behulp van de provider Hallo gedownload door het uitvoeren van de volgende opdracht Hallo uitpakken

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. Hallo-provider met behulp van de volgende opdrachten Hallo installeren:

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   Wachten op Hallo installatie toofinish.
4. Hallo-server registreren in met behulp van de volgende opdracht Hallo Hallo-kluis:

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a>Stap 5: Een Azure storage-account maken

Als u geen Azure storage-account hebt, een geo-replicatie ingeschakeld-account maken in Hallo dezelfde geo als Hallo door het uitvoeren van de volgende opdracht Hallo-kluis:

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

Houd er rekening mee dat Hallo storage-account moet in dezelfde regio bevinden als de service Azure Site Recovery Hallo Hallo en worden gekoppeld aan hetzelfde abonnement Hallo.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Stap 6: Hello Azure Recovery Services-Agent installeren
1. Hello Azure Recovery Services agent op downloaden [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) en installeren op elke Hyper-V-host-server zich bevindt in VMM Hallo u clouds wilt tooprotect.
2. Voer Hallo opdracht op alle VMM-hosts te volgen:

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>Stap 7: Cloud configureren beveiligingsinstellingen
1. Maak een beleid voor replicatie tooAzure door het uitvoeren van de volgende opdracht Hallo:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. Een beveiligingscontainer door het uitvoeren van de volgende opdrachten Hallo ophalen:

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. Hallo beleid details tooa variabele Hallo-taak die is gemaakt met en houd Hallo beschrijvende naam krijgen:

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Koppeling van de beveiligingscontainer Hallo Hallo beginnen met Hallo replicatiebeleid:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. Nadat het Hallo-taak is voltooid, voert u Hallo volgende opdracht:

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. Nadat het Hallo taak zijn verwerkt, voert u Hallo volgende opdracht:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).

## <a name="step-8-configure-network-mapping"></a>Stap 8: Netwerktoewijzing configureren
Voordat u begint met de netwerktoewijzing controleert u of virtuele machines op de bronserver VMM Hallo verbonden tooa VM-netwerk. Daarnaast maakt u een of meer virtuele netwerken in Azure.

Meer informatie over hoe toocreate een virtueel netwerk met Azure Resource Manager en PowerShell in [een virtueel netwerk maken met een site-naar-site VPN-verbinding met Azure Resource Manager en PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

Houd er rekening mee dat meerdere netwerken voor virtuele Machine toegewezen tooa één Azure-netwerk kunnen worden. Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtual machine zich bevindt, wordt Hallo replica virtuele machine verbonden toothat Doelsubnet worden na failover. Als er geen Doelsubnet met een overeenkomende naam, wordt de Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk zijn.

1. de eerste opdracht Hallo opgehaald servers voor de huidige Azure Site Recovery-kluis Hallo. Hallo opdracht slaat Hallo Microsoft Azure Site Recovery-servers in Hallo $Servers matrixvariabele.

        $Servers = Get-AzureRmSiteRecoveryServer
2. de tweede opdracht Hallo ophalen Hallo een netwerk met site recovery voor de eerste server Hallo in Hallo $Servers matrix. Hallo opdracht slaat Hallo netwerken in Hallo $Networks variabele.

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. Hallo derde opdracht haalt virtuele Azure-netwerken en dat de waarde in Hallo $AzureVmNetworks variabele.

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. Hallo laatste cmdlet maakt een toewijzing tussen Hallo primaire netwerk en hello Azure virtuele machine. het primaire netwerk Hallo geeft Hallo cmdlet als Hallo eerste element van $Networks. Hallo cmdlet geeft een VM-netwerk als eerste element van $AzureVmNetworks Hallo.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>Stap 9: Beveiliging voor virtuele machines inschakelen
Nadat het Hallo-servers, clouds en netwerken correct zijn geconfigureerd, kunt u beveiliging voor virtuele machines in de cloud Hallo inschakelen.

 Let op Hallo volgende:

* Virtuele machines moeten voldoen aan de Azure-vereisten. Controleer deze in [vereisten en ondersteuning](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in Hallo planning guide.
* tooenable protection, Hallo-besturingssysteem en de schijfeigenschappen besturingssysteem moeten worden ingesteld voor Hallo virtuele machine. Wanneer u een virtuele machine in VMM met een virtuele machine-sjabloon maakt, kunt u Hallo-eigenschap instellen. U kunt deze eigenschappen voor de bestaande virtuele machines ook instellen op Hallo **algemene** en **hardwareconfiguratie** tabbladen van de eigenschappen van de virtuele machine Hallo. Als u deze eigenschappen niet ingesteld in VMM, moet u kunnen tooconfigure ze in hello Azure Site Recovery-portal.

1. tooenable beveiliging Hallo opdracht tooget hello beveiligingscontainer volgende uitvoeren:

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. Hallo beveiligde entiteit (VM) door het uitvoeren van de volgende opdracht Hallo ophalen:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. Hallo DR voor Hallo VM inschakelen door het uitvoeren van de volgende opdracht Hallo:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>Uw implementatie testen
tootest uw implementatie kunt u een test uitvoeren failover voor een enkele virtuele machine of een herstelplan dat bestaat uit meerdere virtuele machines maken en een test failover voor Hallo plan uitvoeren. Failover van de test wordt uw failover- en herstelmechanisme in een geïsoleerd netwerk gesimuleerd. Opmerking:

* Als u tooconnect toohello virtuele machine in Azure met extern bureaublad na failover Hallo wilt, moet u verbinding met extern bureaublad inschakelen op Hallo virtuele machine voordat u Hallo testfailover uitvoert.
* Na een failover gebruikt u een openbaar IP-adres tooconnect toohello virtuele machine in Azure met behulp van extern bureaublad. Als u toodo dit wilt, zorg ervoor dat u geen domeinbeleid hebt geïmplementeerd die verhinderen dat u verbinding maakt tooa virtuele machine via een openbaar adres.

Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).

### <a name="run-a-test-failover"></a>Een testfailover uitvoeren
- Start de testfailover Hallo door het uitvoeren van Hallo volgende opdracht:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>Een geplande failover uitvoeren
- Start Hallo geplande failover door het uitvoeren van de volgende opdracht Hallo:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>Een niet-geplande failover uitvoeren
- Start niet-geplande failover door het uitvoeren van de volgende opdracht Hallo Hallo:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <a name=monitor></a>Voor Monitoractiviteit
Gebruik hello opdrachten toomonitor Hallo activiteit te volgen. Houd er rekening mee dat u toowait Between-taken voor Hallo verwerking toofinish hebt.

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>Volgende stappen
[Lees meer](/powershell/module/azurerm.recoveryservices.backup/#recovery) over Azure Site Recovery met Azure Resource Manager PowerShell-cmdlets.
