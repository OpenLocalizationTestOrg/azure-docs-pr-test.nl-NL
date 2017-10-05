---
title: Een schijf toevoegen aan de Linux-VM met de Azure CLI | Microsoft Docs
description: Meer informatie over een permanente schijf toevoegen aan uw Linux-VM met de Azure CLI 1.0 en 2.0.
keywords: virtuele Linux-machine, resource-schijf toevoegen
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 3005a066-7a84-4dc5-bdaa-574c75e6e411
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 02/02/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 185dd276cd79cb7053605d651e8ecdc7fd1e7636
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-disk-to-a-linux-vm"></a><span data-ttu-id="9fb67-104">Een schijf toevoegen aan een virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="9fb67-104">Add a disk to a Linux VM</span></span>
<span data-ttu-id="9fb67-105">In dit artikel laat zien hoe een permanente schijf koppelen met uw virtuele machine zodat u kunt uw gegevens - zelfs als uw virtuele machine is ingericht vanwege onderhoud vergroten of verkleinen.</span><span class="sxs-lookup"><span data-stu-id="9fb67-105">This article shows how to attach a persistent disk to your VM so that you can preserve your data - even if your VM is reprovisioned due to maintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="9fb67-106">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="9fb67-106">Quick Commands</span></span>
<span data-ttu-id="9fb67-107">Het volgende voorbeeld wordt een `50`GB schijf naar de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9fb67-107">The following example attaches a `50`GB disk to the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="9fb67-108">Beheerde schijven gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9fb67-108">To use managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="9fb67-109">Niet-beheerde schijven gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9fb67-109">To use unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="9fb67-110">Een beheerde schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="9fb67-110">Attach a managed disk</span></span>

<span data-ttu-id="9fb67-111">Beheerde schijven kunt u zich kunt richten op uw virtuele machines en hun schijven zonder dat u Azure Storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="9fb67-111">Using managed disks enables you to focus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="9fb67-112">Kunt u snel maken en een beheerde schijf koppelen aan een virtuele machine met behulp van de dezelfde Azure-resourcegroep, of u kunt een willekeurig aantal schijven maken en deze vervolgens te koppelen.</span><span class="sxs-lookup"><span data-stu-id="9fb67-112">You can quickly create and attach a managed disk to a VM using the same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-to-a-vm"></a><span data-ttu-id="9fb67-113">Een nieuwe schijf koppelen aan een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="9fb67-113">Attach a new disk to a VM</span></span>

