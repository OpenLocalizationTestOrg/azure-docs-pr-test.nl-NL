---
title: aaaCreate een Ubuntu Linux-VHD en uploaden in Azure
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) die een Ubuntu Linux-besturingssysteem bevat.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>Een virtuele Ubuntu-machine voor Azure voorbereiden
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>Officiële Ubuntu cloud installatiekopieën
Ubuntu publiceert nu officiële Azure VHD's worden gedownload op [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/). Als u uw eigen gespecialiseerde Ubuntu-installatiekopie van toobuild nodig voor Azure, plaats gebruik Hallo handmatige procedure eronder wordt aanbevolen toostart met deze bekende werkt VHD's en indien nodig aanpassen. Hallo laatste installatiekopie releases kunnen altijd worden gevonden op Hallo volgende locaties:

* Ubuntu 12.04/nauwkeurig: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/betrouwbare: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u al een Ubuntu Linux-besturingssysteem tooa virtuele harde schijf hebt geïnstalleerd. Meerdere hulpprogramma's bestaan toocreate VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V. Zie voor instructies [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).

**Opmerkingen bij de installatie Ubuntu**

* Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.
* Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.  U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of Hallo cmdlet convert-vhd.
* Bij het installeren van Hallo Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt). Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit moet toobe gekoppeld tooanother VM voor het oplossen van problemen. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.
* Configureer een partitie van de wisseling niet op Hallo OS-schijf. Hallo Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.  Meer informatie hierover vindt u in onderstaande Hallo stappen.
* Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.

## <a name="manual-steps"></a>Handmatige stappen
> [!NOTE]
> Voordat u probeert toocreate uw eigen aangepaste installatiekopie Ubuntu voor Azure, overweeg Hallo met vooraf gemaakte en installatiekopieën van getest [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) in plaats daarvan.
> 
> 

1. Selecteer Hallo virtuele machine in Hallo middelste deelvenster van de Hyper-V-beheer.

2. Klik op **Connect** tooopen Hallo venster voor Hallo virtuele machine.

3. Huidige Hallo-opslagplaatsen in Hallo installatiekopie toouse Ubuntu van Azure repo's vervangen. Hallo stappen verschillen, afhankelijk van Hallo Ubuntu-versie.
   
    Voordat u bewerkt `/etc/apt/sources.list`, het is aanbevolen toomake een back-up:
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. Hallo Ubuntu Azure installatiekopieën volgt nu Hallo *hardware stuk* kernel (HWE). Hallo besturingssysteem toohello nieuwste kernel bijwerken door het uitvoeren van de volgende opdrachten Hallo:

    Ubuntu 12.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **Zie ook:**
    - [https://Wiki.Ubuntu.com/kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://Wiki.Ubuntu.com/kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. Hallo kernel opstarten regel voor wormgaten tooinclude kernel extra parameters voor Azure wijzigen. dit open toodo `/etc/default/grub` vinden in een teksteditor Hallo variabele met de naam `GRUB_CMDLINE_LINUX_DEFAULT` (of toe te voegen indien nodig) en bewerk het tooinclude Hallo volgende parameters:
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    Opslaan en sluiten van dit bestand en voer `sudo update-grub`. Dit zorgt ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure technische ondersteuning helpen kan bij het opsporen van problemen worden verzonden.

6. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.  Dit is meestal Hallo standaard.

7. Hello Azure Linux Agent installeren:
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    Hallo `walinuxagent` pakket kan verwijderen Hallo `NetworkManager` en `NetworkManager-gnome` pakketten als ze zijn geïnstalleerd.

8. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer. Uw Linux VHD is nu gereed toobe tooAzure geüpload.

## <a name="next-steps"></a>Volgende stappen
U bent nu klaar toouse uw Ubuntu Linux virtuele harde schijf toocreate nieuwe virtuele machines in Azure. Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="references"></a>Verwijzingen
Ubuntu hardware inschakelen (HWE) kernel:

* [http://blog.utlemming.org/2015/01/Ubuntu-1404-Azure-images-Now-Tracking.HTML](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-Azure-cloud-images-Now-Using-Hwe.HTML](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

