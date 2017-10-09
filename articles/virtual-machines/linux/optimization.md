---
title: aaaOptimize uw Linux-VM op Azure | Microsoft Docs
description: Meer informatie over een aantal tips toomake voor optimalisatie zeker dat u uw Linux-VM voor optimale prestaties in Azure hebt ingesteld
keywords: virtuele Linux-machine, linux virtuele machine, ubuntu virtuele machine
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 8baa30c8-d40e-41ac-93d0-74e96fe18d4c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 89a9ac022928a2801a9a15e1c172340352745354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a>Uw Linux VM optimaliseren voor Azure
Maken van virtuele Linux-machine (VM) is eenvoudig toodo Hallo vanaf de opdrachtregel of in Hallo-portal. Deze zelfstudie leert u hoe tooensure u dit hebt ingesteld toooptimize de prestaties op Hallo Microsoft Azure-platform. In dit onderwerp maakt gebruik van een virtuele Ubuntu Server-machine, maar u kunt ook maken Linux virtuele machine met [uw eigen installatiekopieën die u als sjabloon](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="prerequisites"></a>Vereisten
In dit onderwerp wordt ervan uitgegaan dat u hebt al een werkende Azure-abonnement ([gratis proefversie te registreren](https://azure.microsoft.com/pricing/free-trial/)) en u hebt al een virtuele machine ingericht in uw Azure-abonnement. Zorg ervoor dat er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in tooyour Azure-abonnement met [az aanmelding](/cli/azure/#login) voordat u [een virtuele machine maken](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-os-disk"></a>Azure Besturingssysteemschijf
Wanneer u een Linux-VM in Azure maakt, heeft deze twee schijven zijn gekoppeld. **/ dev/sda** staat voor de schijf OS **/dev/sdb** staat voor de tijdelijke schijf.  Gebruik niet de belangrijkste besturingssysteemschijf hello (**/dev/sda**) voor alles behalve Hallo-besturingssysteem die is geoptimaliseerd voor snelle VM-opstarten en biedt geen goede prestaties voor uw werkbelastingen. Gewenste tooattach een of meer schijven tooyour VM tooget permanente en geoptimaliseerde opslag voor uw gegevens. 

## <a name="adding-disks-for-size-and-performance-targets"></a>Het toevoegen van schijven voor grootte- en prestatiedoelen
Op basis van VM-grootte hello, kunt u koppelen van too16 extra schijven op een A-serie, 32 schijven op een D-reeks en 64 schijven op een machine G-serie - elk up too1 TB groot. U kunt extra schijven toevoegen naar behoefte per uw ruimte en de vereisten voor IOps. Elke schijf heeft een prestatiedoel van 500 IOps voor Standard-opslag en omhoog in too5000 IOP's per schijf voor Premium-opslag.  Zie voor meer informatie over Premium-opslag schijven [Premium-opslag: krachtige opslag voor Azure Virtual machines](../../storage/common/storage-premium-storage.md)

tooachieve Hallo hoogste IOps op schijven met Premium-opslag waar de cache-instellingen zijn ingesteld tooeither **ReadOnly** of **geen**, moet u uitschakelen **barrières** terwijl koppeling van Hallo bestandssysteem in Linux. U hoeft niet barrières omdat Hallo schrijft tooPremium opslag back-schijven zijn duurzame voor deze cache-instellingen.

* Als u **reiserFS**, uitschakelen barrières met Hallo koppelpunt optie `barrier=none` (gebruikt voor het inschakelen van barrières `barrier=flush`)
* Als u **ext3/ext4**, uitschakelen barrières met Hallo koppelpunt optie `barrier=0` (gebruikt voor het inschakelen van barrières `barrier=1`)
* Als u **XFS**, uitschakelen barrières met Hallo koppelpunt optie `nobarrier` (gebruik Hallo-optie voor het inschakelen van barrières `barrier`)

## <a name="unmanaged-storage-account-considerations"></a>Aandachtspunten voor gebruikersaccounts onbeheerde opslag
Hallo standaardactie wanneer u een virtuele machine met Azure CLI 2.0 Hallo maakt is toouse Azure beheerd schijven.  Deze schijven worden afgehandeld door hello Azure-platform en hoeven niet alle toostore voorbereidings- of locatie ze.  Niet-beheerde schijven vereisen een opslagaccount en hebben enkele aanvullende prestatie-overwegingen.  Zie voor meer informatie over beheerde schijven [overzicht Azure Managed Disks](../windows/managed-disks-overview.md).  Hallo volgende sectie worden prestatie-overwegingen wanneer u het niet-beheerde schijven gebruikt.  Hallo opnieuw, standaard en aanbevolen opslagoplossing is toouse beheerd schijven.

Als u een virtuele machine met niet-beheerde schijven maken, controleert u of u Koppel de schijven van de storage-accounts die zich bevindt in Hallo dezelfde regio bevinden als uw VM tooensure nabijheid en netwerklatentie minimaliseren.  Elk Standard-opslag-account is een maximum van 20 k IOps en een capaciteit van de grootte van 500 TB.  Deze limiet werkt tooapproximately 40 intensief gebruikt schijven, inclusief Hallo OS-schijf en eventuele gegevensschijven die u maakt. Er is geen limiet voor de maximale IOps voor Premium Storage-accounts, maar er is een limiet van 32 TB. 

Wanneer het omgaan met een hoge IOps werkbelastingen en u hebt ervoor gekozen Standard-opslag voor uw schijven, moet u mogelijk toosplit Hallo schijven over meerdere storage accounts toomake zeker dat u hebt geen Hallo 20.000 IOps voor Standard-opslag-accounts beperken bereikt. Uw virtuele machine mag een combinatie van schijven uit via verschillende storage-accounts en storage-account typen tooachieve de optimale configuratie.
 

## <a name="your-vm-temporary-drive"></a>De VM tijdelijke schijf
Wanneer u een virtuele machine, maakt Azure biedt standaard u met een besturingssysteemschijf (**/dev/sda**) en een tijdelijke schijf (**/dev/sdb**).  Alle aanvullende schijven u, weergeven als toevoegen **/dev/sdc**, **/dev/sdd**, **/dev/sde** enzovoort. Alle gegevens op de tijdelijke schijf (**/dev/sdb**) is niet duurzame, en kunnen verloren gaan als specifieke gebeurtenissen, zoals VM-grootte, opnieuw installeren, of onderhoud zorgt ervoor uw virtuele machine opnieuw wordt opgestart dat.  Hallo grootte en het type van de tijdelijke schijf is gerelateerde toohello VM-grootte u hebt gekozen tijdens de implementatie. Alle Hallo premium grootte van virtuele machines (DS, G en DS_V2-serie) Hallo tijdelijke station worden ondersteund door een lokale SSD voor extra prestaties van up too48k IOps. 

## <a name="linux-swap-file"></a>Wisselbestand van Linux
Als uw Azure VM van een installatiekopie van een Ubuntu of virtuele CoreOS is, kunt u CustomData toosend toocloud initialisatie in een cloud-configuratie kunt gebruiken. Als u [geüpload een aangepaste installatiekopie van Linux](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) die gebruikmaakt van cloud-init, u ook configureren met behulp van cloud-init swap-partities.

Ubuntu Cloud afbeeldingen, moet u cloud-init tooconfigure Hallo wisselen partitie. Zie voor meer informatie [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

Voor installatiekopieën zonder ondersteuning voor cloud-init zijn VM-installatiekopieën die zijn geïmplementeerd vanaf hello Azure Marketplace een geïntegreerd met Hallo OS VM Linux-Agent. Deze agent kan Hallo VM toointeract met verschillende Azure-services. Ervan uitgaande dat u een standaardinstallatiekopie van hello Azure Marketplace hebt geïmplementeerd, moet u toodo configureren hello toocorrectly na van instellingen voor het wisselbestand Linux:

Zoek en wijzigen van twee vermeldingen in Hallo **/etc/waagent.conf** bestand. Ze bepalen Hallo bestaan van een speciale wisselbestand en grootte van het wisselbestand Hallo. Hallo parameters zoekt u toomodify zijn `ResourceDisk.EnableSwap=N` en`ResourceDisk.SwapSizeMB=0` 

Hallo parameters toohello volgende instellingen wijzigen:

* ResourceDisk.EnableSwap=Y
* ResourceDisk.SwapSizeMB={size in MB toomeet uw behoeften} 

Zodra u hebt aangebracht Hallo wijzigen, moet toorestart hello waagent of opnieuw opstarten van uw Linux-VM tooreflect deze wijzigingen.  U weet Hallo wijzigingen zijn uitgevoerd en er is een wisselbestand gemaakt wanneer u Hallo `free` opdracht tooview vrije ruimte. Hallo volgende voorbeeld heeft een wisselbestand van 512MB gemaakt naar aanleiding van Hallo wijzigen **waagent.conf** bestand:

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a>I/o-planning algoritme voor Premium-opslag
Hallo i/o-planning standaardalgoritme is met Hallo 2.6.18 Linux kernel gewijzigd van de Deadline tooCFQ (volledig evenredige queuing algoritme). Er is te verwaarlozen verschil in prestatieverschillen tussen CFQ en de Deadline voor willekeurige toegang i/o-patronen.  Voor op SSD gebaseerd schijven waarbij Hallo schijf-i/o-patroon hoofdzakelijk is sequentiële terug overschakelen toohello Nooperation of Deadline algoritme kunt bereiken betere i/o-prestaties.

### <a name="view-hello-current-io-scheduler"></a>Weergave Hallo huidige i/o-planner
Hallo volgende opdracht gebruiken:  

```bash
cat /sys/block/sda/queue/scheduler
```

Ziet u uitvoer, waarmee wordt aangegeven van de huidige Taakplanner hello te volgen.  

```bash
noop [deadline] cfq
```

### <a name="change-hello-current-device-devsda-of-io-scheduling-algorithm"></a>Huidige Hallo-apparaat (/ dev/sda) van i/o-algoritme planning wijzigen
Hallo volgende opdrachten gebruiken:  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> Toepassen van deze instelling voor **/dev/sda** alleen is niet handig. Ingesteld op alle gegevensschijven waar opeenvolgende i/o zomaar Hallo i/o-patroon.  

U ziet Hallo volgende uitvoer, die aangeeft dat **grub.cfg** met succes is opnieuw opgebouwd en die standaard Hallo scheduler bijgewerkte tooNOOP is.  

```bash
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.13.0-34-generic
Found initrd image: /boot/initrd.img-3.13.0-34-generic
Found linux image: /boot/vmlinuz-3.13.0-32-generic
Found initrd image: /boot/initrd.img-3.13.0-32-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
done
```

Voor Hallo Redhat distributie familie hoeft u alleen Hallo volgende opdracht:   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-tooachieve-higher-iops"></a>Met behulp van Software-RAID tooachieve hogere I / Ops
Als uw werkbelastingen meer IOps vereisen dan één schijf kan bieden, moet u toouse een software-RAID-configuratie van meerdere schijven. Omdat Azure al schijf tolerantie op Hallo lokale fabric laag voert, kunt u Hallo hoogste niveau van de prestaties van een configuratie van RAID-0 striping van bereiken.  Inrichten en schijven te maken in hello Azure-omgeving en koppelt u ze tooyour Linux-VM voordat partitioneren, formatteren en koppelen van stations Hallo.  Meer informatie over het configureren van een software-RAID-instellingen op uw Linux-VM in azure vindt u in Hallo  **[configureren van Software-RAID op Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**  document.

## <a name="next-steps"></a>Volgende stappen
Denk eraan dat als alle optimalisatie discussies, u tooperform tests vóór moet en na elke wijziging toomeasure Hallo botsing hello wijziging heeft.  Optimalisatie wordt stap voor stap processen met verschillende resultaten op verschillende computers in uw omgeving.  Wat werkt voor één configuratie werkt niet voor anderen.

Sommige nuttige koppelingen tooadditional resources: 

* [Premium Storage: opslag met hoge prestaties voor de werkbelasting van virtuele Azure-machines](../../storage/common/storage-premium-storage.md)
* [Gebruikershandleiding voor Azure Linux-Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [MySQL-prestaties op Azure Linux virtuele machines optimaliseren](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configureren van Software-RAID op Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

