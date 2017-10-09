---
title: aaaUse een Linux VM probleemoplossing in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe problemen met de virtuele machine tootroubleshoot Linux via verbindende Hallo OS schijf tooa herstel VM hello Azure-portal
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
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="68804-103">Linux-VM oplossen door het Hallo OS tooa schijfherstel VM koppelen met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="68804-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="68804-104">Als uw virtuele Linux-machine (VM) een opstart- of -fout optreedt, moet u mogelijk tooperform stappen voor probleemoplossing in het virtuele harde schijf hello, zelf.</span><span class="sxs-lookup"><span data-stu-id="68804-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="68804-105">Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab` dat verhindert Hallo VM kunnen tooboot is.</span><span class="sxs-lookup"><span data-stu-id="68804-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="68804-106">De details van dit artikel hoe toouse hello Azure portal tooconnect uw virtuele harde schijf tooanother Linux VM toofix geen fouten bevat en klik vervolgens opnieuw maken van de oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="68804-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="68804-107">Overzicht van het herstelproces</span><span class="sxs-lookup"><span data-stu-id="68804-107">Recovery process overview</span></span>
<span data-ttu-id="68804-108">Hallo procedure voor probleemoplossing is als volgt:</span><span class="sxs-lookup"><span data-stu-id="68804-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="68804-109">Verwijder Hallo VM zonder problemen Hallo virtuele harde schijven te houden.</span><span class="sxs-lookup"><span data-stu-id="68804-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="68804-110">Koppelen en koppelen van Hallo virtuele harde schijf tooanother Linux-VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="68804-110">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="68804-111">Verbinding maken met toohello VM probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="68804-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="68804-112">Bestanden bewerken of toofix problemen van alle hulpprogramma's uitvoeren op Hallo oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="68804-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="68804-113">Ontkoppel en Hallo virtuele harde schijf van Hallo probleemoplossing VM loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="68804-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="68804-114">Een virtuele machine maken met Hallo oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="68804-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="68804-115">Opstartproblemen bepalen</span><span class="sxs-lookup"><span data-stu-id="68804-115">Determine boot issues</span></span>
<span data-ttu-id="68804-116">Bekijk Hallo boot diagnostics- en VM schermafbeelding toodetermine waarom uw virtuele machine niet kunnen tooboot correct is.</span><span class="sxs-lookup"><span data-stu-id="68804-116">Examine hello boot diagnostics and VM screenshot toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="68804-117">Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab`, of een onderliggende virtuele harde schijf wordt verwijderd of verplaatst.</span><span class="sxs-lookup"><span data-stu-id="68804-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="68804-118">Selecteer uw virtuele machine in Hallo-portal en schuif omlaag toohello **ondersteuning + probleemoplossing** sectie.</span><span class="sxs-lookup"><span data-stu-id="68804-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="68804-119">Klik op **opstarten diagnostics** tooview Hallo consoleberichten gestreamd vanaf uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="68804-119">Click **Boot diagnostics** tooview hello console messages streamed from your VM.</span></span> <span data-ttu-id="68804-120">Bekijk Hallo console-logboeken toosee als u kunt vaststellen waarom hello VM wordt uitgevoerd als een probleem.</span><span class="sxs-lookup"><span data-stu-id="68804-120">Review hello console logs toosee if you can determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="68804-121">Hallo volgende voorbeeld ziet u dat een virtuele machine is vastgelopen in de onderhoudsmodus die handmatige interactie vereist:</span><span class="sxs-lookup"><span data-stu-id="68804-121">hello following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Diagnostische gegevens over opstarten console weer te geven VM Logboeken](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="68804-123">U kunt ook klikken op **schermafbeelding** aan de bovenkant Hallo van Hallo boot diagnostics logboek toodownload een vastleggen van de schermopname Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="68804-123">You can also click **Screenshot** across hello top of hello boot diagnostics log toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="68804-124">Bestaande virtuele harde schijf details weergeven</span><span class="sxs-lookup"><span data-stu-id="68804-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="68804-125">Voordat u uw virtuele harde schijf tooanother VM koppelen kunt, moet u tooidentify Hallo-naam van Hallo virtuele harde schijf (VHD).</span><span class="sxs-lookup"><span data-stu-id="68804-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="68804-126">Selecteer uw resourcegroep van Hallo-portal en selecteer vervolgens uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="68804-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="68804-127">Klik op **Blobs**, Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="68804-127">Click **Blobs**, as in hello following example:</span></span>

![Selecteer de storage-blobs](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="68804-129">Hebben doorgaans een container met de naam **VHD's** die de virtuele harde schijven worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="68804-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="68804-130">Selecteer Hallo container tooview een lijst met virtuele harde schijven.</span><span class="sxs-lookup"><span data-stu-id="68804-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="68804-131">Opmerking Hallo-naam van uw VHD (Hallo voorvoegsel is gewoonlijk Hallo-naam van uw virtuele machine):</span><span class="sxs-lookup"><span data-stu-id="68804-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![Identificeren van de VHD in de storage-container](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="68804-133">Uw bestaande virtuele harde schijf in Hallo lijst selecteren en kopiëren Hallo-URL voor gebruik in Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="68804-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![Kopieer de URL van bestaande virtuele harde schijf](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="68804-135">Bestaande virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="68804-135">Delete existing VM</span></span>
<span data-ttu-id="68804-136">Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="68804-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="68804-137">Een virtuele harde schijf is waar Hallo besturingssysteem zelf, toepassingen en configuraties worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="68804-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="68804-138">Hallo VM zelf zijn gewoon metagegevens die definieert Hallo grootte of de locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC).</span><span class="sxs-lookup"><span data-stu-id="68804-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="68804-139">Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld tooa VM.</span><span class="sxs-lookup"><span data-stu-id="68804-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="68804-140">Hoewel gegevensschijven kunnen worden gekoppeld en ontkoppeld, zelfs wanneer Hallo VM wordt uitgevoerd, kan de besturingssysteemschijf Hallo kan niet worden losgekoppeld tenzij Hallo VM-resource wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="68804-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="68804-141">Hallo lease blijft tooassociate Hallo OS-schijf met een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.</span><span class="sxs-lookup"><span data-stu-id="68804-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="68804-142">eerste stap toorecover Hallo uw VM is toodelete Hallo VM-resource zelf.</span><span class="sxs-lookup"><span data-stu-id="68804-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="68804-143">Verwijderen Hallo VM verlaat Hallo virtuele harde schijven in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="68804-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="68804-144">Na het Hallo die virtuele machine is verwijderd, Hallo virtuele harde schijf tooanother VM tootroubleshoot koppelen en Hallo fouten op te lossen.</span><span class="sxs-lookup"><span data-stu-id="68804-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="68804-145">Uw virtuele machine in de portal van Hallo selecteren en klik vervolgens op **verwijderen**:</span><span class="sxs-lookup"><span data-stu-id="68804-145">Select your VM in hello portal, then click **Delete**:</span></span>

![VM boot diagnostics schermafbeelding opstartfout](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="68804-147">Wacht totdat het Hallo VM verwijderen voordat u Hallo virtuele harde schijf tooanother VM koppelen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="68804-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="68804-148">Hallo-lease op het virtuele harde schijf hello, waarin deze zijn gekoppeld aan VM Hallo moet toobe vrijgegeven voordat u Hallo virtuele harde schijf tooanother VM kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="68804-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="68804-149">Bestaande virtuele harde schijf tooanother VM koppelen</span><span class="sxs-lookup"><span data-stu-id="68804-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="68804-150">Voor Hallo volgende stappen, u een andere virtuele machine gebruiken voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="68804-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="68804-151">U koppelt Hallo bestaande virtuele harde schijf toothis VM toobe kunnen toobrowse probleemoplossing en inhoud van de schijf Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="68804-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="68804-152">Dit proces kunt u toocorrect eventuele fouten in de configuratie of revisie aanvullende toepassings- of logboekbestanden, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="68804-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="68804-153">Kies of maak een ander VM-toouse voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="68804-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="68804-154">Selecteer uw resourcegroep van Hallo-portal en selecteer vervolgens uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="68804-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="68804-155">Selecteer **schijven** en klik vervolgens op **Attach bestaande**:</span><span class="sxs-lookup"><span data-stu-id="68804-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Bestaande schijf in de portal Hallo koppelen](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="68804-157">tooselect uw bestaande virtuele harde schijf klikt u op **VHD-bestand**:</span><span class="sxs-lookup"><span data-stu-id="68804-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![Zoeken naar bestaande VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="68804-159">Uw opslagaccount en container selecteren en klik vervolgens op uw bestaande VHD.</span><span class="sxs-lookup"><span data-stu-id="68804-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="68804-160">Klik op Hallo **Selecteer** knop tooconfirm uw keuze:</span><span class="sxs-lookup"><span data-stu-id="68804-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![Uw bestaande VHD selecteren](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="68804-162">Met de VHD die is geselecteerd, klikt u op **OK** tooattach Hallo bestaande virtuele harde schijf:</span><span class="sxs-lookup"><span data-stu-id="68804-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![Bevestig de bestaande virtuele harde schijf koppelen](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="68804-164">Na enkele seconden Hallo **schijven** deelvenster voor uw virtuele machine een lijst met uw bestaande virtuele harde schijf als een gegevensschijf verbonden:</span><span class="sxs-lookup"><span data-stu-id="68804-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Bestaande virtuele harde schijf gekoppeld als een gegevensschijf](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="68804-166">Hallo bijgesloten gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="68804-166">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="68804-167">Hallo beschreven hieronder Hallo stappen vereist op een Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="68804-167">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="68804-168">Als u van een andere Linux distro zoals Red Hat Enterprise Linux of SUSE gebruikmaakt, Hallo locaties logboekbestand en `mount` opdrachten mogelijk enigszins anders.</span><span class="sxs-lookup"><span data-stu-id="68804-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="68804-169">Raadpleeg toohello-documentatie voor uw specifieke distro voor Hallo benodigde wijzigingen in de opdrachten.</span><span class="sxs-lookup"><span data-stu-id="68804-169">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="68804-170">SSH-tooyour het oplossen van problemen met de juiste referenties Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="68804-170">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="68804-171">Als deze schijf Hallo eerste gegevens schijf is gekoppeld aan tooyour probleemoplossing VM is, is deze waarschijnlijk aangesloten te`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="68804-171">If this disk is hello first data disk attached tooyour troubleshooting VM, it is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="68804-172">Gebruik `dmseg` toolist gekoppelde schijven:</span><span class="sxs-lookup"><span data-stu-id="68804-172">Use `dmseg` toolist attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="68804-173">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="68804-173">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="68804-174">In de Hallo voorgaande voorbeeld, Hallo OS-schijf is op `/dev/sda` en Hallo tijdelijke schijf opgegeven voor elke virtuele machine is op `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="68804-174">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="68804-175">Als u meerdere gegevensschijven had, moeten ze op `/dev/sdd`, `/dev/sde`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="68804-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="68804-176">Maak een map toomount uw bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="68804-176">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="68804-177">Hallo volgende voorbeeld maakt u een map met de naam `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="68804-177">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="68804-178">Als u meerdere partities op de bestaande virtuele harde schijf hebt, koppel Hallo vereist partitie.</span><span class="sxs-lookup"><span data-stu-id="68804-178">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="68804-179">Hallo volgende voorbeeld koppelt Hallo eerste primaire partitie op `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="68804-179">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="68804-180">Aanbevolen procedure is toomount gegevensschijven op virtuele machines in Azure worden verkregen met Hallo (UUID) universally unique identifier van Hallo virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="68804-180">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="68804-181">Voor dit scenario voor de korte voor probleemoplossing is koppelen Hallo virtuele harde schijf met behulp van Hallo UUID niet nodig.</span><span class="sxs-lookup"><span data-stu-id="68804-181">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="68804-182">Echter, bij normaal gebruik bewerken `/etc/fstab` toomount virtuele harde schijven met de apparaatnaam van het in plaats van UUID kan ertoe leiden dat Hallo VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="68804-182">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="68804-183">Los problemen op de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="68804-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="68804-184">Hallo bestaande virtuele harde schijf gekoppeld, kunt u eventuele onderhoud en probleemoplossing naar behoefte nu uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="68804-184">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="68804-185">Zodra u Hallo problemen hebt opgelost, kunt u doorgaan met de Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="68804-185">Once you have addressed hello issues, continue with hello following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="68804-186">Ontkoppel en loskoppelen van de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="68804-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="68804-187">Zodra de fouten opgelost zijn, loskoppelen Hallo bestaande virtuele harde schijf van uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="68804-187">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="68804-188">U kunt de virtuele harde schijf niet gebruiken met een andere VM tot Hallo lease Hallo virtuele harde schijf toohello probleemoplossing VM koppelen is vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="68804-188">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="68804-189">Ontkoppelen van Hallo SSH-sessie tooyour VM probleemoplossing, Hallo bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="68804-189">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="68804-190">Eerst buiten Hallo van de bovenliggende map voor uw koppelpunt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="68804-190">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="68804-191">Nu Ontkoppel Hallo bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="68804-191">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="68804-192">Hallo volgende voorbeeld ontkoppelt Hallo-apparaat op `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="68804-192">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="68804-193">Nu loskoppelen Hallo virtuele harde schijf van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="68804-193">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="68804-194">Selecteer uw virtuele machine in Hallo-portal en klik op **schijven**.</span><span class="sxs-lookup"><span data-stu-id="68804-194">Select your VM in hello portal and click **Disks**.</span></span> <span data-ttu-id="68804-195">Selecteer uw bestaande virtuele harde schijf en klik vervolgens op **Detach**:</span><span class="sxs-lookup"><span data-stu-id="68804-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Loskoppelen van de bestaande virtuele harde schijf](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="68804-197">Wacht totdat het Hallo VM heeft Hallo gegevensschijf is losgekoppeld voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="68804-197">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="68804-198">Virtuele machine van de oorspronkelijke harde schijf maken</span><span class="sxs-lookup"><span data-stu-id="68804-198">Create VM from original hard disk</span></span>
<span data-ttu-id="68804-199">toocreate een virtuele machine van de oorspronkelijke virtuele harde schijf gebruiken [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="68804-199">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="68804-200">Hallo sjabloon een virtuele machine implementeert in een bestaand virtueel netwerk met behulp van Hallo VHD URL uit Hallo eerder opdracht.</span><span class="sxs-lookup"><span data-stu-id="68804-200">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="68804-201">Klik op Hallo **tooAzure implementeren** knop als volgt:</span><span class="sxs-lookup"><span data-stu-id="68804-201">Click hello **Deploy tooAzure** button as follows:</span></span>

![Implementeer de virtuele machine van de sjabloon vanuit GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="68804-203">Hallo-sjabloon wordt geladen in hello Azure-portal voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="68804-203">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="68804-204">Geef de namen van Hallo voor uw nieuwe virtuele machine en de bestaande Azure-resources en plak Hallo URL tooyour bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="68804-204">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="68804-205">toobegin Hallo-implementatie, klikt u op **aankoop**:</span><span class="sxs-lookup"><span data-stu-id="68804-205">toobegin hello deployment, click **Purchase**:</span></span>

![VM van sjabloon implementeren](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="68804-207">Diagnostische gegevens over opstarten weer inschakelen</span><span class="sxs-lookup"><span data-stu-id="68804-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="68804-208">Wanneer u uw virtuele machine van Hallo bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="68804-208">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="68804-209">toocheck Hallo status van diagnostische gegevens over opstarten en schakel indien nodig, selecteert u uw virtuele machine in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="68804-209">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="68804-210">Onder **bewaking**, klikt u op **diagnostische instellingen**.</span><span class="sxs-lookup"><span data-stu-id="68804-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="68804-211">Zorg ervoor dat de status van de Hallo **op**, en het selectievakje naast Hallo te**opstarten diagnostics** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="68804-211">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="68804-212">Als u geen wijzigingen aanbrengen, klikt u op **opslaan**:</span><span class="sxs-lookup"><span data-stu-id="68804-212">If you make any changes, click **Save**:</span></span>

![Bijwerken van diagnostische gegevens van de instellingen voor opstarten](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="68804-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68804-214">Next steps</span></span>
<span data-ttu-id="68804-215">Als u verbinding maken met tooyour VM problemen ondervindt, raadpleegt u [oplossen SSH-verbindingen tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68804-215">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="68804-216">Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Linux-VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68804-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="68804-217">Zie voor meer informatie over het gebruik van Resource Manager [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68804-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
