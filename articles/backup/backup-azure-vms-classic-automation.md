---
title: aaaDeploy en beheren van back-up voor virtuele Azure-machines met behulp van PowerShell | Microsoft Docs
description: Meer informatie over hoe toodeploy en beheren van Azure Backup met behulp van PowerShell.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a>Gebruik AzureRM.Backup cmdlets tooback van virtuele machines
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-vms-automation.md)
> * [Klassiek](backup-azure-vms-classic-automation.md)
>
>

Dit artikel ziet u hoe toouse Azure PowerShell voor back-up en herstel van virtuele Azure-machines. In Azure zijn twee verschillende implementatiemodellen beschikbaar voor het maken van en werken met resources: Resource Manager en het klassieke model. In dit artikel bevat informatie over met behulp van Hallo Classic deployment model tooback up gegevens tooa Backup-kluis. Als u niet een back-upkluis in uw abonnement hebt gemaakt, raadpleegt u Hallo Resource Manager-versie van dit artikel [gebruik AzureRM.RecoveryServices.Backup cmdlets tooback van virtuele machines](backup-azure-vms-automation.md). Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

> [!IMPORTANT]
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017. **Per 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>

## <a name="concepts"></a>Concepten
In dit artikel bevat informatie die specifieke toohello PowerShell-cmdlets gebruikt tooback van virtuele machines. Raadpleeg voor inleidende informatie over het beveiligen van Azure Virtual machines [plannen van uw back-infrastructuur van de virtuele machine in Azure](backup-azure-vms-introduction.md).

> [!NOTE]
> Lees voordat u begint, Hallo [vereisten](backup-azure-vms-prepare.md) vereist toowork met Azure Backup en Hallo [beperkingen](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) van Hallo huidige VM-back-upoplossing.
>
>

toouse PowerShell nemen effectief, een ogenblik toounderstand Hallo hiërarchie van objecten en waar toostart.

