---
title: aaaPrepare een Debian Linux VHD in Azure | Microsoft Docs
description: Meer informatie over hoe toocreate Debian 7 en 8 VHD-bestanden voor de implementatie in Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a>Een Debian VHD voor Azure voorbereiden
## <a name="prerequisites"></a>Vereisten
Deze sectie wordt ervan uitgegaan dat u al een Debian Linux-besturingssysteem hebt geïnstalleerd vanuit een .iso-bestand dat is gedownload van Hallo [Debian website](https://www.debian.org/distrib/) tooa virtuele hardeschijf. Meerdere hulpprogramma's bestaan toocreate VHD-bestanden; Hyper-V is slechts één voorbeeld. Zie voor instructies over het gebruik van Hyper-V [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](https://technet.microsoft.com/library/hh846766.aspx).

## <a name="installation-notes"></a>Opmerkingen bij de installatie
* Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.
* Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure. U kunt converteren Hallo tooVHD schijfindeling met Hyper-V-beheer of Hallo **convert-vhd** cmdlet.
* Bij het installeren van Hallo Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt). Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit moet toobe gekoppeld tooanother VM voor het oplossen van problemen. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.
* Configureer een partitie van de wisseling niet op Hallo OS-schijf. Hello Azure Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf. Meer informatie hierover vindt u in onderstaande Hallo stappen.
* Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.

## <a name="use-azure-manage-toocreate-debian-vhds"></a>Azure beheren toocreate Debian VHD gebruiken
Er zijn extra beschikbaar voor het genereren van Debian VHD's voor Azure, zoals Hallo [azure-beheren](https://github.com/credativ/azure-manage) scripts van [credativ](http://www.credativ.com/). Dit is de aanbevolen aanpak ten opzichte van een installatiekopie van het maken van nieuw Hallo. Bijvoorbeeld, toocreate een Debian 8 VHD uitgevoerd Hallo na opdrachten toodownload azure beheren (en afhankelijkheden) en Hallo azure_build_image script uitvoeren:

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a>Handmatig een Debian VHD voorbereiden
1. Selecteer Hallo virtuele machine in Hyper-V-beheer.
2. Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.
3. Hallo-regel voor commentaar **deb cdrom** in `/etc/apt/source.list` als u Hallo VM op basis van een ISO-bestand instelt.
4. Hallo bewerken `/etc/default/grub` bestand en wijzig Hallo **GRUB_CMDLINE_LINUX** parameter als volgt tooinclude kernel extra parameters voor Azure.
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. Hallo wormgaten bouwen en uitvoeren:
   
        # sudo update-grub
6. Debian van Azure-opslagplaatsen too/etc/apt/sources.list voor Debian 7 of 8 toevoegen:
   
    **Debian 7.x 'Wheezy'**
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    **Debian 8.x 'Jessie'**

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. Hello Azure Linux Agent installeren:
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. Voor Debian 7 is het vereiste toorun Hallo 3,16 gebaseerde kernel uit Hallo wheezy backports opslagplaats. Maak eerst een bestand met de naam van /etc/apt/preferences.d/linux.pref Hello inhoud na:
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    Voer 'apt sudo get-installeren linux-installatiekopie-amd64' tooinstall Hallo nieuwe kernel.
3. Inrichting ervan ongedaan Hallo virtuele machine en deze voorbereiden voor het inrichten op Azure en uitvoeren:
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. Klik op **actie** -afsluiten > omlaag in de Hyper-V-beheer. Uw Linux VHD is nu gereed toobe tooAzure geüpload.

## <a name="next-steps"></a>Volgende stappen
U bent nu klaar toouse uw Debian virtuele harde schijf toocreate nieuwe virtuele machines in Azure. Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

