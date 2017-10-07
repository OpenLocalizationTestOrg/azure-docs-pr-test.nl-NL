---
title: aaaReplicate Hyper-V-machines tooAzure in de klassieke portal Hallo met PowerShell | Microsoft Docs
description: Hallo replicatie van Hyper-V virtuele machines in VMM-clouds met Site Recovery en PowerShell in de klassieke portal Hallo automatiseren
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a>Hyper-V-machines tooAzure met PowerShell in de klassieke portal Hallo repliceren
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

Hallo artikel bevat vereisten voor Hallo scenario en ziet u hoe tooset van Site Recovery-kluis installeert Azure Site Recovery Provider op de bronserver VMM Hallo Hallo, Hallo-server registreren in de kluis hello, Azure storage-account toevoegen, hello Azure installeren Recovery Services-agent op Hyper-V-hostservers Configureer beveiligingsinstellingen voor VMM-clouds die wordt toegepast tooall beveiligde virtuele machines, en schakel vervolgens de beveiliging voor deze virtuele machines. Voltooien door failover toomake testen Hallo controleren of dat alles werkt zoals verwacht.

Als u problemen bij het instellen van dit scenario, stel uw vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.
>
>

## <a name="before-you-start"></a>Voordat u begint
Zorg ervoor dat u deze vereisten hebt voldaan:

### <a name="azure-prerequisites"></a>Vereisten voor Azure
* U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
* U moet een Azure storage-account toostore gerepliceerde gegevens. Hallo-account moet geo-replicatie is ingeschakeld. Deze moet in dezelfde regio als de Azure Site Recovery-kluis Hallo Hallo en worden gekoppeld aan hetzelfde abonnement Hallo. [Meer informatie over Azure storage](../storage/common/storage-introduction.md).
* U moet zorgen dat virtuele machines die u wilt dat tooprotect voldoen aan toomake [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

### <a name="vmm-prerequisites"></a>VMM-vereisten
* U moet de VMM-server waarop System Center 2012 R2.
* U moet ten minste één cloud op Hallo gewenste tooprotect VMM-server. Hallo cloud moet bevatten:
  * Een of meer VMM-hostgroepen.
  * Een of meer Hyper-V-hostservers of -clusters in elke hostgroep.
  * Een of meer virtuele machines op Hallo bron Hyper-V-server.

### <a name="hyper-v-prerequisites"></a>Hyper-V-vereisten
* Hallo Hyper-V-hostservers moeten ten minste draaien **Windows Server 2012** met Hyper-V-rol of **Microsoft Hyper-V Server 2012** en hebben Hallo nieuwste updates zijn geïnstalleerd.
* Als u Hyper-V in een cluster uitvoert, wordt die clusterbroker niet automatisch gemaakt als u een cluster op basis van een statisch IP-adres hebt. U moet tooconfigure hello clusterbroker handmatig. toodo dit door in Serverbeheer > Failoverclusterbeheer toohello cluster verbinding, klikt u op **functie configureren** en selecteer **Hyper-V Replica Broker** in Hallo **rol selecteren**scherm van de wizard maximale beschikbaarheid Hallo.
* Alle Hyper-V-hostserver of het cluster waarvoor u de toomanage beveiliging moet worden opgenomen in een VMM-cloud.

### <a name="network-mapping-prerequisites"></a>Vereisten voor netwerktoewijzing
Als u virtuele machines in Azure koppelingen van Netwerktoewijzingen tussen VM-netwerken op Hallo bron-VMM-server beveiligen en gericht op Azure-netwerken tooenable Hallo volgende:

* Alle machines die een failover op Hallo dezelfde netwerk verbinding kan maken van andere, ongeacht welk herstelplan ze tooeach.
* Als een netwerkgateway ingesteld op Hallo Azure-doelnetwerk is, kunnen virtuele machines verbinding tooother on-premises virtuele machines maken.
* Als u niet configureert netwerk alleen virtuele machines met failover in Hallo dezelfde toewijzing herstelplan kunnen tooconnect tooeach andere worden na failover tooAzure.

Als u wilt dat de netwerktoewijzing toodeploy moet u de volgende Hallo:

* Hallo virtuele machines die u wilt dat tooprotect op Hallo bron-VMM-server moet zijn verbonden tooa VM-netwerk. Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud.
* Een Azure-netwerk toowhich gerepliceerde virtuele machines verbinding kunnen maken na een failover. U selecteert dit netwerk op Hallo moment van failover. Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als uw Azure Site Recovery-abonnement.

### <a name="powershell-prerequisites"></a>PowerShell-vereisten
Zorg ervoor dat u Azure PowerShell gereed toogo hebt. Als u al van PowerShell gebruikmaakt, moet u tooupgrade tooversion 0.8.10 of hoger. Zie voor meer informatie over het instellen van PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs). Zodra u hebt ingesteld en geconfigureerd PowerShell, kunt u alle beschikbare Hallo-cmdlets voor Hallo service weergeven [hier](/powershell/azure/overview).

