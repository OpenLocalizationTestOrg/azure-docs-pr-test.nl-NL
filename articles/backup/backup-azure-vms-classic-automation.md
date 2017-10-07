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
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="ae8c1-103">Gebruik AzureRM.Backup cmdlets tooback van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ae8c1-103">Use AzureRM.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae8c1-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ae8c1-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="ae8c1-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="ae8c1-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="ae8c1-106">Dit artikel ziet u hoe toouse Azure PowerShell voor back-up en herstel van virtuele Azure-machines.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-106">This article shows you how toouse Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="ae8c1-107">In Azure zijn twee verschillende implementatiemodellen beschikbaar voor het maken van en werken met resources: Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="ae8c1-108">In dit artikel bevat informatie over met behulp van Hallo Classic deployment model tooback up gegevens tooa Backup-kluis.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-108">This article covers using hello Classic deployment model tooback up data tooa Backup vault.</span></span> <span data-ttu-id="ae8c1-109">Als u niet een back-upkluis in uw abonnement hebt gemaakt, raadpleegt u Hallo Resource Manager-versie van dit artikel [gebruik AzureRM.RecoveryServices.Backup cmdlets tooback van virtuele machines](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="ae8c1-109">If you have not created a Backup vault in your subscription, see hello Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="ae8c1-110">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae8c1-111">U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-111">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="ae8c1-112">Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="ae8c1-112">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="ae8c1-113">Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-113">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="ae8c1-114">U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-114">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="ae8c1-115">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="ae8c1-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="ae8c1-116">Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-116">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="ae8c1-117">U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-117">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="ae8c1-118">In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-118">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="ae8c1-119">Concepten</span><span class="sxs-lookup"><span data-stu-id="ae8c1-119">Concepts</span></span>
<span data-ttu-id="ae8c1-120">In dit artikel bevat informatie die specifieke toohello PowerShell-cmdlets gebruikt tooback van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-120">This article provides information specific toohello PowerShell cmdlets used tooback up virtual machines.</span></span> <span data-ttu-id="ae8c1-121">Raadpleeg voor inleidende informatie over het beveiligen van Azure Virtual machines [plannen van uw back-infrastructuur van de virtuele machine in Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ae8c1-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ae8c1-122">Lees voordat u begint, Hallo [vereisten](backup-azure-vms-prepare.md) vereist toowork met Azure Backup en Hallo [beperkingen](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) van Hallo huidige VM-back-upoplossing.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-122">Before you start, read hello [prerequisites](backup-azure-vms-prepare.md) required toowork with Azure Backup, and hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of hello current VM backup solution.</span></span>
>
>

<span data-ttu-id="ae8c1-123">toouse PowerShell nemen effectief, een ogenblik toounderstand Hallo hiërarchie van objecten en waar toostart.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-123">toouse PowerShell effectively, take a moment toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Objecthiërarchie](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="ae8c1-125">Hallo twee belangrijkste stromen u beveiliging inschakelt voor een virtuele machine en herstellen van gegevens vanaf een herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-125">hello two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="ae8c1-126">Hallo van dit artikel worden toohelp u meer bijzonder geschikt voor het werken met Hallo PowerShell-cmdlets tooenable deze twee scenario's.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-126">hello focus of this article is toohelp you become adept at working with hello PowerShell cmdlets tooenable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="ae8c1-127">De installatie en registratie</span><span class="sxs-lookup"><span data-stu-id="ae8c1-127">Setup and Registration</span></span>
<span data-ttu-id="ae8c1-128">toobegin:</span><span class="sxs-lookup"><span data-stu-id="ae8c1-128">toobegin:</span></span>

