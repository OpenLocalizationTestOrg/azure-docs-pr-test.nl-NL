---
title: aaaSynonyms preview-zelfstudie in Azure Search | Microsoft Docs
description: Hallo synoniemen preview-functie tooan index toevoegen in Azure Search.
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a>Synoniemenzelfstudie (preview, C#) voor Azure Search

Een query uitbreiden synoniemen door overeenkomende op voorwaarden die worden beschouwd als dezelfde toohello invoer term. U kunt bijvoorbeeld 'auto' toomatch documenten met voorwaarden Hallo 'auto' of 'vehicle'.

In Azure Search worden synoniemen gedefinieerd in een *synoniementoewijzing* op basis van *toewijzingsregels* waarmee equivalente termen worden gekoppeld. Maken van meerdere synoniem maps, plaatst u deze als een index van de beschikbare tooany servicegebeurtenis resource en vervolgens verwijzen naar welke één toouse op Hallo veldniveau. Op het moment dat de query heeft daarnaast toosearching een Azure Search-index een zoekopdracht in een kaart synoniem als er een is opgegeven voor velden die worden gebruikt in query Hallo.

> [!NOTE]
> Hallo-synoniemen functie is momenteel in preview en alleen ondersteund Hallo meest recente preview-API en SDK-versies (api-version = 2016-09-01-Preview, SDK versie 4.x-preview). Azure Portal biedt er momenteel geen ondersteuning voor. Preview-API's vallen niet onder een SLA en de previewfuncties kunnen veranderen. Daarom raden we u af om deze in productietoepassingen te gebruiken.

## <a name="prerequisites"></a>Vereisten

Zelfstudie vereisten zijn Hallo volgende:

* [Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure Search-service](search-create-service-portal.md)
* [Preview-versie van de .NET-bibliotheek Microsoft.Azure.Search](https://aka.ms/search-sdk-preview)
* [Hoe toouse Azure zoeken vanuit een .NET-toepassing](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a>Overzicht

Query's voor en na demonstreren Hallo-waarde van synoniemen. In deze zelfstudie gebruikt u een voorbeeldtoepassing die query's uitvoert en resultaten retourneert in een voorbeeldindex. Hallo-voorbeeldtoepassing maakt een kleine index met de naam "hotels" is gevuld met twee documenten. Hallo-toepassing wordt uitgevoerd zoekopdrachten met voorwaarden en die niet in de index hello voorkomen, Hallo synoniemen functie, activeert vervolgens problemen Hallo dezelfde zoekopdrachten opnieuw. Hallo-code hieronder laat zien Hallo algemene stroom.

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
Hallo stappen toocreate en Hallo voorbeeld index te vullen worden beschreven [hoe toouse Azure zoeken vanuit een .NET-toepassing](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

## <a name="before-queries"></a>'Voor'-query's

In `RunQueriesWithNonExistentTermsInIndex` worden er zoekquery's uitgevoerd met 'vijfsterren', 'internet' en 'voordelig EN hotel'.
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
Geen van de twee geïndexeerde documenten Hallo Hallo-termen bevatten zodat we Hallo volgende eerst de uitvoer van Hallo `RunQueriesWithNonExistentTermsInIndex`.
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a>Synoniemen inschakelen

U kunt synoniemen op basis van twee stappen inschakelen. We eerst definiëren en synoniem regels uploaden en configureer vervolgens velden toouse ze. Hallo-proces wordt beschreven in `UploadSynonyms` en `EnableSynonymsInHotelsIndex`.

1. Voeg een synoniem kaart tooyour search-service. In `UploadSynonyms`, we vier regels definiëren in onze synoniem kaart 'desc synonymmap' en toohello service uploaden.
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
Een kaart synoniem toohello open-source standaard moet voldoen `solr` indeling. Hallo-indeling wordt uitgelegd in [synoniemen in Azure Search](search-synonyms.md) onder sectie Hallo `Apache Solr synonym format`.

2. De doorzoekbare velden toouse Hallo synoniem kaart in Hallo indexdefinitie configureren. In `EnableSynonymsInHotelsIndex`, we synoniemen op twee velden inschakelen `category` en `tags` door Hallo instelling `synonymMaps` toohello eigenschapsnaam van Hallo zojuist synoniem kaart geüpload.
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
Wanneer u een synoniemtoewijzing toevoegt, is het niet nodig om indexen opnieuw op te bouwen. U kunt een synoniem kaart tooyour service toevoegen en wijzig bestaande velddefinities in een index toouse Hallo nieuwe synoniem kaart. Hallo toevoeging van nieuwe kenmerken heeft geen invloed op de beschikbaarheid van de index. Hallo geldt ook tijdens het uitschakelen van synoniemen voor een veld. U kunt eenvoudig hello instellen `synonymMaps` eigenschap tooan lege lijst.
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a>'Na'-query's

Nadat het Hallo synoniem kaart wordt geüpload en Hallo index bijgewerkte toouse Hallo synoniem kaart, Hallo tweede `RunQueriesWithNonExistentTermsInIndex` aanroep levert Hallo volgende:

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
Hallo eerste query vindt Hallo document van de regel Hallo `five star=>luxury`. Hallo tweede query wordt uitgebreid Hallo zoekactie met `internet,wifi` en Hallo derde met zowel `hotel, motel` en `economy,inexpensive=>budget` bij het zoeken naar documenten Hallo overeenkomt.

Volledig toe te voegen synoniemen Hallo zoekervaring wordt gewijzigd. Hallo oorspronkelijke query's kunnen in deze zelfstudie tooreturn betekenisvolle resultaten Hoewel Hallo documenten in onze index relevant zijn. Doordat synoniemen kunt we een index tooinclude voorwaarden gemeenschappelijk zonder wijzigingen toounderlying gegevens in de index Hallo gebruiken uitbreiden.

## <a name="sample-application-source-code"></a>Broncode van een voorbeeldtoepassing
U vindt de volledige broncode Hallo van Hallo-voorbeeldtoepassing die is gebruikt in deze doorloop op [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).

## <a name="next-steps"></a>Volgende stappen

* Bekijk [hoe toouse synoniemen in Azure Search](search-synonyms.md)
* Neem [REST API-documentatie over synoniemen](https://aka.ms/rgm6rq) door.
* Hallo-verwijzingen voor Hallo Bladeren [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) en [REST-API](https://docs.microsoft.com/rest/api/searchservice/).