Zie toolearn over tips waarmee u Hallo-cmdlets, zoals hoe parameterwaarden, in- en uitgangen doorgaans worden uitgevoerd in Azure PowerShell gebruiken kunt [aan de slag met Azure-Cmdlets](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Stap 1: Stel Hallo-abonnement
Voer deze cmdlets in PowerShell:

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

Hallo-elementen in Hallo "haken" vervangen door uw specifieke gegevens.

## <a name="step-2-create-a-site-recovery-vault"></a>Stap 2: Een Site Recovery-kluis maken
Hallo-elementen in Hallo "haken" vervangen door uw specifieke gegevens in PowerShell en voer deze opdrachten:

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a>Stap 3: Een kluisregistratiesleutel genereren
Genereer een registratiesleutel in Hallo kluis. Nadat u hello Azure Site Recovery Provider downloaden en op Hallo VMM-server installeren, gebruikt u deze sleutel tooregister Hallo VMM-server in Hallo kluis.

1. Hallo kluis instellingenbestand ophalen en Hallo context instellen:

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. Hallo kluis context door het uitvoeren van de volgende opdrachten Hallo instellen:

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Stap 4: Hello Azure Site Recovery Provider installeren
1. Maak een map door het uitvoeren van de volgende opdracht Hallo op Hallo-VMM-machine:

   ```

   pushd C:\ASR\

   ```
2. Hallo-bestanden met behulp van de provider Hallo gedownload door het uitvoeren van de volgende opdracht Hallo uitpakken

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. Hallo-provider met behulp van de volgende opdrachten Hallo installeren:

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   Wachten op Hallo installatie toofinish.
4. Hallo-server registreren in met behulp van de volgende opdracht Hallo Hallo-kluis:

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a>Stap 5: Een Azure storage-account maken
Als u geen Azure storage-account hebt, kunt u een geo-replicatie ingeschakeld-account maken door het uitvoeren van de volgende opdracht Hallo:

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

Houd er rekening mee dat Hallo storage-account moet in dezelfde regio bevinden als de service Azure Site Recovery Hallo Hallo en worden gekoppeld aan hetzelfde abonnement Hallo.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Stap 6: Hello Azure Recovery Services-Agent installeren
Hello Azure-portal installeren hello Azure Recovery Services-agent op elke Hyper-V-hostserver die zich in de VMM-clouds hello wilt u tooprotect.

Voer Hallo opdracht op alle VMM-hosts te volgen:

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a>Stap 7: Cloud configureren beveiligingsinstellingen
1. Maak een cloud beveiliging profiel tooAzure door het uitvoeren van de volgende opdracht Hallo:

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. Een beveiligingscontainer door het uitvoeren van de volgende opdrachten Hallo ophalen:

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. Koppeling van de beveiligingscontainer Hallo Hallo beginnen met Hallo cloud:

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. Nadat het Hallo-taak is voltooid, voert u Hallo volgende opdracht:

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. Nadat het Hallo taak zijn verwerkt, voert u Hallo volgende opdracht:

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



Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).

## <a name="step-8-configure-network-mapping"></a>Stap 8: Netwerktoewijzing configureren
Voordat u begint met de netwerktoewijzing controleert u of virtuele machines op de bronserver VMM Hallo verbonden tooa VM-netwerk. Daarnaast maakt u een of meer virtuele netwerken in Azure. Houd er rekening mee dat meerdere VM-netwerken kunnen bestaan uit toegewezen tooa één Azure-netwerk.

Houd er rekening mee dat als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtual machine zich bevindt, wordt Hallo replica virtuele machine na een failover worden verbonden toothat Doelsubnet. Als er geen een Doelsubnet met een overeenkomende naam beschikbaar is, worden Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk.

de eerste opdracht Hallo opgehaald servers voor de huidige Azure Site Recovery-kluis Hallo. Hallo opdracht slaat Hallo Microsoft Azure Site Recovery-servers in Hallo $Servers matrixvariabele.

    $Servers = Get-AzureSiteRecoveryServer


de tweede opdracht Hallo ophalen Hallo een netwerk met site recovery voor de eerste server Hallo in Hallo $Servers matrix. Hallo opdracht slaat Hallo netwerken in Hallo $Networks variabele.

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

