---
title: aaaBest procedures voor Azure SQL Data Warehouse | Microsoft Docs
description: Aanbevelingen en aanbevolen procedures voor het ontwikkelen van oplossingen voor Azure SQL Data Warehouse. Deze helpen u goede resultaten te bereiken.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1f42908fc03e1ca52278a6853d1afe9543d648b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Aanbevolen procedures voor Azure SQL Data Warehouse
In dit artikel is een verzameling van veel aanbevolen procedures waarmee u tooachieve optimale prestaties van uw Azure SQL Data Warehouse.  Sommige Hallo-concepten in dit artikel zijn basic en eenvoudig tooexplain, andere concepten zijn meer geavanceerde en we zojuist Hallo oppervlak scratchruimte in dit artikel.  Hallo-doel van dit artikel is toogive u enkele algemene richtlijnen en tooraise bewustzijn van belangrijke gebieden toofocus als u uw datawarehouse bouwen.  Elke sectie vindt u tooa concept en vervolgens point toomore u gedetailleerde welke behandeld Hallo concept uitvoeriger artikelen.

Laat u niet afschrikken door dit artikel als u net met Azure SQL Data Warehouse begint.  Hallo-volgorde van onderwerpen Hallo is voornamelijk in volgorde van belangrijkheid Hallo.  Als u start gericht op Hallo eerst enkele concepten, zult u in orde.  Zodra u wat meer ervaring hebt opgedaan met SQL Date Warehouse, kunt u teruggaan naar dit artikel en andere onderwerpen bekijken.  Won't duurt lang voor van alles toomake zin.

## <a name="reduce-cost-with-pause-and-scale"></a>Kosten verlagen met onderbreken en schalen
Een belangrijke functie van SQL Data Warehouse is Hallo mogelijkheid toopause wanneer u niet gebruikt, die Hallo facturering van rekenresources stopt.  Een andere belangrijke functie is Hallo mogelijkheid tooscale resources.  Het onderbreken en schalen kan worden gedaan via hello Azure-portal of via PowerShell-opdrachten.  Vertrouwd raken met deze functies zoals kan aanzienlijk verminderd Hallo kosten van uw datawarehouse wanneer deze zich niet in gebruik.  Als u wilt dat altijd uw datawarehouse toegankelijk is, kunt u tooconsider verkleinen toohello kleinste grootte, een DW100 dan onderbreken.

Zie ook [Rekenresources onderbreken][Pause compute resources], [Rekenresources hervatten][Resume compute resources], [Rekenresources schalen].

## <a name="drain-transactions-before-pausing-or-scaling"></a>Transacties stoppen voor onderbreken of schalen
Wanneer u onderbreken of schalen van uw SQL Data Warehouse, achtergrond Hallo die uw query's worden geannuleerd wanneer u Hallo initieert onderbreken of schalen van de aanvraag.  Annuleren van een eenvoudige query is een snelle bewerking en is bijna geen impact toohello duurt toopause of schalen van uw exemplaar.  Echter, transactionele query's die de structuur van uw gegevens of Hallo Hallo gegevens wijzigen, mogelijk niet kunnen toostop snel.  **Transactiequery’s moeten per definitie volledig worden voltooid of hun wijzigingen volledig terugdraaien.**  Hallo voltooid werk door een transactionele query terugdraaien kan duren lang, of zelfs langer dan de oorspronkelijke wijziging Hallo Hallo query is toegepast.  Bijvoorbeeld, als u een query die verwijderen van rijen en heeft al een uur actief annuleert, kan dit duren Hallo systeem een uur tooinsert back Hallo rijen die zijn verwijderd.  Als u uitvoert, onderbreken of schalen terwijl transacties tijdens de vlucht, uw onderbreken zijn of tootake schalen lijkt heeft erg lang omdat onderbreken en schalen toowait voor Hallo terugdraaien toocomplete voordat deze kan worden voortgezet.

Zie ook [Inzicht in transacties][Understanding transactions], [Transacties optimaliseren][Optimizing transactions]

