---
title: Een schijf koppelen aan een Linux-VM in Azure | Microsoft Docs
description: Informatie over het een gegevensschijf koppelen aan een Linux-VM met het klassieke implementatiemodel en de schijf initialiseren zodat deze gereed voor gebruik is
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
ms.openlocfilehash: 017ba7197e11c2b222082833d5acabb9e542b762
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-virtual-machine"></a><span data-ttu-id="6bf87-103">Hoe een gegevensschijf koppelen aan een virtuele Linux-Machine</span><span class="sxs-lookup"><span data-stu-id="6bf87-103">How to Attach a Data Disk to a Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="6bf87-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6bf87-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6bf87-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6bf87-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="6bf87-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6bf87-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="6bf87-107">Zie hoe [een gegevensschijf met het implementatiemodel van Resource Manager koppelen](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6bf87-107">See how to [attach a data disk using the Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6bf87-108">U kunt zowel leeg schijven en schijven met gegevens naar uw Azure VM's kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="6bf87-108">You can attach both empty disks and disks that contain data to your Azure VMs.</span></span> <span data-ttu-id="6bf87-109">Beide typen schijven zijn VHD-bestanden die zich in een Azure storage-account bevinden.</span><span class="sxs-lookup"><span data-stu-id="6bf87-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="6bf87-110">Als met een schijf toevoegen aan een Linux-machine, hoeft nadat u de schijf koppelen te initialiseren en formatteren zodat deze gereed voor gebruik is.</span><span class="sxs-lookup"><span data-stu-id="6bf87-110">As with adding any disk to a Linux machine, after you attach the disk you need to initialize and format it so it's ready for use.</span></span> <span data-ttu-id="6bf87-111">Dit artikel gegevens zowel leeg schijven en schijven met al gegevens naar uw virtuele machines, evenals hoe u kunt vervolgens initialiseren en formatteren van een nieuwe schijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="6bf87-111">This article details attaching both empty disks and disks already containing data to your VMs, as well as how to then initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="6bf87-112">Het is een best practice om een of meer afzonderlijke schijven te bewaren van gegevens van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6bf87-112">It's a best practice to use one or more separate disks to store a virtual machine's data.</span></span> <span data-ttu-id="6bf87-113">Wanneer u een virtuele machine in Azure maakt, heeft deze een besturingssysteem en een tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="6bf87-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="6bf87-114">**Gebruik de tijdelijke schijf geen permanente gegevens opslaan.**</span><span class="sxs-lookup"><span data-stu-id="6bf87-114">**Do not use the temporary disk to store persistent data.**</span></span> <span data-ttu-id="6bf87-115">Zoals de naam al aangeeft, biedt deze alleen tijdelijke opslag.</span><span class="sxs-lookup"><span data-stu-id="6bf87-115">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="6bf87-116">Biedt geen redundantie of back-up omdat deze zich niet in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="6bf87-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="6bf87-117">De tijdelijke schijf is gewoonlijk beheerd door de Azure Linux Agent en automatisch gekoppeld aan **mnt/resourcegroep** (of **mnt** Ubuntu afbeeldingen).</span><span class="sxs-lookup"><span data-stu-id="6bf87-117">The temporary disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="6bf87-118">Aan de andere kant een gegevensschijf kan de naam van de kernel Linux ongeveer `/dev/sdc`, en u moet partitie formatteren, en koppel deze resource.</span><span class="sxs-lookup"><span data-stu-id="6bf87-118">On the other hand, a data disk might be named by the Linux kernel something like `/dev/sdc`, and you need to partition, format, and mount this resource.</span></span> <span data-ttu-id="6bf87-119">Zie de [gebruikershandleiding voor Azure Linux Agent] [ Agent] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6bf87-119">See the [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="6bf87-120">Initialiseer de gegevensschijf van een nieuwe in Linux</span><span class="sxs-lookup"><span data-stu-id="6bf87-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="6bf87-121">SSH met uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6bf87-121">SSH to your VM.</span></span> <span data-ttu-id="6bf87-122">Zie voor meer informatie [aanmelden met een virtuele machine met Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="6bf87-122">For more information, see [How to log on to a virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="6bf87-123">Vervolgens moet u de apparaat-id voor de gegevensschijf initialiseren vinden.</span><span class="sxs-lookup"><span data-stu-id="6bf87-123">Next you need to find the device identifier for the data disk to initialize.</span></span> <span data-ttu-id="6bf87-124">Er zijn twee manieren doen:</span><span class="sxs-lookup"><span data-stu-id="6bf87-124">There are two ways to do that:</span></span>
   
    <span data-ttu-id="6bf87-125">een) Grep voor SCSI-apparaten in de logboeken, zoals in de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6bf87-125">a) Grep for SCSI devices in the logs, such as in the following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="6bf87-126">Recente Ubuntu distributies, moet u wellicht gebruiken `sudo grep SCSI /var/log/syslog` omdat registratie in `/var/log/messages` standaard mogelijk uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6bf87-126">For recent Ubuntu distributions, you may need to use `sudo grep SCSI /var/log/syslog` because logging to `/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="6bf87-127">U vindt de id van de laatste gegevensschijf die is toegevoegd in de berichten die worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6bf87-127">You can find the identifier of the last data disk that was added in the messages that are displayed.</span></span>
   
    ![De berichten van de schijf ophalen](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="6bf87-129">OF</span><span class="sxs-lookup"><span data-stu-id="6bf87-129">OR</span></span>
   
    <span data-ttu-id="6bf87-130">b) Gebruik de `lsscsi` opdracht om erachter te komen de apparaat-id.</span><span class="sxs-lookup"><span data-stu-id="6bf87-130">b) Use the `lsscsi` command to find out the device id.</span></span> <span data-ttu-id="6bf87-131">U kunt `lsscsi` installeren met `yum install lsscsi` (Red Hat-distributies) of `apt-get install lsscsi` (Debian-distributies).</span><span class="sxs-lookup"><span data-stu-id="6bf87-131">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="6bf87-132">U vindt de schijf die u zoekt door de *lun* of **nummer van de logische eenheid**.</span><span class="sxs-lookup"><span data-stu-id="6bf87-132">You can find the disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="6bf87-133">Bijvoorbeeld, de *lun* voor de schijven die door u bijgevoegde gemakkelijk kunnen worden gezien vanaf `azure vm disk list <virtual-machine>` als:</span><span class="sxs-lookup"><span data-stu-id="6bf87-133">For example, the *lun* for the disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="6bf87-134">De uitvoer lijkt op het volgende:</span><span class="sxs-lookup"><span data-stu-id="6bf87-134">The output is similar to the following:</span></span>

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
   
    <span data-ttu-id="6bf87-135">Deze gegevens met de uitvoer van vergelijken `lsscsi` voor dezelfde virtuele machine steekproef:</span><span class="sxs-lookup"><span data-stu-id="6bf87-135">Compare this data with the output of `lsscsi` for the same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="6bf87-136">Het laatste aantal in de tuple in elke rij is de *lun*.</span><span class="sxs-lookup"><span data-stu-id="6bf87-136">The last number in the tuple in each row is the *lun*.</span></span> <span data-ttu-id="6bf87-137">Zie `man lsscsi` voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6bf87-137">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="6bf87-138">Typ de volgende opdracht om uw apparaat te maken bij de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="6bf87-138">At the prompt, type the following command to create your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="6bf87-139">Wanneer u wordt gevraagd, typt u  **n**  een partitie maken.</span><span class="sxs-lookup"><span data-stu-id="6bf87-139">When prompted, type **n** to create a partition.</span></span>

    ![Apparaat maken](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="6bf87-141">Wanneer u wordt gevraagd, typt u **p** om te maken van de partitie de primaire partitie.</span><span class="sxs-lookup"><span data-stu-id="6bf87-141">When prompted, type **p** to make the partition the primary partition.</span></span> <span data-ttu-id="6bf87-142">Type **1** zodat het de eerste partitie en typ vervolgens invoeren voor het accepteren van de standaardwaarde voor de cilinder.</span><span class="sxs-lookup"><span data-stu-id="6bf87-142">Type **1** to make it the first partition, and then type enter to accept the default value for the cylinder.</span></span> <span data-ttu-id="6bf87-143">Op sommige systemen kan deze de standaardwaarden van de eerste en de laatste sectoren, in plaats van de cilinder weergeven.</span><span class="sxs-lookup"><span data-stu-id="6bf87-143">On some systems, it can show the default values of the first and the last sectors, instead of the cylinder.</span></span> <span data-ttu-id="6bf87-144">U kunt deze standaardinstellingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="6bf87-144">You can choose to accept these defaults.</span></span>

    ![Partitie maken](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="6bf87-146">Type **p** om de details over de schijf die wordt opgedeeld te bekijken.</span><span class="sxs-lookup"><span data-stu-id="6bf87-146">Type **p** to see the details about the disk that is being partitioned.</span></span>

    ![Schijfgegevens lijst](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="6bf87-148">Type **w** de instellingen voor de schijf te schrijven.</span><span class="sxs-lookup"><span data-stu-id="6bf87-148">Type **w** to write the settings for the disk.</span></span>

    ![De schijfwijzigingen geschreven](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="6bf87-150">Nu kunt u het bestandssysteem op de nieuwe partitie maken.</span><span class="sxs-lookup"><span data-stu-id="6bf87-150">Now you can create the file system on the new partition.</span></span> <span data-ttu-id="6bf87-151">Het partitienummer toevoegen aan de apparaat-ID (in het volgende voorbeeld `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="6bf87-151">Append the partition number to the device ID (in the following example `/dev/sdc1`).</span></span> <span data-ttu-id="6bf87-152">Het volgende voorbeeld wordt een partitie ext4 op /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="6bf87-152">The following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Bestandssysteem maken](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="6bf87-154">SuSE Linux Enterprise 11 alleen ondersteuning voor alleen-lezentoegang voor ext4-bestandssystemen.</span><span class="sxs-lookup"><span data-stu-id="6bf87-154">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="6bf87-155">Voor deze systemen, is het aanbevolen om het nieuwe bestandssysteem als ext3 in plaats van ext4.</span><span class="sxs-lookup"><span data-stu-id="6bf87-155">For these systems, it is recommended to format the new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="6bf87-156">Moet een directory koppelen van het nieuwe bestandssysteem als volgt:</span><span class="sxs-lookup"><span data-stu-id="6bf87-156">Make a directory to mount the new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="6bf87-157">Ten slotte kunt u het station als volgt koppelen:</span><span class="sxs-lookup"><span data-stu-id="6bf87-157">Finally you can mount the drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="6bf87-158">De gegevensschijf is nu gereed voor gebruik als **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="6bf87-158">The data disk is now ready to use as **/datadrive**.</span></span>
   
    ![Maken van de map en de schijf koppelen](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="6bf87-160">Het nieuwe station aan /etc/fstab toevoegen:</span><span class="sxs-lookup"><span data-stu-id="6bf87-160">Add the new drive to /etc/fstab:</span></span>
   
    <span data-ttu-id="6bf87-161">Om te controleren of dat de schijf automatisch opnieuw wordt gekoppeld na opnieuw opstarten moet deze worden toegevoegd aan het bestand/etc/fstab-fouten.</span><span class="sxs-lookup"><span data-stu-id="6bf87-161">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="6bf87-162">Het is ook raadzaam een dat de UUID (Universally Unique IDentifier) wordt gebruikt in /etc/fstab om te verwijzen naar het station in plaats van alleen de naam van het apparaat (dat wil zeggen /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="6bf87-162">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="6bf87-163">Met behulp van de UUID voorkomt de onjuiste schijf wordt gekoppeld aan een bepaalde locatie als het besturingssysteem detecteert een schijffout tijdens het opstarten en eventuele resterende gegevensschijven vervolgens deze apparaat-id's worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6bf87-163">Using the UUID avoids the incorrect disk being mounted to a given location if the OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="6bf87-164">Als u de UUID van het nieuwe station zoekt, kunt u de **blkid** hulpprogramma:</span><span class="sxs-lookup"><span data-stu-id="6bf87-164">To find the UUID of the new drive, you can use the **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="6bf87-165">De uitvoer lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6bf87-165">The output looks similar to the following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="6bf87-166">Onjuist bewerken van de **/etc/fstab** bestand kan leiden tot een systeem opgestart.</span><span class="sxs-lookup"><span data-stu-id="6bf87-166">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="6bf87-167">Als u niet zeker, Raadpleeg de distributie-documentatie voor informatie over het correct dit bestand te bewerken.</span><span class="sxs-lookup"><span data-stu-id="6bf87-167">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="6bf87-168">Het is ook raadzaam dat een back-up van het bestand /etc/fstab is gemaakt voordat u bewerkt.</span><span class="sxs-lookup"><span data-stu-id="6bf87-168">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="6bf87-169">Open vervolgens de **/etc/fstab** bestand in een teksteditor:</span><span class="sxs-lookup"><span data-stu-id="6bf87-169">Next, open the **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="6bf87-170">In dit voorbeeld gebruiken we de UUID-waarde voor de nieuwe **/dev/sdc1** apparaat dat is gemaakt in de vorige stappen en het koppelpunt **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="6bf87-170">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="6bf87-171">Voeg de volgende regel toe aan het einde van de **/etc/fstab** bestand:</span><span class="sxs-lookup"><span data-stu-id="6bf87-171">Add the following line to the end of the **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="6bf87-172">Of op systemen die op basis van SuSE Linux moet u wellicht een iets andere notatie:</span><span class="sxs-lookup"><span data-stu-id="6bf87-172">Or, on systems based on SuSE Linux you may need to use a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="6bf87-173">De `nofail` optie zorgt ervoor dat de VM start zelfs als het bestandssysteem beschadigd is of de schijf tijdens het opstarten niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="6bf87-173">The `nofail` option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="6bf87-174">Zonder deze optie kunnen optreden gedrag zoals beschreven in [niet kan SSH voor Linux VM vanwege FSTAB-fouten](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="6bf87-174">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="6bf87-175">Nu kunt u testen of het bestandssysteem door ontkoppelen en opnieuw het opstellen van het bestandssysteem, dat wil zeggen correct is gekoppeld</span><span class="sxs-lookup"><span data-stu-id="6bf87-175">You can now test that the file system is mounted properly by unmounting and then remounting the file system, i.e.</span></span> <span data-ttu-id="6bf87-176">in het voorbeeld van een koppelpunt `/datadrive` gemaakt in de eerdere stappen:</span><span class="sxs-lookup"><span data-stu-id="6bf87-176">using the example mount point `/datadrive` created in the earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="6bf87-177">Als de `mount` opdracht, treedt een fout, controleert u het bestand/etc/fstab-fouten voor de juiste syntaxis.</span><span class="sxs-lookup"><span data-stu-id="6bf87-177">If the `mount` command produces an error, check the /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="6bf87-178">Als extra gegevensstations of partities worden gemaakt, / etc/fstab ook afzonderlijk aangaan.</span><span class="sxs-lookup"><span data-stu-id="6bf87-178">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="6bf87-179">Het station beschrijfbare maken door met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6bf87-179">Make the drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="6bf87-180">Een gegevensschijf vervolgens verwijderen zonder te bewerken fstab kan ervoor zorgen dat de virtuele machine niet kunnen worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="6bf87-180">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="6bf87-181">Als dit vaak het geval is, bieden de meeste distributies ofwel de `nofail` en/of `nobootwait` opstarttijd fstab-opties waarmee u een systeem op te starten, zelfs als de schijf niet koppelen aan.</span><span class="sxs-lookup"><span data-stu-id="6bf87-181">If this is a common occurrence, most distributions provide either the `nofail` and/or `nobootwait` fstab options that allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="6bf87-182">Raadpleeg de distributie-documentatie voor meer informatie over deze parameters.</span><span class="sxs-lookup"><span data-stu-id="6bf87-182">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="6bf87-183">TRIM/UNMAP ondersteuning voor Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="6bf87-183">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="6bf87-184">Sommige kernels Linux ondersteuning TRIM/UNMAP bewerkingen voor het negeren van niet-gebruikte blokken op de schijf.</span><span class="sxs-lookup"><span data-stu-id="6bf87-184">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="6bf87-185">Deze bewerkingen zijn voornamelijk nuttig in standard-opslag om te informeren over Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6bf87-185">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="6bf87-186">'S te verwijderen kunt kosten besparen, als u grote bestanden maken en deze vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="6bf87-186">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="6bf87-187">Er zijn twee manieren om in te schakelen TRIM ondersteunen in uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="6bf87-187">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="6bf87-188">Raadpleeg uw distributiepunt gebruikelijke voor de aanbevolen aanpak:</span><span class="sxs-lookup"><span data-stu-id="6bf87-188">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="6bf87-189">Gebruik de `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6bf87-189">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="6bf87-190">In sommige gevallen de `discard` optie prestaties gevolgen kan hebben.</span><span class="sxs-lookup"><span data-stu-id="6bf87-190">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="6bf87-191">U kunt ook uitvoeren de `fstrim` opdracht handmatig vanaf de opdrachtregel of toe te voegen aan uw crontab regelmatig wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="6bf87-191">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="6bf87-192">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="6bf87-192">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="6bf87-193">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="6bf87-193">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="6bf87-194">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="6bf87-194">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="6bf87-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bf87-195">Next Steps</span></span>
<span data-ttu-id="6bf87-196">Meer informatie over het gebruik van uw Linux-VM in de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="6bf87-196">You can read more about using your Linux VM in the following articles:</span></span>

* <span data-ttu-id="6bf87-197">[Aanmelden met een virtuele machine waarop Linux wordt uitgevoerd][Logon]</span><span class="sxs-lookup"><span data-stu-id="6bf87-197">[How to log on to a virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="6bf87-198">Het ontkoppelen van een schijf van een virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="6bf87-198">How to detach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="6bf87-199">De Azure CLI gebruiken met het klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="6bf87-199">Using the Azure CLI with the Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="6bf87-200">Configureren van RAID op een virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="6bf87-200">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="6bf87-201">LVM configureren op een virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="6bf87-201">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
