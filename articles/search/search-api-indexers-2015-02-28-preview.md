---
title: 'Indexbewerkingen (Azure Search Service REST-API: 2015-02-28-Preview) | Microsoft Docs'
description: 'Indexbewerkingen (Azure Search Service REST-API: 2015-02-28-Preview)'
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>Indexbewerkingen (Azure Search Service REST-API: 2015-02-28-Preview)
> [!NOTE]
> Dit artikel wordt beschreven indexeerfuncties in Hallo [2015-02-28-Preview REST-API](search-api-2015-02-28-preview.md). Deze API-versie wordt preview-versies van Azure Blob Storage een indexeerfunctie met document uitpakken en Azure Table Storage indexeerfunctie, plus andere verbeteringen toegevoegd. Hallo API ondersteunt ook algemeen beschikbaar indexeerfuncties (GA), met inbegrip van indexeerfuncties voor Azure SQL Database, SQL Server op Azure VM's en Azure Cosmos DB.
> 
> 

## <a name="overview"></a>Overzicht
Azure Search kunt rechtstreeks te integreren met algemene gegevensbronnen verwijderen Hallo nodig toowrite code tooindex uw gegevens. tooset omhoog deze up die u kunt hello Azure Search API toocreate aanroepen en beheren **indexeerfuncties** en **gegevensbronnen**. 

Een **indexeerfunctie** is een resource die gegevensbronnen met de zoekindexen doel verbindt. Een indexeerfunctie wordt gebruikt in de volgende manieren Hallo: 

* Uitvoeren van een momentopname van Hallo gegevens toopopulate een index.
* Een index met wijzigingen in de gegevensbron Hallo volgens een schema worden gesynchroniseerd. Hallo planning maakt deel uit van Hallo indexeerfunctie definitie.
* Op aanvraag tooupdate een index zo nodig worden aangeroepen. 

