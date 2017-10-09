---
title: een schijf tooLinux VM met aaaAdd hello Azure CLI | Microsoft Docs
description: Meer informatie over tooadd een permanente schijf tooyour Linux-VM met hello Azure CLI 1.0 en 2.0.
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
ms.openlocfilehash: 0dc5236be62d96b70dd47a7f621f626a037e22aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-disk-tooa-linux-vm"></a>Voeg een schijf tooa Linux VM
Dit artikel laat zien hoe tooattach een permanente schijf tooyour VM zodat u kunt uw gegevens - zelfs als uw virtuele machine is ingericht vanwege toomaintenance vergroten of verkleinen. 

## <a name="quick-commands"></a>Snelle opdrachten
Hallo volgende voorbeeld wordt een `50`GB schijf toohello VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

toouse schijven die worden beheerd:

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

toouse zonder begeleiding schijven:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>Een beheerde schijf koppelen

Beheerde schijven kunt u toofocus op uw virtuele machines en hun schijven zonder dat u Azure Storage-accounts. U kunt snel maken en koppelen van een beheerde schijf tooa virtuele machine met behulp van dezelfde Azure-resourcegroep Hallo of u kunt een willekeurig aantal schijven maken en deze vervolgens te koppelen.


### <a name="attach-a-new-disk-tooa-vm"></a>Een nieuwe schijf tooa VM koppelen

Als u alleen een nieuwe schijf nodig op de virtuele machine, kunt u Hallo `az vm disk attach` opdracht.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>Een bestaande schijf koppelen 

In veel gevallen koppelt u de schijven die al zijn gemaakt. U eerst vinden Hallo schijf-id en vervolgens doorgeven dat toohello `az vm disk attach` opdracht. Hallo volgende voorbeeld wordt een schijf die is gemaakt met `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

Hallo uitvoer ziet er ongeveer zo Hallo volgende (kunt u Hallo `-o table` tooany tooformat Hallo opdrachtuitvoer in optie):

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

Een nieuwe schijf koppelen is snel als u niet erg vindt voor het maken van een schijf in Hallo hetzelfde opslagaccount als uw virtuele machine. Type `azure vm disk attach-new` toocreate en koppelt u een nieuwe schijf GB voor de virtuele machine. Als u een opslagaccount niet expliciet identificeren, de schijf die u maakt in geplaatst Hallo dezelfde opslagaccount waarin de OS-schijf zich bevindt. Hallo volgende voorbeeld wordt een `50`GB schijf toohello VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a>Verbinding maken met toohello Linux VM toomount Hallo nieuwe schijf
> [!NOTE]
> In dit onderwerp tooa VM verbinding maakt met behulp van gebruikersnamen en wachtwoorden. toouse paren van openbare en persoonlijke sleutels toocommunicate met uw virtuele machine, Zie [hoe tooUse SSH met Linux op Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
> 
> 

U moet tooSSH in uw Azure VM-toopartition opmaken en de nieuwe schijf koppelen zodat uw Linux-VM kan worden gebruikt. Als u niet bekend bent met verbinding te maken met **ssh**, Hallo-opdracht heeft Hallo vorm `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`, en lijkt op Hallo volgende:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

Uitvoer

```bash
hello authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) toohello list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome tooUbuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

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

hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

ops@myVM:~$
```

Nu dat u bent verbonden tooyour VM, kunt u nu tooattach een schijf.  Zoek eerst Hallo schijf, met `dmesg | grep SCSI` (Hallo methode gebruik toodiscover de nieuwe schijf kan verschillen). In dit geval wordt er ongeveer als volgt uitziet:

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

en in geval van dit onderwerp Hallo Hallo `sdc` schijf is Hallo die we willen. Nu partitie Hallo schijf met `sudo fdisk /dev/sdc` --ervan uitgaande dat in uw aanvraag Hallo schijf is `sdc`, en u een primaire schijf op partitie 1 maken en accepteren Hallo andere standaardinstellingen.

```bash
sudo fdisk /dev/sdc
```

Uitvoer

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide toowrite them.
After that, of course, hello previous content won't be recoverable.

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

Hallo partitie maken door te typen `p` Hallo een opdrachtprompt:

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
hello partition table has been altered!

Calling ioctl() toore-read partition table.
Syncing disks.
```

