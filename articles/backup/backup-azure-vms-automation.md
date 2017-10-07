---
title: "aaaDeploy en beheren van back-ups voor Resource Manager geïmplementeerde VM's met behulp van PowerShell | Microsoft Docs"
description: "Gebruik PowerShell toodeploy en back-ups in Azure voor Resource Manager geïmplementeerde VM's beheren"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a>Gebruik AzureRM.RecoveryServices.Backup cmdlets tooback van virtuele machines
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-vms-automation.md)
> * [Klassiek](backup-azure-vms-classic-automation.md)
>
>

Dit artikel laat zien hoe toouse Azure PowerShell-cmdlets tooback up en herstel Azure een virtuele machine (VM) van een Recovery Services-kluis. Een Recovery Services-kluis is een Azure Resource Manager-resource en gebruikte tooprotect gegevens en activa in Azure Backup- en Azure Site Recovery services. U kunt een Recovery Services-kluis tooprotect Azure Service Manager geïmplementeerde VM's en Azure Resource Manager geïmplementeerde VM's gebruiken.

> [!NOTE]
> Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel is voor gebruik met virtuele machines die zijn gemaakt met behulp van Hallo Resource Manager-model.
>
>

In dit artikel leert u met behulp van PowerShell tooprotect een virtuele machine en gegevens terugzetten vanaf een herstelpunt.

## <a name="concepts"></a>Concepten
Als u niet bekend met hello Azure Backup-service voor een overzicht van service Hallo bent, Bekijk [wat is Azure Backup?](backup-introduction-to-azure-backup.md) Voordat u begint, zorg ervoor dat hebben betrekking op Hallo essentials over Hallo vereisten nodig toowork met Azure Backup en beperkingen van Hallo huidige VM-back-upoplossing Hallo.

toouse PowerShell effectief is noodzakelijk toounderstand Hallo hiërarchie van objecten en waar toostart.

