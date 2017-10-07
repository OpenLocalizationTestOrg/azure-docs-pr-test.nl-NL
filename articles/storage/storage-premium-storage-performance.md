---
title: 'Azure Premium-opslag: Ontwerpen voor prestaties | Microsoft Docs'
description: Ontwerp hoogwaardige toepassingen met behulp van Azure Premium-opslag. Premium-opslag biedt ondersteuning voor schijven voor hoge prestaties, lage latentie voor I/O-intensieve werkbelastingen die worden uitgevoerd op Azure Virtual Machines.
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: e6a409c3-d31a-4704-a93c-0a04fdc95960
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: aungoo
ms.openlocfilehash: 75845eb4707e8e5606153a5e1a7c10b4113ee121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-premium-storage-design-for-high-performance"></a>Azure Premium-opslag: Ontwerp voor hoge prestaties
## <a name="overview"></a>Overzicht
In dit artikel bevat richtlijnen voor het bouwen van krachtige toepassingen met behulp van Azure Premium-opslag. U kunt de instructies in dit document gecombineerd met de prestaties van best practices van toepassing tootechnologies gebruikt door de toepassing hello gebruiken. tooillustrate hello richtlijnen, hebben we SQL Server wordt uitgevoerd op de Premium-opslag als voorbeeld in dit hele document gebruikt.

Hoewel we prestaties scenario's voor het Hallo-opslaglaag in dit artikel, moet u toooptimize Hallo toepassingslaag. Bijvoorbeeld, als u een SharePoint-Farm op Azure Premium-opslag host, kunt u Hallo SQL Server-voorbeelden uit dit artikel toooptimize Hallo-databaseserver. Bovendien Hallo de SharePoint-Farm-webserver en de toepassing server tooget Hallo meeste prestaties optimaliseren.

Dit artikel helpt antwoord volgen Veelgestelde vragen over het optimaliseren van de toepassingsprestaties op Azure Premium-opslag

* Hoe toomeasure de toepassingsprestaties van uw?  
* Waarom zijn verwachte hoge prestaties niet zien?  
* Welke factoren van invloed op de toepassingsprestaties van uw op Premium-opslag?  
* Hoe deze factoren van invloed op prestaties van uw toepassing op Premium-opslag?  
* Hoe kunt u optimaliseren voor IOPS, bandbreedte en latentie?  

We hebben deze richtlijnen die specifiek voor Premium-opslag omdat werkbelasting op Premium-opslag zeer gevoelige prestaties zijn. We hebben voorbeelden verstrekt, indien van toepassing. U kunt ook enkele van deze richtlijnen tooapplications IaaS VM's met met standaard opslagschijven toepassen.

Voordat u begint, als u nieuwe tooPremium opslag, lees dan eerst Hallo [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](storage-premium-storage.md) en [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md)artikelen.

## <a name="application-performance-indicators"></a>Prestatie-indicatoren van toepassing
We controleren of een toepassing wordt uitgevoerd met behulp van prestatie-indicatoren, zoals goed of niet, hoe snel een gebruikersaanvraag, hoeveel gegevens van een toepassing per aanvraag verwerken wordt verwerkt door een toepassing, hoeveel aanvragen verwerken van een toepassing is in een specifieke periode, hoe lang die een gebruiker toowait tooget een antwoord heeft na hun aanvraag. Hallo technische voorwaarden voor deze prestatie-indicatoren zijn IOPS, doorvoer of bandbreedte en latentie.

In deze sectie bespreken we Hallo algemene prestatie-indicatoren in de context Hallo van Premium-opslag. In Hallo volgende sectie, toepassingsvereisten verzamelen, leert u hoe toomeasure deze prestatie-indicatoren voor uw toepassing. Verderop in de toepassingsprestaties optimaliseren u leert over Hallo factoren die invloed hebben op deze prestatie-indicatoren en aanbevelingen toooptimize ze.

## <a name="iops"></a>IOPS
IOPS is aantal aanvragen dat uw toepassing toohello opslagschijven in één seconde verzendt. Een i/o-bewerking kan worden gelezen of opeenvolgende of willekeurig schrijven. OLTP-toepassingen zoals een online retail-website moeten tooprocess veel gelijktijdige gebruiker onmiddellijk aanvraagt. Hallo gebruikersaanvragen invoegen zijn en werk intensieve databasetransacties welke toepassing hello snel moet verwerken. Daarom vereisen OLTP-toepassingen zeer hoge IOPS. Dergelijke toepassingen miljoenen kleine en willekeurige i/o-aanvragen worden verwerkt. Als u een dergelijke toepassing hebt, moet u Hallo toepassing infrastructuur toooptimize ontwerpen voor IOPS. In hello later sectie *toepassingsprestaties optimaliseren*, bespreken we in detail alle Hallo factoren die u, tooget overwegen moet hoge IOPS.

Wanneer koppelt u een premium-opslag schijf tooyour grootschalige virtuele machine, Azure voorziet u een gegarandeerd aantal IOPS volgens de specificatie van Hallo-schijf. Een schijf P50 levert bijvoorbeeld 7500 IOPS. Elke grote schaal VM-grootte heeft ook een specifieke IOPS limiet die deze kan tolereren. Zo heeft een standaard GS5 VM 80.000 IOP's beperken.

## <a name="throughput"></a>Doorvoer
Doorvoer- of bandbreedte is Hallo en de hoeveelheid gegevens dat uw toepassing toohello opslagschijven in een opgegeven interval verzendt. Als uw toepassing met het uitvoeren van de i/o-bewerkingen met grote i/o-eenheid grootten, is er een hoge doorvoer vereist. Datawarehouse-toepassingen vaak tooissue scan bewerkingsintensieve bewerkingen die toegang tot grote delen van gegevens op een tijdstip en meest bulkbewerkingen worden uitgevoerd. Met andere woorden, vereisen dergelijke toepassingen hogere doorvoer. Als u een dergelijke toepassing hebt, moet u de infrastructuur toooptimize ontwerpen voor doorvoer. In de volgende sectie hello, besproken in detail Hallo factoren u moet tooachieve dit afstemmen.

Wanneer koppelt u een premium-opslag schijf tooa grootschalige virtuele machine, Azure bepalingen doorvoer volgens de specificatie van die schijf. Een schijf P50 levert bijvoorbeeld 250 MB per tweede schijf doorvoer. Elke grote schaal VM-grootte heeft ook als specifieke doorvoer limiet die deze kan tolereren. Standaard GS5 VM heeft bijvoorbeeld een maximale doorvoer van 2.000 MB per seconde. 

Er is een relatie tussen de doorvoer en IOP's, zoals wordt weergegeven in onderstaande Hallo-formule.

![](media/storage-premium-storage-performance/image1.png)

Het is daarom belangrijk toodetermine Hallo optimale doorvoer en IOPS-waarden die vereist zijn voor uw toepassing. Als u toooptimize een probeert, wordt Hallo andere ook beïnvloed. In een volgende sectie *toepassingsprestaties optimaliseren*, behandeld in meer informatie over het optimaliseren van IOPS en Doorvoerlimieten.

## <a name="latency"></a>Latentie
Latentie is Hallo het duurt voordat een toepassing tooreceive één aanvraag, verzenden toohello opslagschijven en Hallo antwoord toohello client verzenden. Dit is een kritieke meting van de prestaties van een toepassing in toevoeging tooIOPS en doorvoer. Hallo latentie van de schijf voor een premium-opslag is Hallo keer tooretrieve Hallo-informatie voor een aanvraag duurt en communiceren tooyour toepassing weer. Premium-opslag biedt een consistente lage latenties. Als u alleen-lezen-hostcaching op schijven met opslagruimte premium inschakelt, kunt u veel lagere latentie mogelijk lezen krijgen. Bespreken we schijfcache in de volgende sectie uitvoeriger op *toepassingsprestaties optimaliseren*.

Wanneer het optimaliseren van uw toepassing tooget hogere IOPS en Doorvoerlimieten, heeft dit gevolgen voor Hallo latentie van uw toepassing. Na het afstemmen van de toepassingsprestaties Hallo Hallo latentie van Hallo toepassing tooavoid altijd geëvalueerd onverwacht hoge latentie gedrag.

## <a name="gather-application-performance-requirements"></a>Verzamelen van prestaties toepassingsvereisten
Hallo eerste stap bij het ontwerpen van krachtige toepassingen die worden uitgevoerd op Azure Premium-opslag is toounderstand Hallo prestatie-eisen van uw toepassing. Wanneer u prestatie-eisen verzameld, kunt u uw toepassing tooachieve Hallo optimale prestaties te optimaliseren.

In de vorige sectie hello, we uitgelegd Hallo algemene prestatie-indicatoren, IOPS, doorvoer en latentie. U moet nagaan welke van deze prestatie-indicatoren kritieke tooyour toepassing toodeliver Hallo desired-gebruikerservaring. Bijvoorbeeld, telt hoge IOPS miljoenen transacties worden verwerkt in een tweede meeste tooOLTP-toepassingen. Dat hoge doorvoersnelheid essentieel voor de verwerking van grote hoeveelheden gegevens in een tweede Data Warehouse-toepassingen is. Zeer lage latentie is van cruciaal belang voor realtime toepassingen zoals live videostreaming websites.

