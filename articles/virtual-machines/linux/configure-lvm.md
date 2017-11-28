---
title: LVM configureren op een virtuele machine met Linux | Microsoft Docs
description: Informatie over het configureren van LVM op Linux in Azure.
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
ms.openlocfilehash: 7926627aaa3f0da935131f491d927ab5cb4b35c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="8fb6d-103">LVM configureren op een virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="8fb6d-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="8fb6d-104">Dit document wordt uitgelegd hoe het configureren van logische Volume Manager (LVM) in uw virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-104">This document will discuss how to configure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="8fb6d-105">Het is mogelijk LVM configureren op elke schijf die is gekoppeld aan de virtuele machine, standaard de meeste cloud afbeeldingen geen LVM geconfigureerd op de schijf met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-105">While it is feasible to configure LVM on any disk attached to the virtual machine, by default most cloud images will not have LVM configured on the OS disk.</span></span> <span data-ttu-id="8fb6d-106">Dit is om problemen te voorkomen met groepen dubbele volume als de besturingssysteemschijf is ooit gekoppeld aan een andere virtuele machine van de dezelfde distributie en het type, dat wil zeggen tijdens een scenario voor herstel.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-106">This is to prevent problems with duplicate volume groups if the OS disk is ever attached to another VM of the same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="8fb6d-107">Daarom is het aanbevolen alleen voor LVM gebruiken op de gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-107">Therefore it is recommended only to use LVM on the data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="8fb6d-108">Lineaire versus striped logische volumes</span><span class="sxs-lookup"><span data-stu-id="8fb6d-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="8fb6d-109">LVM kan worden gebruikt om een aantal fysieke schijven samenvoegen tot één opslagvolume.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-109">LVM can be used to combine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="8fb6d-110">Standaard wordt LVM meestal gemaakt lineaire logische volumes, wat betekent dat de fysieke opslag samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-110">By default LVM will usually create linear logical volumes, which means that the physical storage is concatenated together.</span></span> <span data-ttu-id="8fb6d-111">In dit geval wordt lees-/ schrijfbewerkingen doorgaans alleen worden verzonden voor één schijf.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-111">In this case read/write operations will typically only be sent to a single disk.</span></span> <span data-ttu-id="8fb6d-112">We kunnen daarentegen ook striped logische volumes waar de lees- en schrijfbewerkingen worden gedistribueerd naar meerdere schijven die zijn opgenomen in de groep volume (dat wil zeggen vergelijkbaar met RAID 0) maken.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-112">In contrast, we can also create striped logical volumes where reads and writes are distributed to multiple disks contained in the volume group (i.e. similar to RAID0).</span></span> <span data-ttu-id="8fb6d-113">Voor betere prestaties is het waarschijnlijk wilt u uw logische volumes stripe zodat lees- en schrijfbewerkingen gebruikmaken van alle schijven in de bijgesloten gegevens.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-113">For performance reasons it is likely you will want to stripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="8fb6d-114">Dit document wordt beschreven hoe u verschillende gegevensschijven combineren in een groep één volume en maak vervolgens logische striped volumes.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-114">This document will describe how to combine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="8fb6d-115">De onderstaande stappen zijn enigszins gegeneraliseerd om te werken met de meeste distributies.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-115">The steps below are somewhat generalized to work with most distributions.</span></span> <span data-ttu-id="8fb6d-116">In de meeste gevallen zijn de hulpprogramma's en werkstromen voor het beheren van LVM in Azure niet fundamenteel anders dan andere omgevingen.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-116">In most cases the utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="8fb6d-117">Gebruikelijke ook Raadpleeg de leverancier van uw Linux voor documentatie en aanbevolen procedures voor het gebruik van LVM met uw bepaalde distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="8fb6d-118">Gegevensschijven koppelen</span><span class="sxs-lookup"><span data-stu-id="8fb6d-118">Attaching data disks</span></span>
<span data-ttu-id="8fb6d-119">Een wilt meestal beginnen met twee of meer gegevensschijven zijn leeg bij gebruik van LVM.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-119">One will usually want to start with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="8fb6d-120">Op basis van uw i/o-behoeften, kunt u schijven die zijn opgeslagen in de Standard-opslag, met maximaal 500 i/o/ps per schijf of onze Premium-opslag met maximaal 5000 i/o/ps per schijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-120">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="8fb6d-121">In dit artikel gaat niet informatie over het inrichten en gegevensschijven koppelen aan een virtuele Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-121">This article will not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span> <span data-ttu-id="8fb6d-122">Zie het artikel van Microsoft Azure [een schijf koppelen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor gedetailleerde instructies over hoe u een lege gegevensschijf koppelen aan een virtuele Linux-machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-122">Please see the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-lvm-utilities"></a><span data-ttu-id="8fb6d-123">De hulpprogramma's voor LVM installeren</span><span class="sxs-lookup"><span data-stu-id="8fb6d-123">Install the LVM utilities</span></span>
* <span data-ttu-id="8fb6d-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="8fb6d-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="8fb6d-125">**RHEL, CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="8fb6d-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="8fb6d-126">**SLES 12 en openSUSE**</span><span class="sxs-lookup"><span data-stu-id="8fb6d-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="8fb6d-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="8fb6d-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="8fb6d-128">Op SLES11 moet u ook bewerken `/etc/sysconfig/lvm` en stel `LVM_ACTIVATED_ON_DISCOVERED` naar 'inschakelen':</span><span class="sxs-lookup"><span data-stu-id="8fb6d-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` to "enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="8fb6d-129">LVM configureren</span><span class="sxs-lookup"><span data-stu-id="8fb6d-129">Configure LVM</span></span>
<span data-ttu-id="8fb6d-130">In deze handleiding wordt ervan uitgegaan hebt u drie gegevensschijven die we naar als verwijzen gekoppeld `/dev/sdc`, `/dev/sdd` en `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-130">In this guide we will assume you have attached three data disks, which we'll refer to as `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="8fb6d-131">Houd er rekening mee dat deze altijd mogelijk niet hetzelfde padnamen in uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-131">Note that these may not always be the same path names in your VM.</span></span> <span data-ttu-id="8fb6d-132">U kunt uitvoeren '`sudo fdisk -l`' of een vergelijkbare opdracht om een lijst van uw beschikbare schijven.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-132">You can run '`sudo fdisk -l`' or similar command to list your available disks.</span></span>