![Recovery Services-objecthiërarchie](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

tooview hello AzureRm.RecoveryServices.Backup PowerShell-cmdlet-verwijzing, Zie Hallo [Azure Backup - Cmdlets voor Recovery Services](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure-bibliotheek.

## <a name="setup-and-registration"></a>De installatie en registratie
toobegin:

1. [Download de nieuwste versie Hallo van PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (Hallo minimaal vereiste versie is: 1.4.0)
2. Zoeken hello Azure back-up PowerShell-cmdlets zijn beschikbaar op Hallo volgende opdracht te typen:

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


Hallo na taken kan worden geautomatiseerd met PowerShell:

* Een Recovery Services-kluis maken
* Back-ups maken van Azure-VM's
* Een back-uptaak wordt geactiveerd
* Een back-uptaak bewaken
* Een Azure-virtuele machine herstellen

## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken
volgende stappen uit Hallo leiden u bij het maken van een Recovery Services-kluis. Een Recovery Services-kluis is anders dan een back-upkluis.

1. Als u van Azure Backup voor Hallo eerst gebruikmaakt, moet u Hallo  **[registreren AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  cmdlet tooregister hello Azure Recovery Service provider met uw abonnement.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hallo Recovery Services-kluis is een Resource Manager-bron, dus u tooplace moet deze binnen een resourcegroep. U kunt een bestaande resourcegroep gebruiken of een resourcegroep maken met de Hallo  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet. Bij het maken van een resourcegroep Hallo naam en locatie voor resourcegroep Hallo opgeven.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Gebruik Hallo  **[nieuw AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  cmdlet toocreate Hallo Recovery Services-kluis. Zorg ervoor dat toospecify dezelfde locatie voor de kluis Hallo Hallo werd gebruikt voor de resourcegroep Hallo.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Geef een Hallo van opslag redundantie toouse; u kunt [lokaal redundante opslag (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) of [geografisch redundante opslag (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Hallo volgende voorbeeld ziet Hallo BackupStorageRedundancy - optie voor testvault tooGeoRedundant is ingesteld.

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > Veel Azure Backup-cmdlets vereisen Hallo Recovery Services-kluis object als invoer. Daarom is het handige toostore Hallo back-up Recovery Services-kluis object in een variabele.
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a>Hallo-kluizen in een abonnement weergeven
Gebruik  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview Hallo lijst met alle kluizen in het huidige abonnement Hallo. U kunt deze opdracht toocheck dat een nieuwe kluis is gemaakt of toosee Hallo beschikbaar kluizen in Hallo abonnement gebruiken.

Hallo-opdracht Get-AzureRmRecoveryServicesVault tooview alle kluizen in Hallo abonnement uitgevoerd. Hallo wordt volgende voorbeeld weergegeven voor elke kluis Hallo-informatie.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="back-up-azure-vms"></a>Back-ups maken van Azure-VM's
Gebruik een Recovery Services-kluis tooprotect uw virtuele machines. Voordat u Hallo beveiliging toepast, Hallo kluis context (Hallo type gegevens beveiligd in de kluis Hallo) instellen en controleren van beveiligingsbeleid Hallo. Hallo-beveiligingsbeleid is Hallo plannen wanneer Hallo back-uptaken uitgevoerd en hoe lang de momentopname van elke back-up wordt bewaard.

### <a name="set-vault-context"></a>Set kluis context
Voordat u de beveiliging op een virtuele machine inschakelt, gebruikt u  **[Set AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset Hallo kluis context. Zodra Hallo kluis context is ingesteld, wordt het volgende cmdlets tooall toegepast. Hallo volgende voorbeeld wordt ingesteld Hallo kluis context voor de kluis hello, *testvault*.

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a>Een beveiligingsbeleid maken
Als u een Recovery Services-kluis maakt, beschikt u over de standaardbeveiliging en bewaarbeleid. Hallo protection-standaardbeleid een back-uptaak elke dag op de opgegeven tijd wordt geactiveerd. Hallo standaard bewaarbeleid behoudt Hallo dagelijkse herstelpunt voor 30 dagen. Hallo standaard kunt u beleid tooquickly beveiligen van uw virtuele machine en beleid hello later met verschillende gegevens te bewerken.

Gebruik  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview Hallo-beveiligingsbeleid in Hallo kluis. U kunt deze cmdlet tooget een specifiek beleid of tooview Hallo beleidsregels die zijn gekoppeld aan een type werkbelasting. Hallo voorbeeld van de volgende beleidsregels voor het type werkbelasting, AzureVM opgehaald.

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> Hallo tijdzone van Hallo BackupTime veld in PowerShell is UTC. Wanneer de back-uptijd Hallo in hello Azure-portal wordt weergegeven, is tijd Hallo gecorrigeerde tooyour lokale tijdzone.
>
>

Het beveiligingsbeleid van een back-up is gekoppeld aan ten minste één bewaarbeleid. Bewaarbeleid definieert hoe lang een herstelpunt wordt bewaard voordat deze wordt verwijderd. Gebruik  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  tooview Hallo standaardbeleid bewaren.  Op dezelfde manier kunt u  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain Hallo standaardbeleid planning. Hallo  **[nieuw AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet maakt een PowerShell-object dat back-upbeleid informatie bevat. Hallo planning en het bewaren van beleidsobjecten worden gebruikt als invoer toohello  **[nieuw AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet. Hallo volgende voorbeeld wordt opgeslagen Hallo planning beleid en Hallo bewaarbeleid in variabelen. Hallo voorbeeld maakt gebruik van deze variabelen toodefine Hallo parameters bij het maken van een beveiligingsbeleid *NewPolicy*.

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a>Beveiliging inschakelen
Als u de back-beveiligingsbeleid Hallo hebt gedefinieerd, moet u nog steeds Hallo beleid voor een item inschakelen. Gebruik  **[inschakelen AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable beveiliging. Inschakelen van beveiliging vereist twee objecten - Hallo item en Hallo-beleid. Zodra het Hallo-beleid is gekoppeld aan de kluis hello, worden Hallo back-werkstroom wordt geactiveerd op Hallo moment is gedefinieerd in het beleidsschema Hallo.

Hallo voorbeeld de beveiliging schakelt voor Hallo item, V2VM, met behulp van beleid hello, NewPolicy te volgen. tooenable hello beveiliging op niet-versleutelde Resource Manager virtuele machines

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

tooenable hello beveiliging op virtuele machines (versleuteld met behulp van BEK en KEK) versleuteld, moet u toogive hello Azure Backup-service machtiging tooread sleutels en geheimen van de sleutelkluis.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

tooenable hello beveiliging op virtuele machines (versleuteld met BEK alleen) versleuteld, moet u toogive hello Azure Backup-service machtiging tooread geheimen van de sleutelkluis.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> Als u hello Azure Government cloud gebruikt, gebruikt u Hallo waarde ff281ffe-705c-4f53-9f37-a40e6f2c68f3 voor Hallo parameter **- ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet .
>
>

Voor klassieke virtuele machines

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a>Een beveiligingsbeleid wijzigen
toomodify hello protection-beleid, gebruik [Set AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy of RetentionPolicy-objecten.

Hallo wordt volgende voorbeeld Hallo recovery point bewaren too365 dagen.

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a>Activeren van een back-up
U kunt  **[back-up AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger een back-uptaak. Als het Hallo eerste back-up is, is een volledige back-up. Volgende back-ups duren voordat een incrementele kopie. Ervoor toouse worden  **[Set AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset Hallo kluis context voordat de back-uptaak Hallo. Hallo volgende voorbeeld wordt ervan uitgegaan kluis context is ingesteld.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> Hallo tijdzone van Hallo StartTime en EndTime velden in PowerShell is UTC. Wanneer het Hallo-tijd in hello Azure-portal wordt weergegeven, is tijd Hallo gecorrigeerde tooyour lokale tijdzone.
>
>

## <a name="monitoring-a-backup-job"></a>Bewaking van een back-uptaak
U kunt langlopende bewerkingen, zoals back-uptaken bewaken zonder hello Azure-portal. tooget hello status van een taak wordt uitgevoerd, gebruik Hallo  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet. Deze cmdlet opgehaald Hallo back-uptaken voor een specifieke kluis en de kluis die is opgegeven in Hallo kluis context. Hallo volgende voorbeeld wordt Hallo-status van een taak wordt uitgevoerd als een matrix, en opgeslagen Hallo status in Hallo $joblist variabele.

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Gebruik in plaats van deze taken voor voltooiing - dit is niet nodig aanvullende code - polling Hallo  **[wacht AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet. Deze cmdlet onderbreekt Hallo worden uitgevoerd totdat Hallo-taak is voltooid of Hallo opgegeven time-outwaarde is bereikt.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a>Een Azure-virtuele machine herstellen
Er is een belangrijke verschil tussen Hallo herstellen van een virtuele machine met behulp van hello Azure-portal en het herstellen van een virtuele machine met behulp van PowerShell. PowerShell is Hallo restore-bewerking is voltooid zodra het Hallo-schijven en configuratie-informatie uit Hallo herstelpunt worden gemaakt.

> [!NOTE]
> Hallo-herstelbewerking maakt geen een virtuele machine.
>
>

toocreate een virtuele machine van de schijf, Zie sectie Hallo [maken Hallo VM van opgeslagen schijven](backup-azure-vms-automation.md#create-a-vm-from-stored-disks). Hallo basisstappen toorestore een Azure VM zijn:

* Hallo VM selecteren
* Kies een herstelpunt
* Hallo schijven herstellen
* Hallo VM maken van opgeslagen schijven

Hallo volgende afbeelding ziet u de objecthiërarchie Hallo van Hallo RecoveryServicesVault omlaag toohello BackupRecoveryPoint.

![Recovery Services-objecthiërarchie BackupContainer weergeven](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

back-upgegevens toorestore, identificeren Hallo back-up item en Hallo herstelpunt dat Hallo punt in tijd gegevens bevat. Gebruik Hallo  **[terugzetten AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore gegevens van Hallo toohello klantaccount-kluis.

### <a name="select-hello-vm"></a>Hallo VM selecteren
tooget hello PowerShell-object waarmee Hallo rechts item back-up, starten vanuit het Hallo-container in Hallo kluis en boven naar beneden Hallo objecthiërarchie werken. tooselect Hallo-container die virtuele machine, gebruik Hallo Hallo vertegenwoordigt  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet en doorsluizen die toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a>Kies een herstelpunt
Gebruik Hallo  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  cmdlet toolist alle voor Hallo back-item herstelpunten. Kies vervolgens Hallo herstel punt toorestore. Als u niet zeker welk herstelpunt punt toouse weet, is een goede gewoonte toochoose Hallo meest recente RecoveryPointType = AppConsistent punt in de lijst Hallo.

Hallo-variabele, in Hallo script volgen, **$rp**, is een matrix van herstelpunten voor Hallo back-item van Hallo afgelopen zeven dagen geselecteerde. Hallo array in omgekeerde volgorde gesorteerd tijd met de meest recente herstelpunt Hallo bij index 0. Gebruik standaard PowerShell matrix toopick Hallo herstelpunt te indexeren. In Hallo voorbeeld selecteert $rp [0] Hallo meest recente herstelpunt.

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-hello-disks"></a>Hallo schijven herstellen
Gebruik Hallo  **[terugzetten AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore gegevens een back-item en herstel van de configuratie tooa verwijzen. Wanneer u een herstelpunt hebt geïdentificeerd, gebruiken als Hallo-waarde voor Hallo **- RecoveryPoint** parameter. In het vorige voorbeeldcode hello, **$rp [0]** Hallo herstel punt toouse is. In de volgende voorbeeldcode Hallo **$rp [0]** Hallo herstel punt toouse voor het herstellen van Hallo schijf is.

toorestore hello schijven en configuratie-informatie:

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Gebruik Hallo  **[wacht AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait voor Hallo terugzetten taak toocomplete cmdlet.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

Zodra de hersteltaak Hallo is voltooid, gebruikt u Hallo  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  cmdlet tooget Hallo details van Hallo herstelbewerking. Hallo JobDetails eigenschap heeft Hallo informatie nodig toorebuild Hallo VM.

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

Wanneer u schijven Hallo herstelt, gaan toohello volgende sectie toocreate Hallo VM.

## <a name="create-a-vm-from-restored-disks"></a>Een virtuele machine maken van herstelde schijven
Nadat u Hallo schijven teruggezet hebt, gebruikt u deze stappen toocreate en Hallo virtuele machine van de schijf configureren.

> [!NOTE]
> toocreate versleuteld VM's van herstelde schijven, uw Azure rol moet beschikken over de machtiging tooperform Hallo actie **Microsoft.KeyVault/vaults/deploy/action**. Als uw rol is niet gemachtigd dit, maakt u een aangepaste rol met deze actie. Zie voor meer informatie [aangepaste rollen in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).
>
>

1. Query Hallo schijfeigenschappen voor Hallo taakdetails hersteld.

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. Hello Azure storage-context instellen en herstel Hallo JSON-configuratiebestand.

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. Hallo JSON configuration file toocreate Hallo VM-configuratie gebruiken.

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. Hallo besturingssysteemschijf en gegevensschijven koppelen. Afhankelijk van de configuratie van de Hallo van uw virtuele machines, klikt u op Hallo relevante koppeling tooview respectieve cmdlets: 
    - [Niet-beheerde, niet-versleutelde virtuele machines](#non-managed-non-encrypted-vms)
    - [Niet-beheerde, gecodeerde VMs (alleen BEK)](#non-managed-encrypted-vms-bek-only)
    - [Niet-beheerde, gecodeerde VMs (BEK en KEK)](#non-managed-encrypted-vms-bek-and-kek)
    - [Beheerd, niet-versleutelde virtuele machines](#managed-non-encrypted-vms)
    - [Beheerde, gecodeerde VMs (BEK en KEK)](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a>Niet-beheerde, niet-versleutelde virtuele machines

    Hallo voorbeeld te volgen voor niet-beheerde, niet-versleutelde VM's gebruiken.

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a>Niet-beheerde, gecodeerde VMs (alleen BEK)

    Voor niet-beheerde, gecodeerde virtuele machines (versleuteld met BEK alleen), moet u toorestore Hallo geheime toohello sleutelkluis voordat u schijven kunt koppelen. Zie voor meer informatie artikel Hallo [een versleutelde virtuele machine herstellen vanaf een herstelpunt voor Azure Backup](backup-azure-restore-key-secret.md). Hallo volgende voorbeeld ziet u hoe tooattach besturingssysteem en gegevensschijven voor virtuele machines versleuteld.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a>Niet-beheerde, gecodeerde VMs (BEK en KEK)

    Voor niet-beheerde, gecodeerde virtuele machines (versleuteld met behulp van BEK en KEK), moet u toorestore Hallo sleutel en geheime toohello sleutelkluis voordat u schijven kunt koppelen. Zie voor meer informatie artikel Hallo [een versleutelde virtuele machine herstellen vanaf een herstelpunt voor Azure Backup](backup-azure-restore-key-secret.md). Hallo volgende voorbeeld ziet u hoe tooattach besturingssysteem en gegevensschijven voor virtuele machines versleuteld.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a>Beheerd, niet-versleutelde virtuele machines

    Voor niet-versleutelde VM's van beheerde, zult u toocreate beheerd schijven van blob-opslag nodig, en voeg vervolgens Hallo-schijven. Zie voor gedetailleerde informatie Hallo artikel [koppelen van een schijf tooa voor gegevens virtuele machine van Windows met behulp van PowerShell](../virtual-machines/windows/attach-disk-ps.md). Hallo volgende voorbeeldcode ziet u hoe tooattach gegevensschijven Hallo voor niet-versleutelde VM's van beheerde.

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a>Beheerde, gecodeerde VMs (BEK en KEK)

    Voor beheerde versleutelde virtuele machines (versleuteld met behulp van BEK en KEK), hebt u toocreate beheerd schijven van blob-opslag nodig, en voeg vervolgens Hallo-schijven. Zie voor gedetailleerde informatie Hallo artikel [koppelen van een schijf tooa voor gegevens virtuele machine van Windows met behulp van PowerShell](../virtual-machines/windows/attach-disk-ps.md). Hallo ziet volgende voorbeeldcode u hoe tooattach gegevensschijven Hallo voor beheerde versleutelde virtuele machines.

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. Hallo-netwerkinstellingen ingesteld.

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. Hallo virtuele machine maken.

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a>Volgende stappen
Als u liever toouse PowerShell tooengage met uw Azure-resources, Zie Hallo PowerShell artikel [implementeren en beheren van back-up voor Windows Server](backup-client-automation.md). Als u DPM-back-ups beheren, Zie Hallo artikel [implementeren en beheren van Backup voor DPM](backup-dpm-automation.md). Hebben beide van deze artikelen een versie voor implementaties van Resource Manager en klassieke implementaties.  
