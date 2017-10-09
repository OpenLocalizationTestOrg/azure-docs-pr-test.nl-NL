---
title: aaaAzure Linux VM's en Azure Storage | Microsoft Docs
description: Beschrijving van Azure Standard en Premium-opslag en zowel beheerde als onbeheerde schijven met Linux virtuele machines.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: d364c69e-0bd1-4f80-9838-bbc0a95af48c
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 2/7/2017
ms.author: rasquill
ms.openlocfilehash: d34441698a4e59721847685099e5fb3aa378c597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-storage"></a>Azure- en Linux-VM-opslag
Azure-opslag is Hallo cloud opslagoplossing voor moderne toepassingen die afhankelijk van duurzaamheid, beschikbaarheid en schaalbaarheid toomeet Hallo behoeften van klanten zijn.  In aanvulling toomaking het mogelijk dat ontwikkelaars toobuild grootschalige toepassingen toosupport nieuwe scenario's, Azure Storage biedt ook Hallo opslagbasis voor Azure Virtual Machines.

## <a name="managed-disks"></a>Beheerde schijven

Virtuele machines in Azure zijn nu beschikbaar via [Azure beheerd schijven](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), waardoor u toocreate uw virtuele machines zonder te maken of beheren van een [Azure Storage-accounts](../../storage/common/storage-introduction.md) zelf. U opgeven of u wilt dat Premium of Standard-opslag- en hoe groot Hallo schijf worden moeten en Azure Hallo VM-schijven voor u maakt. Virtuele machines met beheerd schijven hebben veel belangrijke functies, waaronder:

- Ondersteuning voor automatische schaalbaarheid. Azure Hallo schijven maakt en beheert Hallo onderliggende opslag toosupport up too10, 000 schijven per abonnement.
- Hogere betrouwbaarheid met Beschikbaarheidssets. Azure zorgt ervoor dat VM-schijven van elkaar geïsoleerd in Beschikbaarheidssets automatisch worden.
- Verbeterde toegangsbeheer. Beheerde schijven beschikbaar stellen tal van bewerkingen die worden beheerd door [gebaseerd toegangsbeheer (RBAC)](../../active-directory/role-based-access-control-what-is.md).

