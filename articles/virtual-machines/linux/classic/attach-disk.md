---
title: een schijf tooa Linux VM in Azure aaaAttach | Microsoft Docs
description: Meer informatie over hoe een data tooattach tooa Linux VM schijf met Hallo-Classic deployment model en Hallo schijf initialiseren zodat deze gereed voor gebruik is
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="651af-103">Hoe tooAttach een gegevensschijf tooa virtuele Linux-Machine</span><span class="sxs-lookup"><span data-stu-id="651af-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="651af-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="651af-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="651af-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="651af-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="651af-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="651af-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="651af-107">Zie hoe te[een gegevensschijf met Resource Manager-implementatiemodel Hallo koppelen](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="651af-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="651af-108">U kunt zowel leeg schijven en schijven met gegevens tooyour Azure Virtual machines koppelen.</span><span class="sxs-lookup"><span data-stu-id="651af-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="651af-109">Beide typen schijven zijn VHD-bestanden die zich in een Azure storage-account bevinden.</span><span class="sxs-lookup"><span data-stu-id="651af-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="651af-110">Als bij het toevoegen van een schijf tooa Linux-machine nadat u Hallo schijf koppelt u tooinitialize moet en formatteer deze zodat deze gereed voor gebruik is.</span><span class="sxs-lookup"><span data-stu-id="651af-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="651af-111">Dit artikel gegevens zowel leeg schijven en schijven gegevens tooyour virtuele machines, ook al met hoe toothen initialiseren en formatteren van een nieuwe schijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="651af-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="651af-112">Het is een best practice toouse een of meer afzonderlijke schijven toostore gegevens van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="651af-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="651af-113">Wanneer u een virtuele machine in Azure maakt, heeft deze een besturingssysteem en een tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="651af-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="651af-114">**Gebruik geen Hallo tijdelijke schijf toostore permanente gegevens.**</span><span class="sxs-lookup"><span data-stu-id="651af-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="651af-115">Zoals Hallo-naam aangeeft, biedt deze alleen tijdelijke opslag.</span><span class="sxs-lookup"><span data-stu-id="651af-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="651af-116">Biedt geen redundantie of back-up omdat deze zich niet in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="651af-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="651af-117">Hallo tijdelijke schijf is gewoonlijk beheerd door hello Azure Linux Agent en automatisch te worden gekoppeld**mnt/resourcegroep** (of **mnt** Ubuntu afbeeldingen).</span><span class="sxs-lookup"><span data-stu-id="651af-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="651af-118">Op Hallo daarentegen, een gegevensschijf kan de naam van Hallo Linux kernel ongeveer `/dev/sdc`, en u moet toopartition, te maken en koppelen van deze resource.</span><span class="sxs-lookup"><span data-stu-id="651af-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="651af-119">Zie Hallo [gebruikershandleiding voor Azure Linux Agent] [ Agent] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="651af-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="651af-120">Initialiseer de gegevensschijf van een nieuwe in Linux</span><span class="sxs-lookup"><span data-stu-id="651af-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="651af-121">SSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="651af-121">SSH tooyour VM.</span></span> <span data-ttu-id="651af-122">Zie voor meer informatie [hoe toolog op tooa virtuele machine met Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="651af-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="651af-123">Vervolgens moet u toofind Hallo apparaat-id voor Hallo gegevens schijf tooinitialize.</span><span class="sxs-lookup"><span data-stu-id="651af-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="651af-124">Er zijn twee manieren toodo die:</span><span class="sxs-lookup"><span data-stu-id="651af-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="651af-125">a) Grep voor SCSI-apparaten in Hallo zich aanmeldt, zoals in de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="651af-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="651af-126">Recente Ubuntu distributies, moet u wellicht toouse `sudo grep SCSI /var/log/syslog` omdat logboekregistratie te`/var/log/messages` standaard mogelijk uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="651af-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="651af-127">U vindt Hallo-id van het laatste gegevensschijf hello, die is toegevoegd in het Hallo-berichten die worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="651af-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![Hallo schijf berichten ophalen](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="651af-129">OF</span><span class="sxs-lookup"><span data-stu-id="651af-129">OR</span></span>
   
    <span data-ttu-id="651af-130">b) Hallo gebruik `lsscsi` toofind opdracht out Hallo apparaat-id. `lsscsi` kan worden geïnstalleerd door een van beide `yum install lsscsi` (gebaseerd op Red Hat distributies) of `apt-get install lsscsi` (gebaseerd op Debian distributies).</span><span class="sxs-lookup"><span data-stu-id="651af-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="651af-131">U vindt Hallo schijf die u zoekt door de *lun* of **nummer van de logische eenheid**.</span><span class="sxs-lookup"><span data-stu-id="651af-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="651af-132">Bijvoorbeeld, Hallo *lun* voor Hallo-schijven die u hebt gekoppeld kunnen eenvoudig worden gezien vanaf `azure vm disk list <virtual-machine>` als:</span><span class="sxs-lookup"><span data-stu-id="651af-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="651af-133">Hallo-uitvoer is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="651af-133">hello output is similar toohello following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="651af-134">Deze gegevens met de uitvoer van Hallo vergelijken `lsscsi` voor Hallo steekproef dezelfde virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="651af-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="651af-135">Hallo laatste nummer in de tuple Hallo in elke rij is Hallo *lun*.</span><span class="sxs-lookup"><span data-stu-id="651af-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="651af-136">Zie `man lsscsi` voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="651af-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="651af-137">Type Hallo volgende opdracht toocreate uw apparaat bij Hallo-prompt:</span><span class="sxs-lookup"><span data-stu-id="651af-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="651af-138">Wanneer u wordt gevraagd, typt u  **n**  toocreate een partitie.</span><span class="sxs-lookup"><span data-stu-id="651af-138">When prompted, type **n** toocreate a partition.</span></span>

    ![Apparaat maken](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="651af-140">Wanneer u wordt gevraagd, typt u **p** toomake Hallo partitie Hallo primaire partitie.</span><span class="sxs-lookup"><span data-stu-id="651af-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="651af-141">Type **1** toomake het eerste partitie Hallo en typ vervolgens tooaccept Hallo-standaardwaarde opgeven voor Hallo cilinder.</span><span class="sxs-lookup"><span data-stu-id="651af-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="651af-142">Het kan standaardwaarden Hallo Hallo eerst weergeven en Hallo laatste sectoren, in plaats van Hallo cilinder op sommige systemen.</span><span class="sxs-lookup"><span data-stu-id="651af-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="651af-143">U kunt deze standaardinstellingen tooaccept.</span><span class="sxs-lookup"><span data-stu-id="651af-143">You can choose tooaccept these defaults.</span></span>

    ![Partitie maken](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="651af-145">Type **p** toosee Hallo details over Hallo-schijf die wordt opgedeeld.</span><span class="sxs-lookup"><span data-stu-id="651af-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![Schijfgegevens lijst](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="651af-147">Type **w** toowrite Hallo-instellingen voor Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="651af-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![Hallo schijfwijzigingen schrijven](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="651af-149">Nu kunt u Hallo-bestandssysteem op Hallo nieuwe partitie maken.</span><span class="sxs-lookup"><span data-stu-id="651af-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="651af-150">Hallo partitie nummer toohello apparaat-ID toevoegen (in het volgende voorbeeld Hallo `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="651af-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="651af-151">Hallo volgende voorbeeld wordt een partitie ext4 op /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="651af-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Bestandssysteem maken](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="651af-153">SuSE Linux Enterprise 11 alleen ondersteuning voor alleen-lezentoegang voor ext4-bestandssystemen.</span><span class="sxs-lookup"><span data-stu-id="651af-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="651af-154">Voor deze systemen wordt tooformat Hallo nieuw bestandssysteem als ext3 in plaats van ext4 aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="651af-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="651af-155">Een directory toomount Hallo nieuwe bestandssysteem, moet u als volgt:</span><span class="sxs-lookup"><span data-stu-id="651af-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="651af-156">Ten slotte kunt u Hallo station, als volgt koppelen:</span><span class="sxs-lookup"><span data-stu-id="651af-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="651af-157">Hallo gegevensschijf is nu gereed toouse als **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="651af-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![Hallo directory en koppelpunten Hallo schijf maken](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="651af-159">Hallo nieuwe station te/etc/fstab toevoegen:</span><span class="sxs-lookup"><span data-stu-id="651af-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="651af-160">tooensure hello station wordt automatisch opnieuw gekoppeld nadat deze moet opnieuw worden opgestart toohello /etc/fstab bestand toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="651af-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="651af-161">Bovendien is het nadrukkelijk aanbevolen dat die Hallo UUID (Universally Unique IDentifier) wordt gebruikt in /etc/fstab toorefer toohello station in plaats van alleen Hallo apparaatnaam (dat wil zeggen /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="651af-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="651af-162">Hallo met UUID Hallo foutieve schijfconfiguratie gekoppelde tooa locatie krijgt als Hallo OS een schijffout gedetecteerd tijdens het opstarten en eventuele resterende gegevensschijven vervolgens wordt toegewezen aan de apparaat-id's wordt voorkomt.</span><span class="sxs-lookup"><span data-stu-id="651af-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="651af-163">toofind Hallo UUID van het nieuwe station hello, kunt u Hallo **blkid** hulpprogramma:</span><span class="sxs-lookup"><span data-stu-id="651af-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="651af-164">Hallo-uitvoer ziet er vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="651af-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="651af-165">Onjuist bewerken van Hallo **/etc/fstab** bestand kan leiden tot een systeem opgestart.</span><span class="sxs-lookup"><span data-stu-id="651af-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="651af-166">Als u niet zeker, Raadpleeg toohello distributie van documentatie voor informatie over hoe tooproperly dit bestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="651af-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="651af-167">Het is ook raadzaam dat een back-up van Hallo /etc/fstab bestand is gemaakt voordat u bewerkt.</span><span class="sxs-lookup"><span data-stu-id="651af-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="651af-168">Open vervolgens Hallo **/etc/fstab** bestand in een teksteditor:</span><span class="sxs-lookup"><span data-stu-id="651af-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="651af-169">In dit voorbeeld gebruiken we Hallo UUID-waarde voor Hallo nieuwe **/dev/sdc1** apparaat dat is gemaakt in de vorige stappen Hallo en Hallo koppelpunt **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="651af-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="651af-170">Voeg na einde van regel toohello Hallo Hallo **/etc/fstab** bestand:</span><span class="sxs-lookup"><span data-stu-id="651af-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="651af-171">Of op systemen die op basis van SuSE Linux moet u wellicht toouse een iets andere indeling:</span><span class="sxs-lookup"><span data-stu-id="651af-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="651af-172">Hallo `nofail` optie zorgt ervoor dat Hallo VM start, zelfs als Hallo bestandssysteem beschadigd is of Hallo schijf tijdens het opstarten niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="651af-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="651af-173">Zonder deze optie kunnen optreden gedrag zoals beschreven in [niet kan SSH tooLinux VM vanwege fouten tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="651af-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="651af-174">Nu kunt u testen of Hallo-bestandssysteem is gekoppeld naar behoren ontkoppelen en vervolgens stationseigendom Hallo bestandssysteem, dat wil zeggen gebruikt Hallo voorbeeld koppelpunt `/datadrive` gemaakt in Hallo eerder stappen:</span><span class="sxs-lookup"><span data-stu-id="651af-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="651af-175">Als hello `mount` opdracht, treedt een fout, Controleer Hallo/etc/fstab-bestand voor de juiste syntaxis.</span><span class="sxs-lookup"><span data-stu-id="651af-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="651af-176">Als extra gegevensstations of partities worden gemaakt, / etc/fstab ook afzonderlijk aangaan.</span><span class="sxs-lookup"><span data-stu-id="651af-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="651af-177">Hallo station beschrijfbare maken met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="651af-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="651af-178">Vervolgens kan een gegevensschijf zonder te bewerken fstab verwijdert Hallo VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="651af-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="651af-179">Als dit vaak het geval is, de meeste distributies bieden beide Hallo `nofail` en/of `nobootwait` fstab-opties waarmee een tooboot systeem, zelfs als de schijf Hallo toomount tijdens het opstarten mislukt.</span><span class="sxs-lookup"><span data-stu-id="651af-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="651af-180">Raadpleeg de distributie-documentatie voor meer informatie over deze parameters.</span><span class="sxs-lookup"><span data-stu-id="651af-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="651af-181">TRIM/UNMAP ondersteuning voor Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="651af-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="651af-182">Sommige kernels Linux ondersteunen TRIM/UNMAP operations toodiscard niet-gebruikte blokken op Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="651af-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="651af-183">Deze bewerkingen zijn voornamelijk nuttig in standard-opslag tooinform Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="651af-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="651af-184">'S te verwijderen kunt kosten besparen, als u grote bestanden maken en deze vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="651af-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="651af-185">Er zijn twee manieren tooenable TRIM ondersteunen in uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="651af-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="651af-186">Raadpleeg uw distributiepunt gebruikelijke voor Hallo aanbevolen benadering:</span><span class="sxs-lookup"><span data-stu-id="651af-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="651af-187">Gebruik Hallo `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="651af-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="651af-188">In sommige gevallen Hallo `discard` optie prestaties gevolgen kan hebben.</span><span class="sxs-lookup"><span data-stu-id="651af-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="651af-189">U kunt ook uitvoeren Hallo `fstrim` opdracht handmatig vanaf de opdrachtregel Hallo of voeg tooyour crontab toorun regelmatig:</span><span class="sxs-lookup"><span data-stu-id="651af-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="651af-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="651af-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="651af-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="651af-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="651af-192">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="651af-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="651af-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="651af-193">Next Steps</span></span>
<span data-ttu-id="651af-194">Meer informatie over het gebruik van uw Linux-VM in Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="651af-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="651af-195">[Hoe toolog op tooa virtuele machine met Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="651af-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="651af-196">Hoe toodetach een schijf van een virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="651af-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="651af-197">Hello Azure CLI gebruiken met Hallo klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="651af-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="651af-198">Configureren van RAID op een virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="651af-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="651af-199">LVM configureren op een virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="651af-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
