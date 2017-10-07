---
title: aaa "uploaden van gegevens (.NET - Azure Search) | Microsoft Docs'
description: Meer informatie over hoe tooupload gegevens tooan index in met behulp van Azure Search .NET SDK Hallo.
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a>Het uploaden van gegevens tooAzure zoeken met Hallo .NET SDK
> [!div class="op_single_selector"]
> * [Overzicht](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

In dit artikel wordt uitgelegd hoe u toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport gegevens in een Azure Search-index.

Voordat u deze procedure begint, moet u al [een Azure Search-index hebben gemaakt](search-what-is-an-index.md). In dit artikel wordt ervan uitgegaan dat u al hebt gemaakt een `SearchServiceClient` object, zoals aangegeven [een Azure Search index maken met .NET SDK Hallo](search-create-index-dotnet.md#CreateSearchServiceClient).

> [!NOTE]
> Alle voorbeeldcode in dit artikel is geschreven in C#. U vindt de volledige broncode Hallo [op GitHub](http://aka.ms/search-dotnet-howto). U kunt ook lezen over Hallo [Azure Search .NET SDK](search-howto-dotnet-sdk.md) voor een meer gedetailleerde doorloop van Hallo voorbeeldcode.

In de volgorde toopush documenten in uw index met behulp van Hallo .NET SDK, moet u naar:

1. Maak een `SearchIndexClient` object tooconnect tooyour search-index.
2. Maak een `IndexBatch` met Hallo documenten toobe toegevoegd, gewijzigd of verwijderd.
3. Hallo aanroepen `Documents.Index` methode van uw `SearchIndexClient` toosend hello `IndexBatch` tooyour search-index.

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Maak een instantie van klasse SearchIndexClient Hallo
tooimport gegevens in uw index met hello Azure Search .NET SDK, moet u een exemplaar van Hallo toocreate `SearchIndexClient` klasse. U kunt deze instantie zelf samenstellen, maar de eenvoudiger als u al een `SearchServiceClient` exemplaar toocall de `Indexes.GetClient` methode. Hier is bijvoorbeeld hoe u zou krijgen een `SearchIndexClient` voor Hallo index "hotels" met de naam van een `SearchServiceClient` met de naam `serviceClient`:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> In een standaardzoektoepassing wordt het beheer van de index en de invulling daarvan afgehandeld door een afzonderlijk onderdeel van de zoekquery’s. `Indexes.GetClient`is handig voor het invullen van een index, omdat u problemen van het bieden van een andere Hallo `SearchCredentials`. Dit wordt uitgevoerd door Hallo beheersleutel doorgeeft die gebruikte toocreate u Hallo `SearchServiceClient` toohello nieuwe `SearchIndexClient`. Hallo deel van uw toepassing waarmee query's uitvoert, het is echter beter toocreate hello `SearchIndexClient` rechtstreeks zodat u in een querysleutel in plaats van een administratorsleutel doorgeven kunt. Dit komt overeen met de Hallo [principe van minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege) en helpt uw toepassing veiliger toomake. U vindt meer informatie over administratorsleutels en querysleutels in Hallo [Azure Search REST API-verwijzing](https://docs.microsoft.com/rest/api/searchservice/).
> 
> 

`SearchIndexClient` heeft een `Documents`-eigenschap. Deze eigenschap bevat alle Hallo-methoden, moet u tooadd, wijzigen, verwijderen of documenten in uw index opvragen.

## <a name="decide-which-indexing-action-toouse"></a>Bepaal welke indexering actie toouse
tooimport gegevens met behulp van Hallo .NET SDK, moet u toopackage van uw gegevens in een `IndexBatch` object. Een `IndexBatch` omvat een verzameling van `IndexAction` objecten, die elk een document en een eigenschap die Azure Search welke actie tooperform op het document (uploaden, samenvoegen, verwijderen, enzovoort). Afhankelijk van welke van Hallo onderstaande bewerkingen die u kiest, moet alleen bepaalde velden voor elk document opnemen:

| Actie | Beschrijving | Vereiste velden voor elk document | Opmerkingen |
| --- | --- | --- | --- |
| `Upload` |Een `Upload` actie is vergelijkbaar tooan "upsert", waarbij Hallo document wordt ingevoegd als het nieuwe en bijgewerkt/vervangen als deze bestaat. |sleutel, plus andere velden die u wenst dat toodefine |Wanneer het bijwerken/vervangen van een bestaand document wordt elk veld dat niet is opgegeven in de aanvraag Hallo hebt ingesteld te`null`. Dit gebeurt zelfs als Hallo veld eerder tooa null-waarde is ingesteld. |
| `Merge` |Een bestaand document met het Hallo updates opgegeven velden. Als Hallo document niet in de index hello bestaat, mislukt de Hallo samenvoegen. |sleutel, plus andere velden die u wenst dat toodefine |Elk veld dat u in een samenvoeging opgeeft wordt vervangen door Hallo bestaand veld in Hallo-document. ook velden van het type `DataType.Collection(DataType.String)`. Bijvoorbeeld, als hello document bevat een veld `tags` met waarde `["budget"]` en u een samenvoeging met de waarde `["economy", "pool"]` voor `tags`, uiteindelijke waarde van Hallo Hallo `tags` veld `["economy", "pool"]`. Het wordt dus niet `["budget", "economy", "pool"]`. |
| `MergeOrUpload` |Deze bewerking gedraagt zich als `Merge` wanneer een document met de opgegeven sleutel al Hallo in Hallo index bestaat. Als het Hallo-document niet bestaat, gedraagt zich als `Upload` met een nieuw document. |sleutel, plus andere velden die u wenst dat toodefine |- |
| `Delete` |Verwijdert het opgegeven document Hallo van Hallo index. |alleen sleutel |Alle velden die u opgeeft dan Hallo sleutelveld worden genegeerd. Als u wilt dat tooremove een afzonderlijk veld uit een document, gebruikt u `Merge` en stelt u Hallo veld expliciet toonull. |

U kunt opgeven welke actie wilt u toouse met verschillende statische methoden van Hallo Hallo `IndexBatch` en `IndexAction` klassen, zoals wordt weergegeven in de volgende sectie Hallo.

## <a name="construct-your-indexbatch"></a>Uw IndexBatch maken
Nu u weet welke tooperform acties op uw documenten, bent u klaar tooconstruct hello `IndexBatch`. voorbeeld hieronder toont hoe Hallo toocreate een batch met verschillende bewerkingen. Dit voorbeeld wordt een aangepaste klasse aangeroepen Opmerking `Hotel` die tooa document in de index "hotels" hello wordt toegewezen.

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
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
            }),
        IndexAction.Upload(
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
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

In dit geval gebruiken we `Upload`, `MergeOrUpload`, en `Delete` als onze zoekacties, zoals opgegeven door Hallo methoden aangeroepen op Hallo `IndexAction` klasse.

We gaan ervan uit dat deze voorbeeldindex "hotels" al is gevuld met een aantal documenten. Hoe we hoefden niet toospecify alle mogelijke documentvelden Hallo bij gebruik van `MergeOrUpload` en hoe we alleen opgegeven Hallo documentsleutel (`HotelId`) bij gebruik van `Delete`.

Merk ook op die u kunt alleen too1000 documenten in een enkele indexeringsaanvraag opnemen.

> [!NOTE]
> In dit voorbeeld passen we verschillende bewerkingen toodifferent documenten. Als u deze wilde tooperform dezelfde bewerkingen op alle documenten in Hallo batch, in plaats van aanroepen Hallo `IndexBatch.New`, kunt u andere statische methode van Hallo `IndexBatch`. U kunt bijvoorbeeld batches maken door `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, of `IndexBatch.Delete` aan te roepen. Deze methoden maken gebruik van een verzameling van documenten (objecten van het type `Hotel` in dit voorbeeld) in plaats van `IndexAction`-objecten.
> 
> 

## <a name="import-data-toohello-index"></a>Index van toohello importeren
Nu dat u een geïnitialiseerd hebt `IndexBatch` object, kunt u deze verzenden toohello index door aan te roepen `Documents.Index` op uw `SearchIndexClient` object. Hallo volgende voorbeeld wordt getoond hoe toocall `Index`, plus een aantal extra stappen die u moet tooperform:

```csharp
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
```

Opmerking Hallo `try` / `catch` omringende Hallo aanroep toohello `Index` methode. Hallo catch-blok verwerkt een belangrijke foutaanvraag voor indexering. Als uw Azure Search-service geen tooindex aantal Hallo documenten in batch Hallo, een `IndexBatchException` verstuurd door `Documents.Index`. Dit kan gebeuren als u documenten indexeert terwijl uw service zwaar wordt belast. **Wij raden u aan deze aanvraag expliciet in uw code te behandelen.** U kunt vertraging en probeer het vervolgens opnieuw indexeren Hallo-documenten die niet of u kunt zich aanmelden en doorgaan zoals Hallo voorbeeld, of kunt u iets anders, afhankelijk van de gegevensvereisten consistentie van uw toepassing.

Ten slotte Hallo code in de vorige twee seconden vertraagd Hallo-voorbeeld. Het indexeren verloopt asynchroon op in uw Azure Search-service, zodat het Hallo-voorbeeldtoepassing moet toowait een korte tijd tooensure dat Hallo documenten beschikbaar voor zoeken zijn. Dergelijke vertragingen zijn doorgaans alleen nodig is demo’s, testen en voorbeeldtoepassingen.

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a>Hoe documenten worden verwerkt door Hallo .NET SDK
U vraagt zich misschien af hoe hello Azure Search .NET SDK is kunnen tooupload exemplaren van een gebruiker gedefinieerde klasse zoals `Hotel` toohello index. toohelp deze vraag te beantwoorden, bekijken we Hallo `Hotel` klasse, die wordt toegewezen toohello indexschema dat is gedefinieerd in [een Azure Search index maken met .NET SDK Hallo](search-create-index-dotnet.md#DefineIndex):

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
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

    // ToString() method omitted for brevity...
}
```

Hallo eerst te beginnen toonotice is dat elke openbare eigenschap van `Hotel` overeenkomt met tooa veld in de indexdefinitie hello, maar met een cruciaal verschil: Hallo-naam van elk veld begint met een kleine letter ("kamelen"), terwijl Hallo-naam van elke bevolking de eigenschap van `Hotel` begint met een hoofdletter ("Pascal geval'). Dit is een veelvoorkomend scenario in .NET-toepassingen die gegevens koppelen waarbij Hallo doelschema buiten Hallo beheer van de ontwikkelaar van de toepassing hello is. In plaats van tooviolate Hallo .NET-naamgevingsregels door het maken van de eigenschap namen kamelen, kunt u zien Hallo SDK toomap Hallo eigenschap namen toocamel case automatisch met Hallo `[SerializePropertyNamesAsCamelCase]` kenmerk.

> [!NOTE]
> Hello Azure Search .NET SDK maakt gebruik van Hallo [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) bibliotheek tooserialize en deserialiseren van uw aangepaste model objecten tooand van JSON. U kunt deze serialisatie indien nodig aanpassen. Meer informatie vindt u in [Aangepaste serialisatie met JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet). Een voorbeeld hiervan is Hallo gebruik Hallo `[JsonProperty]` -kenmerk op Hallo `DescriptionFr` eigenschap in de bovenstaande Hallo voorbeeldcode.
> 
> 

Hallo wat belangrijk is over Hallo `Hotel` klasse, zijn de gegevenstypen Hallo van Hallo openbare eigenschappen. Hallo .NET-typen van deze eigenschappen worden toegewezen tootheir gelijkwaardige veldtypen in Hallo indexdefinitie. Bijvoorbeeld, Hallo `Category` tekenreekseigenschap toegewezen toohello `category` veld van het type `DataType.String`. Er zijn vergelijkbare type toewijzingen tussen `bool?` en `DataType.Boolean`, `DateTimeOffset?` en `DataType.DateTimeOffset`, enzovoort. Hallo specifieke regels voor de toewijzing van Hallo type zijn gedocumenteerd in Hallo `Documents.Get` methode in Hallo [Azure Search .NET SDK verwijzing](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).

Deze mogelijkheid toouse uw eigen klassen als documenten werkt beide kanten; U kunt ook zoekresultaten ophalen en Hallo SDK automatisch deserialiseert tooa type van uw keuze, zoals wordt weergegeven in Hallo [volgende artikel](search-query-dotnet.md).

> [!NOTE]
> Hello Azure Search .NET SDK biedt ook ondersteuning voor dynamisch getypeerde documenten met behulp van Hallo `Document` klasse, die een sleutel/waarde-aan veldwaarden namen toofield toewijst. Dit is nuttig in scenario's, indien u niet weet Hallo Indexeer schema op het moment van ontwerp of dat het onhandig toobind toospecific modelklassen normaal zou zijn. Alle Hallo methoden in Hallo SDK die met documenten werken hebben overloads die met Hallo werken `Document` klasse, evenals sterk getypeerde overloads die een generiek typeparameter moeten uitvoeren. Alleen voor het laatste hello worden gebruikt in Hallo voorbeeldcode in dit artikel.
> 
> 

**Waarom u nullable-gegevenstypen moet gebruiken**

Bij het ontwerpen van uw eigen model klassen toomap tooan Azure Search-index we raden u aan om eigenschappen van waardentypen zoals `bool` en `int` toobe null-waarden bevatten (bijvoorbeeld `bool?` in plaats van `bool`). Als u een niet-nullbare eigenschap gebruikt, hebt u te**garanderen** dat de documenten in uw index geen null-waarde voor het betreffende veld Hallo bevatten. Hallo SDK noch hello Azure Search-service kunt u tooenforce dit.

Dit is niet alleen een hypothetische probleem: Stel een scenario waarin het toevoegen van een nieuw veld tooan bestaande index van het type `DataType.Int32`. Na het bijwerken van de indexdefinitie hello, moeten alle documenten een null-waarde voor het nieuwe veld (omdat alle typen null in Azure Search). Als u vervolgens een modelklasse met een niet-nullbare `int` eigenschap voor dat veld gebruikt, ontvangt u een `JsonSerializationException` zoals deze bij het tooretrieve documenten:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Daarom wordt u aangeraden nullbare typen in uw modelklassen te gebruiken.

## <a name="next-steps"></a>Volgende stappen
Na het vullen van uw Azure Search-index, zult u gereed toostart uitgeven van query's toosearch voor documenten. Zie [Een query uitvoeren in uw Azure-zoekindex](search-query-overview.md) voor meer informatie.