## <a name="maintain-statistics"></a>Statistieken bijhouden
Anders dan SQL Server, die statistieken automatisch detecteert en creëert of bijwerkt in kolommen, vereist SQL Data Warehouse het handmatig bijhouden van statistieken.  Terwijl we toochange bent van plan zijn dit in toekomstige, voor nu is het verstandig toomaintain uw tooensure statistieken die SQL Data Warehouse plannen Hallo Hallo geoptimaliseerd.  Hallo plannen die zijn gemaakt door optimalisatie van Hallo zijn alleen nuttig als Hallo beschikbare statistieken.  **Steekproef statistieken maken voor elke kolom is een eenvoudige manier tooget gestart met statistieken.**  Is even belangrijk tooupdate statistieken omdat belangrijke wijzigingen tooyour gegevens plaatsvinden.  Voorzichtig kan worden tooupdate uw statistieken dagelijks of na elke load.  Er zijn altijd verschillen tussen de prestaties en Hallo kosten toocreate en update statistics. Als u dat het duurt te lang toomaintain alle van de statistieken vindt, kunt u tootry toobe meer selectieve over welke kolommen hebben statistieken of welke kolommen regelmatig hoeft te worden bijgewerkt.  U kunt bijvoorbeeld tooupdate datumkolommen, waar de nieuwe waarden toegevoegd, per dag worden kunnen. **U krijgt Hallo profiteren door statistieken op kolommen die betrokken zijn in joins van kolommen die worden gebruikt in Hallo waar component en kolommen gevonden in de GROUP BY.**

Zie ook [Tabelstatistieken beheren][Manage table statistics], [CREATE STATISTICS][CREATE STATISTICS], [UPDATE STATISTICS][UPDATE STATISTICS]

## <a name="group-insert-statements-into-batches"></a>INSERT-instructie in batches groeperen
Een eenmalige load tooa kleine tabel met een INSERT-instructie of zelfs een periodieke opnieuw laden van een opzoeken prima kan uitvoeren voor uw behoeften met een instructie als `INSERT INTO MyLookup VALUES (1, 'Type 1')`.  Echter, als u nodig hebt tooload duizenden of miljoenen rijen gedurende de dag hello, vindt u mogelijk dat singleton VOEGT net niet kunnen bijhouden.  In plaats daarvan de processen ontwikkelen, zodat ze tooa-bestand schrijven en een ander proces periodiek wordt geleverd langs en dit bestand wordt geladen.

Zie ook [INSERT][INSERT]

## <a name="use-polybase-tooload-and-export-data-quickly"></a>PolyBase tooload en exporteren van gegevens snel gebruiken
SQL Data Warehouse ondersteunt het laden en exporteren van gegevens via verschillende toepassingen, waaronder Azure Data Factory, PolyBase en BCP.  Voor kleine hoeveelheden gegevens waarbij prestaties niet belangrijk zijn, kunnen al deze toepassingen aan uw vereisten voldoen.  Wanneer u bij het laden of exporteren van grote hoeveelheden gegevens of snelle prestaties nodig is, is PolyBase Hallo beste keuze.  PolyBase wordt is ontworpen tooleverage Hallo MPP (Massively Parallel Processing) architectuur van SQL Data Warehouse en daarom geladen en exporteren van gegevens MAGNITUDE sneller dan enig ander hulpprogramma.  PolyBase-loads kunnen worden uitgevoerd met behulp van CTAS of INSERT INTO.  **Met behulp van CTAS wordt geminimaliseerd transactielogboeken en de snelste manier tooload Hallo uw gegevens.**  Azure Data Factory ondersteunt ook PolyBase-loads.  PolyBase ondersteunt verschillende bestandsindelingen, waaronder GZip.  **toomaximize doorvoer bij gebruik van gzip-tekstbestanden, einde bestanden omhoog in 60 of meer bestanden toomaximize parallelle uitvoering van uw belasting.**  Voor een snellere totale doorvoer, kunt u overwegen gegevens gelijktijdig te laden.

