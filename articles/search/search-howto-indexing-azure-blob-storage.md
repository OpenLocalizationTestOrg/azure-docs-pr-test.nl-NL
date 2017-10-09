---
title: aaaIndexing Azure Blob Storage met Azure Search
description: Meer informatie over hoe tooindex Azure Blob Storage en uitpakken van met Azure Search tekstdocumenten
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/22/2017
ms.author: eugenesh
ms.openlocfilehash: 1bdd34e66a4a9192ed88cacbc7b8456d0dcdfeb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a>Documenten in Azure Blob Storage met Azure Search indexeren
Dit artikel laat zien hoe toouse Azure Search tooindex documenten (zoals PDF-bestanden, Microsoft Office-documenten en enkele andere algemene indelingen) opgeslagen in Azure Blob storage. Hierin wordt uitgelegd eerst Hallo basisprincipes van instellen en configureren van een blob-indexering. Vervolgens biedt een meer gedetailleerde uitleg van gedrag en scenario's bent u waarschijnlijk tooencounter.

## <a name="supported-document-formats"></a>Ondersteunde documentindelingen voor
Hallo blob indexeerfunctie kunt Haal de tekst uit Hallo opmaak van documenten te volgen:

* PDF
* Microsoft Office indelingen: DOCX/DOC, XLSX/XLS, PPTX/PPT bericht (Outlook e-mailberichten)  
* HTML
* XML
* POSTCODE
* EML
* RTF-INDELING
* Tekstbestanden (Zie ook [indexeren als tekst zonder opmaak](#IndexingPlainText))
* JSON (Zie [indexeren JSON-blobs](search-howto-index-json-blobs.md))
* CSV (Zie [indexeren CSV blobs](search-howto-index-csv-blobs.md) preview-functie)

> [!IMPORTANT]
> Ondersteuning voor CSV en JSON-matrices is momenteel in preview. Deze indelingen zijn alleen beschikbaar is met versie **2016-09-01-Preview** Hallo REST-API of versie 2.x-preview Hallo .NET SDK. Maak onthouden, preview-API's zijn bedoeld voor testen en evalueren en mag niet worden gebruikt in een productieomgeving.
>
>

## <a name="setting-up-blob-indexing"></a>Instellen van de blob-indexering
U kunt instellen dat een Azure Blob Storage indexeerfunctie gebruiken:

* [Azure Portal](https://ms.portal.azure.com)
* Azure Search [REST-API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)
* Azure Search [.NET SDK](https://aka.ms/search-sdk)

> [!NOTE]
> Sommige functies (bijvoorbeeld een veld-verwijzingen) zijn nog niet beschikbaar in Hallo-portal en hebt toobe programmatisch gebruikt.
>
>

Hier ziet u Hallo-stroom met Hallo REST-API.

### <a name="step-1-create-a-data-source"></a>Stap 1: Een gegevensbron maken
Een gegevensbron bepaalt welke gegevens tooindex, referenties die nodig zijn tooaccess Hallo gegevens en beleidsregels tooefficiently wijzigingen in gegevens hello (nieuwe, gewijzigde of verwijderde rijen). Een gegevensbron kan worden gebruikt door meerdere indexeerfuncties in Hallo dezelfde search-service.

Voor blob-indexering moet gegevensbron Hallo Hallo volgende vereiste eigenschappen hebben:

* **naam** Hallo unieke naam van de gegevensbron Hallo binnen uw search-service is.
* **type** moet `azureblob`.
* **referenties** biedt Hallo account verbindingsreeks voor opslag als Hallo `credentials.connectionString` parameter. Zie [hoe toospecify referenties](#Credentials) hieronder voor meer informatie.
* **container** Hiermee geeft u een container in uw opslagaccount. Standaard zijn alle blobs in de container Hallo worden opgehaald. Als u alleen tooindex blobs in een bepaalde virtuele map wilt, kunt u met behulp van Hallo optionele map **query** parameter.

een gegevensbron toocreate:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

Zie voor meer informatie over Hallo maken Datasource API [Datasource maken](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="how-toospecify-credentials"></a>Hoe toospecify referenties ####

U kunt opgeven dat Hallo referenties voor Hallo blob-container in een van de volgende manieren:

- **Volledige toegang account opslagverbindingsreeks**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`. Hallo-verbindingsreeks kunt u krijgen via hello Azure-portal door te navigeren blade opslagaccount toohello > Instellingen > sleutels (voor klassieke opslagaccounts) of instellingen > toegangssleutels (voor Azure Resource Manager storage-accounts).
- **Shared access signature voor Storage account** (SAS)-verbindingsreeks: `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=b&sp=rl` Hallo SAS Hallo lijst en leesrechten op containers en objecten moet hebben (in dit geval blobs).
-  **Shared access signature voor containers**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<hello signature>&se=<hello validity end time>&sp=rl` Hallo SAS Hallo lijst en leesrechten op Hallo container moet hebben.

Toegang tot de handtekeningen voor meer informatie over gedeelde opslag, Zie [handtekeningen voor gedeelde toegang met behulp van](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Als u SAS-referenties gebruikt, moet u tooupdate hello gegevensbronreferenties regelmatig met vernieuwde handtekeningen tooprevent ze zijn verlopen. Als de SAS-referenties is verlopen, Hallo indexeerfunctie mislukt met een foutbericht te`Credentials provided in hello connection string are invalid or have expired.`.  

### <a name="step-2-create-an-index"></a>Stap 2: Een index maken
Hallo index geeft Hallo velden in een document, kenmerken, en andere constructies definiëren die vorm Hallo-zoekfunctie.

Hier ziet u hoe een index met een doorzoekbare toocreate `content` toostore Hallo tekst opgehaald uit de blobs veld:   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

Zie voor meer informatie over het maken van indexen [Index maken](https://docs.microsoft.com/rest/api/searchservice/create-index)

### <a name="step-3-create-an-indexer"></a>Stap 3: Maak een indexeerfunctie
Een indexeerfunctie een gegevensbron is verbonden met een doel search-index en vindt u een planning tooautomate Hallo gegevens vernieuwen.

Zodra het Hallo-index en gegevensbron zijn gemaakt, bent u klaar toocreate Hallo indexeerfunctie:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Elke twee uur wordt uitgevoerd door deze indexeerfunctie (schema-interval is ingesteld, te 'PT2H'). een indexeerfunctie toorun elke 30 minuten ingesteld hello-interval te 'PT30M'. Hallo kortste voor het interval is 5 minuten. Hallo schema is optioneel - als u dit weglaat, een indexeerfunctie slechts één keer is uitgevoerd wanneer deze gemaakt. U kunt echter een indexeerfunctie op aanvraag uitvoeren op elk gewenst moment.   

Voor meer informatie over Hallo indexeerfunctie-API maken, Bekijk [indexeerfunctie maken](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="how-azure-search-indexes-blobs"></a>Hoe Azure Search indexeert blobs

Afhankelijk van Hallo [indexeerfunctie configuratie](#PartsOfBlobToIndex), Hallo blob indexeerfunctie kunt indexeren opslag bestaan alleen uit metagegevens (is nuttig wanneer alleen voorzichtig over Hallo metagegevens en hoeft niet tooindex Hallo inhoud van BLOB's), metagegevens voor de opslag en inhoud, of beide metagegevens en tekstinhoud. Standaard haalt Hallo indexeerfunctie metagegevens en de inhoud.

> [!NOTE]
> Standaard worden de blobs met gestructureerde inhoud, zoals de JSON- of CSV geïndexeerd als een enkel deel van de tekst. Als u de blobs JSON en CSV tooindex gestructureerd wilt, Zie [indexeren JSON-blobs](search-howto-index-json-blobs.md) en [indexeren CSV blobs](search-howto-index-csv-blobs.md) preview-functies.
>
> Een samengestelde of ingesloten document (zoals een ZIP-archief of een Word-document met ingesloten Outlook e-mail met bijlagen) worden ook geïndexeerd als één document.

* Hallo tekstinhoud van Hallo document wordt geëxtraheerd in een tekenreeksveld met de naam `content`.

> [!NOTE]
> Azure Search beperkt hoeveel tekst worden uitgepakt, afhankelijk van Hallo prijscategorie: 32.000 tekens gratis laag, 64.000 voor Basic en 4 miljoen voor Standard-, Standard S2- en Standard-S3 lagen. Een waarschuwing is opgenomen in Hallo indexeerfunctie statusantwoord voor ingekorte documenten.  

* Eigenschappen van de gebruiker opgegeven metagegevens is aanwezig op Hallo blob, zijn indien van toepassing, uitgepakt woordelijk.
* Eigenschappen van de standaard blob-metagegevens worden uitgepakt in de volgende velden Hallo:

  * **metagegevens\_opslag\_naam** (Edm.String) - bestandsnaam Hallo van Hallo blob. Bijvoorbeeld, als er een /my-container/my-folder/subfolder/resume.pdf blob, Hallo-waarde van dit veld is `resume.pdf`.
  * **metagegevens\_opslag\_pad** (Edm.String) - Hallo volledige URI van de blob hello, met inbegrip van Hallo storage-account. Bijvoorbeeld: `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`
  * **metagegevens\_opslag\_inhoud\_type** (Edm.String) - inhoudstype zoals opgegeven door de code Hallo tooupload Hallo blob wordt gebruikt. Bijvoorbeeld `application/octet-stream`.
  * **metagegevens\_opslag\_laatste\_gewijzigd** (Edm.DateTimeOffset) - laatst gewijzigd tijdstempel voor Hallo blob. Azure Search gebruikt deze tijdstempel tooidentify gewijzigd blobs, tooavoid indexeren alles na het Hallo-indexering.
  * **metagegevens\_opslag\_grootte** (Edm.Int64) - blob-grootte in bytes.
  * **metagegevens\_opslag\_inhoud\_md5** (Edm.String) - MD5-hash van Hallo blob-inhoud, indien beschikbaar.
* Metagegevens eigenschappen specifieke tooeach documentindeling worden uitgepakt in Hallo velden [hier](#ContentSpecificMetadata).

U hoeft niet toodefine velden voor alle Hallo boven de eigenschappen in uw zoekindex - NET vastleggen Hallo-eigenschappen die u nodig hebt voor uw toepassing.

> [!NOTE]
> Hallo-veldnamen in uw bestaande index niet vaak hetzelfde Hallo veldnamen gegenereerd tijdens het uitpakken van het document. U kunt **veld toewijzingen** toomap Hallo-Eigenschapsnamen is verstrekt door Azure Search toohello-veldnamen in uw search-index. Hier ziet u een voorbeeld van een veld toewijzingen hieronder gebruiken.
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a>Document sleutels en veldtoewijzingen definiëren
In Azure Search identificatie Hallo documentsleutel unieke van een document. Elke search-index moet exact één sleutelveld van het type Edm.String hebben. Hallo sleutelveld is vereist voor elk document dat wordt toegevoegd toohello index (dit is daadwerkelijk Hallo alleen verplicht veld).  

U moet zorgvuldig overwegen welke uitgepakte veld toohello sleutelveld voor de index moet worden toegewezen. Hallo kandidaten zijn:

* **metagegevens\_opslag\_naam** : dit kan een handige kandidaat, maar houd er rekening mee dat 1) Hallo namen mogelijk niet uniek zijn, zoals u wellicht blobs met dezelfde naam in andere mappen Hallo en Hallo 2) de naam mag de tekens bevatten die zijn ongeldig in het document sleutels, zoals streepjes. U kunt maken met ongeldige tekens met behulp van Hallo `base64Encode` [veld toewijzing functie](search-indexer-field-mappings.md#base64EncodeFunction) : als u dit doet, tooencode document sleutels onthouden wanneer deze worden doorgegeven in de API zoals opzoeken aanroept. (Bijvoorbeeld in .NET kunt u Hallo [UrlTokenEncode methode](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) daarvoor).
* **metagegevens\_opslag\_pad** - uniekheid gebruik van het volledige pad Hallo zorgt, maar Hallo-pad bevat zeker `/` tekens [ongeldig in een documentsleutel](https://docs.microsoft.com/rest/api/searchservice/naming-rules).  Zoals hierboven, hebt u de optie Hallo HALLO hallo sleutels codering `base64Encode` [functie](search-indexer-field-mappings.md#base64EncodeFunction).
* Als geen van bovenstaande Hallo opties werkt, kunt u een aangepaste metagegevens eigenschap toohello blobs toevoegen. Deze optie is, de blob uploaden proces tooadd echter vereist dat metagegevens eigenschap tooall blobs. Aangezien het Hallo-sleutel is een vereiste eigenschap, mislukken alle blobs waarvoor geen die eigenschap toobe geïndexeerd.

> [!IMPORTANT]
> Als er geen expliciete toewijzing voor sleutelveld in Hallo index hello, gebruikt Azure Search automatisch `metadata_storage_path` zoals Hallo toegangssleutel en de base 64-gecodeerd sleutelwaarden (Hallo tweede optie hierboven).
>
>

In dit voorbeeld Hallo we kiezen `metadata_storage_name` veld Hallo documentsleutel. We gaan ook wordt ervan uitgegaan dat uw index heeft een sleutelveld `key` en een veld `fileSize` voor het opslaan van de grootte van de Hallo-document. toowire proces gewenste, geef Hallo volgende veldtoewijzingen bij het maken of bijwerken van de indexeerfunctie:

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

toobring deze allemaal samen hier hoe u het veldtoewijzingen en de inschakelen base 64-codering van sleutels voor een bestaande indexeerfunctie kunt toevoegen:

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> Zie toolearn meer informatie over het veldtoewijzingen [in dit artikel](search-indexer-field-mappings.md).
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a>Beheren welke blobs zijn geïndexeerd.
U kunt bepalen welke blobs worden geïndexeerd en die zijn overgeslagen.

### <a name="index-only-hello-blobs-with-specific-file-extensions"></a>Indexeer alleen Hallo blobs met specifieke extensies
U kunt alleen Hallo blobs met Hallo bestandsnaamextensies u opgeeft via Hallo index `indexedFileNameExtensions` configuratieparameter indexeerfunctie. Hallo-waarde is een tekenreeks met een door komma's gescheiden lijst met bestandsextensies (met een voorafgaande punt). Bijvoorbeeld: tooindex alleen hello. PDF en. DOCX blobs, doen dit:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a>BLOB's met bepaalde bestandsextensies uitsluiten
U kunt BLOB's met specifieke bestandsnaamextensies uitsluiten van het indexeren met Hallo `excludedFileNameExtensions` configuratieparameter. Hallo-waarde is een tekenreeks met een door komma's gescheiden lijst met bestandsextensies (met een voorafgaande punt). Bijvoorbeeld, blobs tooindex alle, behalve de Hello. PNG en. JPEG-extensies doen dit:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

Als beide `indexedFileNameExtensions` en `excludedFileNameExtensions` parameters aanwezig zijn, Azure Search eerst kijkt `indexedFileNameExtensions`, klikt u vervolgens op `excludedFileNameExtensions`. Dit betekent dat als hello dezelfde bestandsextensie aanwezig in beide lijsten is wordt uitgesloten van het indexeren.

### <a name="dealing-with-unsupported-content-types"></a>Omgaan met niet-ondersteunde typen inhoud

Standaard Hallo blob indexeerfunctie stopt zodra er een blob met een niet-ondersteunde inhoudstype (bijvoorbeeld een afbeelding) aangetroffen. U kunt uiteraard Hallo `excludedFileNameExtensions` parameter tooskip bepaalde typen inhoud. Echter, moet u mogelijk tooindex blobs zonder alle Hallo mogelijke inhoudstypen van tevoren weten. toocontinue indexeren als een niet-ondersteund type inhoud wordt aangetroffen, stel Hallo `failOnUnsupportedContentType` configuratieparameter te`false`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a>Fouten bij het parseren worden genegeerd

Azure Search document extractie logica is niet perfect en tooparse documenten met een ondersteund type inhoud soms zoals mislukken. DOCX of. PDF-BESTAND. Als u niet dat toointerrupt Hallo indexeren in dergelijke gevallen wilt, stelt u Hallo `maxFailedItems` en `maxFailedItemsPerBatch` parameters toosome redelijke configuratiewaarden. Bijvoorbeeld:

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-hello-blob-are-indexed"></a>Bepalen welke onderdelen van Hallo blob zijn geïndexeerd.

U kunt bepalen welke onderdelen van Hallo blobs zijn geïndexeerd met Hallo `dataToExtract` configuratieparameter. Het kan duren voordat Hallo volgende waarden:

* `storageMetadata`-Geeft aan dat alleen Hallo [standaard blob-eigenschappen en metagegevens gebruiker opgegeven](../storage/blobs/storage-properties-metadata.md) zijn geïndexeerd.
* `allMetadata`-Hiermee geeft u de opslag metagegevens en Hallo [inhoudstype specifieke metagegevens](#ContentSpecificMetadata) uitgepakt van Hallo blob inhoud worden geïndexeerd.
* `contentAndMetadata`-Geeft aan dat alle metagegevens en opgehaald uit de blob Hallo tekstinhoud worden geïndexeerd. Dit is de standaardwaarde Hallo.

Gebruik bijvoorbeeld tooindex alleen Hallo opslag metagegevens:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-toocontrol-how-blobs-are-indexed"></a>Met behulp van blob metagegevens toocontrol hoe blobs worden geïndexeerd

Hallo-configuratieparameters die hierboven worden beschreven toepassing tooall blobs. Soms is het raadzaam toocontrol hoe *afzonderlijke blobs* zijn geïndexeerd. U kunt dit doen door toe te voegen Hallo volgende blob-metagegevenseigenschappen en waarden:

| De naam van eigenschap | Waarde van eigenschap | Uitleg |
| --- | --- | --- |
| AzureSearch_Skip |'true' |Hiermee geeft u Hallo blob indexeerfunctie toocompletely overslaan Hallo blob. Uitpakken van metagegevens noch inhoud wordt uitgevoerd. Dit is handig wanneer een bepaalde blob herhaaldelijk mislukt en Hallo indexing-proces wordt onderbroken. |
| AzureSearch_SkipContent |'true' |Dit is het equivalent van `"dataToExtract" : "allMetadata"` instelling beschreven [hierboven](#PartsOfBlobToIndex) bereik tooa bepaalde blob. |

## <a name="incremental-indexing-and-deletion-detection"></a>Detectie van incrementele indexeren en verwijderen
Bij het instellen van een blob indexeerfunctie toorun volgens een planning, het opnieuw indexeren alleen Hallo blobs, gewijzigde zoals wordt bepaald door het Hallo-blob `LastModified` timestamp.

> [!NOTE]
> U hebt geen toospecify een detectie wijzigingsbeleid – incrementele indexeren automatisch voor u is ingeschakeld.

toosupport verwijderen documenten, gebruikt een benadering 'voorlopig verwijderen'. Als u Hallo blobs rechtstreekse verwijdert, worden overeenkomstige documenten uit Hallo search-index niet worden verwijderd. Gebruik in plaats daarvan Hallo stappen te volgen:  

1. Toevoegen van een aangepaste metagegevens eigenschap toohello blob tooindicate tooAzure zoeken logisch wordt verwijderd
2. Configureer een beleid voor voorlopig verwijderen op Hallo-gegevensbron
3. Nadat Hallo indexeerfunctie heeft verwerkt Hallo-blob (zoals weergegeven door de status van de indexeerfunctie Hallo API), kunt u fysiek Hallo blob verwijderen

Bijvoorbeeld, Hallo beleid na een blob toobe verwijderd als er een eigenschap metadata beschouwt `IsDeleted` met Hallo waarde `true`:

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a>Indexeren van grote gegevenssets

Indexeren van blobs, kan een tijdrovend proces zijn. In gevallen waar u miljoenen blobs tooindex hebt, kunt u versnellen door uw gegevens te partitioneren en het gebruik van meerdere indexeerfuncties tooprocess Hallo gegevens parallel te indexeren. Hier ziet u hoe u kunt dit instellen:

- Partitioneren van uw gegevens in meerdere blob-containers of virtuele mappen
- Instellen van meerdere Azure Search gegevensbronnen, één per container of de map. toopoint tooa blob-map, gebruik Hallo `query` parameter:

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- Maak een bijbehorende indexeerfunctie voor elke gegevensbron. Alle Indexeerfuncties kunnen punt toohello Hallo hetzelfde doel search-index.  

- Een zoekeenheid in uw service kan een indexeerfunctie worden uitgevoerd op elk moment. Maken van meerdere indexeerfuncties zoals hierboven beschreven, is alleen nuttig als ze daadwerkelijk parallel worden uitgevoerd. toorun meerdere indexeerfuncties parallel uitschalen uw search-service door het maken van een geschikt aantal partities en replica's. Bijvoorbeeld, als uw search-service heeft 6 search-eenheden (bijvoorbeeld 2 partities x 3 replica's), vervolgens 6 Indexeerfuncties kunnen tegelijkertijd worden uitgevoerd, wat resulteert in een six-fold toename in doorvoer voor indexering Hallo. toolearn meer informatie over schaalbaarheid en capaciteitsplanning, Zie [schalen niveaus van de bron voor query's en workloads in Azure Search indexeren](search-capacity-planning.md).

## <a name="indexing-documents-along-with-related-data"></a>Indexeren van documenten samen met verwante gegevens

U kunt te 'samenstellen' documenten uit meerdere bronnen in uw index. U kunt bijvoorbeeld toomerge tekst uit blobs met andere metagegevens die zijn opgeslagen in Cosmos-database. U kunt zelfs Hallo push indexering API samen met verschillende indexeerfuncties te bouwen documenten zoeken uit meerdere delen. 

Voor deze toowork moeten alle Indexeerfuncties en andere onderdelen tooagree op Hallo documentsleutel. Zie voor een gedetailleerde procedure in dit artikel externe: [documenten worden gecombineerd met andere gegevens in Azure Search ](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html).

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a>Indexering als tekst zonder opmaak 

Als u al uw blobs bevatten tekst zonder opmaak in dezelfde codering hello, kunt u indexering prestaties aanzienlijk verbeteren met behulp van **modus voor het parseren van tekst**. toouse tekst bij het parseren van modus set Hallo `parsingMode` configuratie-eigenschap te`text`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

Standaard Hallo `UTF-8` codering wordt verondersteld. een andere codering toospecify gebruiken Hallo `encoding` configuratie-eigenschap: 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a>Eigenschappen voor typespecifieke metagegevens van inhoud
Hallo volgende tabel geeft een overzicht van de verwerking wordt uitgevoerd voor elke documentindeling en beschrijft eigenschappen voor metagegevens Hallo door Azure Search hebt uitgepakt.

| Documentindeling / type inhoud | Eigenschappen van de specifieke metagegevens inhoudstype | Verwerkingsgegevens |
| --- | --- | --- |
| HTML-CODE (`text/html`) |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |HTML-opmaak van strook / en haal de tekst |
| PDF-BESTAND (`application/pdf`) |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |Haal de tekst, inclusief ingesloten documenten (met uitzondering van installatiekopieën) |
| DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Haal de tekst, inclusief ingesloten documenten |
| DOC (application/msword) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Haal de tekst, inclusief ingesloten documenten |
| XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Haal de tekst, inclusief ingesloten documenten |
| XLS (toepassing/vnd.ms-excel) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Haal de tekst, inclusief ingesloten documenten |
| PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Haal de tekst, inclusief ingesloten documenten |
| PPT (vnd.ms-toepassing-powerpoint) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Haal de tekst, inclusief ingesloten documenten |
| Bericht (vnd.ms-toepassing-outlook) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |Haal de tekst, met inbegrip van bijlagen |
| ZIP (toepassing/zip) |`metadata_content_type` |Haal de tekst uit alle documenten in Hallo archief |
| XML (application/xml) |`metadata_content_type`</br>`metadata_content_encoding`</br> |XML-opmaak van strook / en haal de tekst |
| JSON (application/json) |`metadata_content_type`</br>`metadata_content_encoding` |Haal de tekst<br/>Opmerking: Als u meerdere documenten uit een JSON-blob velden tooextract nodig hebt, raadpleegt u [indexeren JSON-blobs](search-howto-index-json-blobs.md) voor meer informatie |
| EML (bericht/rfc822) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |Haal de tekst, met inbegrip van bijlagen |
| RTF-indeling (toepassing/rtf) |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | Haal de tekst|
| Tekst zonder opmaak (text/plain) |`metadata_content_type`</br>`metadata_content_encoding`</br> | Haal de tekst|


## <a name="help-us-make-azure-search-better"></a>Help ons Azure Search te verbeteren
Als u functieaanvragen of suggesties voor verbeteringen hebt, laat ons weten op onze [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).