Hallo derde opdracht uw Azure-abonnementen opgehaald met behulp van de cmdlet Get-AzureSubscription hello en slaat deze waarde op in Hallo $Subscriptions variabele.

    $Subscriptions = Get-AzureSubscription



Hallo vierde opdracht haalt virtuele netwerken in Azure met behulp van de cmdlet Get-AzureVNetSite hello en dat de waarde in Hallo $AzureVmNetworks variabele.

    $AzureVmNetworks = Get-AzureVNetSite



Hallo laatste cmdlet maakt een toewijzing tussen Hallo primaire netwerk en hello Azure virtuele machine. het primaire netwerk Hallo geeft Hallo cmdlet als Hallo eerste element van $Networks. Hallo cmdlet geeft een VM-netwerk als eerste element van $AzureVmNetworks Hallo met behulp van de-ID. Hallo-opdracht bevat uw Azure-abonnement-ID.

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a>Stap 9: Beveiliging voor virtuele machines inschakelen
Nadat de servers, clouds en netwerken correct zijn geconfigureerd, kunt u beveiliging voor virtuele machines in de cloud Hallo inschakelen. Let op Hallo volgende:

Virtuele machines moeten voldoen aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

tooenable beveiliging Hallo-besturingssysteem en de schijfeigenschappen besturingssysteem moeten worden ingesteld voor Hallo virtuele machine. Wanneer u een virtuele machine in VMM met een virtuele machine-sjabloon maakt, kunt u Hallo-eigenschap instellen. U kunt deze eigenschappen voor de bestaande virtuele machines ook instellen op Hallo **algemene** en **hardwareconfiguratie** tabbladen van de eigenschappen van de virtuele machine Hallo. Als u deze eigenschappen niet ingesteld in VMM, moet u kunnen tooconfigure ze in hello Azure Site Recovery-portal.

1. tooenable beveiliging Hallo opdracht tooget hello beveiligingscontainer volgende uitvoeren:

     $ProtectionContainer = get-AzureSiteRecoveryProtectionContainer-$CloudName naam
2. Hallo beveiligde entiteit (VM) door het uitvoeren van de volgende opdracht Hallo ophalen:

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. Hallo DR voor Hallo VM inschakelen door het uitvoeren van de volgende opdracht Hallo:

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a>Uw implementatie testen
tootest plannen voor uw implementatie kunt u een testfailover voor één virtuele machine uitvoeren of maken van een herstelplan dat bestaat uit meerdere virtuele machines en een testfailover voor Hallo uitvoeren. Met een testfailover wordt uw failover- en herstelmechanisme in een geïsoleerd netwerk gesimuleerd. Opmerking:

* Als u tooconnect toohello virtuele machine in Azure met extern bureaublad na een failover Hallo wilt, moet u verbinding met extern bureaublad inschakelen op Hallo virtuele machine voordat u Hallo testfailover uitvoeren.
* Na een failover gebruikt u een openbaar IP-adres tooconnect toohello virtuele machine in Azure met behulp van extern bureaublad. Als u toodo dit wilt, zorg ervoor dat u geen domeinbeleid hebt geïmplementeerd die verhinderen dat u verbinding maakt tooa virtuele machine via een openbaar adres.

Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).

### <a name="create-a-recovery-plan"></a>Een herstelplan maken
1. Maken van een XML-bestand als een sjabloon voor het herstelplan met behulp van onderstaande Hallo-gegevens en deze opslaan als 'C:\RPTemplatePath.xml'.
2. Hallo RecoveryPlan knooppunt Id, naam, PrimaryServerId en SecondaryServerId wijzigen.
3. Hallo ProtectionEntity knooppunt PrimaryProtectionEntityId (vmid uit VMM) wijzigen.
4. U kunt meer virtuele machines toevoegen door meer ProtectionEntity knooppunten toe te voegen.

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. Hallo-gegevens in de sjabloon Hallo invullen:

        $TemplatePath = "C:\RPTemplatePath.xml";



1. Hallo RecoveryPlan maken:

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a>Een testfailover uitvoeren
1. Hallo RecoveryPlan object ophalen door het uitvoeren van de volgende opdracht Hallo:

     $RPObject = get-AzureSiteRecoveryRecoveryPlan-naam $RPName;
2. Start de testfailover Hallo door het uitvoeren van Hallo volgende opdracht:

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


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
[Lees meer](/powershell/azure/overview) over Azure Site Recovery PowerShell-cmdlets. </a>.
