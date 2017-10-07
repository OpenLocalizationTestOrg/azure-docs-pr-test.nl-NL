---
title: Azure Backup-Server v2 aaaInstall | Microsoft Docs
description: Azure back-upserver v2 biedt verbeterde back-mogelijkheden voor het beveiligen van virtuele machines, bestanden en mappen en werkbelastingen. Meer informatie over hoe tooAzure tooinstall of upgrade van de back-upserver van v2.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="bd695-104">V2 voor Azure Backup-Server installeren</span><span class="sxs-lookup"><span data-stu-id="bd695-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="bd695-105">Azure Backup-Server beveiligt uw virtuele machines (VM's), werkbelastingen, bestanden en mappen en meer.</span><span class="sxs-lookup"><span data-stu-id="bd695-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="bd695-106">Azure back-upserver van v2 bouwt voort op Azure Backup-Server v1- en biedt u de nieuwe functies die niet beschikbaar in v1.</span><span class="sxs-lookup"><span data-stu-id="bd695-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="bd695-107">Zie voor een vergelijking van functies tussen v1- en v2 [Azure Backup-Server protection matrix](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="bd695-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="bd695-108">Hallo aanvullende functies in de back-upserver van v2 zijn een upgrade van de back-upserver van v1.</span><span class="sxs-lookup"><span data-stu-id="bd695-108">hello additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="bd695-109">Back-upserver van v1 is echter niet vereist voor de installatie van de back-upserver van v2.</span><span class="sxs-lookup"><span data-stu-id="bd695-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="bd695-110">Als u tooupgrade van back-upserver van v1 tooBackup Server v2, installeert u de back-upserver van v2 op Hallo back-upserver protection-server.</span><span class="sxs-lookup"><span data-stu-id="bd695-110">If you want tooupgrade from Backup Server v1 tooBackup Server v2, install Backup Server v2 on hello Backup Server protection server.</span></span> <span data-ttu-id="bd695-111">Uw bestaande back-upserver instellingen blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="bd695-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="bd695-112">U kunt back-upserver van v2 installeren op Windows Server 2012 R2 of Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="bd695-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="bd695-113">tootake profiteren van nieuwe functies, zoals System Center 2016 Data Protection Manager moderne back-up opslag, moet u back-upserver van v2 installeren op Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="bd695-113">tootake advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="bd695-114">Vóór de upgrade van tooor installeren back-upserver van v2 lezen over Hallo [installatievereisten](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="bd695-114">Before you upgrade tooor install Backup Server v2, read about hello [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="bd695-115">Azure Backup-Server heeft Hallo dezelfde codebasis als System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="bd695-115">Azure Backup Server has hello same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="bd695-116">Back-Server v1 gelijkwaardige tooData Protection Manager 2012 R2 is en back-upserver van v2 gelijkwaardige tooData Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="bd695-116">Backup Server v1 is equivalent tooData Protection Manager 2012 R2, and Backup Server v2 is equivalent tooData Protection Manager 2016.</span></span> <span data-ttu-id="bd695-117">In dit artikel wordt soms verwijst naar Hallo Data Protection Manager-documentatie.</span><span class="sxs-lookup"><span data-stu-id="bd695-117">This article occasionally references hello Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-toov2"></a><span data-ttu-id="bd695-118">Back-upserver toov2 upgraden</span><span class="sxs-lookup"><span data-stu-id="bd695-118">Upgrade Backup Server toov2</span></span>
<span data-ttu-id="bd695-119">tooupgrade van back-upserver van v1 tooBackup Server v2, Controleer of de installatie heeft Hallo vereiste updates:</span><span class="sxs-lookup"><span data-stu-id="bd695-119">tooupgrade from Backup Server v1 tooBackup Server v2, make sure your installation has hello required updates:</span></span>

