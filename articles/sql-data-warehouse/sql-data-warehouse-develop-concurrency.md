---
title: beheer van aaaConcurrency en de belasting in SQL Data Warehouse | Microsoft Docs
description: Begrijpen en de belasting van gelijktijdigheid management in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a>Beheer van gelijktijdigheid van taken en de belasting in SQL Data Warehouse
toodeliver voorspelbare prestaties op schaal, Microsoft Azure SQL Data Warehouse kunt u bepalen gelijktijdigheid niveaus en toewijzingen zoals geheugen en CPU-prioriteit. In dit artikel vindt u toohello concepten van gelijktijdigheid en werkbelasting management, waarin wordt uitgelegd hoe u beide functies geïmplementeerd en hoe u ze kunt beheren in uw datawarehouse. Beheer van SQL Data Warehouse werkbelasting is beoogde toohelp omgeving met meerdere gebruikers die u ondersteunt. Het is niet bedoeld voor werkbelastingen van meerdere tenants.

## <a name="concurrency-limits"></a>Limieten voor gelijktijdigheid van taken
SQL Data Warehouse kunt up too1, 024 gelijktijdige verbindingen. Alle 1024 verbindingen kunnen query's tegelijk verzenden. Toooptimize doorvoer, SQL Data Warehouse kan echter een aantal query's tooensure dat elke query een minimale geheugentoekenning ontvangt wachtrij. Queuing treedt op tijdens het uitvoeren van een query. Wanneer gelijktijdigheid limieten zijn bereikt, SQL Data Warehouse kunt verhogen nodig totale doorvoer door ervoor te zorgen dat de actieve query's toocritically toegang krijgen door queuing query's geheugenbronnen.  

Limieten voor gelijktijdigheid van taken worden bepaald door twee concepten: *gelijktijdige query's* en *gelijktijdigheid sleuven*. Moet in een tooexecute query uitvoeren in zowel Hallo query gelijktijdigheid limiet en Hallo gelijktijdigheid sleuf toewijzing.

* Gelijktijdige query's zijn Hallo query's uitvoeren op Hallo van dezelfde tijd. SQL Data Warehouse biedt ondersteuning voor maximaal too32 gelijktijdige query's op Hallo grotere DWU.
* Gelijktijdigheid sleuven worden toegewezen op basis van DWU. Elke DWU 100 biedt 4 gelijktijdigheid sleuven. Bijvoorbeeld, een DW100 toewijst 4 gelijktijdigheid sleuven en DW1000 40 toewijst. Elke query maakt gebruik van een of meer gelijktijdigheid sleuven, afhankelijk van Hallo [bronklasse](#resource-classes) van Hallo-query. Query uitvoeren in Hallo smallrc bronklasse één gelijktijdigheid sleuf in beslag nemen. Query uitvoeren in een hogere bronklasse verbruikt meer gelijktijdigheid sleuven.

Hallo volgende tabel beschrijft Hallo limieten voor gelijktijdige query's en gelijktijdigheid sleuven op Hallo verschillende grootten van DWU.

### <a name="concurrency-limits"></a>Limieten voor gelijktijdigheid van taken
| DWU | Maximum aantal gelijktijdige query 's | Gelijktijdigheid sleuven toegewezen |
|:--- |:---:|:---:|
| DW100 |4 |4 |
| DW200 |8 |8 |
| DW300 |12 |12 |
| DW400 |16 |16 |
| DW500 |20 |20 |
| DW600 |24 |24 |
| DW1000 |32 |40 |
| DW1200 |32 |48 |
| DW1500 |32 |60 |
| DW2000 ZIJN |32 |80 |
| DW3000 |32 |120 |
| DW6000 |32 |240 |

Als een van deze drempels wordt voldaan, worden de nieuwe query's in de wachtrij en de eerste in, First-out ' op basis van een uitgevoerd.  Als een query's is voltooid en Hallo aantal query's en sleuven onder Hallo limieten valt, worden in de wachtrij query's vrijgegeven. 

> [!NOTE]  
> *Selecteer* query's uitvoeren op uitsluitend dynamische Beheerweergave bekijkt (DMV's) of catalogusweergaven niet worden geregeld door een Hallo gelijktijdigheid limieten. U kunt system ongeacht het aantal query's uitvoeren op het Hallo Hallo bewaken.
> 
> 