![Objecthiërarchie](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

Hallo twee belangrijkste stromen u beveiliging inschakelt voor een virtuele machine en herstellen van gegevens vanaf een herstelpunt. Hallo van dit artikel worden toohelp u meer bijzonder geschikt voor het werken met Hallo PowerShell-cmdlets tooenable deze twee scenario's.

## <a name="setup-and-registration"></a>De installatie en registratie
toobegin:

1. [Download de meest recente PowerShell](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)
2. Zoeken hello Azure back-up PowerShell-cmdlets zijn beschikbaar op Hallo volgende opdracht te typen:

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

Hallo kunnen volgende installatie en registratietaken worden geautomatiseerd met PowerShell:

* Een back-upkluis maken
* Hallo VMs registreren met hello Azure Backup-service

### <a name="create-a-backup-vault"></a>Een back-upkluis maken
> [!WARNING]
> Voor klanten die gebruikmaken van Azure Backup voor Hallo eerst, moet u tooregister hello Azure Backup-provider toobe gebruikt met uw abonnement. Dit kan worden gedaan door het uitvoeren van de volgende opdracht Hallo: Register AzureRmResourceProvider - ProviderNamespace 'Microsoft.Backup'
>
>

U kunt een nieuwe back-upkluis met Hallo maken **nieuw AzureRmBackupVault** cmdlet. Hallo back-upkluis is een ARM-bron, dus u tooplace moet deze binnen een resourcegroep. Voer Hallo volgende opdrachten in een verhoogde Azure PowerShell-console:

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

U kunt een lijst met alle Hallo back-upkluizen krijgen in een bepaald abonnement met behulp van Hallo **Get-AzureRmBackupVault** cmdlet.

> [!NOTE]
> Dit is handig toostore Hallo back-upkluis-object in een variabele. Hallo kluis object is nodig als invoer voor veel Azure Backup-cmdlets.
>
>

### <a name="registering-hello-vms"></a>Hallo VMs registreren
de eerste stap Hallo naar het configureren van back-up met Azure Backup is tooregister uw computer of virtuele machine met een Azure Backup-kluis. Hallo **registreren AzureRmBackupContainer** cmdlet Hallo invoergegevens van een virtuele machine van Azure IaaS neemt en registreert deze bij Hallo opgegeven kluis. Hallo registerbewerking hello Azure virtuele machine koppelt aan Hallo back-upkluis en houdt Hallo VM levenscyclus Hallo back-up.

Registreren van uw virtuele machine met hello Azure Backup-service, maakt een site op het hoogste containerobject. Een container bevat doorgaans meerdere items die u kunnen een back-up, maar in geval van virtuele machines Hallo zal er slechts één back-item voor Hallo-container.

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>Back-ups maken van virtuele Azure-machines
### <a name="create-a-protection-policy"></a>Een beveiligingsbeleid maken
Het is niet verplicht toocreate een nieuwe beveiligingsgroep beleid toostart back-up van uw virtuele machines. Hallo-kluis wordt geleverd met een 'standaardbeleid' die kan worden gebruikt tooquickly inschakelen van de beveiliging en later bewerkt met de juiste details Hallo. U kunt een lijst met Hallo beleidsregels beschikbaar in de kluis Hallo opvragen met Hallo **Get-AzureRmBackupProtectionPolicy** cmdlet:

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> Hallo tijdzone van Hallo BackupTime veld in PowerShell is UTC. Wanneer de back-uptijd Hallo in hello Azure-portal wordt weergegeven, is Hallo tijdzone uitgelijnde tooyour lokaal systeem samen met de Hallo UTC-offset.
>
>

Er is een back-upbeleid gekoppeld aan ten minste één bewaarbeleid. Hallo bewaarbeleid definieert hoe lang een herstelpunt wordt gehouden met Azure Backup. Hallo **nieuw AzureRmBackupRetentionPolicy** cmdlet maakt een PowerShell-objecten die informatie over bewaarbeleid bevatten. Deze bewaren beleid-objecten worden gebruikt als invoer toohello *nieuw AzureRmBackupProtectionPolicy* cmdlet, of rechtstreeks met de Hallo *inschakelen AzureRmBackupProtection* cmdlet.

Een back-upbeleid definieert wanneer en hoe vaak hello back-up van een item wordt uitgevoerd. Hallo **nieuw AzureRmBackupProtectionPolicy** cmdlet maakt een PowerShell-object dat back-upbeleid informatie bevat. Hallo back-beleid wordt gebruikt als een invoer toohello *inschakelen AzureRmBackupProtection* cmdlet.

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>Beveiliging inschakelen
Beveiliging in te schakelen moet u twee objecten - hello Item en Hallo beleid en beide nodig toobelong toohello dezelfde kluis. Als Hallo beleid is gekoppeld aan Hallo-item, wordt Hallo back-werkstroom starten op Hallo gedefinieerde planning.

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>Eerste back-up
back-upschema Hallo zorgt voor de volgende back-ups Hallo Hallo incrementele kopie en volledige initiële kopie van de Hallo voor Hallo-item te doen. Echter, als u wilt dat tooforce Hallo eerste back-toohappen op een bepaald tijdstip of zelfs onmiddellijk vervolgens gebruiken Hallo **back-up AzureRmBackupItem** cmdlet:

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> Hallo tijdzone Hallo StartTime en EndTime velden wordt weergegeven in PowerShell is UTC. Wanneer Hallo vergelijkbare gegevens in hello Azure-portal wordt weergegeven, is Hallo tijdzone uitgelijnde tooyour lokale systeemklok.
>
>

### <a name="monitoring-a-backup-job"></a>Bewaking van een back-uptaak
De meeste langlopende bewerkingen in Azure Backup gemodelleerd zijn als een taak. Dit maakt het eenvoudig tootrack uitgevoerd zonder tookeep hello Azure portal openen te allen tijde.

tooget hello laatste status van een taak wordt uitgevoerd, gebruik Hallo **Get-AzureRmBackupJob** cmdlet.

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

In plaats van deze taken voor voltooiing - dit is niet nodig, aanvullende code - polling is eenvoudiger toouse hello **wacht AzureRmBackupJob** cmdlet. Wanneer gebruikt in een script, wordt Hallo cmdlet Hallo uitvoering onderbroken totdat Hallo-taak is voltooid of Hallo opgegeven time-outwaarde is bereikt.

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>Een Azure-virtuele machine herstellen
In de volgorde toorestore back-upgegevens, moet u tooidentify Hallo back-up Item en Hallo herstelpunt die Hallo punt in tijd gegevens bevat. Deze informatie is opgegeven toohello terugzetten AzureRmBackupItem cmdlet tooinitiate terugzetten van gegevens uit Hallo kluis toohello van klant-account.

### <a name="select-hello-vm"></a>Hallo VM selecteren
tooget hello PowerShell-object waarmee Hallo juiste back-Item, u moet toostart van Hallo Container in Hallo kluis en boven naar beneden objecthiërarchie werken. tooselect Hallo-container die virtuele machine, gebruik Hallo Hallo vertegenwoordigt **Get-AzureRmBackupContainer** cmdlet en doorsluizen die toohello **Get-AzureRmBackupItem** cmdlet.

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>Kies een herstelpunt
U kunt nu alle Hallo herstelpunten voor de back-item Hallo Hallo met aanbieden **Get-AzureRmBackupRecoveryPoint** cmdlet, en kies Hallo herstel punt toorestore. Meestal gebruikers Hallo meest recente Kies *AppConsistent* wijst u in de lijst Hallo.

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

Hallo variabele ```$rp``` is een matrix van herstelpunten voor Hallo back-item, in omgekeerde volgorde gesorteerd tijd geselecteerd - de meest recente herstelpunt Hallo bij index 0 is. Gebruik standaard PowerShell matrix toopick Hallo herstelpunt te indexeren. Bijvoorbeeld: ```$rp[0]``` Hallo meest recente herstelpunt wordt geselecteerd.

### <a name="restoring-disks"></a>Herstellen van schijven
Er is een belangrijke verschil tussen Hallo herstelbewerkingen gedaan via hello Azure-portal en via Azure PowerShell. Met PowerShell stopt Hallo restore-bewerking op het Hallo-schijven en configuratie-informatie herstellen vanaf herstelpunt Hallo. Er wordt een virtuele machine niet gemaakt.

> [!WARNING]
> Hallo terugzetten AzureRmBackupItem maakt een virtuele machine niet. Herstelt alleen Hallo schijven toohello storage-account opgegeven. Dit is niet hetzelfde gedrag treedt in hello Azure-portal Hallo.
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

U krijgt Hallo details van Hallo herstelbewerking met Hallo **Get-AzureRmBackupJobDetails** cmdlet wanneer Hallo hersteltaak is voltooid. Hallo *ErrorDetails* eigenschap heeft Hallo informatie nodig toorebuild Hallo VM.

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a>Hallo VM bouwen
Gebouw Hallo VM buiten Hallo hersteld schijven kan worden gedaan met behulp van de oudere Azure Service Management PowerShell-cmdlets Hallo Hallo van nieuwe Azure Resource Manager-sjablonen of zelfs met hello Azure-portal. In een kort voorbeeld we tonen hoe tooget er met hello Azure Service Management-cmdlets.

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

Voor meer informatie over het lezen van toobuild een virtuele machine van de schijven Hallo hersteld, over Hallo cmdlets volgen:

* [Voeg AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [Nieuwe AzureVMConfig](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [Nieuwe-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>Codevoorbeelden
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a>1. Hallo-voltooiingsstatus van onderliggende taken ophalen
tootrack hello voltooiingsstatus van afzonderlijke onderliggende taken, kunt u Hallo **Get-AzureRmBackupJobDetails** cmdlet:

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2. Maak een rapport dagelijks/wekelijks back-uptaken
Beheerders willen doorgaans tooknow welke back-uptaken die worden uitgevoerd in Hallo afgelopen 24 uur Hallo status van deze back-uptaken. Bovendien Hallo en de hoeveelheid gegevens overgedragen biedt beheerders een tooestimate manier hun maandelijkse gebruiksgegevens van de gegevens. Hallo onderstaande script Hallo ruwe gegevens ophaalt uit hello Azure Backup-service en Hallo gegevens weergegeven in Hallo PowerShell-console.

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

Als u tooadd mogelijkheden toothis rapportuitvoer voor grafieken wilt, leren van Hallo TechNet-blogbericht [voor grafieken met PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>Volgende stappen
Als u liever met behulp van PowerShell tooengage met uw Azure-resources, bekijk Hallo PowerShell artikel voor het beveiligen van Windows Server [implementeren en beheren van back-up voor Windows Server](backup-client-automation-classic.md). Er is ook een PowerShell-artikel voor het beheren van back-ups van DPM [implementeren en beheren van Backup voor DPM](backup-dpm-automation-classic.md). Hebben beide van deze artikelen een versie voor implementaties van Resource Manager, evenals klassieke implementaties.