- <span data-ttu-id="bd695-120">[Bijwerken van beveiligingsagents Hallo](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) op Hallo beveiligde servers.</span><span class="sxs-lookup"><span data-stu-id="bd695-120">[Update hello protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on hello protected servers.</span></span>
- <span data-ttu-id="bd695-121">Windows Server 2012 R2 tooWindows Server 2016 upgraden.</span><span class="sxs-lookup"><span data-stu-id="bd695-121">Upgrade Windows Server 2012 R2 tooWindows Server 2016.</span></span>
- <span data-ttu-id="bd695-122">Azure Backup-serverbeheerder voor extern bijwerken op alle productieservers.</span><span class="sxs-lookup"><span data-stu-id="bd695-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="bd695-123">Zorg ervoor dat de back-ups toocontinue zonder opnieuw opstarten van de productieserver zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="bd695-123">Ensure that backups are set toocontinue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="bd695-124">Stappen voor de upgrade voor back-upserver van v2</span><span class="sxs-lookup"><span data-stu-id="bd695-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="bd695-125">In Hallo Download Center [Hallo upgrade installatieprogramma downloaden](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="bd695-125">In hello Download Center, [download hello upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="bd695-126">Nadat u de wizard setup Hallo hebt uitgepakt, zorg ervoor dat **setup.exe uitvoeren** is geselecteerd en selecteer vervolgens **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="bd695-126">After you extract hello setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Installatieprogramma van de Setup - setup uitvoeren](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="bd695-128">In de wizard back-upserver van Microsoft Azure Hallo onder **installeren**, selecteer **Microsoft Azure Backup-Server**.</span><span class="sxs-lookup"><span data-stu-id="bd695-128">In hello Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Installatieprogramma van de Setup - Selecteer installeren](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="bd695-130">Op Hallo **Welkom** pagina, Hallo waarschuwingen bekijken en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bd695-130">On hello **Welcome** page, review hello warnings, and then select **Next**.</span></span>

  ![Installatieprogramma van de Setup - welkomstpagina](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="bd695-132">Hallo-installatiewizard voert controles van vereisten toomake ervoor dat uw omgeving een upgrade kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bd695-132">hello setup wizard performs prerequisite checks toomake sure your environment can upgrade.</span></span> <span data-ttu-id="bd695-133">Op Hallo **vereiste controleert** pagina **controleren**.</span><span class="sxs-lookup"><span data-stu-id="bd695-133">On hello **Prerequisite Checks** page, select **Check**.</span></span>

  ![Installatieprogramma van de Setup - vereisten controleert pagina](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="bd695-135">De vereiste controles Hallo moet voldoen aan uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="bd695-135">Your environment must pass hello prerequisite checks.</span></span> <span data-ttu-id="bd695-136">Als uw omgeving niet Hallo controles slaagt, houd er rekening mee Hallo problemen en los ze.</span><span class="sxs-lookup"><span data-stu-id="bd695-136">If your environment doesn't pass hello checks, note hello issues and fix them.</span></span> <span data-ttu-id="bd695-137">Selecteer **opnieuw controleren**.</span><span class="sxs-lookup"><span data-stu-id="bd695-137">Then, select **Check Again**.</span></span> <span data-ttu-id="bd695-138">Nadat u de vereiste controles Hallo doorgeven, selecteert u **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bd695-138">After you pass hello prerequisite checks, select **Next**.</span></span>

  ![Installatieprogramma van de Setup - opnieuw controleren](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="bd695-140">Op Hallo **SQL-instellingen** pagina, selecteert u de relevante optie Hallo voor uw installatie van SQL en selecteer vervolgens **controleren en installeren**.</span><span class="sxs-lookup"><span data-stu-id="bd695-140">On hello **SQL Settings** page, select hello relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Installatieprogramma van de Setup - pagina van de SQL-instellingen](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="bd695-142">Hallo controles kunnen enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="bd695-142">hello checks might take a few minutes.</span></span> <span data-ttu-id="bd695-143">Wanneer Hallo controles zijn voltooid, selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bd695-143">When hello checks are finished, select **Next**.</span></span>

  ![Installatieprogramma van de Setup - SQL-instellingen controleren en knop installeren](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="bd695-145">Op Hallo **installatie-instellingen** eventuele wijzigingen toohello locatie waar back-up-Server is geïnstalleerd of toohello scratchruimte locatie maken.</span><span class="sxs-lookup"><span data-stu-id="bd695-145">On hello **Installation Settings** page, make any changes toohello location where Backup Server is installed, or toohello Scratch Location.</span></span> <span data-ttu-id="bd695-146">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bd695-146">Select **Next**.</span></span>

  ![Installatieprogramma van de Setup - pagina installatie-instellingen](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="bd695-148">toofinish hello setup wizard selecteert u **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="bd695-148">toofinish hello setup wizard, select **Finish**.</span></span>

  ![Installatieprogramma van de Setup - voltooien](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="bd695-150">Opslag toevoegen voor moderne back-up-opslag</span><span class="sxs-lookup"><span data-stu-id="bd695-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="bd695-151">back-upserver v2-efficiëntie back-upopslag tooimprove voegt ondersteuning toe voor volumes.</span><span class="sxs-lookup"><span data-stu-id="bd695-151">tooimprove backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="bd695-152">Zoals back-upserver van v1 ondersteunt v2 back-upserver schijven.</span><span class="sxs-lookup"><span data-stu-id="bd695-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="bd695-153">Volumes en schijven toevoegen</span><span class="sxs-lookup"><span data-stu-id="bd695-153">Add volumes and disks</span></span>
<span data-ttu-id="bd695-154">Als u back-upserver v2 op Windows Server 2016 uitvoert, kunt u volumes toostore back-upgegevens.</span><span class="sxs-lookup"><span data-stu-id="bd695-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes toostore backup data.</span></span> <span data-ttu-id="bd695-155">Volumes bieden opslagbesparing en snellere back-ups.</span><span class="sxs-lookup"><span data-stu-id="bd695-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="bd695-156">Omdat volumes nieuwe tooBackup Server, moet u ze toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bd695-156">Because volumes are new tooBackup Server, you must add them.</span></span> 

<span data-ttu-id="bd695-157">Wanneer u een volume tooBackup Server toevoegt, kunt u Hallo volume een beschrijvende naam geven.</span><span class="sxs-lookup"><span data-stu-id="bd695-157">When you add a volume tooBackup Server, you can give hello volume a friendly name.</span></span> <span data-ttu-id="bd695-158">Klik op Hallo **beschrijvende naam** kolom Hallo volume dat u wilt dat tooname.</span><span class="sxs-lookup"><span data-stu-id="bd695-158">Click hello **Friendly Name** column of hello volume you want tooname.</span></span> <span data-ttu-id="bd695-159">U kunt Hallo naam later, indien nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bd695-159">You can change hello name later, if necessary.</span></span> <span data-ttu-id="bd695-160">U kunt ook gebruik van PowerShell tooadd of beschrijvende namen voor volumes wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bd695-160">You also can use PowerShell tooadd or change friendly names for volumes.</span></span>

<span data-ttu-id="bd695-161">tooadd een volume in Hallo Administrator-Console:</span><span class="sxs-lookup"><span data-stu-id="bd695-161">tooadd a volume in hello Administrator Console:</span></span>

1. <span data-ttu-id="bd695-162">Selecteer in hello Azure back-up Server Administrator-Console, **Management** > **schijfopslag** > **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bd695-162">In hello Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Open Hallo schijfopslag toevoegen-wizard](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="bd695-164">Hiermee opent u Hallo schijfopslag toevoegen-wizard.</span><span class="sxs-lookup"><span data-stu-id="bd695-164">This opens hello Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="bd695-165">Op Hallo **schijfopslag toevoegen** pagina in Hallo **beschikbare volumes** vak en selecteer vervolgens selecteert u een volume **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bd695-165">On hello **Add Disk Storage** page, in hello **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="bd695-166">In Hallo **volumes geselecteerd** vak en selecteer vervolgens een beschrijvende naam voor Hallo volume **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd695-166">In hello **Selected volumes** box, enter a friendly name for hello volume, and then select **OK**.</span></span>

      ![Schijfopslag wizard Add - volume toevoegen](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="bd695-168">Desgewenst kunt u een schijf tooadd behoren Hallo schijf tooa beveiligingsgroep met de oude opslag.</span><span class="sxs-lookup"><span data-stu-id="bd695-168">If you want tooadd a disk, hello disk must belong tooa protection group that has legacy storage.</span></span> <span data-ttu-id="bd695-169">Deze schijven kunnen alleen worden gebruikt voor deze beveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="bd695-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="bd695-170">Als back-upserver geen bronnen die oudere beveiliging, wordt niet Hallo schijf weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bd695-170">If Backup Server doesn't have sources that have legacy protection, hello disk isn't listed.</span></span>

  <span data-ttu-id="bd695-171">Zie voor meer informatie over het toevoegen van schijven [toe te voegen schijven tooincrease oude opslag](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="bd695-171">For more information about adding disks, see [Adding disks tooincrease legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="bd695-172">U kan een schijf een beschrijvende naam geven.</span><span class="sxs-lookup"><span data-stu-id="bd695-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-toovolumes"></a><span data-ttu-id="bd695-173">Werkbelastingen toovolumes toewijzen</span><span class="sxs-lookup"><span data-stu-id="bd695-173">Assign workloads toovolumes</span></span>

<span data-ttu-id="bd695-174">Back-up-server kunt u opgeven welke workloads toowhich volumes zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bd695-174">In Backup Server, you specify which workloads are assigned toowhich volumes.</span></span> <span data-ttu-id="bd695-175">U kunt bijvoorbeeld dure volumes die ondersteuning bieden voor een groot aantal i/o-bewerkingen per tweede (IOPS) toostore alleen werkbelastingen waarvoor frequente, hoog volume back-ups instellen.</span><span class="sxs-lookup"><span data-stu-id="bd695-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="bd695-176">Een voorbeeld is SQL Server met de transactielogboeken.</span><span class="sxs-lookup"><span data-stu-id="bd695-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="bd695-177">Update DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="bd695-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="bd695-178">tooupdate hello eigenschappen van een volume in de opslaggroep Hallo in back-upserver Hallo PowerShell-cmdlet Update-DPMDiskStorage gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bd695-178">tooupdate hello properties of a volume in hello storage pool in Backup Server, use hello PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="bd695-179">Syntaxis:</span><span class="sxs-lookup"><span data-stu-id="bd695-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="bd695-180">Alle wijzigingen die u maakt met behulp van PowerShell worden doorgevoerd in Hallo gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="bd695-180">All changes that you make by using PowerShell are reflected in hello UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="bd695-181">Gegevensbronnen beveiligen</span><span class="sxs-lookup"><span data-stu-id="bd695-181">Protect data sources</span></span>
<span data-ttu-id="bd695-182">toobegin het beschermen van de gegevensbronnen, maakt een beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="bd695-182">toobegin protecting data sources, create a protection group.</span></span> <span data-ttu-id="bd695-183">Hallo stappen markeren wijzigingen of toevoegingen toohello wizard nieuwe beveiligingsgroep te volgen.</span><span class="sxs-lookup"><span data-stu-id="bd695-183">hello following steps highlight changes or additions toohello New Protection Group wizard.</span></span>

<span data-ttu-id="bd695-184">toocreate een beveiligingsgroep:</span><span class="sxs-lookup"><span data-stu-id="bd695-184">toocreate a protection group:</span></span>

1. <span data-ttu-id="bd695-185">Selecteer in de beheerdersconsole van back-up Server Hallo, **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="bd695-185">In hello Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="bd695-186">Selecteer op het lint Hallo **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="bd695-186">On hello tool ribbon, select **New**.</span></span>

    <span data-ttu-id="bd695-187">Hiermee opent u de wizard voor Hallo nieuwe beveiligingsgroep maken.</span><span class="sxs-lookup"><span data-stu-id="bd695-187">This opens hello Create New Protection Group wizard.</span></span>

  ![Wizard nieuwe beveiligingsgroep maken](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="bd695-189">Op Hallo **Welkom** pagina **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bd695-189">On hello **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="bd695-190">Op Hallo **Type beveiligingsgroep selecteren** pagina, selecteert u Hallo type beveiligingsgroep die u wilt toocreate en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bd695-190">On hello **Select Protection Group Type** page, select hello type of protection group you want toocreate, and then select **Next**.</span></span>

  ![De pagina Type beveiligingsgroep selecteren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="bd695-192">Op Hallo **groepsleden selecteren** pagina in Hallo **beschikbare leden** deelvenster, Hallo leden met protection agents worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bd695-192">On hello **Select Group Members** page, in hello **Available members** pane, hello members with protection agents are listed.</span></span> <span data-ttu-id="bd695-193">Bijvoorbeeld, selecteert u volume D:\ en E:\ en voeg ze toohello **leden geselecteerd** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="bd695-193">For this example, select volume D:\ and E:\ and add them toohello **Selected members** pane.</span></span> <span data-ttu-id="bd695-194">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bd695-194">Select **Next**.</span></span>

  ![De pagina leden groep selecteren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="bd695-196">Op Hallo **methode voor gegevensbeveiliging selecteren** pagina, voert u een **naam beveiligingsgroep**, selecteer de beveiligingsmethode Hallo en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bd695-196">On hello **Select Data Protection Method** page, enter a **Protection group name**, select hello protection method, and then select **Next**.</span></span> <span data-ttu-id="bd695-197">Als u beveiliging op korte termijn wilt, moet u Hallo **schijf** back-up van methode.</span><span class="sxs-lookup"><span data-stu-id="bd695-197">If you want short-term protection, you must select hello **Disk** backup method.</span></span>

  ![De pagina methode voor gegevensbeveiliging selecteren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="bd695-199">Op Hallo **Kortetermijndoelen opgeven** pagina, selecteer Hallo details voor **bewaartermijn** en **Synchronisatiefrequentie**.</span><span class="sxs-lookup"><span data-stu-id="bd695-199">On hello **Specify Short-Term Goals** page, select hello details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="bd695-200">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bd695-200">Then, select **Next**.</span></span> <span data-ttu-id="bd695-201">Eventueel toochange Hallo planning voor wanneer herstelpunten genomen, selecteer zijn **wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="bd695-201">Optionally, toochange hello schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Pagina Kortetermijndoelen opgeven](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="bd695-203">Op Hallo **toewijzing van schijfopslag controleren** pagina bekijkt u meer informatie over het Hallo-gegevensbronnen die u hebt geselecteerd, hun grootte en de waarden voor Hallo ruimte toobe ingericht en Hallo doel opslagvolume.</span><span class="sxs-lookup"><span data-stu-id="bd695-203">On hello **Review Disk Storage Allocation** page, review details about hello data sources you selected, their size, and  values for hello space toobe provisioned and hello target storage volume.</span></span>

  ![Pagina van de toewijzing van schijfopslag controleren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="bd695-205">Opslagvolumes zijn gebaseerd op Hallo werkbelasting volume toewijzing (ingesteld met behulp van PowerShell) en Hallo beschikbare opslag.</span><span class="sxs-lookup"><span data-stu-id="bd695-205">Storage volumes are based on hello workload volume allocation (set by using PowerShell) and hello available storage.</span></span> <span data-ttu-id="bd695-206">U kunt Hallo opslagvolumes wijzigen door het selecteren van andere volumes in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd695-206">You can change hello storage volumes by selecting other volumes in hello drop-down menu.</span></span> <span data-ttu-id="bd695-207">Als u de waarde voor Hallo wijzigt **Doelopslag**, Hallo waarde voor **beschikbaar schijfopslag** dynamisch gewijzigd tooreflect waarden onder **vrije ruimte** en **Underprovisioned ruimte**.</span><span class="sxs-lookup"><span data-stu-id="bd695-207">If you change hello value for **Target Storage**, hello value for **Available disk storage** dynamically changes tooreflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="bd695-208">Als gegevensbronnen Hallo toenemen als gepland, de waarde voor Hallo Hallo **Underprovisioned ruimte** kolom in **beschikbaar schijfopslag** weerspiegelt Hallo hoeveelheid extra opslagruimte die nodig is.</span><span class="sxs-lookup"><span data-stu-id="bd695-208">If hello data sources grow as planned, hello value for hello **Underprovisioned Space** column in **Available disk storage** reflects hello amount of additional storage that's needed.</span></span> <span data-ttu-id="bd695-209">Gebruik deze waarde toohelp plan uw opslag nodig voor goede back-ups.</span><span class="sxs-lookup"><span data-stu-id="bd695-209">Use this value toohelp plan your storage needs for smooth backups.</span></span> <span data-ttu-id="bd695-210">Als het Hallo-waarde nul is, moet u er geen mogelijke problemen met opslag in de nabije toekomst Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="bd695-210">If hello value is zero, there are no potential problems with storage in hello foreseeable future.</span></span> <span data-ttu-id="bd695-211">Als Hallo een getal dan nul is, u hoeft niet voldoende opslag die is toegewezen (op basis van uw beveiliging beleid en Hallo gegevensgrootte van uw beveiligde leden).</span><span class="sxs-lookup"><span data-stu-id="bd695-211">If hello value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and hello data size of your protected members).</span></span>

  ![Onderbezette schijfopslag](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="bd695-213">toofinish maken van de wizard beveiligingsgroep groeperen en volledige Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd695-213">toofinish creating your protection group, complete hello wizard.</span></span>

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a><span data-ttu-id="bd695-214">Verouderde opslag tooModern back-up opslag migreren</span><span class="sxs-lookup"><span data-stu-id="bd695-214">Migrate legacy storage tooModern Backup Storage</span></span>
<span data-ttu-id="bd695-215">Na de upgrade tooor installeren back-upserver van v2 en upgrade Hallo besturingssysteem tooWindows Server 2016, werk uw beveiliging groepen toouse moderne back-up-opslag.</span><span class="sxs-lookup"><span data-stu-id="bd695-215">After you upgrade tooor install Backup Server v2 and upgrade hello operating system tooWindows Server 2016, update your protection groups toouse Modern Backup Storage.</span></span> <span data-ttu-id="bd695-216">Standaard zijn beveiligingsgroepen niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="bd695-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="bd695-217">Ze blijven toofunction als ze in eerste instantie zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="bd695-217">They continue toofunction as they were initially set up.</span></span> 

<span data-ttu-id="bd695-218">Bijwerken van beveiliging groepen toouse moderne back-up-opslag is optioneel.</span><span class="sxs-lookup"><span data-stu-id="bd695-218">Updating protection groups toouse Modern Backup Storage is optional.</span></span> <span data-ttu-id="bd695-219">beveiligingsgroep tooupdate hello, stop de beveiliging van alle gegevensbronnen met behulp van Hallo behouden gegevensoptie.</span><span class="sxs-lookup"><span data-stu-id="bd695-219">tooupdate hello protection group, stop protection of all data sources by using hello retain data option.</span></span> <span data-ttu-id="bd695-220">Vervolgens voegt u Hallo gegevensbronnen tooa nieuwe beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="bd695-220">Then, add hello data sources tooa new protection group.</span></span>

1. <span data-ttu-id="bd695-221">Selecteer in de Hallo Administrator-Console, Hallo **beveiliging** functie.</span><span class="sxs-lookup"><span data-stu-id="bd695-221">In hello Administrator Console, select hello **Protection** feature.</span></span> <span data-ttu-id="bd695-222">In Hallo **Beveiligingsgroepslid** lijst en selecteer vervolgens met de rechtermuisknop op Hallo lid **beveiliging van lid stoppen**.</span><span class="sxs-lookup"><span data-stu-id="bd695-222">In hello **Protection Group Member** list, right-click hello member, and then select **Stop protection of member**.</span></span>

  ![Beveiliging van lid stoppen](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="bd695-224">In Hallo **verwijderen uit groep** in het dialoogvenster, bekijk Hallo gebruikt schijfruimte vrij en Hallo beschikbare vrije ruimte voor Hallo-opslaggroep.</span><span class="sxs-lookup"><span data-stu-id="bd695-224">In hello **Remove from Group** dialog box, review hello used disk space and hello available free space for hello storage pool.</span></span> <span data-ttu-id="bd695-225">Hallo standaard tooleave Hallo herstelpunten op schijf Hallo is en dat deze tooexpire per hun bijbehorende bewaarbeleid.</span><span class="sxs-lookup"><span data-stu-id="bd695-225">hello default is tooleave hello recovery points on hello disk and allow them tooexpire per their associated retention policy.</span></span> <span data-ttu-id="bd695-226">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd695-226">Click **OK**.</span></span>

  <span data-ttu-id="bd695-227">Als u tooimmediately return Hallo gebruikt ruimte toohello gratis schijfopslaggroep wilt, selecteert u Hallo **replica op schijf verwijderen** selectievakje toodelete Hallo back-upgegevens (en herstelpunten) die zijn gekoppeld aan dit lid.</span><span class="sxs-lookup"><span data-stu-id="bd695-227">If you want tooimmediately return hello used disk space toohello free storage pool, select hello **Delete replica on disk** check box toodelete hello backup data (and recovery points) associated with that member.</span></span>

  ![Dialoogvenster groep verwijderen](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="bd695-229">Maak een beveiligingsgroep die gebruik maakt van opslag voor moderne back-up.</span><span class="sxs-lookup"><span data-stu-id="bd695-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="bd695-230">Hallo onbeveiligd gegevensbronnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="bd695-230">Include hello unprotected data sources.</span></span>


## <a name="add-disks-tooincrease-legacy-storage"></a><span data-ttu-id="bd695-231">Schijven tooincrease oude opslag toevoegen</span><span class="sxs-lookup"><span data-stu-id="bd695-231">Add disks tooincrease legacy storage</span></span>

<span data-ttu-id="bd695-232">Als u oude opslag met back-upserver toouse wilt, moet u mogelijk tooadd schijven tooincrease oude opslag.</span><span class="sxs-lookup"><span data-stu-id="bd695-232">If you want toouse legacy storage with Backup Server, you might need tooadd disks tooincrease legacy storage.</span></span> 

<span data-ttu-id="bd695-233">schijfopslag tooadd:</span><span class="sxs-lookup"><span data-stu-id="bd695-233">tooadd disk storage:</span></span>

1. <span data-ttu-id="bd695-234">Selecteer in de Hallo Administrator-Console, **Management** > **schijfopslag** > **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bd695-234">In hello Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Schijfopslag dialoogvenster toevoegen](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="bd695-236">In Hallo **schijfopslag toevoegen** dialoogvenster Selecteer **schijven toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bd695-236">In hello **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="bd695-237">Selecteer in Hallo lijst met beschikbare schijven Hallo schijven die u wilt dat tooadd, selecteer **toevoegen**, en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd695-237">In hello list of available disks, select hello disks you want tooadd, select **Add**, and then select **OK**.</span></span>

## <a name="update-hello-data-protection-manager-protection-agent"></a><span data-ttu-id="bd695-238">Hallo Data Protection Manager protection agent bijwerken</span><span class="sxs-lookup"><span data-stu-id="bd695-238">Update hello Data Protection Manager protection agent</span></span>

<span data-ttu-id="bd695-239">Back-upserver maakt gebruik van System Center Data Protection Manager-beveiligingsagent Hallo voor updates.</span><span class="sxs-lookup"><span data-stu-id="bd695-239">Backup Server uses hello System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="bd695-240">Als u een beveiligingsagent dat geen netwerk verbonden toohello bijwerkt, kunt u Hallo toocomplete Data Protection Manager Administrator-Console de upgrade van een verbonden agent niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bd695-240">If you are upgrading a protection agent that is not connected toohello network, you cannot use hello Data Protection Manager Administrator Console toocomplete a connected agent upgrade.</span></span> <span data-ttu-id="bd695-241">De beveiligingsagent Hallo in een niet-actieve domeinomgeving, moet u upgraden.</span><span class="sxs-lookup"><span data-stu-id="bd695-241">You must upgrade hello protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="bd695-242">Tot Hallo-clientcomputer verbonden toohello netwerk is, is Hallo die Data Protection Manager Administrator-Console ziet u dat Hallo update van de beveiligingsagent in behandeling.</span><span class="sxs-lookup"><span data-stu-id="bd695-242">Until hello client computer is connected toohello network, hello Data Protection Manager Administrator Console shows that hello protection agent update is pending.</span></span>

<span data-ttu-id="bd695-243">Hallo volgende secties wordt beschreven hoe de beveiligingsagents tooupdate voor clientcomputers die zijn verbonden en clientcomputers die niet zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="bd695-243">hello following sections describe how tooupdate protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="bd695-244">Een beveiligingsagent voor een verbonden clientcomputer bijwerken</span><span class="sxs-lookup"><span data-stu-id="bd695-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="bd695-245">Selecteer in de beheerdersconsole van back-up Server Hallo, **Management** > **Agents**.</span><span class="sxs-lookup"><span data-stu-id="bd695-245">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="bd695-246">Selecteer in weergavepaneel Hallo Hallo clientcomputers waarvoor u tooupdate Hallo-beveiligingsagent wilt.</span><span class="sxs-lookup"><span data-stu-id="bd695-246">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="bd695-247">Hallo **agentupdates** kolom wordt aangegeven wanneer een update van de beveiligingsagent beschikbaar is voor elke beveiligde computer.</span><span class="sxs-lookup"><span data-stu-id="bd695-247">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="bd695-248">In Hallo **acties** deelvenster, Hallo **Update** actie is alleen beschikbaar wanneer een beveiligde computer is geselecteerd en er updates beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="bd695-248">In hello **Actions** pane, hello **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="bd695-249">tooinstall bijgewerkt beveiligingsagents op geselecteerde Hallo-computers in Hallo **acties** deelvenster **Update**.</span><span class="sxs-lookup"><span data-stu-id="bd695-249">tooinstall updated protection agents on hello selected computers, in hello **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="bd695-250">Een beveiligingsagent op een clientcomputer die niet verbonden bijwerken</span><span class="sxs-lookup"><span data-stu-id="bd695-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="bd695-251">Selecteer in de beheerdersconsole van back-up Server Hallo, **Management** > **Agents**.</span><span class="sxs-lookup"><span data-stu-id="bd695-251">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="bd695-252">Selecteer in weergavepaneel Hallo Hallo clientcomputers waarvoor u tooupdate Hallo-beveiligingsagent wilt.</span><span class="sxs-lookup"><span data-stu-id="bd695-252">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="bd695-253">Hallo **agentupdates** kolom wordt aangegeven wanneer een update van de beveiligingsagent beschikbaar is voor elke beveiligde computer.</span><span class="sxs-lookup"><span data-stu-id="bd695-253">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="bd695-254">In Hallo **acties** deelvenster, Hallo **Update** actie is niet beschikbaar wanneer een beveiligde computer is geselecteerd tenzij er updates beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="bd695-254">In hello **Actions** pane, hello **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="bd695-255">tooinstall bijgewerkt beveiligingsagents op computers met Hallo geselecteerd, selecteer **Update**.</span><span class="sxs-lookup"><span data-stu-id="bd695-255">tooinstall updated protection agents on hello selected computers, select **Update**.</span></span>

4. <span data-ttu-id="bd695-256">Voor een clientcomputer die niet netwerk toohello, verbonden totdat het Hallo-computer is verbonden toohello netwerk, Hallo **agentstatus** kolom ziet u de status van **Update in behandeling**.</span><span class="sxs-lookup"><span data-stu-id="bd695-256">For a client computer that is not connected toohello network, until hello computer is connected toohello network, hello **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="bd695-257">Nadat een clientcomputer verbonden toohello netwerk is, Hallo **agentupdates** kolom voor de clientcomputer Hallo ziet u de status van **Updating**.</span><span class="sxs-lookup"><span data-stu-id="bd695-257">After a client computer is connected toohello network, hello **Agent Updates** column for hello client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a><span data-ttu-id="bd695-258">Verouderde beveiligingsgroepen van oude en nieuwe versie van synchronisatie Hallo met Azure verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bd695-258">Move legacy Protection groups from old version and sync hello new version with Azure</span></span>

<span data-ttu-id="bd695-259">Wanneer zowel Azure Backup-Server en Hallo OS worden bijgewerkt, bent u klaar tooprotect nieuwe gegevensbronnen moderne back-up-opslag.</span><span class="sxs-lookup"><span data-stu-id="bd695-259">Once Azure Backup Server and hello OS are both updated, you are ready tooprotect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="bd695-260">Echter al beveiligde gegevensbronnen blijft toobe beveiligd in de verouderde Hallo manier zoals ze in Azure Backup-Server waren maar alle nieuwe bescherming moderne back-up-opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bd695-260">However already protected data sources will continue toobe protected in hello legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="bd695-261">Onderstaande stappen zijn toomigrate gegevensbronnen van de legacy-modus van beveiliging tooModern back-upopslag.</span><span class="sxs-lookup"><span data-stu-id="bd695-261">Below steps are toomigrate data sources from legacy  mode of protection tooModern backup storage.</span></span>

<span data-ttu-id="bd695-262">• Hallo nieuwe volumes toohello DPM-opslaggroep toevoegen en beschrijvende namen en data source-labels toewijzen indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="bd695-262">• Add hello new volume(s) toohello DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="bd695-263">• Voor elke gegevensbron die in de legacy-modus, stop de beveiliging van gegevensbronnen van Hallo en 'Beveiligde gegevens behouden'.</span><span class="sxs-lookup"><span data-stu-id="bd695-263">• For each data source that is in legacy mode, stop protection of hello data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="bd695-264">Hierdoor kan herstel van de oude herstelpunten na de migratie.</span><span class="sxs-lookup"><span data-stu-id="bd695-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="bd695-265">• Maken van een nieuwe pagina en selecteer Hallo gegevensbronnen die zijn opgeslagen met behulp van de nieuwe indeling toobe.</span><span class="sxs-lookup"><span data-stu-id="bd695-265">• Create a new PG and select hello data sources that are toobe stored using new format.</span></span>
<span data-ttu-id="bd695-266">• DPM wordt een kopie van de replica doen vanuit oudere back-upopslag Hallo in Hallo moderne back-upopslag volume lokaal.</span><span class="sxs-lookup"><span data-stu-id="bd695-266">• DPM will do a replica copy from hello legacy backup storage into hello Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="bd695-267">Opmerking: Deze wordt gezien als een na een herstelbewerking wordt uitgevoerd taak • alle nieuwe punten voor synchronisatie en herstel vervolgens worden opgeslagen in moderne back-up-opslag.</span><span class="sxs-lookup"><span data-stu-id="bd695-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="bd695-268">• Oude herstelpunten worden verwijderd uit als ze verlopen en uiteindelijk Hallo-schijfruimte vrij.</span><span class="sxs-lookup"><span data-stu-id="bd695-268">• Old recovery points will be pruned out as they expire and eventually free up hello disk space.</span></span>
<span data-ttu-id="bd695-269">• Zodra alle Hallo verouderde volumes zijn verwijderd uit de oude opslag hello, Hallo schijf kunnen worden verwijderd uit Azure back-up en het Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="bd695-269">• Once all hello legacy volumes are deleted from hello old storage, hello disk can be removed from Azure backup and hello system.</span></span>
<span data-ttu-id="bd695-270">• Maak een back-up van hello Azure DPMDB.</span><span class="sxs-lookup"><span data-stu-id="bd695-270">• Take a backup of hello  Azure DPMDB.</span></span>

<span data-ttu-id="bd695-271">Deel 2:-belangrijke zaken > Hallo nieuwe server moet toobe met de dezelfde naam als Hallo oorspronkelijke Azure Backup-server.</span><span class="sxs-lookup"><span data-stu-id="bd695-271">Part 2: -Important items> hello new server will need toobe named same as hello original Azure Backup server.</span></span> <span data-ttu-id="bd695-272">U kunt Hallo-naam van Hallo nieuwe Azure Backup-server niet wijzigen als u wilt dat oude opslaggroep toouse en DPMDB tooretain-herstelpunten -, is de back-up van DPMDB hebt moet zoals toobe hersteld moet</span><span class="sxs-lookup"><span data-stu-id="bd695-272">You cannot change hello name of hello new Azure backup server if you want toouse old storage pool and DPMDB tooretain recovery points -Must have backup of DPMDB  as it will need toobe restored</span></span>

1) <span data-ttu-id="bd695-273">Afsluiten Hallo oorspronkelijke Azure Backup-server of weghalen Hallo-kabel.</span><span class="sxs-lookup"><span data-stu-id="bd695-273">Shutdown hello original Azure backup server or take it off hello wire.</span></span>
2) <span data-ttu-id="bd695-274">Hallo-computeraccount in active directory herstellen.</span><span class="sxs-lookup"><span data-stu-id="bd695-274">Reset hello machine account in active directory.</span></span>
3) <span data-ttu-id="bd695-275">Server 2016 op nieuwe machine en de naam van het Hallo dezelfde computernaam als Hallo oorspronkelijke Azure Backup-server installeren.</span><span class="sxs-lookup"><span data-stu-id="bd695-275">Install Server 2016 on new machine and name it hello same machine name as hello original Azure Backup server.</span></span>
4) <span data-ttu-id="bd695-276">Hallo domein koppelen</span><span class="sxs-lookup"><span data-stu-id="bd695-276">Join hello Domain</span></span>
5) <span data-ttu-id="bd695-277">Installeer Azure Backup-server V2 (verplaatsen DPM-opslaggroepschijven van de oude server en importeer)</span><span class="sxs-lookup"><span data-stu-id="bd695-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="bd695-278">Hallo DPMDB overgenomen uit het einde van deel 2 herstellen</span><span class="sxs-lookup"><span data-stu-id="bd695-278">Restore hello DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="bd695-279">Hallo opslag van Hallo oorspronkelijke back-upserver toohello nieuwe server koppelen.</span><span class="sxs-lookup"><span data-stu-id="bd695-279">Attach hello storage from hello original backup server toohello new server.</span></span>
8) <span data-ttu-id="bd695-280">Hallo DPMDB van SQL herstellen</span><span class="sxs-lookup"><span data-stu-id="bd695-280">From SQL Restore hello DPMDB</span></span>
9) <span data-ttu-id="bd695-281">Installeren vanaf de opdrachtregel beheerder op de nieuwe server cd tooMicrosoft Azure Backup-locatie en de bin-map</span><span class="sxs-lookup"><span data-stu-id="bd695-281">From admin command line on new server cd tooMicrosoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="bd695-282">Voorbeeld van pad: C:\windows\system32 > cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="bd695-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="bd695-283">back-up tooAzure Voer DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="bd695-283">tooAzure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="bd695-284">Voer DPMSYNC-SYNC-Opmerking Als u nieuwe schijven toohello DPM opslaggroep in plaats van de oude versie Hallo verplaatsen hebt toegevoegd Voer DPMSYNC - reallocatereplica uit</span><span class="sxs-lookup"><span data-stu-id="bd695-284">Run DPMSYNC -SYNC Note If you have added NEW disks toohello DPM Storage pool instead of moving hello old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="bd695-285">Nieuwe PowerShell-cmdlets in v2</span><span class="sxs-lookup"><span data-stu-id="bd695-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="bd695-286">Wanneer u v2 voor Azure Backup-Server installeert, zijn twee nieuwe cmdlets zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="bd695-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="bd695-287">Koppelpunt DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="bd695-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="bd695-288">Ontkoppeling DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="bd695-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="bd695-289">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bd695-289">Next steps</span></span>

<span data-ttu-id="bd695-290">Meer informatie over hoe tooprepare uw server of met het beveiligen van een werkbelasting beginnen:</span><span class="sxs-lookup"><span data-stu-id="bd695-290">Learn how tooprepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="bd695-291">Back-upserver van werkbelastingen voorbereiden</span><span class="sxs-lookup"><span data-stu-id="bd695-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="bd695-292">Back-upserver tooback van een VMware-server gebruiken</span><span class="sxs-lookup"><span data-stu-id="bd695-292">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="bd695-293">Back-upserver tooback van SQL Server gebruiken</span><span class="sxs-lookup"><span data-stu-id="bd695-293">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="bd695-294">Moderne back-upopslag met back-upserver gebruiken</span><span class="sxs-lookup"><span data-stu-id="bd695-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

