---
title: aaaCreate en een Oracle Linux VHD uploaden | Microsoft Docs
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) met een Oracle Linux-besturingssysteem.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>Een virtuele Oracle Linux-machine voor Azure voorbereiden
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u al een Oracle Linux-besturingssysteem tooa virtuele harde schijf hebt geïnstalleerd. Meerdere hulpprogramma's bestaan toocreate VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V. Zie voor instructies [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="oracle-linux-installation-notes"></a>Opmerkingen bij de installatie van de Oracle Linux
* Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.
* Oracle van Red Hat compatibel kernel en hun UEK3 (Unbreakable Enterprise Kernel) worden beide ondersteund op Hyper-V en Azure. Zorg ervoor dat tooupdate toohello nieuwste kernel tijdens het voorbereiden van uw Oracle Linux VHD voor de beste resultaten.
* UEK2 van Oracle wordt niet ondersteund op Hyper-V en Azure zoals geen stuurprogramma's Hallo vereist bevat.
* Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.  U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of Hallo cmdlet convert-vhd.
* Bij het installeren van Hallo Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt). Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit moet toobe gekoppeld tooanother VM voor het oplossen van problemen. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.
* NUMA wordt niet ondersteund voor grotere VM-groottes vanwege tooa fout in de kernel-versies van Linux onder 2.6.37. Dit probleem voornamelijk effecten distributies met Hallo upstream Red Hat 2.6.32 kernel. Handmatige installatie van hello Azure Linux-agent (waagent) wordt automatisch NUMA uitgeschakeld in Hallo WORMGATEN configuratie voor Hallo Linux kernel. Meer informatie hierover vindt u in onderstaande Hallo stappen.
* Configureer een partitie van de wisseling niet op Hallo OS-schijf. Hallo Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.  Meer informatie hierover vindt u in onderstaande Hallo stappen.
* Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.
* Zorg ervoor dat Hallo `Addons` opslagplaats is ingeschakeld. Hallo-bestand bewerken `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) of `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux), en wijzig Hallo regel `enabled=0` te`enabled=1` onder **[ol6_addons]** of **[ol7_addons]** in deze het bestand.

## <a name="oracle-linux-64"></a>Oracle Linux 6.4 +
U moet de specifieke configuratiestappen in Hallo besturingssysteem Hallo virtuele machine toorun in Azure voltooien.

1. Selecteer Hallo virtuele machine in Hallo middelste deelvenster van de Hyper-V-beheer.
2. Klik op **Connect** tooopen Hallo venster voor Hallo virtuele machine.
3. NetworkManager verwijderen door het uitvoeren van de volgende opdracht Hallo:
   
        # sudo rpm -e --nodeps NetworkManager
   
    **Opmerking:** als Hallo pakket nog niet is geïnstalleerd, deze opdracht mislukt met een foutbericht weergegeven. Dit is normaal.
4. Maak een bestand met de naam **netwerk** in Hallo `/etc/sysconfig/` map waarin zich de volgende tekst hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. Maak een bestand met de naam **ifcfg eth0** in Hallo `/etc/sysconfig/network-scripts/` map waarin zich de volgende tekst hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. Wijzig de udev regels tooavoid statische regels voor Hallo Ethernet-interface (s) te genereren. Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. Zorg ervoor dat Hallo netwerkservice tijdens het opstarten wordt gestart door het uitvoeren van de volgende opdracht Hallo:
   
        # chkconfig network on
8. Python-pyasn1 door het uitvoeren van de volgende opdracht Hallo installeren:
   
        # sudo yum install python-pyasn1
9. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. dit open toodo ' / boot/grub/menu.lst ' in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   Hiermee zorgt u ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen. Hiermee wordt het NUMA uitgeschakeld vanwege tooa fout in Oracle van Red Hat compatibel kernel.
   
   Bovendien toohello hierboven, het is raadzaam te*verwijderen* Hallo volgende parameters:
   
        rhgb quiet crashkernel=auto
   
   Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.
   
   Hallo `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter verminderen Hallo en de hoeveelheid beschikbaar geheugen in Hallo VM 128 MB of meer, die mogelijk problemen op Hallo kleinere VM opmerking.
10. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.  Dit is meestal Hallo standaard.
11. Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo. Hallo meest recente versie is 2.0.15.
    
        # sudo yum install WALinuxAgent
    
    Houd er rekening mee dat installeren Hallo WALinuxAgent pakket Hallo NetworkManager wordt verwijderd en NetworkManager gnome pakketten als ze zijn niet al verwijderd zoals beschreven in stap 2.
12. Maak geen wisselruimte op Hallo OS-schijf.
    
    Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren. Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is. Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer. Uw Linux VHD is nu gereed toobe tooAzure geüpload.

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0 +
**Wijzigingen in Oracle Linux 7**

Een virtuele machine van de Oracle Linux 7 voorbereiden voor Azure is heel vergelijkbaar tooOracle Linux 6, maar er zijn echter enkele belangrijke verschillen opgemerkt:

* Hallo Red Hat compatibel kernel zowel van Oracle UEK3 worden ondersteund in Azure.  Hallo UEK3 kernel wordt aanbevolen.
* Hallo NetworkManager van het pakket niet meer veroorzaakt een conflict met hello Azure Linux-agent. Dit pakket wordt standaard geïnstalleerd en wordt aangeraden deze niet is verwijderd.
* GRUB2 wordt nu gebruikt als Hallo standaard bootloader, zodat het Hallo-procedure voor het bewerken van de kernel parameters is gewijzigd (Zie hieronder).
* XFS is nu Hallo standaardbestandssysteem. Hallo ext4 bestandssysteem kan nog steeds worden gebruikt, indien gewenst.

**Configuratiestappen**

1. Selecteer Hallo virtuele machine in Hyper-V-beheer.
2. Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.
3. Maak een bestand met de naam **netwerk** in Hallo `/etc/sysconfig/` map waarin zich de volgende tekst hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. Maak een bestand met de naam **ifcfg eth0** in Hallo `/etc/sysconfig/network-scripts/` map waarin zich de volgende tekst hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. Wijzig de udev regels tooavoid statische regels voor Hallo Ethernet-interface (s) te genereren. Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. Zorg ervoor dat Hallo netwerkservice tijdens het opstarten wordt gestart door het uitvoeren van de volgende opdracht Hallo:
   
        # sudo chkconfig network on
7. Hallo python pyasn1 pakket installeren door het uitvoeren van de volgende opdracht Hallo:
   
        # sudo yum install python-pyasn1
8. Voer Hallo opdracht tooclear Hallo huidige yum metagegevens te volgen en geen updates installeren:
   
        # sudo yum clean all
        # sudo yum -y update
9. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. toodo dat openen '/ standaard/etc/grub' in een tekst-editor en bewerk Hallo `GRUB_CMDLINE_LINUX` parameter, bijvoorbeeld:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Hiermee zorgt u ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen. Het ook uitgeschakeld Hallo nieuwe indicatie 7 naamgevingsregels voor NIC's. Bovendien toohello hierboven, het is raadzaam te*verwijderen* Hallo volgende parameters:
   
       rhgb quiet crashkernel=auto
   
   Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.
   
   Hallo `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter verminderen Hallo en de hoeveelheid beschikbaar geheugen in Hallo VM 128 MB of meer, die mogelijk problemen op Hallo kleinere VM opmerking.
10. Wanneer u klaar bent editing '/ standaard/etc/grub' uitgevoerd per hierboven Hallo toorebuild Hallo wormgaten configuratie te volgen:
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.  Dit is meestal Hallo standaard.
12. Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. Maak geen wisselruimte op Hallo OS-schijf.
    
    Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren. Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is. Na de installatie van hello Azure Linux Agent (Zie de vorige stap Hallo), wijzigen Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer. Uw Linux VHD is nu gereed toobe tooAzure geüpload.

## <a name="next-steps"></a>Volgende stappen
U bent nu klaar toouse uw Oracle Linux .vhd toocreate nieuwe virtuele machines in Azure. Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