Zie ook [Gegevens laden][Load data], [Gids voor gebruik van PolyBase][Guide for using PolyBase], [Laadpatronen en -strategieën voor Azure SQL Data Warehouse][Azure SQL Data Warehouse loading patterns and strategies], [Gegevens laden met Azure Data Factory][Load Data with Azure Data Factory], [Gegevens verplaatsen met Azure Data Factory][Move data with Azure Data Factory], [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT], [CREATE TABLE AS SELECT (CTAS)][Create table as select (CTAS)]

## <a name="load-then-query-external-tables"></a>Externe tabellen laden en vervolgens query’s uitvoeren
Polybase, ook wel bekend als externe tabellen kan Hallo snelste manier tooload gegevens zijn, is het niet optimaal is voor query's. SQL Data Warehouse PolyBase-tabellen ondersteunen momenteel alleen Azure-blob-bestanden. Deze bestanden worden niet door rekenresources ondersteunt.  Als gevolg hiervan SQL Data Warehouse kan geen werkitem offload en daarom Hallo hele bestand door deze te laden tootempdb in volgorde tooread Hallo gegevens moet lezen.  Dus als er meerdere query's die van deze gegevens opvragen, het is beter tooload deze gegevens eenmaal en query's Hallo lokale tabel gebruiken.

Zie ook [Gids voor gebruik van PolyBase][Guide for using PolyBase]

## <a name="hash-distribute-large-tables"></a>Grote tabellen distribueren met hash
Tabellen worden standaard gedistribueerd middels Round Robin.  Dit maakt het eenvoudig voor gebruikers tooget tabellen maken zonder toodecide hoe hun tabellen moeten worden verdeeld.  Round Robin-tabellen leveren voldoende prestaties voor sommige workloads, maar in de meeste gevallen leidt het selecteren van een distributiekolom tot veel betere prestaties.  Hallo meest voorkomende voorbeeld van wanneer een tabel die is geleverd door een kolom wordt ver leveren betere prestaties dan een Round Robin-tabel is wanneer twee grote feitentabellen zijn gekoppeld.  Als u hebt een ordertabel, die is gedistribueerd door order_id, en een transactietabel, die wordt ook gedistribueerd door order_id, wanneer u een tabel met bestellingen tabel tooyour transacties op order_id koppelt, wordt deze query bijvoorbeeld een Pass Through-query, wat betekent dat We elimineren gegevensverplaatsingsbewerkingen.  Minder stappen betekent een snellere query.  Minder gegevensverplaatsing maakt query’s ook sneller.  Deze uitleg NET beschadigingen Hallo voor aanvallen. Bij het laden van een gedistribueerde tabel, moet u dat uw binnenkomende gegevens niet is gesorteerd op Hallo distributiesleutel als dit de belasting wordt vertraagd.  Zie Hallo onderstaande links voor veel meer informatie over hoe een kolom van het distributiepunt te selecteren de prestaties en hoe verbeteren kunt toodefine een gedistribueerde tabel in Hallo WITH-clausule van de instructie tabellen maken.

Zie ook [Tabeloverzicht][Table overview], [Tabeldistributie][Table distribution], [Tabeldistributie selecteren][Selecting table distribution], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="do-not-over-partition"></a>Niet te veel partities maken
Partities voor uw gegevens maken kan zeer effectief zijn voor het bijhouden van gegevens door te schakelen tussen partities of het optimaliseren van scans door het schrappen van partities. Te veel partities kunnen echter uw query’s vertragen.  Een partitiestrategie met een hoge granulatie die goed werkt voor SQL Server werkt mogelijk niet goed voor SQL Data Warehouse.  Met te veel partities kunt Hallo effectiviteit van de geclusterde columnstore-indexen ook beperken als elke partitie minder dan 1 miljoen rijen heeft.  Houd er rekening mee dat achter de schermen hello, SQL Data Warehouse partities van uw gegevens voor u in 60 databases, dus als u een tabel met 100 partities maakt, daadwerkelijk dit in 6000 partities resulteert.  Elke werkbelasting verschilt zodat Hallo best adviezen tooexperiment met partitioneren toosee wat het beste voor uw workload werkt.  Overweeg een lagere granulatie dan die in SQL Server misschien wel effectief was.  U zou bijvoorbeeld wekelijkse of maandelijkse partities kunnen gebruiken in plaats van dagelijkse partities.

