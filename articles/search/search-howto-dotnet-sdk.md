---
title: aaaHow toouse Azure Search vanuit een .NET-toepassing | Microsoft Docs
description: Hoe toouse Azure zoeken vanuit een .NET-toepassing
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a>Hoe toouse Azure zoeken vanuit een .NET-toepassing
In dit artikel wordt een overzicht tooget u snel Hello [Azure Search .NET SDK](https://aka.ms/search-sdk). U kunt Hallo .NET SDK tooimplement een uitgebreide ervaring van uw toepassing met behulp van Azure Search zoeken.

## <a name="whats-in-hello-azure-search-sdk"></a>Wat is er in hello Azure Search SDK
Hallo SDK bestaat uit een clientbibliotheek `Microsoft.Azure.Search`. Deze maakt u toomanage uw indexen, gegevensbronnen en indexeerfuncties, evenals uploaden documenten beheren en uitvoeren van query's zonder te hoeven toodeal met details op Hallo van HTTP- en JSON.

Hallo-clientbibliotheek definieert klassen als `Index`, `Field`, en `Document`, evenals bewerkingen, zoals `Indexes.Create` en `Documents.Search` op Hallo `SearchServiceClient` en `SearchIndexClient` klassen. Deze klassen zijn ingedeeld in Hallo volgende naamruimten:

* [Microsoft.Azure.Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [Microsoft.Azure.Search.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

de huidige versie Hallo van hello Azure Search .NET SDK is nu algemeen beschikbaar. Als u tooprovide feedback wilt voor ons tooincorporate in de volgende versie hello, gaat u naar onze [feedbackpagina](https://feedback.azure.com/forums/263029-azure-search/).

Hallo .NET SDK versie ondersteunt `2016-09-01` Hallo [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/). Deze versie biedt nu ondersteuning voor aangepaste analyzers en ondersteuning van Azure-Blob en Azure Table-indexeerfunctie. Preview-functies die zijn *niet* deel uitmaken van deze versie, zoals ondersteuning voor het indexeren van JSON en CSV-bestanden bevinden zich in [preview](search-api-2015-02-28-preview.md) en beschikbaar via Hallo oudere [2.0-preview-versie van Hallo .NET SDK ](https://aka.ms/search-sdk-preview).

Deze SDK biedt geen ondersteuning voor [beheerbewerkingen](https://docs.microsoft.com/rest/api/searchmanagement/) zoals maken en schalen van de Search-services en API-sleutels beheren. Als u toomanage uw zoeken in resources van een .NET-toepassing moet, kunt u Hallo [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a>Bijwerken van de meest recente versie toohello van Hallo SDK
Als u al een oudere versie van hello Azure Search .NET SDK en u tooupgrade toohello nieuwe algemeen beschikbaar versie dat wilt, [in dit artikel](search-dotnet-sdk-migration.md) wordt uitgelegd hoe.

## <a name="requirements-for-hello-sdk"></a>Vereisten voor Hallo SDK
1. Visual Studio 2017.
2. Uw eigen Azure Search-service. In de volgorde toouse Hallo SDK moet u Hallo-naam van uw service en een of meer API-sleutels. [Maken van een service in de portal Hallo](search-create-service-portal.md) helpt u bij deze stappen.
3. Hello Azure Search .NET SDK downloaden [NuGet-pakket](http://www.nuget.org/packages/Microsoft.Azure.Search) met behulp van 'NuGet-pakketten beheren' in Visual Studio. Zoeken Hallo pakketnaam `Microsoft.Azure.Search` op NuGet.org.

Hello Azure Search .NET SDK biedt ondersteuning voor toepassingen die gericht is op Hallo .NET Framework 4.6 en .NET Core.

## <a name="core-scenarios"></a>Belangrijkste scenario 's
Er zijn verschillende dingen die u moet toodo in uw zoektoepassing. In deze zelfstudie aan bod deze belangrijkste scenario's:

* Een index te maken
* Hallo-index met de documenten in te vullen
* Zoeken naar documenten met behulp van de zoekopdracht in volledige tekst en filters

Hallo voorbeeldcode die volgt illustreert elk van deze. U kunt gratis toouse Hallo codefragmenten in uw eigen toepassing.

### <a name="overview"></a>Overzicht
Hallo voorbeeldtoepassing we je worden verkennen maakt u een nieuwe index met de naam "hotels" gevuld met een paar documenten en vervolgens bepaalde zoekquery's worden uitgevoerd. Hier volgt Hallo belangrijkste programma, met algemene stroom Hallo:

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> U vindt de volledige broncode Hallo van Hallo-voorbeeldtoepassing die is gebruikt in deze doorloop op [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).
> 
>

We doorlopen deze stap voor stap. Eerst moet u toocreate een nieuwe `SearchServiceClient`. Dit object maakt toomanage indexen. In de volgorde tooconstruct een moet u tooprovide de naam van uw Azure Search-service, evenals een beheer-API-sleutel. U kunt deze informatie invoeren in Hallo `appsettings.json` bestand Hallo [voorbeeldtoepassing](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> Als u een onjuist sleutel (bijvoorbeeld een query waarin een beheersleutel vereist is), Hallo `SearchServiceClient` genereert een `CloudException` Hallo fout bericht 'Verboden' Hello eerste keer dat u een bewerkingsmethode aanroepen, zoals `Indexes.Create`. Als dit tooyou gebeurt, Controleer onze API-sleutel.
> 
> 

Hallo aanroepen volgende paar regels methoden toocreate index met de naam "hotels", eerst verwijderen als deze al bestaat. We doorlopen die deze methoden enigszins hoger.

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

Hallo-index moet vervolgens toobe ingevuld. toodo, moeten we een `SearchIndexClient`. Er zijn twee manieren tooobtain een: door deze samen te stellen of door het aanroepen van `Indexes.GetClient` op Hallo `SearchServiceClient`. We Hallo laatstgenoemde gebruiken voor het gemak.

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> In een standaardzoektoepassing wordt het beheer van de index en de invulling daarvan afgehandeld door een afzonderlijk onderdeel van de zoekquery’s. `Indexes.GetClient`is handig voor het invullen van een index, omdat u problemen van het bieden van een andere Hallo `SearchCredentials`. Dit wordt uitgevoerd door Hallo beheersleutel doorgeeft die gebruikte toocreate u Hallo `SearchServiceClient` toohello nieuwe `SearchIndexClient`. Hallo deel van uw toepassing waarmee query's uitvoert, het is echter beter toocreate hello `SearchIndexClient` rechtstreeks zodat u in een querysleutel in plaats van een administratorsleutel doorgeven kunt. Dit is consistent met de Hallo principe van minimale bevoegdheden en helpt uw toepassing veiliger toomake. U vindt meer informatie over administratorsleutels en querysleutels [hier](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).
> 
> 

Nu dat we hebben een `SearchIndexClient`, we Hallo index kunt vullen. Dit wordt gedaan door een andere methode die u kunt later zien.

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

Ten slotte we enkele zoekopdrachten uitvoeren en Hallo resultaten weer te geven. Nu we gebruiken een ander `SearchIndexClient`:

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

Laten we bekijkt hello `RunQueries` methode later. Hier volgt Hallo code toocreate Hallo nieuwe `SearchIndexClient`:

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

Nu we een querysleutel gebruiken aangezien er geen schrijftoegang toohello index hoeft. U kunt deze informatie invoeren in Hallo `appsettings.json` bestand Hallo [voorbeeldtoepassing](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

Als u deze toepassing met een geldige servicenaam en API-sleutels uitvoert, er Hallo uitvoer als volgt:

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

de volledige broncode Hallo van de toepassing hello wordt op Hallo einde van dit artikel aangeboden.

We zullen Haal vervolgens bekijkt hello methoden aangeroepen door `Main`.

### <a name="creating-an-index"></a>Een index te maken
Na het maken van een `SearchServiceClient`, Hallo volgende dat `Main` biedt is delete Hallo "hotels" index als deze al bestaat. Dat is gebeurd door Hallo methode te volgen:

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

Deze methode gebruikt Hallo gegeven `SearchServiceClient` toocheck als Hallo index bestaat, en zo ja, verwijderen.

> [!NOTE]
> Hallo voorbeeldcode in dit artikel gebruikt synchrone methoden Hallo Hallo Azure Search .NET SDK voor eenvoud. Aangeraden Hallo asynchrone methoden te gebruiken in uw eigen toepassingen tookeep ze schaalbaar en responsief. Bijvoorbeeld, in de Hallo methode boven gebruiken `ExistsAsync` en `DeleteAsync` in plaats van `Exists` en `Delete`.
> 
> 

Vervolgens `Main` maakt een nieuwe index "hotels" door deze methode aanroept:

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

Deze methode maakt u een nieuwe `Index` object met een lijst met `Field` objecten die Hallo-schema van de nieuwe Hallo-index definieert. Elk veld heeft een naam, gegevenstype en verschillende kenmerken die het zoekgedrag definiëren. Hallo `FieldBuilder` reflectie toocreate een lijst met klasse gebruikt `Field` objecten voor index vindt van Hallo Hallo openbare eigenschappen en kenmerken van Hallo gegeven `Hotel` modelklasse. We gaan die nader bekeken Hallo `Hotel` klasse later op.

> [!NOTE]
> U kunt altijd Hallo lijst maken met `Field` objecten rechtstreeks in plaats van `FieldBuilder` indien nodig. Bijvoorbeeld, kunt u niet een modelklasse toouse of moet u een bestaande modelklasse die u niet toomodify wilt door toe te voegen kenmerken toouse.
>
> 

Bovendien toofields, u kunt ook toevoegen scoreprofiel profielen, suggestiefunctie of CORS opties toohello Index (deze weggelaten van Hallo voorbeeld als beknopt alternatief bevat). U vindt meer informatie over Hallo indexobject en de samenstellende delen in Hallo [SDK-naslaginformatie](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), evenals als in Hallo [Azure Search REST API-verwijzing](https://docs.microsoft.com/rest/api/searchservice/).

### <a name="populating-hello-index"></a>Hallo-index te vullen
de volgende stap Hallo in `Main` toopopulate Hallo gemaakte index is. Dit doet u in de volgende methode Hallo:

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
        new Hotel()
        { 
            HotelId = "1", 
            BaseRate = 199.0, 
            Description = "Best hotel in town",
            DescriptionFr = "Meilleur hôtel en ville",
            HotelName = "Fancy Stay",
            Category = "Luxury", 
            Tags = new[] { "pool", "view", "wifi", "concierge" },
            ParkingIncluded = false, 
            SmokingAllowed = false,
            LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero), 
            Rating = 5, 
            Location = GeographyPoint.Create(47.678581, -122.131577)
        },
        new Hotel()
        { 
            HotelId = "2", 
            BaseRate = 79.99,
            Description = "Cheapest hotel in town",
            DescriptionFr = "Hôtel le moins cher en ville",
            HotelName = "Roach Motel",
            Category = "Budget",
            Tags = new[] { "motel", "budget" },
            ParkingIncluded = true,
            SmokingAllowed = true,
            LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
            Rating = 1,
            Location = GeographyPoint.Create(49.678581, -122.131577)
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
        // hello batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log hello failed document keys and continue.
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents toobe indexed...\n");
    Thread.Sleep(2000);
}
```

Deze methode heeft vier onderdelen. Hallo maakt eerst een matrix van `Hotel` objecten die als onze invoergegevens tooupload toohello index fungeert. Deze gegevens zijn vastgelegd voor eenvoud. In uw eigen toepassing, wordt uw gegevens waarschijnlijk afkomstig zijn van een externe gegevensbron, zoals een SQL-database.

het tweede gedeelte Hallo maakt een `IndexBatch` met Hallo documenten. Geef van gewenste tooapply toohello batch tijdens Hallo, in dit geval door het aanroepen maken van Hallo-bewerking `IndexBatch.Upload`. Hallo batch is vervolgens geüploade toohello Azure Search indexeren met Hallo `Documents.Index` methode.

> [!NOTE]
> In dit voorbeeld zijn er alleen documenten te uploaden. Indien u toomerge wijzigingen in bestaande documenten of verwijderen wenste, kunt u batches maken door het aanroepen van `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, of `IndexBatch.Delete` in plaats daarvan. Ook kunt u verschillende bewerkingen in één batch elkaar door aan te roepen `IndexBatch.New`, wat een verzameling van duurt `IndexAction` objecten, die elk een bepaalde bewerking voor een document wordt Azure Search tooperform uitgelegd. U kunt elk maken `IndexAction` met een eigen bewerking door het aanroepen van de bijbehorende methode Hallo zoals `IndexAction.Merge`, `IndexAction.Upload`, enzovoort.
> 
> 

Hallo derde deel van deze methode is een blok catch die verantwoordelijk is voor een belangrijke foutaanvraag voor indexering. Als uw Azure Search-service geen tooindex aantal Hallo documenten in batch Hallo, een `IndexBatchException` verstuurd door `Documents.Index`. Dit kan gebeuren als u documenten indexeert terwijl uw service zwaar wordt belast. **Wij raden u aan deze aanvraag expliciet in uw code te behandelen.** U kunt vertraging en probeer het vervolgens opnieuw indexeren Hallo-documenten die niet of u kunt zich aanmelden en doorgaan zoals Hallo voorbeeld, of kunt u iets anders, afhankelijk van de gegevensvereisten consistentie van uw toepassing.

> [!NOTE]
> U kunt Hallo `FindFailedActionsToRetry` methode tooconstruct een nieuwe batch met Hallo alleen acties die niet in een eerdere aanroep te`Index`. Hallo-methode wordt beschreven [hier](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) en er is een beschrijving van hoe tooproperly gebruiken [op StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).
>
>

Ten slotte Hallo `UploadDocuments` methode twee seconden vertraagd. Het indexeren verloopt asynchroon op in uw Azure Search-service, zodat het Hallo-voorbeeldtoepassing moet toowait een korte tijd tooensure dat Hallo documenten beschikbaar voor zoeken zijn. Dergelijke vertragingen zijn doorgaans alleen nodig is demo’s, testen en voorbeeldtoepassingen.

#### <a name="how-hello-net-sdk-handles-documents"></a>Hoe documenten worden verwerkt door Hallo .NET SDK
U vraagt zich misschien af hoe hello Azure Search .NET SDK is kunnen tooupload exemplaren van een gebruiker gedefinieerde klasse zoals `Hotel` toohello index. toohelp deze vraag te beantwoorden, bekijken we Hallo `Hotel` klasse:

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

Hallo eerst te beginnen toonotice is dat elke openbare eigenschap van `Hotel` overeenkomt met tooa veld in de indexdefinitie hello, maar met een cruciaal verschil: Hallo-naam van elk veld begint met een kleine letter ("kamelen"), terwijl Hallo-naam van elke bevolking de eigenschap van `Hotel` begint met een hoofdletter ("Pascal geval'). Dit is een veelvoorkomend scenario in .NET-toepassingen die gegevens koppelen waarbij Hallo doelschema buiten Hallo beheer van de ontwikkelaar van de toepassing hello is. In plaats van tooviolate Hallo .NET-naamgevingsregels door het maken van de eigenschap namen kamelen, kunt u zien Hallo SDK toomap Hallo eigenschap namen toocamel case automatisch met Hallo `[SerializePropertyNamesAsCamelCase]` kenmerk.

> [!NOTE]
> Hello Azure Search .NET SDK maakt gebruik van Hallo [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) bibliotheek tooserialize en deserialiseren van uw aangepaste model objecten tooand van JSON. U kunt deze serialisatie indien nodig aanpassen. Zie voor meer informatie [aangepaste serialisatie met JSON.NET](#JsonDotNet).
> 
> 

Hallo tweede ding toonotice zijn Hallo kenmerken zoals `IsFilterable`, `IsSearchable`, `Key`, en `Analyzer` dat elke openbare eigenschap opmaken. Deze kenmerken toewijzen rechtstreeks toohello [overeenkomende kenmerken van hello Azure Search-index](https://docs.microsoft.com/rest/api/searchservice/create-index#request). Hallo `FieldBuilder` klasse gebruikt deze tooconstruct velddefinities voor Hallo-index.

Hallo derde wat ook belangrijk is Hallo `Hotel` klasse, zijn de gegevenstypen Hallo van Hallo openbare eigenschappen. Hallo .NET-typen van deze eigenschappen worden toegewezen tootheir gelijkwaardige veldtypen in Hallo indexdefinitie. Bijvoorbeeld, Hallo `Category` tekenreekseigenschap toegewezen toohello `category` veld van het type `Edm.String`. Er zijn vergelijkbare type toewijzingen tussen `bool?` en `Edm.Boolean`, `DateTimeOffset?` en `Edm.DateTimeOffset`, enz. Hallo specifieke regels voor de toewijzing van Hallo type zijn gedocumenteerd in Hallo `Documents.Get` methode in Hallo [Azure Search .NET SDK verwijzing](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_). Hallo `FieldBuilder` klasse zorgt voor deze toewijzing is voor u, maar kan nog steeds handig toounderstand geval u eventuele problemen met de serialisatie tootroubleshoot nodig.

Deze mogelijkheid toouse uw eigen klassen als documenten werkt beide kanten; U kunt ook zoekresultaten ophalen en Hallo SDK automatisch deserialiseert tooa type van uw keuze, zoals we in de volgende sectie Hallo ziet.

> [!NOTE]
> Hello Azure Search .NET SDK biedt ook ondersteuning voor dynamisch getypeerde documenten met behulp van Hallo `Document` klasse, die een sleutel/waarde-aan veldwaarden namen toofield toewijst. Dit is nuttig in scenario's, indien u niet weet Hallo Indexeer schema op het moment van ontwerp of dat het onhandig toobind toospecific modelklassen normaal zou zijn. Alle Hallo methoden in Hallo SDK die met documenten werken hebben overloads die met Hallo werken `Document` klasse, evenals sterk getypeerde overloads die een generiek typeparameter moeten uitvoeren. Alleen laatste hello worden gebruikt in de voorbeeldcode Hallo in deze zelfstudie. Hallo `Document` klasse neemt over van `Dictionary<string, object>`. U vindt andere details [hier](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).
> 
> 

**Waarom u nullable-gegevenstypen moet gebruiken**

Bij het ontwerpen van uw eigen model klassen toomap tooan Azure Search-index we raden u aan om eigenschappen van waardentypen zoals `bool` en `int` toobe null-waarden bevatten (bijvoorbeeld `bool?` in plaats van `bool`). Als u een niet-nullbare eigenschap gebruikt, hebt u te**garanderen** dat de documenten in uw index geen null-waarde voor het betreffende veld Hallo bevatten. Hallo SDK noch hello Azure Search-service kunt u tooenforce dit.

Dit is niet alleen een hypothetische probleem: Stel een scenario waarin het toevoegen van een nieuw veld tooan bestaande index van het type `Edm.Int32`. Na het bijwerken van de indexdefinitie hello, moeten alle documenten een null-waarde voor het nieuwe veld (omdat alle typen null in Azure Search). Als u vervolgens een modelklasse met een niet-nullbare `int` eigenschap voor dat veld gebruikt, ontvangt u een `JsonSerializationException` zoals deze bij het tooretrieve documenten:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Daarom wordt u aangeraden nullbare typen in uw modelklassen te gebruiken.

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a>Aangepaste met JSON.NET-serialisatie
Hallo SDK maakt gebruik van JSON.NET voor het serialiseren en deserialiseren van documenten. U kunt aanpassen serialisatie en deserialisatie indien nodig door het definiëren van uw eigen `JsonConverter` of `IContractResolver` (Zie Hallo [JSON.NET documentatie](http://www.newtonsoft.com/json/help/html/Introduction.htm) voor meer informatie). Dit kan nuttig zijn wanneer u een bestaande modelklasse tooadapt van uw toepassing voor gebruik met Azure Search en andere meer geavanceerde scenario's wilt. Met aangepaste serialisatie kunt u bijvoorbeeld:

* Opnemen of uitsluiten van bepaalde eigenschappen van uw modelklasse als documentvelden worden opgeslagen.
* Koppeling tussen de namen van eigenschappen in uw code en veldnamen in uw index.
* Aangepaste kenmerken die kunnen worden gebruikt voor de toewijzing van eigenschappen toodocument velden maken.

Hier vindt u voorbeelden van de implementatie van aangepaste serialisatie in Hallo-controles voor hello Azure Search .NET SDK op GitHub. Is een goed uitgangspunt [deze map](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models). Deze bevat klassen die worden gebruikt door Hallo aangepaste serialisatie-tests.

### <a name="searching-for-documents-in-hello-index"></a>Zoeken naar documenten in Hallo index
laatste stap in de voorbeeldtoepassing Hallo Hallo is toosearch voor een aantal documenten in Hallo index. Hallo methode volgende gebeurt:

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

Telkens wanneer een query wordt uitgevoerd, wordt deze methode maakt eerst een nieuwe `SearchParameters` object. Dit is de gebruikte toospecify aanvullende opties voor Hallo query zoals sorteren en filteren van, paginering facetten. Bij deze methode instelt we Hallo `Filter`, `Select`, `OrderBy`, en `Top` eigenschap voor verschillende query's. Alle Hallo `SearchParameters` eigenschappen zijn gedocumenteerd [hier](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).

de volgende stap Hallo is tooactually Hallo zoekopdracht uitvoeren. Dit wordt gedaan met behulp van Hallo `Documents.Search` methode. Voor elke query, geven we Hallo zoeken tekst toouse als tekenreeks (of `"*"` als er geen zoektekst), plus Hallo zoeken parameters eerder hebt gemaakt. We ook opgeven `Hotel` als Hallo typeparameter voor `Documents.Search`, waarin u Hallo SDK toodeserialize documenten in de zoekresultaten Hallo bepaald in objecten van het type `Hotel`.

> [!NOTE]
> U vindt meer informatie over de syntaxis Hallo zoekquery expressie [hier](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).
> 
> 

Ten slotte na elke query doorlopen met deze methode alle Hallo treffers in zoekresultaten Hallo elke document toohello console afdrukken:

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

U gaat nu een nader bekeken Hallo query's op zijn beurt. Hier volgt Hallo code tooexecute Hallo eerste query:

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

In dit geval we zoeken hotels die overeenkomen met de Hallo woord 'budget' en we willen tooget terug alleen Hallo hotel namen, zoals opgegeven door Hallo `Select` parameter. Hier volgen Hallo resultaten:

    Name: Roach Motel

Vervolgens we wilt toofind Hallo hotels met een elke nacht tarief van minder dan €150 en alleen Hallo hotel-ID en een beschrijving geretourneerd:

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

Deze query gebruikt een OData `$filter` expressie, `baseRate lt 150`, toofilter Hallo documenten in Hallo index. U vindt meer informatie over Hallo OData-syntaxis die ondersteuning biedt voor Azure Search [hier](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).

Hier volgen Hallo resultaten van Hallo-query:

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

We willen vervolgens toofind Hallo bovenste twee hotels die onlangs zijn renovated en Hallo hotel naam en de datum van laatste renovatie niet weergeven. Dit is Hallo code: 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

In dit geval opnieuw gebruiken we OData syntaxis toospecify hello `OrderBy` parameter als `lastRenovationDate desc`. We ook ingesteld `Top` too2 tooensure alleen krijgen we Hallo twee bovenste documenten. Net als voorheen kunt we ingesteld `Select` toospecify welke velden moeten worden geretourneerd.

Hier volgen Hallo resultaten:

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Tot slot willen we toofind alle hotels die overeenkomen met Hallo woord 'motel':

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

En hier vindt u Hallo resultaten, die alle velden bevatten omdat er geen Hallo opgegeven is `Select` eigenschap:

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

Deze stap Hallo zelfstudie is voltooid, maar hier niet stoppen. **Volgende stappen** bevat aanvullende bronnen voor meer informatie over Azure Search.

## <a name="next-steps"></a>Volgende stappen
* Hallo-verwijzingen voor Hallo Bladeren [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) en [REST-API](https://docs.microsoft.com/rest/api/searchservice/).
* Uw medeweten via verdiepen [video's en andere voorbeelden en zelfstudies](search-video-demo-tutorial-list.md).
* Bekijk [naamconventies](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn Hallo regels voor het benoemen van verschillende objecten.
* Bekijk [ondersteunde gegevenstypen](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.