Een **indexeerfunctie** is nuttig wanneer u regelmatig updates tooan index wilt. U kunt een inline-planning instellen als onderdeel van de definitie van een indexeerfunctie of uitvoeren op aanvraag met behulp van [uitvoeren indexeerfunctie](#RunIndexer). 

Een **gegevensbron** geeft aan welke gegevens moeten toobe geïndexeerd, referenties tooaccess Hallo gegevens en beleidsregels tooenable Azure Search tooefficiently identificeren wijzigingen in Hallo gegevens (zoals gewijzigd of verwijderde rijen in een databasetabel). Het gedefinieerd als een onafhankelijke resource zodat deze kan worden gebruikt door meerdere indexeerfuncties.

Hallo volgende gegevensbronnen worden momenteel ondersteund:

* **Azure SQL Database** en **SQL Server op Azure Virtual machines**. Zie voor een gerichte procedure [in dit artikel](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 
* **Azure Cosmos DB**. Zie voor een gerichte procedure [in dit artikel](search-howto-index-documentdb.md). 
* **Azure Blob Storage**, waaronder Hallo volgende document indelingen: PDF-, Microsoft Office (DOCX/DOC, XSLX/XLS, PPTX/PPT, bericht) HTML, XML, POSTCODE en tekst zonder opmaak bestanden (inclusief JSON). Zie voor een gerichte procedure [in dit artikel](search-howto-indexing-azure-blob-storage.md).
* **Azure-tabelopslag**. Zie voor een gerichte procedure [in dit artikel](search-howto-indexing-azure-tables.md).

We overweegt ondersteuning toevoegen voor extra gegevensbronnen in toekomstige Hallo. ons prioriteren deze beslissingen toohelp Geef uw feedback op Hallo [forum met feedback van Azure Search](http://feedback.azure.com/forums/263029-azure-search).

Zie [Servicelimieten](search-limits-quotas-capacity.md) voor maximaal bron verwante resources voor tooindexer en gegevens wordt beperkt.

## <a name="typical-usage-flow"></a>Typische gebruiksscenario stroom
U kunt maken en beheren van Indexeerfuncties en gegevensbronnen via eenvoudige HTTP-aanvragen (POST, GET, PUT, DELETE) op basis van een bepaalde `data source` of `indexer` resource.

Het instellen van automatische indexering is doorgaans een proces vier stappen:

1. Hallo-gegevensbron met Hallo-gegevens die moeten worden geïndexeerd toobe identificeren. Houd er rekening mee dat Azure Search mogelijk geen ondersteuning voor alle gegevenstypen Hallo aanwezig in de gegevensbron. Zie [ondersteunde gegevenstypen](https://msdn.microsoft.com/library/azure/dn798938.aspx) voor Hallo-lijst.
2. Een Azure Search-index waarvan het schema compatibel met uw gegevensbron is maken.
3. Maak een Azure Search-gegevensbron, zoals beschreven in [gegevensbron maken](#CreateDataSource).
4. Maak een Azure Search-indexeerfunctie zoals beschreven [indexeerfunctie maken](#CreateIndexer).

U moet over het maken van een indexeerfunctie voor elke combinatie target index en gegevensbron plannen. U kunt meerdere indexeerfuncties geschreven naar de Hallo dezelfde hebben index, en u kunt hergebruiken Hallo dezelfde gegevensbron voor meerdere indexeerfuncties. Echter een indexeerfunctie kan slechts één gegevensbron gebruiken op een tijdstip en kan alleen enkele index tooa schrijven. 

Na het maken van een indexeerfunctie kunt u de status ervan kan worden uitgevoerd met behulp van Hallo ophalen [indexeerfunctie Status ophalen](#GetIndexerStatus) bewerking. U kunt ook een indexeerfunctie uitvoeren op elk gewenst moment (in plaats van of in aanvullende toorunning het periodiek volgens een schema) met behulp van Hallo [indexeerfunctie worden uitgevoerd](#RunIndexer) bewerking.

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>Gegevensbron maken
Een gegevensbron wordt in Azure Search met indexeerfuncties, bieden Hallo-verbindingsgegevens voor de ad-hoctaak of geplande gegevensvernieuwing van een doelindex gebruikt. U kunt een nieuwe gegevensbron binnen een Azure Search-service met behulp van een HTTP POST-aanvraag maken.

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

U kunt ook gebruiken PUT en Hallo gegevensbronnaam op Hallo URI opgeven. Als het Hallo-gegevensbron niet bestaat, wordt deze gemaakt.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> maximum aantal gegevensbronnen dat is toegestaan Hallo varieert per prijscategorie. Hallo gratis service kunt u too3-gegevensbronnen. Standard-service kan 50 gegevensbronnen. Zie [Servicelimieten](search-limits-quotas-capacity.md) voor meer informatie.
> 
> 

**Aanvraag**

HTTPS is vereist voor alle aanvragen van de service. Hallo **gegevensbron maken** aanvraag kan worden geconstrueerd met een methode POST of PUT. Wanneer u POST, moet u de naam van een gegevensbron in de aanvraagtekst Hallo samen met de definitie van de gegevensbron Hallo opgeven. Hallo-naam is met PUT, onderdeel van Hallo-URL. Als de gegevensbron Hallo niet bestaat, wordt deze gemaakt. Als deze al bestaat, is het bijgewerkte toohello nieuwe definitie. 

Hallo-gegevensbronnaam moet in kleine letters worden, beginnen met een letter of cijfer, hebben geen slashes of punten en minder dan 128 tekens bevatten. Hallo rest van de naam van de Hallo kan na het Hallo-gegevensbronnaam starten met een letter of cijfer bevatten een letter, cijfer en streepjes, zolang Hallo streepjes niet opeenvolgende zijn. Zie [naamgevingsregels](https://msdn.microsoft.com/library/azure/dn857353.aspx) voor meer informatie.

Hallo `api-version` is vereist. de huidige versie Hallo is `2015-02-28`.

**Aanvraagheaders**

Hallo volgende lijst beschrijft Hallo vereiste en optionele aanvraagheaders. 

* `Content-Type`: Vereist. Stel deze optie te`application/json`
* `api-key`: Vereist. Hallo `api-key` gebruikte tooauthenticate Hallo aanvraag tooyour Search-service is. Het is een tekenreekswaarde, een unieke tooyour-service. Hallo **gegevensbron maken** aanvraag moet bevatten een `api-key` header tooyour beheersleutel (als tegengestelde tooa querysleutel) ingesteld. 

U moet ook Hallo service naam tooconstruct Hallo aanvraag-URL. U kunt beide servicenaam Hallo ophalen en `api-key` van uw servicedashboard in Hallo [Azure Portal](https://portal.azure.com/). Zie [maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) voor pagina navigatie hulp.

<a name="CreateDataSourceRequestSyntax"></a>
**Syntaxis van de aanvraag hoofdtekst**

Hallo-hoofdtekst van Hallo-aanvraag bevat een definitie van de gegevensbron, waaronder het type gegevensbron hello, referenties tooread Hallo gegevens, evenals de detectie van een optionele gegevens wijzigen en gegevens verwijdering detectie beleidsregels voor gebruikte tooefficiently identificeren gewijzigd of verwijderde gegevens in de gegevensbron Hallo gebruikt in combinatie met een regelmatig geplande indexeerfunctie. 

Hallo-syntaxis voor het Hallo-aanvraaglading structureren is als volgt. Een voorbeeld van een aanvraag wordt aangeboden op verder in dit onderwerp.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

Aanvraag bevat Hallo volgende eigenschappen: 

* `name`: Vereist. Hallo-naam van Hallo-gegevensbron. Naam van een gegevensbron moet alleen kleine letters, cijfers of afbreekstreepjes bevatten, mag niet beginnen of eindigen met streepjes en beperkte too128 tekens.
* `description`: Een optionele beschrijving. 
* `type`: Vereist. Moet een gegevensbrontypen Hallo ondersteund:
  * `azuresql`-Azure SQL Database of SQL Server op Azure Virtual machines
  * `documentdb`-Cosmos azure DB
  * `azureblob`-Azure Blob-opslag
  * `azuretable`-Azure-tabelopslag
* `credentials`:
  * Hallo vereist `connectionString` -eigenschap geeft op Hallo-verbindingsreeks voor Hallo-gegevensbron. Hallo-indeling van de verbindingsreeks hello, is afhankelijk van type gegevensbron Hallo: 
    * Dit is Hallo gebruikelijke SQL Server-verbindingsreeks voor Azure SQL. Als u hello Azure portal tooretrieve Hallo verbindingsreeks, gebruikt u Hallo `ADO.NET connection string` optie.
    * Azure Cosmos DB moet Hallo-verbindingsreeks in de volgende indeling Hallo: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`. Hallo-waarden zijn vereist. U vindt deze in Hallo [Azure-portal](https://portal.azure.com/).  
    * Dit is Hallo-verbindingsreeks voor opslag-account voor Azure-Blob en Table Storage. Hallo-indeling wordt beschreven [hier](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/). HTTPS-eindpunt-protocol is vereist.  
* `container`, vereist: Hiermee geeft u op Hallo gegevens tooindex Hallo met `name` en `query` eigenschappen: 
  * `name`Vereist:
    * Azure SQL: Hiermee geeft u het Hallo-tabel of weergave. U kunt schema gekwalificeerde namen, zoals `[dbo].[mytable]`.
    * DocumentDB: Hiermee geeft u Hallo-verzameling. 
    * Azure Blob Storage: Hiermee geeft u Hallo storage-container.
    * Azure Table Storage: geeft de naam Hallo van Hallo tabel. 
  * `query`, optioneel:
    * DocumentDB: Hiermee kunt u toospecify een query die wordt samengevoegd een willekeurige indeling van de JSON-document in een platte schema dat u kunt de Azure Search index.  
    * Azure Blob Storage: Hiermee kunt u een virtuele map in de blob-container Hallo toospecify. Bijvoorbeeld: voor blobpad `mycontainer/documents/blob.pdf`, `documents` kan worden gebruikt als Hallo virtuele map.
    * Azure Table Storage: Hiermee kunt u een query of filters set rijen toobe geïmporteerd Hallo toospecify.
    * Azure SQL: query wordt niet ondersteund. Als u deze functionaliteit nodig, neem stemmen voor [deze suggestie](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* Hallo optionele `dataChangeDetectionPolicy` en `dataDeletionDetectionPolicy` eigenschappen worden hieronder beschreven.

<a name="DataChangeDetectionPolicies"></a>
**Beleid voor de detectie van gegevens wijzigen**

Hallo-doel van een data detectie wijzigingsbeleid is tooefficiently artikelen gewijzigde gegevens identificeren. Ondersteunde beleidsregels variëren, afhankelijk van het type gegevensbron Hallo. De volgende secties beschrijven elk beleid. 

***Wijziging detectie Bovengrensbeleid*** 

Gebruik dit beleid wanneer de gegevensbron bevat een kolom of een eigenschap die voldoet aan de volgende criteria Hallo:

* Alle voegt een waarde opgeven voor Hallo-kolom. 
* Alle updates tooan item ook Hallo-waarde van Hallo kolom wijzigen. 
* Hallo-waarde van deze kolom wordt verhoogd met elke wijziging.
* Query's die gebruikmaken van een filter-component vergelijkbare toohello volgende `WHERE [High Water Mark Column] > [Current High Water Mark Value]` efficiënt kunnen worden uitgevoerd.

Bijvoorbeeld: bij gebruik van Azure SQL-gegevensbronnen, een geïndexeerde `rowversion` kolom is Hallo ideaal geschikt is voor gebruik met met Hallo high-water mark beleid. 

Dit beleid kan als volgt worden opgegeven:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

Wanneer u Azure Cosmos DB-gegevensbronnen, moet u Hallo `_ts` eigenschap verstrekt door Azure Cosmos DB. 

Bij gebruik van Azure Blob-gegevensbronnen, Azure Search automatisch maakt gebruik van een bovengrens wijzigingsbeleid detectie op basis van een blob het laatst is gewijzigd van het tijdstempel; u hoeft niet toospecify dergelijk beleid zelf.   

***In SQL geïntegreerde wijzigingsbeleid***

Als uw SQL database ondersteunt [bijhouden](https://msdn.microsoft.com/library/bb933875.aspx), wordt aangeraden SQL geïntegreerde wijzigen Traceringsbeleid. Dit beleid kunt Hallo meest efficiënt bijhouden en staat Azure Search tooidentify verwijderde rijen zonder dat u toohave hoeft een kolom met expliciete 'voorlopig verwijderen' in uw schema.

Geïntegreerd wijzigingen bijhouden wordt ondersteund vanaf Hallo versies van SQL Server-database te volgen: 

* SQL Server 2008 R2, als u SQL Server op Azure Virtual machines.
* Azure SQL Database V12, als u Azure SQL Database.  

Wanneer met behulp van SQL geïntegreerde wijzigingen bijhouden beleid, geef geen een afzonderlijke gegevens detectie verwijderingsbeleid - dit beleid bevat ingebouwde ondersteuning voor het identificeren van verwijderde rijen. 

Dit beleid kan alleen worden gebruikt met tabellen. Deze kan niet worden gebruikt met weergaven. U moet tooenable bijhouden voor Hallo tabel u voordat u dit beleid kunt gebruiken. Zie [inschakelen en uitschakelen van bijhouden](https://msdn.microsoft.com/library/bb964713.aspx) voor instructies.    

Hallo structureren **gegevensbron maken** aanvraagt, SQL geïntegreerde wijzigingen bijhouden van beleid kan als volgt worden opgegeven:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**Beleid voor de detectie van gegevens verwijderen**

Hallo-doel van een gegevens-verwijderingsbeleid detectie is tooefficiently verwijderde gegevensitems identificeren. Is momenteel alleen ondersteund Hallo beleid Hallo `Soft Delete` beleid, waardoor identificeren verwijderde items die zijn gebaseerd op Hallo-waarde van een `soft delete` kolom of eigenschap in het Hallo-gegevensbron. Dit beleid kan als volgt worden opgegeven:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> Alleen kolommen met een tekenreeks, geheel getal of Boole-waarden worden ondersteund. waarde die wordt gebruikt als Hallo `softDeleteMarkerValue` moet een tekenreeks, zelfs als de bijbehorende kolom Hallo gehele getallen of Booleaanse waarden bevat. Bijvoorbeeld, als Hallo-waarde die wordt weergegeven in de gegevensbron 1 is, gebruikt u `"1"` als Hallo `softDeleteMarkerValue`.    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**Aanvraag hoofdtekst voorbeelden**

Als u van plan toouse Hallo-gegevensbron met een indexeerfunctie die volgens een planning wordt uitgevoerd bent, in dit voorbeeld ziet u hoe toospecify wijzigen en verwijderen van een beleid voor detectie: 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

Als u alleen toouse Hallo gegevensbron voor eenmalige kopiëren van gegevens van hello wilt, kunnen Hallo beleidsregels worden weggelaten:

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**Antwoord**

Aanvraag is gelukt: 201 gemaakt. 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>Gegevensbron bijwerken
U kunt een bestaande gegevensbron met behulp van een HTTP PUT-aanvraag bijwerken. U opgeven Hallo naam van Hallo data source tooupdate op Hallo aanvraag-URI:

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Hallo `api-version` is vereist. de huidige versie Hallo is `2015-02-28`. [Azure Search API-versies](https://msdn.microsoft.com/library/azure/dn864560.aspx) details en meer informatie over alternatieve versies heeft.

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Aanvraag**

Hallo aanvraag hoofdtekst syntaxis is Hallo als voor dezelfde [gegevensbron maken aanvragen](#CreateDataSourceRequestSyntax).

Sommige eigenschappen kunnen niet worden bijgewerkt op een bestaande gegevensbron. Bijvoorbeeld, wijzigen u Hallo-type van een bestaande gegevensbron niet.  

Als u niet toochange Hallo-verbindingsreeks voor een bestaande gegevensbron wilt, kunt u Hallo letterlijke `<unchanged>` Hallo-verbindingsreeks. Dit is handig in situaties waar u moet een gegevensbron tooupdate, maar geen verbindingsreeks voor gemakkelijke toegang toohello omdat het vertrouwelijke gegevens.

**Antwoord**

Aanvraag is gelukt: 201 gemaakt als een nieuwe gegevensbron is gemaakt en 204 geen inhoud als een bestaande gegevensbron is bijgewerkt.

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>Lijst met gegevensbronnen
Hallo **lijst gegevensbronnen** bewerking retourneert een lijst van gegevensbronnen Hallo in uw Azure Search-service. 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

Hallo `api-version` is vereist. de huidige versie Hallo is `2015-02-28`. 

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Antwoord**

Aanvraag is gelukt: 200 OK.

Hier volgt een voorbeeld-antwoordtekst:

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

Houd er rekening mee dat u kunt filteren, antwoord Hallo omlaag toojust Hallo eigenschappen die u geïnteresseerd bent in. Bijvoorbeeld: als u wilt dat alleen een lijst met namen van gegevensbronnen, Hallo OData gebruiken `$select` query-optie:

    GET /datasources?api-version=205-02-28&$select=name

In dit geval zou Hallo reactie van Hallo bovenstaande voorbeeld als volgt uitzien: 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

Dit is een nuttig toosave bandbreedte als er een groot aantal gegevensbronnen in uw zoekservice.

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>Gegevensbron ophalen
Hallo **gegevensbron ophalen** bewerking Hallo gegevensbrondefinitie opgehaald uit Azure Search.

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

Hallo `api-version` is vereist. de huidige versie Hallo is `2015-02-28`. 

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Antwoord**

Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.

Hallo-antwoord is vergelijkbaar tooexamples in [gegevensbron maken voorbeeld aanvragen](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> Stel geen Hallo `Accept` aanvraagheader te`application/json;odata.metadata=none` wanneer het aanroepen van deze API als in dat geval zal `@odata.type` kenmerk toobe weggelaten uit het antwoord Hallo en u niet kunt toodifferentiate tussen gegevens wijzigen en detectie van gegevens verwijderen beleidsregels met verschillende typen. 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>Gegevensbron verwijderen
Hallo **gegevensbron verwijderen** bewerking verwijdert u een gegevensbron van uw Azure Search-service.

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Als alle indexeerfuncties verwijst naar Hallo-gegevensbron die u wilt verwijderen, wordt nog steeds Hallo verwijderbewerking voortgezet. Deze indexeerfuncties echter verandert in een foutstatus van de volgende keer wordt uitgevoerd.  
> 
> 

Hallo `api-version` is vereist. de huidige versie Hallo is `2015-02-28`. 

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Antwoord**

Statuscode: 204 geen inhoud wordt geretourneerd voor een geslaagde reactie.

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>Maak indexeerfunctie
U kunt een nieuwe indexeerfunctie binnen een Azure Search-service met behulp van een HTTP POST-aanvraag maken.

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

U kunt ook gebruiken PUT en Hallo gegevensbronnaam op Hallo URI opgeven. Als het Hallo-gegevensbron niet bestaat, wordt deze gemaakt.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> maximum aantal toegestane indexeerfuncties Hallo varieert per prijscategorie. Hallo gratis service kunt u too3 indexeerfuncties. Standard-service kan 50 indexeerfuncties. Zie [Servicelimieten](search-limits-quotas-capacity.md) voor meer informatie.
> 
> 

Hallo `api-version` is vereist. de huidige versie Hallo is `2015-02-28`. 

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

<a name="CreateIndexerRequestSyntax"></a>
**Syntaxis van de aanvraag hoofdtekst**

Hallo-hoofdtekst van Hallo-aanvraag bevat een definitie van een indexeerfunctie waarin Hallo-gegevensbron en Hallo doelindex voor indexeren, evenals optionele indexering planning en parameters. 

Hallo-syntaxis voor het Hallo-aanvraaglading structureren is als volgt. Een voorbeeld van een aanvraag wordt aangeboden op verder in dit onderwerp.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**Indexeerfunctie planning**

Een indexeerfunctie kunt optioneel een planning opgeven. Als een planning aanwezig is, wordt periodiek Hallo indexeerfunctie uitgevoerd volgens de planning. Planning heeft Hallo volgende kenmerken:

* `interval`: Vereist. Een duration-waarde die een interval of de periode voor de indexeerfunctie aangeeft wordt uitgevoerd. Hallo kleinste toegestane interval is 5 minuten. Hallo langste is één dag. Moet zijn geformatteerd als de waarde van een XSD-'dayTimeDuration' (een beperkte subset van een [duur van de ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) waarde). Hallo-patroon hiervoor is: `"P[nD][T[nH][nM]]"`. Voorbeelden: `PT15M` voor elke 15 minuten `PT2H` voor elke 2 uur. 
* `startTime`: Vereist. Een UTC datetime wanneer Hallo indexeerfunctie moet zijn gestart. 

**Indexeerfunctie Parameters**

Een indexeerfunctie kunt eventueel verschillende parameters die invloed hebben op het gedrag opgeven. Hallo-parameters zijn optioneel.  

* `maxFailedItems`: het aantal items dat niet kan toobe Hallo geïndexeerd voordat de uitvoerbewerking van de indexeerfunctie wordt beschouwd als een fout. De standaardwaarde is 0. Informatie over mislukte items wordt geretourneerd door Hallo [indexeerfunctie Status ophalen](#GetIndexerStatus) bewerking. 
* `maxFailedItemsPerBatch`: het aantal items dat niet kan toobe Hallo geïndexeerd in elke batch voordat de uitvoerbewerking van de indexeerfunctie wordt beschouwd als een fout. De standaardwaarde is 0.
* `base64EncodeKeys`: Geeft aan of document sleutels base 64-codering. Azure Search gelden beperkingen voor tekens die gebruikt in een documentsleutel worden kunnen. Hallo-waarden in de brongegevens bevatten echter tekens die ongeldig zijn. Als het benodigde tooindex dergelijke als document sleutels waarden, kan deze vlag tootrue worden ingesteld. Standaard is `false`.
* `batchSize`: Geeft het aantal items die zijn gelezen uit de gegevensbron Hallo en geïndexeerde Hallo als één batch in de volgorde tooimprove prestaties. Hallo standaard, is afhankelijk van type gegevensbron Hallo: is 1000 voor Azure SQL en Azure Cosmos DB en 10 voor Azure Blob Storage.

**Veld-verwijzingen**

U kunt veld toewijzingen toomap een veldnaam in Hallo tooa ander veld gegevensbronnaam in doelindex hello gebruiken. Neem bijvoorbeeld een brontabel met een veld `_id`. Azure Search toegestaan niet in de naam van een veld met een onderstrepingsteken beginnen zodat Hallo veld naam moet worden gewijzigd. U kunt dit doen met behulp van Hallo `fieldMappings` eigenschap van de indexeerfunctie Hallo als volgt: 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

U kunt meerdere veldtoewijzingen opgeven: 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

Bron- en doelserver veldnamen zijn hoofdlettergevoelig.

<a name="FieldMappingFunctions"></a>
***Veld toewijzing functies***

Veldtoewijzingen kunnen ook worden gebruikt tootransform veldwaarden voor bron met *toewijzing functies*.

Slechts één van deze functie wordt momenteel ondersteund: `jsonArrayToStringCollection`. Een veld met een tekenreeks die is opgemaakt als een JSON-matrix in een verzameling (EDM.String) veld in Hallo doelindex worden geparseerd. Het is bedoeld voor gebruik met Azure SQL-indexeerfunctie in het bijzonder omdat SQL beschikt niet over een eigen verzamelingsgegevenstype. Worden kan gebruikt als volgt: 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

Bijvoorbeeld, als hello bevat bronveld Hallo tekenreeks `["red", "white", "blue"]`, en vervolgens het doelveld Hallo van het type `Collection(Edm.String)` worden ingevuld met Hallo drie waarden `"red"`, `"white"` en `"blue"`.

Houd er rekening mee dat Hallo `targetFieldName` eigenschap is optioneel; als u bent vergeten, Hallo `sourceFieldName` waarde wordt gebruikt. 

<a name="CreateIndexerRequestExamples"></a>
**Aanvraag hoofdtekst voorbeelden**

Hallo volgende voorbeeld wordt een indexeerfunctie waarmee gegevens worden gekopieerd vanuit Hallo tabel waarnaar wordt verwezen door Hallo `ordersds` gegevensbron toohello `orders` index volgens een schema dat begint op 1 januari 2015 UTC en wordt elk uur wordt uitgevoerd. Elke aanroep van indexeerfunctie is geslaagd als niet meer dan 5 items toobe geïndexeerd in elke batch mislukt, en niet meer dan 10 items toobe geïndexeerd in totaal mislukken. 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**Antwoord**

201 gemaakt voor de aanvraag is gelukt.

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>Indexeerfunctie bijwerken
U kunt een bestaande indexeerfunctie met behulp van een HTTP PUT-aanvraag bijwerken. U opgeven Hallo naam van Hallo indexeerfunctie tooupdate op Hallo aanvraag-URI:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Hallo `api-version` is vereist. de huidige versie Hallo is `2015-02-28`. 

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Aanvraag**

Hallo aanvraag hoofdtekst syntaxis is Hallo als voor dezelfde [maken indexeerfunctie aanvragen](#CreateIndexerRequestSyntax).

**Antwoord**

Aanvraag is gelukt: 201 gemaakt als een nieuwe indexeerfunctie is gemaakt en 204 geen inhoud als een bestaande indexeerfunctie is bijgewerkt.

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>Lijst met indexeerfuncties
Hallo **lijst indexeerfuncties** bewerking retourneert Hallo lijst met indexeerfuncties in uw Azure Search-service. 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


Hallo `api-version` is vereist. Hallo preview-versie is `2015-02-28-Preview`. [Azure Search versioning](https://msdn.microsoft.com/library/azure/dn864560.aspx) details en meer informatie over alternatieve versies heeft.

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Antwoord**

Aanvraag is gelukt: 200 OK.

Hier volgt een voorbeeld-antwoordtekst:

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

Houd er rekening mee dat u kunt filteren, antwoord Hallo omlaag toojust Hallo eigenschappen die u geïnteresseerd bent in. Bijvoorbeeld: als u alleen een lijst met namen van de indexeerfunctie wilt, Hallo OData gebruiken `$select` query-optie:

    GET /indexers?api-version=2014-10-20-Preview&$select=name

In dit geval zou Hallo reactie van Hallo bovenstaande voorbeeld als volgt uitzien: 

    {
      "value" : [ { "name": "myindexer" } ]
    }

Dit is een nuttig toosave bandbreedte als er een groot aantal indexeerfuncties in uw zoekservice.

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>Indexeerfunctie ophalen
Hallo **ophalen indexeerfunctie** bewerking Hallo indexeerfunctie definitie opgehaald uit Azure Search.

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Hallo `api-version` is vereist. Hallo preview-versie is `2015-02-28-Preview`. 

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Antwoord**

Statuscode: 200 OK wordt geretourneerd voor een geslaagde reactie.

Hallo-antwoord is vergelijkbaar tooexamples in [indexeerfunctie maken voorbeeld aanvragen](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>Indexeerfunctie verwijderen
Hallo **indexeerfunctie verwijderen** bewerking verwijdert een indexeerfunctie van uw Azure Search-service.

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Wanneer een indexeerfunctie wordt verwijderd, Hallo indexeerfunctie uitvoeringen uitgevoerd op dat moment toocompletion wordt uitgevoerd, maar er is geen verdere uitvoeringen wordt gepland. Pogingen toouse die een niet-bestaande indexeerfunctie resulteert in het HTTP-statuscode 404 wordt niet gevonden. 

Hallo `api-version` is vereist. Hallo preview-versie is `2015-02-28-Preview`. 

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Antwoord**

Statuscode: 204 geen inhoud wordt geretourneerd voor een geslaagde reactie.

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>Indexeerfunctie uitvoeren
In aanvulling toorunning periodiek volgens een schema, kan een indexeerfunctie ook worden aangeroepen op verzoek via Hallo **uitvoeren indexeerfunctie** bewerking: 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

Hallo `api-version` is vereist. Hallo preview-versie is `2015-02-28-Preview`. 

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Antwoord**

Statuscode: 202 geaccepteerde wordt geretourneerd voor een geslaagde reactie.

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>Status van de indexeerfunctie ophalen
Hallo **indexeerfunctie Status ophalen** bewerking Hallo huidige status en uitvoering geschiedenis van een indexeerfunctie haalt: 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


Hallo `api-version` is vereist. Hallo preview-versie is `2015-02-28-Preview`. 

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Antwoord**

Statuscode: 200 OK voor een geslaagde reactie.

Hallo-antwoordtekst bevat informatie over de algehele status van de indexeerfunctie, Hallo laatste indexeerfunctie aanroepen, evenals Hallo geschiedenis van recente indexeerfunctie aanroepen (indien aanwezig). 

Een voorbeeld-antwoordtekst ziet er als volgt: 

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

**Status van de indexeerfunctie**

Status van de indexeerfunctie kunt Hallo volgende waarden zijn:

* `running`Hiermee wordt aangegeven op dat Hallo indexeerfunctie wordt normaal uitgevoerd. Houd er rekening mee dat sommige Hallo indexeerfunctie uitvoeringen nog steeds is beschadigd, dus is het een goed idee toocheck hello `lastResult` ook de eigenschap. 
* `error`Hiermee wordt aangegeven op dat Hallo indexeerfunctie is een fout die niet kan worden hersteld zonder menselijke tussenkomst opgetreden. Bijvoorbeeld, referenties voor gegevensbron Hallo mogelijk verlopen of Hallo schema van de gegevensbron Hallo of Hallo doelindex is gewijzigd in een recente manier. 

**Resultaat van uitvoering indexeerfunctie**

Het resultaat van een indexeerfunctie-uitvoering bevat informatie over een enkel indexeerfunctie worden uitgevoerd. de meest recente resultaat Hallo is opgehaald als Hallo `lastResult` eigenschap van Hallo indexeerfunctie status. Andere recente resultaten, indien aanwezig, worden geretourneerd als Hallo `executionHistory` eigenschap van Hallo indexeerfunctie status. 

Resultaat van uitvoering indexeerfunctie bevat Hallo volgende eigenschappen: 

* `status`: status van de uitvoering van een Hallo. Zie [indexeerfunctie Execution Status](#IndexerExecutionStatus) hieronder voor meer informatie. 
* `errorMessage`: foutbericht voor een mislukte uitvoering. 
* `startTime`: Hallo tijd in UTC wanneer deze-uitvoering wordt gestart.
* `endTime`: Hallo tijd in UTC wanneer deze-uitvoering is beëindigd. Deze waarde is niet ingesteld als het Hallo-uitvoering wordt nog uitgevoerd.
* `errors`: een matrix van itemniveau fouten, indien van toepassing. Elk item bevat een documentsleutel (`key` eigenschap) en een foutbericht (`errorMessage` eigenschap). 
* `itemsProcessed`: aantal gegevensbronitems (bijvoorbeeld tabelrijen) die indexeerfunctie geprobeerd tooindex tijdens het uitvoeren van deze Hallo Hallo. 
* `itemsFailed`: aantal items dat is mislukt tijdens het uitvoeren van deze Hallo.  
* `initialTrackingState`: altijd `null` Hallo eerste indexeerfunctie wordt uitgevoerd, of als Hallo gegevens bijhouden beleid wijzigt, is niet ingeschakeld op Hallo gegevensbron die wordt gebruikt. Als dit beleid is ingeschakeld, in een volgende uitvoering deze waarde geeft Hallo eerste (laagste) bijhouden waarde verwerkt door deze kan worden uitgevoerd. 
* `finalTrackingState`: altijd `null` als Hallo gegevens bijhouden beleid wijzigt, is niet ingeschakeld op Hallo gegevensbron die wordt gebruikt. Anders geeft Hallo nieuwste (hoogste) bijhouden van wijzigingen is verwerkt door deze uitvoering waarde. 

<a name="IndexerExecutionStatus"></a>
**Uitvoeringsstatus van indexeerfunctie**

Uitvoeringsstatus van de indexeerfunctie wordt vastgelegd Hallo status van een enkele indexeerfunctie worden uitgevoerd. Deze kan Hallo volgende waarden hebben:

* `success`Hiermee wordt aangegeven dat Hallo indexeerfunctie uitvoering is voltooid.
* `inProgress`Geeft aan dat Hallo indexeerfunctie worden uitgevoerd in voortgang. 
* `transientFailure`Hiermee wordt aangegeven dat de uitvoering van een indexeerfunctie is mislukt. Zie `errorMessage` eigenschap voor meer informatie. Hallo mislukken kan of kan geen menselijke tussenkomst toofix vereist - bijvoorbeeld een incompatibel schema tussen Hallo gegevensbron en Hallo doelindex is hersteld vereist in te grijpen, maar niet door een tijdelijke gegevensbron uitvaltijd. Aanroepen van de indexeerfunctie wordt voortgezet per planning, indien aanwezig. 
* `persistentFailure`Hiermee wordt aangegeven op dat Hallo indexeerfunctie is mislukt op een manier die menselijke tussenkomst vereist. Geplande indexeerfunctie uitvoeringen gestopt. Gebruik nadat Hallo-probleem opgelost, opnieuw instellen indexeerfunctie API toorestart Hallo gepland uitvoeringen. 
* `reset`Hiermee wordt aangegeven dat indexeerfunctie Hallo is opnieuw ingesteld door een tooReset aanroep van indexeerfunctie API (Zie hieronder). 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>Indexeerfunctie opnieuw instellen
Hallo **indexeerfunctie opnieuw** bewerking wordt opnieuw ingesteld Hallo-status is gekoppeld aan Hallo indexeerfunctie voor bijhouden. Hiermee kunt u tootrigger van-begin opnieuw indexeren (bijvoorbeeld als het schema van de gegevensbron is gewijzigd) of toochange Hallo gegevens wijzigen detectie beleid voor een gegevensbron die is gekoppeld aan Hallo indexeerfunctie.   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

Hallo `api-version` is vereist. Hallo preview-versie is `2015-02-28-Preview`. 

Hallo `api-key` moet een beheersleutel (als tegengestelde tooa query-sleutel). Raadpleeg de sectie van de toohello verificatie in [REST-API van zoekservice](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn meer informatie over sleutels. [Maken van een service voor zoeken in Hallo portal](search-create-service-portal.md) wordt uitgelegd hoe tooget Hallo service-URL en sleuteleigenschappen in Hallo aanvraag gebruikt.

**Antwoord**

Statuscode: 204 geen inhoud voor een geslaagde reactie.

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>Toewijzing tussen de SQL-gegevenstypen en Azure Search-gegevenstypen
<table style="font-size:12">
<tr>
<td>SQL-gegevenstype</td>    
<td>Toegestaan doelindex veldtypen</td>
<td>Opmerkingen</td>
</tr>
<tr>
<td>bits</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>int en smallint, tinyint</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>reële float</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>smallmoney, geld<br>Decimale<br>numerieke
</td>
<td>Edm.String</td>
<td>Azure Search biedt geen ondersteuning voor het decimale typen converteren naar Edm.Double omdat dit precisie verliezen
</td>
</tr>
<tr>
<td>CHAR, nchar, varchar, nvarchar</td>
<td>Edm.String<br/>Collection(EDM.String)</td>
<td>Zie [veld toewijzing functies](#FieldMappingFunctions) in dit document voor meer informatie over het tootransform een kolom met tekenreeksen in een verzameling (EDM.String)</td>
</tr>
<tr>
<td>smalldatetime, datetime, datetime2, date, datetimeoffset</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>Geografie</td>
<td>Edm.GeographyPoint</td>
<td>Alleen Geografie exemplaren van het type punt met SRID 4326 (dit is standaard Hallo) worden ondersteund</td>
</tr>
<tr>
<td>ROWVERSION</td>
<td>N.v.t.</td>
<td>Kolommen van de rij-versie in Hallo-zoekindex kunnen niet worden opgeslagen, maar ze kunnen worden gebruikt voor het bijhouden</td>
</tr>
<tr>
<td>tijd, timespan<br>Binary, varbinary, afbeelding,<br>XML, geometry, CLR-typen</td>
<td>N.v.t.</td>
<td>Niet ondersteund</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Toewijzing tussen JSON-gegevenstypen en Azure Search-gegevenstypen
<table style="font-size:12">
<tr>
<td>JSON-gegevenstype</td>    
<td>Toegestaan doelindex veldtypen</td>
<td>Opmerkingen</td>
</tr>
<tr>
<td>BOOL</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Integraal cijfers</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Getallen met drijvende komma</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Tekenreeks</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>matrices met primitieve typen, bijvoorbeeld ["a", "b", "c"]</td>
<td>Collection(EDM.String)</td>
<td></td>
</tr>
<tr>
<td>Tekenreeksen die lijken op datums</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>GeoJSON point-objecten</td>
<td>Edm.GeographyPoint</td>
<td>GeoJSON punten zijn JSON-objecten in de volgende indeling Hallo: {'type': 'Point', 'coordinates': [lang, lat]} </td>
</tr>
<tr>
<td>Andere JSON-objecten</td>
<td>N.v.t.</td>
<td>Niet ondersteund. Azure Search ondersteunt momenteel alleen primitieve typen en tekenreeks verzamelingen</td>
</tr>
</table>