Zie ook [Tabellen partitioneren][Table partitioning]

## <a name="minimize-transaction-sizes"></a>Transactiegrootten minimaliseren
De instructies INSERT, UPDATE en DELETE worden in een transactie uitgevoerd en wanneer ze mislukken, moeten ze worden teruggedraaid.  toominimize hello potentiële voor een lange terugdraaien minimaliseren transactie grootten indien mogelijk.  Dit kan door de instructies INSERT, UPDATE en DELETE op te delen.  Bijvoorbeeld, als er een INSERT-bewerking die u verwacht tootake 1 uur, indien mogelijk, onderverdelen Hallo invoegen in 4 delen, die elk in 15 minuten wordt uitgevoerd.  Maak gebruik van speciale minimale logboekregistratie gevallen, zoals CTAS, TRUNCATE, DROP TABLE of INSERT tooempty tabellen, tooreduce terugdraaien risico.  Een andere manier tooeliminate Rollback is toouse metagegevens alleen bewerkingen zoals partitie switching voor gegevensbeheer.  Bijvoorbeeld, in plaats daarvan dan een instructie DELETE toodelete alle rijen in een tabel waarop Hallo ORDER_DATE weergegeven in oktober 2001 is uitgevoerd, kan partitioneren uw gegevens maandelijks en vervolgens overschakelen van de partitie met gegevens voor een lege partitie van een andere tabel hello (Zie ALTER TABEL voorbeelden).  Voor niet-gepartitioneerde tabellen kunt u met behulp van een CTAS toowrite Hallo gegevens die u wilt tookeep in een tabel in plaats van met behulp van verwijderen.  Als een CTAS vergt Hallo dezelfde hoeveelheid tijd, is een veel veiligere bewerking toorun zoals die minimale transactielogboeken zijn en snel kan worden geannuleerd indien nodig.

Zie ook [Inzicht in transacties][Understanding transactions], [Transacties optimaliseren][Optimizing transactions], [Tabellen partitioneren][Table partitioning], [TRUNCATE TABLE][TRUNCATE TABLE], [ALTER TABLE][ALTER TABLE], [CREATE TABLE AS SELECT (CTAS)][Create table as select (CTAS)]

## <a name="use-hello-smallest-possible-column-size"></a>Minimale grootte aan mogelijke kolom hello gebruiken
Hallo kleinste gegevenstype gebruiken die ondersteuning voor uw gegevens bieden wordt bij het definiëren van uw DDL queryprestaties verbeteren.  Dit is met name belangrijk voor CHAR- en VARCHAR-kolommen.  Als het langste Hallo-waarde in een kolom bestaat uit 25 tekens, definieert u de kolom als VARCHAR(25) op verzoek.  Vermijd alle kolommen tooa grote standaard tekens.  Definieer daarnaast kolommen als VARCHAR als dat alles is wat nodig is in plaats van NVARCHAR.

Zie ook [Tabeloverzicht][Table overview], [Gegevenstypes tabel][Table data types], [CREATE TABLE][CREATE TABLE]

