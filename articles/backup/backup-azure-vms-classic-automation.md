---
title: Implementeren en beheren van back-up voor virtuele Azure-machines met behulp van PowerShell | Microsoft Docs
description: Informatie over het implementeren en beheren van Azure Backup met behulp van PowerShell.
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
ms.openlocfilehash: 5f0f06adb8177ce2d17aa0b40666470279c04e22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-azurermbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="20462-103">AzureRM.Backup-cmdlets gebruiken om back-up van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="20462-103">Use AzureRM.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20462-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="20462-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="20462-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="20462-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="20462-106">Dit artikel laat zien hoe u Azure PowerShell gebruikt voor back-up en herstel van virtuele Azure-machines.</span><span class="sxs-lookup"><span data-stu-id="20462-106">This article shows you how to use Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="20462-107">In Azure zijn twee verschillende implementatiemodellen beschikbaar voor het maken van en werken met resources: Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="20462-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="20462-108">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel voor back-ups naar een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="20462-108">This article covers using the Classic deployment model to back up data to a Backup vault.</span></span> <span data-ttu-id="20462-109">Als u niet een back-upkluis in uw abonnement hebt gemaakt, raadpleegt u de Resource Manager-versie van dit artikel [gebruik AzureRM.RecoveryServices.Backup-cmdlets voor back-up van virtuele machines](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="20462-109">If you have not created a Backup vault in your subscription, see the Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="20462-110">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="20462-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20462-111">U kunt uw back-upkluizen nu upgraden naar Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="20462-111">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="20462-112">Zie voor meer informatie het artikel [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md) (Een back-upkluis upgraden naar een Recovery Services-kluis).</span><span class="sxs-lookup"><span data-stu-id="20462-112">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="20462-113">Microsoft adviseert om uw back-upkluizen te upgraden naar Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="20462-113">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="20462-114">Na 15 oktober 2017 kunt u PowerShell niet meer gebruiken voor het maken van back-upkluizen.</span><span class="sxs-lookup"><span data-stu-id="20462-114">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="20462-115">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="20462-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="20462-116">Alle resterende back-upkluizen worden automatisch omgezet in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="20462-116">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="20462-117">Het is niet mogelijk om via de klassieke portal toegang te krijgen tot uw back-upgegevens.</span><span class="sxs-lookup"><span data-stu-id="20462-117">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="20462-118">In plaats daarvan gebruikt u Azure Portal voor toegang tot uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="20462-118">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="20462-119">Concepten</span><span class="sxs-lookup"><span data-stu-id="20462-119">Concepts</span></span>
<span data-ttu-id="20462-120">In dit artikel bevat informatie die specifiek zijn voor de PowerShell-cmdlets gebruikt voor back-up van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="20462-120">This article provides information specific to the PowerShell cmdlets used to back up virtual machines.</span></span> <span data-ttu-id="20462-121">Raadpleeg voor inleidende informatie over het beveiligen van Azure Virtual machines [plannen van uw back-infrastructuur van de virtuele machine in Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="20462-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="20462-122">Lees voordat u begint, de [vereisten](backup-azure-vms-prepare.md) vereist voor het werken met Azure Backup en de [beperkingen](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) van de huidige VM-back-upoplossing.</span><span class="sxs-lookup"><span data-stu-id="20462-122">Before you start, read the [prerequisites](backup-azure-vms-prepare.md) required to work with Azure Backup, and the [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of the current VM backup solution.</span></span>
>
>

<span data-ttu-id="20462-123">PowerShell als effectief wilt gebruiken, neem even de tijd om te begrijpen van de hiërarchie van objecten en van waar u wilt beginnen.</span><span class="sxs-lookup"><span data-stu-id="20462-123">To use PowerShell effectively, take a moment to understand the hierarchy of objects and from where to start.</span></span>

![Objecthiërarchie](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="20462-125">De twee belangrijkste stromen u beveiliging inschakelt voor een virtuele machine en herstellen van gegevens vanaf een herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="20462-125">The two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="20462-126">De focus van dit artikel is om te helpen u bijzonder geschikt voor het werken met de PowerShell-cmdlets voor het inschakelen van deze twee scenario's.</span><span class="sxs-lookup"><span data-stu-id="20462-126">The focus of this article is to help you become adept at working with the PowerShell cmdlets to enable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="20462-127">De installatie en registratie</span><span class="sxs-lookup"><span data-stu-id="20462-127">Setup and Registration</span></span>
<span data-ttu-id="20462-128">Om te beginnen met:</span><span class="sxs-lookup"><span data-stu-id="20462-128">To begin:</span></span>

1. <span data-ttu-id="20462-129">[Download de meest recente PowerShell](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="20462-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="20462-130">De beschikbare Azure back-up PowerShell-cmdlets vinden door de volgende opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="20462-130">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

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

<span data-ttu-id="20462-131">De volgende taken voor de installatie en registratie kunnen worden geautomatiseerd met PowerShell:</span><span class="sxs-lookup"><span data-stu-id="20462-131">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="20462-132">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="20462-132">Create a backup vault</span></span>
* <span data-ttu-id="20462-133">Registreren van de virtuele machines met de Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="20462-133">Registering the VMs with the Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="20462-134">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="20462-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="20462-135">Voor klanten met Azure Backup voor de eerste keer, moet u de Azure Backup-provider die moet worden gebruikt met uw abonnement te registreren.</span><span class="sxs-lookup"><span data-stu-id="20462-135">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="20462-136">Dit kan worden gedaan door de volgende opdracht uit te voeren: Register AzureRmResourceProvider - ProviderNamespace 'Microsoft.Backup'</span><span class="sxs-lookup"><span data-stu-id="20462-136">This can be done by running the following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="20462-137">U kunt maken met een nieuwe back-upkluis met de **nieuw AzureRmBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20462-137">You can create a new backup vault using the **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="20462-138">De back-upkluis is een ARM-bron, dus u moet deze binnen een resourcegroep te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="20462-138">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="20462-139">Voer de volgende opdrachten in een verhoogde Azure PowerShell-console:</span><span class="sxs-lookup"><span data-stu-id="20462-139">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="20462-140">U krijgt een lijst met alle back-upkluizen in een bepaald abonnement met de **Get-AzureRmBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20462-140">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="20462-141">Is het handig voor het opslaan van het back-upkluis-object in een variabele.</span><span class="sxs-lookup"><span data-stu-id="20462-141">It is convenient to store the backup vault object into a variable.</span></span> <span data-ttu-id="20462-142">Het object van de kluis is nodig als invoer voor veel Azure Backup-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="20462-142">The vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-the-vms"></a><span data-ttu-id="20462-143">Registreren van de virtuele machines</span><span class="sxs-lookup"><span data-stu-id="20462-143">Registering the VMs</span></span>
<span data-ttu-id="20462-144">De eerste stap naar de back-up configureren met Azure Backup is uw computer of virtuele machine met een Azure Backup-kluis registreren.</span><span class="sxs-lookup"><span data-stu-id="20462-144">The first step towards configuring backup with Azure Backup is to register your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="20462-145">De **registreren AzureRmBackupContainer** cmdlet neemt de invoergegevens van een virtuele machine van Azure IaaS en registreert deze bij de opgegeven kluis.</span><span class="sxs-lookup"><span data-stu-id="20462-145">The **Register-AzureRmBackupContainer** cmdlet takes the input information of an Azure IaaS virtual machine and registers it with the specified vault.</span></span> <span data-ttu-id="20462-146">De registerbewerking wordt gekoppeld aan virtuele machine van Azure met de back-upkluis en volgt de virtuele machine via de levenscyclus van de back-up.</span><span class="sxs-lookup"><span data-stu-id="20462-146">The register operation associates the Azure virtual machine with the backup vault and tracks the VM through the backup lifecycle.</span></span>

<span data-ttu-id="20462-147">Registreren van uw virtuele machine met de Azure Backup-service, maakt een site op het hoogste containerobject.</span><span class="sxs-lookup"><span data-stu-id="20462-147">Registering your VM with the Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="20462-148">Een container bevat doorgaans meerdere items die u kunnen een back-up, maar in het geval van virtuele machines wordt er slechts één back-item voor de container.</span><span class="sxs-lookup"><span data-stu-id="20462-148">A container typically contains multiple items that can be backed up, but in the case of VMs there will be only one backup item for the container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="20462-149">Back-ups maken van virtuele Azure-machines</span><span class="sxs-lookup"><span data-stu-id="20462-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="20462-150">Een beveiligingsbeleid maken</span><span class="sxs-lookup"><span data-stu-id="20462-150">Create a protection policy</span></span>
<span data-ttu-id="20462-151">Het is niet verplicht te maken van een nieuw beveiligingsbeleid back-up van uw virtuele machines starten.</span><span class="sxs-lookup"><span data-stu-id="20462-151">It is not mandatory to create a new protection policy to start backup of your VMs.</span></span> <span data-ttu-id="20462-152">De kluis wordt geleverd met een 'standaardbeleid' die kunnen worden gebruikt voor het snel geschikt maken van beveiliging en later bewerkt met de juiste gegevens.</span><span class="sxs-lookup"><span data-stu-id="20462-152">The vault comes with a 'Default Policy' that can be used to quickly enable protection, and then edited later with the right details.</span></span> <span data-ttu-id="20462-153">U kunt een lijst van de beleidsregels die beschikbaar zijn in de kluis ophalen met behulp van de **Get-AzureRmBackupProtectionPolicy** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="20462-153">You can get a list of the policies available in the vault by using the **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="20462-154">De tijdzone van het veld BackupTime in PowerShell is UTC.</span><span class="sxs-lookup"><span data-stu-id="20462-154">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="20462-155">Echter, wanneer de back-uptijd wordt weergegeven in de Azure portal, de tijdzone wordt uitgelijnd met het lokale systeem samen met de UTC-offset.</span><span class="sxs-lookup"><span data-stu-id="20462-155">However, when the backup time is shown in the Azure portal, the timezone is aligned to your local system along with the UTC offset.</span></span>
>
>

<span data-ttu-id="20462-156">Er is een back-upbeleid gekoppeld aan ten minste één bewaarbeleid.</span><span class="sxs-lookup"><span data-stu-id="20462-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="20462-157">Het bewaarbeleid definieert hoe lang een herstelpunt wordt gehouden met Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="20462-157">The retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="20462-158">De **nieuw AzureRmBackupRetentionPolicy** cmdlet maakt een PowerShell-objecten die informatie over bewaarbeleid bevatten.</span><span class="sxs-lookup"><span data-stu-id="20462-158">The **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="20462-159">Deze bewaren beleidsobjecten worden gebruikt als invoer voor de *nieuw AzureRmBackupProtectionPolicy* cmdlet, of rechtstreeks met de *inschakelen AzureRmBackupProtection* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20462-159">These retention policy objects are used as inputs to the *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="20462-160">Een back-upbeleid definieert wanneer en hoe vaak de back-up van een item wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="20462-160">A backup policy defines when and how often the backup of an item is done.</span></span> <span data-ttu-id="20462-161">De **nieuw AzureRmBackupProtectionPolicy** cmdlet maakt een PowerShell-object dat back-upbeleid informatie bevat.</span><span class="sxs-lookup"><span data-stu-id="20462-161">The **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="20462-162">Het back-upbeleid wordt gebruikt als invoer voor de *inschakelen AzureRmBackupProtection* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20462-162">The backup policy is used as an input to the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="20462-163">Beveiliging inschakelen</span><span class="sxs-lookup"><span data-stu-id="20462-163">Enable protection</span></span>
<span data-ttu-id="20462-164">Twee objecten - het Item en het beleid voor het inschakelen van beveiliging omvat en beide moeten deel uitmaken van dezelfde kluis.</span><span class="sxs-lookup"><span data-stu-id="20462-164">Enabling protection involves two objects - the Item and the Policy, and both need to belong to the same vault.</span></span> <span data-ttu-id="20462-165">Als het beleid is gekoppeld aan het item, wordt de back-werkstroom starten op het opgegeven schema.</span><span class="sxs-lookup"><span data-stu-id="20462-165">Once the policy has been associated with the item, the backup workflow will kick in at the defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="20462-166">Eerste back-up</span><span class="sxs-lookup"><span data-stu-id="20462-166">Initial backup</span></span>
<span data-ttu-id="20462-167">Het back-upschema zorgt voor de volgende back-ups en de incrementele kopie van de volledige initiële kopie voor het item te doen.</span><span class="sxs-lookup"><span data-stu-id="20462-167">The backup schedule will take care of doing the full initial copy for the item and the incremental copy for the subsequent backups.</span></span> <span data-ttu-id="20462-168">Echter, als u wilt zorgen dat de eerste back-up naar gebeuren op een bepaalde tijd of zelfs onmiddellijk gebruikt u de **back-up AzureRmBackupItem** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="20462-168">However, if you want to force the initial backup to happen at a certain time or even immediately then use the **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="20462-169">De tijdzone van de StartTime en EndTime velden wordt weergegeven in PowerShell is UTC.</span><span class="sxs-lookup"><span data-stu-id="20462-169">The timezone of the StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="20462-170">Wanneer de dezelfde informatie wordt weergegeven in de Azure portal, is echter de tijdzone op de lokale klok uitgelijnd.</span><span class="sxs-lookup"><span data-stu-id="20462-170">However, when the similar information is shown in the Azure portal, the timezone is aligned to your local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="20462-171">Bewaking van een back-uptaak</span><span class="sxs-lookup"><span data-stu-id="20462-171">Monitoring a backup job</span></span>
<span data-ttu-id="20462-172">De meeste langlopende bewerkingen in Azure Backup gemodelleerd zijn als een taak.</span><span class="sxs-lookup"><span data-stu-id="20462-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="20462-173">Hiermee kunt u gemakkelijk voortgang volgen zonder te houden van de Azure-portal openen te allen tijde.</span><span class="sxs-lookup"><span data-stu-id="20462-173">This makes it easy to track progress without having to keep the Azure portal open at all times.</span></span>

<span data-ttu-id="20462-174">Als u de meest recente status van een taak wordt uitgevoerd, gebruikt de **Get-AzureRmBackupJob** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20462-174">To get the latest status of an in-progress job, use the **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="20462-175">In plaats van deze taken voor voltooiing - dit is niet nodig, aanvullende code - polling is het eenvoudiger om te gebruiken de **wacht AzureRmBackupJob** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20462-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler to use the **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="20462-176">Als in een script gebruikt, wordt de cmdlet de uitvoering onderbroken totdat de taak is voltooid of de opgegeven time-outwaarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="20462-176">When used in a script, the cmdlet will pause the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="20462-177">Een Azure-virtuele machine herstellen</span><span class="sxs-lookup"><span data-stu-id="20462-177">Restore an Azure VM</span></span>
<span data-ttu-id="20462-178">Als u wilt back-upgegevens herstellen, moet u identificeren van het artikel back-up en het herstelpunt dat de gegevens van de punt in tijd bevat.</span><span class="sxs-lookup"><span data-stu-id="20462-178">In order to restore backup data, you need to identify the backed-up Item and the Recovery Point that holds the point-in-time data.</span></span> <span data-ttu-id="20462-179">Deze informatie wordt verstrekt aan de cmdlet terugzetten AzureRmBackupItem terugzetten van gegevens uit de kluis om het account van de klant te initiëren.</span><span class="sxs-lookup"><span data-stu-id="20462-179">This information is supplied to the Restore-AzureRmBackupItem cmdlet to initiate a restore of data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="20462-180">Selecteer de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="20462-180">Select the VM</span></span>
<span data-ttu-id="20462-181">Als u het PowerShell-object waarmee de juiste back-artikel, moet u starten vanuit de Container in de kluis en boven naar beneden objecthiërarchie werken.</span><span class="sxs-lookup"><span data-stu-id="20462-181">To get the PowerShell object that identifies the right backup Item, you need to start from the Container in the vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="20462-182">Gebruik om te selecteren in de container waarin de VM vertegenwoordigt, de **Get-AzureRmBackupContainer** cmdlet en doorsluizen die u wilt de **Get-AzureRmBackupItem** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20462-182">To select the container that represents the VM, use the **Get-AzureRmBackupContainer** cmdlet and pipe that to the **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="20462-183">Kies een herstelpunt</span><span class="sxs-lookup"><span data-stu-id="20462-183">Choose a recovery point</span></span>
<span data-ttu-id="20462-184">U kunt nu aanbieden alle herstelpunten voor de back-item met de **Get-AzureRmBackupRecoveryPoint** cmdlet, en kies het herstelpunt te herstellen.</span><span class="sxs-lookup"><span data-stu-id="20462-184">You can now list all the recovery points for the backup item using the **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose the recovery point to restore.</span></span> <span data-ttu-id="20462-185">Meestal gebruikers het meest recente Kies *AppConsistent* wijst u in de lijst.</span><span class="sxs-lookup"><span data-stu-id="20462-185">Typically users pick the most recent *AppConsistent* point in the list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="20462-186">De variabele ```$rp``` is een matrix van herstelpunten voor de geselecteerde back-up artikel, in omgekeerde volgorde gesorteerd tijd - het laatste herstelpunt bij index 0 is.</span><span class="sxs-lookup"><span data-stu-id="20462-186">The variable ```$rp``` is an array of recovery points for the selected backup item, sorted in reverse order of time - the latest recovery point is at index 0.</span></span> <span data-ttu-id="20462-187">Gebruik standaard PowerShell matrix indexeren om op te halen van het herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="20462-187">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="20462-188">Bijvoorbeeld: ```$rp[0]``` wordt het meest recente herstelpunt selecteren.</span><span class="sxs-lookup"><span data-stu-id="20462-188">For example: ```$rp[0]``` will select the latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="20462-189">Herstellen van schijven</span><span class="sxs-lookup"><span data-stu-id="20462-189">Restoring disks</span></span>
<span data-ttu-id="20462-190">Er is een belangrijk verschil tussen de herstelbewerkingen die zijn gedaan via de Azure-portal en via Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20462-190">There is a key difference between the restore operations done through the Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="20462-191">Met PowerShell stopt de herstelbewerking bij het herstellen van de schijven en configuratie-informatie van het herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="20462-191">With PowerShell, the restore operation stops at restoring the disks and config information from the recovery point.</span></span> <span data-ttu-id="20462-192">Er wordt een virtuele machine niet gemaakt.</span><span class="sxs-lookup"><span data-stu-id="20462-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="20462-193">De Restore-AzureRmBackupItem maakt een virtuele machine niet.</span><span class="sxs-lookup"><span data-stu-id="20462-193">The Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="20462-194">De schijven wordt alleen hersteld naar het opgegeven opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="20462-194">It only restores the disks to the specified storage account.</span></span> <span data-ttu-id="20462-195">Dit is niet hetzelfde gedrag die treden er al in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="20462-195">This is not the same behavior you will experience in the Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="20462-196">U kunt de details ophalen van de restore-bewerking via de **Get-AzureRmBackupJobDetails** cmdlet wanneer de hersteltaak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="20462-196">You can get the details of the restore operation using the **Get-AzureRmBackupJobDetails** cmdlet once the Restore job has completed.</span></span> <span data-ttu-id="20462-197">De *ErrorDetails* eigenschap heeft de benodigde informatie om het opnieuw opbouwen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="20462-197">The *ErrorDetails* property will have the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-the-vm"></a><span data-ttu-id="20462-198">De virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="20462-198">Build the VM</span></span>
<span data-ttu-id="20462-199">Het bouwen van de virtuele machine buiten de herstelde schijven kan worden gedaan met behulp van de oudere Azure Service Management PowerShell-cmdlets, de nieuwe Azure Resource Manager-sjablonen of zelfs via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="20462-199">Building the VM out of the restored disks can be done using the older Azure Service Management PowerShell cmdlets, the new Azure Resource Manager templates, or even using the Azure portal.</span></span> <span data-ttu-id="20462-200">We tonen hoe u er met de Azure Service Management-cmdlets in een kort voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="20462-200">In a quick example, we will show how to get there using the Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="20462-201">Lees voor meer informatie over het bouwen van een virtuele machine van de herstelde schijven over de volgende cmdlets:</span><span class="sxs-lookup"><span data-stu-id="20462-201">For more information on how to build a VM from the restored disks, read about the following cmdlets:</span></span>

* [<span data-ttu-id="20462-202">Voeg AzureDisk</span><span class="sxs-lookup"><span data-stu-id="20462-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="20462-203">Nieuwe AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="20462-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="20462-204">Nieuwe-AzureVM</span><span class="sxs-lookup"><span data-stu-id="20462-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="20462-205">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="20462-205">Code samples</span></span>
### <a name="1-get-the-completion-status-of-job-sub-tasks"></a><span data-ttu-id="20462-206">1. De voltooiingsstatus van onderliggende taken ophalen</span><span class="sxs-lookup"><span data-stu-id="20462-206">1. Get the completion status of job sub-tasks</span></span>
<span data-ttu-id="20462-207">Om bij te houden de voltooiingsstatus van afzonderlijke onderliggende taken, kunt u de **Get-AzureRmBackupJobDetails** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="20462-207">To track the completion status of individual sub-tasks, you can use the **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data to Backup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="20462-208">2. Maak een rapport dagelijks/wekelijks back-uptaken</span><span class="sxs-lookup"><span data-stu-id="20462-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="20462-209">Beheerders willen doorgaans weten back-uptaken uitgevoerd in de afgelopen 24 uur de status van deze back-uptaken.</span><span class="sxs-lookup"><span data-stu-id="20462-209">Administrators typically want to know what backup jobs ran in the last 24 hours, the status of those backup jobs.</span></span> <span data-ttu-id="20462-210">Bovendien geeft de hoeveelheid gegevens overgedragen beheerders een manier om in te schatten van de maandelijkse gebruiksgegevens van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="20462-210">Additionally, the amount of data transferred gives administrators a way to estimate their monthly data usage.</span></span> <span data-ttu-id="20462-211">Het onderstaande script de ruwe gegevens ophaalt uit de Azure Backup-service en de informatie in de PowerShell-console weergegeven.</span><span class="sxs-lookup"><span data-stu-id="20462-211">The script below pulls the raw data from the Azure Backup service and displays the information in the PowerShell console.</span></span>

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
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -To $enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for the last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract the information for the reports
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

<span data-ttu-id="20462-212">Als u wilt de mogelijkheden voor grafieken toevoegen aan de rapportuitvoer van dit, leren van de TechNet-blogbericht [voor grafieken met PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="20462-212">If you want to add charting capabilities to this report output, learn from the TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="20462-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20462-213">Next steps</span></span>
<span data-ttu-id="20462-214">Als u liever met PowerShell koppelen aan uw Azure-resources, controleert u het PowerShell-artikel voor het beveiligen van Windows Server [implementeren en beheren van back-up voor Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="20462-214">If you prefer using PowerShell to engage with your Azure resources, check out the PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="20462-215">Er is ook een PowerShell-artikel voor het beheren van back-ups van DPM [implementeren en beheren van Backup voor DPM](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="20462-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="20462-216">Hebben beide van deze artikelen een versie voor implementaties van Resource Manager, evenals klassieke implementaties.</span><span class="sxs-lookup"><span data-stu-id="20462-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
