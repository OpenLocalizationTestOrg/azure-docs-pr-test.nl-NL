---
title: aaaConfigure software-RAID op een virtuele machine met Linux | Microsoft Docs
description: Meer informatie over hoe toouse mdadm tooconfigure RAID op Linux in Azure.
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="4ee3a-103">Software-RAID configureren onder Linux</span><span class="sxs-lookup"><span data-stu-id="4ee3a-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="4ee3a-104">Het is een algemene scenario toouse software RAID op Linux virtuele machines in Azure toopresent bijgesloten gegevens meerdere als een enkel RAID-apparaat schijven.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-104">It's a common scenario toouse software RAID on Linux virtual machines in Azure toopresent multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="4ee3a-105">Dit kan doorgaans worden gebruikte tooimprove prestaties en toestaan voor verbeterde doorvoer vergeleken toousing één schijf.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-105">Typically this can be used tooimprove performance and allow for improved throughput compared toousing just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="4ee3a-106">Gegevensschijven koppelen</span><span class="sxs-lookup"><span data-stu-id="4ee3a-106">Attaching data disks</span></span>
<span data-ttu-id="4ee3a-107">Twee of meer leeg gegevensschijven zijn benodigde tooconfigure een RAID-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-107">Two or more empty data disks are needed tooconfigure a RAID device.</span></span>  <span data-ttu-id="4ee3a-108">Hallo primaire reden voor het maken van een RAID-apparaat is tooimprove prestaties van de schijf-i/o.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-108">hello primary reason for creating a RAID device is tooimprove performance of your disk IO.</span></span>  <span data-ttu-id="4ee3a-109">Op basis van uw i/o-behoeften, kunt u tooattach schijven die zijn opgeslagen in de Standard-opslag met up too500 i/o/ps per schijf of onze Premium-opslag met up too5000 i/o/ps per schijf.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-109">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="4ee3a-110">In dit artikel gaat niet informatie over het tooprovision en koppelt u gegevens schijven tooa virtuele Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-110">This article does not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span>  <span data-ttu-id="4ee3a-111">Zie de Microsoft Azure-artikel Hallo [een schijf koppelen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor gedetailleerde instructies over hoe tooattach gegevens in een lege schijf tooa virtuele Linux-machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-111">See hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-mdadm-utility"></a><span data-ttu-id="4ee3a-112">Hallo mdadm hulpprogramma installeren</span><span class="sxs-lookup"><span data-stu-id="4ee3a-112">Install hello mdadm utility</span></span>
* <span data-ttu-id="4ee3a-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="4ee3a-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="4ee3a-114">**CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="4ee3a-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="4ee3a-115">**SLES en openSUSE**</span><span class="sxs-lookup"><span data-stu-id="4ee3a-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a><span data-ttu-id="4ee3a-116">Hallo partities op schijf maken</span><span class="sxs-lookup"><span data-stu-id="4ee3a-116">Create hello disk partitions</span></span>
<span data-ttu-id="4ee3a-117">In dit voorbeeld maken we een enkele schijfpartitie op /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="4ee3a-118">nieuwe schijfpartitie Hallo wordt /dev/sdc1 aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-118">hello new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="4ee3a-119">Start `fdisk` toobegin partities maken</span><span class="sxs-lookup"><span data-stu-id="4ee3a-119">Start `fdisk` toobegin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="4ee3a-120">Tik op "n" op Hallo vragen toocreate een  **n** euwe partitie:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-120">Press 'n' at hello prompt toocreate a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="4ee3a-121">Druk op 'p' toocreate een **p**rimaire partitie:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-121">Next, press 'p' toocreate a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="4ee3a-122">Druk op '1' tooselect partitienummer 1:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-122">Press '1' tooselect partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="4ee3a-123">Selecteer het beginpunt van een nieuwe partitie Hallo of druk op Hallo `<enter>` tooaccept hello tooplace Hallo standaardpartitie aan begin Hallo Hallo vrije ruimte op station Hallo:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-123">Select hello starting point of hello new partition, or press `<enter>` tooaccept hello default tooplace hello partition at hello beginning of hello free space on hello drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="4ee3a-124">Selecteer Hallo grootte van Hallo partitie, bijvoorbeeld '+10G' type toocreate een 10 GB-partitie.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-124">Select hello size of hello partition, for example type '+10G' toocreate a 10 gigabyte partition.</span></span> <span data-ttu-id="4ee3a-125">Of druk op `<enter>` maken van een enkele partitie die de hele station Hallo omvat:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-125">Or, press `<enter>` create a single partition that spans hello entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="4ee3a-126">Hallo-ID vervolgens wijzigen en **t**ype Hallo partitie van Hallo standaard-ID '83' (Linux) tooID 'fd' (Linux raid automatisch):</span><span class="sxs-lookup"><span data-stu-id="4ee3a-126">Next, change hello ID and **t**ype of hello partition from hello default ID '83' (Linux) tooID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. <span data-ttu-id="4ee3a-127">Ten slotte Schrijf Hallo partitie tabel toohello station en fdisk sluiten:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-127">Finally, write hello partition table toohello drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a><span data-ttu-id="4ee3a-128">Hallo RAID-matrix maken</span><span class="sxs-lookup"><span data-stu-id="4ee3a-128">Create hello RAID array</span></span>
1. <span data-ttu-id="4ee3a-129">Hallo volgende voorbeeld wordt 'stripe' (RAID-niveau 0) drie partities zich op drie aparte gegevensschijven (sdc1, sdd1, sde1).</span><span class="sxs-lookup"><span data-stu-id="4ee3a-129">hello following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="4ee3a-130">Nadat u deze opdracht uitvoert op een nieuw RAID-apparaat aangeroepen **/dev/md127** wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="4ee3a-131">Let ook op dat als deze gegevens schijven we eerder onderdeel van een andere uitgeschakelde RAID-matrix mogelijk nodig tooadd hello `--force` parameter toohello `mdadm` opdracht:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary tooadd hello `--force` parameter toohello `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="4ee3a-132">Hallo-bestandssysteem op Hallo nieuwe RAID-apparaat maken</span><span class="sxs-lookup"><span data-stu-id="4ee3a-132">Create hello file system on hello new RAID device</span></span>
   
    <span data-ttu-id="4ee3a-133">a.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-133">a.</span></span> <span data-ttu-id="4ee3a-134">**CentOS, Oracle Linux SLES 12, openSUSE en Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="4ee3a-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="4ee3a-135">b.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-135">b.</span></span> <span data-ttu-id="4ee3a-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="4ee3a-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="4ee3a-137">c.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-137">c.</span></span> <span data-ttu-id="4ee3a-138">**SLES 11** - boot.md inschakelen en mdadm.conf maken</span><span class="sxs-lookup"><span data-stu-id="4ee3a-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="4ee3a-139">Opnieuw opstarten nadat u deze wijzigingen aanbrengt op SUSE systemen mogelijk vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="4ee3a-140">Deze stap is *niet* vereist voor SLES 12.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="4ee3a-141">Hallo nieuwe file system te/etc/fstab toevoegen</span><span class="sxs-lookup"><span data-stu-id="4ee3a-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4ee3a-142">Hallo /etc/fstab bestand onjuist bewerkt, kan dit leiden tot een systeem opgestart.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-142">Improperly editing hello /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="4ee3a-143">Als u niet zeker, Raadpleeg toohello distributie van documentatie voor informatie over hoe tooproperly dit bestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-143">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="4ee3a-144">Het is ook raadzaam dat een back-up van Hallo /etc/fstab bestand is gemaakt voordat u bewerkt.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-144">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="4ee3a-145">Maak Hallo gewenst koppelpunt voor het nieuwe bestandssysteem, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="4ee3a-146">Bij het bewerken van /etc/fstab Hallo **UUID** moet gebruikte tooreference Hallo file system in plaats van Hallo apparaatnaam.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-146">When editing /etc/fstab, hello **UUID** should be used tooreference hello file system rather than hello device name.</span></span>  <span data-ttu-id="4ee3a-147">Gebruik Hallo `blkid` hulpprogramma toodetermine Hallo UUID voor het nieuwe bestandssysteem Hallo:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-147">Use hello `blkid` utility toodetermine hello UUID for hello new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="4ee3a-148">Open /etc/fstab in een teksteditor en voeg een vermelding voor het nieuwe bestandssysteem hello, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-148">Open /etc/fstab in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="4ee3a-149">Of op **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="4ee3a-150">Vervolgens opslaan en sluiten /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="4ee3a-151">Testen die Hallo/etc/fstab-invoer correct is:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-151">Test that hello /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="4ee3a-152">Als deze opdracht in een foutbericht weergegeven resulteert, controleert u Hallo syntaxis in Hallo /etc/fstab bestand.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-152">If this command results in an error message, please check hello syntax in hello /etc/fstab file.</span></span>
   
    <span data-ttu-id="4ee3a-153">Voer vervolgens Hallo `mount` opdracht tooensure Hallo-bestandssysteem is gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-153">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="4ee3a-154">(Optioneel) Opstartparameters failsafe</span><span class="sxs-lookup"><span data-stu-id="4ee3a-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="4ee3a-155">**fstab-configuratie**</span><span class="sxs-lookup"><span data-stu-id="4ee3a-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="4ee3a-156">Groot aantal distributies zijn beide Hallo `nobootwait` of `nofail` parameters die kunnen worden toegevoegd als toohello bestand/etc/fstab koppelen.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-156">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello /etc/fstab file.</span></span> <span data-ttu-id="4ee3a-157">Deze parameters toestaan voor fouten bij het koppelen van een bepaald bestandssysteem en Hallo Linux system toocontinue tooboot toestaan, zelfs als deze tooproperly koppelpunt Hallo RAID-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-157">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="4ee3a-158">Raadpleeg tooyour distributie van documentatie voor meer informatie over deze parameters.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-158">Refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="4ee3a-159">Voorbeeld (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="4ee3a-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="4ee3a-160">**Linux-opstartparameters**</span><span class="sxs-lookup"><span data-stu-id="4ee3a-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="4ee3a-161">Hallo in toevoeging toohello hierboven parameters, kernel-parameter '`bootdegraded=true`' hello system tooboot kunt toestaan, zelfs als Hallo RAID wordt beschouwd als beschadigd of gedegradeerd, bijvoorbeeld als een gegevensstation per ongeluk is verwijderd van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-161">In addition toohello above parameters, hello kernel parameter "`bootdegraded=true`" can allow hello system tooboot even if hello RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from hello virtual machine.</span></span> <span data-ttu-id="4ee3a-162">Standaard kan dit ook leiden tot een niet-opstartbare systeem.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="4ee3a-163">Raadpleeg de documentatie op hoe de kernel-parameters voor het bewerken van tooproperly tooyour distributie van.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-163">Please refer tooyour distribution's documentation on how tooproperly edit kernel parameters.</span></span> <span data-ttu-id="4ee3a-164">Bijvoorbeeld in een groot aantal distributies (CentOS, Oracle Linux, SLES 11) deze parameters kunnen handmatig worden toegevoegd toohello '`/boot/grub/menu.lst`' bestand.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually toohello "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="4ee3a-165">Op Ubuntu deze parameter kan worden toegevoegd toohello `GRUB_CMDLINE_LINUX_DEFAULT` variabele op '/ etc/standaard/grub'.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-165">On Ubuntu this parameter can be added toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="4ee3a-166">TRIM/UNMAP-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="4ee3a-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="4ee3a-167">Sommige kernels Linux ondersteunen TRIM/UNMAP operations toodiscard niet-gebruikte blokken op Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-167">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="4ee3a-168">Deze bewerkingen zijn voornamelijk nuttig in standard-opslag tooinform Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-168">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="4ee3a-169">'S te verwijderen kunt kosten besparen, als u grote bestanden maken en deze vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="4ee3a-170">RAID kan geen verwijderde opdrachten uitgeven als Hallo chunkgrootte voor de matrix Hallo tooless dan Hallo-standaard (512KB) is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-170">RAID may not issue discard commands if hello chunk size for hello array is set tooless than hello default (512KB).</span></span> <span data-ttu-id="4ee3a-171">Dit komt doordat Hallo ontkoppelen granulatie op Hallo Host is ook 512KB.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-171">This is because hello unmap granularity on hello Host is also 512KB.</span></span> <span data-ttu-id="4ee3a-172">Als u de chunkgrootte van Hallo matrix via mdadm van gewijzigd `--chunk=` parameter en klik vervolgens TRIM/ontkoppelen aanvragen kunnen worden genegeerd door de kernel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-172">If you modified hello array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by hello kernel.</span></span>

<span data-ttu-id="4ee3a-173">Er zijn twee manieren tooenable TRIM ondersteunen in uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-173">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="4ee3a-174">Raadpleeg uw distributiepunt gebruikelijke voor Hallo aanbevolen benadering:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-174">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="4ee3a-175">Gebruik Hallo `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-175">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="4ee3a-176">In sommige gevallen Hallo `discard` optie prestaties gevolgen kan hebben.</span><span class="sxs-lookup"><span data-stu-id="4ee3a-176">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="4ee3a-177">U kunt ook uitvoeren Hallo `fstrim` opdracht handmatig vanaf de opdrachtregel Hallo of voeg tooyour crontab toorun regelmatig:</span><span class="sxs-lookup"><span data-stu-id="4ee3a-177">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="4ee3a-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="4ee3a-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="4ee3a-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="4ee3a-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