## <a name="use-temporary-heap-tables-for-transient-data"></a>Tijdelijke heap-tabellen gebruiken voor tijdelijke gegevens
Wanneer u zijn tijdelijk gegevens in SQL Data Warehouse aanvoer, kan het gebeuren dat met behulp van een tabel heap zal maken Hallo algehele proces sneller.  Als u laadt gegevens alleen toostage voordat u meer transformaties bij het laden van de tabel tooheap Hallo moeten veel sneller dan bij het laden van Hallo gegevens tooa de geclusterde columnstore-tabel.  Bovendien wordt tijdens het laden van gegevens tooa tijdelijke tabel ook laden veel sneller dan bij het laden van een tabel toopermanent opslag.  Tijdelijke tabellen beginnen met een '#' en zijn alleen toegankelijk door Hallo-sessie waarin het is gemaakt, zodat ze kunnen alleen in beperkte gevallen werken.   Heap tabellen zijn gedefinieerd in de WITH-clausule Hallo van een tabel maken.  Als u een tijdelijke tabel gebruikt, Onthoud u ook toocreate statistieken voor deze tijdelijke tabel.

Zie ook [Tijdelijke tabellen][Temporary tables], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="optimize-clustered-columnstore-tables"></a>Geclusterde columnstore-tabellen optimaliseren
Geclusterde columnstore-indexen zijn een van de meest efficiënte manieren Hallo die u uw gegevens in Azure SQL Data Warehouse opslaat kunt.  Tabellen worden in SQL Data Warehouse standaard als geclusterde columnstore gemaakt.  tooget hello beste prestaties voor query's op de columnstore-tabellen, met een goede segment kwaliteit is belangrijk.  Wanneer rijen toocolumnstore tabellen onder geheugendruk geschreven worden, oplopen columnstore segment kwaliteit.  Segmentkwaliteit kan worden gemeten aan de hand van het aantal rijen in een gecomprimeerde rijengroep.  Zie Hallo [oorzaken van slechte columnstore-index kwaliteit] [ Causes of poor columnstore index quality] in Hallo [tabel indexen] [ Table indexes] artikel voor stapsgewijze instructies in detecteren en de kwaliteit van segment voor de geclusterde columnstore-tabellen te verbeteren.  Omdat columnstore segmenten van hoge kwaliteit belangrijk is, is het een goed idee toouse gebruikers-id's in het Hallo grote of middelgrote bronklasse om gegevens te laden.  Hallo minder dwu's u gebruikt, Hallo groter Hallo bronklasse gewenste tooassign tooyour laden van de gebruiker.

Omdat een columnstore-tabellen in het algemeen won't push-gegevens in een gecomprimeerde columnstore-segment totdat er meer dan 1 miljoen rijen per tabel zijn en elke SQL Data Warehouse-tabel is gepartitioneerd in 60 tabellen als vuistregel, columnstore-tabellen, een query won't profiteren tenzij Hallo tabel meer dan 60 miljoen rijen heeft.  Voor de tabel met minder dan 60 miljoen rijen kan software niet zorgen dat elke zin toohave een columnstore-index.  Het is misschien ook niet verkeerd.  Bovendien, als u uw gegevens partitioneren, vervolgens wilt u tooconsider dat elke partitie toohave 1 miljoen rijen toobenefit van een geclusterde columnstore-index moet.  Als een tabel partities 100 heeft, dan deze toohave ten minste 6 miljard rijen toobenefit in een store, geclusterde kolommen moet (60 distributies * 100 partities * 1 miljoen rijen).  Als de tabel geen 6 miljard rijen in dit voorbeeld heeft, Verminder het aantal partities Hallo of gebruik in plaats hiervan een heap-tabel.  Het kan ook zijn waard toosee experimenteren als betere prestaties kan worden verkregen met een heap-tabel met secundaire indexen in plaats van een columnstore-tabel.  Columnstore-tabellen ondersteunen secondaire sleutels nog niet.

Tijdens het opvragen van een columnstore-tabel wordt query's sneller uitgevoerd als u alleen Hallo kolommen, u moet selecteert.  

Zie ook [Tabel-indexen][Table indexes], [Gids columnstore-indexen][Columnstore indexes guide], [Columnstore-indexen herbouwen][Rebuilding columnstore indexes]