En een partitie bestandssysteem toohello schrijven met Hallo **mkfs** opdracht geven bestandssysteem Hallo type en de naam van het apparaat. In dit onderwerp we maken gebruik van `ext4` en `/dev/sdc1` van boven:

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
65523 blocks (5.00%) reserved for hello super user
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

Nu we een directory toomount Hallo bestandssysteem via maken `mkdir`:

```bash
sudo mkdir /datadrive
```

En koppelt u de directory met behulp van Hallo `mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

Hallo gegevensschijf is nu gereed toouse als `/datadrive`.

```bash
ls
```

Uitvoer

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

tooensure hello station wordt automatisch opnieuw gekoppeld nadat deze moet opnieuw worden opgestart toohello /etc/fstab bestand toegevoegd. Bovendien is het raadzaam die Hallo UUID (Universally Unique IDentifier) wordt gebruikt in/etc/fstab toorefer toohello station in plaats van alleen Hallo apparaatnaam (zoals `/dev/sdc1`). Als een schijffout Hallo OS tijdens het opstarten detecteert, met behulp van Hallo UUID Hallo foutieve schijfconfiguratie gekoppelde tooa opgegeven locatie wordt voorkomt. Resterende gegevensschijven zou worden toegewezen die dezelfde apparaat-id. toofind Hallo UUID van het nieuwe station hello, gebruikt u Hallo **blkid** hulpprogramma:

```bash
sudo -i blkid
```

Hallo-uitvoer ziet er vergelijkbare toohello volgende:

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> Onjuist bewerken van Hallo **/etc/fstab** bestand kan leiden tot een systeem opgestart. Als u niet zeker, Raadpleeg toohello distributie van documentatie voor informatie over hoe tooproperly dit bestand bewerken. Het is ook raadzaam dat een back-up van Hallo /etc/fstab bestand is gemaakt voordat u bewerkt.
> 
> 

Open vervolgens Hallo **/etc/fstab** bestand in een teksteditor:

```bash
sudo vi /etc/fstab
```

In dit voorbeeld gebruiken we Hallo UUID-waarde voor Hallo nieuwe **/dev/sdc1** apparaat dat is gemaakt in de vorige stappen Hallo en Hallo koppelpunt **/datadrive**. Voeg na einde van regel toohello Hallo Hallo **/etc/fstab** bestand:

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> Later kan een gegevensschijf zonder te bewerken fstab verwijdert Hallo VM toofail tooboot. De meeste distributies bieden beide Hallo `nofail` en/of `nobootwait` fstab-opties. Deze opties kunnen een tooboot systeem, zelfs als de schijf Hallo toomount tijdens het opstarten mislukt. Raadpleeg de distributie-documentatie voor meer informatie over deze parameters.
> 
> Hallo **nofail** optie zorgt ervoor dat Hallo VM start, zelfs als Hallo bestandssysteem beschadigd is of Hallo schijf tijdens het opstarten niet bestaat. Zonder deze optie kunnen optreden gedrag zoals beschreven in [niet kan SSH tooLinux VM vanwege tooFSTAB fouten](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>TRIM/UNMAP ondersteuning voor Linux in Azure
Sommige kernels Linux ondersteunen TRIM/UNMAP operations toodiscard niet-gebruikte blokken op Hallo schijf. Dit is vooral handig in standard-opslag tooinform Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd. Dit bespaart kosten als u grote bestanden maken en deze vervolgens te verwijderen.

Er zijn twee manieren tooenable TRIM ondersteunen in uw Linux-VM. Raadpleeg uw distributiepunt gebruikelijke voor Hallo aanbevolen benadering:

* Gebruik Hallo `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* In sommige gevallen Hallo `discard` optie prestaties gevolgen kan hebben. U kunt ook uitvoeren Hallo `fstrim` opdracht handmatig vanaf de opdrachtregel Hallo of voeg tooyour crontab toorun regelmatig:
  
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
* Denk eraan dat dat de nieuwe schijf is niet beschikbaar toohello VM als opnieuw wordt opgestart tenzij u die informatie tooyour schrijven [fstab](http://en.wikipedia.org/wiki/Fstab) bestand.
* tooensure uw Linux-VM is onjuist geconfigureerd; revisie Hallo [optimaliseren van de prestaties van uw Linux-machine](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) aanbevelingen.
* Uw opslagcapaciteit uitbreiden door extra schijven toe te voegen en [configureren RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor extra prestaties.