## <a name="resource-classes"></a>Resource-klassen
Resource klassen help bepaalt u de toewijzing van geheugen en CPU-cycli tooa query opgegeven. U kunt twee soorten resource klassen tooa gebruiker in Hallo vorm databaserollen toewijzen. Hallo twee soorten resource klassen zijn als volgt:
1. Dynamische Resource-klassen (**smallrc, mediumrc, largerc, xlargerc**) toewijzen van een variabele hoeveelheid geheugen, afhankelijk van Hallo huidige DWU. Dit betekent dat wanneer u tooa opschalen groter DWU uw query's ophalen automatisch meer geheugen. 
2. Statische Resource-klassen (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) toewijzen Hallo dezelfde hoeveelheid geheugen ongeacht de huidige DWU Hallo (mits Hallo DWU zelf onvoldoende geheugen beschikbaar heeft.) Dit betekent dat op een groter aantal dwu's, u meer query's in elke bronklasse gelijktijdig uitvoeren kunt.

Gebruikers in **smallrc** en **staticrc10** krijgen een kleinere hoeveelheid geheugen en kunnen profiteren van de hogere gelijktijdigheid van taken. Gebruikers toegewezen daarentegen te**xlargerc** of **staticrc80** grote hoeveelheden geheugen, zijn opgegeven en daarom minder van de query's kunnen tegelijkertijd worden uitgevoerd.

Standaard is elke gebruiker een lid van Hallo kleine bronklasse, **smallrc**. Hallo procedure `sp_addrolemember` is tooincrease Hallo bronklasse, gebruikt en `sp_droprolemember` is toodecrease Hallo bronklasse gebruikt. Zou deze opdracht Hallo bronklasse van loaduser bijvoorbeeld te verhogen**largerc**:

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a>Query's die niet voldoen aan voor resource-klassen