## <a name="use-larger-resource-class-tooimprove-query-performance"></a>Grotere resource tooimprove klasse queryprestaties gebruiken
SQL Data Warehouse maakt gebruik van resourcegroepen gebruiken als een manier tooallocate geheugen tooqueries.  Out of box hello, worden alle gebruikers toohello kleine bronklasse die 100 MB aan geheugen per distributiepunt toekent toegewezen.  Aangezien er zijn altijd gegeven 60 distributies en elk distributiepunt een minimum van 100 MB, wide Hallo totale systeemgeheugen toewijzing 6000 MB of iets minder 6 GB is.  Bepaalde query's, zoals grote joins of belastingen tooclustered columnstore-tabellen, profiteren van grotere geheugentoewijzingen.  Bij andere query’s, zoals pure scans, is er geen merkbaar verschil.  Hallo spiegelen zijde, met behulp van grotere resource categorieën heeft gevolgen voor gelijktijdigheid van taken, zodat de gewenste tootake dit in aanmerking voordat u alle van de grote resourceklasse van uw gebruikers-tooa verplaatst.

Zie ook [Gelijktijdigheid en werklastbeheer][Concurrency and workload management]

## <a name="use-smaller-resource-class-tooincrease-concurrency"></a>Gebruik van kleinere bronklasse tooIncrease gelijktijdigheid van taken
Als u daar iets van merkt wordt dat gebruikersquery toohave een lange vertraging wordt opnieuw, het is mogelijk dat zich uw gebruikers in grotere resource klassen en veel gelijktijdigheid sleuven veroorzaakt door andere query's tooqueue up verbruiken.  toosee als gebruikers query's in de wachtrij staan, voert u `SELECT * FROM sys.dm_pdw_waits` toosee als de rijen worden geretourneerd.

Zie ook [Gelijktijdigheid en werklastbeheer][Concurrency and workload management], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="use-dmvs-toomonitor-and-optimize-your-queries"></a>Gebruik DMV's toomonitor en optimaliseren van uw query 's
SQL Data Warehouse heeft verschillende DMV's die gebruikt toomonitor queryuitvoering worden kunnen.  Stapsgewijze instructies Hallo bewaking onderstaande artikel wordt uitgelegd op hoe toolook op Hallo details van een uitvoeren van een query.  tooquickly zoeken naar query's in deze DMV's, met behulp van de optie LABEL Hallo met uw query's kan helpen.

Zie ook [Uw workload controleren met DMV's][Monitor your workload using DMVs], [LABEL][LABEL], [OPTION][OPTION], [sys.dm_exec_sessions][sys.dm_exec_sessions], [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests], [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps], [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], [sys.dm_pdw_dms_workers], [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="other-resources"></a>Meer informatie
Zie ook ons artikel [Problemen oplossen][Troubleshooting] voor veelvoorkomende problemen en oplossingen.

Als u niet wat u zoekt in dit artikel vinden, probeert u Hallo 'Zoeken naar documenten' aan de linkerkant Hallo van deze pagina toosearch alle hello Azure SQL Data Warehouse-documenten.  Hallo [Azure SQL Data Warehouse MSDN-Forum] [ Azure SQL Data Warehouse MSDN Forum] is maken als een plaats voor u tooask vragen tooother gebruikers en toohello SQL Data Warehouse-productgroep.  We houden deze forum tooensure dat uw vragen worden beantwoord door een andere gebruiker of een van ons.  Als u liever tooask uw vragen over stackoverloop, we hebben ook een [Azure SQL Data Warehouse Stack Overflow-Forum][Azure SQL Data Warehouse Stack Overflow Forum].

Ten slotte gebruik Hallo [Azure SQL Data Warehouse Feedback] [ Azure SQL Data Warehouse Feedback] toomake functieaanvragen pagina.  Het toevoegen van aanvragen of het stemmen op andere aanvragen helpt ons prioriteit te geven aan bepaalde functies.

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./sql-data-warehouse-load-polybase-guide.md
[Load data]: ./sql-data-warehouse-overview-load.md
[Move data with Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[Load data with Azure Data Factory]: ./sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[Rekenresources schalen]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[sys.dm_pdw_dms_workers]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/2015/08/11/choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  http://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies
