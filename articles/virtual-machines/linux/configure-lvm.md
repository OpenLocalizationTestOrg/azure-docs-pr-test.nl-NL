---
title: aaaConfigure LVM op een virtuele machine met Linux | Microsoft Docs
description: Meer informatie over hoe tooconfigure LVM op Linux in Azure.
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="9238d-103">LVM configureren op een virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="9238d-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="9238d-104">Dit document wordt besproken hoe tooconfigure logische Volume Manager (LVM) in uw virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="9238d-104">This document will discuss how tooconfigure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="9238d-105">Wanneer deze is mogelijk tooconfigure LVM op elke schijf die is gekoppeld toohello virtuele machine, standaard de meeste cloud installatiekopieën geen LVM geconfigureerd op Hallo besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="9238d-105">While it is feasible tooconfigure LVM on any disk attached toohello virtual machine, by default most cloud images will not have LVM configured on hello OS disk.</span></span> <span data-ttu-id="9238d-106">Dit is tooprevent problemen met dubbele volume groepen als besturingssysteemschijf ooit is Hallo gekoppeld tooanother VM Hallo dezelfde distributie en het type, dat wil zeggen tijdens een scenario voor herstel.</span><span class="sxs-lookup"><span data-stu-id="9238d-106">This is tooprevent problems with duplicate volume groups if hello OS disk is ever attached tooanother VM of hello same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="9238d-107">Daarom is het raadzaam alleen toouse LVM op Hallo gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="9238d-107">Therefore it is recommended only toouse LVM on hello data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="9238d-108">Lineaire versus striped logische volumes</span><span class="sxs-lookup"><span data-stu-id="9238d-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="9238d-109">LVM mag gebruikte toocombine een aantal fysieke schijven in één opslagvolume.</span><span class="sxs-lookup"><span data-stu-id="9238d-109">LVM can be used toocombine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="9238d-110">Standaard wordt LVM meestal gemaakt lineaire logische volumes, wat betekent dat fysieke opslag Hallo samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="9238d-110">By default LVM will usually create linear logical volumes, which means that hello physical storage is concatenated together.</span></span> <span data-ttu-id="9238d-111">In dit geval worden lees-/ schrijfbewerkingen doorgaans alleen verzonden tooa één schijf.</span><span class="sxs-lookup"><span data-stu-id="9238d-111">In this case read/write operations will typically only be sent tooa single disk.</span></span> <span data-ttu-id="9238d-112">We kunnen daarentegen ook striped logische volumes waarop lees- en schrijfbewerkingen gedistribueerde toomultiple schijven die zijn opgenomen in de groep van Hallo-volume (dat wil zeggen vergelijkbare tooRAID0 zijn) maken.</span><span class="sxs-lookup"><span data-stu-id="9238d-112">In contrast, we can also create striped logical volumes where reads and writes are distributed toomultiple disks contained in hello volume group (i.e. similar tooRAID0).</span></span> <span data-ttu-id="9238d-113">Voor betere prestaties is het waarschijnlijk zult u toostripe uw logische volumes zodat lees- en schrijfbewerkingen gebruikmaken van alle schijven in de bijgesloten gegevens.</span><span class="sxs-lookup"><span data-stu-id="9238d-113">For performance reasons it is likely you will want toostripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="9238d-114">Dit document wordt beschreven hoe toocombine gegevens van verschillende schijven in een groep één volume en maak vervolgens logische striped volumes.</span><span class="sxs-lookup"><span data-stu-id="9238d-114">This document will describe how toocombine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="9238d-115">Hallo onderstaande stappen zijn enigszins gegeneraliseerde toowork met de meeste distributies.</span><span class="sxs-lookup"><span data-stu-id="9238d-115">hello steps below are somewhat generalized toowork with most distributions.</span></span> <span data-ttu-id="9238d-116">In de meeste gevallen Hallo hulpprogramma's en werkstromen voor het beheren van LVM in Azure zijn niet fundamenteel anders dan andere omgevingen.</span><span class="sxs-lookup"><span data-stu-id="9238d-116">In most cases hello utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="9238d-117">Gebruikelijke ook Raadpleeg de leverancier van uw Linux voor documentatie en aanbevolen procedures voor het gebruik van LVM met uw bepaalde distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="9238d-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="9238d-118">Gegevensschijven koppelen</span><span class="sxs-lookup"><span data-stu-id="9238d-118">Attaching data disks</span></span>
<span data-ttu-id="9238d-119">Een zult meestal toostart met twee of meer gegevensschijven zijn leeg bij gebruik van LVM.</span><span class="sxs-lookup"><span data-stu-id="9238d-119">One will usually want toostart with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="9238d-120">Op basis van uw i/o-behoeften, kunt u tooattach schijven die zijn opgeslagen in de Standard-opslag met up too500 i/o/ps per schijf of onze Premium-opslag met up too5000 i/o/ps per schijf.</span><span class="sxs-lookup"><span data-stu-id="9238d-120">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="9238d-121">In dit artikel wordt niet ingegaan op de details over het tooprovision en koppelt u gegevens schijven tooa virtuele Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="9238d-121">This article will not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span> <span data-ttu-id="9238d-122">Zie de Microsoft Azure-artikel Hallo [een schijf koppelen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor gedetailleerde instructies over hoe tooattach gegevens in een lege schijf tooa virtuele Linux-machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="9238d-122">Please see hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-lvm-utilities"></a><span data-ttu-id="9238d-123">Hallo LVM hulpprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="9238d-123">Install hello LVM utilities</span></span>
* <span data-ttu-id="9238d-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="9238d-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="9238d-125">**RHEL, CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="9238d-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="9238d-126">**SLES 12 en openSUSE**</span><span class="sxs-lookup"><span data-stu-id="9238d-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="9238d-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="9238d-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="9238d-128">Op SLES11 moet u ook bewerken `/etc/sysconfig/lvm` en stel `LVM_ACTIVATED_ON_DISCOVERED` te 'inschakelen':</span><span class="sxs-lookup"><span data-stu-id="9238d-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` too"enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="9238d-129">LVM configureren</span><span class="sxs-lookup"><span data-stu-id="9238d-129">Configure LVM</span></span>
<span data-ttu-id="9238d-130">In deze handleiding wordt ervan uitgegaan hebt u drie gegevensschijven die we verwijzen gekoppeld tooas `/dev/sdc`, `/dev/sdd` en `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="9238d-130">In this guide we will assume you have attached three data disks, which we'll refer tooas `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="9238d-131">Opmerking deze niet kunnen worden altijd Hallo dezelfde padnamen in uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9238d-131">Note that these may not always be hello same path names in your VM.</span></span> <span data-ttu-id="9238d-132">U kunt uitvoeren '`sudo fdisk -l`' of een vergelijkbare opdracht toolist uw beschikbare schijven.</span><span class="sxs-lookup"><span data-stu-id="9238d-132">You can run '`sudo fdisk -l`' or similar command toolist your available disks.</span></span>

1. <span data-ttu-id="9238d-133">Hallo fysieke volumes voorbereiden:</span><span class="sxs-lookup"><span data-stu-id="9238d-133">Prepare hello physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="9238d-134">Een volume-groep maken.</span><span class="sxs-lookup"><span data-stu-id="9238d-134">Create a volume group.</span></span> <span data-ttu-id="9238d-135">In dit voorbeeld we Hallo volume groep bellen `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="9238d-135">In this example we are calling hello volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="9238d-136">Hallo logische of meer volumes maken.</span><span class="sxs-lookup"><span data-stu-id="9238d-136">Create hello logical volume(s).</span></span> <span data-ttu-id="9238d-137">Hallo we onderstaande opdracht maakt u één logische volume aangeroepen `data-lv01` toospan Hallo hele volume groeperen, maar het is ook mogelijk toocreate Opmerking meerdere logische volumes in Hallo volume groep.</span><span class="sxs-lookup"><span data-stu-id="9238d-137">hello command below we will create a single logical volume called `data-lv01` toospan hello entire volume group, but note that it is also feasible toocreate multiple logical volumes in hello volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="9238d-138">Logische Hallo-volume formatteren</span><span class="sxs-lookup"><span data-stu-id="9238d-138">Format hello logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="9238d-139">Bij gebruik van SLES11 `-t ext3` in plaats van ext4.</span><span class="sxs-lookup"><span data-stu-id="9238d-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="9238d-140">SLES11 ondersteunt alleen-lezentoegang tooext4 bestandssystemen.</span><span class="sxs-lookup"><span data-stu-id="9238d-140">SLES11 only supports read-only access tooext4 filesystems.</span></span>

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="9238d-141">Hallo nieuwe file system te/etc/fstab toevoegen</span><span class="sxs-lookup"><span data-stu-id="9238d-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9238d-142">Onjuist bewerken van Hallo `/etc/fstab` bestand kan leiden tot een systeem opgestart.</span><span class="sxs-lookup"><span data-stu-id="9238d-142">Improperly editing hello `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="9238d-143">Als u niet zeker, Zie toohello distributie van documentatie voor informatie over hoe tooproperly dit bestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="9238d-143">If unsure, please refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="9238d-144">Het is ook aanbevolen een back-up van Hallo `/etc/fstab` bestand is gemaakt voordat u kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="9238d-144">It is also recommended that a backup of hello `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="9238d-145">Maak Hallo gewenst koppelpunt voor het nieuwe bestandssysteem, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9238d-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="9238d-146">Hallo logisch Volumepad vinden</span><span class="sxs-lookup"><span data-stu-id="9238d-146">Locate hello logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="9238d-147">Open `/etc/fstab` in een teksteditor en voeg een vermelding voor het nieuwe bestandssysteem hello, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9238d-147">Open `/etc/fstab` in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="9238d-148">Vervolgens opslaan en sluiten `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="9238d-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="9238d-149">Testen die Hallo `/etc/fstab` invoer correct is:</span><span class="sxs-lookup"><span data-stu-id="9238d-149">Test that hello `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="9238d-150">Als u deze opdracht resulteert in een foutbericht Controleer Hallo syntaxis in Hallo `/etc/fstab` bestand.</span><span class="sxs-lookup"><span data-stu-id="9238d-150">If this command results in an error message please check hello syntax in hello `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="9238d-151">Voer vervolgens Hallo `mount` opdracht tooensure Hallo-bestandssysteem is gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="9238d-151">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="9238d-152">(Optioneel) Opstartparameters failsafe in`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="9238d-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="9238d-153">Groot aantal distributies zijn beide Hallo `nobootwait` of `nofail` koppelen van de parameters die kunnen worden toegevoegd als toohello `/etc/fstab` bestand.</span><span class="sxs-lookup"><span data-stu-id="9238d-153">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello `/etc/fstab` file.</span></span> <span data-ttu-id="9238d-154">Deze parameters toestaan voor fouten bij het koppelen van een bepaald bestandssysteem en Hallo Linux system toocontinue tooboot toestaan, zelfs als deze tooproperly koppelpunt Hallo RAID-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="9238d-154">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="9238d-155">Raadpleeg tooyour distributie van documentatie voor meer informatie over deze parameters.</span><span class="sxs-lookup"><span data-stu-id="9238d-155">Please refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="9238d-156">Voorbeeld (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="9238d-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="9238d-157">TRIM/UNMAP-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="9238d-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="9238d-158">Sommige kernels Linux ondersteunen TRIM/UNMAP operations toodiscard niet-gebruikte blokken op Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="9238d-158">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="9238d-159">Deze bewerkingen zijn voornamelijk nuttig in standard-opslag tooinform Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9238d-159">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="9238d-160">'S te verwijderen kunt kosten besparen, als u grote bestanden maken en deze vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9238d-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="9238d-161">Er zijn twee manieren tooenable TRIM ondersteunen in uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="9238d-161">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="9238d-162">Raadpleeg uw distributiepunt gebruikelijke voor Hallo aanbevolen benadering:</span><span class="sxs-lookup"><span data-stu-id="9238d-162">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="9238d-163">Gebruik Hallo `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9238d-163">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="9238d-164">In sommige gevallen Hallo `discard` optie prestaties gevolgen kan hebben.</span><span class="sxs-lookup"><span data-stu-id="9238d-164">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="9238d-165">U kunt ook uitvoeren Hallo `fstrim` opdracht handmatig vanaf de opdrachtregel Hallo of voeg tooyour crontab toorun regelmatig:</span><span class="sxs-lookup"><span data-stu-id="9238d-165">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="9238d-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="9238d-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="9238d-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="9238d-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
