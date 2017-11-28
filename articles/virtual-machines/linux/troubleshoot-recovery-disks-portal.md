---
title: Gebruik een op Linux VM probleemoplossing in de Azure portal | Microsoft Docs
description: Meer informatie over het oplossen van problemen voor Linux-virtuele machine door verbinding te maken van de besturingssysteemschijf voor een herstel-VM met de Azure portal
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: c96ff625c3e83f6fc9057f1163c877e8e0aed5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="f6036-103">Problemen oplossen van een Linux-VM met de OS-schijf koppelen aan een herstel-VM met de Azure portal</span><span class="sxs-lookup"><span data-stu-id="f6036-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="f6036-104">Als uw virtuele Linux-machine (VM) een opstart- of -fout optreedt, moet u wellicht de stappen voor probleemoplossing uitvoeren op de virtuele harde schijf zelf.</span><span class="sxs-lookup"><span data-stu-id="f6036-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="f6036-105">Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab` die verhindert dat de virtuele machine kunnen opstarten is.</span><span class="sxs-lookup"><span data-stu-id="f6036-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="f6036-106">Dit artikel wordt uitgelegd hoe u met de Azure-portal verbinding maken met de virtuele harde schijf aan een andere Linux VM eventuele fouten te corrigeren en vervolgens opnieuw maken van de oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="f6036-106">This article details how to use the Azure portal to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="f6036-107">Overzicht van het herstelproces</span><span class="sxs-lookup"><span data-stu-id="f6036-107">Recovery process overview</span></span>
<span data-ttu-id="f6036-108">Het probleemoplossingsproces is als volgt:</span><span class="sxs-lookup"><span data-stu-id="f6036-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="f6036-109">Verwijder de virtuele machine zonder problemen, om de virtuele harde schijven te houden.</span><span class="sxs-lookup"><span data-stu-id="f6036-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="f6036-110">Koppelen en koppel de virtuele harde schijf aan een andere Linux VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="f6036-110">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="f6036-111">Maak verbinding met de VM voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="f6036-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="f6036-112">Bewerken van bestanden of alle hulpmiddelen voor het oplossen van problemen op de oorspronkelijke virtuele harde schijf worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f6036-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="f6036-113">Koppel de virtuele harde schijf van de VM voor probleemoplossing los.</span><span class="sxs-lookup"><span data-stu-id="f6036-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="f6036-114">Een virtuele machine maken met de oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="f6036-114">Create a VM using the original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="f6036-115">Opstartproblemen bepalen</span><span class="sxs-lookup"><span data-stu-id="f6036-115">Determine boot issues</span></span>
<span data-ttu-id="f6036-116">Raadpleeg de diagnostische gegevens over opstarten en schermopname van de VM om te bepalen waarom de virtuele machine kan niet correct worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="f6036-116">Examine the boot diagnostics and VM screenshot to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="f6036-117">Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab`, of een onderliggende virtuele harde schijf wordt verwijderd of verplaatst.</span><span class="sxs-lookup"><span data-stu-id="f6036-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="f6036-118">Selecteer uw virtuele machine in de portal en schuif vervolgens omlaag naar de **ondersteuning + probleemoplossing** sectie.</span><span class="sxs-lookup"><span data-stu-id="f6036-118">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="f6036-119">Klik op **opstarten diagnostics** om de consoleberichten gestreamd vanaf uw virtuele machine weer te geven.</span><span class="sxs-lookup"><span data-stu-id="f6036-119">Click **Boot diagnostics** to view the console messages streamed from your VM.</span></span> <span data-ttu-id="f6036-120">Bekijk de logboeken van de console om te zien als kunt u bepalen waarom de virtuele machine wordt uitgevoerd als een probleem.</span><span class="sxs-lookup"><span data-stu-id="f6036-120">Review the console logs to see if you can determine why the VM is encountering an issue.</span></span> <span data-ttu-id="f6036-121">Het volgende voorbeeld ziet u dat een virtuele machine is vastgelopen in de onderhoudsmodus die handmatige interactie vereist:</span><span class="sxs-lookup"><span data-stu-id="f6036-121">The following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Diagnostische gegevens over opstarten console weer te geven VM Logboeken](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="f6036-123">U kunt ook klikken op **schermafbeelding** aan de bovenkant van het logboek boot diagnostics voor het downloaden van een vastleggen van de VM-schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="f6036-123">You can also click **Screenshot** across the top of the boot diagnostics log to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="f6036-124">Bestaande virtuele harde schijf details weergeven</span><span class="sxs-lookup"><span data-stu-id="f6036-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="f6036-125">Voordat u de virtuele harde schijf aan een andere virtuele machine koppelen kunt, moet u de naam van de virtuele harde schijf (VHD).</span><span class="sxs-lookup"><span data-stu-id="f6036-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="f6036-126">Selecteer uw resourcegroep via de portal en selecteer vervolgens uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="f6036-126">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="f6036-127">Klik op **Blobs**, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f6036-127">Click **Blobs**, as in the following example:</span></span>

