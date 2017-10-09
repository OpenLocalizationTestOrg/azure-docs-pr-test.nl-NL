---
title: aaaReplicate Hyper-V-machines in VMM tooa secundaire site met PowerShell (Azure Resource Manager) | Microsoft Docs
description: Hierin wordt beschreven hoe toodeploy Azure Site Recovery tooorchestrate replicatie, failovers en herstel van Hyper-V-machines in VMM clouds tooa secundaire VMM-site met behulp van PowerShell (Resource Manager)
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a>Hyper-V virtuele machines in VMM-clouds tooa secundaire VMM-site met behulp van PowerShell (Resource Manager) repliceren
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Klassieke portal](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Welkom tooAzure Site Recovery. Gebruik dit artikel als u wilt dat tooreplicate lokale Hyper-V virtuele machines die worden beheerd in System Center Virtual Machine Manager (VMM) clouds tooa secundaire site.

Dit artikel laat zien hoe toouse PowerShell tooautomate algemene taken moet u tooperform bij het instellen van Azure Site Recovery tooreplicate Hyper-V virtuele machines in System Center VMM-clouds tooSystem Center VMM-clouds in de secundaire site.

Hallo artikel bevat vereisten voor Hallo scenario en laat zien u

* Hoe tooset van een Recovery Services-kluis
* Hello Azure Site Recovery Provider installeren op de bronserver VMM Hallo en Hallo doel-VMM-server
* Hallo VMM server (s) in Hallo kluis registreren
* Replicatiebeleid voor Hallo VMM-Cloud te configureren. Hallo replicatie-instellingen in het Hallo-beleid worden toegepast tooall beveiligde virtuele machines
* Schakel de beveiliging voor Hallo virtuele machines.
* Hallo testfailover van virtuele machines afzonderlijk of als onderdeel van een herstel plan toomake controleren of alles werkt zoals verwacht.
* Voer een geplande of een niet-geplande failover van virtuele machines afzonderlijk of als onderdeel van een plan toomake voor herstel controleren of dat alles werkt zoals verwacht.

Als u problemen bij het instellen van dit scenario, stel uw vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure heeft twee verschillende [implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) voor het maken van en werken met resources: Azure Resource Manager en het klassieke model. Azure heeft bovendien twee portals: de klassieke Azure-portal die ondersteuning biedt voor het klassieke implementatiemodel Hallo Hallo en hello Azure-portal met ondersteuning voor beide implementatiemodellen. In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.
>
>

## <a name="on-premises-prerequisites"></a>Vereisten voor on-premises
Dit is wat u nodig hebt in Hallo primaire en secundaire on-premises sites toodeploy van dit scenario:

| **Vereisten** | **Details** |
| --- | --- |
| **VMM** |Het is raadzaam om de implementatie van een VMM-beheerserver in Hallo primaire site en een VMM-server op Hallo secundaire site.<br/><br/> U kunt ook [repliceren tussen clouds op één VMM-server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). toodo dit moet u ten minste twee clouds die zijn geconfigureerd op Hallo VMM-server.<br/><br/> VMM-servers waarop ten minste System Center 2012 SP1 met de nieuwste updates Hallo.<br/><br/> Elke VMM-server moet op een of meer clouds zijn geconfigureerd en alle clouds moeten Hallo Hyper-V capaciteitsprofiel instellen. <br/><br/>Clouds moeten een of meer VMM-hostgroepen bevatten.<br/><br/>Meer informatie over het instellen van VMM-clouds in [configureren Hallo VMM fabric cloud](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), en [overzicht: privéclouds maken met System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).<br/><br/> VMM-servers moeten toegang tot internet hebben. |
| **Hyper-V** |Hyper-V-servers moeten ten minste draaien op Windows Server 2012 met Hallo Hyper-V-rol en hebben Hallo nieuwste updates zijn geïnstalleerd.<br/><br/> Een Hyper-V-server moet een of meer virtuele machines bevatten.<br/><br/>  Hyper-V-hostservers moeten zich in hostgroepen in Hallo primaire en secundaire VMM-clouds.<br/><br/> Als u Hyper-V in een cluster op Windows Server 2012 R2 moet u eerst installeren [2961977 bijwerken](https://support.microsoft.com/kb/2961977)<br/><br/> Als u werkt met Hyper-V in een cluster op Windows Server 2012-opmerking die clusterbroker niet automatisch gemaakt als u een statische IP-adressen gebaseerde cluster hebt. U moet tooconfigure hello clusterbroker handmatig. [Lees meer](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Provider** |Tijdens de implementatie van Site Recovery kunt u hello Azure Site Recovery Provider installeren op VMM-servers. Hallo Provider communiceert met Site Recovery via HTTPS 443 tooorchestrate replicatie. Gegevensreplicatie plaatsvindt tussen Hallo primaire en secundaire servers voor Hyper-V via LAN hello of een VPN-verbinding.<br/><br/> Hallo Provider die op Hallo VMM-server wordt uitgevoerd moet toegang tot toothese URL's: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.<br/><br/> Bovendien toestaan firewall communicatie van Hallo VMM-servers toohello [Azure datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653) en Hallo HTTPS (443)-protocol toe te staan. |

### <a name="network-mapping-prerequisites"></a>Vereisten voor netwerktoewijzing
Koppelingen van Netwerktoewijzingen tussen VMM VM-netwerken op Hallo primaire en secundaire VMM-servers:

* Replica-VM optimaal op secundaire Hyper-V-hosts plaatsen na een failover.
* Verbinding met het maken van replica VMs tooappropriate VM-netwerken.
* Als u geen netwerk configureert toewijzing replica VMs niet verbonden tooany netwerk na een failover.
* Als u wilt dat tooset netwerk is toewijzen tijdens het siteherstel implementatie hier wat u nodig hebt:

  * Zorg ervoor dat virtuele machines op Hallo bron Hyper-V-hostserver verbonden tooa VMM VM-netwerk. Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud.
  * Controleer of Hallo secundaire cloud die u voor herstel heeft een bijbehorende VM-netwerk is geconfigureerd. Deze VM-netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo secundaire cloud.

Meer informatie over het configureren van netwerken in VMM in Hallo hieronder artikelen

* [Hoe tooconfigure logische netwerken in VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Hoe tooconfigure VM-netwerken en gateways in VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)

[Meer informatie](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) over hoe netwerktoewijzing werkt.

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
1. Een Azure Resource Manager-resourcegroep maken als u nog niet hebt

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Een nieuwe Recovery Services-kluis maken en opslaan van Hallo ASR kluis object is gemaakt in een variabele (later worden gebruikt). U kunt ook Hallo ASR kluis post maken van het object met de cmdlet Get-AzureRMRecoveryServicesVault Hallo ophalen:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Stap 3: Hallo Recovery Services-kluis context instellen
1. Als u een kluis hebt gemaakt hebt, uitgevoerd Hallo onderstaande opdracht tooget Hallo kluis.

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. Hallo kluis context instellen door te voeren Hallo onder opdracht.

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

## <a name="step-5-create-and-associate-a-replication-policy"></a>Stap 5: Maken en koppelen van een beleid voor wachtwoordreplicatie
1. Maak een Hyper-V 2012 R2 replicatie-beleid door het uitvoeren van de volgende opdracht Hallo:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > Hallo VMM-cloud Hyper-V-hosts met verschillende versies van Windows Server (zoals vermeld in de Hyper-V-vereisten Hallo) kan bevatten, maar Hallo replicatiebeleid specifieke versie van het besturingssysteem is. Als u andere hosts die worden uitgevoerd op verschillende besturingssysteemversies hebt, maakt u afzonderlijke replicatiegroepen beleid voor elk type van de versie van het besturingssysteem. Voor bijvoorbeeld: als u vijf hosts die worden uitgevoerd op Windows-Servers 2012 en drie op Windows Server 2012 R2 hebt, maakt u twee replicatie beleidsregels: één voor elk type besturingssysteemversies.

1. Hallo primaire beveiligingscontainer (primaire VMM-Cloud) en herstel de beveiligingscontainer (herstelserver VMM-Cloud) door het uitvoeren van de volgende opdrachten Hallo ophalen:

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. Hallo-beleid die u hebt gemaakt in stap 1 ophalen Hallo beschrijvende naam van het Hallo-beleid

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Hallo koppeling van Hallo beveiligingscontainer (VMM-Cloud) beginnen met het replicatiebeleid Hallo:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. Wachten op Hallo beleid koppeling taak toocomplete. U kunt controleren als Hallo-taak is voltooid met behulp van de volgende PowerShell-codefragment Hallo.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   Nadat het Hallo taak zijn verwerkt, voert u Hallo volgende opdracht:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).

## <a name="step-6-configure-network-mapping"></a>Stap 6: Netwerktoewijzing configureren
1. de eerste opdracht Hallo opgehaald servers voor de huidige Azure Site Recovery-kluis Hallo. Hallo opdracht slaat Hallo Microsoft Azure Site Recovery-servers in Hallo $Servers matrixvariabele.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Hallo hieronder opdrachten ophalen Hallo site recovery-netwerk voor Hallo bron-VMM-server en Hallo doel-VMM-server.

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > Hallo bron-VMM-server kan worden Hallo eerste of tweede matrix van één in Hallo servers Hallo. Hallo-namen van Hallo VMM-servers controleren en Hallo netwerken op de juiste wijze ophalen


1. Hallo laatste cmdlet een toewijzing gemaakt tussen het primaire netwerk Hallo en Hallo herstel. Hallo cmdlet geeft Hallo primaire netwerk als eerste element van $PrimaryNetworks en Hallo herstel netwerk als het eerste element van $RecoveryNetworks Hallo Hallo.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>Stap 7: De toewijzing van opslag configureren
1. Hallo onder opdracht ophalen Hallo lijst met opslagclassificaties in $storageclassifications-variabele.

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. Hallo hieronder opdrachten Hallo bron classificatie in de variabele $SourceClassificaion en doel classificatie in $TargetClassification-variabele ophalen.

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > Hallo-bron en doel classificaties kunnen elk element in Hallo matrix zijn. Raadpleeg toohello uitvoer van Hallo onderstaande opdracht toofigure Hallo index van de bron en doel classificaties in $storageclassifications matrix.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object - eigenschap FriendlyName, Id | Tabel opmaken


1. Hallo hieronder cmdlet een toewijzing gemaakt tussen Hallo bron classificatie en Hallo doel classificatie.

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>Stap 8: Beveiliging voor virtuele machines inschakelen
Nadat het Hallo-servers, clouds en netwerken correct zijn geconfigureerd, kunt u beveiliging voor virtuele machines in de cloud Hallo inschakelen.

1. tooenable beveiliging Hallo opdracht tooget hello beveiligingscontainer volgende uitvoeren:

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. Hallo beveiligde entiteit (VM) door het uitvoeren van de volgende opdracht Hallo ophalen:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. Replicatie inschakelen voor Hallo VM door het uitvoeren van de volgende opdracht Hallo:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>Uw implementatie testen
tootest plannen voor uw implementatie kunt u een testfailover voor één virtuele machine uitvoeren of maken van een herstelplan dat bestaat uit meerdere virtuele machines en een testfailover voor Hallo uitvoeren. Met een testfailover wordt uw failover- en herstelmechanisme in een geïsoleerd netwerk gesimuleerd.

> [!NOTE]
> U kunt een herstelplan maken voor uw toepassing in Azure-portal.
>
>

Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).

### <a name="run-a-test-failover"></a>Een testfailover uitvoeren
1. Hallo hieronder cmdlets tooget Hallo VM-netwerk toowhich die u uw virtuele machines naar tootest failover wilt uitvoeren.

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. Voer een testfailover uitgevoerd van een virtuele machine door Hallo volgende te doen:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. Voer een testfailover uitgevoerd van een herstelplan door Hallo volgende te doen:

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>Een geplande failover uitvoeren
1. Voer een geplande failover van een virtuele machine door Hallo volgende te doen:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. Voer een geplande failover van een herstelplan door Hallo volgende te doen:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>Een niet-geplande failover uitvoeren
1. Voer een niet-geplande failover van een virtuele machine door Hallo volgende te doen:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2. Voer een niet-geplande failover van een herstelplan door Hallo volgende te doen:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

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
