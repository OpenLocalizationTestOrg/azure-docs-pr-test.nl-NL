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
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a>LVM configureren op een virtuele Linux-machine in Azure
Dit document wordt besproken hoe tooconfigure logische Volume Manager (LVM) in uw virtuele machine van Azure. Wanneer deze is mogelijk tooconfigure LVM op elke schijf die is gekoppeld toohello virtuele machine, standaard de meeste cloud installatiekopieën geen LVM geconfigureerd op Hallo besturingssysteemschijf. Dit is tooprevent problemen met dubbele volume groepen als besturingssysteemschijf ooit is Hallo gekoppeld tooanother VM Hallo dezelfde distributie en het type, dat wil zeggen tijdens een scenario voor herstel. Daarom is het raadzaam alleen toouse LVM op Hallo gegevensschijven.

## <a name="linear-vs-striped-logical-volumes"></a>Lineaire versus striped logische volumes
LVM mag gebruikte toocombine een aantal fysieke schijven in één opslagvolume. Standaard wordt LVM meestal gemaakt lineaire logische volumes, wat betekent dat fysieke opslag Hallo samengevoegd. In dit geval worden lees-/ schrijfbewerkingen doorgaans alleen verzonden tooa één schijf. We kunnen daarentegen ook striped logische volumes waarop lees- en schrijfbewerkingen gedistribueerde toomultiple schijven die zijn opgenomen in de groep van Hallo-volume (dat wil zeggen vergelijkbare tooRAID0 zijn) maken. Voor betere prestaties is het waarschijnlijk zult u toostripe uw logische volumes zodat lees- en schrijfbewerkingen gebruikmaken van alle schijven in de bijgesloten gegevens.

Dit document wordt beschreven hoe toocombine gegevens van verschillende schijven in een groep één volume en maak vervolgens logische striped volumes. Hallo onderstaande stappen zijn enigszins gegeneraliseerde toowork met de meeste distributies. In de meeste gevallen Hallo hulpprogramma's en werkstromen voor het beheren van LVM in Azure zijn niet fundamenteel anders dan andere omgevingen. Gebruikelijke ook Raadpleeg de leverancier van uw Linux voor documentatie en aanbevolen procedures voor het gebruik van LVM met uw bepaalde distributiepunt.

## <a name="attaching-data-disks"></a>Gegevensschijven koppelen
Een zult meestal toostart met twee of meer gegevensschijven zijn leeg bij gebruik van LVM. Op basis van uw i/o-behoeften, kunt u tooattach schijven die zijn opgeslagen in de Standard-opslag met up too500 i/o/ps per schijf of onze Premium-opslag met up too5000 i/o/ps per schijf. In dit artikel wordt niet ingegaan op de details over het tooprovision en koppelt u gegevens schijven tooa virtuele Linux-machine. Zie de Microsoft Azure-artikel Hallo [een schijf koppelen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor gedetailleerde instructies over hoe tooattach gegevens in een lege schijf tooa virtuele Linux-machine in Azure.

## <a name="install-hello-lvm-utilities"></a>Hallo LVM hulpprogramma's installeren
* **Ubuntu**

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* **RHEL, CentOS & Oracle Linux**

    ```bash   
    sudo yum install lvm2
    ```

* **SLES 12 en openSUSE**

    ```bash   
    sudo zypper install lvm2
    ```

* **SLES 11**

    ```bash   
    sudo zypper install lvm2
    ```

    Op SLES11 moet u ook bewerken `/etc/sysconfig/lvm` en stel `LVM_ACTIVATED_ON_DISCOVERED` te 'inschakelen':

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a>LVM configureren
In deze handleiding wordt ervan uitgegaan hebt u drie gegevensschijven die we verwijzen gekoppeld tooas `/dev/sdc`, `/dev/sdd` en `/dev/sde`. Opmerking deze niet kunnen worden altijd Hallo dezelfde padnamen in uw virtuele machine. U kunt uitvoeren '`sudo fdisk -l`' of een vergelijkbare opdracht toolist uw beschikbare schijven.

1. Hallo fysieke volumes voorbereiden:

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. Een volume-groep maken. In dit voorbeeld we Hallo volume groep bellen `data-vg01`:

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. Hallo logische of meer volumes maken. Hallo we onderstaande opdracht maakt u één logische volume aangeroepen `data-lv01` toospan Hallo hele volume groeperen, maar het is ook mogelijk toocreate Opmerking meerdere logische volumes in Hallo volume groep.

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. Logische Hallo-volume formatteren

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > Bij gebruik van SLES11 `-t ext3` in plaats van ext4. SLES11 ondersteunt alleen-lezentoegang tooext4 bestandssystemen.

## <a name="add-hello-new-file-system-tooetcfstab"></a>Hallo nieuwe file system te/etc/fstab toevoegen
> [!IMPORTANT]
> Onjuist bewerken van Hallo `/etc/fstab` bestand kan leiden tot een systeem opgestart. Als u niet zeker, Zie toohello distributie van documentatie voor informatie over hoe tooproperly dit bestand bewerken. Het is ook aanbevolen een back-up van Hallo `/etc/fstab` bestand is gemaakt voordat u kunt bewerken.

1. Maak Hallo gewenst koppelpunt voor het nieuwe bestandssysteem, bijvoorbeeld:

    ```bash  
    sudo mkdir /data
    ```

2. Hallo logisch Volumepad vinden

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. Open `/etc/fstab` in een teksteditor en voeg een vermelding voor het nieuwe bestandssysteem hello, bijvoorbeeld:

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    Vervolgens opslaan en sluiten `/etc/fstab`.

4. Testen die Hallo `/etc/fstab` invoer correct is:

    ```bash    
    sudo mount -a
    ```

    Als u deze opdracht resulteert in een foutbericht Controleer Hallo syntaxis in Hallo `/etc/fstab` bestand.
   
    Voer vervolgens Hallo `mount` opdracht tooensure Hallo-bestandssysteem is gekoppeld:

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. (Optioneel) Opstartparameters failsafe in`/etc/fstab`
   
    Groot aantal distributies zijn beide Hallo `nobootwait` of `nofail` koppelen van de parameters die kunnen worden toegevoegd als toohello `/etc/fstab` bestand. Deze parameters toestaan voor fouten bij het koppelen van een bepaald bestandssysteem en Hallo Linux system toocontinue tooboot toestaan, zelfs als deze tooproperly koppelpunt Hallo RAID-bestandssysteem. Raadpleeg tooyour distributie van documentatie voor meer informatie over deze parameters.
   
    Voorbeeld (Ubuntu):

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a>TRIM/UNMAP-ondersteuning
Sommige kernels Linux ondersteunen TRIM/UNMAP operations toodiscard niet-gebruikte blokken op Hallo schijf. Deze bewerkingen zijn voornamelijk nuttig in standard-opslag tooinform Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd. 'S te verwijderen kunt kosten besparen, als u grote bestanden maken en deze vervolgens te verwijderen.

Er zijn twee manieren tooenable TRIM ondersteunen in uw Linux-VM. Raadpleeg uw distributiepunt gebruikelijke voor Hallo aanbevolen benadering:

- Gebruik Hallo `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- In sommige gevallen Hallo `discard` optie prestaties gevolgen kan hebben. U kunt ook uitvoeren Hallo `fstrim` opdracht handmatig vanaf de opdrachtregel Hallo of voeg tooyour crontab toorun regelmatig:

    **Ubuntu**

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    **RHEL/CentOS**

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
