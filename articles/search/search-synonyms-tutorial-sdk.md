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
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="e0e4f-103">Synoniemenzelfstudie (preview, C#) voor Azure Search</span><span class="sxs-lookup"><span data-stu-id="e0e4f-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="e0e4f-104">Een query uitbreiden synoniemen door overeenkomende op voorwaarden die worden beschouwd als dezelfde toohello invoer term.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-104">Synonyms expand a query by matching on terms considered semantically equivalent toohello input term.</span></span> <span data-ttu-id="e0e4f-105">U kunt bijvoorbeeld 'auto' toomatch documenten met voorwaarden Hallo 'auto' of 'vehicle'.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-105">For example, you might want "car" toomatch documents containing hello terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="e0e4f-106">In Azure Search worden synoniemen gedefinieerd in een *synoniementoewijzing* op basis van *toewijzingsregels* waarmee equivalente termen worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="e0e4f-107">Maken van meerdere synoniem maps, plaatst u deze als een index van de beschikbare tooany servicegebeurtenis resource en vervolgens verwijzen naar welke één toouse op Hallo veldniveau.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-107">You can create multiple synonym maps, post them as a service-wide resource available tooany index, and then reference which one toouse at hello field level.</span></span> <span data-ttu-id="e0e4f-108">Op het moment dat de query heeft daarnaast toosearching een Azure Search-index een zoekopdracht in een kaart synoniem als er een is opgegeven voor velden die worden gebruikt in query Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-108">At query time, in addition toosearching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e4f-109">Hallo-synoniemen functie is momenteel in preview en alleen ondersteund Hallo meest recente preview-API en SDK-versies (api-version = 2016-09-01-Preview, SDK versie 4.x-preview).</span><span class="sxs-lookup"><span data-stu-id="e0e4f-109">hello synonyms feature is currently in preview and only supported in hello latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="e0e4f-110">Azure Portal biedt er momenteel geen ondersteuning voor.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="e0e4f-111">Preview-API's vallen niet onder een SLA en de previewfuncties kunnen veranderen. Daarom raden we u af om deze in productietoepassingen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0e4f-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e0e4f-112">Prerequisites</span></span>

<span data-ttu-id="e0e4f-113">Zelfstudie vereisten zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="e0e4f-113">Tutorial requirements include hello following:</span></span>

* [<span data-ttu-id="e0e4f-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0e4f-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="e0e4f-115">Azure Search-service</span><span class="sxs-lookup"><span data-stu-id="e0e4f-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="e0e4f-116">Preview-versie van de .NET-bibliotheek Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="e0e4f-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="e0e4f-117">Hoe toouse Azure zoeken vanuit een .NET-toepassing</span><span class="sxs-lookup"><span data-stu-id="e0e4f-117">How toouse Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="e0e4f-118">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e0e4f-118">Overview</span></span>

<span data-ttu-id="e0e4f-119">Query's voor en na demonstreren Hallo-waarde van synoniemen.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-119">Before-and-after queries demonstrate hello value of synonyms.</span></span> <span data-ttu-id="e0e4f-120">In deze zelfstudie gebruikt u een voorbeeldtoepassing die query's uitvoert en resultaten retourneert in een voorbeeldindex.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="e0e4f-121">Hallo-voorbeeldtoepassing maakt een kleine index met de naam "hotels" is gevuld met twee documenten.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-121">hello sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="e0e4f-122">Hallo-toepassing wordt uitgevoerd zoekopdrachten met voorwaarden en die niet in de index hello voorkomen, Hallo synoniemen functie, activeert vervolgens problemen Hallo dezelfde zoekopdrachten opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-122">hello application executes search queries using terms and phrases that do not appear in hello index, enables hello synonyms feature, then issues hello same searches again.</span></span> <span data-ttu-id="e0e4f-123">Hallo-code hieronder laat zien Hallo algemene stroom.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-123">hello code below demonstrates hello overall flow.</span></span>

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
<span data-ttu-id="e0e4f-124">Hallo stappen toocreate en Hallo voorbeeld index te vullen worden beschreven [hoe toouse Azure zoeken vanuit een .NET-toepassing](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="e0e4f-124">hello steps toocreate and populate hello sample index are explained in [How toouse Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="e0e4f-125">'Voor'-query's</span><span class="sxs-lookup"><span data-stu-id="e0e4f-125">"Before" queries</span></span>

<span data-ttu-id="e0e4f-126">In `RunQueriesWithNonExistentTermsInIndex` worden er zoekquery's uitgevoerd met 'vijfsterren', 'internet' en 'voordelig EN hotel'.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
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
<span data-ttu-id="e0e4f-127">Geen van de twee geïndexeerde documenten Hallo Hallo-termen bevatten zodat we Hallo volgende eerst de uitvoer van Hallo `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-127">Neither of hello two indexed documents contain hello terms, so we get hello following output from hello first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="e0e4f-128">Synoniemen inschakelen</span><span class="sxs-lookup"><span data-stu-id="e0e4f-128">Enable synonyms</span></span>

<span data-ttu-id="e0e4f-129">U kunt synoniemen op basis van twee stappen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="e0e4f-130">We eerst definiëren en synoniem regels uploaden en configureer vervolgens velden toouse ze.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-130">We first define and upload synonym rules and then configure fields toouse them.</span></span> <span data-ttu-id="e0e4f-131">Hallo-proces wordt beschreven in `UploadSynonyms` en `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-131">hello process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="e0e4f-132">Voeg een synoniem kaart tooyour search-service.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-132">Add a synonym map tooyour search service.</span></span> <span data-ttu-id="e0e4f-133">In `UploadSynonyms`, we vier regels definiëren in onze synoniem kaart 'desc synonymmap' en toohello service uploaden.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload toohello service.</span></span>
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
<span data-ttu-id="e0e4f-134">Een kaart synoniem toohello open-source standaard moet voldoen `solr` indeling.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-134">A synonym map must conform toohello open source standard `solr` format.</span></span> <span data-ttu-id="e0e4f-135">Hallo-indeling wordt uitgelegd in [synoniemen in Azure Search](search-synonyms.md) onder sectie Hallo `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-135">hello format is explained in [Synonyms in Azure Search](search-synonyms.md) under hello section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="e0e4f-136">De doorzoekbare velden toouse Hallo synoniem kaart in Hallo indexdefinitie configureren.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-136">Configure searchable fields toouse hello synonym map in hello index definition.</span></span> <span data-ttu-id="e0e4f-137">In `EnableSynonymsInHotelsIndex`, we synoniemen op twee velden inschakelen `category` en `tags` door Hallo instelling `synonymMaps` toohello eigenschapsnaam van Hallo zojuist synoniem kaart geüpload.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting hello `synonymMaps` property toohello name of hello newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="e0e4f-138">Wanneer u een synoniemtoewijzing toevoegt, is het niet nodig om indexen opnieuw op te bouwen.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="e0e4f-139">U kunt een synoniem kaart tooyour service toevoegen en wijzig bestaande velddefinities in een index toouse Hallo nieuwe synoniem kaart.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-139">You can add a synonym map tooyour service, and then amend existing field definitions in any index toouse hello new synonym map.</span></span> <span data-ttu-id="e0e4f-140">Hallo toevoeging van nieuwe kenmerken heeft geen invloed op de beschikbaarheid van de index.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-140">hello addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="e0e4f-141">Hallo geldt ook tijdens het uitschakelen van synoniemen voor een veld.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-141">hello same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="e0e4f-142">U kunt eenvoudig hello instellen `synonymMaps` eigenschap tooan lege lijst.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-142">You can simply set hello `synonymMaps` property tooan empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="e0e4f-143">'Na'-query's</span><span class="sxs-lookup"><span data-stu-id="e0e4f-143">"After" queries</span></span>

<span data-ttu-id="e0e4f-144">Nadat het Hallo synoniem kaart wordt geüpload en Hallo index bijgewerkte toouse Hallo synoniem kaart, Hallo tweede `RunQueriesWithNonExistentTermsInIndex` aanroep levert Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="e0e4f-144">After hello synonym map is uploaded and hello index is updated toouse hello synonym map, hello second `RunQueriesWithNonExistentTermsInIndex` call outputs hello following:</span></span>

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="e0e4f-145">Hallo eerste query vindt Hallo document van de regel Hallo `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-145">hello first query finds hello document from hello rule `five star=>luxury`.</span></span> <span data-ttu-id="e0e4f-146">Hallo tweede query wordt uitgebreid Hallo zoekactie met `internet,wifi` en Hallo derde met zowel `hotel, motel` en `economy,inexpensive=>budget` bij het zoeken naar documenten Hallo overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-146">hello second query expands hello search using `internet,wifi` and hello third using both `hotel, motel` and `economy,inexpensive=>budget` in finding hello documents they matched.</span></span>

<span data-ttu-id="e0e4f-147">Volledig toe te voegen synoniemen Hallo zoekervaring wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-147">Adding synonyms completely changes hello search experience.</span></span> <span data-ttu-id="e0e4f-148">Hallo oorspronkelijke query's kunnen in deze zelfstudie tooreturn betekenisvolle resultaten Hoewel Hallo documenten in onze index relevant zijn.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-148">In this tutorial, hello original queries failed tooreturn meaningful results even though hello documents in our index were relevant.</span></span> <span data-ttu-id="e0e4f-149">Doordat synoniemen kunt we een index tooinclude voorwaarden gemeenschappelijk zonder wijzigingen toounderlying gegevens in de index Hallo gebruiken uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-149">By enabling synonyms, we can expand an index tooinclude terms in common use, with no changes toounderlying data in hello index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="e0e4f-150">Broncode van een voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="e0e4f-150">Sample application source code</span></span>
<span data-ttu-id="e0e4f-151">U vindt de volledige broncode Hallo van Hallo-voorbeeldtoepassing die is gebruikt in deze doorloop op [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="e0e4f-151">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0e4f-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0e4f-152">Next steps</span></span>

* <span data-ttu-id="e0e4f-153">Bekijk [hoe toouse synoniemen in Azure Search](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="e0e4f-153">Review [How toouse synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="e0e4f-154">Neem [REST API-documentatie over synoniemen](https://aka.ms/rgm6rq) door.</span><span class="sxs-lookup"><span data-stu-id="e0e4f-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="e0e4f-155">Hallo-verwijzingen voor Hallo Bladeren [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) en [REST-API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="e0e4f-155">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