![Selecteer de storage-blobs](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="f6036-129">Hebben doorgaans een container met de naam **VHD's** die de virtuele harde schijven worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f6036-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="f6036-130">Selecteer de container voor een lijst van virtuele harde schijven.</span><span class="sxs-lookup"><span data-stu-id="f6036-130">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="f6036-131">Houd rekening met de naam van uw VHD (het voorvoegsel is doorgaans de naam van uw virtuele machine):</span><span class="sxs-lookup"><span data-stu-id="f6036-131">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![Identificeren van de VHD in de storage-container](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="f6036-133">Selecteer uw bestaande virtuele harde schijf in de lijst en kopieer de URL voor gebruik in de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="f6036-133">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![Kopieer de URL van bestaande virtuele harde schijf](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="f6036-135">Bestaande virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="f6036-135">Delete existing VM</span></span>
<span data-ttu-id="f6036-136">Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="f6036-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="f6036-137">Een virtuele harde schijf is waar het besturingssysteem zelf, toepassingen en configuraties worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f6036-137">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="f6036-138">De virtuele machine zelf zijn gewoon metagegevens die definieert de grootte of locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC).</span><span class="sxs-lookup"><span data-stu-id="f6036-138">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="f6036-139">Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld aan een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f6036-139">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="f6036-140">Hoewel gegevensschijven zelfs wanneer de virtuele machine wordt uitgevoerd, kunnen worden gekoppeld en losgekoppeld, kan de besturingssysteemschijf niet worden losgekoppeld tenzij de VM-resource wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f6036-140">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="f6036-141">De lease blijft de OS-schijf koppelen aan een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.</span><span class="sxs-lookup"><span data-stu-id="f6036-141">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="f6036-142">De eerste stap voor het herstellen van uw virtuele machine is de VM-resource zelf verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f6036-142">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="f6036-143">Wanneer de virtuele machine wordt verwijderd, blijven de virtuele harde schijven aanwezig in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f6036-143">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="f6036-144">Nadat de virtuele machine wordt verwijderd, kunt u de virtuele harde schijf koppelen aan een andere virtuele machine kunt u de fouten oplossen.</span><span class="sxs-lookup"><span data-stu-id="f6036-144">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="f6036-145">Selecteer uw virtuele machine in de portal en klik vervolgens op **verwijderen**:</span><span class="sxs-lookup"><span data-stu-id="f6036-145">Select your VM in the portal, then click **Delete**:</span></span>

