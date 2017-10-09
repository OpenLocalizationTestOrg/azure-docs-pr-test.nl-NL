---
title: overzicht van benchmarks van aaaAzure SQL-Database
description: Dit onderwerp beschrijft hello Azure SQL Database Benchmark in het meten van de prestaties van Azure SQL Database Hallo gebruikt.
services: sql-database
documentationcenter: na
author: jan-eng
manager: jhubbard
editor: monicar
ms.assetid: e26f8a66-2c12-49d7-8297-45b4d48a5c01
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/21/2016
ms.author: janeng
ms.openlocfilehash: 1024e9ada511935f911cb1345b4dc5508997c702
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-benchmark-overview"></a>Overzicht van Azure SQL Database-benchmark
## <a name="overview"></a>Overzicht
Microsoft Azure SQL Database biedt drie [Servicelagen](sql-database-service-tiers.md) met meerdere prestatieniveaus. Elke prestatieniveau biedt een set resources of 'inschakelen', ontworpen toodeliver steeds sneller de doorvoer te verhogen.

Het is belangrijk toobe kunnen tooquantify hoe Hallo toenemende power van elke prestatieniveau in verbeterde databaseprestaties zet. Deze Microsoft heeft ontwikkeld toodo hello Azure SQL Database Benchmark (ASDB). Hallo benchmark oefent een combinatie van basisbewerkingen gevonden in alle OLTP-werkbelastingen. We meten Hallo doorvoer voor databases die worden uitgevoerd op elk prestatieniveau worden gerealiseerd.

