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
# <a name="configure-software-raid-on-linux"></a>Software-RAID configureren onder Linux
Het is een algemene scenario toouse software RAID op Linux virtuele machines in Azure toopresent bijgesloten gegevens meerdere als een enkel RAID-apparaat schijven. Dit kan doorgaans worden gebruikte tooimprove prestaties en toestaan voor verbeterde doorvoer vergeleken toousing één schijf.

## <a name="attaching-data-disks"></a>Gegevensschijven koppelen
Twee of meer leeg gegevensschijven zijn benodigde tooconfigure een RAID-apparaat.  Hallo primaire reden voor het maken van een RAID-apparaat is tooimprove prestaties van de schijf-i/o.  Op basis van uw i/o-behoeften, kunt u tooattach schijven die zijn opgeslagen in de Standard-opslag met up too500 i/o/ps per schijf of onze Premium-opslag met up too5000 i/o/ps per schijf. In dit artikel gaat niet informatie over het tooprovision en koppelt u gegevens schijven tooa virtuele Linux-machine.  Zie de Microsoft Azure-artikel Hallo [een schijf koppelen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor gedetailleerde instructies over hoe tooattach gegevens in een lege schijf tooa virtuele Linux-machine in Azure.

## <a name="install-hello-mdadm-utility"></a>Hallo mdadm hulpprogramma installeren
* **Ubuntu**
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* **CentOS & Oracle Linux**
```bash
sudo yum install mdadm
```

* **SLES en openSUSE**
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a>Hallo partities op schijf maken
In dit voorbeeld maken we een enkele schijfpartitie op /dev/sdc. nieuwe schijfpartitie Hallo wordt /dev/sdc1 aangeroepen.

1. Start `fdisk` toobegin partities maken

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

2. Tik op "n" op Hallo vragen toocreate een  **n** euwe partitie:

    ```bash
    Command (m for help): n
    ```

3. Druk op 'p' toocreate een **p**rimaire partitie:

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. Druk op '1' tooselect partitienummer 1:

    ```bash
    Partition number (1-4): 1
    ```

5. Selecteer het beginpunt van een nieuwe partitie Hallo of druk op Hallo `<enter>` tooaccept hello tooplace Hallo standaardpartitie aan begin Hallo Hallo vrije ruimte op station Hallo:

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. Selecteer Hallo grootte van Hallo partitie, bijvoorbeeld '+10G' type toocreate een 10 GB-partitie. Of druk op `<enter>` maken van een enkele partitie die de hele station Hallo omvat:

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. Hallo-ID vervolgens wijzigen en **t**ype Hallo partitie van Hallo standaard-ID '83' (Linux) tooID 'fd' (Linux raid automatisch):

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. Ten slotte Schrijf Hallo partitie tabel toohello station en fdisk sluiten:

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a>Hallo RAID-matrix maken
1. Hallo volgende voorbeeld wordt 'stripe' (RAID-niveau 0) drie partities zich op drie aparte gegevensschijven (sdc1, sdd1, sde1).  Nadat u deze opdracht uitvoert op een nieuw RAID-apparaat aangeroepen **/dev/md127** wordt gemaakt. Let ook op dat als deze gegevens schijven we eerder onderdeel van een andere uitgeschakelde RAID-matrix mogelijk nodig tooadd hello `--force` parameter toohello `mdadm` opdracht:

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. Hallo-bestandssysteem op Hallo nieuwe RAID-apparaat maken
   
    a. **CentOS, Oracle Linux SLES 12, openSUSE en Ubuntu**

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    b. **SLES 11**

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    c. **SLES 11** - boot.md inschakelen en mdadm.conf maken

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > Opnieuw opstarten nadat u deze wijzigingen aanbrengt op SUSE systemen mogelijk vereist zijn. Deze stap is *niet* vereist voor SLES 12.
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a>Hallo nieuwe file system te/etc/fstab toevoegen
> [!IMPORTANT]
> Hallo /etc/fstab bestand onjuist bewerkt, kan dit leiden tot een systeem opgestart. Als u niet zeker, Raadpleeg toohello distributie van documentatie voor informatie over hoe tooproperly dit bestand bewerken. Het is ook raadzaam dat een back-up van Hallo /etc/fstab bestand is gemaakt voordat u bewerkt.

1. Maak Hallo gewenst koppelpunt voor het nieuwe bestandssysteem, bijvoorbeeld:

    ```bash
    sudo mkdir /data
    ```
2. Bij het bewerken van /etc/fstab Hallo **UUID** moet gebruikte tooreference Hallo file system in plaats van Hallo apparaatnaam.  Gebruik Hallo `blkid` hulpprogramma toodetermine Hallo UUID voor het nieuwe bestandssysteem Hallo:

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. Open /etc/fstab in een teksteditor en voeg een vermelding voor het nieuwe bestandssysteem hello, bijvoorbeeld:

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    Of op **SLES 11**:

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    Vervolgens opslaan en sluiten /etc/fstab.

4. Testen die Hallo/etc/fstab-invoer correct is:

    ```bash  
    sudo mount -a
    ```

    Als deze opdracht in een foutbericht weergegeven resulteert, controleert u Hallo syntaxis in Hallo /etc/fstab bestand.
   
    Voer vervolgens Hallo `mount` opdracht tooensure Hallo-bestandssysteem is gekoppeld:

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. (Optioneel) Opstartparameters failsafe
   
    **fstab-configuratie**
   
    Groot aantal distributies zijn beide Hallo `nobootwait` of `nofail` parameters die kunnen worden toegevoegd als toohello bestand/etc/fstab koppelen. Deze parameters toestaan voor fouten bij het koppelen van een bepaald bestandssysteem en Hallo Linux system toocontinue tooboot toestaan, zelfs als deze tooproperly koppelpunt Hallo RAID-bestandssysteem. Raadpleeg tooyour distributie van documentatie voor meer informatie over deze parameters.
   
    Voorbeeld (Ubuntu):

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    **Linux-opstartparameters**
   
    Hallo in toevoeging toohello hierboven parameters, kernel-parameter '`bootdegraded=true`' hello system tooboot kunt toestaan, zelfs als Hallo RAID wordt beschouwd als beschadigd of gedegradeerd, bijvoorbeeld als een gegevensstation per ongeluk is verwijderd van Hallo virtuele machine. Standaard kan dit ook leiden tot een niet-opstartbare systeem.
   
    Raadpleeg de documentatie op hoe de kernel-parameters voor het bewerken van tooproperly tooyour distributie van. Bijvoorbeeld in een groot aantal distributies (CentOS, Oracle Linux, SLES 11) deze parameters kunnen handmatig worden toegevoegd toohello '`/boot/grub/menu.lst`' bestand.  Op Ubuntu deze parameter kan worden toegevoegd toohello `GRUB_CMDLINE_LINUX_DEFAULT` variabele op '/ etc/standaard/grub'.


## <a name="trimunmap-support"></a>TRIM/UNMAP-ondersteuning
Sommige kernels Linux ondersteunen TRIM/UNMAP operations toodiscard niet-gebruikte blokken op Hallo schijf. Deze bewerkingen zijn voornamelijk nuttig in standard-opslag tooinform Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd. 'S te verwijderen kunt kosten besparen, als u grote bestanden maken en deze vervolgens te verwijderen.

> [!NOTE]
> RAID kan geen verwijderde opdrachten uitgeven als Hallo chunkgrootte voor de matrix Hallo tooless dan Hallo-standaard (512KB) is ingesteld. Dit komt doordat Hallo ontkoppelen granulatie op Hallo Host is ook 512KB. Als u de chunkgrootte van Hallo matrix via mdadm van gewijzigd `--chunk=` parameter en klik vervolgens TRIM/ontkoppelen aanvragen kunnen worden genegeerd door de kernel Hallo.

Er zijn twee manieren tooenable TRIM ondersteunen in uw Linux-VM. Raadpleeg uw distributiepunt gebruikelijke voor Hallo aanbevolen benadering:

- Gebruik Hallo `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- In sommige gevallen Hallo `discard` optie prestaties gevolgen kan hebben. U kunt ook uitvoeren Hallo `fstrim` opdracht handmatig vanaf de opdrachtregel Hallo of voeg tooyour crontab toorun regelmatig:

    **Ubuntu**

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    **RHEL/CentOS**
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
