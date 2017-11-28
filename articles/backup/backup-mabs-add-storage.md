---
title: aaaUse moderne Backup Storage met Azure Backup-Server v2 | Microsoft Docs
description: Meer informatie over nieuwe functies in Azure Backup-Server v2 Hallo. Dit artikel wordt beschreven hoe tooupgrade uw back-up-Server-installatie.
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
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="6ac10-104">Toevoegen van opslag tooAzure back-upserver van v2</span><span class="sxs-lookup"><span data-stu-id="6ac10-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="6ac10-105">Azure Backup Server v2 wordt geleverd met System Center 2016 Data Protection Manager moderne back-up opslag.</span><span class="sxs-lookup"><span data-stu-id="6ac10-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="6ac10-106">Moderne back-up Storage biedt opslagbesparing van 50 procent van de back-ups die drie keer snellere en efficiëntere opslag.</span><span class="sxs-lookup"><span data-stu-id="6ac10-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="6ac10-107">Biedt ook werkbelasting-bewuste opslag.</span><span class="sxs-lookup"><span data-stu-id="6ac10-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="6ac10-108">toouse moderne back-up-opslag, moet u back-upserver van v2 uitvoeren op Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6ac10-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="6ac10-109">Als u een back-upserver van v2 op een eerdere versie van Windows Server uitvoert, kan niet Azure Backup-Server profiteren van moderne back-up-opslag.</span><span class="sxs-lookup"><span data-stu-id="6ac10-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="6ac10-110">In plaats daarvan beveiligt het werkbelastingen zoals met back-upserver van v1.</span><span class="sxs-lookup"><span data-stu-id="6ac10-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="6ac10-111">Zie voor meer informatie, Hallo back-upserver versie [beveiliging matrix](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="6ac10-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="6ac10-112">Volumes in de back-upserver v2</span><span class="sxs-lookup"><span data-stu-id="6ac10-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="6ac10-113">Back-Server v2 accepteert opslagvolumes.</span><span class="sxs-lookup"><span data-stu-id="6ac10-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="6ac10-114">Wanneer u een volume toevoegt, indelingen back-upserver Hallo volume tooResilient File System (ReFS), waarvoor moderne back-up-opslag is vereist.</span><span class="sxs-lookup"><span data-stu-id="6ac10-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="6ac10-115">een volume tooadd en tooexpand later als u wilt het is raadzaam dat u deze werkstroom:</span><span class="sxs-lookup"><span data-stu-id="6ac10-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="6ac10-116">Back-upserver van v2 op een virtuele machine instellen.</span><span class="sxs-lookup"><span data-stu-id="6ac10-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="6ac10-117">Maak een volume op een virtuele schijf in een opslaggroep:</span><span class="sxs-lookup"><span data-stu-id="6ac10-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="6ac10-118">Voeg een schijf tooa-opslaggroep en een virtuele schijf maken met eenvoudige indeling.</span><span class="sxs-lookup"><span data-stu-id="6ac10-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="6ac10-119">Voeg eventuele extra schijven en Hallo virtuele schijf uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="6ac10-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="6ac10-120">Volumes op Hallo virtuele schijf maken.</span><span class="sxs-lookup"><span data-stu-id="6ac10-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="6ac10-121">Hallo volumes tooBackup Server toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6ac10-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="6ac10-122">Werkbelasting-bewuste opslag configureren.</span><span class="sxs-lookup"><span data-stu-id="6ac10-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="6ac10-123">Een volume maken voor moderne back-up-opslag</span><span class="sxs-lookup"><span data-stu-id="6ac10-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="6ac10-124">Met behulp van back-upserver van v2 met volumes als schijfopslag kunt u controle over opslag.</span><span class="sxs-lookup"><span data-stu-id="6ac10-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="6ac10-125">Een volume kan één schijf zijn.</span><span class="sxs-lookup"><span data-stu-id="6ac10-125">A volume can be a single disk.</span></span> <span data-ttu-id="6ac10-126">Als u wilt dat toekomstige tooextend opslag in hello, echter een volume buiten een schijf die is gemaakt met behulp van opslagruimten maken.</span><span class="sxs-lookup"><span data-stu-id="6ac10-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="6ac10-127">Zo kunt u indien tooexpand Hallo volume voor back-up gewenst.</span><span class="sxs-lookup"><span data-stu-id="6ac10-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="6ac10-128">Deze sectie vindt u aanbevolen procedures voor het maken van een volume met deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="6ac10-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="6ac10-129">Selecteer in Serverbeheer **File and Storage Services** > **Volumes** > **opslaggroepen**.</span><span class="sxs-lookup"><span data-stu-id="6ac10-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="6ac10-130">Onder **fysieke schijven**, selecteer **nieuwe opslaggroep**.</span><span class="sxs-lookup"><span data-stu-id="6ac10-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Een nieuwe opslaggroep maken](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="6ac10-132">In Hallo **taken** vervolgkeuzelijst, selecteer **nieuwe virtuele schijf**.</span><span class="sxs-lookup"><span data-stu-id="6ac10-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Een virtuele schijf toevoegen](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="6ac10-134">Selecteer de opslaggroep Hallo en selecteer vervolgens **fysieke schijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6ac10-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![Toevoegen van een fysieke schijf](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="6ac10-136">Selecteer de fysieke schijf Hallo en selecteer vervolgens **virtuele schijf uitbreiden**.</span><span class="sxs-lookup"><span data-stu-id="6ac10-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Hallo virtuele schijf uitbreiden](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="6ac10-138">Selecteer Hallo virtuele schijf en selecteer vervolgens **NieuwVolume**.</span><span class="sxs-lookup"><span data-stu-id="6ac10-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![Maak een nieuw volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="6ac10-140">In Hallo **Hallo-server en schijf selecteren** dialoogvenster, selecteer Hallo-server en de nieuwe schijf Hallo.</span><span class="sxs-lookup"><span data-stu-id="6ac10-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="6ac10-141">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="6ac10-141">Then, select **Next**.</span></span>

    ![Hallo-server en schijf selecteren](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="6ac10-143">Volumes tooBackup Server schijfopslag toevoegen</span><span class="sxs-lookup"><span data-stu-id="6ac10-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="6ac10-144">een volume tooBackup-Server in Hallo tooadd **Management** deelvenster Hallo opslag opnieuw scannen en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6ac10-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="6ac10-145">Er verschijnt een lijst met alle Hallo volumes beschikbaar toobe toegevoegd voor de opslag van back-up-Server.</span><span class="sxs-lookup"><span data-stu-id="6ac10-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="6ac10-146">Nadat beschikbare volumes zijn toegevoegd toohello lijst met geselecteerde volumes, kunt u ze een beschrijvende naam toohelp u ze beheren geven.</span><span class="sxs-lookup"><span data-stu-id="6ac10-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="6ac10-147">deze volumes tooReFS zodat back-upserver Hallo voordelen van moderne back-up-opslag kunt, selecteer tooformat **OK**.</span><span class="sxs-lookup"><span data-stu-id="6ac10-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![Toevoegen van de beschikbare Volumes](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="6ac10-149">Werkbelasting-bewuste opslag instellen</span><span class="sxs-lookup"><span data-stu-id="6ac10-149">Set up workload-aware storage</span></span>

<span data-ttu-id="6ac10-150">Met de werkbelasting-bewuste opslag, kunt u Hallo volumes waarop bepaalde soorten belasting bij voorkeur zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6ac10-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="6ac10-151">U kunt bijvoorbeeld dure volumes die ondersteuning bieden voor een groot aantal i/o-bewerkingen per tweede (IOPS) toostore alleen Hallo werkbelastingen waarvoor frequente, hoog volume back-ups instellen.</span><span class="sxs-lookup"><span data-stu-id="6ac10-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="6ac10-152">Een voorbeeld is SQL Server met de transactielogboeken.</span><span class="sxs-lookup"><span data-stu-id="6ac10-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="6ac10-153">Andere werkbelastingen zijn back-ups minder vaak, zoals virtuele machines, kunnen worden back-up toolow kosten volumes.</span><span class="sxs-lookup"><span data-stu-id="6ac10-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="6ac10-154">Update DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="6ac10-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="6ac10-155">U kunt de werkbelasting-bewuste opslag instellen met behulp van PowerShell-cmdlet Hallo Update-DPMDiskStorage die Hallo eigenschappen van een volume in de opslaggroep Hallo op een server met Data Protection Manager-updates.</span><span class="sxs-lookup"><span data-stu-id="6ac10-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="6ac10-156">Syntaxis:</span><span class="sxs-lookup"><span data-stu-id="6ac10-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="6ac10-157">Hallo volgende schermafbeelding ziet u Hallo Update DPMDiskStorage cmdlet in Hallo PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="6ac10-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![Hallo Update DPMDiskStorage opdracht in Hallo PowerShell-venster](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="6ac10-159">Hallo-wijzigingen die u aanbrengt met behulp van PowerShell worden doorgevoerd in Hallo back-up Server Administrator-Console.</span><span class="sxs-lookup"><span data-stu-id="6ac10-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![Schijven en volumes in Hallo Administrator-Console](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="6ac10-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6ac10-161">Next steps</span></span>
<span data-ttu-id="6ac10-162">Nadat u de back-up-Server hebt geïnstalleerd, informatie over hoe tooprepare uw server, of met het beveiligen van een werkbelasting beginnen.</span><span class="sxs-lookup"><span data-stu-id="6ac10-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="6ac10-163">Back-upserver van werkbelastingen voorbereiden</span><span class="sxs-lookup"><span data-stu-id="6ac10-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="6ac10-164">Back-upserver tooback van een VMware-server gebruiken</span><span class="sxs-lookup"><span data-stu-id="6ac10-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="6ac10-165">Back-upserver tooback van SQL Server gebruiken</span><span class="sxs-lookup"><span data-stu-id="6ac10-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

