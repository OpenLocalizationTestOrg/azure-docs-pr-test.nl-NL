---
title: aaaConnecting Azure SQL Database tooAzure zoeken met behulp van indexeerfuncties | Microsoft Docs
description: Meer informatie over hoe toopull gegevens van Azure SQL Database tooan Azure Search-index met de indexeerfuncties.
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/13/2017
ms.author: eugenesh
ms.openlocfilehash: b28a11cf18ef994de99e09af90bbfeb171ef3cde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-sql-database-tooazure-search-using-indexers"></a>Verbinding maken met Azure SQL Database tooAzure zoeken met de indexeerfuncties

Voordat u kunt een query een [Azure Search-index](search-what-is-an-index.md), moet u deze vullen met uw gegevens. Als gegevens Hallo in een Azure SQL database woont, een **Azure Search-indexeerfunctie voor Azure SQL Database** (of **Azure SQL-indexeerfunctie** kortweg) kunt automatiseren Hallo indexering, wat betekent minder code toowrite en minder dat infrastructuur toocare over.

Dit artikel behandelt Hallo mechanismen voor het gebruik van [indexeerfuncties](search-indexer-overview.md), maar ook functies die alleen beschikbaar in Azure SQL-databases (bijvoorbeeld geïntegreerd wijzigingen bijhouden) beschreven. 