1. <span data-ttu-id="ae8c1-129">[Download de meest recente PowerShell](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="ae8c1-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="ae8c1-130">Zoeken hello Azure back-up PowerShell-cmdlets zijn beschikbaar op Hallo volgende opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="ae8c1-130">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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

<span data-ttu-id="ae8c1-131">Hallo kunnen volgende installatie en registratietaken worden geautomatiseerd met PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ae8c1-131">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="ae8c1-132">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="ae8c1-132">Create a backup vault</span></span>
* <span data-ttu-id="ae8c1-133">Hallo VMs registreren met hello Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="ae8c1-133">Registering hello VMs with hello Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="ae8c1-134">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="ae8c1-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="ae8c1-135">Voor klanten die gebruikmaken van Azure Backup voor Hallo eerst, moet u tooregister hello Azure Backup-provider toobe gebruikt met uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-135">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="ae8c1-136">Dit kan worden gedaan door het uitvoeren van de volgende opdracht Hallo: Register AzureRmResourceProvider - ProviderNamespace 'Microsoft.Backup'</span><span class="sxs-lookup"><span data-stu-id="ae8c1-136">This can be done by running hello following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="ae8c1-137">U kunt een nieuwe back-upkluis met Hallo maken **nieuw AzureRmBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-137">You can create a new backup vault using hello **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="ae8c1-138">Hallo back-upkluis is een ARM-bron, dus u tooplace moet deze binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-138">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="ae8c1-139">Voer Hallo volgende opdrachten in een verhoogde Azure PowerShell-console:</span><span class="sxs-lookup"><span data-stu-id="ae8c1-139">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="ae8c1-140">U kunt een lijst met alle Hallo back-upkluizen krijgen in een bepaald abonnement met behulp van Hallo **Get-AzureRmBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-140">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="ae8c1-141">Dit is handig toostore Hallo back-upkluis-object in een variabele.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-141">It is convenient toostore hello backup vault object into a variable.</span></span> <span data-ttu-id="ae8c1-142">Hallo kluis object is nodig als invoer voor veel Azure Backup-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-142">hello vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-hello-vms"></a><span data-ttu-id="ae8c1-143">Hallo VMs registreren</span><span class="sxs-lookup"><span data-stu-id="ae8c1-143">Registering hello VMs</span></span>
<span data-ttu-id="ae8c1-144">de eerste stap Hallo naar het configureren van back-up met Azure Backup is tooregister uw computer of virtuele machine met een Azure Backup-kluis.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-144">hello first step towards configuring backup with Azure Backup is tooregister your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="ae8c1-145">Hallo **registreren AzureRmBackupContainer** cmdlet Hallo invoergegevens van een virtuele machine van Azure IaaS neemt en registreert deze bij Hallo opgegeven kluis.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-145">hello **Register-AzureRmBackupContainer** cmdlet takes hello input information of an Azure IaaS virtual machine and registers it with hello specified vault.</span></span> <span data-ttu-id="ae8c1-146">Hallo registerbewerking hello Azure virtuele machine koppelt aan Hallo back-upkluis en houdt Hallo VM levenscyclus Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-146">hello register operation associates hello Azure virtual machine with hello backup vault and tracks hello VM through hello backup lifecycle.</span></span>

<span data-ttu-id="ae8c1-147">Registreren van uw virtuele machine met hello Azure Backup-service, maakt een site op het hoogste containerobject.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-147">Registering your VM with hello Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="ae8c1-148">Een container bevat doorgaans meerdere items die u kunnen een back-up, maar in geval van virtuele machines Hallo zal er slechts één back-item voor Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-148">A container typically contains multiple items that can be backed up, but in hello case of VMs there will be only one backup item for hello container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="ae8c1-149">Back-ups maken van virtuele Azure-machines</span><span class="sxs-lookup"><span data-stu-id="ae8c1-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="ae8c1-150">Een beveiligingsbeleid maken</span><span class="sxs-lookup"><span data-stu-id="ae8c1-150">Create a protection policy</span></span>
<span data-ttu-id="ae8c1-151">Het is niet verplicht toocreate een nieuwe beveiligingsgroep beleid toostart back-up van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-151">It is not mandatory toocreate a new protection policy toostart backup of your VMs.</span></span> <span data-ttu-id="ae8c1-152">Hallo-kluis wordt geleverd met een 'standaardbeleid' die kan worden gebruikt tooquickly inschakelen van de beveiliging en later bewerkt met de juiste details Hallo.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-152">hello vault comes with a 'Default Policy' that can be used tooquickly enable protection, and then edited later with hello right details.</span></span> <span data-ttu-id="ae8c1-153">U kunt een lijst met Hallo beleidsregels beschikbaar in de kluis Hallo opvragen met Hallo **Get-AzureRmBackupProtectionPolicy** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ae8c1-153">You can get a list of hello policies available in hello vault by using hello **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="ae8c1-154">Hallo tijdzone van Hallo BackupTime veld in PowerShell is UTC.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-154">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="ae8c1-155">Wanneer de back-uptijd Hallo in hello Azure-portal wordt weergegeven, is Hallo tijdzone uitgelijnde tooyour lokaal systeem samen met de Hallo UTC-offset.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-155">However, when hello backup time is shown in hello Azure portal, hello timezone is aligned tooyour local system along with hello UTC offset.</span></span>
>
>

<span data-ttu-id="ae8c1-156">Er is een back-upbeleid gekoppeld aan ten minste één bewaarbeleid.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="ae8c1-157">Hallo bewaarbeleid definieert hoe lang een herstelpunt wordt gehouden met Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-157">hello retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="ae8c1-158">Hallo **nieuw AzureRmBackupRetentionPolicy** cmdlet maakt een PowerShell-objecten die informatie over bewaarbeleid bevatten.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-158">hello **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="ae8c1-159">Deze bewaren beleid-objecten worden gebruikt als invoer toohello *nieuw AzureRmBackupProtectionPolicy* cmdlet, of rechtstreeks met de Hallo *inschakelen AzureRmBackupProtection* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-159">These retention policy objects are used as inputs toohello *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with hello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="ae8c1-160">Een back-upbeleid definieert wanneer en hoe vaak hello back-up van een item wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-160">A backup policy defines when and how often hello backup of an item is done.</span></span> <span data-ttu-id="ae8c1-161">Hallo **nieuw AzureRmBackupProtectionPolicy** cmdlet maakt een PowerShell-object dat back-upbeleid informatie bevat.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-161">hello **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="ae8c1-162">Hallo back-beleid wordt gebruikt als een invoer toohello *inschakelen AzureRmBackupProtection* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-162">hello backup policy is used as an input toohello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="ae8c1-163">Beveiliging inschakelen</span><span class="sxs-lookup"><span data-stu-id="ae8c1-163">Enable protection</span></span>
<span data-ttu-id="ae8c1-164">Beveiliging in te schakelen moet u twee objecten - hello Item en Hallo beleid en beide nodig toobelong toohello dezelfde kluis.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-164">Enabling protection involves two objects - hello Item and hello Policy, and both need toobelong toohello same vault.</span></span> <span data-ttu-id="ae8c1-165">Als Hallo beleid is gekoppeld aan Hallo-item, wordt Hallo back-werkstroom starten op Hallo gedefinieerde planning.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-165">Once hello policy has been associated with hello item, hello backup workflow will kick in at hello defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="ae8c1-166">Eerste back-up</span><span class="sxs-lookup"><span data-stu-id="ae8c1-166">Initial backup</span></span>
<span data-ttu-id="ae8c1-167">back-upschema Hallo zorgt voor de volgende back-ups Hallo Hallo incrementele kopie en volledige initiële kopie van de Hallo voor Hallo-item te doen.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-167">hello backup schedule will take care of doing hello full initial copy for hello item and hello incremental copy for hello subsequent backups.</span></span> <span data-ttu-id="ae8c1-168">Echter, als u wilt dat tooforce Hallo eerste back-toohappen op een bepaald tijdstip of zelfs onmiddellijk vervolgens gebruiken Hallo **back-up AzureRmBackupItem** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ae8c1-168">However, if you want tooforce hello initial backup toohappen at a certain time or even immediately then use hello **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="ae8c1-169">Hallo tijdzone Hallo StartTime en EndTime velden wordt weergegeven in PowerShell is UTC.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-169">hello timezone of hello StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="ae8c1-170">Wanneer Hallo vergelijkbare gegevens in hello Azure-portal wordt weergegeven, is Hallo tijdzone uitgelijnde tooyour lokale systeemklok.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-170">However, when hello similar information is shown in hello Azure portal, hello timezone is aligned tooyour local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="ae8c1-171">Bewaking van een back-uptaak</span><span class="sxs-lookup"><span data-stu-id="ae8c1-171">Monitoring a backup job</span></span>
<span data-ttu-id="ae8c1-172">De meeste langlopende bewerkingen in Azure Backup gemodelleerd zijn als een taak.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="ae8c1-173">Dit maakt het eenvoudig tootrack uitgevoerd zonder tookeep hello Azure portal openen te allen tijde.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-173">This makes it easy tootrack progress without having tookeep hello Azure portal open at all times.</span></span>

<span data-ttu-id="ae8c1-174">tooget hello laatste status van een taak wordt uitgevoerd, gebruik Hallo **Get-AzureRmBackupJob** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-174">tooget hello latest status of an in-progress job, use hello **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="ae8c1-175">In plaats van deze taken voor voltooiing - dit is niet nodig, aanvullende code - polling is eenvoudiger toouse hello **wacht AzureRmBackupJob** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler toouse hello **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="ae8c1-176">Wanneer gebruikt in een script, wordt Hallo cmdlet Hallo uitvoering onderbroken totdat Hallo-taak is voltooid of Hallo opgegeven time-outwaarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-176">When used in a script, hello cmdlet will pause hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="ae8c1-177">Een Azure-virtuele machine herstellen</span><span class="sxs-lookup"><span data-stu-id="ae8c1-177">Restore an Azure VM</span></span>
<span data-ttu-id="ae8c1-178">In de volgorde toorestore back-upgegevens, moet u tooidentify Hallo back-up Item en Hallo herstelpunt die Hallo punt in tijd gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-178">In order toorestore backup data, you need tooidentify hello backed-up Item and hello Recovery Point that holds hello point-in-time data.</span></span> <span data-ttu-id="ae8c1-179">Deze informatie is opgegeven toohello terugzetten AzureRmBackupItem cmdlet tooinitiate terugzetten van gegevens uit Hallo kluis toohello van klant-account.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-179">This information is supplied toohello Restore-AzureRmBackupItem cmdlet tooinitiate a restore of data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="ae8c1-180">Hallo VM selecteren</span><span class="sxs-lookup"><span data-stu-id="ae8c1-180">Select hello VM</span></span>
<span data-ttu-id="ae8c1-181">tooget hello PowerShell-object waarmee Hallo juiste back-Item, u moet toostart van Hallo Container in Hallo kluis en boven naar beneden objecthiërarchie werken.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-181">tooget hello PowerShell object that identifies hello right backup Item, you need toostart from hello Container in hello vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="ae8c1-182">tooselect Hallo-container die virtuele machine, gebruik Hallo Hallo vertegenwoordigt **Get-AzureRmBackupContainer** cmdlet en doorsluizen die toohello **Get-AzureRmBackupItem** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-182">tooselect hello container that represents hello VM, use hello **Get-AzureRmBackupContainer** cmdlet and pipe that toohello **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="ae8c1-183">Kies een herstelpunt</span><span class="sxs-lookup"><span data-stu-id="ae8c1-183">Choose a recovery point</span></span>
<span data-ttu-id="ae8c1-184">U kunt nu alle Hallo herstelpunten voor de back-item Hallo Hallo met aanbieden **Get-AzureRmBackupRecoveryPoint** cmdlet, en kies Hallo herstel punt toorestore.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-184">You can now list all hello recovery points for hello backup item using hello **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose hello recovery point toorestore.</span></span> <span data-ttu-id="ae8c1-185">Meestal gebruikers Hallo meest recente Kies *AppConsistent* wijst u in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-185">Typically users pick hello most recent *AppConsistent* point in hello list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="ae8c1-186">Hallo variabele ```$rp``` is een matrix van herstelpunten voor Hallo back-item, in omgekeerde volgorde gesorteerd tijd geselecteerd - de meest recente herstelpunt Hallo bij index 0 is.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-186">hello variable ```$rp``` is an array of recovery points for hello selected backup item, sorted in reverse order of time - hello latest recovery point is at index 0.</span></span> <span data-ttu-id="ae8c1-187">Gebruik standaard PowerShell matrix toopick Hallo herstelpunt te indexeren.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-187">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="ae8c1-188">Bijvoorbeeld: ```$rp[0]``` Hallo meest recente herstelpunt wordt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-188">For example: ```$rp[0]``` will select hello latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="ae8c1-189">Herstellen van schijven</span><span class="sxs-lookup"><span data-stu-id="ae8c1-189">Restoring disks</span></span>
<span data-ttu-id="ae8c1-190">Er is een belangrijke verschil tussen Hallo herstelbewerkingen gedaan via hello Azure-portal en via Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-190">There is a key difference between hello restore operations done through hello Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="ae8c1-191">Met PowerShell stopt Hallo restore-bewerking op het Hallo-schijven en configuratie-informatie herstellen vanaf herstelpunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-191">With PowerShell, hello restore operation stops at restoring hello disks and config information from hello recovery point.</span></span> <span data-ttu-id="ae8c1-192">Er wordt een virtuele machine niet gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="ae8c1-193">Hallo terugzetten AzureRmBackupItem maakt een virtuele machine niet.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-193">hello Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="ae8c1-194">Herstelt alleen Hallo schijven toohello storage-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-194">It only restores hello disks toohello specified storage account.</span></span> <span data-ttu-id="ae8c1-195">Dit is niet hetzelfde gedrag treedt in hello Azure-portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-195">This is not hello same behavior you will experience in hello Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="ae8c1-196">U krijgt Hallo details van Hallo herstelbewerking met Hallo **Get-AzureRmBackupJobDetails** cmdlet wanneer Hallo hersteltaak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-196">You can get hello details of hello restore operation using hello **Get-AzureRmBackupJobDetails** cmdlet once hello Restore job has completed.</span></span> <span data-ttu-id="ae8c1-197">Hallo *ErrorDetails* eigenschap heeft Hallo informatie nodig toorebuild Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-197">hello *ErrorDetails* property will have hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a><span data-ttu-id="ae8c1-198">Hallo VM bouwen</span><span class="sxs-lookup"><span data-stu-id="ae8c1-198">Build hello VM</span></span>
<span data-ttu-id="ae8c1-199">Gebouw Hallo VM buiten Hallo hersteld schijven kan worden gedaan met behulp van de oudere Azure Service Management PowerShell-cmdlets Hallo Hallo van nieuwe Azure Resource Manager-sjablonen of zelfs met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-199">Building hello VM out of hello restored disks can be done using hello older Azure Service Management PowerShell cmdlets, hello new Azure Resource Manager templates, or even using hello Azure portal.</span></span> <span data-ttu-id="ae8c1-200">In een kort voorbeeld we tonen hoe tooget er met hello Azure Service Management-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-200">In a quick example, we will show how tooget there using hello Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="ae8c1-201">Voor meer informatie over het lezen van toobuild een virtuele machine van de schijven Hallo hersteld, over Hallo cmdlets volgen:</span><span class="sxs-lookup"><span data-stu-id="ae8c1-201">For more information on how toobuild a VM from hello restored disks, read about hello following cmdlets:</span></span>

* [<span data-ttu-id="ae8c1-202">Voeg AzureDisk</span><span class="sxs-lookup"><span data-stu-id="ae8c1-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="ae8c1-203">Nieuwe AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="ae8c1-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="ae8c1-204">Nieuwe-AzureVM</span><span class="sxs-lookup"><span data-stu-id="ae8c1-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="ae8c1-205">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="ae8c1-205">Code samples</span></span>
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a><span data-ttu-id="ae8c1-206">1. Hallo-voltooiingsstatus van onderliggende taken ophalen</span><span class="sxs-lookup"><span data-stu-id="ae8c1-206">1. Get hello completion status of job sub-tasks</span></span>
<span data-ttu-id="ae8c1-207">tootrack hello voltooiingsstatus van afzonderlijke onderliggende taken, kunt u Hallo **Get-AzureRmBackupJobDetails** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ae8c1-207">tootrack hello completion status of individual sub-tasks, you can use hello **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="ae8c1-208">2. Maak een rapport dagelijks/wekelijks back-uptaken</span><span class="sxs-lookup"><span data-stu-id="ae8c1-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="ae8c1-209">Beheerders willen doorgaans tooknow welke back-uptaken die worden uitgevoerd in Hallo afgelopen 24 uur Hallo status van deze back-uptaken.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-209">Administrators typically want tooknow what backup jobs ran in hello last 24 hours, hello status of those backup jobs.</span></span> <span data-ttu-id="ae8c1-210">Bovendien Hallo en de hoeveelheid gegevens overgedragen biedt beheerders een tooestimate manier hun maandelijkse gebruiksgegevens van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-210">Additionally, hello amount of data transferred gives administrators a way tooestimate their monthly data usage.</span></span> <span data-ttu-id="ae8c1-211">Hallo onderstaande script Hallo ruwe gegevens ophaalt uit hello Azure Backup-service en Hallo gegevens weergegeven in Hallo PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-211">hello script below pulls hello raw data from hello Azure Backup service and displays hello information in hello PowerShell console.</span></span>

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

<span data-ttu-id="ae8c1-212">Als u tooadd mogelijkheden toothis rapportuitvoer voor grafieken wilt, leren van Hallo TechNet-blogbericht [voor grafieken met PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="ae8c1-212">If you want tooadd charting capabilities toothis report output, learn from hello TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae8c1-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ae8c1-213">Next steps</span></span>
<span data-ttu-id="ae8c1-214">Als u liever met behulp van PowerShell tooengage met uw Azure-resources, bekijk Hallo PowerShell artikel voor het beveiligen van Windows Server [implementeren en beheren van back-up voor Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="ae8c1-214">If you prefer using PowerShell tooengage with your Azure resources, check out hello PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="ae8c1-215">Er is ook een PowerShell-artikel voor het beheren van back-ups van DPM [implementeren en beheren van Backup voor DPM](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="ae8c1-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="ae8c1-216">Hebben beide van deze artikelen een versie voor implementaties van Resource Manager, evenals klassieke implementaties.</span><span class="sxs-lookup"><span data-stu-id="ae8c1-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