1. <span data-ttu-id="8fb6d-133">Bereid de fysieke volumes:</span><span class="sxs-lookup"><span data-stu-id="8fb6d-133">Prepare the physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="8fb6d-134">Een volume-groep maken.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-134">Create a volume group.</span></span> <span data-ttu-id="8fb6d-135">In dit voorbeeld wordt de groep volume belt `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="8fb6d-135">In this example we are calling the volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="8fb6d-136">De logische volumes maken.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-136">Create the logical volume(s).</span></span> <span data-ttu-id="8fb6d-137">De onderstaande opdracht we één logische volume aangeroepen maakt `data-lv01` span van de groep van het gehele volume, maar houd er rekening mee dat het is ook mogelijk meerdere logische om volumes te maken in de groep volume.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-137">The command below we will create a single logical volume called `data-lv01` to span the entire volume group, but note that it is also feasible to create multiple logical volumes in the volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="8fb6d-138">Het logische volume formatteren</span><span class="sxs-lookup"><span data-stu-id="8fb6d-138">Format the logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="8fb6d-139">Bij gebruik van SLES11 `-t ext3` in plaats van ext4.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="8fb6d-140">SLES11 ondersteunt alleen alleen-lezen toegang tot ext4 bestandssystemen.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-140">SLES11 only supports read-only access to ext4 filesystems.</span></span>

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="8fb6d-141">Het nieuwe bestandssysteem aan /etc/fstab toevoegen</span><span class="sxs-lookup"><span data-stu-id="8fb6d-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8fb6d-142">Onjuist bewerken van de `/etc/fstab` bestand kan leiden tot een systeem opgestart.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-142">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="8fb6d-143">Als u niet zeker, raadpleeg dan de distributie-documentatie voor informatie over het correct dit bestand te bewerken.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-143">If unsure, please refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="8fb6d-144">Het is ook aanbevolen een back-up van de `/etc/fstab` bestand is gemaakt voordat u kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-144">It is also recommended that a backup of the `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="8fb6d-145">Maak de gewenste koppelpunt voor het nieuwe bestandssysteem, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8fb6d-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="8fb6d-146">Zoek het logische pad naar het</span><span class="sxs-lookup"><span data-stu-id="8fb6d-146">Locate the logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="8fb6d-147">Open `/etc/fstab` in een teksteditor en voeg een vermelding voor het nieuwe bestandssysteem, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8fb6d-147">Open `/etc/fstab` in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="8fb6d-148">Vervolgens opslaan en sluiten `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="8fb6d-149">Testen of de `/etc/fstab` invoer correct is:</span><span class="sxs-lookup"><span data-stu-id="8fb6d-149">Test that the `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="8fb6d-150">Als u deze opdracht resulteert in een foutbericht Controleer de syntaxis de `/etc/fstab` bestand.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-150">If this command results in an error message please check the syntax in the `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="8fb6d-151">Voer vervolgens de `mount` opdracht om te controleren of het bestandssysteem is gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="8fb6d-151">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="8fb6d-152">(Optioneel) Opstartparameters failsafe in`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="8fb6d-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="8fb6d-153">Groot aantal distributies bevat de `nobootwait` of `nofail` koppelen van de parameters die kunnen worden toegevoegd aan de `/etc/fstab` bestand.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-153">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="8fb6d-154">Deze parameters toestaan voor fouten bij het koppelen van een bepaald bestandssysteem en dat het Linux-systeem om door te gaan om op te starten, zelfs als deze niet correct koppelen het RAID-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-154">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="8fb6d-155">Raadpleeg de distributie-documentatie voor meer informatie over deze parameters.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-155">Please refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="8fb6d-156">Voorbeeld (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="8fb6d-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="8fb6d-157">TRIM/UNMAP-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="8fb6d-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="8fb6d-158">Sommige kernels Linux ondersteuning TRIM/UNMAP bewerkingen voor het negeren van niet-gebruikte blokken op de schijf.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-158">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="8fb6d-159">Deze bewerkingen zijn voornamelijk nuttig in standard-opslag om te informeren over Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-159">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="8fb6d-160">'S te verwijderen kunt kosten besparen, als u grote bestanden maken en deze vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="8fb6d-161">Er zijn twee manieren om in te schakelen TRIM ondersteunen in uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-161">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="8fb6d-162">Raadpleeg uw distributiepunt gebruikelijke voor de aanbevolen aanpak:</span><span class="sxs-lookup"><span data-stu-id="8fb6d-162">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="8fb6d-163">Gebruik de `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8fb6d-163">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="8fb6d-164">In sommige gevallen de `discard` optie prestaties gevolgen kan hebben.</span><span class="sxs-lookup"><span data-stu-id="8fb6d-164">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="8fb6d-165">U kunt ook uitvoeren de `fstrim` opdracht handmatig vanaf de opdrachtregel of toe te voegen aan uw crontab regelmatig wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="8fb6d-165">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="8fb6d-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="8fb6d-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="8fb6d-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="8fb6d-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
