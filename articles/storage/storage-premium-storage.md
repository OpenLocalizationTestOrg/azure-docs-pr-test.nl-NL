---
title: Premium-opslag aaaHigh prestaties en Azure schijven die worden beheerd voor virtuele machines | Microsoft Docs
description: Meer informatie over hoge prestaties Premium-opslag- en beheerde schijven voor virtuele Azure-machines. Azure Active Directory-serie, DSv2-serie GS-serie en Fs-serie VMs ondersteuning voor Premium-opslag.
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: ramankum
ms.openlocfilehash: 2474fa75116fe394672fde48520441fa80cf434f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>Premium-opslag voor hoge prestaties en beheerde schijven voor virtuele machines
Azure Premium-opslag biedt ondersteuning voor hoge prestaties, lage latentie schijven voor virtuele machines (VM's) met input/output (I/O)-intensieve werkbelastingen. VM-schijven die gebruikmaken van Premium-opslag opslaan gegevens op de SSD-schijven (SSD's). tootake profiteren van Hallo snelheid en prestaties van schijven met opslagruimte premium, kunt u bestaande VM-schijven tooPremium opslag migreren.

In Azure, kunt u verschillende premium storage schijven tooa VM koppelen. Gebruik van meerdere schijven, biedt uw toepassingen van too256 TB opslagruimte per virtuele machine. Met de Premium-opslag, kunnen uw toepassingen 80.000 i/o-bewerkingen per seconde (IOPS) per virtuele machine en de schijfdoorvoer van een van up too2, 000 megabytes per seconde (MB/s) per VM bereiken. Leesbewerkingen bieden u een zeer lage latenties.

Azure biedt de mogelijkheid Hallo tootruly lift en shift veeleisende zakelijke toepassingen zoals Dynamics AX, Dynamics CRM, Exchange Server, SAP Business Suite en SharePoint-farms toohello cloud met Premium-opslag. U kunt de database van de prestatie-intensieve werkbelastingen uitvoeren in toepassingen zoals SQL Server, Oracle, MongoDB, MySQL en Redis, waarvoor consistent hoge prestaties en lage latentie.

