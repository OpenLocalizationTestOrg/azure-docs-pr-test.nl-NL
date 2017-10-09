---
title: aaa "maken van een index (.NET API - Azure Search) | Microsoft Docs'
description: Een index in code met Azure Search .NET SDK Hallo maken.
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7fa4030b8c3565bc02b1d6bb4426331657cf3a5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-net-sdk"></a>Een Azure Search index maken met Hallo .NET SDK
> [!div class="op_single_selector"]
> * [Overzicht](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

In dit artikel begeleidt u stapsgewijs door het Hallo-proces voor het maken van een Azure Search [index](https://docs.microsoft.com/rest/api/searchservice/Create-Index) met Hallo [Azure Search .NET SDK](https://aka.ms/search-sdk).

Voordat u de stappen in dit artikel uitvoert en een index maakt, moet u eerst [een Azure Search-service](search-create-service-portal.md) hebben gemaakt.

> [!NOTE]
> Alle voorbeeldcode in dit artikel is geschreven in C#. U vindt de volledige broncode Hallo [op GitHub](http://aka.ms/search-dotnet-howto). U kunt ook lezen over Hallo [Azure Search .NET SDK](search-howto-dotnet-sdk.md) voor een meer gedetailleerde doorloop van Hallo voorbeeldcode.


## <a name="identify-your-azure-search-services-admin-api-key"></a>De admin api-sleutel voor de Azure Search-service vaststellen
Nu u een Azure Search-service hebt ingericht, bent u bijna klaar tooissue aanvragen voor uw service-eindpunt met behulp van Hallo .NET SDK. Eerst moet u tooobtain een Hallo admin api-sleutels die is gegenereerd voor Hallo zoekservice die u hebt ingericht. Hallo .NET SDK verzendt deze api-sleutel voor elke aanvraag tooyour-service. Met een geldige sleutel stelt vertrouwensrelatie op basis van per aanvraag, tussen Hallo verzenden Hallo toepassingsaanvraag en Hallo-service die afhandelt.

1. toofind van uw service api-sleutels, meld u aan toohello [Azure-portal](https://portal.azure.com/)
2. Blade Ga tooyour Azure Search service
3. Klik op Hallo 'Sleutels'-pictogram

Uw service heeft zowel *administratorsleutels* als *querysleutels*.

* De primaire en secundaire *administratorsleutels* verlenen volledige rechten tooall bewerkingen, inclusief Hallo mogelijkheid toomanage Hallo-service, maken en verwijderen van indexen, Indexeerfuncties en gegevensbronnen. Er zijn twee sleutels, zodat u verder kunt toouse Hallo secundaire sleutel als u tooregenerate Hallo primaire sleutel en vice versa besluit.
* Uw *querysleutels* verlenen tooindexes alleen-lezen toegang en -documenten en zijn doorgaans gedistribueerde tooclient toepassingen die zoekaanvragen.

Voor Hallo-toepassing van een index te maken, kunt u ofwel de primaire of secundaire administratorsleutel.

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-hello-searchserviceclient-class"></a>Maak een instantie van klasse SearchServiceClient Hallo
met behulp van toostart hello Azure Search .NET SDK, moet u een exemplaar van Hallo toocreate `SearchServiceClient` klasse. Deze klasse heeft verschillende constructors. Hallo gewenste neemt de naam van uw zoekservice en een `SearchCredentials` object als parameters. `SearchCredentials` verpakt uw api-sleutel.

Hallo-code hieronder maakt u een nieuwe `SearchServiceClient` met waarden voor Hallo zoeken servicenaam en api-sleutel die zijn opgeslagen in het configuratiebestand van de toepassing hello (`appsettings.json` in geval van Hallo Hallo [voorbeeldtoepassing](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

`SearchServiceClient` heeft een `Indexes`-eigenschap. Deze eigenschap bevat alle methoden Hallo toocreate, lijst, update, of u Azure Search-index te verwijderen.

> [!NOTE]
> Hallo `SearchServiceClient` klasse beheert verbindingen tooyour search-service. In de volgorde tooavoid te veel verbindingen te openen, moet u tooshare één exemplaar van proberen `SearchServiceClient` in uw toepassing indien mogelijk. De bijbehorende methoden zijn thread-veilige tooenable delen.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a>Uw Azure Search-index definiëren
Een toohello één aanroep `Indexes.Create` methode de index wilt maken. Deze methode gebruikt een `Index`-object als parameter voor uw Azure Search-index. U moet toocreate een `Index` object en dit als volgt initialiseren:

1. Set Hallo `Name` eigenschap Hallo `Index` object toohello naam van de index.
2. Set Hallo `Fields` eigenschap Hallo `Index` tooan objectmatrix van `Field` objecten. Hallo gemakkelijkste manier toocreate hello `Field` objecten is door de aanroepende Hallo `FieldBuilder.BuildForType` methode, waarbij een modelklasse voor typeparameter Hallo doorgegeven. Een modelklasse heeft de eigenschappen die zijn toegewezen toohello velden van uw index. Hiermee kunt u toobind documenten vanuit uw search-index tooinstances van uw modelklasse.

> [!NOTE]
> Als u niet van plan een modelklasse toouse bent, kunt u uw index nog steeds definiëren door het maken van `Field` objecten rechtstreeks. Hallo-naam van Hallo veld toohello constructor, samen met het Hallo-gegevenstype (of analyse voor tekenreeksvelden), kunt u opgeven. U kunt ook andere eigenschappen instellen, zoals `IsSearchable`, `IsFilterable`, enzovoort.
>
>

Het is belangrijk dat u uw zoekopdracht gebruiker ervaring en zakelijke behoeften rekening houden bij het ontwerpen van uw index als elk veld Hallo moet worden toegewezen [relevante eigenschappen](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Deze eigenschappen bepalen welke zoekfuncties (filteren, facetten, zoekacties volledige tekst sorteren enzovoort) toepassing toowhich velden. Voor elke eigenschap die u niet expliciet instelt, Hallo `Field` klasse toodisabling Hallo bijbehorende zoekfunctie standaardwaarden tenzij expliciet inschakelt.

In ons voorbeeld is de index 'hotels' genoemd en zijn de velden gedefinieerd met een modelklasse. Elke eigenschap van Hallo modelklasse heeft kenmerken Hallo zoekproblemen gedrag van de bijbehorende indexveld Hallo vast te stellen. Hallo modelklasse wordt als volgt gedefinieerd:

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

We hebt zorgvuldig Hallo kenmerken voor elke eigenschap die op basis van onze verwachting dat ze worden gebruikt in een toepassing gekozen. Bijvoorbeeld, is het waarschijnlijk dat mensen die zoeken naar hotels geïnteresseerd zijn in overeenkomende sleutelwoorden in Hallo `description` veld, zodat we een zoekopdracht in volledige tekst voor dat veld inschakelen door toe te voegen Hallo `IsSearchable` toohello kenmerk `Description` eigenschap.

Houd er rekening mee dat precies één veld in de index van het type `string` moet worden Hallo aangemerkt als Hallo *sleutel* veld door toe te voegen Hallo `Key` kenmerk (Zie `HotelId` in Hallo bovenstaande voorbeeld).

bovenstaande Hallo indexdefinitie maakt gebruik van een taalanalyse voor Hallo `description_fr` veld omdat het beoogde toostore Franse tekst. Zie [onderwerp Hallo Language support](https://docs.microsoft.com/rest/api/searchservice/Language-support) en de bijbehorende Hallo [blogbericht](https://azure.microsoft.com/blog/language-support-in-azure-search/) voor meer informatie over taalanalyse.

> [!NOTE]
> Hallo-naam van elke eigenschap in uw modelklasse wordt standaard gebruikt als Hallo-naam van de corresponderende veld Hallo in Hallo index. Als u alle eigenschap namen toocamel case veldnamen toomap wilt, markeer Hallo klasse Hello `SerializePropertyNamesAsCamelCase` kenmerk. Als u toomap tooa andere naam wilt, kunt u Hallo `JsonProperty` kenmerk zoals Hallo `DescriptionFr` eigenschap hierboven. Hallo `JsonProperty` kenmerk heeft voorrang op Hallo `SerializePropertyNamesAsCamelCase` kenmerk.
> 
> 

Nu u een modelklasse hebt gedefinieerd, kunt u heel eenvoudig een indexdefinitie maken:

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-hello-index"></a>Hallo-index maken
Nu dat u een geïnitialiseerd hebt `Index` object, kunt u Hallo index maken door gewoon aan te roepen `Indexes.Create` op uw `SearchServiceClient` object:

```csharp
serviceClient.Indexes.Create(definition);
```

Voor een aanvraag is gelukt, wordt normaal gesproken Hallo-methode retourneren. Als er een probleem met de aanvraag Hallo zoals een ongeldige parameter, genereert de methode Hallo `CloudException`.

Wanneer u met een toodelete index en wilt dit bent klaar, roept u Hallo `Indexes.Delete` methode op uw `SearchServiceClient`. Dit is bijvoorbeeld hoe we de index "hotels" hello wilt verwijderen:

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> Hallo voorbeeldcode in dit artikel gebruikt synchrone methoden Hallo Hallo Azure Search .NET SDK voor eenvoud. Aangeraden Hallo asynchrone methoden te gebruiken in uw eigen toepassingen tookeep ze schaalbaar en responsief. Bijvoorbeeld voorbeelden boven kunnen gebruiken in Hallo `CreateAsync` en `DeleteAsync` in plaats van `Create` en `Delete`.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Nadat een Azure Search-index is gemaakt, kunt u zich gereed te[uw inhoud uploaden naar de index Hallo](search-what-is-data-import.md) zodat u kunt beginnen met het zoeken van gegevens.

