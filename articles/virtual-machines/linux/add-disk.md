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
# <a name="add-a-disk-to-a-linux-vm"></a>Een schijf toevoegen aan een virtuele Linux-machine
In dit artikel laat zien hoe een permanente schijf koppelen met uw virtuele machine zodat u kunt uw gegevens - zelfs als uw virtuele machine is ingericht vanwege onderhoud vergroten of verkleinen. 

## <a name="quick-commands"></a>Snelle opdrachten
Het volgende voorbeeld wordt een `50`GB schijf naar de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`:

Beheerde schijven gebruiken:

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

Niet-beheerde schijven gebruiken:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>Een beheerde schijf koppelen

Beheerde schijven kunt u zich kunt richten op uw virtuele machines en hun schijven zonder dat u Azure Storage-accounts. Kunt u snel maken en een beheerde schijf koppelen aan een virtuele machine met behulp van de dezelfde Azure-resourcegroep, of u kunt een willekeurig aantal schijven maken en deze vervolgens te koppelen.


### <a name="attach-a-new-disk-to-a-vm"></a>Een nieuwe schijf koppelen aan een virtuele machine

Als u alleen een nieuwe schijf nodig op de virtuele machine, kunt u de `az vm disk attach` opdracht.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>Een bestaande schijf koppelen 

In veel gevallen koppelt u de schijven die al zijn gemaakt. U eerst de schijf-id vinden en geeft die aan de `az vm disk attach` opdracht. Het volgende voorbeeld wordt een schijf die is gemaakt met `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.

```azurecli
# find the disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

De uitvoer ziet er ongeveer als volgt (u kunt de `-o table` optie als u wilt willekeurige opdracht van de uitvoer in opmaken):

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


## <a name="attach-an-unmanaged-disk"></a>Een niet-beheerde schijf koppelen

Een nieuwe schijf koppelen is snelle als u niet erg vindt voor het maken van een schijf in hetzelfde opslagaccount als uw virtuele machine. Type `azure vm disk attach-new` maken en koppelen van een nieuwe schijf GB voor de virtuele machine. Als u een opslagaccount niet expliciet identificeren, wordt de schijf die u maakt geplaatst in hetzelfde opslagaccount waarin de OS-schijf zich bevindt. Het volgende voorbeeld wordt een `50`GB schijf naar de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-to-the-linux-vm-to-mount-the-new-disk"></a>Verbinding maken met de Linux-VM naar de nieuwe schijf koppelen
> [!NOTE]
> In dit onderwerp maakt verbinding met een virtuele machine met behulp van gebruikersnamen en wachtwoorden. Zie voor het gebruik van paren van openbare en persoonlijke sleutels om te communiceren met uw virtuele machine, [het gebruik van SSH met Linux op Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
> 
> 

U moet SSH in uw Azure-virtuele machine aan partitie formatteren en de nieuwe schijf koppelen zodat uw Linux-VM kan worden gebruikt. Als u niet bekend bent met verbinding te maken met **ssh**, de opdracht heeft de vorm `ssh <username>@<FQDNofAzureVM> -p <the ssh port>`, en ziet er ongeveer als volgt:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

Uitvoer

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

Nu dat u met uw virtuele machine verbonden bent, kunt u kunt een schijf koppelen.  Zoek eerst de schijf met behulp van `dmesg | grep SCSI` (de methode die u gebruikt voor het detecteren van de nieuwe schijf kan variëren). In dit geval wordt er ongeveer als volgt uitziet:

```bash
dmesg | grep SCSI
```

Uitvoer

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

en in het geval van dit onderwerp, de `sdc` schijf is die we willen. De schijf met nu partitioneren `sudo fdisk /dev/sdc` --ervan uitgaande dat in uw geval de schijf is `sdc`, en u een primaire schijf op partitie 1 maken en de andere standaardinstellingen accepteren.

```bash
sudo fdisk /dev/sdc
```

Uitvoer

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

De partitie maken door te typen `p` bij de opdrachtprompt:

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

En een bestandssysteem schrijven naar de partitie met behulp van de **mkfs** opdracht opgeven van het type van uw bestandssysteem en de naam van het apparaat. In dit onderwerp we maken gebruik van `ext4` en `/dev/sdc1` van boven:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Uitvoer

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

Nu we een directory maken te koppelen van het bestandssysteem via `mkdir`:

```bash
sudo mkdir /datadrive
```

En koppelt u het gebruik van de directory `mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