In aanvulling tooAzure SQL-databases, biedt Azure Search indexeerfuncties voor [Azure Cosmos DB](search-howto-index-documentdb.md), [Azure Blob storage](search-howto-indexing-azure-blob-storage.md), en [Azure-tabelopslag](search-howto-indexing-azure-tables.md). ondersteuning voor andere gegevensbronnen toorequest uw feedback op Hallo [forum met feedback van Azure Search](https://feedback.azure.com/forums/263029-azure-search/).

## <a name="indexers-and-data-sources"></a>Indexeerfuncties en gegevensbronnen

Een **gegevensbron** bepaalt welke gegevens tooindex, referenties voor toegang tot gegevens en beleidsregels die wijzigingen in gegevens hello (nieuwe, gewijzigde of verwijderde rijen) efficiënt te identificeren. Het gedefinieerd als een onafhankelijke resource zodat deze kan worden gebruikt door meerdere indexeerfuncties.

Een **indexeerfunctie** is een bron die een enkele gegevensbron is verbonden met een gerichte search-index. Een indexeerfunctie wordt gebruikt in de volgende manieren Hallo:

* Uitvoeren van een momentopname van Hallo gegevens toopopulate een index.
* Bijwerken van een index met wijzigingen in de gegevensbron Hallo volgens een schema.
* Voer op aanvraag tooupdate een index zo nodig.

Een enkele indexeerfunctie kan alleen gebruiken één tabel of weergave, maar u kunt meerdere indexeerfuncties als u meerdere zoekindexen toopopulate wilt maken. Zie voor meer informatie over concepten [indexbewerkingen: gangbare werkstroom](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow).

U kunt instellen en configureren van een Azure SQL-indexeerfunctie met:

* De wizard gegevens importeren in Hallo [Azure-portal](https://portal.azure.com)
* Azure Search [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet)
* Azure Search [REST-API](https://docs.microsoft.com/en-us/rest/api/searchservice/indexer-operations)

In dit artikel gebruiken we Hallo REST-API toocreate **indexeerfuncties** en **gegevensbronnen**.

## <a name="when-toouse-azure-sql-indexer"></a>Wanneer toouse Azure SQL indexeerfunctie
Afhankelijk van verschillende factoren tooyour gegevens die betrekking hebben, Hallo gebruik van Azure SQL-indexeerfunctie mogelijk of niet. Als uw gegevens Hallo volgens de vereisten past, kunt u Azure SQL-indexeerfunctie.

| Criteria | Details |
|----------|---------|
| Gegevens zijn afkomstig van één tabel of weergave | Als het Hallo-gegevens is verspreid over meerdere tabellen, kunt u één enkele weergave van Hallo gegevens maken. Echter, als u een weergave gebruikt, u niet kunt toouse SQL Server geïntegreerd wijziging detectie toorefresh een index met incrementele wijzigingen. Zie voor meer informatie [vastleggen gewijzigd en verwijderd rijen](#CaptureChangedRows) hieronder. |
| Gegevenstypen zijn compatibel | De meeste, maar niet alle Hallo SQL-typen worden ondersteund in een Azure Search-index. Zie voor een lijst [toewijzing gegevenstypen](#TypeMapping). |
| Synchronisatie van realtime gegevens is niet vereist | Een indexeerfunctie kan de tabel opnieuw indexeren van maximaal vijf minuten. Als uw gegevenswijzigingen vaak en hello verandert nodig toobe weerspiegeld in Hallo index binnen enkele seconden of minuten op één, wordt u aangeraden Hallo [REST-API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) of [.NET SDK](search-import-data-dotnet.md) toopush rechtstreeks rijen bijgewerkt. |
| Incrementele indexeren is mogelijk | Als er een grote gegevensset en plan toorun Hallo indexeerfunctie volgens een schema, de Azure Search moet kunnen identificeren tooefficiently nieuwe, gewijzigde of verwijderde rijen. Niet-incrementele indexeren is alleen toegestaan als u indexeren op aanvraag (niet op schema), of minder dan 100.000 rijen te indexeren. Zie voor meer informatie [vastleggen gewijzigd en verwijderd rijen](#CaptureChangedRows) hieronder. |

## <a name="create-an-azure-sql-indexer"></a>Maak een Azure SQL-indexeerfunctie

1. Hallo-gegevensbron maken:

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of hello table or view that you want tooindex" }
    }
   ```

   U kunt Hallo-verbindingsreeks ophalen van Hallo [Azure-portal](https://portal.azure.com); hello gebruiken `ADO.NET connection string` optie.

2. Hallo doel Azure Search-index maken als u nog niet hebt. U kunt een index maken met Hallo [portal](https://portal.azure.com) of Hallo [Index-API maken](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Zorg ervoor dat Hallo schema van de doelindex is compatibel met het schema van de brontabel Hallo Hallo - Zie [toewijzing tussen SQL en Azure search-gegevenstypen](#TypeMapping).

3. Hallo indexeerfunctie door een naam geven en verwijzen naar Hallo gegevens bron en doel-index maken:

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

Een indexeerfunctie gemaakt op deze manier beschikt niet over een planning. Deze wordt automatisch uitgevoerd zodra wanneer deze gemaakt. U kunt deze opnieuw uitvoeren op elke tijd die een **indexeerfunctie uitvoeren** aanvraag:

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

U kunt verschillende aspecten van de indexeerfunctie gedrag, zoals batchgrootte en het aantal documenten worden overgeslagen voordat de uitvoering van een indexeerfunctie is mislukt. Zie voor meer informatie [indexeerfunctie-API maken](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer).

Mogelijk moet u tooallow Azure-services tooconnect tooyour database. Zie [verbinding te maken van Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) voor instructies over het toodo die.

toomonitor Hallo indexeerfunctie status en geschiedenis van de uitvoering (aantal items dat is geïndexeerd, fouten, enzovoort), gebruik een **indexeerfunctie status** aanvraag:

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

antwoord Hallo ziet vergelijkbare toohello volgende uit:

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

Uitvoergeschiedenis-ups van too50 van meest recent voltooid Hallo-uitvoeringen die zijn gerangschikt in omgekeerde volgorde hello (zodat de meest recente uitvoering Hallo eerst in het antwoord Hallo komt) bevat.
Meer informatie over antwoord Hallo vindt u in [indexeerfunctie Status ophalen](http://go.microsoft.com/fwlink/p/?LinkId=528198)

## <a name="run-indexers-on-a-schedule"></a>Indexeerfuncties volgens een planning wordt uitgevoerd
U kunt ook rangschikken Hallo indexeerfunctie toorun periodiek volgens een schema. toodo dit Hallo toevoegen **planning** eigenschap tijdens het maken of bijwerken van Hallo indexeerfunctie. Hallo in het volgende voorbeeld ziet u een indexeerfunctie PUT-aanvraag tooupdate Hallo:

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

Hallo **interval** parameter is vereist. Hallo interval verwijst toohello tijd tussen twee opeenvolgende indexeerfunctie uitvoeringen Hallo is gestart. Hallo kleinste toegestane interval is 5 minuten. Hallo langste is één dag. Moet zijn geformatteerd als de waarde van een XSD-'dayTimeDuration' (een beperkte subset van een [duur van de ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) waarde). Hallo-patroon hiervoor is: `P(nD)(T(nH)(nM))`. Voorbeelden: `PT15M` voor elke 15 minuten `PT2H` voor elke 2 uur.

Hallo optionele **startTime** geeft aan wanneer hello geplande uitvoeringen moeten worden begonnen. Als dit wordt weggelaten, wordt de Hallo huidige UTC-tijd gebruikt. Deze tijd kan zich op Hallo voorbij – in dat geval de eerste uitvoering Hallo alsof Hallo indexeerfunctie uitgevoerd continu sinds Hallo startTime is gepland.  

Slechts één van de uitvoering van een indexeerfunctie kunt uitvoeren op een tijdstip. Als een indexeerfunctie wordt uitgevoerd wanneer de uitvoering is gepland, Hallo uitvoering uitgesteld tot Hallo volgende geplande tijdstip.

Laten we eens een voorbeeld toomake dit concrete. Stel dat we Hallo volgende per uur schema dat is geconfigureerd:

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

Dit is wat er gebeurt:

1. Hallo eerste indexeerfunctie uitvoering wordt gestart op of rond 1 maart 2015 12:00 uur DE UTC.
2. Stel dat deze uitvoering duurt 20 minuten (of elk gewenst moment minder dan 1 uur).
3. tweede Hallo-uitvoering wordt gestart op of rond 1 maart 2015 1:00 uur
4. Stel nu dat deze uitvoering meer dan een uur – bijvoorbeeld 70 minuten – neemt zodat ongeveer 2:10 uur is voltooid
5. Het is nu 2:00 uur, tijd voor het derde uitvoering toostart Hallo. Echter, omdat Hallo tweede uitvoering van 1 uur is nog steeds uitgevoerd, Hallo derde uitvoeren wordt overgeslagen. Hallo derde uitvoering begint bij 3 uur.

U kunt toevoegen, wijzigen of verwijderen van een planning voor een bestaande indexeerfunctie met behulp van een **PUT indexeerfunctie** aanvraag.

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a>Nieuwe, gewijzigde en verwijderde rijen vastleggen

Maakt gebruik van Azure Search **incrementele indexeren** tooavoid met toore-index Hallo gehele tabel of weergave telkens wanneer een indexeerfunctie wordt uitgevoerd. Azure Search biedt dat twee detectie beleid toosupport incrementele indexeren wijzigen. 

### <a name="sql-integrated-change-tracking-policy"></a>In SQL geïntegreerde wijzigingen bijhouden van beleid
Als uw SQL database ondersteunt [bijhouden](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server), wordt u aangeraden **SQL geïntegreerde wijzigen Traceringsbeleid**. Dit is het meest efficiënt beleid Hallo. Bovendien kunt u Azure Search tooidentify verwijderde rijen zonder dat u tooadd hoeft een expliciete 'soft delete' kolom tooyour tabel.

#### <a name="requirements"></a>Vereisten 

+ Database-versievereisten:
  * SQL Server 2012 SP3 en later, als u SQL Server op Azure Virtual machines.
  * Azure SQL Database V12, als u Azure SQL Database.
+ Alleen tabellen (Er zijn geen weergaven). 
+ In de database Hallo [inschakelen voor het bijhouden](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) voor Hallo tabel. 
+ Er is geen samengestelde primaire sleutel (een primaire sleutel die meer dan één kolom) op Hallo tabel.  

#### <a name="usage"></a>Gebruik

toouse dit beleid maken of bijwerken van de gegevensbron die u als volgt:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

Wanneer met behulp van SQL geïntegreerd bijhouden van beleid, geef geen een afzonderlijke gegevens detectie verwijderingsbeleid - dit beleid bevat ingebouwde ondersteuning voor het identificeren van verwijderde rijen. Echter voor automagically' hello verwijderingen toobe gedetecteerd' moet hello documentsleutel in uw search-index worden Hallo hetzelfde als de primaire sleutel Hallo in Hallo SQL-tabel. 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a>Beleid voor High-Water Mark wijzigen

Beleid voor deze wijziging is afhankelijk van een 'high-water mark' kolom vastleggen Hallo versie of tijd wanneer een rij voor het laatst is bijgewerkt. Als u een weergave, moet u een high-water mark-beleid. Hallo high-water mark kolom moet voldoen aan Hallo volgens de vereisten.

#### <a name="requirements"></a>Vereisten 

* Alle voegt een waarde opgeven voor Hallo-kolom.
* Alle updates tooan item ook Hallo-waarde van Hallo kolom wijzigen.
* Hallo-waarde van deze kolom wordt verhoogd met elke invoegen of bijwerken.
* Query's met Hallo waar te volgen en ORDER BY-componenten efficiënt kunnen worden uitgevoerd:`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`

> [!IMPORTANT] 
> Ten zeerste aangeraden Hallo [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) gegevenstype voor Hallo high-water mark kolom. Als een ander gegevenstype wordt gebruikt, is het bijhouden toocapture alle wijzigingen in de aanwezigheid van transacties die worden uitgevoerd als een query indexeerfunctie Hallo niet gegarandeerd. Wanneer u **rowversion** in een configuratie met alleen-lezen-replica's, moet u Hallo indexeerfunctie verwijzen op Hallo primaire replica. Alleen een primaire replica kan worden gebruikt voor scenario's voor het synchroniseren van gegevens.

#### <a name="usage"></a>Gebruik

toouse een high-water mark-beleid maken of bijwerken van de gegevensbron die u als volgt:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> Als de brontabel Hallo geen een index op Hallo high-water mark kolom heeft, kunnen een query's die worden gebruikt door Hallo SQL indexeerfunctie time-out. In het bijzonder Hallo `ORDER BY [High Water Mark Column]` component vereist een index toorun efficiënt wanneer Hallo tabel veel rijen bevat.
>
>

Als u de time-outfouten ondervindt, kunt u Hallo `queryTimeout` indexeerfunctie configuratie-instelling tooset hello tooa outwaarde query hoger is dan de time-out voor Hallo standaard 5 minuten. Bijvoorbeeld, tooset Hallo time-out too10 minuten maken of bijwerken van Hallo indexeerfunctie Hello volgende configuratie:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

U kunt ook uitschakelen Hallo `ORDER BY [High Water Mark Column]` component. Dit wordt echter niet aanbevolen omdat als Hallo indexeerfunctie worden uitgevoerd door een fout wordt onderbroken, Hallo indexeerfunctie toore proces alle rijen heeft als deze later - wordt uitgevoerd zelfs als Hallo indexeerfunctie al bijna alle Hallo rijen verwerkt door Hallo wanneer die deze is onderbroken. Hallo toodisable `ORDER BY` -component, gebruik Hallo `disableOrderByHighWaterMarkColumn` instellen in de definitie van de indexeerfunctie Hallo:  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a>Beleid voor voorlopig verwijderen kolom verwijdering detectie
Wanneer rijen worden verwijderd uit de brontabel hello, wilt u waarschijnlijk toodelete die rijen uit ook Hallo search-index. Als u Hallo SQL geïntegreerde wijzigingen bijhouden van beleid, dit is afgehandeld voor u. Echter, Hallo high-water mark Traceringsbeleid niet helpt u met verwijderde rijen. Welke toodo?

Als Hallo rijen fysiek zijn verwijderd uit de tabel hello, heeft Azure Search geen manier tooinfer Hallo aanwezigheid van records die niet meer bestaat.  Echter, kunt u Hallo 'soft-delete' techniek toologically verwijderen rijen zonder te verwijderen op tabel Hallo. Voeg een kolom tooyour tabel of weergave en rijen markeren als verwijderd met behulp van die kolom.

Wanneer u Hallo voorlopig verwijderen techniek, kunt u beleid voor voorlopig verwijderen Hallo als volgt bij het maken of bijwerken van de gegevensbron Hallo:

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[hello value that indicates that a row is deleted]"
        }
    }

Hallo **softDeleteMarkerValue** moet een tekenreeks-Hallo tekenreeksrepresentatie van de werkelijke waarde gebruiken. Bijvoorbeeld, als u een kolom met gehele getallen waar verwijderde rijen zijn gemarkeerd met Hallo waarde 1 hebt, gebruik `"1"`. Als u een bits-kolom waar verwijderde rijen zijn gemarkeerd met Booleaanse waarde ' True ' hello hebt, gebruikt u `"True"`.

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a>Toewijzing tussen SQL en Azure Search-gegevenstypen
| SQL-gegevenstype | Toegestaan doelindex veldtypen | Opmerkingen |
| --- | --- | --- |
| bits |Edm.Boolean, Edm.String | |
| int en smallint, tinyint |Edm.Int32, Edm.Int64, Edm.String | |
| bigint |Edm.Int64, Edm.String | |
| reële float |Edm.Double, Edm.String | |
| smallmoney, geld decimale numerieke |Edm.String |Azure Search biedt geen ondersteuning voor het decimale typen converteren naar Edm.Double omdat dit precisie verliezen |
| CHAR, nchar, varchar, nvarchar |Edm.String<br/>Collection(EDM.String) |Een SQL-tekenreeks kan gebruikte toopopulate een veld verzameling (EDM.String) zijn als Hallo tekenreeks een JSON-matrix van tekenreeksen vertegenwoordigt:`["red", "white", "blue"]` |
| smalldatetime, datetime, datetime2, date, datetimeoffset |Edm.DateTimeOffset, Edm.String | |
| uniqueidentifer |Edm.String | |
| Geografie |Edm.GeographyPoint |Alleen Geografie exemplaren van het type punt met SRID 4326 (dit is standaard Hallo) worden ondersteund |
| ROWVERSION |N.v.t. |Kolommen van de rij-versie in Hallo-zoekindex kunnen niet worden opgeslagen, maar ze kunnen worden gebruikt voor het bijhouden |
| tijd, timespan, binary, varbinary, image, xml, geometry, CLR-typen |N.v.t. |Niet ondersteund |

## <a name="configuration-settings"></a>Configuratie-instellingen
SQL-indexeerfunctie beschrijft de verschillende configuratie-instellingen:

| Instelling | Gegevenstype | Doel | Standaardwaarde |
| --- | --- | --- | --- |
| queryTimeout |Tekenreeks |Sets Hallo-out voor de uitvoering van de SQL-query |5 minuten (' 00: 05:00 ") |
| disableOrderByHighWaterMarkColumn |BOOL |Zorgt ervoor dat Hallo SQL-query die wordt gebruikt door Hallo high-water mark beleid tooomit Hallo ORDER BY-component. Zie [High-Water Mark beleid](#HighWaterMarkPolicy) |ONWAAR |

Deze instellingen worden gebruikt in Hallo `parameters.configuration` object in de definitie van de indexeerfunctie Hallo. Bijvoorbeeld, tooset Hallo query time-out too10 minuten, maken of bijwerken van Hallo indexeerfunctie Hello volgende configuratie:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a>Veelgestelde vragen

**V: kan ik Azure SQL-indexeerfunctie gebruiken met SQL-databases die zijn uitgevoerd op IaaS virtuele machines in Azure**

Ja. U moet echter de zoekdatabase service tooconnect tooyour tooallow. Zie voor meer informatie [verbinding van een Azure Search-indexeerfunctie tooSQL Server configureren op een Azure VM](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).

**V: kan ik Azure SQL-indexeerfunctie met SQL-databases met lokale gebruiken?**

Niet rechtstreeks. Er wordt niet aanbevolen noch een rechtstreekse verbinding ondersteuning als dit dus tooopen u uw databases tooInternet verkeer moeten zou. Klanten zijn met dit scenario met brug technologieën zoals Azure Data Factory geslaagd. Zie voor meer informatie [Push gegevens tooan Azure Search-index met Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector).

**V: kan ik Azure SQL-indexeerfunctie gebruiken dan SQL Server op Azure wordt uitgevoerd in een IaaS-databases**

Nee. Dit scenario wordt ondersteund niet omdat Hallo een indexeerfunctie met alle databases dan SQL Server is niet getest.  

**V: kan ik meerdere indexeerfuncties uitgevoerd volgens een planning maken?**

Ja. Echter kan slechts één indexeerfunctie worden uitgevoerd op één knooppunt tegelijk. Als u meerdere indexeerfuncties gelijktijdig uitgevoerd moet, kunt u uw search-service toomore dan één zoekeenheid schaalt.

**V: bevat een indexeerfunctie invloed zijn op de workload van mijn query's uitgevoerd?**

Ja. Indexeerfunctie wordt uitgevoerd op een van de knooppunten Hallo in uw zoekservice en resources voor dat knooppunt worden gedeeld tussen indexeren ten behoeve van de queryverkeer en andere API-aanvragen. Als u werkbelastingen met een intensieve indexeren en de query uitvoert en een hoge frequentie van 503-fouten of toenemende reactietijden optreden, kunt u overwegen [uw search-service schaalt](search-capacity-planning.md).

**V: kan ik gebruik van een secundaire replica in een [failovercluster](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) als een gegevensbron?**

Dat hangt ervan af. U kunt een secundaire replica gebruiken voor volledige indexering van een tabel of weergave. 

Voor incrementele indexeren Azure Search ondersteunt twee beleidsregels wijzigen: SQL geïntegreerd bijgehouden en High-Water Mark wijzigen.

Op alleen-lezen-replica's ondersteunt SQL database geen geïntegreerde wijzigingen bijhouden. Daarom moet u een High-Water Mark beleid gebruiken. 

Onze standaard aanbeveling is toouse Hallo rowversion gegevenstype voor Hallo high-water mark kolom. Echter, is met behulp van rowversion afhankelijk van de SQL-Database `MIN_ACTIVE_ROWVERSION` functie, wat niet wordt ondersteund op alleen-lezen-replica's. U moet daarom Hallo indexeerfunctie tooa primaire replica verwijzen als u van rowversion gebruikmaakt.

Als u toouse rowversion op een alleen-lezen-replica probeert, ziet u de volgende fout Hallo: 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update hello datasource and specify a connection toohello primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

**V: kan ik een alternatieve, niet-tijdstempelkolom gebruiken voor het bijhouden van een high-water mark?**

Het wordt niet aangeraden. Alleen **rowversion** voor betrouwbare gegevenssynchronisatie kunt. Echter, afhankelijk van uw toepassingslogica mogelijk veilige als:

+ U kunt ervoor zorgen dat wanneer Hallo indexeerfunctie wordt uitgevoerd, er zijn geen openstaande transacties op Hallo-tabel die wordt geïndexeerd (bijvoorbeeld alle tabel updates gebeuren als een batch volgens een schema en hello Azure Search-indexeerfunctie planning tooavoid overlapt met het Hallo-tabel is ingesteld schema bijwerken).  

+ U doen een volledige opnieuw indexeren toopick up gemiste rijen regelmatig. 
