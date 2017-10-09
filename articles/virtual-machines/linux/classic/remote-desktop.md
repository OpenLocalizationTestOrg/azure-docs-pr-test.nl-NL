---
title: aaaRemote bureaublad tooa Linux VM | Microsoft Docs
description: Meer informatie over hoe tooinstall en extern bureaublad tooconnect tooa Microsoft Azure Linux VM voor Hallo klassieke implementatiemodel configureren
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>Met behulp van extern bureaublad tooconnect tooa Microsoft Azure Linux VM
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Voor Hallo Resource Manager-versie van dit artikel bijgewerkt, Zie [hier](../use-remote-desktop.md).

## <a name="overview"></a>Overzicht
RDP (Remote Desktop Protocol) is een oorspronkelijk protocol gebruikt voor Windows. Hoe kunnen we RDP tooconnect tooa Linux VM (virtuele machine) op afstand gebruiken?

In deze richtlijnen krijgt u antwoord Hallo! Deze methode kunt u tooinstall en config xrdp op uw Microsoft Azure Linux VM, waarmee u tooit verbinding met extern bureaublad van een Windows-machine. Linux-VM met Ubuntu of OpenSUSE als voorbeeld in deze richtlijnen Hallo zullen worden gebruikt.

Hallo xrdp hulpprogramma is een open source RDP-server waarmee u tooconnect uw Linux-server met extern bureaublad van een Windows-machine. RDP heeft betere prestaties dan VNC (virtuele netwerk computers). VNC renders met JPEG-kwaliteit afbeeldingen en kan traag zijn, terwijl RDP snel en crystal wissen is.

> [!NOTE]
> U moet al een Microsoft Azure-virtuele machine met Linux hebben. Zie toocreate en instellen van een Linux-VM Hallo [Azure Linux VM-zelfstudie](createportal.md).
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>Een eindpunt voor extern bureaublad maken
We gebruiken het standaardeindpunt Hallo 3389 voor extern bureaublad in dit document. Instellen van 3389 eindpunt als `Remote Desktop` tooyour Linux VM, zoals hieronder:

![Afbeelding](./media/remote-desktop/endpoint-for-linux-server.png)

Als u niet weet hoe tooset u een eindpunt voor de virtuele machine, Zie [in deze richtlijnen](setup-endpoints.md).

## <a name="install-gnome-desktop"></a>Gnome bureaublad installeren
Verbinding maken met tooyour Linux VM via `putty`, en installeer `Gnome Desktop`.

Ubuntu, gebruikt u in:

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


Voor OpenSUSE, gebruiken:

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>Xrdp installeren
Ubuntu, gebruikt u in:

    #sudo apt-get install xrdp

Voor OpenSUSE, gebruiken:

> [!NOTE]
> Hallo OpenSUSE versie met Hallo-versie die u gebruikt in de volgende opdracht Hallo bijwerken. Hallo in het volgende voorbeeld is voor `OpenSUSE 13.2`.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>Start xrdp en xdrp service ingesteld op opstartprocedure
Voor OpenSUSE, gebruiken:

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

Voor Ubuntu, xrdp wordt gestart en eanbled op boot-up automatisch na de installatie.

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>Met behulp van xfce als u een virtuele Ubuntu-versie hoger is dan Ubuntu 12.04LTS
Omdat de huidige versie Hallo van xrdp niet Gnome bureaublad voor Ubuntu-versies hoger is dan Ubuntu 12.04LTS ondersteunt, gebruiken we `xfce` bureaublad in plaats daarvan.

tooinstall `xfce`, gebruikt u deze opdracht:

    #sudo apt-get install xubuntu-desktop

Schakel vervolgens `xfce` met de volgende opdracht:

    #echo xfce4-session >~/.xsession

Hallo-configuratiebestand bewerken `/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

Hallo-regel toevoegen `xfce4-session` vóór Hallo regel `/etc/X11/Xsession`.

toorestart hello xrdp service, gebruikt u dit:

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Verbinding maken met uw Linux-VM van een Windows-computer
In een Windows-computer start Hallo extern bureaublad-client en voer de naam van uw DNS-Linux-VM. Of Ga toohello Dashboard van de virtuele machine in hello Azure-portal en klik op `Connect` tooconnect uw Linux-VM. In dat geval ziet u Hallo aanmeldingsvenster:

![Afbeelding](./media/remote-desktop/no2.png)

Aanmelden met Hallo-gebruikersnaam en wachtwoord van uw Linux-VM.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het gebruik van xrdp [http://www.xrdp.org/](http://www.xrdp.org/).