Prijzen voor schijven beheerd is anders dan voor dat niet-beheerde schijven. Zie voor die informatie [prijzen en facturering voor schijven beheerd](../windows/managed-disks-overview.md#pricing-and-billing).

U kunt bestaande virtuele machines die gebruikmaken van niet-beheerde schijven toouse beheerd schijven met converteren [az vm converteren](/cli/azure/vm#convert). Zie voor meer informatie [hoe tooconvert een Linux-VM uit niet-beheerde schijven tooAzure beheerd schijven](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). U kunt een niet-beheerde schijf kan niet converteren naar een beheerde schijf als niet-beheerde Hallo-schijf in een opslagaccount dat is is, of op elk gewenst moment is, versleuteld met [Azure Storage Service versleuteling (SSE)](../../storage/common/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hallo stappen detail hoe tootooconvert zonder begeleiding schijven die zijn of waren, in een versleutelde storage-account te volgen:

- Hallo virtuele harde schijf (VHD) kopiëren met [az storage-blob kopiëren start](/cli/azure/storage/blob/copy#start) tooa storage-account nooit voor Azure Storage-Service: versleuteling is ingeschakeld.
- Maak een VM die gebruikmaakt van beheerde schijven en die VHD-bestand opgeven tijdens het maken van met [az vm maken](/cli/azure/vm#create), of
- Koppel Hallo gekopieerd VHD met [az vm schijf koppelen](/cli/azure/vm/disk#attach) tooa met virtuele machine met schijven die worden beheerd.


## <a name="azure-storage-standard-and-premium"></a>Azure-opslag: Standaard- en Premium
Virtuele machines in Azure--of schijven beheerd of onbeheerd--kunnen gebaseerd zijn op de opslagschijven standard of premium-opslag-schijven. Wanneer u de portal toochoose Hallo uw virtuele machine moet u een vervolgkeuzelijst op Hallo schakelen **basisbeginselen** scherm tooview standard en premium-schijven. Wanneer uitgeschakeld tooSSD, alleen premium-opslag zoals ingeschakelde VM's worden weergegeven, alle back-up SSD-stations.  Wanneer virtuele machines ondersteund door de schijfstations draait standaard opslag is ingeschakeld, uitgeschakeld tooHDD worden weergegeven, samen met de premium-opslag ondersteund door SSD virtuele machines.

Bij het maken van een virtuele machine van Hallo `azure-cli` kunt u bij het kiezen van de VM-grootte Hallo via Hallo kiezen tussen standard en premium `-z` of `--vm-size` cli vlag.

## <a name="creating-a-vm-with-a-managed-disk"></a>Maken van een virtuele machine met een beheerde schijf

Hallo volgende voorbeeld vereist hello Azure CLI 2.0, die u kunt [installeren hier](/cli/azure/install-azure-cli).

Maak eerst een resource groep toomanage Hallo resources met [az groep maken](/cli/azure/group#create):

```azurecli
az group create --location westus --name myResourceGroup
```

Nu maken met virtuele machine Hallo [az vm maken](/cli/azure/vm#create). Geef een unieke `--public-ip-address-dns-name` argument, als `mypublicdns` waarschijnlijk wordt genomen.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns
```

Hallo vorige voorbeeld maakt een virtuele machine met een beheerde schijf in een Standard-opslagaccount. toouse een Premium storage-account toevoegen Hallo `--storage-sku Premium_LRS` argument, zoals Hallo voorbeeld te volgen:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns \
    --storage-sku Premium_LRS
```

## <a name="standard-storage"></a>Standard Storage
Azure Standard-opslag is Hallo standaardtype opslag.  Standard-opslag is terwijl u nog steeds zodat rendabel.  

## <a name="premium-storage"></a>Premium Storage
Azure Premium-opslag biedt ondersteuning voor hoge prestaties, lage latentie schijven voor virtuele machines met I/O-intensieve werkbelastingen. Virtuele machine (VM)-schijven die gebruikmaken van Premium-opslag opslaan gegevens op Solid-State stations (SSD's). U kunt migreren van uw toepassing VM schijven tooAzure Premium-opslag tootake profiteren van Hallo snelheid en prestaties van deze schijven.

Premium-opslag-functies:

* Premium-opslag-schijven: Azure Premium Storage ondersteunt VM-schijven die aangesloten tooDS, DSv2 of Azure Virtual machines GS-serie worden kunnen.
* Premium-pagina-Blob: Gebruikte toohold permanente schijven voor Azure Virtual Machines (VM's) voor pagina-Blobs van het Azure biedt ondersteuning voor Premium-opslag.
* Premium lokaal redundante opslag: Een Premium Storage-account alleen lokaal redundante opslag (LRS) als de replicatieoptie Hallo ondersteunt en bewaard drie kopieën van Hallo gegevens in één regio.
* [Premium-opslag](../../storage/common/storage-premium-storage.md)

## <a name="premium-storage-supported-vms"></a>Premium-opslag ondersteund virtuele machines
Premium-opslag ondersteunt DS-serie, DSv2-serie GS-serie en Fs-serie Azure Virtual Machines (VM's). Standaard- en Premium-opslag-schijven kunt u met Premium-opslag van virtuele machines worden ondersteund. Maar u Premium-opslag schijven niet gebruiken met VM-reeks niet compatibel Premium-opslag zijn.

Hieronder vindt u Hallo Linux-distributies die we gevalideerd met Premium-opslag.

| Distributie | Versie | Ondersteunde Kernel |
| --- | --- | --- |
| Ubuntu |12.04 |3.2.0-75.110+ |
| Ubuntu |14.04 |3.13.0-44.73+ |
| Debian |7.x, 8.x |3.16.7-ckt4-1+ |
| SLES |SLES 12 |3.12.36-38.1+ |
| SLES |SLES 11 SP4 |3.0.101-0.63.1+ |
| CoreOS |584.0.0+ |3.18.4+ |
| Centos |6.5, 6.6, 6.7, 7.0, 7.1 |3.10.0-229.1.2.el7+ |
| RHEL |6.8+, 7.2+ | |

## <a name="azure-file-storage"></a>Azure File storage
Azure File storage biedt bestandsshares in de cloud van Hallo Hallo standaard SMB-protocol gebruiken. Met Azure-bestanden, kunt u zakelijke toepassingen die afhankelijk van het bestand servers tooAzure zijn migreren. Toepassingen die worden uitgevoerd in Azure kunnen eenvoudig bestandsshares koppelen vanuit Azure virtuele machines met Linux. En met Hallo meest recente versie van File storage, kunt u een bestandsshare ook koppelen vanuit een on-premises toepassing die ondersteuning biedt voor SMB 3.0.  Omdat bestandsshares SMB-shares zijn, kunt u ze openen via standaard bestandssysteem API's.

Opslag van bestanden is gebouwd op Hallo dezelfde technologie als Blob, Table en Queue storage, dus File storage Hallo beschikbaarheid, duurzaamheid, schaalbaarheid en geografische redundantie die biedt is ingebouwd in hello Azure storage-platform. Zie voor meer informatie over prestatiedoelen van File storage en limieten voor Azure Storage Scalability and Performance Targets.

* [Hoe toouse Azure File storage met Linux](../../storage/files/storage-how-to-use-files-linux.md)

## <a name="hot-storage"></a>Hot Storage
Hello Azure hot storage-laag is geoptimaliseerd voor het opslaan van gegevens die regelmatig worden geopend.  Hot storage is Hallo standaard opslagtype voor blob-stores.

## <a name="cool-storage"></a>Cool Storage
Hello Azure cool storage-laag is geoptimaliseerd voor het opslaan van gegevens die niet regelmatig worden geopend en een lange levensduur hebben. Gebruiksvoorbeelden voor cool storage zijn back-ups van media-inhoud, wetenschappelijke gegevens, naleving en archivering van gegevens. Alle gegevens die worden zelden geopend is in het algemeen een perfecte keuze voor de cool storage.

|  | Opslaglaag voor 'hot' blobs | Opslaglaag voor 'cool' blobs |
|:--- |:---:|:---:|
| Beschikbaarheid |99,9% |99% |
| Beschikbaarheid (RA-GRS-leesbewerkingen) |99,99% |99,9% |
| Gebruikskosten |Hogere opslagkosten |Lagere opslagkosten |
| Lagere toegang |Hogere toegang | |
| en transactiekosten |en transactiekosten | |

## <a name="redundancy"></a>Redundantie
Hallo-gegevens in uw Microsoft Azure storage-account altijd is gerepliceerd tooensure duurzaamheid en hoge beschikbaarheid, voldoen aan de SERVICEOVEREENKOMST van Azure Storage Hallo zelfs in Hallo vlak van tijdelijke hardwarefouten.

Wanneer u een opslagaccount maakt, moet u een Hallo volgende replicatieopties selecteren:

* Lokaal redundante opslag (LRS)
* Zone-redundante opslag (ZRS)
* Geografisch redundante opslag (GRS)
* Geografisch redundante opslag met leestoegang (RA-GRS)

### <a name="locally-redundant-storage"></a>Lokaal redundante opslag
Lokaal redundante opslag (LRS) repliceert uw gegevens binnen Hallo regio waarin u uw opslagaccount hebt gemaakt. elk verzoek op basis van gegevens in uw opslagaccount toomaximize duurzaamheid driemaal gerepliceerd. Deze drie replica's elke zich bevinden in domeinen met afzonderlijke fouten en upgradedomeinen.  Een aanvraag retourneert is alleen nadat deze geschreven tooall drie replica's is.

### <a name="zone-redundant-storage"></a>Zone-redundante opslag
Zone-redundante opslag (ZRS) uw gegevens gerepliceerd tussen twee toothree faciliteiten in één regio of tussen twee regio's, biedt een hogere duurzaamheid dan LRS. Als uw storage-account ZRS is ingeschakeld heeft, zijn uw gegevens is duurzame zelfs in Hallo geval van storing optreedt in een van de Hallo faciliteiten.

### <a name="geo-redundant-storage"></a>Geografisch redundante opslag
Geografisch redundante opslag (GRS) uw gegevens tooa secundaire regio die honderden mijl weg Hallo primaire regio worden gerepliceerd. Als uw storage-account GRS ingeschakeld heeft, zijn uw gegevens is duurzame zelfs in Hallo geval van een volledige regionale uitval of een noodsituatie in welke Hallo primaire regio kan niet worden hersteld.

### <a name="read-access-geo-redundant-storage"></a>Geografisch redundante opslag met leestoegang
Geografisch redundante opslag met leestoegang (RA-GRS) maximaliseert de beschikbaarheid voor uw opslagaccount alleen-lezentoegang toohello door gegevens te verstrekken op de secundaire locatie hello, Daarnaast toohello replicatie tussen twee regio's worden geleverd door GRS. In Hallo gebeurtenis dat gegevens niet beschikbaar in de primaire regio hello, kan uw toepassing gegevens lezen van de secundaire regio Hallo.

Voor een diepgaand in Azure storage redundantie Zie:

* [Azure Storage-replicatie](../../storage/common/storage-redundancy.md)

## <a name="scalability"></a>Schaalbaarheid
Azure Storage is zeer schaalbaar, zodat u kunt opslaan en verwerken van honderden terabytes aan gegevens toosupport Hallo big data scenario's vereist zijn voor wetenschap, financiële analyse en mediatoepassingen. Of u Hallo kleine hoeveelheden gegevens die nodig zijn voor een klein bedrijf website kunt opslaan. Wat u ook nodig, betaalt u alleen voor Hallo gegevens die u opslaat. Momenteel zijn er tientallen biljoenen unieke klantobjecten opgeslagen in Azure Storage. Daarnaast worden er gemiddeld miljoenen aanvragen per seconde verwerkt.

Voor standard-opslag-accounts: een standard-opslagaccount heeft een maximale totale percentage 20.000 IOPS. Hallo totale IOP's voor alle schijven voor uw virtuele machine in een standard-opslagaccount mag niet meer dan deze limiet.

Voor premium storage-accounts: een premium storage-account heeft de maximale totale doorvoersnelheid van 50 Gbps. de totale doorvoer Hallo voor alle VM-schijven, mag niet meer dan deze limiet.

## <a name="availability"></a>Beschikbaarheid
Wordt gegarandeerd dat ten minste 99,99% (99,9% voor statische Toegangslaag) Hallo tijd, we met succes gegevens over het installatieproces aanvragen tooread van leestoegang geografisch redundante opslag (RA-GRS) Accounts wordt, mits pogingen tooread gegevens uit de primaire regio Hallo is mislukt op de secundaire regio hello later opnieuw.

Wordt gegarandeerd dat minimaal 99,9% (99% voor statische Toegangslaag) Hallo tijd, met succes wordt proces tooread gegevens aanvraagt via lokaal redundante opslag (LRS), Zone-redundante opslag (ZRS) en Accounts geografisch redundante opslag (GRS).

Wordt gegarandeerd dat minimaal 99,9% (99% voor statische Toegangslaag) Hallo tijd, met succes wordt proces aanvraagt toowrite gegevens tooLocally redundante opslag (LRS), Zone redundante opslag (ZRS), en geografisch redundante opslag (GRS) Accounts en leestoegang geografisch Redundant Opslagaccounts (RA-GRS).

* [Azure SLA voor opslag](https://azure.microsoft.com/support/legal/sla/storage/v1_1/)

## <a name="regions"></a>Regio's
Azure is algemeen beschikbaar in 30 regio's Hallo wereld en plannen voor 4 extra gebieden is aangekondigd. Geografische uitbreiding is een prioriteit voor Azure omdat onze klanten tooachieve betere prestaties kunnen en het ondersteunt hun vereisten en voorkeuren met betrekking tot de locatie van gegevens.  De meest recente regio toolaunch azures is in Duitsland.

Hallo Microsoft Cloud Duitsland biedt een gedifferentieerde optie toohello Microsoft Cloud-services al beschikbaar voor Europa, verbeterde mogelijkheden voor innovatie en groei voor maximaal gereglementeerde partners en klanten in Duitsland maken Hallo Europese Unie en Hallo Europese vrije handel koppeling (EFTA).

Klantgegevens in deze nieuwe datacenters, in Magdeburg en Frankfurt, wordt onder het Hallo-beheer van een beheerder gegevens International T-systemen, een onafhankelijke Duitse bedrijfsgegevens en vestiging van Deutsche Telekom beheerd. Commerciële van Microsoft-cloudservices in deze datacenters tooGerman gegevens verwerken voorschriften voldoen en klanten bieden aanvullende opties van hoe en waar gegevens worden verwerkt.

* [Azure-regio's toewijzen](https://azure.microsoft.com/regions/)

## <a name="security"></a>Beveiliging
Azure Storage biedt een uitgebreide reeks beveiligingsmogelijkheden die samen ontwikkelaars kunnen toobuild beveiligde toepassingen. Hallo storage-account zelf kan worden beveiligd met op rollen gebaseerde toegangsbeheer en Azure Active Directory. Gegevens kunnen worden beveiligd tijdens de overdracht tussen een toepassing en Azure met behulp van versleuteling van de Client-Side-, HTTPS- of SMB 3.0. Gegevens kunnen worden ingesteld op toobe automatisch versleuteld wanneer geschreven tooAzure opslag met behulp van versleuteling voor opslag-Service (SSE). Besturingssysteem en gegevensschijven die worden gebruikt door virtuele machines kunnen worden ingesteld als toobe versleuteld met Azure Disk Encryption. Gedelegeerde toegang toohello gegevensobjecten in Azure Storage kunnen worden verleend met behulp van handtekeningen voor gedeelde toegang.

### <a name="management-plane-security"></a>Beveiliging van de vlak Management
Hallo management vlak bestaat uit Hallo gebruikte resources toomanage uw storage-account. In deze sectie bespreken we hello Azure Resource Manager-implementatiemodel en hoe toouse op rollen gebaseerde toegangsbeheer (RBAC) toocontrol toegang krijgen tot tooyour storage-accounts. We zullen ook hebben over het beheren van uw toegangscodes voor opslag en hoe tooregenerate ze.

### <a name="data-plane-security"></a>Beveiliging van gegevens vlak
In deze sectie zullen we toegang toe te staan toohello actuele gegevensobjecten in uw opslagaccount, zoals blobs, bestanden, wachtrijen en tabellen, met behulp van handtekeningen voor gedeelde toegang en toegangsbeleid opgeslagen. Zowel serviceniveau-SAS en account niveau SAS wordt uitgelegd. Ook bekijken we hoe toolimit toegang krijgen tot tooa specifiek IP-adres (of een bereik van IP-adressen), hoe toolimit Hallo protocol tooHTTPS gebruikt en hoe toorevoke een Shared Access Signature zonder te wachten op het tooexpire.

## <a name="encryption-in-transit"></a>Codering in Transit
Deze sectie wordt beschreven hoe u gegevens toosecure wanneer u het overbrengen van of naar Azure Storage. Bespreken we Hallo aanbevolen gebruik van HTTPS en Hallo versleuteling door SMB 3.0 gebruikt voor de Azure-bestandsshares. Er wordt ook rekening houden met kijken clientzijde versleuteling, waarmee u tooencrypt Hallo gegevens voordat deze worden overgedragen naar de opslag in een clienttoepassing en toodecrypt Hallo gegevens nadat deze zijn overgebracht buiten opslag.

## <a name="encryption-at-rest"></a>Codering in rust
We zullen hebben over opslag Service versleuteling (SSE) en hoe u kunt inschakelen voor een opslagaccount, wat resulteert in uw blok-blobs, pagina-blobs en toevoeg-blobs worden automatisch versleuteld wanneer geschreven tooAzure opslag. Ook kijken we hoe u Azure Disk Encryption gebruiken en verkennen Hallo basic verschillen en aanvragen van schijfversleuteling versus SSE ten opzichte van de Client-Side-versleuteling. Kort kijken we FIPS-naleving voor VS Computers van de overheid.

* [Azure Storage-beveiligingshandleiding](../../storage/common/storage-security-guide.md)

## <a name="temporary-disk"></a>Tijdelijke schijf
Elke virtuele machine bevat een tijdelijke schijf. Hallo tijdelijke schijf opslag op korte termijn voor toepassingen en processen en gegevens van de beoogde tooonly opslaan zoals pagina of het swap-bestanden is. Gegevens op de tijdelijke schijf Hallo zijn mogelijk verloren gegaan tijdens een [onderhoud](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) of wanneer u [opnieuw implementeren van een virtuele machine](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Tijdens een standaard herstart Hallo VM moet Hallo-gegevens op de tijdelijke schijf Hallo handhaven.

Op Linux virtuele machines, Hallo schijf wordt meestal **/dev/sdb** en is geformatteerd en gekoppeld, te**mnt** door hello Azure Linux Agent. Hallo-grootte van de tijdelijke schijf Hallo varieert, afhankelijk van de grootte van de Hallo van Hallo virtuele machine. Zie voor meer informatie [grootten voor virtuele Linux-machines](sizes.md).

Zie voor meer informatie over hoe Azure gebruikt voor de tijdelijke schijf Hallo [begrijpen Hallo tijdelijke station op Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="cost-savings"></a>Kostenbesparingen
* [Opslagkosten](https://azure.microsoft.com/pricing/details/storage/)
* [Opslag kosten Rekenmachine](https://azure.microsoft.com/pricing/calculator/?service=storage)

## <a name="storage-limits"></a>Opslaglimieten
* [Service opslaglimieten](../../azure-subscription-service-limits.md#storage-limits)