<span data-ttu-id="9fb67-114">Als u alleen een nieuwe schijf nodig op de virtuele machine, kunt u de `az vm disk attach` opdracht.</span><span class="sxs-lookup"><span data-stu-id="9fb67-114">If you just need a new disk on your VM, you can use the `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="9fb67-115">Een bestaande schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="9fb67-115">Attach an existing disk</span></span> 

<span data-ttu-id="9fb67-116">In veel gevallen koppelt u de schijven die al zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9fb67-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="9fb67-117">U eerst de schijf-id vinden en geeft die aan de `az vm disk attach` opdracht.</span><span class="sxs-lookup"><span data-stu-id="9fb67-117">You first find the disk id and then pass that to the `az vm disk attach` command.</span></span> <span data-ttu-id="9fb67-118">Het volgende voorbeeld wordt een schijf die is gemaakt met `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="9fb67-118">The following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find the disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="9fb67-119">De uitvoer ziet er ongeveer als volgt (u kunt de `-o table` optie als u wilt willekeurige opdracht van de uitvoer in opmaken):</span><span class="sxs-lookup"><span data-stu-id="9fb67-119">The output looks something like the following (you can use the `-o table` option to any command to format the output in ):</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Empty",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 50,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/rasquill-script/providers/Microsoft.Compute/disks/myDataDisk",
  "location": "westus",
  "name": "myDataDisk",
  "osType": null,
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-02T23:35:47.708082+00:00",
  "type": "Microsoft.Compute/disks"
}
```


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="9fb67-120">Een niet-beheerde schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="9fb67-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="9fb67-121">Een nieuwe schijf koppelen is snelle als u niet erg vindt voor het maken van een schijf in hetzelfde opslagaccount als uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9fb67-121">Attaching a new disk is quick if you do not mind creating a disk in the same storage account as your VM.</span></span> <span data-ttu-id="9fb67-122">Type `azure vm disk attach-new` maken en koppelen van een nieuwe schijf GB voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9fb67-122">Type `azure vm disk attach-new` to create and attach a new GB disk for your VM.</span></span> <span data-ttu-id="9fb67-123">Als u een opslagaccount niet expliciet identificeren, wordt de schijf die u maakt geplaatst in hetzelfde opslagaccount waarin de OS-schijf zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="9fb67-123">If you do not explicitly identify a storage account, any disk you create is placed in the same storage account where your OS disk resides.</span></span> <span data-ttu-id="9fb67-124">Het volgende voorbeeld wordt een `50`GB schijf naar de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9fb67-124">The following example attaches a `50`GB disk to the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-to-the-linux-vm-to-mount-the-new-disk"></a><span data-ttu-id="9fb67-125">Verbinding maken met de Linux-VM naar de nieuwe schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="9fb67-125">Connect to the Linux VM to mount the new disk</span></span>
> [!NOTE]
> <span data-ttu-id="9fb67-126">In dit onderwerp maakt verbinding met een virtuele machine met behulp van gebruikersnamen en wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="9fb67-126">This topic connects to a VM using usernames and passwords.</span></span> <span data-ttu-id="9fb67-127">Zie voor het gebruik van paren van openbare en persoonlijke sleutels om te communiceren met uw virtuele machine, [het gebruik van SSH met Linux op Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9fb67-127">To use public and private key pairs to communicate with your VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="9fb67-128">U moet SSH in uw Azure-virtuele machine aan partitie formatteren en de nieuwe schijf koppelen zodat uw Linux-VM kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9fb67-128">You need to SSH into your Azure VM to partition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="9fb67-129">Als u niet bekend bent met verbinding te maken met **ssh**, de opdracht heeft de vorm `ssh <username>@<FQDNofAzureVM> -p <the ssh port>`, en ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="9fb67-129">If you're not familiar with connecting with **ssh**, the command takes the form `ssh <username>@<FQDNofAzureVM> -p <the ssh port>`, and looks like the following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="9fb67-130">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="9fb67-130">Output</span></span>

```bash
The authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) to the list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome to Ubuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

* Documentation:  https://help.ubuntu.com/

System information as of Fri May 22 21:02:32 UTC 2015

System load: 0.37              Memory usage: 2%   Processes:       207
Usage of /:  41.4% of 1.94GB   Swap usage:   0%   Users logged in: 0

Graph this data and manage this system at:
  https://landscape.canonical.com/

Get cloud support with Ubuntu Advantage Cloud Guest:
  http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ops@myVM:~$
```

<span data-ttu-id="9fb67-131">Nu dat u met uw virtuele machine verbonden bent, kunt u kunt een schijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="9fb67-131">Now that you're connected to your VM, you're ready to attach a disk.</span></span>  <span data-ttu-id="9fb67-132">Zoek eerst de schijf met behulp van `dmesg | grep SCSI` (de methode die u gebruikt voor het detecteren van de nieuwe schijf kan variëren).</span><span class="sxs-lookup"><span data-stu-id="9fb67-132">First find the disk, using `dmesg | grep SCSI` (the method you use to discover your new disk may vary).</span></span> <span data-ttu-id="9fb67-133">In dit geval wordt er ongeveer als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="9fb67-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="9fb67-134">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="9fb67-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="9fb67-135">en in het geval van dit onderwerp, de `sdc` schijf is die we willen.</span><span class="sxs-lookup"><span data-stu-id="9fb67-135">and in the case of this topic, the `sdc` disk is the one that we want.</span></span> <span data-ttu-id="9fb67-136">De schijf met nu partitioneren `sudo fdisk /dev/sdc` --ervan uitgaande dat in uw geval de schijf is `sdc`, en u een primaire schijf op partitie 1 maken en de andere standaardinstellingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="9fb67-136">Now partition the disk with `sudo fdisk /dev/sdc` -- assuming that in your case the disk was `sdc`, and make it a primary disk on partition 1, and accept the other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="9fb67-137">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="9fb67-137">Output</span></span>

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

<span data-ttu-id="9fb67-138">De partitie maken door te typen `p` bij de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="9fb67-138">Create the partition by typing `p` at the prompt:</span></span>

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

<span data-ttu-id="9fb67-139">En een bestandssysteem schrijven naar de partitie met behulp van de **mkfs** opdracht opgeven van het type van uw bestandssysteem en de naam van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="9fb67-139">And write a file system to the partition by using the **mkfs** command, specifying your filesystem type and the device name.</span></span> <span data-ttu-id="9fb67-140">In dit onderwerp we maken gebruik van `ext4` en `/dev/sdc1` van boven:</span><span class="sxs-lookup"><span data-stu-id="9fb67-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="9fb67-141">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="9fb67-141">Output</span></span>

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

<span data-ttu-id="9fb67-142">Nu we een directory maken te koppelen van het bestandssysteem via `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="9fb67-142">Now we create a directory to mount the file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="9fb67-143">En koppelt u het gebruik van de directory `mount`:</span><span class="sxs-lookup"><span data-stu-id="9fb67-143">And you mount the directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="9fb67-144">De gegevensschijf is nu gereed voor gebruik als `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="9fb67-144">The data disk is now ready to use as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="9fb67-145">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="9fb67-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="9fb67-146">Om te controleren of dat de schijf automatisch opnieuw wordt gekoppeld na opnieuw opstarten moet deze worden toegevoegd aan het bestand/etc/fstab-fouten.</span><span class="sxs-lookup"><span data-stu-id="9fb67-146">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="9fb67-147">Bovendien is het raadzaam dat de UUID (Universally Unique IDentifier) wordt gebruikt in/etc/fstab om te verwijzen naar het station in plaats van alleen de naam van het apparaat (zoals `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="9fb67-147">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="9fb67-148">Als het besturingssysteem een schijffout tijdens het opstarten detecteert, voorkomt met behulp van de UUID de onjuiste schijf wordt gekoppeld aan een bepaalde locatie.</span><span class="sxs-lookup"><span data-stu-id="9fb67-148">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span></span> <span data-ttu-id="9fb67-149">Resterende gegevensschijven zou worden toegewezen die dezelfde apparaat-id.</span><span class="sxs-lookup"><span data-stu-id="9fb67-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="9fb67-150">Als de UUID van het nieuwe station zoekt, volgt u de **blkid** hulpprogramma:</span><span class="sxs-lookup"><span data-stu-id="9fb67-150">To find the UUID of the new drive, use the **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="9fb67-151">De uitvoer ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="9fb67-151">The output looks similar to the following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="9fb67-152">Onjuist bewerken van de **/etc/fstab** bestand kan leiden tot een systeem opgestart.</span><span class="sxs-lookup"><span data-stu-id="9fb67-152">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="9fb67-153">Als u niet zeker, Raadpleeg de distributie-documentatie voor informatie over het correct dit bestand te bewerken.</span><span class="sxs-lookup"><span data-stu-id="9fb67-153">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="9fb67-154">Het is ook raadzaam dat een back-up van het bestand /etc/fstab is gemaakt voordat u bewerkt.</span><span class="sxs-lookup"><span data-stu-id="9fb67-154">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="9fb67-155">Open vervolgens de **/etc/fstab** bestand in een teksteditor:</span><span class="sxs-lookup"><span data-stu-id="9fb67-155">Next, open the **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="9fb67-156">In dit voorbeeld gebruiken we de UUID-waarde voor de nieuwe **/dev/sdc1** apparaat dat is gemaakt in de vorige stappen en het koppelpunt **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="9fb67-156">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="9fb67-157">Voeg de volgende regel toe aan het einde van de **/etc/fstab** bestand:</span><span class="sxs-lookup"><span data-stu-id="9fb67-157">Add the following line to the end of the **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="9fb67-158">Later een gegevensschijf verwijderen zonder te bewerken fstab kan ervoor zorgen dat de virtuele machine niet kunnen worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="9fb67-158">Later removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="9fb67-159">De meeste distributies Geef ofwel de `nofail` en/of `nobootwait` fstab-opties.</span><span class="sxs-lookup"><span data-stu-id="9fb67-159">Most distributions provide either the `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="9fb67-160">Deze opties kunt een systeem op te starten, zelfs als de schijf niet koppelen tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="9fb67-160">These options allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="9fb67-161">Raadpleeg de distributie-documentatie voor meer informatie over deze parameters.</span><span class="sxs-lookup"><span data-stu-id="9fb67-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="9fb67-162">De **nofail** optie zorgt ervoor dat de VM start zelfs als het bestandssysteem beschadigd is of de schijf tijdens het opstarten niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="9fb67-162">The **nofail** option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="9fb67-163">Zonder deze optie kunnen optreden gedrag zoals beschreven in [niet kan SSH voor Linux VM vanwege FSTAB-fouten](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span><span class="sxs-lookup"><span data-stu-id="9fb67-163">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="9fb67-164">TRIM/UNMAP ondersteuning voor Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="9fb67-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="9fb67-165">Sommige kernels Linux ondersteuning TRIM/UNMAP bewerkingen voor het negeren van niet-gebruikte blokken op de schijf.</span><span class="sxs-lookup"><span data-stu-id="9fb67-165">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="9fb67-166">Dit is vooral handig in standard-opslag om te informeren over Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9fb67-166">This is primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="9fb67-167">Dit bespaart kosten als u grote bestanden maken en deze vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9fb67-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="9fb67-168">Er zijn twee manieren om in te schakelen TRIM ondersteunen in uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="9fb67-168">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="9fb67-169">Raadpleeg uw distributiepunt gebruikelijke voor de aanbevolen aanpak:</span><span class="sxs-lookup"><span data-stu-id="9fb67-169">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="9fb67-170">Gebruik de `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9fb67-170">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="9fb67-171">In sommige gevallen de `discard` optie prestaties gevolgen kan hebben.</span><span class="sxs-lookup"><span data-stu-id="9fb67-171">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="9fb67-172">U kunt ook uitvoeren de `fstrim` opdracht handmatig vanaf de opdrachtregel of toe te voegen aan uw crontab regelmatig wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="9fb67-172">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="9fb67-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="9fb67-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="9fb67-174">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="9fb67-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="9fb67-175">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="9fb67-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="9fb67-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9fb67-176">Next Steps</span></span>
* <span data-ttu-id="9fb67-177">Denk eraan dat de nieuwe schijf is niet beschikbaar voor de virtuele machine als deze opnieuw is opgestart tenzij u deze informatie om te schrijven uw [fstab](http://en.wikipedia.org/wiki/Fstab) bestand.</span><span class="sxs-lookup"><span data-stu-id="9fb67-177">Remember, that your new disk is not available to the VM if it reboots unless you write that information to your [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="9fb67-178">Bekijk uw Linux-VM juist is geconfigureerd, zodat de [optimaliseren van de prestaties van uw Linux-machine](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="9fb67-178">To ensure your Linux VM is configured correctly, review the [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="9fb67-179">Uw opslagcapaciteit uitbreiden door extra schijven toe te voegen en [configureren RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor extra prestaties.</span><span class="sxs-lookup"><span data-stu-id="9fb67-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

