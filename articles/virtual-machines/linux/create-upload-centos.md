---
title: aaaCreate een VHD en uploaden op basis van CentOS Linux in Azure
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) die een besturingssysteem op basis van CentOS Linux bevat.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>Een op CentOS gebaseerde virtuele Azure-machine voorbereiden
* [Een CentOS 6.x virtuele machine voorbereiden voor Azure](#centos-6x)
* [Een CentOS 7.0 + virtuele machine voorbereiden voor Azure](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u al een CentOS hebt geïnstalleerd (of vergelijkbaar afgeleide) Linux-besturingssysteem tooa virtuele harde schijf. Meerdere hulpprogramma's bestaan toocreate VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V. Zie voor instructies [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).

**Opmerkingen bij de installatie van centOS**

* Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.
* Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.  U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of Hallo cmdlet convert-vhd. Als u van VirtualBox gebruikmaakt betekent dit dat selecteren **een vaste grootte** als geboden toohello standaard dynamisch toegewezen bij het Hallo-schijf maken.
* Bij het installeren van Hallo Linux-systeem is *aanbevolen* dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt). Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit toobe gekoppeld tooanother moet identiek zijn VM voor het oplossen van problemen. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven.
* Kernel-ondersteuning voor het koppelen van UDF-bestandssysteem is vereist. Op de eerste keer opstarten op Azure Hallo inrichting configuratie toohello Linux VM doorgegeven via UDF-indeling media die is aangesloten toohello Gast. Hello Azure Linux-agent moet worden kunnen toomount Hallo UDF-bestand system tooread de configuratie en Hallo VM inrichten.
* Kernel-versies van Linux onder 2.6.37 ondersteunen geen NUMA op Hyper-V met grotere virtuele machine. Dit probleem voornamelijk effecten oudere distributies Hallo stroomopwaarts met Red Hat 2.6.32 kernel, en is vastgesteld in RHEL 6.6 (kernel 2.6.32 504). Systemen met aangepaste kernels die ouder zijn dan 2.6.37 of op basis van RHEL kernels die ouder zijn dan 2.6.32-504 moet ingesteld Hallo opstarten parameter `numa=off` op Hallo kernel opdrachtregelprogramma in grub.conf. Zie voor meer informatie Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Configureer een partitie van de wisseling niet op Hallo OS-schijf. Hallo Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.  Meer informatie hierover vindt u in onderstaande Hallo stappen.
* Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.

## <a name="centos-6x"></a>CentOS 6.x

1. Selecteer Hallo virtuele machine in Hyper-V-beheer.

2. Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.

3. In CentOS 6, kan NetworkManager hello Azure Linux agent verstoren. Dit pakket verwijderen door het uitvoeren van de volgende opdracht Hallo:
   
        # sudo rpm -e --nodeps NetworkManager

4. Maken of bewerken Hallo bestand `/etc/sysconfig/network` en voeg de volgende tekst hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Maken of bewerken Hallo bestand `/etc/sysconfig/network-scripts/ifcfg-eth0` en voeg de volgende tekst hello:
   
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
   
        # sudo chkconfig network on

8. Als u toouse hello OpenLogic mirrors die worden gehost in Azure-datacenters hello dat wilt, vervangt u Hallo `/etc/yum.repos.d/CentOS-Base.repo` bestand met de Hallo opslagplaatsen te volgen.  Hierdoor wordt ook toegevoegd Hallo **[openlogic]** opslagplaats met extra pakketten zoals hello Azure Linux agent:

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    Hallo rest van deze handleiding wordt wordt ervan uitgegaan dat u ten minste Hallo `[openlogic]` opslagplaats die wordt gebruikt tooinstall hello Azure Linux agent hieronder.


9. Hallo regel too/etc/yum.conf volgende toevoegen:
    
        http_caching=packages

10. Voer Hallo opdracht tooclear Hallo huidige yum metagegevens en de updatebestanden Hallo systeem met de meest recente hello-pakketten te volgen:
    
        # yum clean all

    Tenzij u een afbeelding voor een oudere versie van CentOS maakt, wordt het aanbevolen om alle Hallo tooupdate pakketten toohello laatste:

        # sudo yum -y update

    Mogelijk opnieuw worden opgestart na het uitvoeren van deze opdracht zijn vereist.

11. (Optioneel) Hallo-stuurprogramma's voor Hallo Linux Integration Services (LIS) installeren.
   
    >[!IMPORTANT]
    Hallo stap is **vereist** voor CentOS 6.3 en lager en optioneel voor latere versies.

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    U kunt ook Hallo handmatige installatie-instructies volgen op Hallo [LIS downloadpagina](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall Hallo RPM naar uw virtuele machine.
 
12. Installeer de hello Azure Linux Agent en afhankelijkheden:
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    Hallo WALinuxAgent pakket verwijdert, Hallo NetworkManager en NetworkManager gnome pakketten als ze zoals beschreven in stap 3 niet al zijn verwijderd.


13. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. toodo deze, open `/boot/grub/menu.lst` in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Hiermee zorgt u ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.
    
    Bovendien toohello hierboven, het is raadzaam te*verwijderen* Hallo volgende parameters:
    
        rhgb quiet crashkernel=auto
    
    Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.  Hallo `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter verminderen Hallo en de hoeveelheid beschikbaar geheugen in Hallo VM 128 MB of meer, die mogelijk problemen op Hallo kleinere VM opmerking.

    >[!Important]
    CentOS 6.5 en eerdere moeten ook worden ingesteld Hallo kernel parameter `numa=off`. Red Hat Zie [KB 436883](https://access.redhat.com/solutions/436883).

14. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.  Dit is meestal Hallo standaard.

15. Maak geen wisselruimte op Hallo OS-schijf.
    
    Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren. Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is. Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen van de volgende parameters in Hallo `/etc/waagent.conf` op de juiste wijze:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer. Uw Linux VHD is nu gereed toobe tooAzure geüpload.


- - -
## <a name="centos-70"></a>CentOS 7.0 +
**Wijzigingen in CentOS 7 (en vergelijkbare afgeleiden)**

Een CentOS 7 virtuele machine voorbereiden voor Azure is heel vergelijkbaar tooCentOS 6, maar er zijn echter enkele belangrijke verschillen opgemerkt:

* Hallo NetworkManager van het pakket niet meer veroorzaakt een conflict met hello Azure Linux-agent. Dit pakket wordt standaard geïnstalleerd en wordt aangeraden deze niet is verwijderd.
* GRUB2 wordt nu gebruikt als Hallo standaard bootloader, zodat het Hallo-procedure voor het bewerken van de kernel parameters is gewijzigd (Zie hieronder).
* XFS is nu Hallo standaardbestandssysteem. Hallo ext4 bestandssysteem kan nog steeds worden gebruikt, indien gewenst.

**Configuratiestappen**

1. Selecteer Hallo virtuele machine in Hyper-V-beheer.

2. Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.

3. Maken of bewerken Hallo bestand `/etc/sysconfig/network` en voeg de volgende tekst hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Maken of bewerken Hallo bestand `/etc/sysconfig/network-scripts/ifcfg-eth0` en voeg de volgende tekst hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Wijzig de udev regels tooavoid statische regels voor Hallo Ethernet-interface (s) te genereren. Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. Als u toouse hello OpenLogic mirrors die worden gehost in Azure-datacenters hello dat wilt, vervangt u Hallo `/etc/yum.repos.d/CentOS-Base.repo` bestand met de Hallo opslagplaatsen te volgen.  Hierdoor wordt ook toegevoegd Hallo **[openlogic]** opslagplaats met pakketten voor hello Azure Linux agent:
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    Hallo rest van deze handleiding wordt wordt ervan uitgegaan dat u ten minste Hallo `[openlogic]` opslagplaats die wordt gebruikt tooinstall hello Azure Linux agent hieronder.

7. Voer Hallo opdracht tooclear Hallo huidige yum metagegevens te volgen en geen updates installeren:
   
        # sudo yum clean all

    Tenzij u een afbeelding voor een oudere versie van CentOS maakt, wordt het aanbevolen om alle Hallo tooupdate pakketten toohello laatste:

        # sudo yum -y update

    Een opnieuw opstarten is mogelijk vereist na het uitvoeren van deze opdracht.

8. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. toodo deze, open `/etc/default/grub` in een tekst-editor en bewerk Hallo `GRUB_CMDLINE_LINUX` parameter, bijvoorbeeld:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Hiermee zorgt u ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen. Het ook uitgeschakeld Hallo nieuwe CentOS 7 naamgevingsregels voor NIC's. Bovendien toohello hierboven, het is raadzaam te*verwijderen* Hallo volgende parameters:
   
        rhgb quiet crashkernel=auto
   
    Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort. Hallo `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter verminderen Hallo en de hoeveelheid beschikbaar geheugen in Hallo VM 128 MB of meer, die mogelijk problemen op Hallo kleinere VM opmerking.

9. Wanneer u klaar bent bewerken `/etc/default/grub` per hierboven uitgevoerd Hallo toorebuild Hallo wormgaten configuratie te volgen:
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. Als de installatiekopie van het Hallo van bouwt **VMWare, VirtualBox of KVM:** Controleer Hallo Hyper-V-stuurprogramma's zijn opgenomen in Hallo initramfs:
   
   Bewerken `/etc/dracut.conf`, inhoud toevoegen:
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   Hallo initramfs bouwen:
   
        # sudo dracut –f -v

11. Installeer de hello Azure Linux Agent en afhankelijkheden:

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. Maak geen wisselruimte op Hallo OS-schijf.
   
   Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren. Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is. Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen van de volgende parameters in Hallo `/etc/waagent.conf` op de juiste wijze:
   
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

## <a name="next-steps"></a>Volgende stappen
U bent nu klaar toouse uw CentOS Linux virtuele harde schijf toocreate nieuwe virtuele machines in Azure. Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

