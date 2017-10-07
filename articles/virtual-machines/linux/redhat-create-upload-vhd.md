---
title: aaaCreate en upload een Red Hat Enterprise Linux VHD voor gebruik in Azure | Microsoft Docs
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) waarop een Red Hat Linux-besturingssysteem.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>Een op Red Hat gebaseerde virtuele machine voor Azure voorbereiden
In dit artikel leert u hoe tooprepare een Red Hat Enterprise Linux (RHEL) virtuele machine voor gebruik in Azure. Hallo-versies van RHEL die worden besproken in dit artikel zijn 6.7 + en 7.1 +. Hallo hypervisors voor voorbereiding die worden besproken in dit artikel zijn Hyper-V, op basis van de kernel virtuele machine (KVM) en VMware. Zie voor meer informatie over de vereisten voor in aanmerking komt voor deelname aan het programma voor toegang tot de Cloud van Red Hat [Red Hat van toegang tot de Cloud website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) en [RHEL uitgevoerd op Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>Voorbereiden van een Red Hat-virtuele machine vanuit Hyper-V-beheer

### <a name="prerequisites"></a>Vereisten
Deze sectie wordt ervan uitgegaan dat u al een ISO-bestand van Hallo Red Hat website en de geïnstalleerde Hallo RHEL installatiekopie tooa virtuele harde schijf (VHD) hebt verkregen. Voor meer informatie over het toouse Hyper-V-beheer tooinstall een besturingssysteemkopie Zie [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).

**Opmerkingen bij de installatie van de RHEL**

* Azure biedt geen ondersteuning voor Hallo VHDX-indeling. Azure ondersteunt alleen vaste VHD. U kunt Hyper-V-beheer tooconvert Hallo-schijfindeling tooVHD gebruiken of kunt u Hallo convert-vhd-cmdlet. Als u VirtualBox gebruikt, selecteert u **een vaste grootte** tegenstelling tot toohello standaard dynamisch toegewezen optie wanneer u Hallo schijf maakt.
* Azure ondersteunt alleen virtuele machines van generatie 1. U kunt virtuele machines van generatie 1 converteren uit VHDX toohello VHD-bestand-indeling en dynamisch uitbreidbare tooa vaste grootte schijf. U kunt een virtuele machine generatie niet wijzigen. Zie voor meer informatie [moet ik een virtuele machine van generatie 1 of 2 maken in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).
* Hallo maximale grootte die toegestaan voor Hallo VHD is 1023 GB.
* Wanneer u Hallo Linux-besturingssysteem installeert, wordt u aangeraden dat u gebruikt standaard partities in plaats van logische Volume Manager (LVM) vaak Hallo standaardinstelling voor vele installaties. Hierdoor wordt voorkomen LVM naam conflicteert met de gekloonde virtuele machines, met name als u ooit tooattach een besturingssysteem schijf tooanother identieke virtuele machine nodig hebt voor het oplossen van problemen. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven.
* Kernel-ondersteuning voor het koppelen van bestandssystemen Universal UDF (Disk Format) is vereist. Op de eerste keer opstarten op Azure, Hallo UDF-indeling media die is doorgegeven gekoppelde toohello Gast Hallo inrichting configuratie toohello virtuele Linux-machine. Hello Azure Linux Agent moet worden kunnen toomount Hallo UDF-bestand system tooread de configuratie en Hallo virtuele machine inrichten.
* Versies van Linux-kernel Hallo die ouder dan 2.6.37 zijn ondersteunen geen niet-uniforme geheugentoegang (NUMA) op Hyper-V met grotere virtuele machine. Dit probleem voornamelijk effecten oudere distributies die gebruikmaken van Hallo stroomopwaarts Red Hat 2.6.32 kernel en is vastgesteld in RHEL 6.6 (kernel 2.6.32 504). Systemen met aangepaste kernels die ouder zijn dan 2.6.37 of RHEL-kernels die ouder dan 2.6.32-504 zijn moeten Hallo ingesteld `numa=off` parameter op Hallo kernel-opdrachtregel in grub.conf opstart. Zie voor meer informatie, Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Configureer een partitie van de wisseling niet op Hallo besturingssysteemschijf. Hallo Linux-Agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.  Meer informatie hierover vindt u in Hallo stappen te volgen.
* Alle VHD's moeten hebben-groottes met veelvouden van 1 MB zijn.

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>Voorbereiden van een RHEL 6 virtuele machine vanuit Hyper-V-beheer

1. Selecteer Hallo virtuele machine in Hyper-V-beheer.

2. Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.

3. In de RHEL 6, kan NetworkManager hello Azure Linux agent verstoren. Dit pakket verwijderen door het uitvoeren van de volgende opdracht Hallo:
   
        # sudo rpm -e --nodeps NetworkManager

4. Maken of bewerken Hallo `/etc/sysconfig/network` bestand en voeg Hallo volgende tekst:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Hallo udev regels tooavoid statische regels voor Hallo Ethernet-interface te genereren verplaatsen (of verwijderen). Deze regels veroorzaken problemen wanneer u een virtuele machine in Microsoft Azure- of Hyper-V: klonen

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:

        # sudo chkconfig network on

8. De installatie van Red Hat abonnement tooenable Hallo van pakketten uit Hallo RHEL opslagplaats registreren door het uitvoeren van de volgende opdracht Hallo:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht. Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. toodo deze wijziging, open `/boot/grub/menu.lst` in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Dit ook zorgt ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.
    
    Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:
    
        rhgb quiet crashkernel=auto
    
    Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.  U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd. Houd er rekening mee dat deze parameter Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo door 128 MB of meer vermindert. Deze configuratie mogelijk problemen op kleinere virtuele machine.

    >[!Important]
    RHEL 6.5 en eerdere moet ook worden ingesteld Hallo `numa=off` kernel-parameter. Red Hat Zie [KB 436883](https://access.redhat.com/solutions/436883).

11. Zorg ervoor dat die Hallo secure shell (SSH)-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten, die meestal Hallo standaardeigenschap. Wijzig /etc/ssh/sshd_config tooinclude Hallo volgt regel:

        ClientAliveInterval 180

12. Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    Installeren Hallo WALinuxAgent pakket verwijderd Hallo NetworkManager en NetworkManager gnome pakketten als ze zijn niet verwijderd in stap 3.

13. Maak geen wisselruimte op Hallo besturingssysteemschijf.

    Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure. Houd er rekening mee dat Hallo lokale schijf van de resource is een tijdelijke schijf en dat deze kan worden leeggemaakt wanneer Hallo virtuele machine is gemaakt. Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzig Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. Hef de registratie van Hallo-abonnement (indien nodig) door het uitvoeren van de volgende opdracht Hallo:

        # sudo subscription-manager unregister

15. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. Klik op **actie** > **afgesloten** in Hyper-V-beheer. Uw Linux VHD is nu gereed toobe tooAzure geüpload.


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>Voorbereiden van een RHEL 7 virtuele machine vanuit Hyper-V-beheer

1. Selecteer Hallo virtuele machine in Hyper-V-beheer.

2. Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.

3. Maken of bewerken Hallo `/etc/sysconfig/network` bestand en voeg Hallo volgende tekst:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:

        # sudo chkconfig network on

6. De installatie van Red Hat abonnement tooenable Hallo van pakketten uit Hallo RHEL opslagplaats registreren door het uitvoeren van de volgende opdracht Hallo:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. toodo deze wijziging, open `/etc/default/grub` in een teksteditor en bewerken Hallo `GRUB_CMDLINE_LINUX` parameter. Bijvoorbeeld:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Dit ook zorgt ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen. Deze configuratie wordt ook uitgeschakeld Hallo nieuwe RHEL 7 naamgevingsregels voor NIC's. Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:
   
        rhgb quiet crashkernel=auto
   
    Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort. U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd. Houd er rekening mee dat deze parameter wordt gereduceerd Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.

8. Nadat u klaar bent bewerken `/etc/default/grub`, voert hello na de opdracht toorebuild Hallo wormgaten configuratie:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten, die meestal Hallo standaardeigenschap. Wijzig `/etc/ssh/sshd_config` tooinclude Hallo volgt regel:

        ClientAliveInterval 180

10. Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht. Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. Maak geen wisselruimte op Hallo besturingssysteemschijf.

    Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure. Houd er rekening mee dat hello lokale resource schijf een tijdelijke schijf is en kan worden leeggemaakt wanneer Hallo virtuele machine gemaakt is. Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzigen Hallo-parameters in volgende `/etc/waagent.conf` op de juiste wijze:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Als u toounregister Hallo abonnement wilt, Voer Hallo volgende opdracht:

        # sudo subscription-manager unregister

14. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Klik op **actie** > **afgesloten** in Hyper-V-beheer. Uw Linux VHD is nu gereed toobe tooAzure geüpload.


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>Een Red Hat-virtuele machine uit KVM voorbereiden
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>Een virtuele machine van RHEL 6 uit KVM voorbereiden

1. Hallo KVM-installatiekopie RHEL 6 downloaden van Hallo Red Hat website.

2. Een root-wachtwoord instellen.

    Een versleutelde wachtwoord genereren voor en kopieer de uitvoer Hallo Hallo-opdracht:

        # openssl passwd -1 changeme

    Stel het wachtwoord voor een hoofdaccount met guestfish:
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Wijziging Hallo tweede veld van de hoofdgebruiker Hallo uit '. ' toohello versleutelde wachtwoord.

3. Een virtuele machine in KVM uit Hallo qcow2 installatiekopie maken. Hallo schijftype te ingesteld**qcow2**, en stel Hallo virtueel netwerk interface-Apparaatmodel te**virtio**. Vervolgens Hallo virtuele machine starten en meld u aan als hoofdmap.

4. Maken of bewerken Hallo `/etc/sysconfig/network` bestand en voeg Hallo volgende tekst:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Hallo udev regels tooavoid statische regels voor Hallo Ethernet-interface te genereren verplaatsen (of verwijderen). Deze regels veroorzaken problemen wanneer u een virtuele machine in Azure of Hyper-V: klonen

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:

        # chkconfig network on

8. De installatie van Red Hat abonnement tooenable Hallo van pakketten uit Hallo RHEL opslagplaats registreren door het uitvoeren van de volgende opdracht Hallo:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. toodo deze configuratie, open `/boot/grub/menu.lst` in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Dit ook zorgt ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.
    
    Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:
    
        rhgb quiet crashkernel=auto
    
    Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort. U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd. Houd er rekening mee dat deze parameter wordt gereduceerd Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.

    >[!Important]
    RHEL 6.5 en eerdere moet ook worden ingesteld Hallo `numa=off` kernel-parameter. Red Hat Zie [KB 436883](https://access.redhat.com/solutions/436883).

10. Hyper-V-modules tooinitramfs toevoegen:  

    Bewerken `/etc/dracut.conf`, en voeg Hallo volgende inhoud:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Opnieuw samenstellen initramfs:

        # dracut -f -v

11. Cloud-init verwijderen:

        # yum remove cloud-init

12. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten:

        # chkconfig sshd on

    Wijzig /etc/ssh/sshd_config tooinclude Hallo volgende regels:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht. Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:

        # yum install WALinuxAgent

        # chkconfig waagent on

15. Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure. Houd er rekening mee dat hello lokale resource schijf een tijdelijke schijf is en kan worden leeggemaakt wanneer Hallo virtuele machine gemaakt is. Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzigen Hallo-parameters in volgende **/etc/waagent.conf** op de juiste wijze:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Hef de registratie van Hallo-abonnement (indien nodig) door het uitvoeren van de volgende opdracht Hallo:

        # subscription-manager unregister

17. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Hallo virtuele machine in KVM afgesloten.

19. Hallo qcow2 installatiekopie toohello VHD-indeling converteren.

    Hiermee converteert u eerst Hallo tooraw afbeeldingsindeling:

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    Zorg ervoor dat het Hallo-grootte van Hallo onbewerkte afbeelding wordt uitgelijnd met 1 MB. Anders afronden Hallo grootte tooalign met minimaal 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Hallo onbewerkte schijf tooa converteren vaste grootte en VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>Een virtuele machine voor RHEL 7 van KVM voorbereiden

1. Hallo KVM-installatiekopie RHEL 7 downloaden van Hallo Red Hat website. Deze procedure maakt gebruik van RHEL 7 als voorbeeld Hallo.

2. Een root-wachtwoord instellen.

    Een versleutelde wachtwoord genereren voor en kopieer de uitvoer Hallo Hallo-opdracht:

        # openssl passwd -1 changeme

    Stel het wachtwoord voor een hoofdaccount met guestfish:

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Wijziging Hallo tweede veld van de hoofdgebruiker van '. ' toohello versleutelde wachtwoord.

3. Een virtuele machine in KVM uit Hallo qcow2 installatiekopie maken. Hallo schijftype te ingesteld**qcow2**, en stel Hallo virtueel netwerk interface-Apparaatmodel te**virtio**. Vervolgens Hallo virtuele machine starten en meld u aan als hoofdmap.

4. Maken of bewerken Hallo `/etc/sysconfig/network` bestand en voeg Hallo volgende tekst:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:

        # chkconfig network on

7. Registreer uw Red Hat abonnement tooenable installatie van pakketten uit Hallo RHEL opslagplaats door het uitvoeren van de volgende opdracht Hallo:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. toodo deze configuratie, open `/etc/default/grub` in een teksteditor en bewerken Hallo `GRUB_CMDLINE_LINUX` parameter. Bijvoorbeeld:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Met deze opdracht zorgt er ook voor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen. Hallo-opdracht worden ook uitgeschakeld Hallo nieuwe RHEL 7 naamconventies NIC's. Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:
   
        rhgb quiet crashkernel=auto
   
    Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort. U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd. Houd er rekening mee dat deze parameter wordt gereduceerd Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.

9. Nadat u klaar bent bewerken `/etc/default/grub`, voert hello na de opdracht toorebuild Hallo wormgaten configuratie:

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. Hyper-V-modules toevoegen aan initramfs.

    Bewerken `/etc/dracut.conf` en inhoud toevoegen:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Opnieuw samenstellen initramfs:

        # dracut -f -v

11. Cloud-init verwijderen:

        # yum remove cloud-init

12. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten:

        # systemctl enable sshd

    Wijzig /etc/ssh/sshd_config tooinclude Hallo volgende regels:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht. Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:

        # yum install WALinuxAgent

    Hallo waagent-service inschakelen:

        # systemctl enable waagent.service

15. Maak geen wisselruimte op Hallo besturingssysteemschijf.

    Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure. Houd er rekening mee dat hello lokale resource schijf een tijdelijke schijf is en kan worden leeggemaakt wanneer Hallo virtuele machine gemaakt is. Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzigen Hallo-parameters in volgende `/etc/waagent.conf` op de juiste wijze:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Hef de registratie van Hallo-abonnement (indien nodig) door het uitvoeren van de volgende opdracht Hallo:

        # subscription-manager unregister

17. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Hallo virtuele machine in KVM afgesloten.

19. Hallo qcow2 installatiekopie toohello VHD-indeling converteren.

    Hiermee converteert u eerst Hallo tooraw afbeeldingsindeling:

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    Zorg ervoor dat het Hallo-grootte van Hallo onbewerkte afbeelding wordt uitgelijnd met 1 MB. Anders afronden Hallo grootte tooalign met minimaal 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Hallo onbewerkte schijf tooa converteren vaste grootte en VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>Een Red Hat-virtuele machine van VMware voorbereiden
### <a name="prerequisites"></a>Vereisten
Deze sectie wordt ervan uitgegaan dat u al een RHEL virtuele machine in VMware hebt geïnstalleerd. Voor meer informatie over hoe tooinstall een besturingssysteem in VMware, Zie [VMware Guest Operating System installatiehandleiding](http://partnerweb.vmware.com/GOSIG/home.html).

* Wanneer u Hallo Linux-besturingssysteem installeert, wordt u aangeraden dat u gebruikt standaard partities in plaats van LVM, vaak Hallo standaardinstelling voor vele installaties. Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machine, met name als de schijf van een besturingssysteem ooit toobe gekoppeld tooanother virtuele machine voor het oplossen van problemen moet. LVM of RAID kan worden gebruikt op gegevensschijven als voorkeur.
* Configureer een partitie van de wisseling niet op Hallo besturingssysteemschijf. U kunt Hallo Linux agent toocreate een wisselbestand op Hallo tijdelijke schijf configureren. U vindt meer informatie over deze in Hallo stappen volgen.
* Wanneer u Hallo virtuele hardeschijf maakt, selecteert u **Store virtuele schijf als een enkel bestand**.

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>Een RHEL 6 virtuele machine van VMware voorbereiden
1. In de RHEL 6, kan NetworkManager hello Azure Linux agent verstoren. Dit pakket verwijderen door het uitvoeren van de volgende opdracht Hallo:
   
        # sudo rpm -e --nodeps NetworkManager

2. Maak een bestand met de naam **netwerk** Hallo in Hallo/etc/sysconfig/directory waarin tekst te volgen:

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. Hallo udev regels tooavoid statische regels voor Hallo Ethernet-interface te genereren verplaatsen (of verwijderen). Deze regels veroorzaken problemen wanneer u een virtuele machine in Azure of Hyper-V: klonen

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:

        # sudo chkconfig network on

6. De installatie van Red Hat abonnement tooenable Hallo van pakketten uit Hallo RHEL opslagplaats registreren door het uitvoeren van de volgende opdracht Hallo:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht. Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. toodo deze, open `/etc/default/grub` in een teksteditor en bewerken Hallo `GRUB_CMDLINE_LINUX` parameter. Bijvoorbeeld:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   Dit ook zorgt ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen. Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:
   
        rhgb quiet crashkernel=auto
   
    Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort. U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd. Houd er rekening mee dat deze parameter wordt gereduceerd Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.

9. Hyper-V-modules tooinitramfs toevoegen:

    Bewerken `/etc/dracut.conf`, en voeg Hallo volgende inhoud:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Opnieuw samenstellen initramfs:

        # dracut -f -v

10. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten, die meestal Hallo standaardeigenschap. Wijzig `/etc/ssh/sshd_config` tooinclude Hallo volgt regel:

    ClientAliveInterval 180

11. Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. Maak geen wisselruimte op Hallo besturingssysteemschijf.

    Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure. Houd er rekening mee dat hello lokale resource schijf een tijdelijke schijf is en kan worden leeggemaakt wanneer Hallo virtuele machine gemaakt is. Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzigen Hallo-parameters in volgende `/etc/waagent.conf` op de juiste wijze:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Hef de registratie van Hallo-abonnement (indien nodig) door het uitvoeren van de volgende opdracht Hallo:

        # sudo subscription-manager unregister

14. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Hallo virtuele machine afsluiten en converteer deze Hallo VMDK-bestand tooa .vhd-bestand.

    Hiermee converteert u eerst Hallo tooraw afbeeldingsindeling:

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    Zorg ervoor dat het Hallo-grootte van Hallo onbewerkte afbeelding wordt uitgelijnd met 1 MB. Anders afronden Hallo grootte tooalign met minimaal 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Hallo onbewerkte schijf tooa converteren vaste grootte en VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>Een RHEL 7 virtuele machine van VMware voorbereiden
1. Maken of bewerken Hallo `/etc/sysconfig/network` bestand en voeg Hallo volgende tekst:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. Maken of bewerken Hallo `/etc/sysconfig/network-scripts/ifcfg-eth0` bestand en voeg Hallo volgende tekst:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. Zorg ervoor dat de netwerkservice Hallo door het uitvoeren van de volgende opdracht Hallo tijdens het opstarten wordt gestart:

        # sudo chkconfig network on

4. De installatie van Red Hat abonnement tooenable Hallo van pakketten uit Hallo RHEL opslagplaats registreren door het uitvoeren van de volgende opdracht Hallo:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. toodo deze wijziging, open `/etc/default/grub` in een teksteditor en bewerken Hallo `GRUB_CMDLINE_LINUX` parameter. Bijvoorbeeld:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Deze configuratie zorgt er ook voor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen. Het ook uitgeschakeld Hallo nieuwe RHEL 7 naamgevingsregels voor NIC's. Bovendien is het raadzaam dat u de volgende parameters Hallo verwijderen:
   
        rhgb quiet crashkernel=auto
   
    Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort. U kunt laten Hallo `crashkernel` optie desgewenst geconfigureerd. Houd er rekening mee dat deze parameter wordt gereduceerd Hallo en de hoeveelheid beschikbaar geheugen in de virtuele machine Hallo 128 MB of meer, die mogelijk problemen op kleinere virtuele machine.

6. Nadat u klaar bent bewerken `/etc/default/grub`, voert hello na de opdracht toorebuild Hallo wormgaten configuratie:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. Hyper-V-modules tooinitramfs toevoegen.

    Bewerken `/etc/dracut.conf`, inhoud toevoegen:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Opnieuw samenstellen initramfs:

        # dracut -f -v

8. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten. Dit is meestal Hallo standaardinstelling. Wijzig `/etc/ssh/sshd_config` tooinclude Hallo volgt regel:

        ClientAliveInterval 180

9. Hallo WALinuxAgent pakket, `WALinuxAgent-<version>`, heeft toohello Red Hat extra's opslagplaats is gepusht. Hallo-opslagplaats voor extra's inschakelen door het uitvoeren van de volgende opdracht Hallo:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. Maak geen wisselruimte op Hallo besturingssysteemschijf.

    Hello Azure Linux Agent kunt wisselruimte automatisch configureren met behulp van Hallo lokale resource schijf die is aangesloten toohello virtuele machine nadat Hallo virtuele machine is ingericht op Azure. Houd er rekening mee dat hello lokale resource schijf een tijdelijke schijf is en kan worden leeggemaakt wanneer Hallo virtuele machine gemaakt is. Nadat u in de vorige stap Hallo hello Azure Linux Agent hebt geïnstalleerd, wijzigen Hallo-parameters in volgende `/etc/waagent.conf` op de juiste wijze:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. Als u toounregister Hallo abonnement wilt, Voer Hallo volgende opdracht:

        # sudo subscription-manager unregister

13. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. Hallo virtuele machine afsluiten en Hallo VMDK-bestand toohello VHD-indeling converteren.

    Hiermee converteert u eerst Hallo tooraw afbeeldingsindeling:

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    Zorg ervoor dat het Hallo-grootte van Hallo onbewerkte afbeelding wordt uitgelijnd met 1 MB. Anders afronden Hallo grootte tooalign met minimaal 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Hallo onbewerkte schijf tooa converteren vaste grootte en VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>Een Red Hat-virtuele machine van een ISO met behulp van een bestand kickstart automatisch voorbereiden
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>Een RHEL 7 virtuele machine uit een bestand kickstart voorbereiden

1.  Maak een kickstart-bestand dat Hallo na inhoud bevat en sla Hallo-bestand. Zie voor meer informatie over installatie kickstart hello [Kickstart installatiehandleiding](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. Plaats Hallo kickstart bestand waartoe Hallo installatie systeem toegang heeft.

3. Maak een nieuwe virtuele machine in Hyper-V-beheer. Op Hallo **virtuele hardeschijf aansluiten** pagina **later een virtuele harde schijf koppelen**, en volledige Hallo Wizard Nieuwe virtuele Machine.

4. Open de instellingen van de virtuele machine Hallo:

    a.  Een nieuwe virtuele machine van de virtuele harde schijf toohello koppelen. Zorg ervoor dat tooselect **VHD-indeling** en **vaste grootte**.

    b.  Hallo installatie ISO toohello DVD-station koppelen.

    c.  Hallo BIOS tooboot instellen vanaf de CD.

5. Hallo virtuele machine te starten. Wanneer de installatiehandleiding hello wordt weergegeven, drukt u op **tabblad** tooconfigure Hallo opstartopties.

6. Voer `inst.ks=<hello location of hello kickstart file>` aan einde van Hallo opstartopties en druk op Hallo **Enter**.

7. Wachten op Hallo installatie toofinish. Wanneer deze voltooid, wordt Hallo virtuele machine automatisch afgesloten. Uw Linux VHD is nu gereed toobe tooAzure geüpload.

## <a name="known-issues"></a>Bekende problemen
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>Hallo Hyper-V-stuurprogramma kan niet worden opgenomen in Hallo initiële RAM-schijf wanneer u een niet-Hyper-V-hypervisor

In sommige gevallen Linux installatieprogramma's mogelijk niet opnemen Hallo stuurprogramma's voor Hyper-V in Hallo initiële RAM-schijf (initrd of initramfs) tenzij Linux vaststelt dat deze wordt uitgevoerd in een Hyper-V-omgeving.

Wanneer u een andere virtualisatie systeem (dat wil zeggen, Virtualbox, Xen, enz.) tooprepare uw Linux-installatiekopie, moet u mogelijk toorebuild initrd tooensure die ten minste Hallo hv_vmbus en hv_storvsc kernel-modules zijn beschikbaar op Hallo initiële RAM-schijf. Dit is een bekend probleem ten minste op systemen die zijn gebaseerd op Hallo upstream Red Hat distributiepunt.

tooresolve dit probleem, Hyper-V-modules tooinitramfs toevoegen en opnieuw maken:

Bewerken `/etc/dracut.conf`, en voeg Hallo volgende inhoud:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

Opnieuw samenstellen initramfs:

        # dracut -f -v

Zie voor meer informatie, Hallo informatie over [opnieuw opbouwen van initramfs](https://access.redhat.com/solutions/1958).

## <a name="next-steps"></a>Volgende stappen
U bent nu klaar toouse uw Red Hat Enterprise Linux virtuele harde schijf toocreate nieuwe virtuele machines in Azure. Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Zie voor meer informatie over Hallo hypervisors die zijn gecertificeerd toorun Red Hat Enterprise Linux, [Hallo Red Hat website](https://access.redhat.com/certified-hypervisors).