![VM boot diagnostics schermafbeelding opstartfout](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="f6036-147">Wacht totdat de virtuele machine verwijderen voordat u de virtuele harde schijf aan een andere virtuele machine koppelen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f6036-147">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="f6036-148">De lease op de virtuele harde schijf waarin deze zijn gekoppeld aan de virtuele machine moet worden vrijgegeven voordat u de virtuele harde schijf aan een andere virtuele machine koppelen kunt.</span><span class="sxs-lookup"><span data-stu-id="f6036-148">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="f6036-149">Bestaande virtuele harde schijf koppelen aan een andere virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f6036-149">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="f6036-150">Voor de volgende stappen gebruikt u een andere virtuele machine voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="f6036-150">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="f6036-151">U koppelen de bestaande virtuele harde schijf aan deze VM voor probleemoplossing kunnen bladeren en de inhoud van de schijf bewerken.</span><span class="sxs-lookup"><span data-stu-id="f6036-151">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="f6036-152">Dit proces kunt u eventuele configuratiefouten te corrigeren of extra toepassing of een systeem-logboekbestanden, bijvoorbeeld controleren.</span><span class="sxs-lookup"><span data-stu-id="f6036-152">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="f6036-153">Kies of maak een andere virtuele machine moet worden gebruikt voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="f6036-153">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="f6036-154">Selecteer uw resourcegroep via de portal en selecteer vervolgens uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="f6036-154">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="f6036-155">Selecteer **schijven** en klik vervolgens op **Attach bestaande**:</span><span class="sxs-lookup"><span data-stu-id="f6036-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Het koppelen van bestaande schijf in de portal](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="f6036-157">Klik om uw bestaande virtuele harde schijf te selecteren op **VHD-bestand**:</span><span class="sxs-lookup"><span data-stu-id="f6036-157">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![Zoeken naar bestaande VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="f6036-159">Uw opslagaccount en container selecteren en klik vervolgens op uw bestaande VHD.</span><span class="sxs-lookup"><span data-stu-id="f6036-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="f6036-160">Klik op de **Selecteer** knop om te bevestigen van uw keuze:</span><span class="sxs-lookup"><span data-stu-id="f6036-160">Click the **Select** button to confirm your choice:</span></span>

    ![Uw bestaande VHD selecteren](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="f6036-162">Met de VHD die is geselecteerd, klikt u op **OK** koppelen van de bestaande virtuele harde schijf:</span><span class="sxs-lookup"><span data-stu-id="f6036-162">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![Bevestig de bestaande virtuele harde schijf koppelen](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="f6036-164">Na enkele seconden, de **schijven** deelvenster voor uw virtuele machine een lijst met uw bestaande virtuele harde schijf als een gegevensschijf verbonden:</span><span class="sxs-lookup"><span data-stu-id="f6036-164">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Bestaande virtuele harde schijf gekoppeld als een gegevensschijf](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="f6036-166">Koppel de gekoppelde gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="f6036-166">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="f6036-167">De volgende voorbeelden worden de stappen die nodig is op een VM Ubuntu in detail beschreven.</span><span class="sxs-lookup"><span data-stu-id="f6036-167">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="f6036-168">Als u gebruikmaakt van een andere Linux distro zoals Red Hat Enterprise Linux of SUSE, de locaties van het logboekbestand en `mount` opdrachten mogelijk enigszins anders.</span><span class="sxs-lookup"><span data-stu-id="f6036-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="f6036-169">Raadpleeg de documentatie voor uw specifieke distro voor de benodigde wijzigingen in de opdrachten.</span><span class="sxs-lookup"><span data-stu-id="f6036-169">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="f6036-170">SSH met uw probleemoplossing virtuele machine met de juiste referenties.</span><span class="sxs-lookup"><span data-stu-id="f6036-170">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="f6036-171">Als u deze schijf is de eerste gegevensschijf gekoppeld aan uw VM voor het oplossen van problemen, waarschijnlijk is verbonden met `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="f6036-171">If this disk is the first data disk attached to your troubleshooting VM, it is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="f6036-172">Gebruik `dmseg` voor een lijst met gekoppelde schijven:</span><span class="sxs-lookup"><span data-stu-id="f6036-172">Use `dmseg` to list attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="f6036-173">De uitvoer lijkt op die in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f6036-173">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="f6036-174">In het voorgaande voorbeeld de OS-schijf is op `/dev/sda` en de tijdelijke schijf die is opgegeven voor elke virtuele machine is op `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="f6036-174">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="f6036-175">Als u meerdere gegevensschijven had, moeten ze op `/dev/sdd`, `/dev/sde`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="f6036-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="f6036-176">Maak een map voor het koppelen van uw bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="f6036-176">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="f6036-177">Het volgende voorbeeld wordt een map met de naam `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="f6036-177">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="f6036-178">Als u meerdere partities op de bestaande virtuele harde schijf hebt, koppelt u de vereiste partitie.</span><span class="sxs-lookup"><span data-stu-id="f6036-178">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="f6036-179">Het volgende voorbeeld koppelt de eerste primaire partitie op `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f6036-179">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="f6036-180">Er is een aanbevolen procedure gegevensschijven koppelen aan virtuele machines in Azure met behulp van de UUID universally unique identifier () van de virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="f6036-180">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="f6036-181">In dit scenario voor korte voor probleemoplossing voor is het koppelen van de virtuele harde schijf met de UUID niet nodig.</span><span class="sxs-lookup"><span data-stu-id="f6036-181">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="f6036-182">Echter, bij normaal gebruik bewerken `/etc/fstab` koppelen van virtuele harde schijven met de apparaatnaam van het in plaats van UUID kan ertoe leiden dat de virtuele machine niet kunnen worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="f6036-182">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="f6036-183">Los problemen op de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="f6036-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="f6036-184">Met de bestaande virtuele harde schijf dat wordt gekoppeld, kunt u nu onderhoud en stappen voor probleemoplossing naar behoefte uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f6036-184">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="f6036-185">Zodra u de problemen hebt opgelost, kunt u doorgaan met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="f6036-185">Once you have addressed the issues, continue with the following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="f6036-186">Ontkoppel en loskoppelen van de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="f6036-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="f6036-187">Zodra de fouten opgelost zijn, loskoppelen de bestaande virtuele harde schijf van uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="f6036-187">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="f6036-188">U kunt de virtuele harde schijf niet gebruiken met eventuele andere virtuele machine totdat de lease koppelen van de virtuele harde schijf voor het oplossen van problemen VM is uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="f6036-188">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="f6036-189">Ontkoppel de bestaande virtuele harde schijf van de SSH-sessie voor uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="f6036-189">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="f6036-190">Eerst buiten de bovenliggende map voor uw koppelpunt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="f6036-190">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="f6036-191">Nu Ontkoppel de bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="f6036-191">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="f6036-192">Het volgende voorbeeld het apparaat op ontkoppelt `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f6036-192">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="f6036-193">Nu loskoppelen van de virtuele harde schijf van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f6036-193">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="f6036-194">Selecteer uw virtuele machine in de portal en klik op **schijven**.</span><span class="sxs-lookup"><span data-stu-id="f6036-194">Select your VM in the portal and click **Disks**.</span></span> <span data-ttu-id="f6036-195">Selecteer uw bestaande virtuele harde schijf en klik vervolgens op **Detach**:</span><span class="sxs-lookup"><span data-stu-id="f6036-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Loskoppelen van de bestaande virtuele harde schijf](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="f6036-197">Wacht totdat de virtuele machine heeft de de gegevensschijf is losgekoppeld voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="f6036-197">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="f6036-198">Virtuele machine van de oorspronkelijke harde schijf maken</span><span class="sxs-lookup"><span data-stu-id="f6036-198">Create VM from original hard disk</span></span>
<span data-ttu-id="f6036-199">Gebruik voor het maken van een virtuele machine van de oorspronkelijke virtuele harde schijf [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="f6036-199">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="f6036-200">De sjabloon implementeert een virtuele machine in een bestaand virtueel netwerk met behulp van de VHD-URL van de vorige opdracht.</span><span class="sxs-lookup"><span data-stu-id="f6036-200">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="f6036-201">Klik op de **implementeren in Azure** knop als volgt:</span><span class="sxs-lookup"><span data-stu-id="f6036-201">Click the **Deploy to Azure** button as follows:</span></span>

![Implementeer de virtuele machine van de sjabloon vanuit GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="f6036-203">De sjabloon is geladen in de Azure-portal voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="f6036-203">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="f6036-204">Geef de naam op voor uw nieuwe virtuele machine en de bestaande Azure-resources en plak de URL naar uw bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="f6036-204">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="f6036-205">Om te beginnen met de implementatie, klikt u op **aankoop**:</span><span class="sxs-lookup"><span data-stu-id="f6036-205">To begin the deployment, click **Purchase**:</span></span>

![VM van sjabloon implementeren](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="f6036-207">Diagnostische gegevens over opstarten weer inschakelen</span><span class="sxs-lookup"><span data-stu-id="f6036-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="f6036-208">Wanneer u uw virtuele machine van de bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f6036-208">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="f6036-209">Controleer de status van diagnostische gegevens over opstarten en schakel indien nodig, selecteert u de virtuele machine in de portal.</span><span class="sxs-lookup"><span data-stu-id="f6036-209">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="f6036-210">Onder **bewaking**, klikt u op **diagnostische instellingen**.</span><span class="sxs-lookup"><span data-stu-id="f6036-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="f6036-211">Zorg ervoor dat de status **op**, en het selectievakje naast **opstarten diagnostics** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f6036-211">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="f6036-212">Als u geen wijzigingen aanbrengen, klikt u op **opslaan**:</span><span class="sxs-lookup"><span data-stu-id="f6036-212">If you make any changes, click **Save**:</span></span>

![Bijwerken van diagnostische gegevens van de instellingen voor opstarten](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="f6036-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f6036-214">Next steps</span></span>
<span data-ttu-id="f6036-215">Als u verbinding maakt met uw virtuele machine problemen ondervindt, raadpleegt u [oplossen SSH-verbindingen met een Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6036-215">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f6036-216">Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Linux-VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6036-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f6036-217">Zie voor meer informatie over het gebruik van Resource Manager [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6036-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
