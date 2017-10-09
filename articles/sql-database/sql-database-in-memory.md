---
title: "aaaAzure SQL Database In het geheugen technologieën | Microsoft Docs"
description: "Azure SQL Database In het geheugen technologieën verbeteren aanzienlijk Hallo prestaties van transactionele en analytics werkbelastingen. Meer informatie over hoe tootake profiteren van deze technologieën."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>Prestaties optimaliseren door technologieën voor In-Memory in SQL-Database

In-Memory technologieën in Azure SQL Database gebruikt, kunt u met verschillende workloads voor verbeterde prestaties bereiken: transactionele (online transactionele verwerking (OLTP)), analytics (online analytical processing (OLAP)), en gemengde (hybride transactie/analytische verwerking (HTAP)). Omdat Hallo efficiënter query en transactieverwerking, In-Memory-technologieën kunnen u ook tooreduce kosten. U nodig tooupgrade Hallo prijscategorie van Hallo database tooachieve prestatiewinst doorgaans niet. In sommige gevallen u zelfs mogelijk Hallo prijscategorie tijdens steeds prestatieverbeteringen met technologieën In het geheugen te verminderen.

Hier vindt u twee voorbeelden van hoe In het geheugen OLTP geholpen toosignificantly de prestaties verbeteren:

- Met behulp van de In-geheugen OLTP [Quorum bedrijfsoplossingen kunnen toodouble van hun werkbelasting is tijdens het aantal dtu's verbeteren met 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).
    - DTU betekent *dtu*, en bevat een mesurement van resourceverbruik.
- Hallo volgende video toont aanzienlijke verbetering in het verbruik van met een werklast voorbeeld: [In het geheugen OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).
    - Zie voor meer informatie Hallo blogbericht: [In het geheugen OLTP in Azure SQL Database-blogberichten](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

In het geheugen technologieën zijn beschikbaar in alle databases in Hallo Premium-laag, met inbegrip van databases in Premium elastische pools.

Hallo volgende video wordt uitgelegd mogelijke prestatieverbeteringen met technologieën in Azure SQL Database In het geheugen. Houd er rekening mee dat Hallo prestatieverbetering te bereiken die u altijd ziet afhankelijk is van veel factoren, onder andere Hallo aard van Hallo werkbelasting en gegevens, toegangstijden van Hallo-database, enzovoort.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

Azure SQL-Database heeft Hallo technologieën In het geheugen te volgen:

- *In het geheugen OLTP* verhoogt de doorvoer en vermindert de latentie voor de transactieverwerking. Scenario's die van de In-geheugen OLTP profiteren zijn: hoge gegevensdoorvoer transactieverwerking zoals handelspartners en games, gegevensopname uit gebeurtenissen of IoT-apparaten, opslaan in cache laden van gegevens en de tijdelijke tabel en de variabele scenario's voor een tabel.
- *Geclusterde columnstore-indexen* verminderen van de opslag van kooldioxide (omhoog too10 keren) en verbeterde prestaties voor query's voor rapportage en analyse. U kunt deze gebruiken met feitentabellen in uw gegevens datamarts toofit meer gegevens in uw database en de prestaties verbeteren. U kunt ook met historische gegevens worden gebruikt in uw tooarchive operationele database en kunnen tooquery van too10 tijden meer gegevens zijn.
- *Niet-geclusterde columnstore-indexen* voor HTAP help u toogain realtime-inzichten in uw bedrijf door het uitvoeren van query's Hallo operationele database rechtstreeks zonder Hallo nodig toorun een dure uitpakken, transformeren en laden (ETL)-proces en wacht voor Hallo datawarehouse toobe ingevuld. Niet-geclusterde columnstore-indexen kunnen zeer snel uitvoering van analysequery's op Hallo OLTP-database, terwijl het Hallo gevolgen voor de operationele werkbelasting Hallo verminderen.
- U kunt ook Hallo combinatie van een tabel geoptimaliseerd voor geheugen met een columnstore-index hebben. Deze combinatie kunt u tooperform zeer snel transactieverwerking, en te*gelijktijdig* uitvoeren analytics query zeer snel op Hallo dezelfde gegevens.

Columnstore-indexen zowel In-geheugen OLTP is onderdeel van de SQL Server-product Hallo sinds 2012 en 2014, respectievelijk. Azure SQL Database en SQL Server delen Hallo dezelfde implementatie van de technologieën In het geheugen. Voortaan kunt zijn nieuwe mogelijkheden voor deze technologieën uitgebracht in Azure SQL Database eerst voordat ze worden vrijgegeven in SQL Server.

Dit onderwerp wordt beschreven aspecten van de In-geheugen OLTP en columnstore-indexen die specifieke tooAzure SQL-Database en tevens voorbeelden:
- Hallo-impact van deze technologieën ziet u op de opslag- en maximale grootte ervan.
- U ziet hoe toomanage verkeer van de databases die gebruikmaken van deze technologieën tussen verschillende Prijscategorieën Hallo Hallo.
- Hier ziet u twee voorbeelden die Hallo gebruik van de In-geheugen OLTP, evenals de columnstore-indexen in Azure SQL Database aangeven.

Zie Hallo volgende bronnen voor meer informatie.

Gedetailleerde informatie over Hallo-technologieën:

- [In het geheugen OLTP-overzicht en gebruiksscenario's](https://msdn.microsoft.com/library/mt774593.aspx) (inclusief verwijzingen toocustomer casestudy's en informatie tooget gestart)
- [Documentatie voor In-geheugen OLTP](http://msdn.microsoft.com/library/dn133186.aspx)
- [Handleiding voor Columnstore-indexen](https://msdn.microsoft.com/library/gg492088.aspx)
- Hybride transactionele/analytische verwerking (HTAP), ook wel bekend als [operationele realtime-analyses](https://msdn.microsoft.com/library/dn817827.aspx)

Een snelle introductie op In het geheugen OLTP: [snel starten 1: In het geheugen OLTP-technologieën voor sneller T-SQL-prestaties](http://msdn.microsoft.com/library/mt694156.aspx) (een ander artikel toohelp u aan de slag)

Gedetailleerde video's over Hallo-technologieën:

- [In het geheugen OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (die een demonstratie van de prestaties van bevat voordelen en stappen tooreproduce deze resultaten zelf)
- [In het geheugen OLTP-video's: Wat is en wanneer en hoe toouse deze](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [Columnstore-Index: In het geheugen Analytics video's van Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a>De grootte van opslag en gegevens

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>Grootte en opslag cap voor In-geheugen OLTP

In het geheugen OLTP bevat geheugen geoptimaliseerde tabellen die worden gebruikt voor het opslaan van gebruikersgegevens. Deze tabellen zijn vereiste toofit in het geheugen. Aangezien u geheugen rechtstreeks in Hallo SQL Database-service beheert, hebben we Hallo concept van een quotum voor gebruikersgegevens. Dit idee is waarnaar wordt verwezen tooas *In het geheugen OLTP-opslag*.

Elke prijscategorie en elke elastische pool prijscategorie ondersteunde zelfstandige-database bevat een bepaalde hoeveelheid In het geheugen OLTP-opslag. Bij Hallo schrijven krijgt u een gigabyte van opslag van elke 125 database transactie-eenheden (dtu's) of een elastische database transactie-eenheden (edtu's).

Hallo [SQL Database Servicelagen](sql-database-service-tiers.md) artikel heeft de officiële lijst Hallo Hallo-geheugen OLTP opslag die beschikbaar is voor elke ondersteunde zelfstandige database en de elastische groep prijscategorie.

Hallo aantal items naar uw opslagruimte In het geheugen OLTP cap te volgen:

- Rijen van de actieve gebruiker gegevens in tabellen geoptimaliseerd voor geheugen en tabelvariabelen. Houd er rekening mee dat de oude rij versies niet voor Hallo cap meetellen.
- Indexen op tabellen geoptimaliseerd voor geheugen.
- Operationele overhead van ALTER TABLE-bewerkingen.

Als u Hallo cap raakt, er een foutbericht out van quota en bent u niet langer kunnen tooinsert of update-gegevens. toomitigate deze fout gegevens verwijderen of vergroot Hallo prijscategorie Hallo database of groep.

Zie voor meer informatie over het gebruik van de opslag In het geheugen OLTP controleren en waarschuwingen te configureren als u bijna Hallo cap raakt [Monitor In-Memory opslag](sql-database-in-memory-oltp-monitoring.md).

#### <a name="about-elastic-pools"></a>Over elastische pools

Hallo-geheugen OLTP-opslag wordt met elastische pools gedeeld voor alle databases in Hallo van toepassingen. Daarom Hallo gebruik in één database kan van invloed andere databases. Er zijn twee oplossingen voor deze:

- Configureer een Max-aantal edtu's voor databases die lager is dan Hallo eDTU aantal voor Hallo pool als geheel. Dit maximum caps Hallo-geheugen OLTP gebruik van de opslag, in een database in Hallo groep, toohello grootte die overeenkomt met toohello eDTU count.
- Configureer een minimum-aantal edtu's die groter is dan 0. Deze minimale garanties dat elke database in de groep Hallo Hallo en de hoeveelheid beschikbaar In het geheugen OLTP-opslag die overeenkomt met toohello heeft geconfigureerd Min eDTU.

### <a name="data-size-and-storage-for-columnstore-indexes"></a>De gegevensgrootte van en opslag voor de columnstore-indexen

Columnstore-indexen zijn niet vereist toofit in het geheugen. Hallo daarom alleen cap op Hallo grootte van de indexen Hallo Hallo maximale totale grootte van de database die wordt beschreven in Hallo [SQL Database Servicelagen](sql-database-service-tiers.md) artikel.

Wanneer u een geclusterde columnstore-indexen gebruikt, wordt voor de opslag van de basistabel Hallo kolommen compressie gebruikt. Deze compressie kan Hallo opslag voetafdruk van uw gebruikersgegevens, wat betekent dat u meer gegevens in de database Hallo past aanzienlijk verminderen. En Hallo compressie kan worden verhoogd met [kolommen archivering compressie](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression). Hallo hoeveelheid compressie die u kunt bereiken, is afhankelijk van Hallo aard van Hallo gegevens, maar 10 keer Hallo compressie is niet ongewoon.

Als u een database met een maximale grootte van 1 terabyte (TB hebt) en u 10 keer Hallo compressie bereiken met columnstore-indexen, kunt u een totaal van 10 TB gebruikersgegevens inpassen in Hallo-database.

Wanneer u niet-geclusterde columnstore-indexen gebruikt, wordt de basistabel Hallo nog steeds in Hallo traditionele rowstore indeling opgeslagen. Hallo opslagbesparing zijn daarom niet zo groot als met geclusterde columnstore-indexen. Echter, als u een aantal niet-geclusterde indexen traditionele met een enkele columnstore-index vervangt, nog steeds ziet u een algemene besparingen in Hallo opslag footprint voor Hallo tabel.

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>Verplaatsen van databases die gebruikmaken van technologieën tussen Prijscategorieën In het geheugen

Er zijn nooit eventuele incompatibiliteiten of andere problemen bij het upgraden van een hogere prijscategorie, zoals van standaard tooPremium tooa. Hallo beschikbaar functionaliteit en resources alleen verhogen.

Maar downgraden Hallo prijscategorie kan een negatieve invloed hebben op uw database. Hallo impact is vooral duidelijk wanneer u van tooStandard Premium downgraden of Basic wanneer uw database In het geheugen OLTP-objecten bevat. Tabellen geoptimaliseerd voor geheugen en columnstore-indexen zijn niet beschikbaar na Hallo downgrade (zelfs als ze zichtbaar blijft). Hallo dezelfde overwegingen van toepassing wanneer u bij het verlagen van Hallo prijscategorie van een pool voor elastische of verplaatsen van een database met technologieën In het geheugen, in een standaard of Basic elastische pool.

### <a name="in-memory-oltp"></a>OLTP in het geheugen

*TooBasic/Standard downgraden*: In het geheugen OLTP-databases in de categorie Standard of Basic Hallo wordt niet ondersteund. Bovendien is het niet mogelijk toomove een database met een In-geheugen OLTP objecten toohello categorie Standard of Basic.

Voordat u Hallo database tooStandard/Basic gedowngraded, verwijdert u alle tabellen geoptimaliseerd voor geheugen en tabeltypen, evenals alle modules met systeemeigen compilatie T-SQL.

Er is een programmatische manier toounderstand of een bepaalde database In het geheugen OLTP ondersteunt. U kunt de Hallo volgende Transact-SQL-query uitvoeren:

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

Als het resultaat Hallo query **1**, In het geheugen OLTP wordt ondersteund in deze database.


*Lagere Premium-laag tooa downgraden*: gegevens in tabellen geoptimaliseerd voor geheugen moet in het Hallo-geheugen OLTP opslag die is gekoppeld aan de prijscategorie van de database Hallo Hallo of beschikbaar is in Hallo elastische pool passen. Als u probeert toolower Hallo prijscategorie of verplaatst Hallo-database naar een groep die beschikt niet over voldoende opslagruimte beschikbaar In het geheugen OLTP, Hallo-bewerking is mislukt.

### <a name="columnstore-indexes"></a>Columnstore-indexen

*Downgraden tooBasic of standaard*: Columnstore-indexen worden ondersteund, alleen op Hallo Premium-prijscategorie en niet op Hallo Standard- of Basic-lagen. Wanneer u uw database tooStandard of Basic gedowngraded, columnstore-index niet meer beschikbaar. Hallo system onderhoudt columnstore-index, maar deze nooit maakt gebruik van Hallo index. Als u later terug tooPremium bijwerkt, wordt de columnstore-index onmiddellijk gereed toobe opnieuw gebruikt.

Als u hebt een **geclusterde** columnstore-index Hallo hele tabel niet meer beschikbaar is na een downgrade van laag. Daarom raden we aan dat u alle neerzetten *geclusterde* columnstore-indexen voordat u uw database hieronder de Premium-laag Hallo downgraden.

*Lagere Premium-laag tooa downgraden*: deze downgrade is geslaagd als de gehele database Hallo past binnen de maximale databasegrootte Hallo voor Hallo doel prijscategorie of binnen Hallo beschikbare opslagruimte in de elastische groep Hallo. Er zijn geen specifieke gevolgen van Hallo columnstore-indexen.


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a>1. Hallo-geheugen OLTP-voorbeeld installeren

U kunt Hallo de voorbeelddatabase van AdventureWorksLT maken met een paar muisklikken in Hallo [Azure-portal](https://portal.azure.com/). Vervolgens hello in deze sectie wordt uitgelegd hoe u uw database AdventureWorksLT met In-geheugen OLTP-objecten aanvullen en prestatievoordelen demonstreren.

Zie voor een meer eenvoudig, maar meer aantrekkelijk prestaties demo voor In-geheugen OLTP:

- De versie: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- Broncode: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>Installatiestappen

1. In Hallo [Azure-portal](https://portal.azure.com/), een Premium-database maken op een server. Set Hallo **bron** toohello de voorbeelddatabase van AdventureWorksLT. Zie voor gedetailleerde instructies [uw eerste Azure SQL-database maken](sql-database-get-started-portal.md).

2. Verbinding maken met toohello database met SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).

3. Kopiëren Hallo [In het geheugen OLTP Transact-SQL-script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Klembord. Hallo T-SQL-script maakt Hallo nodig In het geheugen objecten in de voorbeelddatabase van Hallo AdventureWorksLT die u in stap 1 hebt gemaakt.

4. Hallo T-SQL-script in SSMS te plakken en vervolgens Hallo script wordt uitgevoerd. Hallo `MEMORY_OPTIMIZED = ON` component CREATE TABLE-instructies zijn essentieel. Bijvoorbeeld:


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>Fout 40536


Als u fout 40536 krijgt wanneer u Hallo T-SQL-script uitvoert, voert u Hallo T-SQL-script tooverify of Hallo database biedt ondersteuning voor In het geheugen te volgen:


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


Een resultaat van **0** betekent dat In het geheugen wordt niet ondersteund, en **1** betekent dat wordt ondersteund. toodiagnose hello probleem, zorg ervoor dat Hallo-database op Hallo Premium servicecategorie.


#### <a name="about-hello-created-memory-optimized-items"></a>Over Hallo items geoptimaliseerd voor geheugen gemaakt

**Tabellen**: Hallo voorbeeld bevat Hallo geheugen geoptimaliseerde tabellen te volgen:

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


U kunt inspecteren tabellen geoptimaliseerd voor geheugen via Hallo **Objectverkenner** in SSMS. Met de rechtermuisknop op **tabellen** > **Filter** > **filterinstellingen** > **Is geoptimaliseerd voor geheugen**. Hallo-waarde is gelijk aan 1.


Of u kunt een Hallo catalogusweergaven, zoals query:


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


**Systeemeigen, gecompileerde opgeslagen procedure**: U kunt SalesLT.usp_InsertSalesOrder_inmem inspecteren via een weergave catalogus query:


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a>Hallo voorbeeld OLTP-werkbelasting uitvoeren

het enige verschil tussen de twee volgende Hallo Hallo *opgeslagen procedures* is dat de eerste procedure Hallo versies van Hallo tabellen geoptimaliseerd voor geheugen wordt gebruikt tijdens het Hallo tweede procedure Hallo normale op schijf tabellen gebruikt:

- SalesLT**.** usp_InsertSalesOrder**_inmem**
- SalesLT**.** usp_InsertSalesOrder**_ondisk**


In deze sectie ziet u hoe toouse Hallo handige **ostress.exe** hulpprogramma tooexecute Hallo twee opgeslagen procedures op stress niveaus. U kunt vergelijken hoe lang het duurt voor toofinish van Hallo twee stress wordt uitgevoerd.


Wanneer u ostress.exe uitvoert, wordt u aangeraden dat u de parameterwaarden die zijn ontworpen voor beide volgende Hallo doorgeven:

- Uitvoeren van een groot aantal gelijktijdige verbindingen met behulp - n100.
- Hebt u elke lus verbinding honderden tijdstippen, door met de parameter - r500.


U kunt echter toostart met veel kleiner waarden zoals - n10 en -r50 tooensure dat alles werkt.


### <a name="script-for-ostressexe"></a>Script voor ostress.exe


Deze sectie vindt Hallo T-SQL-script dat is ingesloten in onze ostress.exe vanaf de opdrachtregel. Hallo script maakt gebruik van items die zijn gemaakt door Hallo T-SQL-script dat u eerder hebt geïnstalleerd.


Hallo volgende script voegt een verkoop volgorde voorbeeld met vijf artikelen in Hallo volgende geoptimaliseerd voor geheugen *tabellen*:

- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


Hallo toomake *_ondisk* versie van Hallo voorgaande T-SQL-script voor ostress.exe, vervangt u beide exemplaren van Hallo *_inmem* subtekenreeks met *_ondisk*. Deze vervangingen van invloed op Hallo namen van tabellen en opgeslagen procedures.


### <a name="install-rml-utilities-and-ostress"></a>Hulpprogramma's voor RML en ostress installeren


In het ideale geval zou u toorun ostress.exe plannen op Azure een virtuele machine (VM). Maakt u een [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in Hallo dezelfde Azure geografische regio waarin uw AdventureWorksLT-database zich bevindt. Maar u kunt in plaats daarvan ostress.exe op uw laptop uitvoeren.


Op Hallo VM of op wat u host kiezen, Hallo Replay Markup Language (RML)-hulpprogramma's installeren. Hallo-hulpprogramma's omvatten ostress.exe.

Zie voor meer informatie:
- Hallo ostress.exe discussie in [voorbeelddatabase voor In-geheugen OLTP](http://msdn.microsoft.com/library/mt465764.aspx).
- [De voorbeelddatabase voor In-geheugen OLTP](http://msdn.microsoft.com/library/mt465764.aspx).
- Hallo [blog voor het installeren van ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a>Voer Hallo *_inmem* eerst stresstest voor de werkbelasting


U kunt een *RML Cmd vragen* venster toorun onze ostress.exe vanaf de opdrachtregel. Hallo opdrachtregelparameters direct ostress naar:

- 100 verbindingen gelijktijdig worden uitgevoerd (-n100).
- Elke verbinding 50 keer Hallo T-SQL-script uitvoeren (-r50).


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


toorun hello voorgaande ostress.exe vanaf de opdrachtregel:


1. Hallo database gegevens inhoud herstellen door het uitvoeren van volgende opdracht in SSMS, toodelete Hallo alle Hallo-gegevens die door een eerder uitgevoerde wordt ingevoegd:

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. De tekst hello Hallo voorgaande ostress.exe opdrachtregel tooyour Klembord kopiëren.

3. Vervang Hallo `<placeholders>` voor Hallo parameters -S - u. -P -d Hello echte waarden te corrigeren.

4. De bewerkte opdrachtregel uitvoeren in een venster RML Cmd.


#### <a name="result-is-a-duration"></a>Resultaat is een duur


Wanneer ostress.exe is voltooid, schrijft de front-end Hallo duur uitvoeren als de laatste regel van uitvoer in Hallo RML Cmd-venster. Bijvoorbeeld, een kortere testuitvoering geduurd ongeveer 1,5 minuten:

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>Opnieuw instellen en bewerken voor *_ondisk*, vervolgens opnieuw uitvoeren


Nadat u Hallo resultaat van Hallo hebt *_inmem* uitvoeren, uitvoeren van de volgende stappen uit voor Hallo Hallo *_ondisk* uitvoeren:


1. Hallo-database opnieuw instellen door te voeren na de opdracht in SSMS toodelete Hallo alle Hallo gegevens dat is ingevoegd door Hallo vorige uitvoeren:
```
EXECUTE Demo.usp_DemoReset;
```

2. Hallo ostress.exe opdrachtregel tooreplace alle bewerken *_inmem* met *_ondisk*.

3. Ostress.exe voor Hallo tweede keer opnieuw en Hallo duur resultaat vast te leggen.

4. Hallo-database (voor voorzichtig te verwijderen welke een grote hoeveelheid testgegevens kunnen worden) opnieuw opnieuw instellen.


#### <a name="expected-comparison-results"></a>Van de verwachte vergelijkingsresultaten

Onze tests In het geheugen is gebleken dat prestaties verbeterd door **negen keer** voor deze eenvoudig werkbelasting met ostress uitgevoerd op een virtuele machine van Azure in Hallo dezelfde Azure-regio als Hallo-database.

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a>2. Hallo In-Memory Analytics voorbeeld installeren


In deze sectie maakt vergelijken u hello i/o- en statistieken resultaten wanneer u een columnstore-index ten opzichte van een traditionele b-tree-index.


Voor realtime analyses op een OLTP-werkbelasting is het vaak best toouse een niet-geclusterde columnstore-index. Zie voor meer informatie [Columnstore-indexen beschreven](http://msdn.microsoft.com/library/gg492088.aspx).



### <a name="prepare-hello-columnstore-analytics-test"></a>Hallo columnstore analytics test voorbereiden


1. Hallo toocreate met Azure portal een nieuwe database AdventureWorksLT van Hallo voorbeeld gebruiken.
 - Gebruikt u de exacte naam.
 - Kies een Premium servicecategorie.

2. Kopiëren Hallo [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Klembord.
 - Hallo T-SQL-script maakt Hallo nodig In het geheugen objecten in de voorbeelddatabase van Hallo AdventureWorksLT die u in stap 1 hebt gemaakt.
 - Hallo script maakt Hallo dimensietabel en twee feitentabellen. Hallo feitentabellen worden ingevuld met 3.5 miljoen rijen.
 - Hallo-script kan toocomplete 15 minuten duren.

3. Hallo T-SQL-script in SSMS te plakken en vervolgens Hallo script wordt uitgevoerd. Hallo **COLUMNSTORE** -sleutelwoord in Hallo **CREATE INDEX** instructie is van cruciaal belang, zoals in:<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. AdventureWorksLT toocompatibility niveau 130 instellen:<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    Niveau 130 is niet direct gerelateerd tooIn geheugen functies. Maar niveau 130 biedt doorgaans sneller queryprestaties dan 120.


#### <a name="key-tables-and-columnstore-indexes"></a>Belangrijkste tabellen en columnstore-indexen


- dbo. FactResellerSalesXL_CCI is een tabel die een geclusterde columnstore-index die over compressie op Hallo geavanceerde beschikt *gegevens* niveau.

- dbo. FactResellerSalesXL_PageCompressed is een tabel met een equivalent reguliere geclusterde index, die alleen op Hallo is gecomprimeerd *pagina* niveau.


#### <a name="key-queries-toocompare-hello-columnstore-index"></a>Sleutel query's toocompare hello columnstore-index


Er zijn [verschillende typen van de T-SQL-query die u kunt uitvoeren](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee voor verbeterde prestaties. In stap 2 van Hallo T-SQL-script, betaalt u aandacht toothis paar van query's. Verschillen slechts op één regel:


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


Een geclusterde columnstore-index wordt in Hallo FactResellerSalesXL\_CCI tabel.

Hallo volgende T-SQL-script fragment wordt afgedrukt statistieken voor i/o en tijd voor de query Hallo van elke tabel.


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

In een database met Hallo P2 prijscategorie verwacht u dat ongeveer negen keer Hallo prestatieverbetering te bereiken voor deze query met behulp van de geclusterde columnstore-index Hallo vergeleken met traditionele Hallo-index. Met P15, verwacht u dat ongeveer 57 maal Hallo prestatieverbetering te bereiken met behulp van Hallo columnstore-index.



## <a name="next-steps"></a>Volgende stappen

- [1 voor snel starten: In het geheugen OLTP-technologieën voor betere prestaties van de T-SQL](http://msdn.microsoft.com/library/mt694156.aspx)

- [Gebruik In het geheugen OLTP in een bestaande Azure SQL-toepassing](sql-database-in-memory-oltp-migration.md)

- [Opslag van de monitor In-geheugen OLTP](sql-database-in-memory-oltp-monitoring.md) voor In-geheugen OLTP


## <a name="additional-resources"></a>Aanvullende bronnen

#### <a name="deeper-information"></a>Meer gedetailleerde informatie

- [Meer informatie over hoe Quorum wordt verdubbeld sleutel database werkbelasting tijdens DTU verlagen door 70% met In-geheugen OLTP in SQL-Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [In het geheugen OLTP in Azure SQL Database-blogbericht](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [Meer informatie over In-geheugen OLTP](http://msdn.microsoft.com/library/dn133186.aspx)

- [Meer informatie over de columnstore-indexen](https://msdn.microsoft.com/library/gg492088.aspx)

- [Meer informatie over realtime operationele analytics](http://msdn.microsoft.com/library/dn817827.aspx)

- Zie [algemene patronen van de werkbelasting en overwegingen bij migratie](http://msdn.microsoft.com/library/dn673538.aspx) (waarin wordt beschreven werkbelasting patronen In het geheugen OLTP waarin vaak aanzienlijke prestatieverbeteringen biedt)

#### <a name="application-design"></a>Het ontwerp van toepassing

- [In het geheugen OLTP (optimalisatie In het geheugen)](http://msdn.microsoft.com/library/dn133186.aspx)

- [Gebruik In het geheugen OLTP in een bestaande Azure SQL-toepassing](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a>Hulpprogramma's

- [Azure Portal](https://portal.azure.com/)

- [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)

- [SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)
