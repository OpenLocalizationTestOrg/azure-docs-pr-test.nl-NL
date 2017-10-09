---
title: aaa "query uitvoeren in een index (.NET API - Azure Search) | Microsoft Docs'
description: Een zoekopdracht in Azure search samenstellen en gebruiken van parameters toofilter en sorteren search zoekresultaten.
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a>Query uitvoeren op uw Azure Search-index met behulp van Hallo .NET SDK
> [!div class="op_single_selector"]
> * [Overzicht](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

In dit artikel leert u hoe uw index met behulp tooquery Hallo [Azure Search .NET SDK](https://aka.ms/search-sdk).

Voordat u deze procedure begint, moet u al [een Azure Search-index hebben gemaakt](search-what-is-an-index.md) en moet deze index [gevuld zijn met gegevens](search-what-is-data-import.md).

> [!NOTE]
> Alle voorbeeldcode in dit artikel is geschreven in C#. U vindt de volledige broncode Hallo [op GitHub](http://aka.ms/search-dotnet-howto). U kunt ook lezen over Hallo [Azure Search .NET SDK](search-howto-dotnet-sdk.md) voor een meer gedetailleerde doorloop van Hallo voorbeeldcode.

## <a name="identify-your-azure-search-services-query-api-key"></a>De query api-sleutel voor de Azure Search-service vaststellen
Nu u een Azure Search-index hebt gemaakt, bent u bijna klaar tooissue query's op basis van Hallo .NET SDK. Eerst moet u tooobtain een Hallo query api-sleutels die is gegenereerd voor Hallo zoekservice die u hebt ingericht. Hallo .NET SDK verzendt deze api-sleutel voor elke aanvraag tooyour-service. Met een geldige sleutel stelt vertrouwensrelatie op basis van per aanvraag, tussen Hallo verzenden Hallo toepassingsaanvraag en Hallo-service die afhandelt.

1. toofind api-sleutels met uw service u zich in toohello aanmelden kunt [Azure-portal](https://portal.azure.com/)
2. Blade Ga tooyour Azure Search service
3. Klik op Hallo 'Sleutels'-pictogram

Uw service heeft zowel *administratorsleutels* als *querysleutels*.

* De primaire en secundaire *administratorsleutels* verlenen volledige rechten tooall bewerkingen, inclusief Hallo mogelijkheid toomanage Hallo-service, maken en verwijderen van indexen, Indexeerfuncties en gegevensbronnen. Er zijn twee sleutels, zodat u verder kunt toouse Hallo secundaire sleutel als u tooregenerate Hallo primaire sleutel en vice versa besluit.
* Uw *querysleutels* verlenen tooindexes alleen-lezen toegang en -documenten en zijn doorgaans gedistribueerde tooclient toepassingen die zoekaanvragen.

Voor de toepassing hello van query's op een index, kunt u een van de query-sleutel. De administratorsleutels kunnen ook worden gebruikt voor query's, maar moet u een querysleutel in uw toepassingscode als dit beter Hallo volgt [principe van minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Maak een instantie van klasse SearchIndexClient Hallo
query's tooissue Hello Azure Search .NET SDK, moet u een exemplaar van Hallo toocreate `SearchIndexClient` klasse. Deze klasse heeft verschillende constructors. Hallo gewenste neemt uw naam zoekservice, de naam van de index en een `SearchCredentials` object als parameters. `SearchCredentials` verpakt uw api-sleutel.

Hallo-code hieronder maakt u een nieuwe `SearchIndexClient` voor de index "hotels" hello (gemaakt in [een Azure Search index maken met .NET SDK Hallo](search-create-index-dotnet.md)) met waarden voor Hallo zoeken servicenaam en api-sleutel die zijn opgeslagen in de configuratie van de toepassing hello bestand (`appsettings.json` in geval van Hallo Hallo [voorbeeldtoepassing](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

`SearchIndexClient` heeft een `Documents`-eigenschap. Deze eigenschap bevat dat alle methoden die u nodig hebt tooquery Azure Search-index Hallo.

## <a name="query-your-index"></a>Een query uitvoeren in uw index
Zoeken met Hallo .NET SDK is net zo eenvoudig als aanroepen Hallo `Documents.Search` methode op uw `SearchIndexClient`. Deze methode heeft een aantal parameters, waaronder de zoektekst hello, samen met een `SearchParameters` -object dat gebruikt toofurther verfijnen Hallo query worden kan.

#### <a name="types-of-queries"></a>Typen query 's
Hallo twee main [querytypen](search-query-overview.md#types-of-queries) gewenste zijn `search` en `filter`. Een `search`-query zoekt naar een of meer voorwaarden in alle *doorzoekbare* velden in de index. Een `filter`-query evalueert een Booleaanse expressie op alle *filterbare* velden in een index.

Zowel zoekopdrachten en filters worden uitgevoerd met behulp van Hallo `Documents.Search` methode. Een zoekopdracht kan worden doorgegeven aan Hallo `searchText` parameter, terwijl een filterexpressie kan worden doorgegeven aan Hallo `Filter` eigenschap Hallo `SearchParameters` klasse. toofilter zonder te zoeken, geeft `"*"` voor Hallo `searchText` parameter. toosearch zonder te filteren, stelt u Hallo `Filter` eigenschap niet in of niet doorgegeven een `SearchParameters` instantie.

#### <a name="example-queries"></a>Voorbeelden van query 's
Hallo volgende voorbeeldcode ziet u een aantal verschillende manieren tooquery Hallo "hotels" index die is gedefinieerd in [een Azure Search index maken met .NET SDK Hallo](search-create-index-dotnet.md#DefineIndex). Hallo documenten die worden geretourneerd met Hallo zoekresultaten zijn instanties van Hallo `Hotel` klasse, die is gedefinieerd in [gegevens importeren in met behulp van Azure Search .NET SDK Hallo](search-import-data-dotnet.md#HotelClass). Hallo voorbeeldcode maakt gebruik van een `WriteDocuments` methode toooutput Hallo zoeken resultaten toohello console. Deze methode wordt beschreven in de volgende sectie Hallo.

```csharp
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
```

## <a name="handle-search-results"></a>Zoekresultaten verwerken
Hallo `Documents.Search` methode retourneert een `DocumentSearchResult` -object dat Hallo resultaten van Hallo query bevat. Hallo-voorbeeld in de vorige sectie Hallo gebruikgemaakt van een methode aangeroepen `WriteDocuments` toooutput Hallo search-resultaten toohello console:

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

Hier ziet u wat Hallo resultaten eruitzien zoals voor Hallo query's in de vorige sectie hello, uitgaande Hallo "hotels" index is gevuld met de voorbeeldgegevens Hallo in [gegevens importeren in met behulp van Azure Search .NET SDK Hallo](search-import-data-dotnet.md):

```
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
```

bovenstaande Hallo voorbeeldcode maakt gebruik van Hallo console toooutput zoekresultaten. U moet ook zoekresultaten toodisplay in uw eigen toepassing. Zie [dit voorbeeld op GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) voor een voorbeeld van hoe toorender in een ASP.NET MVC-gebaseerde webtoepassing zoekresultaten.