Vervolgens meten Hallo Maximale prestatie-eisen van uw toepassing tijdens de levensduur. Controlelijst voor het voorbeeld hieronder hello gebruiken als een start. Maximale prestatie-eisen record Hallo tijdens normaal, piek- en rustige uren werkbelasting perioden. Door het identificeren van de vereisten voor alle werkbelastingen niveaus kunt u zich kunt toodetermine Hallo algehele prestaties vereisten van uw toepassing. Hallo normale werkbelasting van een webwinkel wordt bijvoorbeeld Hallo transacties die het meeste dagen in een jaar fungeert. Hallo piek werkbelasting van Hallo website worden Hallo transacties die het tijdens de feestdagen of speciale verkoop gebeurtenissen fungeert. Hallo piek werkbelasting is doorgaans ervaren voor een beperkte periode, maar kan vereisen uw toepassing tooscale twee of meer de normale werking. Ontdek Hallo 50 percentiel, 90 percentiel en 99 percentiel vereisten. Dit helpt uitfilteren eventuele uitschieters in Hallo prestatie-eisen en kunt u uw inspanningen zich richten op voor de juiste waarden hello te optimaliseren.

**Controlelijst voor de vereisten van de toepassingsprestaties**

| **Prestatie-eisen** | **50 percentiel** | **90 percentiel** | **99 percentiel** |
| --- | --- | --- | --- |
| Met maximaal Transacties per seconde | | | |
| % Leesbewerkingen | | | |
| % Schrijfbewerkingen | | | |
| % Willekeurige bewerkingen | | | |
| % Opeenvolgende bewerkingen | | | |
| De grootte van de i/o-aanvraag | | | |
| Gemiddelde doorvoersnelheid | | | |
| Met maximaal Doorvoer | | | |
| Min. Latentie | | | |
| Gemiddelde latentie | | | |
| Met maximaal CPU | | | |
| Gemiddelde CPU | | | |
| Met maximaal Geheugen | | | |
| Gemiddelde geheugen | | | |
| Wachtrijdiepte | | | |

> [!NOTE]
> U moet overwegen deze getallen op basis van de verwachte toekomstige groei van uw toepassing schalen. Het is een goed idee tooplan groei tevoren, omdat deze mogelijk moeilijker toochange Hallo-infrastructuur voor het verbeteren van de prestaties later.
>
>

Als u een bestaande toepassing en toomove tooPremium opslag wilt, moet u eerst Hallo controlelijst hierboven voor de bestaande toepassing hello bouwen. Vervolgens kunt samenstellen van een prototype van uw toepassing op Premium-opslag- en ontwerpfase Hallo-toepassing op basis van de richtlijnen in *toepassingsprestaties optimaliseren* in verderop in dit document. de volgende sectie Hallo beschrijft Hallo-hulpprogramma's kunt u toogather Hallo prestatiemetingen.

Maak een controlelijst vergelijkbare tooyour bestaande toepassing voor Hallo prototype. Met Benchmarking hulpprogramma's kunt u werkbelastingen Hallo simuleren en prestaties van een prototype-toepassing hello meten. Zie de sectie Hallo over [Benchmarking](#benchmarking) toolearn meer. Hierdoor kunt u bepalen of Premium-opslag kan overeenkomen met of groter zijn dan de prestatie-eisen van uw toepassing. Vervolgens kunt u implementeren Hallo dezelfde richtlijnen voor de productietoepassing.

### <a name="counters-toomeasure-application-performance-requirements"></a>Prestatiemeteritems van de prestaties van toomeasure toepassingsvereisten
aanbevolen manier toomeasure prestatie-eisen van uw toepassing Hello, toouse prestatiebewaking hulpprogramma's van besturingssysteem Hallo van Hallo-server. U kunt PerfMon voor Windows- en iostat voor Linux. Deze hulpprogramma's vastleggen tellers bijbehorende tooeach meting in Hallo boven sectie uitgelegd. U moet waarden van deze prestatiemeteritems Hallo vastleggen als uw toepassing wordt uitgevoerd, zijn normaal, de piek- en rustige uren werkbelastingen.

Hallo-prestatiemeteritems zijn beschikbaar voor de processor, geheugen, en elke logische schijf en de fysieke schijf van uw server. Als u premium-opslag-schijven met een virtuele machine, Hallo fysieke schijf-items zijn voor elke schijf premium-opslag en de prestatiemeteritems voor logische schijf zijn voor elk volume dat is gemaakt op Hallo premium-opslag-schijven. U moet waarden voor Hallo-schijven die als host fungeren van de werkbelasting van uw toepassing hello vastleggen. Als er een één tooone toewijzing tussen logische en fysieke schijven, raadpleegt u toophysical schijf tellers; Raadpleeg anders toohello logische schijf tellers. Hallo iostat opdracht genereert op Linux, een CPU- en schijfresources utilization-rapport. Hallo disk utilization-rapport voorziet in statistieken per fysieke apparaat of partitie. Als u een databaseserver met de gegevens en logboekbestanden op afzonderlijke schijven hebt, kunt u deze gegevens voor beide schijven verzamelen. Onderstaande tabel worden beschreven tellers voor schijven, processor en geheugen:

| Prestatiemeteritems | Beschrijving | PerfMon | Iostat |
| --- | --- | --- | --- |
| **IOPS of transacties per seconde** |Het aantal i/o-aanvragen uitgegeven toohello opslagschijf voor de per seconde. |Schijf lezen per seconde <br> Schijf schrijven per seconde |tps <br> r/s <br> w/s |
| **Schijf lees- en schrijfbewerkingen** |% van de lees- en schrijfbewerkingen uitgevoerd op Hallo schijf. |Percentage schijftijd voor lezen <br> Percentage schijftijd voor schrijven |r/s <br> w/s |
| **Doorvoer** |De hoeveelheid gegevens lezen uit of schrijven toohello schijf per seconde. |Gelezen Bytes per seconde <br> Geschreven Bytes per seconde |kB_read/s <br> kB_wrtn/s |
| **Latentie** |Totale tijd toocomplete een schijf-i/o-aanvraag. |Gemiddelde leestijd voor schijf <br> Gemiddelde fysieke schijf |await <br> svctm |
| **I/o-grootte** |Hallo-grootte van i/o-aanvragen verstrekt toohello opslagschijven. |Gemiddeld aantal gelezen Bytes <br> Gemiddelde aantal geschreven Bytes |avgrq sz |
| **Wachtrijdiepte** |Aantal openstaande i/o-wachttijd toobe formulier gelezen of geschreven toohello opslagschijf aanvragen. |Huidige wachtrijlengte voor schijf |avgqu sz |
| **Max. Geheugen** |Hoeveelheid geheugen vereist toorun toepassing soepel |Percentage toegewezen Bytes in gebruik |Vmstat gebruiken |
| **Max. CPU** |De hoeveelheid CPU toorun toepassing soepel vereist |Percentage processortijd |% util |