Hallo bronnen en kracht van elke prijscategorie en prestatieniveau serviceniveau worden uitgedrukt in termen van ['s (Database Transaction Units)](sql-database-what-is-a-dtu.md). Dtu's bieden een manier toodescribe Hallo relatieve capaciteit van een prestatieniveau op basis van een gecombineerde meting van CPU, geheugen, en lezen en schrijven van tarieven die worden aangeboden door elke prestatieniveau. Hallo DTU classificatie van een database verdubbeling toodoubling Hallo database power is gelijk. Hallo benchmark kan ons tooassess Hallo impact op de databaseprestaties Hallo power aangeboden op elk prestatieniveau door de werkelijke databasebewerkingen, tijdens het schalen van de databasegrootte, aantal gebruikers en transactie tarieven in verhouding uitoefenen verhogen toohello resources die worden geleverd toohello database.

Door uitdrukken Hallo doorvoer van Hallo Basic servicelaag met behulp van transacties per uur, Hallo standaard servicelaag met behulp van transacties per minuut en Hallo Premium servicecategorie transacties per seconde, maakt het eenvoudiger tooquickly Hallo gerelateerd de mogelijkheden van de prestaties van elke laag toohello vereisten van een toepassing.

## <a name="correlating-benchmark-results-tooreal-world-database-performance"></a>Databaseprestaties voor benchmark resultaten tooreal world correleren
Het is belangrijk toounderstand die ASDB, zoals alle benchmarks, is representatief en indicatief alleen. Hallo tarieven verkregen met Hallo benchmark toepassing niet hetzelfde als die kan worden verkregen met andere toepassingen wordt worden Hallo transactie. Hallo benchmark bestaat uit een verzameling van een andere transactie typen uitvoeren op een schema met een bereik van tabellen en gegevenstypen. Tijdens het Hallo benchmark oefeningen hello dezelfde basisbewerkingen uit die gangbare tooall OLTP-werkbelastingen zijn, vormt een specifieke klasse van de database of de toepassing niet meer. Hallo-doel van Hallo benchmark is een redelijke handleiding toohello relatieve prestaties van een database die kan worden verwacht voor het omhoog of omlaag schalen tussen prestatieniveaus tooprovide. Verschillende combinaties van werkbelastingen optreden en reageert op verschillende manieren in werkelijkheid databases zijn van verschillende grootte en complexiteit. Bijvoorbeeld, een i/o-intensieve toepassingen mogelijk sneller i/o-drempelwaarden bereikt of een toepassing CPU-intensief CPU-limieten sneller mogelijk bereikt. Er is geen garantie dat een bepaalde database kunnen worden geschaald in Hallo die dezelfde manier als voor Hallo benchmark onder een toenemende laden.

Hallo benchmark en de methodologie worden beschreven in meer detail hieronder.

## <a name="benchmark-summary"></a>Samenvatting van de benchmark
ASDB meet Hallo prestaties van een combinatie van basic databasebewerkingen waarvoor een treden het vaakst in online transactieverwerking (OLTP)-workloads. Hoewel Hallo benchmark is ontworpen met cloud computing in gedachten, is het databaseschema hello, vullen met gegevens en transacties ontworpen toobe grotendeels representatief van basiselementen Hallo meest worden gebruikt in een OLTP-werkbelastingen.

## <a name="schema"></a>Schema
Hallo-schema is ontworpen toohave voldoende diverse en complexiteit toosupport een breed scala aan bewerkingen. Hallo benchmark wordt uitgevoerd op basis van een database bestaat uit zes tabellen. Hallo-tabellen die zijn onderverdeeld in drie categorieën: vaste grootte, schaalbaarheid en groeit. Er zijn twee tabellen van vaste grootte. drie vergroten/verkleinen tabellen. en één groeiende tabel. Vaste grootte tabellen hebben een constant aantal rijen. Schalen tabellen hebben een kardinaliteit die evenredig toodatabase prestaties, maar niet wijzigen tijdens het Hallo-benchmark. Hallo groeiende tabel wordt aangepast als een vergroten/verkleinen tabel op de eerste keer wordt geladen, maar vervolgens Hallo kardinaliteit verandert in Hallo verloop van Hallo benchmark uitgevoerd als rijen worden ingevoegd of verwijderd.

Hallo schema bevat een combinatie van gegevenstypen, met inbegrip van geheel getal, numerieke tekens en datum/tijd. Hallo-schema bevat primaire en secundaire sleutels, maar geen refererende sleutels - dat wil zeggen, er zijn geen referentiële integriteitsbeperkingen tussen tabellen.

Een programma van de generatie gegevens genereert Hallo-gegevens voor de eerste Hallo-database. Geheel getal en numerieke gegevens wordt met verschillende strategieën gegenereerd. In sommige gevallen worden waarden willekeurig verdeeld over een bereik. In andere gevallen is een set waarden willekeurig gepermuteerde tooensure dat een specifiek distributiepunt behouden blijft. Tekstvelden worden gegenereerd vanuit een lijst met woorden tooproduce realistisch ogende gegevens.

Hallo-database wordt aangepast op basis van een 'schaalfactor'. Hallo schaalfactor (afgekort als SF) bepaalt Hallo kardinaliteit Hallo schalen en groeiende tabellen. Zoals hieronder wordt beschreven Hallo sectie gebruikers en Pacing, databasegrootte hello, het aantal gebruikers en de maximale prestaties alle schalen in verhouding tooeach andere.

## <a name="transactions"></a>Transacties
Hallo werkbelasting bestaat uit negen transactietypen, zoals weergegeven in onderstaande tabel voor Hallo. Elke transactie is ontworpen toohighlight een bepaalde set kenmerken in Hallo database-engine en system-hardware, Hallo met hoog contrast uit andere transacties. Deze aanpak is het eenvoudiger tooassess Hallo gevolgen van de verschillende onderdelen toooverall prestaties. Bijvoorbeeld wordt 'Zware lezen' Hallo-transactie een groot aantal leesbewerkingen van de schijf.

| Transactietype | Beschrijving |
| --- | --- |
| Lite lezen |SELECTEER; in het geheugen; alleen-lezen |
| Gemiddeld lezen |SELECTEER; voornamelijk in het geheugen; alleen-lezen |
| Lees zware |SELECTEER; meestal niet in het geheugen; alleen-lezen |
| Update Lite |UPDATE; in het geheugen; lezen / schrijven |
| Zware bijwerken |UPDATE; meestal niet in het geheugen; lezen / schrijven |
| INSERT Lite |INSERT; in het geheugen; lezen / schrijven |
| Zware invoegen |INSERT; meestal niet in het geheugen; lezen / schrijven |
| Verwijderen |VERWIJDEREN; combinatie van in het geheugen en niet in het geheugen; lezen / schrijven |
| CPU-zware |SELECTEER; in het geheugen; relatief intensief CPU-belasting; alleen-lezen |

## <a name="workload-mix"></a>Combinatie van de werkbelasting
Transacties zijn willekeurig geselecteerd uit een gewogen distributiepunt Hello volgen algemene combinatie. Hallo heeft algehele mix een verhouding lezen/schrijven van ongeveer 2:1.

| Transactietype | % van de combinatie |
| --- | --- |
| Lite lezen |35 |
| Gemiddeld lezen |20 |
| Lees zware |5 |
| Update Lite |20 |
| Zware bijwerken |3 |
| INSERT Lite |3 |
| Zware invoegen |2 |
| Verwijderen |2 |
| CPU-zware |10 |

## <a name="users-and-pacing"></a>Gebruikers- en pacing
Hallo benchmark werkbelasting wordt aangedreven vanuit een hulpprogramma waarmee transacties worden verzonden over een set verbindingen toosimulate Hallo gedrag van een aantal gelijktijdige gebruikers. Hoewel alle Hallo verbindingen en transacties machine gegenereerd zijn, voor het gemak verwezen toothese verbindingen als 'gebruikers'. Hoewel elke gebruiker onafhankelijk van alle andere gebruikers werkt, de Hallo voor het uitvoeren van alle gebruikers dezelfde cyclus van stappen hieronder weergegeven:

1. Een databaseverbinding tot stand brengen.
2. Herhaal totdat gesignaleerde tooexit:
   * Selecteer een transactie in willekeurige volgorde (uit een gewogen distributiepunt).
   * Hallo geselecteerd transactie en reactietijd van de meting Hallo uitvoeren.
   * Wachten op een pacing vertraging.
3. Hallo databaseverbinding verbreken.
4. Afsluiten.

Hallo vertraging (in stap 2c) pacing willekeurig is geselecteerd, maar met een distributiepunt die een gemiddelde van tweede 1.0 heeft. Elke gebruiker kan dus gemiddeld genereren voor maximaal één transactie per seconde.

## <a name="scaling-rules"></a>Regels voor vergroten/verkleinen
Hallo aantal gebruikers wordt bepaald door Hallo databasegrootte (in schaalfactor units). Er is een gebruiker voor elke vijf schaalfactor eenheden. Vanwege Hallo pacing vertraging, één gebruiker gemiddeld maximaal één transactie per seconde genereren.

Bijvoorbeeld, een scale-factor van 500 (SF = 500)-database heeft 100 gebruikers en een maximale snelheid van 100 TPS kunt bereiken. een hogere snelheid van TPS toodrive vereist meer gebruikers en een grotere database.

Hallo in de volgende tabel ziet u het aantal gebruikers daadwerkelijk aanhoudend voor elke prijscategorie en prestatieniveau serviceniveau Hallo.

| Servicelaag (prestatieniveau) | Gebruikers | Databaseomvang |
| --- | --- | --- |
| Basic |5 |720 MB |
| Standard (S0) |10 |1 GB |
| Standard (S1) |20 |2.1 GB |
| Standard (S2) |50 |7.1 GB |
| Premium (P1) |100 |14 GB |
| Premium (P2) |200 |28 GB |
| Premium (P6/P3) |800 |114 GB |

## <a name="measurement-duration"></a>Duur van de meting
Een geldig benchmark uitvoeren vereist een actieve status meting duur van ten minste één uur.

## <a name="metrics"></a>Metrische gegevens
Hallo belangrijkste metrische gegevens in Hallo benchmark zijn doorvoer en reactietijd.

* Doorvoer is Hallo essentiële prestatiemeting in Hallo benchmark. Doorvoer wordt vermeld in transacties per eenheid-van-time, waarbij alle transactietypen wordt geteld.
* Reactietijd is een meting van prestaties, voorspelbaarheid. Hallo antwoord tijdsbeperking verschillen afhankelijk van de klasse van de service met hogere klassen van de service met een strengere antwoord tijd vergt, zoals hieronder wordt weergegeven.

| Klasse van Service | Doorvoer meting | Antwoord tijd vergt |
| --- | --- | --- |
| Premium |Transacties per seconde |95e percentiel op 0,5 seconden |
| Standard |Transacties per minuut |90 percentiel op 1,0 seconden |
| Basic |Transacties per uur |80e percentiel op 2.0 seconden |

## <a name="conclusion"></a>Conclusie
Hello Azure SQL Database Benchmark meet Hallo relatieve prestaties van Azure SQL Database uitvoert via Hallo bereik van beschikbare Servicelagen en prestatieniveaus. Hallo benchmark oefent een combinatie van basic databasebewerkingen waarvoor een treden het vaakst in online transactieverwerking (OLTP)-workloads. Door het meten van de werkelijke prestaties biedt Hallo benchmark een duidelijker beoordeling van Hallo impact op de doorvoer van het wijzigen van het prestatieniveau Hallo dan mogelijk alleen aanbieding Hallo resources die worden geleverd op elk niveau zoals CPU-snelheid, geheugengrootte en IOP 's . In toekomstige hello, we gaan tooevolve Hallo benchmark toobroaden het bereik en vouw Hallo-gegevens die zijn opgegeven.

## <a name="resources"></a>Resources
[Inleiding tooSQL Database](sql-database-technical-overview.md)

[Servicelagen en prestatieniveaus](sql-database-service-tiers.md)

[Prestaties richtlijnen voor individuele databases](sql-database-performance-guidance.md)
