---
title: Moderne back-upopslag gebruiken met Azure Backup-Server v2 | Microsoft Docs
description: Meer informatie over de nieuwe functies in v2 voor Azure Backup-Server. In dit artikel wordt beschreven hoe een back-upserver van upgrade.
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
ms.openlocfilehash: 751b9b495fd368dff1f72429707f5f33a0ccb569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-storage-to-azure-backup-server-v2"></a><span data-ttu-id="81c42-104">Opslag toevoegen aan Azure Backup-Server v2</span><span class="sxs-lookup"><span data-stu-id="81c42-104">Add storage to Azure Backup Server v2</span></span>

<span data-ttu-id="81c42-105">Azure Backup Server v2 wordt geleverd met System Center 2016 Data Protection Manager moderne back-up opslag.</span><span class="sxs-lookup"><span data-stu-id="81c42-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="81c42-106">Moderne back-up Storage biedt opslagbesparing van 50 procent van de back-ups die drie keer snellere en efficiëntere opslag.</span><span class="sxs-lookup"><span data-stu-id="81c42-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="81c42-107">Biedt ook werkbelasting-bewuste opslag.</span><span class="sxs-lookup"><span data-stu-id="81c42-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="81c42-108">Voor het gebruik van moderne back-up-opslag, moet u back-upserver van v2 uitvoeren op Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="81c42-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="81c42-109">Als u een back-upserver van v2 op een eerdere versie van Windows Server uitvoert, kan niet Azure Backup-Server profiteren van moderne back-up-opslag.</span><span class="sxs-lookup"><span data-stu-id="81c42-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="81c42-110">In plaats daarvan beveiligt het werkbelastingen zoals met back-upserver van v1.</span><span class="sxs-lookup"><span data-stu-id="81c42-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="81c42-111">Zie voor meer informatie, de versie van de back-upserver [beveiliging matrix](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="81c42-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="81c42-112">Volumes in de back-upserver v2</span><span class="sxs-lookup"><span data-stu-id="81c42-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="81c42-113">Back-Server v2 accepteert opslagvolumes.</span><span class="sxs-lookup"><span data-stu-id="81c42-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="81c42-114">Wanneer u een volume toevoegt, indelingen back-upserver van het volume Resilient File System (ReFS), waarvoor moderne back-up-opslag is vereist.</span><span class="sxs-lookup"><span data-stu-id="81c42-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="81c42-115">Een volume toevoegen en later uitbreiden als u wilt, het is raadzaam dat u deze werkstroom:</span><span class="sxs-lookup"><span data-stu-id="81c42-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="81c42-116">Back-upserver van v2 op een virtuele machine instellen.</span><span class="sxs-lookup"><span data-stu-id="81c42-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="81c42-117">Maak een volume op een virtuele schijf in een opslaggroep:</span><span class="sxs-lookup"><span data-stu-id="81c42-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="81c42-118">Een schijf toevoegen aan een opslaggroep en een virtuele schijf maken met eenvoudige indeling.</span><span class="sxs-lookup"><span data-stu-id="81c42-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="81c42-119">Eventuele extra schijven toevoegen en uitbreiden van de virtuele schijf.</span><span class="sxs-lookup"><span data-stu-id="81c42-119">Add any additional disks, and extend the virtual disk.</span></span>
    3.  <span data-ttu-id="81c42-120">Volumes op de virtuele schijf maken.</span><span class="sxs-lookup"><span data-stu-id="81c42-120">Create volumes on the virtual disk.</span></span>
3.  <span data-ttu-id="81c42-121">De volumes toevoegen aan back-upserver.</span><span class="sxs-lookup"><span data-stu-id="81c42-121">Add the volumes to Backup Server.</span></span>
4.  <span data-ttu-id="81c42-122">Werkbelasting-bewuste opslag configureren.</span><span class="sxs-lookup"><span data-stu-id="81c42-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="81c42-123">Een volume maken voor moderne back-up-opslag</span><span class="sxs-lookup"><span data-stu-id="81c42-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="81c42-124">Met behulp van back-upserver van v2 met volumes als schijfopslag kunt u controle over opslag.</span><span class="sxs-lookup"><span data-stu-id="81c42-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="81c42-125">Een volume kan één schijf zijn.</span><span class="sxs-lookup"><span data-stu-id="81c42-125">A volume can be a single disk.</span></span> <span data-ttu-id="81c42-126">Als u opslag in de toekomst kunt uitbreiden wilt, echter een volume buiten een schijf die is gemaakt met behulp van opslagruimten maken.</span><span class="sxs-lookup"><span data-stu-id="81c42-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="81c42-127">Dit kan helpen als u wilt uitbreiden van het volume voor back-up.</span><span class="sxs-lookup"><span data-stu-id="81c42-127">This can help if you want to expand the volume for backup storage.</span></span> <span data-ttu-id="81c42-128">Deze sectie vindt u aanbevolen procedures voor het maken van een volume met deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="81c42-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="81c42-129">Selecteer in Serverbeheer **File and Storage Services** > **Volumes** > **opslaggroepen**.</span><span class="sxs-lookup"><span data-stu-id="81c42-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="81c42-130">Onder **fysieke schijven**, selecteer **nieuwe opslaggroep**.</span><span class="sxs-lookup"><span data-stu-id="81c42-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Een nieuwe opslaggroep maken](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="81c42-132">In de **taken** vervolgkeuzelijst, selecteer **nieuwe virtuele schijf**.</span><span class="sxs-lookup"><span data-stu-id="81c42-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Een virtuele schijf toevoegen](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="81c42-134">De opslaggroep selecteren en selecteer vervolgens **fysieke schijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="81c42-134">Select the storage pool, and then select **Add Physical Disk**.</span></span>

    ![Toevoegen van een fysieke schijf](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="81c42-136">Selecteer de fysieke schijf en selecteer vervolgens **virtuele schijf uitbreiden**.</span><span class="sxs-lookup"><span data-stu-id="81c42-136">Select the physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![De virtuele schijf uitbreiden](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="81c42-138">Selecteer de virtuele schijf en selecteer vervolgens **NieuwVolume**.</span><span class="sxs-lookup"><span data-stu-id="81c42-138">Select the virtual disk, and then select **New Volume**.</span></span>

    ![Maak een nieuw volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="81c42-140">In de **server en schijf selecteren** dialoogvenster, selecteer de server en de nieuwe schijf.</span><span class="sxs-lookup"><span data-stu-id="81c42-140">In the **Select the server and disk** dialog, select the server and the new disk.</span></span> <span data-ttu-id="81c42-141">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="81c42-141">Then, select **Next**.</span></span>

    ![De server en schijf selecteren](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a><span data-ttu-id="81c42-143">Volumes toevoegen aan back-upserver van schijfopslag</span><span class="sxs-lookup"><span data-stu-id="81c42-143">Add volumes to Backup Server disk storage</span></span>

<span data-ttu-id="81c42-144">Een volume toevoegen aan back-up-Server, in de **Management** deelvenster opnieuw scannen van de opslag en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="81c42-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span></span> <span data-ttu-id="81c42-145">Een lijst van alle volumes die kunnen worden toegevoegd voor de opslag van de back-up-Server wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="81c42-145">A list of all the volumes available to be added for Backup Server Storage appears.</span></span> <span data-ttu-id="81c42-146">Nadat beschikbare volumes zijn toegevoegd aan de lijst met geselecteerde volumes, kunt u ze een beschrijvende naam voor het beheren van deze geven.</span><span class="sxs-lookup"><span data-stu-id="81c42-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span></span> <span data-ttu-id="81c42-147">Om deze volumes Refs zodat back-upserver van de voordelen van moderne back-up-opslag kunt gebruiken, selecteert u **OK**.</span><span class="sxs-lookup"><span data-stu-id="81c42-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span></span>

![Toevoegen van de beschikbare Volumes](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="81c42-149">Werkbelasting-bewuste opslag instellen</span><span class="sxs-lookup"><span data-stu-id="81c42-149">Set up workload-aware storage</span></span>

<span data-ttu-id="81c42-150">Met de werkbelasting-bewuste opslag, kunt u de volumes waarop bepaalde soorten belasting bij voorkeur opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="81c42-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="81c42-151">U kunt bijvoorbeeld instellen dat dure volumes die ondersteuning bieden voor een groot aantal i/o-bewerkingen per seconde (IOPS) voor het opslaan van alleen de werkbelastingen die regelmatig, hoog volume back-ups vereisen.</span><span class="sxs-lookup"><span data-stu-id="81c42-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="81c42-152">Een voorbeeld is SQL Server met de transactielogboeken.</span><span class="sxs-lookup"><span data-stu-id="81c42-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="81c42-153">Andere werkbelastingen zijn back-ups minder vaak, zoals virtuele machines, kunnen een back-up naar goedkope volumes.</span><span class="sxs-lookup"><span data-stu-id="81c42-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="81c42-154">Update DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="81c42-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="81c42-155">U kunt de werkbelasting-bewuste opslag instellen met behulp van de PowerShell-cmdlet Update-DPMDiskStorage, die de eigenschappen van een volume in de opslaggroep op een server met Data Protection Manager-updates.</span><span class="sxs-lookup"><span data-stu-id="81c42-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="81c42-156">Syntaxis:</span><span class="sxs-lookup"><span data-stu-id="81c42-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="81c42-157">De volgende schermafbeelding ziet de cmdlet Update-DPMDiskStorage in het venster PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81c42-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span></span>

![De opdracht Update DPMDiskStorage in het venster PowerShell](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="81c42-159">Met behulp van PowerShell aangebrachte wijzigingen worden doorgevoerd in de back-up Server Administrator-Console.</span><span class="sxs-lookup"><span data-stu-id="81c42-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span></span>

![Schijven en volumes in de Administrator-Console](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="81c42-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81c42-161">Next steps</span></span>
<span data-ttu-id="81c42-162">Nadat u de back-up-Server hebt geïnstalleerd, informatie over het voorbereiden van uw server of met het beveiligen van een werkbelasting beginnen.</span><span class="sxs-lookup"><span data-stu-id="81c42-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="81c42-163">Back-upserver van werkbelastingen voorbereiden</span><span class="sxs-lookup"><span data-stu-id="81c42-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="81c42-164">Back-up-Server gebruiken om back-up van een VMware-server</span><span class="sxs-lookup"><span data-stu-id="81c42-164">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="81c42-165">Back-up-Server gebruiken om back-up van SQL Server</span><span class="sxs-lookup"><span data-stu-id="81c42-165">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)