De gegevensschijf is nu gereed voor gebruik als `/datadrive`.

```bash
ls
```

Uitvoer

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

Om te controleren of dat de schijf automatisch opnieuw wordt gekoppeld na opnieuw opstarten moet deze worden toegevoegd aan het bestand/etc/fstab-fouten. Bovendien is het raadzaam dat de UUID (Universally Unique IDentifier) wordt gebruikt in/etc/fstab om te verwijzen naar het station in plaats van alleen de naam van het apparaat (zoals `/dev/sdc1`). Als het besturingssysteem een schijffout tijdens het opstarten detecteert, voorkomt met behulp van de UUID de onjuiste schijf wordt gekoppeld aan een bepaalde locatie. Resterende gegevensschijven zou worden toegewezen die dezelfde apparaat-id. Als de UUID van het nieuwe station zoekt, volgt u de **blkid** hulpprogramma:

```bash
sudo -i blkid
```

De uitvoer ziet er ongeveer als volgt uit:

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> Onjuist bewerken van de **/etc/fstab** bestand kan leiden tot een systeem opgestart. Als u niet zeker, Raadpleeg de distributie-documentatie voor informatie over het correct dit bestand te bewerken. Het is ook raadzaam dat een back-up van het bestand /etc/fstab is gemaakt voordat u bewerkt.
> 
> 

Open vervolgens de **/etc/fstab** bestand in een teksteditor:

```bash
sudo vi /etc/fstab
```

In dit voorbeeld gebruiken we de UUID-waarde voor de nieuwe **/dev/sdc1** apparaat dat is gemaakt in de vorige stappen en het koppelpunt **/datadrive**. Voeg de volgende regel toe aan het einde van de **/etc/fstab** bestand:

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> Later een gegevensschijf verwijderen zonder te bewerken fstab kan ervoor zorgen dat de virtuele machine niet kunnen worden opgestart. De meeste distributies Geef ofwel de `nofail` en/of `nobootwait` fstab-opties. Deze opties kunt een systeem op te starten, zelfs als de schijf niet koppelen tijdens het opstarten. Raadpleeg de distributie-documentatie voor meer informatie over deze parameters.
> 
> De **nofail** optie zorgt ervoor dat de VM start zelfs als het bestandssysteem beschadigd is of de schijf tijdens het opstarten niet bestaat. Zonder deze optie kunnen optreden gedrag zoals beschreven in [niet kan SSH voor Linux VM vanwege FSTAB-fouten](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>TRIM/UNMAP ondersteuning voor Linux in Azure
Sommige kernels Linux ondersteuning TRIM/UNMAP bewerkingen voor het negeren van niet-gebruikte blokken op de schijf. Dit is vooral handig in standard-opslag om te informeren over Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd. Dit bespaart kosten als u grote bestanden maken en deze vervolgens te verwijderen.

Er zijn twee manieren om in te schakelen TRIM ondersteunen in uw Linux-VM. Raadpleeg uw distributiepunt gebruikelijke voor de aanbevolen aanpak:

* Gebruik de `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* In sommige gevallen de `discard` optie prestaties gevolgen kan hebben. U kunt ook uitvoeren de `fstrim` opdracht handmatig vanaf de opdrachtregel of toe te voegen aan uw crontab regelmatig wordt uitgevoerd:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Problemen oplossen
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Volgende stappen
* Denk eraan dat de nieuwe schijf is niet beschikbaar voor de virtuele machine als deze opnieuw is opgestart tenzij u deze informatie om te schrijven uw [fstab](http://en.wikipedia.org/wiki/Fstab) bestand.
* Bekijk uw Linux-VM juist is geconfigureerd, zodat de [optimaliseren van de prestaties van uw Linux-machine](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) aanbevelingen.
* Uw opslagcapaciteit uitbreiden door extra schijven toe te voegen en [configureren RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor extra prestaties.