Meer informatie over [iostat](http://linuxcommand.org/man_pages/iostat1.html) en [PerfMon](https://msdn.microsoft.com/library/aa645516.aspx).

## <a name="optimizing-application-performance"></a>Optimaliseert de prestaties van toepassingen
Hallo belangrijkste factoren die van invloed op prestaties van een toepassing die wordt uitgevoerd op de Premium-opslag zijn aard van i/o-aanvragen, VM-grootte, de grootte van de schijf, het aantal schijven, schijfcache, Multithreading en wachtrijdiepte. U kunt sommige van deze factoren met knoppen geleverd door het Hallo-systeem beheren. De meeste toepassingen mogelijk geen geven u een optie tooalter Hallo i/o-grootte en wachtrijdiepte rechtstreeks. Bijvoorbeeld, als u SQL Server gebruikt, kiezen u niet Hallo IO diepte van grootte en wachtrij. SQL Server kiest Hallo optimale IO grootte en wachtrij diepte waarden tooget Hallo meeste prestaties. Het is belangrijk toounderstand Hallo gevolgen van beide typen factoren op de toepassingsprestaties van uw, zodat u de juiste resources toomeet prestatievereisten past kunt inrichten.

In deze sectie verwijzen toohello toepassing controlelijst voor de vereisten die u hebt gemaakt, tooidentify hoeveel u toooptimize de toepassingsprestaties van uw nodig. Op basis van dat u zich kunt toodetermine moet die factoren in deze sectie u tootune. toowitness Hallo gevolgen van elke factor voor uw toepassingsprestaties uitvoeren benchmarking hulpprogramma's voor het installatieprogramma van de toepassing. Raadpleeg toohello [Benchmarking](#Benchmarking) sectie op Hallo einde van dit artikel voor stappen toorun algemene benchmarking hulpprogramma's voor Windows en Linux-machines.

### <a name="optimizing-iops-throughput-and-latency-at-a-glance"></a>IOPS, Throughput and Latency optimaliseren in één oogopslag
Hallo in de volgende tabel geeft een overzicht van alle Hallo prestatiefactoren en Hallo stappen toooptimize IOPS, doorvoer en latentie. Hallo secties na dit overzicht bevat een beschrijving van elk factor is veel meer diepte.

| &nbsp; | **IOPS** | **Doorvoer** | **Latentie** |
| --- | --- | --- | --- |
| **Voorbeeldscenario 's** |Enterprise OLTP-toepassing waarvoor zeer hoge transacties per tweede snelheid. |Enterprise gegevensopslag toepassing verwerking van grote hoeveelheden gegevens. |Bijna realtime toepassingen vereisen directe antwoorden toouser aanvragen, zoals online gaming. |
| Prestatiefactoren | &nbsp; | &nbsp; | &nbsp; |
| **I/o-grootte** |I/o-kleinere levert hogere IOPS. |Grotere i/o-grootte tooyields hogere doorvoer. | &nbsp;|
| **VM-grootte** |Gebruik een VM-grootte die groter zijn dan de vereisten voor toepassingsimplementatie IOPS biedt. Zie VM-grootten en hun IOPS-limieten. |Gebruik een VM-grootte met doorvoer limiet groter is dan de vereisten van uw toepassing. VM-grootten en hun doorvoerlimieten hier zien. |Gebruik een VM-grootte of aanbiedingen limieten groter is dan de vereiste toepassing schalen. VM-grootten en hun limieten hier zien. |
| **Grootte van de schijf** |Gebruik een grootte van de schijf die groter zijn dan de vereisten voor toepassingsimplementatie IOPS biedt. Zie schijfgrootten en hun IOPS-limieten. |De grootte van een schijf met doorvoer limiet groter is dan de vereisten van uw toepassing gebruiken. Zie schijfgrootten en hun doorvoerlimieten hier. |Gebruik een grootte van de schijf dat aanbiedingen limieten groter is dan de vereiste toepassing schalen. Zie schijfgrootten en hier hun limieten. |
| **Virtuele machine en Schaallimieten voor schijf** |Limiet van Hallo VM-grootte gekozen IOPS moet groter zijn dan de totale IOP's aangedreven door premium opslagschijven tooit gekoppeld. |Limiet voor doorvoer van Hallo VM-grootte gekozen moet groter zijn dan de totale doorvoer aangedreven door premium opslagschijven tooit gekoppeld. |Schaallimieten van Hallo VM-grootte gekozen moet groter zijn dan de totale schaallimieten van gekoppelde premium-opslag-schijven. |
| **Schijfcache** |ReadOnly-Cache inschakelen op schijven met premium-opslag met lezen zware bewerkingen tooget hoger lezen IOPS. | &nbsp; |ReadOnly-Cache inschakelen op schijven met premium-opslag met gereed zware bewerkingen tooget zeer lage lezen latentie. |
| **Striping van de schijf** |Gebruik van meerdere schijven en stripe ze samen tooget een gecombineerde hogere IOPS en doorvoer limiet. Let op: Hallo gecombineerde limiet is per VM moet groter dan Hallo gecombineerde limieten van de gekoppelde premium-schijven. | &nbsp; | &nbsp; |
| **Stripe-grootte** |Kleinere stripe voor willekeurige kleine i/o-patroon gezien in OLTP-toepassingen. Gebruik bijvoorbeeld stripe-grootte van 64KB voor SQL Server OLTP-toepassing. |Grotere stripe voor opeenvolgende grote i/o-patroon gezien in de datawarehouse-toepassingen. Gebruik bijvoorbeeld 256KB stripe-grootte voor SQL Server Data warehouse-toepassing. | &nbsp; |
| **Multithreading** |Gebruik multithreading toopush hoger aantal aanvragen tooPremium opslag die toohigher IOPS leiden en doorvoer. Bijvoorbeeld, stel SQL Server op een hoog MAXDOP waarde tooallocate meer CPU's tooSQL Server. | &nbsp; | &nbsp; |
| **Wachtrijdiepte** |Grotere wachtrijdiepte levert hogere IOPS. |Grotere wachtrijdiepte levert hogere doorvoer. |Kleinere wachtrijdiepte levert lagere latenties. |

## <a name="nature-of-io-requests"></a>Aard van i/o-aanvragen
Een i/o-aanvraag is een eenheid van i/o-bewerking die uw toepassing gaan uitvoeren. Hallo aard van i/o-aanvragen, willekeurige of opeenvolgende, identificeren lezen of schrijven, klein of groot is, kunt u bepalen Hallo prestatie-eisen van uw toepassing. Het is heel belangrijk toounderstand Hallo aard van i/o-aanvragen, toomake Hallo rechts beslissingen bij het ontwerpen van de infrastructuur van uw toepassing.

I/o-grootte is een van de Hallo meer belangrijke factoren. Hallo i/o-grootte is Hallo grootte van Hallo i/o-bewerkingsaanvraag gegenereerd door uw toepassing. Hallo i/o-grootte heeft een aanzienlijke invloed op prestaties vooral op Hallo IOPS en bandbreedte die toepassing hello kunnen tooachieve is. Hallo volgende formule toont Hallo relatie tussen IOP's, i/o-grootte en bandbreedte/doorvoer.  
    ![](media/storage-premium-storage-performance/image1.png)

Sommige toepassingen kunnen u tooalter hun i/o-grootte, maar sommige toepassingen niet. Bijvoorbeeld SQL Server bepaalt Hallo optimale grootte I/O zelf en biedt geen gebruikers met alle knoppen toochange deze. Op Hallo daarentegen, Oracle biedt een parameter met de naam [DB\_blokkeren\_grootte](https://docs.oracle.com/cd/B19306_01/server.102/b14211/iodesign.htm#i28815) i/o-aanvraaggrootte van Hallo-database die u kunt configureren met behulp Hallo.

Als u met behulp van een toepassing die u toochange Hallo i/o-grootte niet toestaat, gebruikt u Hallo richtlijnen in dit artikel toooptimize Hallo prestaties KPI die de meest relevante tooyour toepassing is. Bijvoorbeeld:

* Een OLTP-toepassing genereert miljoenen kleine en willekeurige i/o-aanvragen. Dit type i/o toohandle aanvraagt, moet u uw toepassing infrastructuur tooget ontwerpen hogere IOPS.  
* Een datawarehouse-toepassing genereert grote en opeenvolgende i/o-aanvragen. toohandle deze type i/o-aanvragen, moet u uw toepassing infrastructuur tooget hogere bandbreedte of doorvoer ontwerpen.

Als u van een toepassing, waarmee u toochange Hallo i/o-grootte gebruikmaakt, gebruiken deze vuistregel voor Hallo IO grootte bovendien tooother prestaties richtlijnen

* Kleinere i/o-grootte tooget hogere IOPS. Bijvoorbeeld: 8 KB voor een OLTP-toepassing.  
* Grotere i/o-grootte tooget hogere bandbreedte/doorvoer. Bijvoorbeeld 1024 KB voor een datawarehouse-toepassing.

Hier volgt een voorbeeld van hoe u Hallo IOPS en doorvoer/bandbreedte voor uw toepassing berekenen kunt. U kunt een toepassing met een schijf P30. Hallo is maximumaantal IOPS en doorvoer/bandbreedte met een schijf P30 bereiken kunt 5000 IOP's en 200 MB per seconde respectievelijk. Als uw toepassing vereist Hallo die maximumaantal IOPS van Hallo P30 schijf en u gebruikt een kleinere IO zoals 8 KB hello waardoor u bandbreedte heeft kunt tooget nu 40 MB per seconde. Als uw toepassing vereist Hallo maximale doorvoer/bandbreedte van P30 schijf en gebruik van i/o groter zoals 1024 KB, hello resulterende IOP's zijn echter minder 200 IOPS. Daarom Hallo i/o-grootte instellen zodat deze voldoet aan de vereiste IOPS en doorvoer/bandbreedte van zowel uw toepassing. De volgende tabel geeft een overzicht van Hallo verschillende i/o-grootte en hun bijbehorende IOPS en Doorvoerlimieten voor een schijf P30.

| Vereisten voor toepassingsimplementatie | I/o-grootte | IOPS | Doorvoer/bandbreedte |
| --- | --- | --- | --- |
| Max. IOP 's |8 kB |5,000 |40 MB per seconde |
| Maximale doorvoer |1024 KB |200 |200 MB per seconde |
| Maximale Throughput + hoge IOPS |64 kB |3,200 |200 MB per seconde |
| Maximale IOPS + hoge doorvoersnelheid |32 KB |5,000 |160 MB per seconde |

Gebruik meerdere premium-schijven samen striped tooget IOPS en bandbreedte die hoger is dan de maximumwaarde Hallo van een schijf één premium-opslag. Bijvoorbeeld, stripe twee P30 schijven tooget een gecombineerde IOPS van 10.000 IOPS of een gecombineerde doorvoer van 400 MB per seconde. Zoals wordt beschreven in de volgende sectie hello, moet u een VM-grootte die ondersteuning biedt voor Hallo gecombineerd schijf IOPS en doorvoer.

> [!NOTE]
> Als u beide IOPS vergroten of andere doorvoer Hallo ook verhoogt, zorg er dan voor dat u doorvoer of IOPS-limieten van Hallo schijf of virtuele machine niet bereikt wanneer ofwel een verhogen.
>
>

toowitness Hallo gevolgen van i/o-grootte voor de prestaties van toepassingen, kunt u benchmarking's uitvoeren op de virtuele machine en de schijven. Meerdere testruns maken en gebruiken van andere i/o-grootte voor elke uitvoering toosee Hallo impact. Raadpleeg toohello [Benchmarking](#Benchmarking) sectie op Hallo einde van dit artikel voor meer informatie.

## <a name="high-scale-vm-sizes"></a>VM-grootten van grote schaal
Wanneer u begint met het ontwerpen van een toepassing, is een van de eerste dingen toodo Hallo, kiest u een VM-toohost uw toepassing. Premium-opslag wordt geleverd met hoge Scale VM-grootten die toepassingen waarbij hogere rekencapaciteit en een hoge lokale schijf i/o-prestaties kunnen worden uitgevoerd. Deze virtuele machines bieden snellere processors, een hogere ratio van geheugen-core- en een Solid-State stations (SSD) voor de lokale schijf Hallo. Voorbeelden van hoge Scale VMs ondersteunende Premium-opslag zijn Hallo DS, DSv2 en GS-serie virtuele machines.

Maximale schaal VM's zijn beschikbaar in verschillende grootten met een verschillend aantal CPU-kernen, geheugen, OS en grootte van de tijdelijke schijf. Elk VM-grootte heeft ook het maximum aantal gegevensschijven dat kunt u toohello VM koppelen. Hallo gekozen VM-grootte heeft gevolgen hoeveel capaciteit verwerking, geheugen en opslagruimte beschikbaar is voor uw toepassing. Het is ook van invloed op hello berekenings- en opslagkosten. Hieronder staat bijvoorbeeld Hallo specificaties van Hallo grootste VM-grootte in een DS-serie, DSv2 reeks en een GS-serie:

| VM-grootte | CPU-kernen | Geheugen | Schijfgrootten VM | Met maximaal Gegevensschijven | Cachegrootte | IOPS | Bandbreedtelimieten i/o-Cache |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS14 |16 |112 GB |OS = 1023 GB <br> Lokale SSD = 224 GB |32 |576 GB |50.000 IOP 'S <br> 512 MB per seconde |4000 IOPS en 33 MB per seconde |
| Standard_GS5 |32 |448 GB |OS = 1023 GB <br> Lokale SSD = 896 GB |64 |4224 GB |80.000 IOP 'S <br> 2.000 MB per seconde |5000 IOP's en 50 MB per seconde |

een volledige lijst met alle beschikbare Azure VM-grootten tooview te verwijzen[Windows VM-grootten](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [Linux VM-grootten](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Kies een VM-grootte die kan voorzien en schaal tooyour gewenst toepassing prestatie-eisen. Bovendien rekening toothis, volgen enkele belangrijke overwegingen bij het kiezen van de VM-grootten.

*Schaallimieten*  
Hallo maximale IOPS-limieten per virtuele machine en per schijf zijn verschillende en onafhankelijk van elkaar. Zorg ervoor dat de toepassing hello IOP's binnen de grenzen Hallo Hallo VM, evenals Hallo premium-schijven gekoppelde tooit van wordt bestuurd. Anders merken toepassingsprestaties beperking.

Stel bijvoorbeeld dat een vereiste toepassing is maximaal 4000 IOPS. tooachieve deze, u bepaling een P30 schijf op een VM DS1. Hallo P30 schijf kunt bieden tot too5, 000 IOPS. Hallo DS1 VM is echter beperkt too3, 200 IOPS. Als gevolg daarvan kan Hallo toepassingsprestaties zal worden beperkt door Hallo VM grens bij 3200 IOPS en zullen er verminderde prestaties. tooprevent deze situatie, kiest u een virtuele machine en schijfgrootte die beide voldoen aan toepassingsvereisten.

*Kosten van bewerking*  
In veel gevallen is het mogelijk dat de totale kosten van bewerking u Premium-opslag is lager dan het gebruik van de Standard-opslag.

Neem bijvoorbeeld een toepassing 16.000 IOPS vereisen. tooachieve deze prestaties, moet u een standaard\_D14 Azure IaaS VM, waardoor een maximumaantal IOPS op 16.000 met 32 standaard opslagschijven voor 1 TB. Elke schijf van 1TB standard-opslag kunt maximaal 500 IOPS bereiken. Hallo geschatte kosten van deze virtuele machine per maand $1,570 zijn. maandelijkse kosten Hallo 32 standaardopslag schijven worden $1,638. Hallo geschatte totale maandelijkse kosten worden $3,208.

Echter, als u gehost Hallo dezelfde toepassing op Premium-opslag, moet u een kleinere VM en minder premium-opslag-schijven, waardoor de totale kosten Hallo. Een standaard\_DS13 VM Hallo 16.000 IOPS vereiste met vier P30 schijven kan worden voorzien. Hallo DS13 VM heeft een maximumaantal IOPS op 25,600 en elke schijf P30 heeft een maximumaantal IOPS op 5.000. Over het algemeen deze configuratie 5.000 x 4 = 20.000 kunt bereiken IOPS. Hallo geschatte kosten van deze virtuele machine per maand $1,003 zijn. Hallo maandelijkse kosten van vier P30 premium-opslag-schijven worden $544.34. Hallo geschatte totale maandelijkse kosten worden $1,544.

De volgende tabel geeft een overzicht van Hallo verdeling van de kosten van dit scenario voor Standard en Premium-opslag.

| &nbsp; | **Standard** | **Premium** |
| --- | --- | --- |
| **Kosten van de virtuele machine per maand** |$1,570.58 (standaard\_D14) |$1,003.66 (standaard\_DS13) |
| **Kost van schijven per maand** |1,638.40 (32 x 1 TB schijven) |544.34 (4 x P30 schijven) |
| **Totale kosten per maand** |$3,208.98 |$1,544.34 |

*Linux-distributies*  

Met Azure Premium-opslag, beschikt u over Hallo hetzelfde niveau van de prestaties voor virtuele machines met Windows en Linux. We bieden ondersteuning voor veel versies van Linux-distributies en ziet u de volledige lijst Hallo [hier](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Het is belangrijk toonote verschillende distributies zijn beter geschikt voor verschillende typen werkbelastingen. U ziet, afhankelijk van Hallo distro die uw werkbelasting wordt uitgevoerd op verschillende prestatieniveaus. Linux-distributies Hallo met uw toepassing testen en kies Hallo die het beste werkt.

Wanneer waarop Linux wordt uitgevoerd met Premium-opslag, controleert u de meest recente updates Hallo over de vereiste stuurprogramma's tooensure hoge prestaties.

## <a name="premium-storage-disk-sizes"></a>Schijfgrootte voor Premium-opslag
Azure Premium-opslag biedt momenteel zeven schijfgrootten. De grootte van elke schijf heeft de limiet van een andere schaal voor IOPS, bandbreedte en opslag. Kies Hallo rechts Premium Storage schijfgrootte afhankelijk van de toepassingsvereisten Hallo en Hallo grote schaal VM-grootte. Hallo in de volgende tabel toont Hallo zeven schijven grootten en hun mogelijkheden. P4 en P6 grootten zijn momenteel alleen ondersteund voor schijven die worden beheerd.

| Premium-schijven Type  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Schijfgrootte           | 32 GB | 64 GB | 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOP's per schijf       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Doorvoer per schijf | 25 MB per seconde  | 50 MB per seconde  | 100 MB per seconde | 150 MB per seconde | 200 MB per seconde | 250 MB per seconde | 250 MB per seconde | 


Hoeveel schijven die u kiest, hangt Hallo schijf grootte gekozen. U kunt één P50 schijf of meerdere P10 schijven toomeet uw vereisten voor toepassingsimplementatie. Aandachtspunten voor gebruikersaccounts onderstaande waardoor Hallo keuze rekening.

*Schaallimieten (IOPS en Doorvoerlimieten)*  
Hallo IOPS en Doorvoerlimieten limieten van elke Premium-schijfgrootte is verschillende en onafhankelijk van schaallimieten voor Hallo VM. Zorg ervoor dat de totale IOP's Hallo en doorvoer van Hallo schijven zijn binnen de grenzen van de schaal van Hallo gekozen VM-grootte.

Bijvoorbeeld als een vereiste toepassing maximaal 250 MB per seconde doorvoer is en u gebruikmaakt van een VM DS4 met één P30 schijf. Hallo DS4 VM kunt gaven ze too256 MB per seconde doorvoer. Een enkele P30 schijf heeft echter doorvoer limiet van 200 MB per seconde. Hallo-toepassing wordt als gevolg daarvan kan worden beperkt op 200 MB per seconde vanwege toohello schijf limiet. tooovercome deze limiet inrichten van meer dan één gegevens schijven toohello VM of het formaat van uw schijven tooP40 of P50.

> [!NOTE]
> Leesbewerkingen geleverd door Hallo cache niet zijn opgenomen in Hallo schijf IOPS en doorvoer, toodisk limieten daarom geen onderwerpnaam. Cache heeft de afzonderlijke IOPS en Doorvoerlimieten bereikt per VM.
>
> In eerste instantie zijn lees- en schrijfbewerkingen bijvoorbeeld 60MB per seconde en 40MB per seconde respectievelijk. Na verloop van tijd Hallo cache warms up en meer en meer Hallo leesbewerkingen uit cache Hallo fungeert. Vervolgens kunt u hogere schrijven doorvoer van Hallo schijf ophalen.
>
>

*Aantal schijven*  
Het aantal schijven u moet door het beoordelen van toepassingsvereisten Hallo bepalen. Elk VM-grootte heeft ook een limiet op Hallo aantal schijven dat kunt u toohello VM koppelen. Dit is meestal tweemaal Hallo aantal kernen. Zorg ervoor dat Hallo VM-grootte die u kiest, kan het aantal schijven nodig Hallo ondersteunen.

Vergeet niet Hallo Premium-opslag schijven hebben hogere prestaties tooStandard mogelijkheden ten opzichte van opslagschijven. Dus als u uw toepassing van Azure IaaS VM standaardopslag tooPremium opslag gebruiken migreert, moet u waarschijnlijk minder premium-schijven tooachieve Hallo dezelfde of een hogere prestaties voor uw toepassing.

## <a name="disk-caching"></a>Schijfcache
Maximale schaal virtuele machines die gebruikmaken van Azure Premium-opslag hebben een meerlaagse caching-technologie BlobCache aangeroepen. BlobCache gebruikt een combinatie van Hallo RAM voor virtuele Machine en de lokale SSD voor opslaan in cache. Deze cache is beschikbaar voor permanente Hallo Premium-opslag-schijven en Hallo VM lokale schijven. Deze cache-instelling is standaard ingesteld tooRead schrijftijd voor OS-schijven en alleen-lezen voor gegevensschijven gehost op Premium-opslag. Met de schijfcache is ingeschakeld op Hallo Premium-opslag-schijven, kunt Hallo grootschalige virtuele machines zeer hoge prestatieniveaus die groter is dan de onderliggende schijfprestaties Hallo bereiken.

> [!WARNING]
> Wijzigen van Hallo cache-instelling van een Azure-schijf wordt losgekoppeld en opnieuw toegevoegd Hallo doelschijf is. Als het Hallo-besturingssysteemschijf, kan Hallo VM opnieuw wordt opgestart. Stop alle toepassingen en services die kunnen worden beïnvloed door deze onderbreking voordat u Hallo schijfcache-instelling wijzigt.
>
>

toolearn meer informatie over hoe BlobCache werkt, raadpleegt u toohello binnen [Azure Premium-opslag](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/) blogbericht.

Het is belangrijk tooenable cache op de juiste set Hallo van schijven. Of u moet inschakelen schijfcache op een schijf premium of niet hangen af van Hallo werkbelasting patroon die schijf verwerkt. De volgende tabel ziet u de Hallo standaard cache-instellingen voor het besturingssysteem en gegevensschijven.

| **Schijftype** | **Standaardinstelling voor Cache** |
| --- | --- |
| Besturingssysteemschijf |ReadWrite |
| Gegevensschijf |Geen |

Hieronder worden aanbevolen schijf cache-instellingen voor gegevensschijven, Hallo

| **Instelling van de schijfcache** | **Aanbeveling als toouse deze instelling** |
| --- | --- |
| Geen |Host-cache configureren als geen voor de alleen-schrijven en schrijven zware schijven. |
| Alleen-lezen |Host-cache configureren als alleen-lezen voor alleen-lezen en alleen-lezen-schijven. |
| ReadWrite |Host-cache configureren zoals ReadWrite alleen als uw toepassing op correcte wijze schrijven in de cache toopersistent gegevensschijven opgeslagen wanneer deze nodig is. |

*Alleen-lezen*  
U kunt door ReadOnly cachegebruik op Premium-opslag gegevens schijven te configureren, lage latentie voor lezen bereiken en zeer hoge lezen IOPS en Doorvoerlimieten ophalen voor uw toepassing. Dit is vanwege twee redenen

1. Leesbewerkingen uitvoeren vanuit cache, die zich op Hallo VM geheugen en de lokale SSD, zijn veel sneller dan leesbewerkingen van de gegevensschijf hello, die zich op Hallo Azure blob-opslag.  
2. Premium-opslag telt niet mee Hallo leesbewerkingen geleverd vanuit cache, naar Hallo schijf-IOPS en doorvoer. Uw toepassing is daarom kunnen tooachieve hogere totale IOP's en doorvoer.

*ReadWrite*  
Hallo OS schijven hebben standaard ReadWrite cachebewerkingen ingeschakeld. Ondersteuning voor cachegebruik op gegevens ook schijven ReadWrite onlangs toegevoegd. Als u van ReadWrite in cache opslaan gebruikmaakt, moet u een goede manier toowrite Hallo gegevens uit de cache toopersistent schijven hebben. Bijvoorbeeld, schrijven van SQL Server-ingangen in cache opgeslagen gegevens toohello permanente opslagschijven op een eigen. ReadWrite cache gebruiken met een toepassing die niet persistent maken Hallo verwerkt vereist gegevens toodata verloren zijn gegaan, kan leiden als Hallo VM vastloopt.

Als u bijvoorbeeld kunt u deze richtlijnen tooSQL Server toepassen uitgevoerd op de Premium-opslag door Hallo-volgende te doen

1. 'ReadOnly' cache configureren op de premium-opslag-schijven die als host fungeert voor gegevensbestanden.  
   a.  Hallo snelle leest uit cache lagere Hallo SQL Server-query-tijd omdat data-pagina's uit Hallo cache vergeleken toodirectly van gegevensschijven Hallo veel sneller worden opgehaald.  
   b.  Leesbewerkingen uit cache verstrekken, betekent dat er is meer doorvoer van gegevensschijven premium beschikbaar. SQL Server kan gebruikmaken van deze extra doorvoer naar meer data-pagina's en andere bewerkingen zoals back-up/herstel ophalen, batch-belastingen en index wordt opnieuw gemaakt.  
2. Configureer 'None' cache op premium-opslag schijven hosting Hallo-logboekbestanden.  
   a.  Logboekbestanden hebben voornamelijk schrijven zware bewerkingen. Ze kunnen daarom niet gebruikmaken van Hallo ReadOnly-cache.

## <a name="disk-striping"></a>Striping van de schijf
Wanneer een grootschalige die virtuele machine is gekoppeld met verschillende premium permanente opslagschijven, Hallo schijven kan worden striped samen tooaggregate hun IOP's, bandbreedte en opslagcapaciteit.

Op Windows, kunt u schijven met opslagruimten toostripe samen gebruiken. U moet één kolom voor elke schijf in een pool configureren. Anders kunt hello algehele prestaties van striped volumes lager zijn dan verwacht vanwege toouneven distributie van verkeer over Hallo-schijven.

Belangrijk: Met Server Manager UI, kunt u Hallo kunt u het totale aantal kolommen van too8 voor striped volumes instellen. Bij het toevoegen van meer dan 8 schijven, gebruikt u PowerShell toocreate Hallo volume. Met behulp van PowerShell, kunt u instellen Hallo aantal kolommen gelijk toohello aantal schijven. Bijvoorbeeld, als er 16 schijven in een stripeset één; 16 kolommen opgeven in Hallo *NumberOfColumns* parameter Hallo *New-VirtualDisk* PowerShell-cmdlet.

Op Linux, Hallo MDADM hulpprogramma toostripe schijven samen te gebruiken. Voor gedetailleerde stappen op de schijven striping van Linux te verwijzen[Software-RAID configureren op Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

*Stripe-grootte*  
Een belangrijke configuratie in striping van de schijf is Hallo stripe-grootte. Hallo stripe-grootte of blokgrootte is de kleinste chunk Hallo van gegevens die van toepassing op striped volumes kunt oplossen. Hallo stripe grootte die u configureert, is afhankelijk van Hallo type toepassing en de aanvraag-patroon. Als u Hallo verkeerde stripe-grootte kiest, kan dit ertoe leiden tooIO uitlijning van gegevenstypen, wat toodegraded prestaties van uw toepassing leidt.

Bijvoorbeeld, als een i/o-aanvraag die is gegenereerd door de toepassing groter dan de schijfgrootte stripe hello is, schrijft Hallo opslagsysteem deze over stripe eenheid grenzen op meer dan één schijf. Wanneer het is tijd tooaccess die gegevens hebt deze tooseek in meer dan één stripe eenheden toocomplete Hallo-aanvraag. Hallo cumulatieve effect van dit gedrag kan toosubstantial prestatievermindering leiden. Daarentegen als Hallo grootte voor i/o-aanvraag kleiner dan stripe-grootte is en als het willekeurig, Hallo i/o-aanvragen op Hallo dezelfde optellen kunnen schijf op Hallo een knelpunt veroorzaakt en uiteindelijk Hallo i/o-prestaties beïnvloeden.

Afhankelijk van het soort werkbelasting Hallo uw toepassing wordt uitgevoerd, kies een passende stripe-grootte. Gebruik een kleinere stripe voor willekeurige kleine i/o-aanvragen. Terwijl voor grote opeenvolgende i/o-aanvragen stripe groter gebruiken. Ontdek Hallo stripe aanbevelingen voor de grootte voor de toepassing hello dat u uitvoert op Premium-opslag. Configureer stripe-grootte van 64KB voor OLTP-werkbelastingen en 256KB voor magazijnbeheer werkbelastingen van gegevens voor SQL Server. Zie [best practices prestaties for SQL Server op Azure Virtual machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md#disks-guidance) toolearn meer.

> [!NOTE]
> U kunt stripe samen een maximum van 32 premium-opslag-schijven op een DS-serie VM en 64 premium-opslag-schijven op een GS-serie VM.
>
>

## <a name="multi-threading"></a>Multithreading
Azure heeft Premium-opslag platform toobe massively parallelle ontworpen. Een toepassing met meerdere threads realiseert daarom veel hogere prestaties dan een toepassing met één thread. Een toepassing met meerdere threads zijn taken opgesplitst in meerdere threads en verhoogt de efficiëntie van de uitvoering door met Hallo VM en schijf resources toohello maximum.

Bijvoorbeeld, als uw toepassing wordt uitgevoerd op één kern VM met twee threads, kunt Hallo CPU schakelen tussen Hallo twee threads tooachieve efficiëntie. Terwijl een thread op een schijf-i/o-toocomplete wacht, kunt Hallo CPU schakelen toohello andere thread. Op deze manier doen twee threads meer dan één thread zou. Als Hallo VM meer dan één kern heeft, sneller het verdere uitgevoerd omdat elke core parallel taken kunt uitvoeren.

U mogelijk niet kunnen toochange Hallo manier een gebruiksklare toepassing wordt geïmplementeerd op een enkele thread of multithreading. SQL Server is bijvoorbeeld geschikt is voor het verwerken van meerdere CPU en meerdere kernen. SQL Server besluit echter onder welke omstandigheden wordt deze gebruikmaken van een of meer threads tooprocess een query. Het kan query's uitvoeren en bouwen indexen met multithreading. SQL Server gebruikt voor een query waarbij grote tabellen koppelen en gegevens worden gesorteerd voordat er wordt teruggekeerd toohello gebruiker, waarschijnlijk meerdere threads. Een gebruiker kan echter niet instellen of SQL Server wordt uitgevoerd een query met een enkele thread of meerdere threads.

Er zijn configuratie-instellingen die u en tooinfluence dit multithreading of een parallelle wijzigen kunt verwerking van een toepassing. In geval van SQL Server is het bijvoorbeeld Hallo maximale mate van parallelle uitvoering configuratie. Deze instelling aangeroepen MAXDOP, kunt u tooconfigure Hallo maximum aantal processors SQL Server gebruiken kunt bij het parallel verwerken. U kunt MAXDOP voor afzonderlijke query's of indexbewerkingen configureren. Dit is nuttig wanneer u toobalance resources van uw systeem voor een kritieke toepassing prestaties wenst.

Stel dat uw toepassing met behulp van SQL Server wordt uitgevoerd een grote query en een indexbewerking Hallo hetzelfde moment. Laat het ons wordt ervan uitgegaan dat u deze Hallo index bewerking toobe meer zodat vergeleken toohello grote query wilde. In dat geval kunt u MAXDOP waarde van de index opnieuw toobe Hallo hoger is dan Hallo MAXDOP waarde voor Hallo query instellen. Op deze manier SQL Server heeft meer aantal processors dat deze kan gebruikmaken van voor Hallo index bewerking vergeleken toohello aantal processors deze kan besteden toohello grote query. Denk eraan dat u het aantal threads dat SQL Server wordt gebruikt voor elke bewerking Hallo zijn niet van invloed. U kunt bepalen Hallo kunt u het maximum aantal processors worden toegewezen voor multithreading.

Meer informatie over [graden van parallelle uitvoering](https://technet.microsoft.com/library/ms188611.aspx) in SQL Server. Ontdek dergelijke instellingen die van invloed zijn op multithreading in uw toepassing en de prestaties van de toooptimize configuraties.

## <a name="queue-depth"></a>Wachtrijdiepte
Hallo wachtrijdiepte of wachtrijlengte of grootte van de wachtrij is Hallo aantal openstaande i/o-aanvragen in Hallo-systeem. Hallo-waarde van wachtrijdiepte bepaalt hoeveel i/o bewerkingen uw toepassing lijnen kunt, welke opslagschijven hello wordt verwerkt. Het is van invloed op alle Hallo drie toepassing prestatie-indicatoren die is besproken in dit artikel te weten, IOPS, doorvoer en latentie.

Wachtrij diepte en multithreading zijn nauw verwant zijn. Hallo wachtrijdiepte waarde geeft aan hoeveel multithreading kan worden bereikt door Hallo-toepassing. Als Hallo wachtrijdiepte groot is, toepassing gelijktijdig kan worden uitgevoerd meer bewerkingen, met andere woorden, meer multithreading. Als Hallo wachtrijdiepte klein is, zelfs als de toepassing met meerdere threads is, heeft dit niet voldoende aanvragen voor gelijktijdige uitvoering uitgelijnd.

Normaal gesproken uit Hallo rek toepassingen staan geen u wachtrijdiepte toochange hello, omdat als onjuist voert deze bewerkingen meer schade dan goed is ingesteld. Toepassingen wordt ingesteld Hallo Rechterwaarde van wachtrijdiepte tooget Hallo optimale prestaties. Echter, het is belangrijk toounderstand dit concept, zodat voor het oplossen van prestatieproblemen met uw toepassing. U kunt ook Hallo gevolgen van het wachtrijdiepte zien door met het uitvoeren van benchmarking's op uw systeem.

Sommige toepassingen bieden instellingen tooinfluence Hallo wachtrijdiepte. Bijvoorbeeld, Hallo MAXDOP (maximale graad van parallelle uitvoering) instelling in SQL Server worden beschreven in de vorige sectie. MAXDOP is een manier tooinfluence wachtrijdiepte en multithreading, hoewel deze Hallo wachtrijdiepte waarde van SQL Server niet rechtstreeks wijzigen.

*Hoge wachtrijdiepte*  
Een hoge wachtrijdiepte meer bewerkingen op Hallo schijf wordt uitgelijnd. Hallo schijf kent de volgende aanvraag Hallo in de wachtrij tevoren. Als gevolg daarvan kan Hallo schijf bewerkingen tevoren plannen en op een optimale wijze worden verwerkt. Sinds de toepassing hello verzendt meer aanvragen toohello schijf, kan Hallo schijf meer parallelle IOs verwerken. Uiteindelijk worden Hallo toepassing kunnen tooachieve hogere IOPS. Sinds de toepassing meer aanvragen verwerkt, verhoogt hello totale doorvoer van de toepassing hello ook de.

Normaal gesproken een toepassing kunt bereiken van maximale doorvoer met 8-16 + openstaande IO's per gekoppelde schijf. Als een wachtrijdiepte een toepassing is niet voldoende IOs toohello system pushen en minder hoeveelheid in een bepaalde periode wordt verwerkt. Met andere woorden, minder doorvoer.

Bijvoorbeeld, in SQL Server, instelling Hallo MAXDOP waarde voor een query te "4" informeert het SQL-Server die van toofour kernen tooexecute Hallo query kan worden gebruikt. SQL Server bepaalt wat de beste wachtrijdiepte waarde en Hallo aantal kernen voor het uitvoeren van de query Hallo is.

*Optimale wachtrijdiepte*  
Zeer hoge wachtrijdiepte waarde heeft ook de nadelen. Als de wachtrijdiepte waarde is te hoog, toepassing hello toodrive geprobeerd zeer hoge IOPS. Tenzij de toepassing heeft permanente schijven met voldoende ingerichte IOP's, kan dit toepassingslatenties negatief beïnvloeden. Volgende formule toont Hallo relatie tussen IOP's, latentie en wachtrijdiepte.  
    ![](media/storage-premium-storage-performance/image6.png)

U moet de wachtrijdiepte tooany hoge waarde, maar de optimale waarde tooan, die voldoende IOPS voor Hallo toepassing kan leveren zonder latenties niet configureren. Bijvoorbeeld, als Hallo application latentie toobe 1 milliseconde moet, Hallo wachtrijdiepte vereist tooachieve 5000 IOP's is, Wachtrijdiepte = 5000 x 0,001 = 5.

*Wachtrijdiepte voor Striped volumes*  
Voor een striped volume een hoog genoeg wachtrijdiepte te onderhouden zodat elke schijf een piek wachtrijdiepte afzonderlijk heeft. Neem bijvoorbeeld een toepassing die een wachtrijdiepte van 2 pushes en er zijn 4 schijven in Hallo streep. Hallo twee i/o-aanvragen gaat tootwo schijven en niet-actieve resterende van twee schijven zijn. Daarom Hallo wachtrijdiepte configureren zodat alle Hallo schijven kunnen bezet zijn. Formule hieronder ziet u hoe toodetermine Hallo wachtrijdiepte van striped volumes.  
    ![](media/storage-premium-storage-performance/image7.png)

## <a name="throttling"></a>Beperking
Azure Premium-opslag voorziet in een opgegeven aantal IOPS en Doorvoerlimieten afhankelijk van de VM-grootten Hallo en schijfgrootten die u kiest. Telkens wanneer uw toepassing toodrive IOPS of doorvoer boven deze limieten probeert van welke Hallo VM of de schijf kan verwerken, wordt het Premium-opslag vertraging. Dit manifesten in de vorm Hallo van verminderde prestaties in uw toepassing. Dit kan betekenen hogere latentie, doorvoer verlagen of IOPS verlagen. Als Premium-opslag niet beperken biedt, wordt uw toepassing kan volledig mislukt door meer dan wat de daarbij behorende bronnen zijn geschikt om dat te bereiken. Dus tooavoid prestaties vanwege problemen met toothrottling, altijd inrichten voldoende bronnen zijn voor uw toepassing. In overweging nemen we in Hallo VM-grootten en schijf grootten hierboven besproken. De beste manier toofigure Hallo benchmarking is welke bronnen moet u toohost uw toepassing.

## <a name="benchmarking"></a>Benchmarking
Benchmarking is Hallo proces simuleren van andere werkbelastingen op uw toepassing en de toepassingsprestaties Hallo voor elke werkbelasting te meten. Hallo-stappen die worden beschreven in de vorige sectie hebt u Hallo toepassing prestatie-eisen verzameld. Door het uitvoeren van hulpprogramma's op Hallo virtuele machines die als host fungeert voor de toepassing hello benchmarking, kunt u bepalen Hallo prestatieniveaus die uw toepassing met Premium-opslag bereiken kunt. In deze sectie bieden we u voorbeelden van benchmarks van een standaard DS14 VM ingericht met Azure Premium-opslag-schijven.

We hebben respectievelijk Iometer en FIO, algemene benchmarking's gebruikt voor Windows en Linux. Deze hulpprogramma's starten meerdere threads simuleren een productie-achtige werkbelasting en meting Hallo systeemprestaties. U kunt ook een parameters zoals blok grootte en wachtrij diepte die u normaal gesproken niet voor een toepassing wijzigen configureren met de Hallo-hulpprogramma's. Hiermee krijgt u meer flexibiliteit toodrive Hallo maximale prestaties op een grootschalige virtuele machine die zijn ingericht met premium-schijven voor verschillende soorten toepassingsworkloads. meer informatie over elk benchmarking hulpprogramma vindt u toolearn [Iometer](http://www.iometer.org/) en [FIO](http://freecode.com/projects/fio).

toofollow hello voorbeelden hieronder, een standaard DS14 VM maken en koppelen van 11 Premium-opslag schijven toohello VM. Hallo 11 schijven 10 schijven configureren met hostcaching als 'Geen' en stripe ze naar een volume NoCacheWrites aangeroepen. Hostcaching als 'ReadOnly' op de resterende schijf Hallo configureren en een volume CacheReads aangeroepen met deze schijf maken. Met deze instellingen, kunt u zich kunt toosee Hallo maximale lezen en schrijven prestaties van een standaard DS14 virtuele machine. Voor gedetailleerde stappen voor het maken van een VM DS14 met premium-schijven gaat te[maken en gebruiken een Premium-opslag-account voor een virtuele machine gegevensschijf](storage-premium-storage.md).

*Opwarmen van Cache Hallo*  
Hallo-schijf met alleen-lezen-hostcaching kunnen toogive worden hogere IOPS dan Hallo schijf limiet. tooget dit maximum lezen prestaties uit Hallo host cache, u moet eerst oefenen cache op Hallo van deze schijf. Dit zorgt ervoor dat Hallo lezen IOs welke benchmarking hulpprogramma op CacheReads volume veranderingen daadwerkelijk treffers Hallo-cache en niet Hallo rechtstreeks. Hallo cache treffers leiden tot extra IOP's uit één cache Hallo schijf ingeschakeld.

> **Belangrijk:**  
> U moet Hallo cache opgewarmd voordat benchmarking, wordt uitgevoerd telkens wanneer de VM opnieuw wordt opgestart.
>
>

#### <a name="iometer"></a>Iometer
[Download Hallo Iometer hulpprogramma](http://sourceforge.net/projects/iometer/files/iometer-stable/2006-07-27/iometer-2006.07.27.win32.i386-setup.exe/download) op Hallo VM.

*Testbestand*  
Iometer maakt gebruik van een testbestand dat is opgeslagen op Hallo volume waarop u Hallo benchmarking test wordt uitgevoerd. Deze stations leesbewerkingen en schrijfbewerkingen op deze test bestand toomeasure Hallo schijf IOPS en doorvoer. Iometer maakt deze testbestand als u deze niet hebt opgegeven. Een bestand voor het testen van 200GB iobw.tst aangeroepen op Hallo CacheReads en NoCacheWrites volumes maken.

*Toegangsspecificaties*  
Hallo-specificaties, aanvragen i/o-grootte, % lezen/schrijven, willekeurige/sequentiële % zijn geconfigureerd met Hallo 'toegangsspecificaties' tabblad in Iometer. Maakt een access-specificatie voor elk Hallo scenario's die hieronder worden beschreven. Maak Hallo toegangsspecificaties en 'Opgeslagen' met een geschikte naam zoals – RandomWrites\_8 kB, RandomReads\_8 kB. Selecteer overeenkomende specificatie Hallo bij het uitvoeren van testscenario Hallo.

Een voorbeeld van de toegangsspecificaties voor maximale IOPS schrijven scenario wordt hieronder weergegeven  
    ![](media/storage-premium-storage-performance/image8.png)

*Maximale IOPS Test specificaties*  
toodemonstrate maximale IOPs, kleinere aanvraag gebruiken. Gebruik van 8 kB aangevraagde grootte en maak specificaties voor willekeurige geschreven en gelezen.

| Specificatie toegang | De aanvraaggrootte van de | Willekeurige % | % Lezen |
| --- | --- | --- | --- |
| RandomWrites\_8 kB |8 KB |100 |0 |
| RandomReads\_8 kB |8 KB |100 |100 |

*Maximale doorvoer Test specificaties*  
toodemonstrate maximale doorvoer, groter aanvraag voor gebruik. De grootte van 64K aanvraag gebruiken en specificaties voor willekeurige schrijfbewerkingen en leesbewerkingen maken.

| Specificatie toegang | De aanvraaggrootte van de | Willekeurige % | % Lezen |
| --- | --- | --- | --- |
| RandomWrites\_64 kB |64 KB |100 |0 |
| RandomReads\_64 kB |64 KB |100 |100 |

*Hallo Iometer Test uitgevoerd*  
Onderstaande toowarm cache Hallo stappen uitvoeren

1. Twee toegangsspecificaties maken met de onderstaande waarden,

   | Naam | De aanvraaggrootte van de | Willekeurige % | % Lezen |
   | --- | --- | --- | --- |
   | RandomWrites\_1 MB |1MB |100 |0 |
   | RandomReads\_1 MB |1MB |100 |100 |
2. Hallo Iometer test voor het initialiseren van de cache-schijf met de volgende parameters worden uitgevoerd. Drie werkthreads gebruiken voor het doelvolume Hallo en een wachtrijdiepte van 128. Stel Hallo 'Uitvoeren tijd' duur van Hallo test too2hrs op Hallo 'Setup testen' tabblad.

   | Scenario | Doelvolume | Naam | Duur |
   | --- | --- | --- | --- |
   | Initialiseer de schijf Cache |CacheReads |RandomWrites\_1 MB |2hrs |
3. Hallo Iometer test voor het opwarmen van cache-schijf met de volgende parameters worden uitgevoerd. Drie werkthreads gebruiken voor het doelvolume Hallo en een wachtrijdiepte van 128. Stel Hallo 'Uitvoeren tijd' duur van Hallo test too2hrs op Hallo 'Setup testen' tabblad.

   | Scenario | Doelvolume | Naam | Duur |
   | --- | --- | --- | --- |
   | Warme van Cache-schijf |CacheReads |RandomReads\_1 MB |2hrs |

Nadat de cache-schijf is opgewarmd, doorgaan met de onderstaande Testscenario's Hallo. toorun hello Iometer testen, gebruikt u ten minste drie worker threads voor **elke** volume als doel. Voor elke werkthread Hallo doelvolume selecteert, wachtrijdiepte ingesteld en selecteert u een van de test-specificaties Hallo opgeslagen, zoals weergegeven in de tabel Hallo hieronder toorun Hallo bijbehorende test-scenario. Hallo tabel toont ook verwachte resultaten voor IOPS en Doorvoerlimieten bij het uitvoeren van deze tests. Voor alle scenario's is een kleine i/o-grootte van 8KB en een hoge wachtrijdiepte van 128 gebruikt.

| Testscenario | Doelvolume | Naam | Resultaat |
| --- | --- | --- | --- |
| Met maximaal Lees IOP 's |CacheReads |RandomWrites\_8 kB |50.000 IOP 'S |
| Met maximaal IOPS schrijven |NoCacheWrites |RandomReads\_8 kB |64.000 IOP 'S |
| Met maximaal Gecombineerde IOP 's |CacheReads |RandomWrites\_8 kB |100.000 IOP 'S |
| NoCacheWrites |RandomReads\_8 kB | &nbsp; | &nbsp; |
| Met maximaal Lees MB per seconde |CacheReads |RandomWrites\_64 kB |524 MB per seconde |
| Met maximaal Schrijven van MB per seconde |NoCacheWrites |RandomReads\_64 kB |524 MB per seconde |
| Gecombineerde MB per seconde |CacheReads |RandomWrites\_64 kB |1000 MB per seconde |
| NoCacheWrites |RandomReads\_64 kB | &nbsp; | &nbsp; |

Hieronder vindt u schermafbeeldingen Hallo Iometer testresultaten voor gecombineerde IOPS en Doorvoerlimieten scenario's.

*Gecombineerde lees- en schrijfbewerkingen maximumaantal IOPS*  
![](media/storage-premium-storage-performance/image9.png)

*Gecombineerde lees- en schrijfbewerkingen maximale doorvoer*  
![](media/storage-premium-storage-performance/image10.png)

### <a name="fio"></a>FIO
FIO is een populair hulpprogramma toobenchmark opslag op Hallo virtuele Linux-machines. Heeft Hallo flexibiliteit tooselect verschillende i/o-grootte, sequentiële of willekeurige lees- en schrijfbewerkingen. Hiermee wordt het werkthreads of processen tooperform Hallo opgegeven i/o-bewerkingen. U kunt opgeven dat Hallo-type van i/o-bewerkingen die elke werkthread moet uitvoeren met behulp van taakbestanden. Een taakbestand per scenario geïllustreerd in de onderstaande Hallo voorbeelden is gemaakt. Hallo-specificaties in deze taak bestanden toobenchmark verschillende workloads die worden uitgevoerd op de Premium-opslag, kunt u wijzigen. In de voorbeelden hello, gebruiken we een actieve standaard DS 14 VM **Ubuntu**. Gebruik Hallo dezelfde instellingen die zijn beschreven in Hallo begin Hallo [sectie Benchmarking](#Benchmarking) en warme Hallo cache voordat Hallo benchmarking tests wordt uitgevoerd.

Voordat u begint, [FIO downloaden](https://github.com/axboe/fio) en installeer deze op uw virtuele machine.

Na de opdracht voor Ubuntu, Hallo uitvoeren

```
apt-get install fio
```

We gebruiken vier werkthreads voor het besturen van schrijfbewerkingen en vier werkthreads voor aangedreven leesbewerkingen op Hallo-schijven. Hallo schrijven werknemers wordt worden volledig verkeer op Hallo 'nocache"volume 10 schijven met cache te ingesteld heeft 'None'. Hallo lezen werknemers zal worden volledig verkeer op Hallo 'readcache' volume 1 schijf met cache set te heeft 'ReadOnly'.

*Maximale schrijven IOP 's*  
Hallo taakbestand maken met de volgende specificaties tooget maximumaantal IOPS schrijven. Geef deze de naam 'fiowrite.ini'.

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[writer1]
rw=randwrite
directory=/mnt/nocache
[writer2]
rw=randwrite
directory=/mnt/nocache
[writer3]
rw=randwrite
directory=/mnt/nocache
[writer4]
rw=randwrite
directory=/mnt/nocache
```

Opmerking Hallo Volg belangrijke dingen die in overeenstemming met de Hallo ontwerprichtlijnen in de vorige secties beschreven zijn. Deze specificaties zijn essentieel toodrive maximumaantal IOPS  

* Een hoge wachtrijdiepte van 256.  
* Een kleine blokgrootte van 8KB.  
* Meerdere threads uitvoeren van willekeurige schrijfbewerkingen.

Hallo opdracht tookick uit Hallo FIO testen gedurende 30 seconden na uitvoeren  

```
sudo fio --runtime 30 fiowrite.ini
```

Tijdens het Hallo-test wordt uitgevoerd, kunt u zich kunt toosee Hallo aantal schrijven van IOPS Hallo VM- en Premium-schijven leveren. Zoals u in onderstaande Hallo-voorbeeld, is de maximale IOPS-limiet van 50.000 IOPS-schrijven leveren van Hallo DS14 VM.  
    ![](media/storage-premium-storage-performance/image11.png)

*Maximale lezen IOP 's*  
Hallo taakbestand maken met de volgende specificaties tooget maximumaantal IOPS op lezen. Geef deze de naam 'fioread.ini'.

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache
```

Opmerking Hallo Volg belangrijke dingen die in overeenstemming met de Hallo ontwerprichtlijnen in de vorige secties beschreven zijn. Deze specificaties zijn essentieel toodrive maximumaantal IOPS

* Een hoge wachtrijdiepte van 256.  
* Een kleine blokgrootte van 8KB.  
* Meerdere threads uitvoeren van willekeurige schrijfbewerkingen.

Hallo opdracht tookick uit Hallo FIO testen gedurende 30 seconden na uitvoeren

```
sudo fio --runtime 30 fioread.ini
```

Tijdens het Hallo-test wordt uitgevoerd, kunt u zich kunt toosee Hallo aantal gelezen IOPS Hallo VM en leveren van Premium-schijven. Zoals u in onderstaande Hallo-voorbeeld, levert Hallo DS14 VM maximaal 64.000 lezen IOPS. Dit is een combinatie van Hallo schijf en Hallo cache prestaties.  
    ![](media/storage-premium-storage-performance/image12.png)

*Maximale lezen en schrijven IOP 's*  
Maak Hallo taakbestand met de volgende specificaties tooget maximale gecombineerde lezen en schrijven IOPS. Geef deze de naam 'fioreadwrite.ini'.

```
[global]
size=30g
direct=1
iodepth=128
ioengine=libaio
bs=4k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache

[writer1]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer2]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer3]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer4]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
```

Opmerking Hallo Volg belangrijke dingen die in overeenstemming met de Hallo ontwerprichtlijnen in de vorige secties beschreven zijn. Deze specificaties zijn essentieel toodrive maximumaantal IOPS

* Een hoge wachtrijdiepte van 128.  
* Een kleine blokgrootte van 4KB.  
* Meerdere threads uitvoeren van willekeurige leest en schrijft.

Hallo opdracht tookick uit Hallo FIO testen gedurende 30 seconden na uitvoeren

```
sudo fio --runtime 30 fioreadwrite.ini
```

Tijdens het Hallo-test wordt uitgevoerd, wordt u kunnen toosee Hallo aantal gecombineerde lezen en schrijven IOPS Hallo VM en leveren van Premium-schijven. Zoals u in onderstaande Hallo-voorbeeld, levert Hallo DS14 VM meer dan 100.000 gecombineerde lezen en schrijven IOP's. Dit is een combinatie van Hallo schijf en Hallo cache prestaties.  
    ![](media/storage-premium-storage-performance/image13.png)

*Maximale gecombineerde doorvoer*  
tooget Hallo maximale gecombineerde lezen en schrijven doorvoer, gebruikt een grotere blok en grote wachtrijdiepte met meerdere threads uitvoeren van lees- en schrijfbewerkingen. U kunt een blokgrootte van 64KB en wachtrijdiepte van 128.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Azure Premium-opslag:

* [Premium Storage: opslag met hoge prestaties voor de werkbelasting van virtuele Azure-machines](storage-premium-storage.md)  

Lees de artikelen over aanbevolen procedures voor prestaties voor SQL Server voor SQL Server-gebruikers:

* [Best Practices prestaties for SQL Server in Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)
* [Azure Premium-opslag biedt de beste prestaties voor SQL Server in Azure VM](http://blogs.technet.com/b/dataplatforminsider/archive/2015/04/23/azure-premium-storage-provides-highest-performance-for-sql-server-in-azure-vm.aspx)
