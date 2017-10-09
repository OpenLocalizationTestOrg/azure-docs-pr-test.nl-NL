---
title: aaaCreate een Linux-VHD en uploaden in Azure
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) die een Linux-besturingssysteem bevat.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a>Informatie voor niet-aanbevolen distributies
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hello Azure-platform SLA van toepassing is toovirtual computers waarop een Linux-besturingssysteem alleen wanneer een Hallo Hallo [goedgekeurde distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) wordt gebruikt. Alle Linux-distributies die zijn opgegeven in hello Azure installatiekopie galerie zijn goedgekeurde distributies met Hallo vereiste configuratie.

* [Linux op Azure - goedgekeurde distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ondersteuning voor Linux-afbeeldingen in Microsoft Azure](https://support.microsoft.com/kb/2941892)

Alle verdelingen uitgevoerd op Azure moet toomeet een aantal vereisten toohave een kans tooproperly op Hallo platform worden uitgevoerd.  In dit artikel is geen uitgebreide omdat elk distributiepunt verschilt; en het is wel mogelijk dat zelfs als u voldoet aan alle Hallo van de onderstaande criteria die u nog steeds toosignificantly uw Linux-systeem tooensure die correct wordt uitgevoerd op Hallo platform aanpassen.

Het is daarom raadzaam dat u met een van begint onze [Linux op Azure goedgekeurde distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) indien mogelijk. Hallo volgende artikelen leidt u door hoe tooprepare Hallo verschillende Linux-distributies die worden ondersteund door Azure goedgekeurde:

* **[Op basis van centOS distributies](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Hallo rest van dit artikel wordt de nadruk gelegd op algemene richtlijnen voor het uitvoeren van uw Linux-distributie op Azure.

## <a name="general-linux-installation-notes"></a>Opmerkingen bij de installatie van de algemene Linux
* Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.  U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of Hallo cmdlet convert-vhd. Als u van VirtualBox gebruikmaakt betekent dit dat selecteren **een vaste grootte** als geboden toohello standaard dynamisch toegewezen bij het Hallo-schijf maken.
* Azure biedt alleen ondersteuning voor virtuele machines van generatie 1. U kunt een generatie 1 virtuele machine uit VHDX toohello VHD-bestand-indeling en dynamisch uitbreidbare tooa vaste schijf grootte converteren. Maar u een virtuele machine generatie niet wijzigen. Zie voor meer informatie [moet ik een virtuele machine van generatie 1 of 2 maken in Hyper-V?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)
* Hallo toegestane maximale lengte voor Hallo dat VHD is 1023 GB.
* Bij het installeren van Hallo Linux-systeem is *aanbevolen* dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt). Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit toobe gekoppeld tooanother moet identiek zijn VM voor het oplossen van problemen. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven.
* Kernel-ondersteuning voor het koppelen van UDF-bestandssysteem is vereist. Op de eerste keer opstarten op Azure Hallo inrichting configuratie toohello Linux VM doorgegeven via UDF-indeling media die is aangesloten toohello Gast. Hello Azure Linux-agent moet worden kunnen toomount Hallo UDF-bestand system tooread de configuratie en Hallo VM inrichten.
* Kernel-versies van Linux onder 2.6.37 ondersteunen geen NUMA op Hyper-V met grotere virtuele machine. Dit probleem voornamelijk effecten oudere distributies Hallo stroomopwaarts met Red Hat 2.6.32 kernel, en is vastgesteld in RHEL 6.6 (kernel 2.6.32 504). Systemen met aangepaste kernels die ouder zijn dan 2.6.37 of op basis van RHEL kernels die ouder zijn dan 2.6.32-504 moet ingesteld Hallo opstarten parameter `numa=off` op Hallo kernel opdrachtregelprogramma in grub.conf. Zie voor meer informatie Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Configureer een partitie van de wisseling niet op Hallo OS-schijf. Hallo Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.  Meer informatie hierover vindt u in onderstaande Hallo stappen.
* Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.

### <a name="installing-kernel-modules-without-hyper-v"></a>Kernelmodules zonder Hyper-V installeren
Azure wordt uitgevoerd op Hallo Hyper-V-hypervisor, dus Linux vereist dat bepaalde kernelmodules zijn geïnstalleerd in de volgorde toorun in Azure. Als u een virtuele machine die is gemaakt buiten de Hyper-V hebt, Hallo Linux-installatieprogramma's kunnen niet Hallo stuurprogramma's voor Hyper-V in opnemen Hallo initiële ramdisk (initrd of initramfs) tenzij er wordt gedetecteerd dat deze wordt uitgevoerd een een Hyper-V-omgeving. Wanneer u een andere virtualisatie systeem (dat wil zeggen Virtualbox, KVM, enz.) tooprepare uw Linux-installatiekopie, moet u mogelijk toorebuild hello initrd tooensure ten minste Hallo `hv_vmbus` en `hv_storvsc` kernelmodules zijn beschikbaar op de eerste ramdisk Hallo.  Dit is een bekend probleem ten minste op systemen die op basis van Hallo upstream Red Hat distributie.

Hallo-mechanisme voor het opnieuw opbouwen Hallo initrd of initramfs-installatiekopie kan variëren afhankelijk van Hallo distributie. Raadpleeg de documentatie bij uw distributiepunt of ondersteuning voor de juiste procedure Hallo.  Hier volgt een voorbeeld van hoe toorebuild initrd met Hallo Hallo `mkinitrd` hulpprogramma:

Eerste back-up Hallo bestaande initrd installatiekopie:

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

Vervolgens opnieuw opbouwen Hallo initrd Hello `hv_vmbus` en `hv_storvsc` kernelmodules:

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a>VHD's vergroten of verkleinen
VHD-installatiekopieën in Azure, moeten een virtuele grootte uitgelijnd too1MB hebben.  VHD's die zijn gemaakt met behulp van Hyper-V moeten normaal gesproken al goed worden uitgelijnd.  Als Hallo VHD is niet correct wordt uitgelijnd vervolgens er een fout bericht vergelijkbaar toohello volgen verschijnt wanneer u toocreate probeert een *installatiekopie* van uw VHD:

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

tooremedy dit kunt u de grootte van virtuele machine met behulp van Hallo Hyper-V Manager-console of Hallo Hallo [formaat VHD](http://technet.microsoft.com/library/hh848535.aspx) Powershell-cmdlet.  Als u bent niet wordt uitgevoerd in een Windows-omgeving is het aanbevolen toouse qemu img tooconvert (indien nodig) en formaat Hallo VHD.

> [!NOTE]
> Er is een bekend probleem in qemu img versies > = 2.2.1 die in een onjuiste indeling VHD resulteert. Hallo-probleem is verholpen in QEMU 2.6. Het verdient aanbeveling toouse qemu-img 2.2.0 of kleine of update too2.6 of hoger. Verwijzing: https://bugs.launchpad.net/qemu/+bug/1490611.
> 
> 

1. VHD rechtstreeks met hulpprogramma's zoals vergroten of verkleinen Hallo `qemu-img` of `vbox-manage` kan leiden tot een opgestart VHD.  Daarom wordt het aanbevolen toofirst converteren Hallo VHD tooa ONBEWERKTE schijfimage.  Als Hallo VM-installatiekopie al als ONBEWERKTE schijfimage (Hallo standaard voor bepaalde Hypervisors zoals KVM gemaakt is) kunt u deze stap overslaan:
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. Berekenen Hallo vereiste grootte van Hallo schijf installatiekopie tooensure die virtuele grootte Hallo uitgelijnde too1MB is.  Hallo bash-shell-script volgen kan u helpen bij dit.  Hallo-script gebruikt '`qemu-img info`' toodetermine virtuele grootte van de installatiekopie van een schijf Hallo Hallo en berekent vervolgens Hallo grootte toohello volgende 1 MB:
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. Grootte van onbewerkte Hallo-schijf met behulp van $rounded_size zoals in Hallo hierboven script wijzigen:
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. Converteer Hallo ONBEWERKTE schijf back tooa vaste grootte VHD:
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   Of, met qemu versie **2.6 +** omvatten Hallo `force_size` optie:

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a>Linux-Kernel-vereisten
Hallo Linux Integration Services (LIS) stuurprogramma's voor Hyper-V en Azure worden aangeleverd rechtstreeks toohello upstream Linux kernel. Groot aantal distributies met een recente versie van Linux kernel (dat wil zeggen 3.x) al deze stuurprogramma's beschikbaar zijn, of anders backported versies van deze stuurprogramma's voorzien van hun kernels.  Deze stuurprogramma's worden voortdurend wordt bijgewerkt in Hallo upstream-kernel met nieuwe oplossingen en functies, indien mogelijk het wordt daarom toorun aanbevolen een [distributie goedgekeurde](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) die deze oplossingen en -updates zal bevatten.

Als u een variant van de Red Hat Enterprise Linux-versies uitvoert **6.0 6.3**, moet u tooinstall Hallo nieuwste LIS stuurprogramma's voor Hyper-V. Hallo-stuurprogramma's kunnen worden gevonden [op deze locatie](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409). Vanaf RHEL **6.4 +** (en afgeleiden) Hallo LIS stuurprogramma's zijn al opgenomen in de kernel Hallo en dus geen aanvullende installatie-pakketten zijn benodigde toorun deze systemen op Azure.

Als u een aangepaste kernel is vereist, is het aanbevolen toouse een meer recente kernelversie (dat wil zeggen **3.8 +**). Voor deze distributies of leveranciers die hun eigen kernel onderhouden, worden sommige inspanning vereist tooregularly backport Hallo LIS stuurprogramma's uit Hallo upstream kernel tooyour aangepaste kernel.  Zelfs als u al een relatief recente kernelversie wordt uitgevoerd, is het raadzaam tookeep bijhouden van een upstream-correcties in Hallo LIS stuurprogramma's en backport die indien nodig. Hallo-locatie van de bronbestanden van Hallo LIS stuurprogramma is beschikbaar in Hallo [instaan](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) bestand in Hallo Linux kernel bronstructuur:

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

Bij een zeer minimale Hallo afwezigheid van de volgende patches Hallo hebben bekend toocause problemen op Azure en zodat deze moeten worden opgenomen in de kernel Hallo. Deze lijst is geen volledig of voltooid voor alle verdelingen:

* [ata_piix: schijven toohello Hyper-V-stuurprogramma's standaard uitgesteld](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [storvsc: Account voor de pakketten in transit in Hallo opnieuw instellen van pad](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [storvsc: informatie over het gebruik van WRITE_SAME voorkomen](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [storvsc: dezelfde schrijven uitschakelen voor RAID en stuurprogramma's voor netwerkadapters virtuele host](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [storvsc: NULL-aanwijzer fix verwijzing](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [storvsc: ring buffer fouten kunnen leiden tot i/o-blokkeren](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [scsi_sysfs: beschermen tegen een dubbele uitvoering van __scsi_remove_device](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a>Hello Azure Linux Agent
Hallo [Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) is vereist tooproperly een Linux-machine inrichten in Azure. U kunt de nieuwste versie hello, problemen met het bestand of pull-aanvragen op Hallo verzenden [Linux Agent GitHub-repo-](https://github.com/Azure/WALinuxAgent).

* Hallo Linux-agent is vrijgegeven onder licentie Hallo Apache 2.0. Groot aantal distributies al Geef RPM of deb pakketten voor Hallo-agent, en dus in sommige gevallen dit kan worden geïnstalleerd en bijgewerkt met weinig moeite.
* Hello Azure Linux Agent vereist Python v2.6 +.
* Hallo-agent ook vereist Hallo python pyasn1 module. De meeste distributies biedt dit als een afzonderlijk pakket dat kan worden geïnstalleerd.
* In sommige gevallen hello Azure Linux Agent mogelijk niet compatibel met NetworkManager. Veel van Hallo RPM/Deb pakketten geleverd door distributies NetworkManager configureren als een conflict toohello waagent-pakket en dus verwijdert NetworkManager wanneer u Hallo Linux agentpakket installeert.

## <a name="general-linux-system-requirements"></a>Linux-systeem voor algemene vereisten

* Hallo kernel opstarten regel in GRUB of GRUB2 tooinclude Hallo volgende parameters wijzigen. Hiermee zorgt u ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen:
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    Hiermee zorgt u ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.
  
    Bovendien toohello hierboven, het is raadzaam te*verwijderen* Hallo volgende parameters als deze bestaan:
  
        rhgb quiet crashkernel=auto
  
    Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort. Hallo `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter verminderen Hallo en de hoeveelheid beschikbaar geheugen in Hallo VM 128 MB of meer, die mogelijk problemen op Hallo kleinere VM opmerking.

* Hello Azure Linux Agent installeren
  
    Hello Azure Linux Agent is vereist voor het inrichten van een Linux-installatiekopie in Azure.  Groot aantal distributies bieden Hallo agent als een pakket RPM of Deb (Hallo pakket heet doorgaans 'WALinuxAgent' of 'walinuxagent').  Hallo agent kunt ook handmatig worden geïnstalleerd door de stappen te volgen Hallo in Hallo [Linux Agent handleiding](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

* Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.  Dit is meestal Hallo standaard.

* Maak geen wisselruimte op Hallo besturingssysteemschijf
  
    Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren. Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is. Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* Voer Hallo opdrachten toodeprovision Hallo virtuele machine na een laatste stap:
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > Op Virtualbox mogelijk ziet u volgende fout nadat Hallo ' waagent-force - deprovision': `[Errno 5] Input/output error`. Dit foutbericht is niet kritiek en kan worden genegeerd.
  > 
  > 

* U wordt vervolgens tooshut omlaag Hallo virtuele machine nodig hebt en Hallo VHD tooAzure uploaden.