> [!NOTE]
> Voor de beste prestaties voor uw toepassing hello wordt u aangeraden een VM-schijf waarvoor hoge IOPS tooPremium opslag te migreren. Als de schijf niet hoge IOPS vereist, kunt u kosten beperken door deze te houden in standard-Azure-opslag. Standard-opslag worden VM schijfgegevens opgeslagen op de vaste harde schijven (HDD's) in plaats van op SSD's.
> 

Azure biedt twee manieren toocreate premium-opslag-schijven voor virtuele machines:

* **Niet-beheerde schijven**

    de oorspronkelijke methode Hallo is zonder begeleiding toouse schijven. In een niet-beheerde schijf beheert u Hallo storage-accounts is dat u toostore Hallo virtuele harde schijf (VHD)-bestanden die overeenkomen met tooyour VM-schijven. VHD-bestanden worden opgeslagen als pagina-blobs in Azure storage-accounts. 

* **Beheerde schijven**

    Wanneer u de optie [Azure beheerd schijven](storage-managed-disks-overview.md), Azure beheert Hallo storage-accounts die u voor uw VM-schijven gebruikt. U geeft Hallo schijftype (Premium of standaard) en Hallo grootte van Hallo-schijf die u nodig hebt. Azure maakt en beheert de Hallo schijf voor u. U hebt geen tooworry over Hallo schijven plaatsen in meerdere tooensure van de storage-accounts die u voor uw storage-accounts binnen de schaalbaarheidslimieten voor te blijven. Azure verwerkt die voor u.

Het is raadzaam dat u beheerde schijven, tootake profiteren van veel functies kiest.

de slag met Premium-opslag tooget [uw gratis Azure-account maken](https://azure.microsoft.com/pricing/free-trial/). 

Zie voor meer informatie over het migreren van uw bestaande virtuele machines tooPremium opslag [converteren van een virtuele machine van Windows van niet-beheerde schijven toomanaged schijven](../virtual-machines/virtual-machines-windows-convert-unmanaged-to-managed-disks.md) of [een Linux-VM te converteren van niet-beheerde schijven toomanaged schijven](../virtual-machines/linux/convert-unmanaged-to-managed-disks.md).

> [!NOTE]
> Premium-opslag is beschikbaar in de meeste regio's. Voor Hallo lijst met beschikbare regio's, in [Azure-services per regio](https://azure.microsoft.com/regions/#services), bekijkt hello gebieden waarin ondersteund Premium ondersteuning grootte-serie VMs (DS-serie, DSV2-serie GS-serie en virtuele machines Fs-serie) worden ondersteund.
> 

## <a name="features"></a>Functies

Hier volgen enkele Hallo functies van Premium-opslag:

* **Premium-opslag-schijven**

    Premium-opslag ondersteunt het VM-schijven die kunnen worden gekoppeld toospecific grootte-serie virtuele machines. Premium-opslag ondersteunt DS-serie, DSv2-serie GS-serie, Ls-serie en virtuele machines Fs-serie. U hebt de mogelijkheid van zeven schijfgrootten: P4 (32GB), P6 (64GB), P10 (128GB), P20 (512GB), P30 (1024GB), p 40 (2048GB), P50 (4095GB). P4 en P6 schijfgrootten worden alleen nog ondersteund voor schijven die worden beheerd. De grootte van elke schijf heeft zijn eigen prestatiespecificaties. Afhankelijk van uw toepassing, kunt u een of meer schijven tooyour VM koppelen. Hallo-specificaties in nader worden beschreven [Premium-opslag schaalbaarheids- en prestatiedoelen](#scalability-and-performance-targets).

* **Premium-pagina-blobs**

    Premium-opslag biedt ondersteuning voor pagina-blobs. Pagina-blobs toostore permanente, niet-beheerde schijven voor virtuele machines in Premium-opslag gebruiken. Premium-opslag komt niet in tegenstelling tot standaard Azure Storage ondersteunt blok-blobs, toevoeg-blobs, bestanden, tabellen of wachtrijen. Premium-pagina-blobs ondersteunt zes groottes van P10 tooP50 en P60 (8191GiB). Premium P60 pagina-blob is geen ondersteunde toobe gekoppeld als VM-schijven. 

    Een object dat wordt geplaatst in een premium storage-account is een pagina-blob. Hallo-pagina-blob uitlijnen tooone Hallo ingerichte grootten ondersteund. Daarom een premium storage-account is niet bedoeld voor het toobe toostore klein blobs gebruikt.

* **Premium-opslagaccount**

    toostart een premium storage-account voor niet-beheerde schijven u Premium-opslag maken. In Hallo [Azure-portal](https://portal.azure.com), toocreate een premium storage-account kiezen Hallo **Premium** prestatielaag. Selecteer Hallo **lokaal redundante opslag (LRS)** replicatie-optie. U kunt een premium storage-account ook maken door het Instellingstype hello te**Premium_LRS** in een van de volgende locaties Hallo:
    * [REST API voor Storage](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (versie 2014-02-14 of een latere versie)
    * [REST API van Opslagservicebeheer](http://msdn.microsoft.com/library/azure/ee460799.aspx) (versie 2014-10-01 of een latere versie voor Azure klassieke implementaties)
    * [Azure Storage Resource Provider REST-API](https://docs.microsoft.com/rest/api/storagerp) (voor implementaties van Azure Resource Manager)
    * [Azure PowerShell](../powershell-install-configure.md) (versie 0.8.10 of een latere versie)

    toolearn over opslagaccountlimieten premium, Zie [Premium-opslag schaalbaarheids- en prestatiedoelen](#premium-storage-scalability-and-performance-targets).

* **Lokaal redundant Premium-opslag**

    Premium-opslagaccount ondersteunt alleen lokaal redundante opslag als Hallo replicatie-optie. Lokaal redundante opslag houdt drie kopieën van Hallo gegevens in één regio. Voor regionale noodherstel, u moet back-up in een andere regio uw VM-schijven met behulp van [Azure Backup](../backup/backup-introduction-to-azure-backup.md). U moet ook een geografisch redundante opslag (GRS)-account gebruiken als Hallo back-upkluis. 

    Azure maakt gebruik van uw storage-account als een container voor uw niet-beheerde schijven. Wanneer u een Azure Active Directory-serie, DSv2-serie GS-serie, maakt of Fs-serie-VM met niet-beheerde schijven, en u selecteert een premium storage-account, het besturingssysteem en gegevensschijven worden opgeslagen in dit opslagaccount.

## <a name="supported-vms"></a>Ondersteunde virtuele machines
Premium-opslag ondersteunt DS-serie, DSv2-serie GS-serie, Ls-serie en virtuele machines Fs-serie. Met deze VM-typen kunt u schijven standard en premium storage. U niet premium-opslag-schijven gebruiken met VM-reeks die geen Premium-opslag-compatibel.

Zie voor meer informatie over de VM-typen en groottes in Azure voor Windows [Windows VM-grootten](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Zie voor meer informatie over de VM-typen en groottes in Azure voor Linux [Linux VM-grootten](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Dit zijn enkele functies Hallo Hallo DS-serie, DSv2-serie GS-serie Ls-serie en Fs-serie virtuele machines:

* **Cloudservice**

    U kunt virtuele machines DS-serie tooa cloudservice met alleen DS-serie virtuele machines toevoegen. Voeg geen DS-serie VMs tooan bestaande cloudservice met elk type dan DS-serie virtuele machines. U kunt uw bestaande VHD's tooa nieuwe cloudservice met alleen DS-serie virtuele machines migreren. Als u wilt dat toouse hetzelfde virtuele IP-adres voor het nieuwe cloudservice hello, die als host fungeert voor uw virtuele machines van DS-serie gebruik Hallo [gereserveerde IP-adressen](../virtual-network/virtual-networks-instance-level-public-ip.md). Virtuele machines GS-serie kunnen tooan bestaande cloudservice met alleen GS-serie virtuele machines worden toegevoegd.

* **Schijf van besturingssysteem**

    U kunt uw toouse VM voor Premium-opslag instellen premium of een standaardbesturingssysteem worden uitgevoerd-schijf. Voor de beste ervaring hello, wordt u aangeraden de schijf van een besturingssysteem op basis van een Premium-opslag.

* **Gegevensschijven**

    Kunt u premium en standard schijven in Hallo dezelfde VM voor Premium-opslag. Met Premium-opslag kunt u een virtuele machine inrichten en verschillende permanente gegevens schijven toohello VM koppelen. Indien nodig, tooincrease Hallo capaciteit en prestaties van Hallo volume, kunt u stripe over uw schijven.

    > [!NOTE]
    > Als u premium-opslag-gegevensschijven stripe met behulp van [opslagruimten](http://technet.microsoft.com/library/hh831739.aspx), opslagruimten instellen met 1 kolom voor elke schijf die u gebruikt. Anders wordt de algemene prestaties van Hallo striped volume mogelijk lager is dan verwacht vanwege ongelijke verdeling van het verkeer over Hallo schijven. Standaard wordt in Serverbeheer kunt u kolommen voor up too8 schijven instellen. Als u meer dan 8 schijven hebt, gebruikt u PowerShell toocreate Hallo volume. Het aantal kolommen Hallo handmatig opgeven. Anders blijft Hallo Serverbeheer UI toouse 8 kolommen, zelfs als u meer schijven voor hebt. Bijvoorbeeld, als er 32 schijven in een stripeset één, 32 kolommen opgeven. toospecify hello aantal kolommen maakt gebruik van virtuele schijf, in Hallo Hallo [New-VirtualDisk](http://technet.microsoft.com/library/hh848643.aspx) PowerShell-cmdlet gebruik Hallo *NumberOfColumns* parameter. Zie voor meer informatie [overzicht van opslagruimten](http://technet.microsoft.com/library/hh831739.aspx) en [Storage Spaces Veelgestelde vragen over](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx).
    >
    > 

* **Cache**

    Virtuele machines in de Hallo grootte reeks die ondersteuning bieden voor Premium-opslag hebben een unieke cachebewerkingen mogelijkheid voor een hoge mate van doorvoer en latentie. Hallo caching mogelijkheid overschrijdt onderliggende schijfprestaties voor premium-opslag. U kunt instellen Hallo schijf cachebeleid op schijven met premium-opslag te**ReadOnly**, **ReadWrite**, of **geen**. Hallo standaard schijf cachebeleid **ReadOnly** voor alle schijven voor premium-gegevens, en **ReadWrite** voor besturingssysteem schijven. Voor optimale prestaties voor uw toepassing corrigeren gebruik Hallo cache-instelling. Bijvoorbeeld voor gegevensschijven die veel vraagt van de lezen of alleen-lezen, zoals SQL Server-gegevensbestanden, stelt u Hallo cachebeleid te**ReadOnly**. Voor schijven schrijven zware of alleen-schrijven gegevens, zoals SQL Server-logboekbestanden, stelt u Hallo cachebeleid te**geen**. toolearn meer informatie over het optimaliseren van uw ontwerp met Premium-opslag, Zie [ontwerpen voor prestaties voor Premium-opslag](storage-premium-storage-performance.md).

* **Analytische gegevens**

    VM diagnostische gegevens in Hallo tooanalyze VM prestaties met behulp van de schijven in Premium-opslag inschakelen [Azure-portal](https://portal.azure.com). Zie voor meer informatie [Azure VM bewaking met de extensie voor diagnostische gegevens van Azure](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/). 

    schijfprestaties toosee, hulpprogramma's voor gebruik op basis van het besturingssysteem, zoals [Windows Prestatiemeter](https://technet.microsoft.com/library/cc749249.aspx) voor VM's van Windows en Hallo [iostat](http://linux.die.net/man/1/iostat) opdracht voor virtuele Linux-machines.

* **VM-schaallimieten en prestaties**

    Elke Premium-opslag ondersteund VM-grootte heeft schaallimieten en prestatiespecificaties voor IOPS, bandbreedte en Hallo aantal schijven dat per virtuele machine kan worden gekoppeld. Wanneer u premium-opslag-schijven met virtuele machines gebruikt, zorg ervoor dat er voldoende IOPS en bandbreedte op de VM-verkeer toodrive schijf.

    Een VM STANDARD_DS1 heeft bijvoorbeeld een toegewezen bandbreedte van 32 MB/s voor premium schijf opslagverkeer. Een schijf P10 premium-opslag kan bieden een bandbreedte van 100 MB/s. Als een schijf P10 premium-opslag gekoppelde toothis VM is, kan het alleen Ga up too32 MB/s. Het Hallo u maximaal 100 MB/s die Hallo P10 schijf krijgt niet gebruiken.

    Hallo is grootste VM in Hallo DS-serie momenteel Hallo Standard_DS15_v2. Hallo Standard_DS15_v2 kan over alle schijven bieden up too960 MB/s. Hallo is grootste VM in Hallo GS-serie Hallo Standard_GS5. Hallo Standard_GS5 kan up too2, 000 MB/s verdeeld over alle schijven bieden.

    Houd er rekening mee dat deze limieten alleen beschikbaar voor schijf verkeer zijn. Deze limieten bevatten geen treffers in cache en netwerkverkeer. Een afzonderlijke bandbreedte is beschikbaar voor VM-netwerkverkeer. Bandbreedte voor netwerkverkeer wijkt af van Hallo toegewezen bandbreedte die wordt gebruikt door de premium-opslag-schijven.

    Zie voor Hallo meest actuele informatie over maximale IOPS en doorvoerlimieten (bandbreedte) voor Premium-opslag ondersteund virtuele machines, [Windows VM-grootten](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [Linux VM-grootten](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

    Zie voor meer informatie over de premium-opslag-schijven en de IOPS en doorvoerlimieten ervan Hallo-tabel in de volgende sectie Hallo.

## <a name="scalability-and-performance-targets"></a>Schaalbaarheids- en prestatiedoelen
In deze sectie beschrijven we Hallo schaalbaarheid en prestaties doelen tooconsider wanneer u Premium-opslag gebruikt.

Premium-opslagaccounts hebben Hallo schaalbaarheidsdoelen te volgen:

| Capaciteit van de totale account | Totale bandbreedte voor een account met lokaal redundante opslag |
| --- | --- | 
| Schijf capaciteit: 35 TB <br>Momentopname maken van capaciteit: 10 TB | Up too50 gigabits per seconde voor binnenkomende<sup>1</sup> + uitgaande<sup>2</sup> |

<sup>1</sup> alle gegevens (aanvragen) die worden verzonden tooa storage-account

<sup>2</sup> alle gegevens (antwoorden) die afkomstig zijn van een opslagaccount

Zie voor meer informatie [Azure Storage schaalbaarheids- en prestatiedoelen](storage-scalability-targets.md).

Als u premium storage-accounts voor niet-beheerde schijven gebruikt en uw toepassing hello schaalbaarheidsdoelen van een enkele opslagaccount overschrijdt, kunt u toomigrate toomanaged schijven. Als u niet toomigrate toomanaged schijven wilt, bouw uw toepassing toouse meerdere opslagaccounts. Partitioneren vervolgens uw gegevens over de storage-accounts. Bijvoorbeeld, als u tooattach 51 TB schijven over meerdere virtuele machines wilt, verdeeld over deze twee storage-accounts. 35 TB is Hallo limiet voor een enkele premium storage-account. Zorg ervoor dat een enkele premium storage-account nooit meer dan 35 TB aan ingerichte schijven heeft.

### <a name="premium-storage-disk-limits"></a>Premium-opslaglimieten schijf
Wanneer u een premium-opslagschijf Hallo grootte van Hallo schijf inrichten bepaalt Hallo maximale IOPS en doorvoerlimieten (bandbreedte). Azure biedt zeven schijftypen premium storage: P4 (beheerd schijven alleen), P6 (beheerd schijven alleen), P10, P20 P30, p 40 en P50. Elk type opslagschijf premium heeft bepaalde limieten voor IOPS en doorvoerlimieten. Limieten voor het Hallo-schijftypen worden beschreven in de volgende tabel Hallo:

| Premium-schijven Type  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Schijfgrootte           | 32 GB| 64 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOP's per schijf       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Doorvoer per schijf | 25 MB per seconde  | 50 MB per seconde  | 100 MB per seconde | 150 MB per seconde | 200 MB per seconde | 250 MB per seconde | 250 MB per seconde | 

> [!NOTE]
> Zorg ervoor dat voldoende bandbreedte beschikbaar is op uw VM toodrive schijf verkeer, zoals beschreven in [VMs Premium-opslag ondersteund](#premium-storage-supported-vms). Anders is de doorvoercapaciteit van de schijf en IOPS beperkte toolower waarden. Maximale doorvoer en IOP's zijn gebaseerd op Hallo VM-limieten, niet op Hallo schijfruimtelimiet beschreven in de voorgaande tabel Hallo.  
> 
> 

Hier volgen enkele belangrijke opmerkingen tooknow over de schaalbaarheids- en prestatiedoelen Premium-opslag:

* **Ingerichte capaciteit en prestaties**

    Wanneer u een premium-opslagschijf, in tegenstelling tot standaard opslag inrichten wordt gegarandeerd Hallo capaciteit, IOPS en doorvoer van die schijf. Als u een schijf P50 maakt, richt Azure bijvoorbeeld 4095 GB opslagcapaciteit 7.500 IOPS en 250 MB/s doorvoer voor die schijf. Uw toepassing kunt gebruiken of een deel van het Hallo-capaciteit en prestaties.

* **Grootte van de schijf**

    Azure maps Hallo schijf grootte (naar boven afronden) toohello dichtstbijzijnde premium schijf opslagoptie, zoals opgegeven in de tabel in de voorgaande sectie Hallo Hallo. Bijvoorbeeld, is een schijfgrootte van 100 GB geclassificeerd als een optie P10. Kan uitvoeren van too500 IOP's, met up too100 MB/s doorvoer. Op deze manier een schijf met een grootte van die 400 GB is geclassificeerd als een P20. Up too2, 300 IOP's, met 150 MB/s doorvoer kan uitvoeren.
    
    > [!NOTE]
    > U kunt gemakkelijk Hallo grootte van bestaande schijven verhogen. U kunt bijvoorbeeld tooincrease Hallo grootte van een schijf van 30 GB too128 GB of TB zelfs too1. Of u wellicht tooconvert tooa P30 schijf van uw P20 omdat u meer capaciteit of meer IOPS en doorvoerlimieten nodig hebt. 
    > 
 
* **I/o-grootte**

    Hallo-grootte van een i/o-is 256 KB. Hallo-gegevens die worden overgedragen, is minder dan 256 KB, worden beschouwd als 1 i/o-eenheid. I/o-grotere worden geteld als meerdere i/o's van de grootte van 256 KB. Bijvoorbeeld, worden 1100 KB i/o geteld als 5 i/o-eenheden.

* **Doorvoer**

    Hallo doorvoer limiet omvat schrijfbewerkingen toohello schijf en het omvat leesbewerkingen schijf die niet worden aangeboden via Hallo cache. Een schijf P10 heeft bijvoorbeeld 100 MB/s doorvoer per schijf. Enkele voorbeelden van geldige doorvoer voor een schijf P10 worden weergegeven in de volgende tabel Hallo:

    | Maximale doorvoer per P10 schijf | Niet-cache leest van de schijf | Niet-cache schrijft toodisk |
    | --- | --- | --- |
    | 100 MB/s | 100 MB/s | 0 |
    | 100 MB/s | 0 | 100 MB/s |
    | 100 MB/s | 60 MB/s | 40 MB/s |

* **Treffers in cache**

    Treffers in cache zijn niet beperkt door Hallo IOPS of doorvoer van Hallo schijf toegewezen. Bijvoorbeeld, wanneer u een gegevensschijf met gebruikt een **ReadOnly** cache-instelling op een virtuele machine die wordt ondersteund door de Premium-opslag, leest die worden aangeboden via Hallo cache zijn niet onderwerp toohello IOPS en doorvoer caps van Hallo schijf. Als Hallo werkbelasting van een schijf hoofdzakelijk is leest, kunt u zeer hoge doorvoersnelheid krijgen. Hallo-cache is onderwerp tooseparate IOPS en doorvoerlimieten op Hallo VM-niveau, op basis van Hallo VM-grootte. DS-serie VMs hebben ongeveer 4000 IOPS en 33 MB/s doorvoer per core voor cache en lokale SSD-i/o's. GS-serie VM's hebben een limiet van 5000 IOP's en 50 MB/s doorvoer per core voor cache en lokale SSD-i/o's. 

## <a name="throttling"></a>Beperking
Beperking optreden, als uw toepassing IOPS of doorvoer overschrijdt de Hallo toegewezen limieten voor de schijf voor een premium-opslag. Beperking ook optreden als het verkeer van de totale schijfruimte over alle schijven op Hallo VM Hallo schijf bandbreedte beschikbaar is voor Hallo VM overschrijdt. tooavoid beperking, is het raadzaam dat u aantal openstaande i/o-aanvragen voor schijf Hallo Hallo beperkt. Gebruik een beperken op basis van schaalbaarheids- en prestatiedoelen voor Hallo schijf die u hebt ingericht, en Hallo schijf bandbreedte beschikbaar toohello VM.  

Uw toepassing hello laagste latentie kunt bereiken bij is ontwikkeld tooavoid beperking. Echter, als hello aantal openstaande i/o-aanvragen voor Hallo schijf te klein is, uw toepassing kan niet profiteren van Hallo maximale IOPS en doorvoerlimieten niveaus die beschikbaar toohello schijf.

Hallo volgen voorbeelden laten zien hoe toocalculate beperking niveaus. Alle berekeningen zijn gebaseerd op een i/o-grootte van 256 KB.

### <a name="example-1"></a>Voorbeeld 1
Uw toepassing is 495 i/o-eenheden met een grootte van 16 KB in één seconde op een schijf P10 verwerkt. Hallo i/o-eenheden worden beschouwd als 495 IOPS. Als u probeert een 2 MB i/o's in dezelfde tweede hello, Hallo totaal van i/o-eenheden is gelijk too495 + 8 IOPS. Dit komt doordat 2 MB i/o = 2048 KB / 256 KB = 8 i/o-eenheden wanneer Hallo i/o-grootte 256 KB is. Beperking doet zich voor omdat Hallo som van 495 + 8 Hallo 500 IOPS voor Hallo schijf overschrijdt.

### <a name="example-2"></a>Voorbeeld 2
Uw toepassing is 400 i/o-eenheden met een grootte van 256 KB op een schijf P10 verwerkt. de totale bandbreedte Hallo verbruikt is (400 &#215; 256) * 1024 KB = 100 MB/s. Een schijf P10 heeft een doorvoer limiet van 100 MB/s. Als uw toepassing tooperform meer i/o-bewerkingen in deze tweede probeert, is deze beperkt omdat het Hallo toegewezen overschrijdt.

### <a name="example-3"></a>Voorbeeld 3
U hebt een VM DS4 met twee P30 schijven die zijn gekoppeld. Elke schijf P30 is geschikt 200 MB/s-doorvoer. Een VM DS4 heeft echter een capaciteit van de totale schijfruimte netwerkbandbreedte van 256 MB/s. U beide gekoppelde schijven toohello maximale doorvoer kan geen station op deze VM DS4 op Hallo hetzelfde moment. tooresolve, kunt u ondersteuning van verkeer van 200 MB/s op één schijf en 56 MB/s op Hallo andere schijf. Als Hallo som van uw verkeer schijf via 256 MB/s gaat, wordt de schijf verkeer beperkt.

> [!NOTE]
> Als uw schijf verkeer voornamelijk uit kleine i/o-grootten bestaat, wordt uw toepassing waarschijnlijk bereikt die Hallo IOPS voordat Hallo doorvoer limiet. Echter als Hallo schijf verkeer voornamelijk uit grote i/o-grootten bestaat, wordt uw toepassing waarschijnlijk bereikt die Hallo doorvoer eerst in plaats van Hallo IOPS limiet. U kunt uw toepassing IOPS en doorvoercapaciteit met behulp van de optimale grootte voor i/o-maximaliseren. Bovendien kunt u het aantal openstaande i/o-aanvragen voor een schijf Hallo beperken.
> 

toolearn meer informatie over het ontwerpen voor hoge prestaties met behulp van Premium-opslag, Zie [ontwerpen voor prestaties voor Premium-opslag](storage-premium-storage-performance.md).

## <a name="snapshots-and-copy-blob"></a>Momentopnamen en Blob kopiëren

toohello Storage-service, Hallo VHD-bestand is een pagina-blob. U kunt momentopnamen van pagina-blobs en kopieer deze tooanother locatie, zoals tooa ander opslagaccount.

### <a name="unmanaged-disks"></a>Niet-beheerde schijven

Maak [incrementele momentopnamen](storage-incremental-snapshots.md) voor niet-beheerde premium-schijven Hallo dezelfde manier als u momentopnamen met standard-opslag. Premium-opslag ondersteunt alleen lokaal redundante opslag als Hallo replicatie-optie. U wordt aangeraden dat u momentopnamen maken en vervolgens Hallo momentopnamen tooa geografisch redundante standard-opslagaccount kopieert. Zie voor meer informatie [Azure redundantie opslagopties](storage-redundancy.md).

Als een schijf aangesloten tooa VM is, worden bepaalde API-bewerkingen op Hallo schijf zijn niet toegestaan. Bijvoorbeeld, u kunt niet uitvoeren een [Blob kopiëren](/rest/api/storageservices/Copy-Blob) bewerking op de blob als Hallo schijf tooa VM gekoppeld. In plaats daarvan eerst een momentopname maken van blob met behulp van Hallo [momentopname Blob](/rest/api/storageservices/Snapshot-Blob) REST-API. Voer Hallo [Blob kopiëren](/rest/api/storageservices/Copy-Blob) Hallo momentopname toocopy Hallo schijf is gekoppeld. U kunt ook Hallo schijf loskoppelen en vervolgens alle noodzakelijke bewerkingen uitvoeren.

Hallo volgende limieten toopremium storage blob momentopnamen van toepassing:

| Limiet voor Premium-opslag | Waarde |
| --- | --- |
| Maximum aantal momentopnamen per blob | 100 |
| Account opslagcapaciteit voor momentopnamen<br>(Gegevens alleen momentopnamen bevat. Bevat geen gegevens in basis blob.) | 10 TB |
| Minimale tijd tussen opeenvolgende momentopnamen | 10 minuten |

toomaintain geografisch redundante exemplaren van de momentopnamen, u kunt momentopnamen kopiëren vanuit een premium storage-account tooa geografisch redundante opslag met standard-account met behulp van AzCopy of Blob kopiëren. Zie voor meer informatie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md) en [Blob kopiëren](/rest/api/storageservices/Copy-Blob).

Zie voor gedetailleerde informatie over het uitvoeren van de REST-bewerkingen op de pagina-blobs in een premium-opslagaccount [servicebewerkingen met Azure Premium Storage-Blob](http://go.microsoft.com/fwlink/?LinkId=521969).

### <a name="managed-disks"></a>Managed Disks

Een momentopname voor een beheerde schijf is een alleen-lezen kopie van het Hallo-beheerde schijven. Hallo momentopname wordt opgeslagen als een standard-beheerde schijven. Op dit moment [incrementele momentopnamen](storage-incremental-snapshots.md) worden niet ondersteund voor beheerde schijven. toolearn hoe tootake een momentopname voor een beheerde schijf zien [een kopie maken van een VHD die is opgeslagen als een Azure beheerd schijf met beheerde momentopnamen in Windows](../virtual-machines/virtual-machines-windows-snapshot-copy-managed-disk.md) of [een kopie maken van een VHD die is opgeslagen als een Azure beheerd schijf met behulp van beheerd momentopnamen in Linux](../virtual-machines/linux/snapshot-copy-managed-disk.md).

Als een beheerde schijf gekoppelde tooa VM, worden bepaalde API-bewerkingen op Hallo schijf zijn niet toegestaan. U kunt bijvoorbeeld een shared access signature (SAS) tooperform een kopieerbewerking niet genereren tijdens het Hallo-schijf is aangesloten tooa VM. In plaats daarvan maakt eerst een momentopname van Hallo schijf en Voer Hallo kopie van Hallo momentopname. U kunt ook Hallo schijf loskoppelen en vervolgens een kopieerbewerking SAS tooperform hello te genereren.


## <a name="premium-storage-for-linux-vms"></a>Premium-opslag voor virtuele Linux-machines
U kunt Hallo informatie toohelp van uw virtuele Linux-machines in Premium-opslag instellen te volgen:

tooachieve schaalbaarheid gericht in Premium-opslag voor alle schijven van premium-opslag met cache set te**ReadOnly** of **geen**, moet u "barrières" uitschakelen wanneer u het bestandssysteem Hallo koppelt. U hoeft niet barrières in dit scenario omdat Hallo schrijft toopremium opslagschijven duurzame voor deze cache-instellingen zijn. Wanneer de schrijfaanvraag Hallo met succes is voltooid, is gegevens toohello permanente archief geschreven. toodisable 'barrières,' Gebruik een van de volgende methoden Hallo. Hallo voor uw bestandssysteem kiezen:
  
* Voor **reiserFS**, toodisable barrières, gebruik Hallo `barrier=none` optie koppelen. (tooenable barrières, gebruik `barrier=flush`.)
* Voor **ext3/ext4**, toodisable barrières, gebruik Hallo `barrier=0` optie koppelen. (tooenable barrières, gebruik `barrier=1`.)
* Voor **XFS**, toodisable barrières, gebruik Hallo `nobarrier` optie koppelen. (tooenable barrières, gebruik `barrier`.)
* Voor premium-schijven met cache te ingesteld**ReadWrite**, barrières voor schrijven duurzaamheid inschakelen.
* Voor volume labels toopersist na het opnieuw opstarten Hallo virtuele machine, moet u bijwerken /etc/fstab met hello (UUID) universally unique identifier verwijzingen toohello schijven. Zie voor meer informatie [toevoegen van een beheerde schijf tooa Linux VM](../virtual-machines/linux/add-disk.md).

Hallo volgende Linux-distributies zijn gevalideerd voor Azure Premium-opslag. Voor betere prestaties en stabiliteit met Premium-opslag, raden we aan dat u uw virtuele machines tooone van deze versies, ten minste upgraden (of tooa latere versie). Sommige versies vereisen Hallo Hallo nieuwste Linux Integration Services (LIS), v4.0, voor Azure. Volg Hallo koppeling wordt weergegeven in de volgende tabel Hallo toodownload en installeer een distributiepunt. We toevoegen installatiekopieën toohello lijst als we validatie voltooid. Houd er rekening mee dat onze validaties weergegeven dat de prestaties wisselend voor elke installatiekopie. Prestaties zijn afhankelijk van werkbelasting kenmerken en de instellingen van uw installatiekopie. Andere installatiekopieën zijn voor verschillende soorten werkbelastingen afgestemd.

| Distributie | Versie | Ondersteunde kernel | Details |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-AMD64-server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-AMD64-server-20150123-en-us-30GB |
| Debian | 7.x, 8.x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| SUSE-sles-12-prioriteit-v20150213 <br> SUSE-sles-12-v20150213 |
| SUSE | SLES 11 SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | Virtuele CoreOS 584.0.0 |
| CentOS | 6.5, 6.6, 6.7, 7.0 | &nbsp; | [LIS4 vereist](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Zie de opmerking in de volgende sectie Hallo* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [Aanbevolen LIS4](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Zie de opmerking in de volgende sectie Hallo* |
| Red Hat Enterprise Linux (RHEL) | 6.8+, 7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+, 7.2+ | &nbsp; | UEK4 of RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 of RHCK met[LIS 4.1 +](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 of RHCK met[LIS 4.1 +](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>LIS stuurprogramma's voor OpenLogic CentOS

Als u OpenLogic CentOS virtuele machines uitvoert, voert u Hallo opdracht tooinstall Hallo meest recente stuurprogramma's te volgen:

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

tooactivate hello nieuwe stuurprogramma's, Hallo computer opnieuw opstarten.

## <a name="pricing-and-billing"></a>Prijzen en facturering

Als u Premium-opslag gebruikt, past u Hallo volgende factureringsvoorwaarden:

* **Premium-opslag schijf en de blob-grootte**

    Facturering voor een schijf voor premium-opslag of blob, is afhankelijk van Hallo ingericht grootte van Hallo schijf of blob. Azure maps Hallo ingerichte grootte (naar boven afronden) toohello dichtstbijzijnde premium-opslag-schijfoptie. Zie voor meer informatie Hallo-tabel in [Premium-opslag schaalbaarheids- en prestatiedoelen](#premium-storage-scalability-and-performance-targets). Elke schijf maps tooa ondersteund ingerichte schijfgrootte en dienovereenkomstig wordt gefactureerd. Facturering voor ingerichte schijven wordt elk uur naar rato via maandbedrag Hallo voor Hallo Premium-opslag-aanbieding. Als u een schijf P10 ingericht en deze na 20 uur verwijderd, kunt u wordt bijvoorbeeld voor gefactureerd voor Hallo P10 biedt naar rato too20 uur. Dit is ongeacht Hallo hoeveelheid gegevens geschreven toohello schijf of Hallo IOPS en doorvoer gebruikt.

* **Premium niet-beheerde schijven momentopnamen**

    Momentopnamen op zonder begeleiding premium-schijven wordt gefactureerd voor Hallo extra capaciteit die wordt gebruikt door Hallo momentopnamen. Zie voor meer informatie over momentopnamen [een momentopname maken van een blob](/rest/api/storageservices/Snapshot-Blob).

* **Premium-beheerde schijven momentopnamen**

    Een momentopname van een beheerde schijf is een alleen-lezen kopie van Hallo schijf. Hallo schijf wordt opgeslagen als een standard-beheerde schijven. De kosten van een momentopname Hallo dezelfde als een standaard schijf beheerde. Als u een momentopname van een beheerde schijf van 128 GB premium is Hallo kosten van het Hallo-momentopname gelijkwaardige tooa 128 GB-standard-beheerde schijven.  

* **Uitgaande gegevensoverdracht**

    [Uitgaande gegevensoverdracht](https://azure.microsoft.com/pricing/details/data-transfers/) (gegevens uit de Azure-datacenters gaan) worden gefactureerd voor bandbreedtegebruik.

Zie voor gedetailleerde informatie over prijzen voor Premium-opslag, Premium-opslag ondersteund VM's en beheerde schijven, deze artikelen:

* [Prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Virtuele Machines prijzen](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Beheerde schijven prijzen](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Ondersteuning van Azure back-up 

Voor regionale noodherstel, u moet back-up in een andere regio uw VM-schijven met behulp van [Azure Backup](../backup/backup-introduction-to-azure-backup.md) en een GRS-opslagaccount als een back-upkluis.

toocreate een back-uptaak met back-ups op basis van tijd eenvoudig herstel van de virtuele machine en bewaarbeleid voor back-up, gebruikt u Azure Backup. U kunt back-up beide gebruiken met niet-beheerde en beheerde schijven. Zie voor meer informatie [Azure Backup voor VM's met niet-beheerde schijven](../backup/backup-azure-vms-first-look-arm.md) en [Azure Backup voor virtuele machines met beheerde schijven](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). 

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over de Premium-opslag, Hallo artikelen te volgen.

### <a name="design-and-implement-with-premium-storage"></a>Ontwerpen en implementeren met Premium-opslag
* [Ontwerpen voor prestaties voor Premium-opslag](storage-premium-storage-performance.md)
* [BLOB storage-bewerkingen met Premium-opslag](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>Gebruiksaanwijzing
* [TooAzure Premium-opslag migreren](storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>Blogberichten
* [Algemeen beschikbaar Azure Premium-opslag](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [GS-serie aangekondigd Hallo: toe te voegen Premium-opslag ondersteuning toohello grootste Hallo VM's in openbare cloud](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)
