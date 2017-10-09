---
title: aaaCreate een VHD en uploaden SUSE Linux in Azure
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) waarop een SUSE Linux-besturingssysteem.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Een op SLES of openSUSE gebaseerde virtuele machine voor Azure voorbereiden
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u al hebt geïnstalleerd een SUSE of openSUSE Linux-besturingssysteem tooa virtuele harde schijf. Meerdere hulpprogramma's bestaan toocreate VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V. Zie voor instructies [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="sles--opensuse-installation-notes"></a>SLES / openSUSE opmerkingen bij de installatie
* Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.
* Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.  U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of Hallo cmdlet convert-vhd.
* Bij het installeren van Hallo Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt). Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit moet toobe gekoppeld tooanother VM voor het oplossen van problemen. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.
* Configureer een partitie van de wisseling niet op Hallo OS-schijf. Hallo Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.  Meer informatie hierover vindt u in onderstaande Hallo stappen.
* Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.

## <a name="use-suse-studio"></a>SUSE Studio gebruiken
[SUSE Studio](http://www.susestudio.com) eenvoudig kunt maken en beheren van uw afbeeldingen SLES en openSUSE voor Azure en Hyper-V. Dit is de aanbevolen aanpak voor het aanpassen van uw eigen installatiekopieën SLES en openSUSE Hallo.

Als een alternatieve toobuilding uw eigen VHD, SUSE publiceert ook BYOS (uw eigen abonnement Bring) installatiekopieën voor SLES op [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>SUSE Linux Enterprise Server 11 SP4 voorbereiden
1. Selecteer Hallo virtuele machine in Hallo middelste deelvenster van de Hyper-V-beheer.
2. Klik op **Connect** tooopen Hallo venster voor Hallo virtuele machine.
3. Registreren van uw systeem SUSE Linux Enterprise tooallow het toodownload updates en pakketten worden geïnstalleerd.
4. Hallo systeem bijwerken met de meest recente patches Hallo:
   
        # sudo zypper update
5. Hello Azure Linux Agent uit Hallo SLES opslagplaats installeren:
   
        # sudo zypper install WALinuxAgent
6. Controleer als waagent te 'op' is ingesteld in chkconfig en als dat niet inschakelen voor automatisch starten:
   
        # sudo chkconfig waagent on
7. Controleer of waagent-service wordt uitgevoerd en als dat niet starten: 
   
        # sudo service waagent start
8. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. dit open toodo ' / boot/grub/menu.lst ' in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    Hierdoor worden alle console berichten worden toohello eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.
9. Bevestig dat fstab /boot/grub/menu.lst en/etc/beide verwijzing Hallo-schijf met de UUID (door uuid) in plaats van Hallo schijf-ID (door-id). 
   
    Schijf UUID ophalen
   
        # ls /dev/disk/by-uuid/
   
    Als /dev/disk/by-id-/boot/grub/menu.lst zowel/etc/fstab gebruikt, worden bijgewerkt met Hallo juiste door uuid waarde
   
    Voordat de wijziging
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    Na wijziging
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. Wijzig de udev regels tooavoid statische regels voor Hallo Ethernet-interface (s) te genereren. Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. Het verdient aanbeveling tooedit Hallo bestand '/ etc/sysconfig/netwerk/dhcp' en wijzigt u Hallo `DHCLIENT_SET_HOSTNAME` parameter toohello volgende:
    
     DHCLIENT_SET_HOSTNAME = "Nee"
12. In '/ etc/sudoers', uitschakelen of verwijderen Hallo volgende regels, indien aanwezig:
    
     Standaard targetpw # om Hallo-wachtwoord van de doelgebruiker Hallo dat wil zeggen hoofdmap alle ALL=(ALL) alle vragen # waarschuwing! Gebruik alleen deze samen met 'Standaardwaarden targetpw'!
13. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.  Dit is meestal Hallo standaard.
14. Maak geen wisselruimte op Hallo OS-schijf.
    
    Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren. Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is. Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Opmerking: deze moet u toobe toowhatever ingesteld.
15. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent-force - deprovision
    # <a name="export-histsize0"></a>exporteren van HISTSIZE = 0
    # <a name="logout"></a>afmelden
16. Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer. Uw Linux VHD is nu gereed toobe tooAzure geüpload.

- - -
## <a name="prepare-opensuse-131"></a>OpenSUSE 13,1 + voorbereiden
1. Selecteer Hallo virtuele machine in Hallo middelste deelvenster van de Hyper-V-beheer.
2. Klik op **Connect** tooopen Hallo venster voor Hallo virtuele machine.
3. Voer op Hallo-shell Hallo-opdracht '`zypper lr`'. Als u deze opdracht retourneert de uitvoer vergelijkbare toohello te volgen, en vervolgens het Hallo-opslagplaatsen zijn geconfigureerd zoals verwacht--zonder aanpassingen nodig zijn (opmerking die versienummers kunnen verschillen):
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    Als Hallo opdracht retourneert 'Geen opslagplaatsen gedefinieerd...' gebruikt Hallo opdrachten tooadd na deze repo's:
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    U kunt vervolgens controleren of het Hallo-opslagplaatsen zijn toegevoegd met de opdracht Hallo '`zypper lr`' opnieuw. Als een van de relevante update-opslagplaatsen Hallo niet is ingeschakeld, wordt dit inschakelen met de volgende opdracht:
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. Hallo kernel toohello meest recente versie bijwerken:
   
        # sudo zypper up kernel-default
   
    Of tooupdate Hallo systeem met alle Hallo meest recente patches:
   
        # sudo zypper update
5. Hello Azure Linux Agent installeren.
   
   # <a name="sudo-zypper-install-walinuxagent"></a>sudo zypper installeren WALinuxAgent
6. Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen. toodo deze, open ' / boot/grub/menu.lst ' in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:
   
     console = ttyS0 earlyprintk ttyS0 rootdelay = 300 =
   
   Hierdoor worden alle console berichten worden toohello eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen. Bovendien verwijderen Hallo volgende parameters uit Hallo kernel opstarten regel als deze bestaan:
   
     libata.atapi_enabled=0 reserve = 0x1f0, 0x8
7. Het verdient aanbeveling tooedit Hallo bestand '/ etc/sysconfig/netwerk/dhcp' en wijzigt u Hallo `DHCLIENT_SET_HOSTNAME` parameter toohello volgende:
   
     DHCLIENT_SET_HOSTNAME = "Nee"
8. **Belangrijk:** In '/ etc/sudoers', uitschakelen of verwijderen Hallo volgende regels, indien aanwezig:
   
     Standaard targetpw # om Hallo-wachtwoord van de doelgebruiker Hallo dat wil zeggen hoofdmap alle ALL=(ALL) alle vragen # waarschuwing! Gebruik alleen deze samen met 'Standaardwaarden targetpw'!
9. Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.  Dit is meestal Hallo standaard.
10. Maak geen wisselruimte op Hallo OS-schijf.
    
    Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren. Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is. Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Opmerking: deze moet u toobe toowhatever ingesteld.
11. Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent-force - deprovision
    # <a name="export-histsize0"></a>exporteren van HISTSIZE = 0
    # <a name="logout"></a>afmelden
12. Zorg ervoor dat hello die Azure Linux Agent wordt uitgevoerd bij het opstarten:
    
        # sudo systemctl enable waagent.service
13. Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer. Uw Linux VHD is nu gereed toobe tooAzure geüpload.

## <a name="next-steps"></a>Volgende stappen
U bent nu klaar toouse uw SUSE Linux virtuele harde schijf toocreate nieuwe virtuele machines in Azure. Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

