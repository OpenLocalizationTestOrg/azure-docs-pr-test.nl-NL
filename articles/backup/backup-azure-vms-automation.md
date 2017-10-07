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
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="ee496-103">Gebruik AzureRM.RecoveryServices.Backup cmdlets tooback van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ee496-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee496-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee496-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="ee496-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="ee496-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="ee496-106">Dit artikel laat zien hoe toouse Azure PowerShell-cmdlets tooback up en herstel Azure een virtuele machine (VM) van een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="ee496-106">This article shows you how toouse Azure PowerShell cmdlets tooback up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="ee496-107">Een Recovery Services-kluis is een Azure Resource Manager-resource en gebruikte tooprotect gegevens en activa in Azure Backup- en Azure Site Recovery services.</span><span class="sxs-lookup"><span data-stu-id="ee496-107">A Recovery Services vault is an Azure Resource Manager resource and is used tooprotect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="ee496-108">U kunt een Recovery Services-kluis tooprotect Azure Service Manager geïmplementeerde VM's en Azure Resource Manager geïmplementeerde VM's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee496-108">You can use a Recovery Services vault tooprotect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="ee496-109">Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ee496-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ee496-110">In dit artikel is voor gebruik met virtuele machines die zijn gemaakt met behulp van Hallo Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="ee496-110">This article is for use with VMs created using hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="ee496-111">In dit artikel leert u met behulp van PowerShell tooprotect een virtuele machine en gegevens terugzetten vanaf een herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="ee496-111">This article walks you through using PowerShell tooprotect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="ee496-112">Concepten</span><span class="sxs-lookup"><span data-stu-id="ee496-112">Concepts</span></span>
<span data-ttu-id="ee496-113">Als u niet bekend met hello Azure Backup-service voor een overzicht van service Hallo bent, Bekijk [wat is Azure Backup?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="ee496-113">If you are not familiar with hello Azure Backup service, for an overview of hello service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="ee496-114">Voordat u begint, zorg ervoor dat hebben betrekking op Hallo essentials over Hallo vereisten nodig toowork met Azure Backup en beperkingen van Hallo huidige VM-back-upoplossing Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee496-114">Before you start, ensure that you cover hello essentials about hello prerequisites needed toowork with Azure Backup, and hello limitations of hello current VM backup solution.</span></span>

<span data-ttu-id="ee496-115">toouse PowerShell effectief is noodzakelijk toounderstand Hallo hiërarchie van objecten en waar toostart.</span><span class="sxs-lookup"><span data-stu-id="ee496-115">toouse PowerShell effectively, it is necessary toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Recovery Services-objecthiërarchie](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="ee496-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell-cmdlet-verwijzing, Zie Hallo [Azure Backup - Cmdlets voor Recovery Services](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="ee496-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see hello [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="ee496-118">De installatie en registratie</span><span class="sxs-lookup"><span data-stu-id="ee496-118">Setup and Registration</span></span>
<span data-ttu-id="ee496-119">toobegin:</span><span class="sxs-lookup"><span data-stu-id="ee496-119">toobegin:</span></span>

1. <span data-ttu-id="ee496-120">[Download de nieuwste versie Hallo van PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (Hallo minimaal vereiste versie is: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="ee496-120">[Download hello latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="ee496-121">Zoeken hello Azure back-up PowerShell-cmdlets zijn beschikbaar op Hallo volgende opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="ee496-121">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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


<span data-ttu-id="ee496-122">Hallo na taken kan worden geautomatiseerd met PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ee496-122">hello following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="ee496-123">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="ee496-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="ee496-124">Back-ups maken van Azure-VM's</span><span class="sxs-lookup"><span data-stu-id="ee496-124">Back up Azure VMs</span></span>
* <span data-ttu-id="ee496-125">Een back-uptaak wordt geactiveerd</span><span class="sxs-lookup"><span data-stu-id="ee496-125">Trigger a backup job</span></span>
* <span data-ttu-id="ee496-126">Een back-uptaak bewaken</span><span class="sxs-lookup"><span data-stu-id="ee496-126">Monitor a backup job</span></span>
* <span data-ttu-id="ee496-127">Een Azure-virtuele machine herstellen</span><span class="sxs-lookup"><span data-stu-id="ee496-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ee496-128">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="ee496-128">Create a recovery services vault</span></span>
<span data-ttu-id="ee496-129">volgende stappen uit Hallo leiden u bij het maken van een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="ee496-129">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="ee496-130">Een Recovery Services-kluis is anders dan een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="ee496-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="ee496-131">Als u van Azure Backup voor Hallo eerst gebruikmaakt, moet u Hallo  **[registreren AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  cmdlet tooregister hello Azure Recovery Service provider met uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="ee496-131">If you are using Azure Backup for hello first time, you must use hello **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="ee496-132">Hallo Recovery Services-kluis is een Resource Manager-bron, dus u tooplace moet deze binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ee496-132">hello Recovery Services vault is a Resource Manager resource, so you need tooplace it within a resource group.</span></span> <span data-ttu-id="ee496-133">U kunt een bestaande resourcegroep gebruiken of een resourcegroep maken met de Hallo  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee496-133">You can use an existing resource group, or create a resource group with hello **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="ee496-134">Bij het maken van een resourcegroep Hallo naam en locatie voor resourcegroep Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="ee496-134">When creating a resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="ee496-135">Gebruik Hallo  **[nieuw AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  cmdlet toocreate Hallo Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="ee496-135">Use hello **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet toocreate hello Recovery Services vault.</span></span> <span data-ttu-id="ee496-136">Zorg ervoor dat toospecify dezelfde locatie voor de kluis Hallo Hallo werd gebruikt voor de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee496-136">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="ee496-137">Geef een Hallo van opslag redundantie toouse; u kunt [lokaal redundante opslag (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) of [geografisch redundante opslag (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="ee496-137">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="ee496-138">Hallo volgende voorbeeld ziet Hallo BackupStorageRedundancy - optie voor testvault tooGeoRedundant is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ee496-138">hello following example shows hello -BackupStorageRedundancy option for testvault is set tooGeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="ee496-139">Veel Azure Backup-cmdlets vereisen Hallo Recovery Services-kluis object als invoer.</span><span class="sxs-lookup"><span data-stu-id="ee496-139">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="ee496-140">Daarom is het handige toostore Hallo back-up Recovery Services-kluis object in een variabele.</span><span class="sxs-lookup"><span data-stu-id="ee496-140">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="ee496-141">Hallo-kluizen in een abonnement weergeven</span><span class="sxs-lookup"><span data-stu-id="ee496-141">View hello vaults in a subscription</span></span>
<span data-ttu-id="ee496-142">Gebruik  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview Hallo lijst met alle kluizen in het huidige abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee496-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="ee496-143">U kunt deze opdracht toocheck dat een nieuwe kluis is gemaakt of toosee Hallo beschikbaar kluizen in Hallo abonnement gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee496-143">You can use this command toocheck that a new vault was created, or toosee hello available vaults in hello subscription.</span></span>

<span data-ttu-id="ee496-144">Hallo-opdracht Get-AzureRmRecoveryServicesVault tooview alle kluizen in Hallo abonnement uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ee496-144">Run hello command, Get-AzureRmRecoveryServicesVault, tooview all vaults in hello subscription.</span></span> <span data-ttu-id="ee496-145">Hallo wordt volgende voorbeeld weergegeven voor elke kluis Hallo-informatie.</span><span class="sxs-lookup"><span data-stu-id="ee496-145">hello following example shows hello information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="ee496-146">Back-ups maken van Azure-VM's</span><span class="sxs-lookup"><span data-stu-id="ee496-146">Back up Azure VMs</span></span>
<span data-ttu-id="ee496-147">Gebruik een Recovery Services-kluis tooprotect uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ee496-147">Use a Recovery Services vault tooprotect your virtual machines.</span></span> <span data-ttu-id="ee496-148">Voordat u Hallo beveiliging toepast, Hallo kluis context (Hallo type gegevens beveiligd in de kluis Hallo) instellen en controleren van beveiligingsbeleid Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee496-148">Before you apply hello protection, set hello vault context (hello type of data protected in hello vault), and verify hello protection policy.</span></span> <span data-ttu-id="ee496-149">Hallo-beveiligingsbeleid is Hallo plannen wanneer Hallo back-uptaken uitgevoerd en hoe lang de momentopname van elke back-up wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="ee496-149">hello protection policy is hello schedule when hello backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="ee496-150">Set kluis context</span><span class="sxs-lookup"><span data-stu-id="ee496-150">Set vault context</span></span>
<span data-ttu-id="ee496-151">Voordat u de beveiliging op een virtuele machine inschakelt, gebruikt u  **[Set AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset Hallo kluis context.</span><span class="sxs-lookup"><span data-stu-id="ee496-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context.</span></span> <span data-ttu-id="ee496-152">Zodra Hallo kluis context is ingesteld, wordt het volgende cmdlets tooall toegepast.</span><span class="sxs-lookup"><span data-stu-id="ee496-152">Once hello vault context is set, it applies tooall subsequent cmdlets.</span></span> <span data-ttu-id="ee496-153">Hallo volgende voorbeeld wordt ingesteld Hallo kluis context voor de kluis hello, *testvault*.</span><span class="sxs-lookup"><span data-stu-id="ee496-153">hello following example sets hello vault context for hello vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="ee496-154">Een beveiligingsbeleid maken</span><span class="sxs-lookup"><span data-stu-id="ee496-154">Create a protection policy</span></span>
<span data-ttu-id="ee496-155">Als u een Recovery Services-kluis maakt, beschikt u over de standaardbeveiliging en bewaarbeleid.</span><span class="sxs-lookup"><span data-stu-id="ee496-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="ee496-156">Hallo protection-standaardbeleid een back-uptaak elke dag op de opgegeven tijd wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="ee496-156">hello default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="ee496-157">Hallo standaard bewaarbeleid behoudt Hallo dagelijkse herstelpunt voor 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="ee496-157">hello default retention policy retains hello daily recovery point for 30 days.</span></span> <span data-ttu-id="ee496-158">Hallo standaard kunt u beleid tooquickly beveiligen van uw virtuele machine en beleid hello later met verschillende gegevens te bewerken.</span><span class="sxs-lookup"><span data-stu-id="ee496-158">You can use hello default policy tooquickly protect your VM and edit hello policy later with different details.</span></span>

<span data-ttu-id="ee496-159">Gebruik  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview Hallo-beveiligingsbeleid in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="ee496-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** tooview hello protection policies in hello vault.</span></span> <span data-ttu-id="ee496-160">U kunt deze cmdlet tooget een specifiek beleid of tooview Hallo beleidsregels die zijn gekoppeld aan een type werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="ee496-160">You can use this cmdlet tooget a specific policy, or tooview hello policies associated with a workload type.</span></span> <span data-ttu-id="ee496-161">Hallo voorbeeld van de volgende beleidsregels voor het type werkbelasting, AzureVM opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ee496-161">hello following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="ee496-162">Hallo tijdzone van Hallo BackupTime veld in PowerShell is UTC.</span><span class="sxs-lookup"><span data-stu-id="ee496-162">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="ee496-163">Wanneer de back-uptijd Hallo in hello Azure-portal wordt weergegeven, is tijd Hallo gecorrigeerde tooyour lokale tijdzone.</span><span class="sxs-lookup"><span data-stu-id="ee496-163">However, when hello backup time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

<span data-ttu-id="ee496-164">Het beveiligingsbeleid van een back-up is gekoppeld aan ten minste één bewaarbeleid.</span><span class="sxs-lookup"><span data-stu-id="ee496-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="ee496-165">Bewaarbeleid definieert hoe lang een herstelpunt wordt bewaard voordat deze wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ee496-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="ee496-166">Gebruik  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  tooview Hallo standaardbeleid bewaren.</span><span class="sxs-lookup"><span data-stu-id="ee496-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** tooview hello default retention policy.</span></span>  <span data-ttu-id="ee496-167">Op dezelfde manier kunt u  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain Hallo standaardbeleid planning.</span><span class="sxs-lookup"><span data-stu-id="ee496-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** tooobtain hello default schedule policy.</span></span> <span data-ttu-id="ee496-168">Hallo  **[nieuw AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet maakt een PowerShell-object dat back-upbeleid informatie bevat.</span><span class="sxs-lookup"><span data-stu-id="ee496-168">hello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="ee496-169">Hallo planning en het bewaren van beleidsobjecten worden gebruikt als invoer toohello  **[nieuw AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee496-169">hello schedule and retention policy objects are used as inputs toohello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="ee496-170">Hallo volgende voorbeeld wordt opgeslagen Hallo planning beleid en Hallo bewaarbeleid in variabelen.</span><span class="sxs-lookup"><span data-stu-id="ee496-170">hello following example stores hello schedule policy and hello retention policy in variables.</span></span> <span data-ttu-id="ee496-171">Hallo voorbeeld maakt gebruik van deze variabelen toodefine Hallo parameters bij het maken van een beveiligingsbeleid *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="ee496-171">hello example uses those variables toodefine hello parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="ee496-172">Beveiliging inschakelen</span><span class="sxs-lookup"><span data-stu-id="ee496-172">Enable protection</span></span>
<span data-ttu-id="ee496-173">Als u de back-beveiligingsbeleid Hallo hebt gedefinieerd, moet u nog steeds Hallo beleid voor een item inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ee496-173">Once you have defined hello backup protection policy, you still must enable hello policy for an item.</span></span> <span data-ttu-id="ee496-174">Gebruik  **[inschakelen AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable beveiliging.</span><span class="sxs-lookup"><span data-stu-id="ee496-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** tooenable protection.</span></span> <span data-ttu-id="ee496-175">Inschakelen van beveiliging vereist twee objecten - Hallo item en Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="ee496-175">Enabling protection requires two objects - hello item and hello policy.</span></span> <span data-ttu-id="ee496-176">Zodra het Hallo-beleid is gekoppeld aan de kluis hello, worden Hallo back-werkstroom wordt geactiveerd op Hallo moment is gedefinieerd in het beleidsschema Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee496-176">Once hello policy has been associated with hello vault, hello backup workflow is triggered at hello time defined in hello policy schedule.</span></span>

<span data-ttu-id="ee496-177">Hallo voorbeeld de beveiliging schakelt voor Hallo item, V2VM, met behulp van beleid hello, NewPolicy te volgen.</span><span class="sxs-lookup"><span data-stu-id="ee496-177">hello following example enables protection for hello item, V2VM, using hello policy, NewPolicy.</span></span> <span data-ttu-id="ee496-178">tooenable hello beveiliging op niet-versleutelde Resource Manager virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ee496-178">tooenable hello protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="ee496-179">tooenable hello beveiliging op virtuele machines (versleuteld met behulp van BEK en KEK) versleuteld, moet u toogive hello Azure Backup-service machtiging tooread sleutels en geheimen van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="ee496-179">tooenable hello protection on encrypted VMs (encrypted using BEK and KEK), you need toogive hello Azure Backup service permission tooread keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="ee496-180">tooenable hello beveiliging op virtuele machines (versleuteld met BEK alleen) versleuteld, moet u toogive hello Azure Backup-service machtiging tooread geheimen van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="ee496-180">tooenable hello protection on encrypted VMs (encrypted using BEK only), you need toogive hello Azure Backup service permission tooread secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="ee496-181">Als u hello Azure Government cloud gebruikt, gebruikt u Hallo waarde ff281ffe-705c-4f53-9f37-a40e6f2c68f3 voor Hallo parameter **- ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet .</span><span class="sxs-lookup"><span data-stu-id="ee496-181">If you are using hello Azure Government cloud, then use hello value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for hello parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="ee496-182">Voor klassieke virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ee496-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="ee496-183">Een beveiligingsbeleid wijzigen</span><span class="sxs-lookup"><span data-stu-id="ee496-183">Modify a protection policy</span></span>
<span data-ttu-id="ee496-184">toomodify hello protection-beleid, gebruik [Set AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy of RetentionPolicy-objecten.</span><span class="sxs-lookup"><span data-stu-id="ee496-184">toomodify hello protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="ee496-185">Hallo wordt volgende voorbeeld Hallo recovery point bewaren too365 dagen.</span><span class="sxs-lookup"><span data-stu-id="ee496-185">hello following example changes hello recovery point retention too365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="ee496-186">Activeren van een back-up</span><span class="sxs-lookup"><span data-stu-id="ee496-186">Trigger a backup</span></span>
<span data-ttu-id="ee496-187">U kunt  **[back-up AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger een back-uptaak.</span><span class="sxs-lookup"><span data-stu-id="ee496-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** tootrigger a backup job.</span></span> <span data-ttu-id="ee496-188">Als het Hallo eerste back-up is, is een volledige back-up.</span><span class="sxs-lookup"><span data-stu-id="ee496-188">If it is hello initial backup, it is a full backup.</span></span> <span data-ttu-id="ee496-189">Volgende back-ups duren voordat een incrementele kopie.</span><span class="sxs-lookup"><span data-stu-id="ee496-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="ee496-190">Ervoor toouse worden  **[Set AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset Hallo kluis context voordat de back-uptaak Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee496-190">Be sure toouse **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context before triggering hello backup job.</span></span> <span data-ttu-id="ee496-191">Hallo volgende voorbeeld wordt ervan uitgegaan kluis context is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ee496-191">hello following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="ee496-192">Hallo tijdzone van Hallo StartTime en EndTime velden in PowerShell is UTC.</span><span class="sxs-lookup"><span data-stu-id="ee496-192">hello timezone of hello StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="ee496-193">Wanneer het Hallo-tijd in hello Azure-portal wordt weergegeven, is tijd Hallo gecorrigeerde tooyour lokale tijdzone.</span><span class="sxs-lookup"><span data-stu-id="ee496-193">However, when hello time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="ee496-194">Bewaking van een back-uptaak</span><span class="sxs-lookup"><span data-stu-id="ee496-194">Monitoring a backup job</span></span>
<span data-ttu-id="ee496-195">U kunt langlopende bewerkingen, zoals back-uptaken bewaken zonder hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ee496-195">You can monitor long-running operations, such as backup jobs, without using hello Azure portal.</span></span> <span data-ttu-id="ee496-196">tooget hello status van een taak wordt uitgevoerd, gebruik Hallo  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee496-196">tooget hello status of an in-progress job, use hello **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="ee496-197">Deze cmdlet opgehaald Hallo back-uptaken voor een specifieke kluis en de kluis die is opgegeven in Hallo kluis context.</span><span class="sxs-lookup"><span data-stu-id="ee496-197">This cmdlet gets hello backup jobs for a specific vault, and that vault is specified in hello vault context.</span></span> <span data-ttu-id="ee496-198">Hallo volgende voorbeeld wordt Hallo-status van een taak wordt uitgevoerd als een matrix, en opgeslagen Hallo status in Hallo $joblist variabele.</span><span class="sxs-lookup"><span data-stu-id="ee496-198">hello following example gets hello status of an in-progress job as an array, and stores hello status in hello $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="ee496-199">Gebruik in plaats van deze taken voor voltooiing - dit is niet nodig aanvullende code - polling Hallo  **[wacht AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee496-199">Instead of polling these jobs for completion - which is unnecessary additional code - use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="ee496-200">Deze cmdlet onderbreekt Hallo worden uitgevoerd totdat Hallo-taak is voltooid of Hallo opgegeven time-outwaarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="ee496-200">This cmdlet pauses hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="ee496-201">Een Azure-virtuele machine herstellen</span><span class="sxs-lookup"><span data-stu-id="ee496-201">Restore an Azure VM</span></span>
<span data-ttu-id="ee496-202">Er is een belangrijke verschil tussen Hallo herstellen van een virtuele machine met behulp van hello Azure-portal en het herstellen van een virtuele machine met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee496-202">There is a key difference between hello restoring a VM using hello Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="ee496-203">PowerShell is Hallo restore-bewerking is voltooid zodra het Hallo-schijven en configuratie-informatie uit Hallo herstelpunt worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ee496-203">With PowerShell, hello restore operation is complete once hello disks and configuration information from hello recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="ee496-204">Hallo-herstelbewerking maakt geen een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ee496-204">hello restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="ee496-205">toocreate een virtuele machine van de schijf, Zie sectie Hallo [maken Hallo VM van opgeslagen schijven](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="ee496-205">toocreate a virtual machine from disk, see hello section, [Create hello VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="ee496-206">Hallo basisstappen toorestore een Azure VM zijn:</span><span class="sxs-lookup"><span data-stu-id="ee496-206">hello basic steps toorestore an Azure VM are:</span></span>

* <span data-ttu-id="ee496-207">Hallo VM selecteren</span><span class="sxs-lookup"><span data-stu-id="ee496-207">Select hello VM</span></span>
* <span data-ttu-id="ee496-208">Kies een herstelpunt</span><span class="sxs-lookup"><span data-stu-id="ee496-208">Choose a recovery point</span></span>
* <span data-ttu-id="ee496-209">Hallo schijven herstellen</span><span class="sxs-lookup"><span data-stu-id="ee496-209">Restore hello disks</span></span>
* <span data-ttu-id="ee496-210">Hallo VM maken van opgeslagen schijven</span><span class="sxs-lookup"><span data-stu-id="ee496-210">Create hello VM from stored disks</span></span>

<span data-ttu-id="ee496-211">Hallo volgende afbeelding ziet u de objecthiërarchie Hallo van Hallo RecoveryServicesVault omlaag toohello BackupRecoveryPoint.</span><span class="sxs-lookup"><span data-stu-id="ee496-211">hello following graphic shows hello object hierarchy from hello RecoveryServicesVault down toohello BackupRecoveryPoint.</span></span>

![Recovery Services-objecthiërarchie BackupContainer weergeven](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="ee496-213">back-upgegevens toorestore, identificeren Hallo back-up item en Hallo herstelpunt dat Hallo punt in tijd gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="ee496-213">toorestore backup data, identify hello backed-up item and hello recovery point that holds hello point-in-time data.</span></span> <span data-ttu-id="ee496-214">Gebruik Hallo  **[terugzetten AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore gegevens van Hallo toohello klantaccount-kluis.</span><span class="sxs-lookup"><span data-stu-id="ee496-214">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="ee496-215">Hallo VM selecteren</span><span class="sxs-lookup"><span data-stu-id="ee496-215">Select hello VM</span></span>
<span data-ttu-id="ee496-216">tooget hello PowerShell-object waarmee Hallo rechts item back-up, starten vanuit het Hallo-container in Hallo kluis en boven naar beneden Hallo objecthiërarchie werken.</span><span class="sxs-lookup"><span data-stu-id="ee496-216">tooget hello PowerShell object that identifies hello right backup item, start from hello container in hello vault, and work your way down hello object hierarchy.</span></span> <span data-ttu-id="ee496-217">tooselect Hallo-container die virtuele machine, gebruik Hallo Hallo vertegenwoordigt  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet en doorsluizen die toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee496-217">tooselect hello container that represents hello VM, use hello **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that toohello **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="ee496-218">Kies een herstelpunt</span><span class="sxs-lookup"><span data-stu-id="ee496-218">Choose a recovery point</span></span>
<span data-ttu-id="ee496-219">Gebruik Hallo  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  cmdlet toolist alle voor Hallo back-item herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="ee496-219">Use hello **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet toolist all recovery points for hello backup item.</span></span> <span data-ttu-id="ee496-220">Kies vervolgens Hallo herstel punt toorestore.</span><span class="sxs-lookup"><span data-stu-id="ee496-220">Then choose hello recovery point toorestore.</span></span> <span data-ttu-id="ee496-221">Als u niet zeker welk herstelpunt punt toouse weet, is een goede gewoonte toochoose Hallo meest recente RecoveryPointType = AppConsistent punt in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee496-221">If you are unsure which recovery point toouse, it is a good practice toochoose hello most recent RecoveryPointType = AppConsistent point in hello list.</span></span>

<span data-ttu-id="ee496-222">Hallo-variabele, in Hallo script volgen, **$rp**, is een matrix van herstelpunten voor Hallo back-item van Hallo afgelopen zeven dagen geselecteerde.</span><span class="sxs-lookup"><span data-stu-id="ee496-222">In hello following script, hello variable, **$rp**, is an array of recovery points for hello selected backup item, from hello past seven days.</span></span> <span data-ttu-id="ee496-223">Hallo array in omgekeerde volgorde gesorteerd tijd met de meest recente herstelpunt Hallo bij index 0.</span><span class="sxs-lookup"><span data-stu-id="ee496-223">hello array is sorted in reverse order of time with hello latest recovery point at index 0.</span></span> <span data-ttu-id="ee496-224">Gebruik standaard PowerShell matrix toopick Hallo herstelpunt te indexeren.</span><span class="sxs-lookup"><span data-stu-id="ee496-224">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="ee496-225">In Hallo voorbeeld selecteert $rp [0] Hallo meest recente herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="ee496-225">In hello example, $rp[0] selects hello latest recovery point.</span></span>

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



### <a name="restore-hello-disks"></a><span data-ttu-id="ee496-226">Hallo schijven herstellen</span><span class="sxs-lookup"><span data-stu-id="ee496-226">Restore hello disks</span></span>
<span data-ttu-id="ee496-227">Gebruik Hallo  **[terugzetten AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore gegevens een back-item en herstel van de configuratie tooa verwijzen.</span><span class="sxs-lookup"><span data-stu-id="ee496-227">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore a backup item's data and configuration tooa recovery point.</span></span> <span data-ttu-id="ee496-228">Wanneer u een herstelpunt hebt geïdentificeerd, gebruiken als Hallo-waarde voor Hallo **- RecoveryPoint** parameter.</span><span class="sxs-lookup"><span data-stu-id="ee496-228">Once you have identified a recovery point, use it as hello value for hello **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="ee496-229">In het vorige voorbeeldcode hello, **$rp [0]** Hallo herstel punt toouse is.</span><span class="sxs-lookup"><span data-stu-id="ee496-229">In hello previous sample code, **$rp[0]** was hello recovery point toouse.</span></span> <span data-ttu-id="ee496-230">In de volgende voorbeeldcode Hallo **$rp [0]** Hallo herstel punt toouse voor het herstellen van Hallo schijf is.</span><span class="sxs-lookup"><span data-stu-id="ee496-230">In hello following sample code, **$rp[0]** is hello recovery point toouse for restoring hello disk.</span></span>

<span data-ttu-id="ee496-231">toorestore hello schijven en configuratie-informatie:</span><span class="sxs-lookup"><span data-stu-id="ee496-231">toorestore hello disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="ee496-232">Gebruik Hallo  **[wacht AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait voor Hallo terugzetten taak toocomplete cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee496-232">Use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet toowait for hello Restore job toocomplete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="ee496-233">Zodra de hersteltaak Hallo is voltooid, gebruikt u Hallo  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  cmdlet tooget Hallo details van Hallo herstelbewerking.</span><span class="sxs-lookup"><span data-stu-id="ee496-233">Once hello Restore job has completed, use hello **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet tooget hello details of hello restore operation.</span></span> <span data-ttu-id="ee496-234">Hallo JobDetails eigenschap heeft Hallo informatie nodig toorebuild Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="ee496-234">hello JobDetails property has hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="ee496-235">Wanneer u schijven Hallo herstelt, gaan toohello volgende sectie toocreate Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="ee496-235">Once you restore hello disks, go toohello next section toocreate hello VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="ee496-236">Een virtuele machine maken van herstelde schijven</span><span class="sxs-lookup"><span data-stu-id="ee496-236">Create a VM from restored disks</span></span>
<span data-ttu-id="ee496-237">Nadat u Hallo schijven teruggezet hebt, gebruikt u deze stappen toocreate en Hallo virtuele machine van de schijf configureren.</span><span class="sxs-lookup"><span data-stu-id="ee496-237">After you have restored hello disks, use these steps toocreate and configure hello virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="ee496-238">toocreate versleuteld VM's van herstelde schijven, uw Azure rol moet beschikken over de machtiging tooperform Hallo actie **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="ee496-238">toocreate encrypted VMs from restored disks, your Azure role must have permission tooperform hello action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="ee496-239">Als uw rol is niet gemachtigd dit, maakt u een aangepaste rol met deze actie.</span><span class="sxs-lookup"><span data-stu-id="ee496-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="ee496-240">Zie voor meer informatie [aangepaste rollen in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="ee496-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="ee496-241">Query Hallo schijfeigenschappen voor Hallo taakdetails hersteld.</span><span class="sxs-lookup"><span data-stu-id="ee496-241">Query hello restored disk properties for hello job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="ee496-242">Hello Azure storage-context instellen en herstel Hallo JSON-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="ee496-242">Set hello Azure storage context and restore hello JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="ee496-243">Hallo JSON configuration file toocreate Hallo VM-configuratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee496-243">Use hello JSON configuration file toocreate hello VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="ee496-244">Hallo besturingssysteemschijf en gegevensschijven koppelen.</span><span class="sxs-lookup"><span data-stu-id="ee496-244">Attach hello OS disk and data disks.</span></span> <span data-ttu-id="ee496-245">Afhankelijk van de configuratie van de Hallo van uw virtuele machines, klikt u op Hallo relevante koppeling tooview respectieve cmdlets:</span><span class="sxs-lookup"><span data-stu-id="ee496-245">Depending on hello configuration of your VMs, click on hello relevant link tooview respective cmdlets:</span></span> 
    - [<span data-ttu-id="ee496-246">Niet-beheerde, niet-versleutelde virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ee496-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="ee496-247">Niet-beheerde, gecodeerde VMs (alleen BEK)</span><span class="sxs-lookup"><span data-stu-id="ee496-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="ee496-248">Niet-beheerde, gecodeerde VMs (BEK en KEK)</span><span class="sxs-lookup"><span data-stu-id="ee496-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="ee496-249">Beheerd, niet-versleutelde virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ee496-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="ee496-250">Beheerde, gecodeerde VMs (BEK en KEK)</span><span class="sxs-lookup"><span data-stu-id="ee496-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="ee496-251">Niet-beheerde, niet-versleutelde virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ee496-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="ee496-252">Hallo voorbeeld te volgen voor niet-beheerde, niet-versleutelde VM's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee496-252">Use hello following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="ee496-253">Niet-beheerde, gecodeerde VMs (alleen BEK)</span><span class="sxs-lookup"><span data-stu-id="ee496-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="ee496-254">Voor niet-beheerde, gecodeerde virtuele machines (versleuteld met BEK alleen), moet u toorestore Hallo geheime toohello sleutelkluis voordat u schijven kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="ee496-254">For non-managed, encrypted VMs (encrypted using BEK only), you need toorestore hello secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="ee496-255">Zie voor meer informatie artikel Hallo [een versleutelde virtuele machine herstellen vanaf een herstelpunt voor Azure Backup](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="ee496-255">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="ee496-256">Hallo volgende voorbeeld ziet u hoe tooattach besturingssysteem en gegevensschijven voor virtuele machines versleuteld.</span><span class="sxs-lookup"><span data-stu-id="ee496-256">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="ee496-257">Niet-beheerde, gecodeerde VMs (BEK en KEK)</span><span class="sxs-lookup"><span data-stu-id="ee496-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="ee496-258">Voor niet-beheerde, gecodeerde virtuele machines (versleuteld met behulp van BEK en KEK), moet u toorestore Hallo sleutel en geheime toohello sleutelkluis voordat u schijven kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="ee496-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need toorestore hello key and secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="ee496-259">Zie voor meer informatie artikel Hallo [een versleutelde virtuele machine herstellen vanaf een herstelpunt voor Azure Backup](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="ee496-259">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="ee496-260">Hallo volgende voorbeeld ziet u hoe tooattach besturingssysteem en gegevensschijven voor virtuele machines versleuteld.</span><span class="sxs-lookup"><span data-stu-id="ee496-260">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="ee496-261">Beheerd, niet-versleutelde virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ee496-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="ee496-262">Voor niet-versleutelde VM's van beheerde, zult u toocreate beheerd schijven van blob-opslag nodig, en voeg vervolgens Hallo-schijven.</span><span class="sxs-lookup"><span data-stu-id="ee496-262">For managed non-encrypted VMs, you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="ee496-263">Zie voor gedetailleerde informatie Hallo artikel [koppelen van een schijf tooa voor gegevens virtuele machine van Windows met behulp van PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ee496-263">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="ee496-264">Hallo volgende voorbeeldcode ziet u hoe tooattach gegevensschijven Hallo voor niet-versleutelde VM's van beheerde.</span><span class="sxs-lookup"><span data-stu-id="ee496-264">hello following sample code shows how tooattach hello data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="ee496-265">Beheerde, gecodeerde VMs (BEK en KEK)</span><span class="sxs-lookup"><span data-stu-id="ee496-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="ee496-266">Voor beheerde versleutelde virtuele machines (versleuteld met behulp van BEK en KEK), hebt u toocreate beheerd schijven van blob-opslag nodig, en voeg vervolgens Hallo-schijven.</span><span class="sxs-lookup"><span data-stu-id="ee496-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="ee496-267">Zie voor gedetailleerde informatie Hallo artikel [koppelen van een schijf tooa voor gegevens virtuele machine van Windows met behulp van PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ee496-267">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="ee496-268">Hallo ziet volgende voorbeeldcode u hoe tooattach gegevensschijven Hallo voor beheerde versleutelde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ee496-268">hello following sample code shows how tooattach hello data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="ee496-269">Hallo-netwerkinstellingen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ee496-269">Set hello Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="ee496-270">Hallo virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="ee496-270">Create hello virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="ee496-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ee496-271">Next steps</span></span>
<span data-ttu-id="ee496-272">Als u liever toouse PowerShell tooengage met uw Azure-resources, Zie Hallo PowerShell artikel [implementeren en beheren van back-up voor Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="ee496-272">If you prefer toouse PowerShell tooengage with your Azure resources, see hello PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="ee496-273">Als u DPM-back-ups beheren, Zie Hallo artikel [implementeren en beheren van Backup voor DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="ee496-273">If you manage DPM backups, see hello article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="ee496-274">Hebben beide van deze artikelen een versie voor implementaties van Resource Manager en klassieke implementaties.</span><span class="sxs-lookup"><span data-stu-id="ee496-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
