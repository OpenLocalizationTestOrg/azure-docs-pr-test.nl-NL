---
title: aaaUpgrading toohello Azure Search .NET SDK versie 1.1 | Microsoft Docs
description: Een upgrade toohello Azure Search .NET SDK versie 1.1
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a>Een upgrade toohello Azure Search .NET SDK versie 3
Als u versie 2.0 preview of oudere Hallo [Azure Search .NET SDK](https://aka.ms/search-sdk), dit artikel helpt u bij het bijwerken van uw toepassing toouse versie 3.

Zie voor een meer algemene overzicht Hallo SDK inclusief voorbeelden [hoe toouse Azure zoeken vanuit een .NET-toepassing](search-howto-dotnet-sdk.md).

Versie 3 van hello Azure Search .NET SDK bevat een aantal wijzigingen uit eerdere versies. Dit zijn vooral kleine, zodat u uw code wijzigt, moet alleen minimale inspanning nodig. Zie [stappen tooupgrade](#UpgradeSteps) voor instructies over het toochange uw code toouse Hallo nieuwe SDK-versie.

> [!NOTE]
> Als u versie 1.0.2-preview of ouder, u moet eerst tooversion 1.1 upgraden en vervolgens bijwerken tooversion 3. Zie [bijlage: stappen tooupgrade tooversion 1.1](#UpgradeStepsV1) voor instructies.
>
> Verschillende versies van de REST-API, met inbegrip van de meest recente Hallo biedt ondersteuning voor uw Azure Search-service-exemplaar. Wanneer deze niet langer Hallo recentste is, maar het is raadzaam dat u de nieuwste versie van code toouse Hallo migreert, kunt u een versie toouse blijven. Wanneer u Hallo REST-API gebruikt, moet u Hallo API-versie opgeven in elke aanvraag via Hallo api-versie-parameter. Wanneer u Hallo .NET SDK, bepaalt Hallo-versie van Hallo SDK u de desbetreffende versie Hallo Hallo REST-API. Als u een oudere SDK gebruikt, kunt u blijven toorun die code zonder wijzigingen als Hallo service bijgewerkte toosupport een nieuwere API-versie.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a>Wat is er nieuw in versie 3
Versie 3 hello Azure Search .NET SDK doelen Hallo laatste algemeen beschikbaar versie van hello Azure Search REST API specifiek 2016-09-01. Dit maakt het mogelijk toouse vele nieuwe functies van Azure Search vanuit een .NET-toepassing, waaronder de volgende Hallo:

* [Analysevoorzieningen aanpassen](https://aka.ms/customanalyzers)
* [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) en [Azure Table Storage](search-howto-indexing-azure-tables.md) indexeerfunctie-ondersteuning
* Aanpassing van de indexeerfunctie via [veld toewijzingen](search-indexer-field-mappings.md)
* ETags ondersteuning voor het tooenable veilige gelijktijdige bijwerken van definities, Indexeerfuncties en gegevensbronnen van index
* Ondersteuning voor het bouwen van de index velddefinities declaratief door uw modelklasse versieren en Hallo nieuwe `FieldBuilder` klasse.
* Ondersteuning voor .NET Core en draagbare .NET-profiel 111

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Stappen tooupgrade
Eerst uw NuGet-verwijzing voor bijwerken `Microsoft.Azure.Search` beide Hallo NuGet Package Manager-Console of door met de rechtermuisknop op uw projectverwijzingen te selecteren 'Beheren NuGet-pakketten...' in Visual Studio.

Zodra de NuGet heeft nieuwe hello-pakketten en afhankelijkheden zijn gedownload, opnieuw worden opgebouwd uw project. Afhankelijk van hoe uw code is gestructureerd, deze mogelijk opnieuw worden opgebouwd is. Als dit het geval is, bent u klaar toogo!

Als uw build is mislukt, kunt u een opbouwfout Hallo volgende moeten zien:

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

de volgende stap Hallo toofix is deze build-fout. Zie [wijzigingen op te splitsen in versie 3](#ListOfChanges) voor meer informatie over wat Hallo-fout veroorzaakt en hoe toofix deze.

Mogelijk ziet u extra build waarschuwingen gerelateerde tooobsolete methoden of eigenschappen. Hallo waarschuwingen bevat instructies over welke toouse in plaats daarvan Hallo functie afgeschafte. Bijvoorbeeld, als uw toepassing gebruikt Hallo `IndexingParameters.Base64EncodeKeys` eigenschap, krijgt u een waarschuwing dat`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`

Als u eventuele fouten in de build hebt opgelost, kunt u wijzigingen aanbrengen tooyour toepassing tootake profiteren van nieuwe functionaliteit als u wenst. Nieuwe functies in Hallo SDK worden beschreven in [wat is er nieuw in versie 3](#WhatsNew).

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a>Wijzigingen op te splitsen in versie 3
Er wijzigingen een klein aantal grote wijzigingen in versie 3 waarvoor code bovendien toorebuilding uw toepassing.

### <a name="indexesgetclient-return-type"></a>Het retourtype Indexes.GetClient
Hallo `Indexes.GetClient` methode heeft een nieuwe retourtype. Voorheen geretourneerd `SearchIndexClient`, maar dit is te wijzigen`ISearchIndexClient` in preview-versie 2.0 en die wijziging weerspiegelt tooversion 3. Dit is toosupport klanten die toomock Hallo willen `GetClient` methode voor de eenheidstests door te retourneren van een mock-implementatie van `ISearchIndexClient`.

#### <a name="example"></a>Voorbeeld
Als uw code ziet er als volgt:

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a>AnalyzerName, gegevenstype en andere zijn niet langer impliciet converteerbare toostrings
Er zijn vele typen in hello Azure Search .NET SDK, die zijn afgeleid van `ExtensibleEnum`. Eerder deze typen zijn alle impliciet converteerbare tootype `string`. Echter een probleem is gedetecteerd op Hallo `Object.Equals` implementatie voor deze klassen en corrigeren Hallo bug vereist deze impliciete conversie uit te schakelen. Expliciete conversie te`string` is wel toegestaan.

#### <a name="example"></a>Voorbeeld
Als uw code ziet er als volgt:

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a>Verouderd leden verwijderd

Mogelijk ziet u eigenschappen die zijn gemarkeerd als verouderd in de preview-versie 2.0 en daarna zijn verwijderd in versie 3 of build fouten gerelateerde toomethods. Als u dergelijke fouten optreden, wordt hier hoe tooresolve ze:

- Als u deze constructor: `ScoringParameter(string name, string value)`, gebruik in plaats daarvan deze:`ScoringParameter(string name, IEnumerable<string> values)`
- Als u eerder Hallo `ScoringParameter.Value` eigenschap, gebruik Hallo `ScoringParameter.Values` eigenschap of Hallo `ToString` methode in plaats daarvan.
- Als u eerder Hallo `SearchRequestOptions.RequestId` eigenschap, gebruik Hallo `ClientRequestId` eigenschap in plaats daarvan.

### <a name="removed-preview-features"></a>Verwijderde preview-functies

Als u een van versie 2.0 preview tooversion 3 upgrade, worden op de hoogte dat JSON en CSV-ondersteuning voor Blob indexeerfuncties parseren is verwijderd omdat deze functies zijn nog steeds in preview. In het bijzonder Hallo volgende methoden Hallo `IndexingParametersExtensions` klasse zijn verwijderd:

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

Als uw toepassing een vaste afhankelijkheid van deze functies heeft, zich u niet kunnen tooupgrade tooversion 3 Hallo Azure Search .NET SDK. U kunt blijven toouse versie 2.0-preview. Echter, neem Houd rekening met het **we raden niet met behulp van voorbeeld SDK's in productietoepassingen**. Preview-functies voor evaluatie alleen zijn en kunnen worden gewijzigd.

## <a name="conclusion"></a>Conclusie
Als u meer informatie over het gebruik van Azure Search .NET SDK Hallo nodig hebt, raadpleegt u onze onlangs bijgewerkt [How-to](search-howto-dotnet-sdk.md).

Uw feedback is Welkom op Hallo SDK. Als u problemen ondervindt, kunt u gratis tooask ons voor hulp bij het Hallo [Azure Search MSDN-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch). Als u een bug vinden, kunt u een probleem bestanden per Hallo [Azure .NET SDK GitHub-opslagplaats](https://github.com/Azure/azure-sdk-for-net/issues). Zorg ervoor dat tooprefix de titel van uw probleem met ' Search SDK: '.

Hartelijk dank voor het gebruik van Azure Search.

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a>Bijlage: Stappen tooupgrade tooversion 1.1
> [!NOTE]
> Deze sectie geldt alleen toousers van hello Azure Search .NET SDK versie 1.0.2-preview en ouder.
> 
> 

Eerst uw NuGet-verwijzing voor bijwerken `Microsoft.Azure.Search` beide Hallo NuGet Package Manager-Console of door met de rechtermuisknop op uw projectverwijzingen te selecteren 'Beheren NuGet-pakketten...' in Visual Studio.

Zodra de NuGet heeft nieuwe hello-pakketten en afhankelijkheden zijn gedownload, opnieuw worden opgebouwd uw project.

Als u eerder met versie 1.0.0-preview, 1.0.1-preview of 1.0.2-preview, Hallo build moet slagen en u bent klaar toogo!

Als u eerder versie 0.13.0-preview of ouder, ziet u fouten Hallo volgende maken:

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

de volgende stap Hallo is fouten in de build toofix Hallo één voor één. De meeste moeten sommige klasse en methode namen die zijn gewijzigd in Hallo SDK wijzigen. [Lijst met wijzigingen op te splitsen in versie 1.1](#ListOfChangesV1) bevat een overzicht van deze wijzigingen in de naam.

Als u aangepaste klassen toomodel uw documenten en deze klassen eigenschappen met niet-nullbare primitieve typen hebben (bijvoorbeeld `int` of `bool` in C#), er is een fix bug in Hallo 1.1-versie van Hallo-SDK van waarmee u houden moet rekening. Zie [oplossingen voor problemen in versie 1.1](#BugFixesV1) voor meer informatie.

Ten slotte, als u eventuele fouten in de build hebt opgelost, kunt u wijzigingen aanbrengen tooyour toepassing tootake profiteren van nieuwe functionaliteit als u wenst.

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a>Lijst met wijzigingen op te splitsen in versie 1.1
Hallo is hieronder geordend op Hallo kans dat Hallo wijziging invloed is op uw toepassingscode.

#### <a name="indexbatch-and-indexaction-changes"></a>Wijzigingen in IndexBatch en IndexAction
`IndexBatch.Create`de naam is gewijzigd te`IndexBatch.New` en niet langer heeft een `params` argument. U kunt `IndexBatch.New` voor batches die een mix van verschillende soorten acties (samenvoegingen, verwijderingen, enzovoort). Bovendien, er zijn nieuwe statische methoden voor het maken van batches waar alle Hallo acties zijn Hallo dezelfde: `Delete`, `Merge`, `MergeOrUpload`, en `Upload`.

`IndexAction`Openbare constructors beschikt niet langer over en de eigenschappen zijn nu niet-wijzigbaar. U moet Hallo nieuwe statische methoden gebruiken voor het maken van acties voor verschillende doeleinden: `Delete`, `Merge`, `MergeOrUpload`, en `Upload`. `IndexAction.Create`is verwijderd. Als u Hallo overbelasting waarvoor alleen een document hebt gebruikt, moet u ervoor toouse `Upload` in plaats daarvan.

##### <a name="example"></a>Voorbeeld
Als uw code ziet er als volgt:

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

Als u wilt, kunt u verder vereenvoudigen het toothis:

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a>IndexBatchException wijzigingen
Hallo `IndexBatchException.IndexResponse` eigenschap heeft gekregen te`IndexingResults`, en het type is nu `IList<IndexingResult>`.

##### <a name="example"></a>Voorbeeld
Als uw code ziet er als volgt:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a>Bewerking methode wijzigingen
Elke bewerking in hello Azure Search .NET SDK is beschikbaar als een set van methode overloads voor synchrone en asynchrone aanroepfuncties. Hallo is handtekeningen en waarbij van de overloads van deze methode gewijzigd in versie 1.1.

Hallo 'indexstatistieken ophalen'-bewerking in oudere versies van Hallo SDK blootgesteld bijvoorbeeld deze handtekeningen:

In `IIndexOperations`:

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

In `IndexOperationsExtensions`:

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

Hallo methode handtekeningen voor Hallo dezelfde bewerking in versie 1.1 zien er als volgt:

In `IIndexesOperations`:

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

In `IndexesOperationsExtensions`:

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

Vanaf versie 1.1 ordent hello Azure Search .NET SDK bewerking methoden anders:

* Optionele parameters zijn nu gemodelleerd als parameters in plaats daarvan standaard dan aanvullende methode overloads. Hierdoor Hallo aantal methode overloads, soms aanzienlijk wordt gereduceerd.
* Hallo uitbreidingsmethoden verbergen nu een groot aantal Hallo overbodige details van HTTP van Hallo aanroeper. Bijvoorbeeld, oudere versies van Hallo SDK een antwoordobject met een HTTP-statuscode die u vaak een geretourneerd toocheck niet nodig omdat bewerking methoden throw `CloudException` voor elke statuscode die een fout aangeeft. nieuwe uitbreiding methoden NET return modelobjecten Hallo, Hallo niet meer toounwrap hoeft op te slaan u ze in uw code.
* Als u daarentegen tonen hello core interfaces nu methoden waarmee u meer controle op Hallo HTTP niveau als u deze nodig hebt. U kunt nu doorgeven in aangepaste HTTP-headers toobe opgenomen in aanvragen en nieuwe Hallo `AzureOperationResponse<T>` retourneren type biedt u directe toegang toohello `HttpRequestMessage` en `HttpResponseMessage` voor Hallo-bewerking. `AzureOperationResponse`is gedefinieerd in Hallo `Microsoft.Rest.Azure` naamruimte en vervangt `Hyak.Common.OperationResponse`.

#### <a name="scoringparameters-changes"></a>ScoringParameters wijzigingen
Een nieuwe klasse met de naam `ScoringParameter` is toegevoegd in de nieuwste SDK toomake Hallo eenvoudiger tooprovide parameters tooscoring profielen in een zoekopdracht. Eerder Hallo `ScoringProfiles` eigenschap Hallo `SearchParameters` klasse was getypeerd als `IList<string>`; Nu het is getypeerd als `IList<ScoringParameter>`.

##### <a name="example"></a>Voorbeeld
Als uw code ziet er als volgt:

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen: 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a>Wijzigingen in het gegevensmodel klasse
Vervaldatum toohello handtekening wijzigingen beschreven in [bewerking methode wijzigingen](#OperationMethodChanges), veel klassen in Hallo `Microsoft.Azure.Search.Models` naamruimte hebt gewijzigd of verwijderd. Bijvoorbeeld:

* `IndexDefinitionResponse`is vervangen door`AzureOperationResponse<Index>`
* `DocumentSearchResponse`naam te is gewijzigd`DocumentSearchResult`
* `IndexResult`naam te is gewijzigd`IndexingResult`
* `Documents.Count()`nu retourneert een `long` met Hallo document telling in plaats van een`DocumentCountResponse`
* `IndexGetStatisticsResponse`naam te is gewijzigd`IndexGetStatisticsResult`
* `IndexListResponse`naam te is gewijzigd`IndexListResult`

toosummarize, `OperationResponse`-afgeleide klassen die beschikbaar waren alleen toowrap een modelobject zijn verwijderd. Hallo resterende klassen hebben gehad hun achtervoegsel gewijzigd van `Response` te`Result`.

##### <a name="example"></a>Voorbeeld
Als uw code ziet er als volgt:

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a>Antwoord klassen en IEnumerable
Een aanvullende wijzigen die invloed kan zijn op uw code is dat antwoord-klassen die verzamelingen houdt niet langer implementeren `IEnumerable<T>`. In plaats daarvan kunt u de verzamelingseigenschap Hallo rechtstreeks openen. Als bijvoorbeeld uw code ziet er als volgt:

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a>Speciaal geval voor webtoepassingen
Als u een webtoepassing die serialiseert `DocumentSearchResponse` direct toosend toohello browser zoekresultaten, moet u toochange uw code of Hallo resultaten niet correct worden geconverteerd. Als bijvoorbeeld uw code ziet er als volgt:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

U kunt dit wijzigen door Hallo `.Results` eigenschap van Hallo zoeken antwoord toofix zoeken resultaat rendering:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

Hebt u toolook voor dergelijke gevallen in uw code zelf; **Hallo compiler wordt geen waarschuwing** omdat `JsonResult.Data` is van het type `object`.

#### <a name="cloudexception-changes"></a>CloudException wijzigingen
Hallo `CloudException` klasse is verplaatst van Hallo `Hyak.Common` naamruimte toohello `Microsoft.Rest.Azure` naamruimte. Ook de `Error` eigenschap heeft gekregen te`Body`.

#### <a name="searchserviceclient-and-searchindexclient-changes"></a>Wijzigingen in SearchServiceClient en SearchIndexClient
type Hallo Hallo `Credentials` eigenschap is gewijzigd van `SearchCredentials` tooits basisklasse `ServiceClientCredentials`. Als u nodig hebt tooaccess hello `SearchCredentials` van een `SearchIndexClient` of `SearchServiceClient`, gebruik Hallo nieuwe `SearchCredentials` eigenschap.

In oudere versies van Hallo SDK, `SearchServiceClient` en `SearchIndexClient` had constructors die een `HttpClient` parameter. Deze zijn vervangen door een constructors die een `HttpClientHandler` en een matrix van `DelegatingHandler` objecten. Dit maakt het eenvoudiger tooinstall aangepaste handlers toopre proces HTTP-aanvragen indien nodig.

Ten slotte Hallo constructors die een `Uri` en `SearchCredentials` zijn gewijzigd. Bijvoorbeeld, als er een code die er als volgt uit:

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

Ook opmerking dat Hallo Hallo type parameter referenties te is gewijzigd`ServiceClientCredentials`. Dit is waarschijnlijk niet tooaffect uw code sinds `SearchCredentials` is afgeleid van `ServiceClientCredentials`.

#### <a name="passing-a-request-id"></a>Een aanvraag-ID doorgeven
In oudere versies van Hallo SDK kan stelt u een aanvraag-ID op Hallo `SearchServiceClient` of `SearchIndexClient` en zou worden opgenomen in elke aanvraag toohello REST-API. Dit is handig voor het oplossen van problemen met uw search-service als u toocontact ondersteuning nodig hebt. Het is echter nuttiger tooset een unieke aanvraag-ID voor elke bewerking in plaats van toouse Hallo dezelfde ID voor alle bewerkingen. Om deze reden Hallo `SetClientRequestId` methoden van `SearchServiceClient` en `SearchIndexClient` zijn verwijderd. In plaats daarvan kunt u doorgeven een aanvraag-ID tooeach bewerkingsmethode via Hallo optionele `SearchRequestOptions` parameter.

> [!NOTE]
> In een toekomstige release Hallo SDK wordt er een nieuw mechanisme voor het instellen van een aanvraag-ID globaal op Hallo client objecten die consistent zijn met de Hallo benadering die wordt gebruikt door andere Azure-SDK toevoegen.
> 
> 

#### <a name="example"></a>Voorbeeld
Als u hebt de code die er als volgt uit:

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a>Wijzigingen in de naam van de gebruikersinterface
Hallo bewerking groepsnamen interface hebben alle gewijzigde toobe consistent zijn met de bijbehorende Eigenschapsnamen:

* type Hallo `ISearchServiceClient.Indexes` gewijzigd van `IIndexOperations` te`IIndexesOperations`.
* type Hallo `ISearchServiceClient.Indexers` gewijzigd van `IIndexerOperations` te`IIndexersOperations`.
* type Hallo `ISearchServiceClient.DataSources` gewijzigd van `IDataSourceOperations` te`IDataSourcesOperations`.
* type Hallo `ISearchIndexClient.Documents` gewijzigd van `IDocumentOperations` te`IDocumentsOperations`.

Deze wijziging is waarschijnlijk niet tooaffect uw code, tenzij u mocks van deze interfaces voor testdoeleinden gemaakt.

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a>Oplossingen voor problemen in versie 1.1
Er is een fout in oudere versies van hello Azure Search .NET SDK betreffende tooserialization van aangepaste modelklassen. Hallo fout kan optreden als u een aangepaste modelklasse met een eigenschap van een niet-nullbare waardetype gemaakt.

#### <a name="steps-tooreproduce"></a>Stappen tooreproduce
Maak een aangepaste modelklasse met een eigenschap van niet-nullbare waardetype. Bijvoorbeeld, Voeg een openbare `UnitCount` eigenschap van het type `int` in plaats van `int?`.

Als u een document met de standaardwaarde Hallo van dat type index (bijvoorbeeld 0 voor `int`), Hallo veld wordt niet null zijn in Azure Search. Als u dat document vervolgens zoekt, Hallo `Search` aanroep genereert `JsonSerializationException` klagen dat kan niet worden geconverteerd `null` te`int`.

Ook filters werkt mogelijk niet zoals verwacht omdat null toohello index in plaats van de waarde Hallo bedoeld is geschreven.

#### <a name="fix-details"></a>Gegevens herstellen
We hebben dit probleem opgelost in versie 1.1 van Hallo SDK. Op dit moment hebt u een modelklasse als volgt:

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

en u `IntValue` too0, dat waarde is nu correct geserialiseerd als 0 op Hallo kabel en als 0 in Hallo index opgeslagen. Ophalen ook werkt zoals verwacht.

Er is een mogelijk probleem toobe op de hoogte met deze methode: als u een modeltype met een niet-nullbare eigenschap gebruikt, hebt u te**garanderen** dat de documenten in uw index geen null-waarde voor het betreffende veld Hallo bevatten. Hallo SDK noch hello Azure Search REST API kunt u tooenforce dit.

Dit is niet alleen een hypothetische probleem: Stel een scenario waarin het toevoegen van een nieuw veld tooan bestaande index van het type `Edm.Int32`. Na het bijwerken van de indexdefinitie hello, moeten alle documenten een null-waarde voor het nieuwe veld (omdat alle typen null in Azure Search). Als u vervolgens een modelklasse met een niet-nullbare `int` eigenschap voor dat veld gebruikt, ontvangt u een `JsonSerializationException` zoals deze bij het tooretrieve documenten:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Daarom nog steeds wordt aangeraden nullbare typen te gebruiken in uw modelklassen als een best practice.

Zie voor meer informatie over deze fout en Hallo correctie [dit probleem op GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).