Er zijn enkele typen query's die niet van een grotere geheugentoewijzing profiteren. Hallo system hun klasse resourcetoewijzing negeert en voer deze query's altijd in plaats daarvan in Hallo kleine bronklasse. Als deze query's worden altijd uitgevoerd in de kleine bronklasse Hallo, kunnen ze worden uitgevoerd wanneer gelijktijdigheid sleuven onder druk zijn en ze meer sleuven dan nodig won't verbruiken. Zie [Resource klasse uitzonderingen](#query-exceptions-to-concurrency-limits) voor meer informatie.

## <a name="details-on-resource-class-assignment"></a>Meer informatie over klasse resourcetoewijzing


Enkele meer informatie over de bronklasse:

* *Rol ALTER* machtiging is vereist toochange Hallo bronklasse van een gebruiker.
* Hoewel u een gebruiker tooone of meer van de Hallo hogere resource klassen toevoegen kunt, voorrang dynamische Bronklassen statische resource klassen. Dat wil zeggen, als een gebruiker is toegewezen tooboth **mediumrc**(dynamische) en **staticrc80**(statische) **mediumrc** Hallo resource klasse die wordt gehonoreerd.
 * Wanneer een gebruiker toomore dan één resource-klasse in een specifieke klasse brontype (meer dan één dynamische bronklasse of meer dan één statische bronklasse) toegewezen wordt, wordt de hoogste bronklasse Hallo gehonoreerd. Dat wil zeggen, als een gebruiker is toegewezen tooboth mediumrc en largerc, is hoger bronklasse hello (largerc) gehonoreerd. En als een gebruiker is toegewezen tooboth **staticrc20** en **statirc80**, **staticrc80** wordt gebruikt.
* De bronklasse Hallo van gebruiker met beheerdersrechten Hallo system kan niet worden gewijzigd.

Zie voor een gedetailleerd voorbeeld [Changing gebruiker resource klasse voorbeeld](#changing-user-resource-class-example).

## <a name="memory-allocation"></a>Toewijzing van geheugen
Er zijn voor- en nadelen tooincreasing bronklasse van een gebruiker. Een bronklasse voor een gebruiker stijgt, biedt de query's toegang toomore geheugen, wat kan betekenen dat query's sneller uitgevoerd.  Hogere resource klassen Verminder echter ook Hallo aantal gelijktijdige query's die kunnen worden uitgevoerd. Dit is Hallo compromis tussen het toewijzen van grote hoeveelheden geheugen tooa één query of andere query's, die ook geheugentoewijzingen, toorun gelijktijdig moeten toestaan. Als een gebruiker hoge toewijzingen van geheugen voor een query krijgt, andere gebruikers geen toegang toothat dezelfde geheugen toorun een query.

Hallo tabel maps Hallo geheugen toegewezen tooeach distributie door DWU en resource-klasse.

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a>Geheugentoewijzingen per distributiepunt voor dynamische Bronklassen (MB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |100 |100 |200 |400 |
| DW200 |100 |200 |400 |800 |
| DW300 |100 |200 |400 |800 |
| DW400 |100 |400 |800 |1,600 |
| DW500 |100 |400 |800 |1,600 |
| DW600 |100 |400 |800 |1,600 |
| DW1000 |100 |800 |1,600 |3,200 |
| DW1200 |100 |800 |1,600 |3,200 |
| DW1500 |100 |800 |1,600 |3,200 |
| DW2000 ZIJN |100 |1,600 |3,200 |6,400 |
| DW3000 |100 |1,600 |3,200 |6,400 |
| DW6000 |100 |3,200 |6,400 |12,800 |

Hallo tabel maps Hallo geheugen toegewezen tooeach distributie door DWU en statische bronklasse. Opmerking dat Hallo hogere resource klassen hun geheugen hebben verminderd toohonor Hallo globale DWU limieten.

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a>Geheugentoewijzingen per distributiepunt voor statische resource klassen (MB)
| DWU | staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |100 |200 |400 |400 |400 |400 |400 |400 |
| DW200 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW300 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW400 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW500 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW600 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW1000 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW1200 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW1500 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW2000 ZIJN |100 |200 |400 |800 |1,600 |3,200 |6,400 |6,400 |
| DW3000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |6,400 |
| DW6000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |12,800 |

Van Hallo voorafgaand aan de tabel, kunt u zien dat een query uitgevoerd op een dw2000 zijn in Hallo **xlargerc** bronklasse toegang too6, 400 MB aan geheugen binnen elke 60 gedistribueerde databases Hallo zou hebben.  In SQL Data Warehouse zijn er 60 distributies. Daarom moet toocalculate Hallo totale geheugentoewijzing voor een query in een bepaalde bron-klasse, Hallo hierboven waarden worden vermenigvuldigd met 60.

### <a name="memory-allocations-system-wide-gb"></a>Geheugen toewijzingen hele systeem (GB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |6 |6 |12 |23 |
| DW200 |6 |12 |23 |47 |
| DW300 |6 |12 |23 |47 |
| DW400 |6 |23 |47 |94 |
| DW500 |6 |23 |47 |94 |
| DW600 |6 |23 |47 |94 |
| DW1000 |6 |47 |94 |188 |
| DW1200 |6 |47 |94 |188 |
| DW1500 |6 |47 |94 |188 |
| DW2000 ZIJN |6 |94 |188 |375 |
| DW3000 |6 |94 |188 |375 |
| DW6000 |6 |188 |375 |750 |

In deze tabel van geheugentoewijzingen van het hele systeem, kunt u zien dat een totaal van 375 GB geheugen wordt toegewezen door een query uitgevoerd op een dw2000 zijn in Hallo xlargerc bronklasse (distributies 6400 MB * 60 * 1024 tooconvert tooGB) via Hallo geheel van uw SQL Data Warehouse.

Hallo geldt dezelfde berekening toostatic resource klassen.
 
## <a name="concurrency-slot-consumption"></a>Gelijktijdigheid sleuf verbruik  
SQL Data Warehouse verleent meer geheugen tooqueries uitgevoerd in de hogere resource-klassen. Geheugen is een vaste resource.  Daarom hello meer geheugen toegewezen per query, Hallo minder gelijktijdige query's kunnen uitvoeren. Hallo herhaalt onderstaande alle vorige concepten Hallo in één weergave met Hallo aantal sleuven beschikbaar gelijktijdigheid van taken door DWU en Hallo sleuven verbruikt door de resourceklasse van elke.  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a>Toewijzing en het verbruik van gelijktijdigheid sleuven voor dynamische Bronklassen  
| DWU | Maximum aantal gelijktijdige query 's | Gelijktijdigheid sleuven toegewezen | Gebruikt door smallrc sleuven | Gebruikt door mediumrc sleuven | Gebruikt door largerc sleuven | Gebruikt door xlargerc sleuven |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |1 |2 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |
| DW400 |16 |16 |1 |4 |8 |16 |
| DW500 |20 |20 |1 |4 |8 |16 |
| DW600 |24 |24 |1 |4 |8 |16 |
| DW1000 |32 |40 |1 |8 |16 |32 |
| DW1200 |32 |48 |1 |8 |16 |32 |
| DW1500 |32 |60 |1 |8 |16 |32 |
| DW2000 ZIJN |32 |80 |1 |16 |32 |64 |
| DW3000 |32 |120 |1 |16 |32 |64 |
| DW6000 |32 |240 |1 |32 |64 |128 |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a>Toewijzing en het verbruik van gelijktijdigheid sleuven voor statische resource klassen  
| DWU | Maximum aantal gelijktijdige query 's | Gelijktijdigheid sleuven toegewezen |staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |2 |4 |4 |4 |4 |4 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW400 |16 |16 |1 |2 |4 |8 |16 |16 |16 |16 |
| DW500 | 20| 20| 1| 2| 4| 8| 16| 16| 16| 16|
| DW600 | 24| 24| 1| 2| 4| 8| 16| 16| 16| 16|
| DW1000 | 32| 40| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1200 | 32| 48| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1500 | 32| 60| 1| 2| 4| 8| 16| 32| 32| 32|
| DW2000 ZIJN | 32| 80| 1| 2| 4| 8| 16| 32| 64| 64|
| DW3000 | 32| 120| 1| 2| 4| 8| 16| 32| 64| 64|
| DW6000 | 32| 240| 1| 2| 4| 8| 16| 32| 64| 128|

Uit deze tabellen ziet u dat SQL Data Warehouse wordt uitgevoerd als DW1000 een maximum van 32 gelijktijdige query's en een totaal van 40 gelijktijdigheid sleuven wijst. Als alle gebruikers worden uitgevoerd in smallrc, zou 32 gelijktijdige query's worden toegestaan, omdat elke query 1 gelijktijdigheid sleuf zou gebruiken. Als alle gebruikers op een DW1000 in mediumrc werd uitgevoerd, elke query 800 MB per distributiepunt voor een toewijzing van het totale geheugen van 47 GB per query toegewezen zou en gelijktijdigheid beperkt too5 gebruikers worden zou (40 gelijktijdigheid sleuven / 8-sleuven per gebruiker mediumrc).

## <a name="selecting-proper-resource-class"></a>Juiste bronklasse selecteren  
Het wordt aangeraden tooa bronklasse voor toopermanently toewijzen gebruikers in plaats van de resource-klassen te wijzigen. Bijvoorbeeld maken belasting tooclustered columnstore-tabellen voor hogere kwaliteit indexen wanneer meer geheugen toegewezen. tooensure die belastingen toegang toohigher geheugen hebben, specifiek voor het laden van gegevens maken van een gebruiker en deze tooa hogere resource gebruikersklasse permanent toewijzen.
Er zijn een aantal best practices toofollow hier. Zoals eerder vermeld, SQL DW ondersteunt twee soorten klasse brontypen: statische resource klassen en dynamische Bronklassen.
### <a name="loading-best-practices"></a>Bij het laden van aanbevolen procedures
1.  Als Hallo verwachtingen belastingen met normale hoeveelheid gegevens, is een statische bronklasse een goede keuze. Later, wanneer tooget schaalt meer verwerkingskracht, Hallo datawarehouse kan worden query toorun meer gelijktijdige out-of-the-box, zoals Hallo load gebruiker meer geheugen geen verbruikt.
2.  Als Hallo verwachtingen grotere hoeveelheden in sommige gevallen, is een dynamische bronklasse een goede keuze. Later, wanneer meer verwerkingskracht omhoog tooget schalen, krijgt Hallo load gebruiker meer geheugen out-of-the-box, zodat Hallo load tooperform daarom sneller.

Hallo nodig tooprocess geheugenbelasting efficiënt hangt af van Hallo aard van het Hallo-tabel is geladen en Hallo en de hoeveelheid gegevens verwerkt. Voor het exemplaar vereist bij het laden van gegevens in tabellen CCI dat sommige geheugen toolet CCI rowgroups bereiken optimalisatie. Zie voor meer informatie kolomopslagindexen Hallo - richtlijnen laden van gegevens.

Als een best practice we adviseren u toouse ten minste 200MB aan geheugen voor belastingen.

### <a name="querying-best-practices"></a>Aanbevolen procedures voor het opvragen
Query's hebben verschillende vereisten, afhankelijk van de complexiteit. Geheugen per query verhogen of een uitbreiding van Hallo gelijktijdigheid zijn beide tooaugment geldige manieren totale doorvoer afhankelijk van Hallo query behoeften.
1.  Indien de Hallo verwachtingen reguliere, complexe query's (bijvoorbeeld toogenerate dagelijkse en wekelijkse rapporten) en hoeft niet tootake profiteren van gelijktijdigheid van taken, is een dynamische bronklasse een goede keuze. Als Hallo system meer gegevens tooprocess heeft, bieden schaalt Hallo datawarehouse daarom automatisch meer geheugen toohello gebruiker Hallo-query uit te voeren.
2.  Indien de Hallo verwachtingen variabele of Dagverloop gelijktijdigheid patronen (bijvoorbeeld als Hallo database query wordt uitgevoerd via een webgebruikersinterface grotendeels toegankelijk), een statische bronklasse is een goede keuze. Later, wanneer toodata datawarehouse schaalt, Hallo-gebruiker is gekoppeld aan de statische bronklasse hello wordt automatisch worden kunnen toorun meer gelijktijdige query's.

Selecteren juiste geheugentoekenning afhankelijk van het Hallo-behoeften van uw query is niet-triviale, omdat deze afhankelijk van veel factoren af zoals de hoeveelheid gegevens die zijn opgevraagd is, Hallo Hallo aard van het tabelschema hello, en verschillende join, selectie en groep predicaten. Een algemeen verwerkt toewijzen van meer geheugen kunt query's toocomplete sneller, maar zou Hallo algehele gelijktijdigheid van taken. Als geen gelijktijdigheid van taken een probleem is, komt te veel toewijzen van geheugen niet schadelijk zijn. toofine afstemmen doorvoer, probeert verschillende versies van het resource-klassen is mogelijk vereist.

Kunt u Hallo volgende opgeslagen procedure toofigure uit gelijktijdigheid van taken en het geheugen verlenen per bronklasse op een gegeven SLO en Hallo dichtstbijzijnde best bronklasse voor geheugen rekenintensieve CCI bewerkingen op niet-gepartitioneerde CCI tabel op een bepaalde bron-klasse:

#### <a name="description"></a>Beschrijving:  
Hier volgt Hallo doel van deze opgeslagen procedure:  
1. toohelp gebruiker uitzoeken gelijktijdigheid van taken en het geheugen verlenen per bronklasse op een gegeven SLO. Gebruiker moet tooprovide NULL voor schema- en tablename voor deze zoals weergegeven in Hallo voorbeeld hieronder.  
2. toohelp gebruiker Bereken Hallo dichtstbijzijnde best bronklasse voor Hallo geheugen intensed CCI operations (belasting, tabel kopiëren, opnieuw opbouwen index, enzovoort) in niet-gepartitioneerde CCI tabel op een bepaalde bron-klasse. Hallo opgeslagen procedure maakt gebruik van tabel schema toofind uit Hallo vereiste geheugen toekennen voor deze.

#### <a name="dependencies--restrictions"></a>Afhankelijkheden en beperkingen:
- Deze opgeslagen procedure is niet ontworpen toocalculate geheugenvereiste voor de tabel is gepartitioneerd cci.    
- Deze opgeslagen procedure neemt geheugenvereiste in aanmerking voor Hallo Selecteer deel van INSERT-CTAS-selecteren en wordt ervan uitgegaan dat het toobe een eenvoudige SELECT.
- Deze opgeslagen procedure wordt een tijdelijke tabel gebruikt, zodat deze kan worden gebruikt in Hallo sessie waarin deze opgeslagen procedure is gemaakt.    
- Deze opgeslagen procedure is afhankelijk van de huidige aanbiedingen hello (zoals de hardwareconfiguratie, DMS config) en als een van die verandert vervolgens deze opgeslagen procedure werkt niet correct.  
- Deze opgeslagen procedure is afhankelijk van bestaande aangeboden gelijktijdigheid limiet en als die wordt gewijzigd vervolgens deze opgeslagen procedure werkt niet correct.  
- Deze opgeslagen procedure is afhankelijk van bestaande resource klasse aanbiedingen en als die vervolgens dit wijzigingen juist proc wuold werkt het programma niet opgeslagen.  

>  [!NOTE]  
>  Als u geen uitvoer na uitvoering van opgeslagen procedure met parameters die zijn opgegeven, kan er twee situaties. <br />1. Beide DW-Parameter bevat ongeldige SLO waarde <br />2. OF er zijn geen overeenkomende bronklasse voor CCI bewerking als de tabelnaam is opgegeven. <br />Bijvoorbeeld: bij DW100, hoogste geheugentoekenning beschikbaar is 400MB en als tabelschema breed voldoende toocross Hallo vereiste van 400MB.
      
#### <a name="usage-example"></a>Voorbeeld van gebruik:
Syntaxis:  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:Geef een NULL-parameter tooextract huidige DWU van Hallo DW DB Hallo of geef alle DWU vorm van 'DW100' hello ondersteund
2. @SCHEMA_NAME:Geef een schemanaam van tabel Hallo
3. @TABLE_NAME:Geef een tabelnaam van belang zijn Hallo

Voorbeelden voor het uitvoeren van deze opgeslagen procedure:  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

Tabel1 in Hallo bovenstaande voorbeelden gebruikt kan worden gemaakt zoals hieronder:  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a>Hier volgt de definitie van Hallo opgeslagen procedure:
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a>Query urgentie
SQL Data Warehouse implementeert resource klassen met behulp van werkbelastinggroepen. Er zijn een totaal van acht werkbelastinggroepen die Hallo gedrag van Hallo resource klassen via Hallo verschillende grootten van DWU beheren. Voor elke DWU SQL Data Warehouse maakt gebruik van vier Hallo acht werkbelastinggroepen. Dit is wel zinvol omdat elke werkbelastinggroep tooone van vier klassen van de resource is toegewezen: smallrc, mediumrc, largerc, of xlargerc. Hallo belang van inzicht in werkbelastinggroepen Hallo is dat enkele van deze werkbelastinggroepen toohigher zijn ingesteld *belang*. Urgentie wordt gebruikt voor CPU planning. Query's uitvoeren met een hoge urgentie krijgt drie keer meer CPU-cycli dan die met een gemiddeld urgentie. Daarom bepalen gelijktijdigheid sleuf toewijzingen ook voor CPU-prioriteit. Als een query 16 of meer sleuven verbruikt, voert deze als hoge urgentie.

Hallo toont volgende tabel Hallo belang toewijzingen voor elke werkbelastinggroep.

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a>Werkbelasting groep toewijzingen tooconcurrency sleuven en urgentie
| Werkbelastinggroepen | Gelijktijdigheid sleuf toewijzing | MB / distributie | Toewijzing van belang |
|:--- |:---:|:---:|:--- |
| SloDWGroupC00 |1 |100 |Middelgroot |
| SloDWGroupC01 |2 |200 |Middelgroot |
| SloDWGroupC02 |4 |400 |Middelgroot |
| SloDWGroupC03 |8 |800 |Middelgroot |
| SloDWGroupC04 |16 |1,600 |Hoog |
| SloDWGroupC05 |32 |3,200 |Hoog |
| SloDWGroupC06 |64 |6,400 |Hoog |
| SloDWGroupC07 |128 |12,800 |Hoog |

Van Hallo **toewijzing en het verbruik van gelijktijdigheid sleuven** grafiek, kunt u zien dat een DW500 1, 4, 8 of 16 gelijktijdigheid sleuven voor smallrc, mediumrc largerc en xlargerc, respectievelijk gebruikt. U kunt deze waarden opzoeken in de voorgaande diagram toofind Hallo belang voor elke objectklasse resource Hallo.

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a>Toewijzing van resource klassen tooimportance DW500
| Bronklasse | Werkbelastinggroep | Gelijktijdigheid sleuven gebruikt | MB / distributie | Urgentie |
|:--- |:--- |:---:|:---:|:--- |
| smallrc |SloDWGroupC00 |1 |100 |Middelgroot |
| mediumrc |SloDWGroupC02 |4 |400 |Middelgroot |
| largerc |SloDWGroupC03 |8 |800 |Middelgroot |
| xlargerc |SloDWGroupC04 |16 |1,600 |Hoog |
| staticrc10 |SloDWGroupC00 |1 |100 |Middelgroot |
| staticrc20 |SloDWGroupC01 |2 |200 |Middelgroot |
| staticrc30 |SloDWGroupC02 |4 |400 |Middelgroot |
| staticrc40 |SloDWGroupC03 |8 |800 |Middelgroot |
| staticrc50 |SloDWGroupC03 |16 |1,600 |Hoog |
| staticrc60 |SloDWGroupC03 |16 |1,600 |Hoog |
| staticrc70 |SloDWGroupC03 |16 |1,600 |Hoog |
| staticrc80 |SloDWGroupC03 |16 |1,600 |Hoog |

U kunt Hallo DMV-query toolook op Hallo verschillen in de geheugenbrontoewijzing in detail uit Hallo perspectief van de resourceregeling Hallo of tooanalyze actief en historische gebruik van de werkbelastinggroepen Hallo te volgen bij het oplossen.

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a>Query's die worden geacht gelijktijdigheid limieten
De meeste query's worden geregeld door de resource-klassen. Deze query's moeten binnen het Hallo gelijktijdige query zowel gelijktijdigheid sleuf drempelwaarden passen. Een gebruiker kiezen niet, tooexclude een query uit Hallo gelijktijdigheid sleuf model.

tooreiterate, hello volgende instructies inwilligen resource klassen:

* INSERT SELECT
* UPDATE
* VERWIJDEREN
* Selecteer (tijdens het opvragen van gebruikerstabellen)
* ALTER INDEX REBUILD
* ALTER INDEX REORGANIZE
* ALTER TABLE REBUILD
* INDEX MAKEN
* GECLUSTERDE COLUMNSTORE-INDEX MAKEN
* TABLE AS SELECT (CTAS) MAKEN
* Gegevens laden
* Data movement-bewerkingen uitgevoerd door Hallo Data Movement Service (DMS)

## <a name="query-exceptions-tooconcurrency-limits"></a>Query uitzonderingen tooconcurrency limieten
Sommige query's kunnen niet van toepassing hello resource klasse toowhich Hallo gebruiker is toegewezen. Deze uitzonderingen toohello gelijktijdigheid limieten worden aangebracht als Hallo geheugenbronnen die nodig zijn voor een bepaalde opdracht laag, vaak zijn omdat Hallo-opdracht een Metagegevensbewerking is. Hallo-doel van deze uitzonderingen is tooavoid groter geheugentoewijzingen voor query's die wordt nooit nodig. In dergelijke gevallen toegewezen Hallo standaard kleine bronklasse (smallrc) altijd, ongeacht de werkelijke bronklasse Hallo gebruikt is toohello gebruiker. Bijvoorbeeld: `CREATE LOGIN` altijd in smallrc wordt uitgevoerd. Hallo-resources die vereist toofulfill deze bewerking zijn zeer lage dus maakt geen zin tooinclude Hallo query in Hallo gelijktijdigheid sleuf model.  Deze query's worden ook niet beperkt door de limiet van 32 Hallo gebruikers gelijktijdigheid, een onbeperkt aantal deze query's kunt uitvoeren om toohello sessielimiet van 1024-sessies.

Hallo instructies te volgen doen resource klassen niet van toepassing:

* MAKEN of DROP TABLE
* ALTER TABLE... SWITCH, GESPLITSTE of partitie samenvoegen
* ALTER INDEX UITSCHAKELEN
* INDEX VERWIJDEREN
* CREATE, UPDATE of DROP STATISTICS
* TABEL AFKAPPEN
* ALTER AUTORISATIE
* AANMELDING MAKEN
* CREATE, ALTER of DROP USER
* CREATE, ALTER of DROP PROCEDURE
* MAKEN of weergave verwijderen
* WAARDEN INVOEGEN
* Selecteer in het systeemweergaven en DMV 's
* UITLEGGEN
* DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <a name="changing-user-resource-class-example"></a>Een voorbeeld van een gebruiker resource klasse wijzigen
1. **Aanmelding maken:** opent u een verbinding tooyour **master** op Hallo SQL server die als host fungeert voor uw SQL Data Warehouse-database van de database en Hallo volgende opdrachten uit te voeren.
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > Het is een goed idee toocreate een gebruiker in de hoofddatabase Hallo voor gebruikers van Azure SQL Data Warehouse. Maken van een gebruiker in master, kunt een gebruiker toologin met hulpmiddelen zoals SSMS zonder een databasenaam opgeven.  Ook kunnen ze toouse Hallo object explorer tooview alle databases op een SQL-server.  Zie voor meer informatie over het maken en beheren van gebruikers [beveiligen van een database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].
   > 
   > 
2. **SQL Data Warehouse-gebruiker maken:** opent u een verbinding toohello **SQL Data Warehouse** database en Hallo volgende opdracht uit te voeren.
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. **Machtigingen toekennen:** Hallo volgende voorbeeld verleent `CONTROL` op Hallo **SQL Data Warehouse** database. `CONTROL`op Hallo is het equivalent van db_owner in SQL Server Hallo databaseniveau.
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. **Bronklasse verhogen:** gebruik Hallo volgende query tooadd een tooa hoger werkbelasting management gebruikersrol.
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. **Bronklasse verkleinen:** gebruik Hallo volgende query tooremove een gebruiker vanuit een beheerrol werkbelasting.
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > Het is niet mogelijk tooremove een gebruiker vanuit smallrc.
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a>In de wachtrij query detectie- en andere DMV 's
U kunt Hallo `sys.dm_pdw_exec_requests` DMV tooidentify query's die in een wachtrij gelijktijdigheid wachten. Query's te wachten op een site gelijktijdigheid van taken heeft een status van **onderbroken**.

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

Werkbelasting management-rollen kunnen worden bekeken met `sys.database_principals`.

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

Hallo volgende query ziet u welke rol u elke gebruiker is toegewezen.

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

SQL Data Warehouse heeft Hallo volgende wacht typen:

* **LocalQueriesConcurrencyResourceType**: query's die zich buiten de Hallo gelijktijdigheid sleuf framework. Functies, zoals DMV-query's en system `SELECT @@VERSION` zijn voorbeelden van lokale query's.
* **UserConcurrencyResourceType**: query's die zich in Hallo gelijktijdigheid sleuf framework bevinden. Query's op tabellen van de eindgebruiker vertegenwoordigen voorbeelden die dit brontype wilt gebruiken.
* **DmsConcurrencyResourceType**: wacht ten gevolge van data movement-bewerkingen.
* **BackupConcurrencyResourceType**: deze wachttijd geeft aan dat een database worden back-up. Hallo maximale waarde voor dit resourcetype is 1. Als meerdere back-ups op Hallo aangevraagd hetzelfde moment, Hallo anderen in de wachtrij wordt geplaatst.

Hallo `sys.dm_pdw_waits` DMV mag gebruikte toosee welke resources een aanvraag wordt gewacht.

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

Hallo `sys.dm_pdw_resource_waits` DMV toont alleen Hallo resource-wacht gebruikt door een bepaalde query. Alleen meet Hallo tijd wachten op resources toobe opgegeven wachttijd voor resource, zoals tegengestelde toosignal wachttijd is Hallo tijd die nodig is voor Hallo onderliggende SQL servers tooschedule Hallo-query op Hallo CPU.

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

Hallo `sys.dm_pdw_wait_stats` DMV kan worden gebruikt voor analyse van de historische trend van wacht.

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het beheren van databasegebruikers en beveiliging [beveiligen van een database in SQL Data Warehouse][Secure a database in SQL Data Warehouse]. Zie voor meer informatie over hoe groter resource klassen kan worden verbeterd geclusterde columnstore-index kwaliteit [opnieuw opbouwen van indexen tooimprove segment kwaliteit].

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[opnieuw opbouwen van indexen tooimprove segment kwaliteit]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
