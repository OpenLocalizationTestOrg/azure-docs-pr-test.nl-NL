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
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a><span data-ttu-id="fe7e2-103">Het uploaden van gegevens tooAzure zoeken met Hallo .NET SDK</span><span class="sxs-lookup"><span data-stu-id="fe7e2-103">Upload data tooAzure Search using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe7e2-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="fe7e2-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="fe7e2-105">.NET</span><span class="sxs-lookup"><span data-stu-id="fe7e2-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="fe7e2-106">REST</span><span class="sxs-lookup"><span data-stu-id="fe7e2-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="fe7e2-107">In dit artikel wordt uitgelegd hoe u toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport gegevens in een Azure Search-index.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-107">This article will show you how toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="fe7e2-108">Voordat u deze procedure begint, moet u al [een Azure Search-index hebben gemaakt](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="fe7e2-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="fe7e2-109">In dit artikel wordt ervan uitgegaan dat u al hebt gemaakt een `SearchServiceClient` object, zoals aangegeven [een Azure Search index maken met .NET SDK Hallo](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="fe7e2-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="fe7e2-110">Alle voorbeeldcode in dit artikel is geschreven in C#.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="fe7e2-111">U vindt de volledige broncode Hallo [op GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="fe7e2-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="fe7e2-112">U kunt ook lezen over Hallo [Azure Search .NET SDK](search-howto-dotnet-sdk.md) voor een meer gedetailleerde doorloop van Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

<span data-ttu-id="fe7e2-113">In de volgorde toopush documenten in uw index met behulp van Hallo .NET SDK, moet u naar:</span><span class="sxs-lookup"><span data-stu-id="fe7e2-113">In order toopush documents into your index using hello .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="fe7e2-114">Maak een `SearchIndexClient` object tooconnect tooyour search-index.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-114">Create a `SearchIndexClient` object tooconnect tooyour search index.</span></span>
2. <span data-ttu-id="fe7e2-115">Maak een `IndexBatch` met Hallo documenten toobe toegevoegd, gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-115">Create an `IndexBatch` containing hello documents toobe added, modified, or deleted.</span></span>
3. <span data-ttu-id="fe7e2-116">Hallo aanroepen `Documents.Index` methode van uw `SearchIndexClient` toosend hello `IndexBatch` tooyour search-index.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-116">Call hello `Documents.Index` method of your `SearchIndexClient` toosend hello `IndexBatch` tooyour search index.</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="fe7e2-117">Maak een instantie van klasse SearchIndexClient Hallo</span><span class="sxs-lookup"><span data-stu-id="fe7e2-117">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="fe7e2-118">tooimport gegevens in uw index met hello Azure Search .NET SDK, moet u een exemplaar van Hallo toocreate `SearchIndexClient` klasse.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-118">tooimport data into your index using hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="fe7e2-119">U kunt deze instantie zelf samenstellen, maar de eenvoudiger als u al een `SearchServiceClient` exemplaar toocall de `Indexes.GetClient` methode.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance toocall its `Indexes.GetClient` method.</span></span> <span data-ttu-id="fe7e2-120">Hier is bijvoorbeeld hoe u zou krijgen een `SearchIndexClient` voor Hallo index "hotels" met de naam van een `SearchServiceClient` met de naam `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="fe7e2-120">For example, here is how you would obtain a `SearchIndexClient` for hello index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="fe7e2-121">In een standaardzoektoepassing wordt het beheer van de index en de invulling daarvan afgehandeld door een afzonderlijk onderdeel van de zoekquery’s.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="fe7e2-122">`Indexes.GetClient`is handig voor het invullen van een index, omdat u problemen van het bieden van een andere Hallo `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-122">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="fe7e2-123">Dit wordt uitgevoerd door Hallo beheersleutel doorgeeft die gebruikte toocreate u Hallo `SearchServiceClient` toohello nieuwe `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-123">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="fe7e2-124">Hallo deel van uw toepassing waarmee query's uitvoert, het is echter beter toocreate hello `SearchIndexClient` rechtstreeks zodat u in een querysleutel in plaats van een administratorsleutel doorgeven kunt.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-124">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="fe7e2-125">Dit komt overeen met de Hallo [principe van minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege) en helpt uw toepassing veiliger toomake.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-125">This is consistent with hello [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help toomake your application more secure.</span></span> <span data-ttu-id="fe7e2-126">U vindt meer informatie over administratorsleutels en querysleutels in Hallo [Azure Search REST API-verwijzing](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="fe7e2-126">You can find out more about admin keys and query keys in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="fe7e2-127">`SearchIndexClient` heeft een `Documents`-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="fe7e2-128">Deze eigenschap bevat alle Hallo-methoden, moet u tooadd, wijzigen, verwijderen of documenten in uw index opvragen.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-128">This property provides all hello methods you need tooadd, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="fe7e2-129">Bepaal welke indexering actie toouse</span><span class="sxs-lookup"><span data-stu-id="fe7e2-129">Decide which indexing action toouse</span></span>
<span data-ttu-id="fe7e2-130">tooimport gegevens met behulp van Hallo .NET SDK, moet u toopackage van uw gegevens in een `IndexBatch` object.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-130">tooimport data using hello .NET SDK, you will need toopackage up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="fe7e2-131">Een `IndexBatch` omvat een verzameling van `IndexAction` objecten, die elk een document en een eigenschap die Azure Search welke actie tooperform op het document (uploaden, samenvoegen, verwijderen, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="fe7e2-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action tooperform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="fe7e2-132">Afhankelijk van welke van Hallo onderstaande bewerkingen die u kiest, moet alleen bepaalde velden voor elk document opnemen:</span><span class="sxs-lookup"><span data-stu-id="fe7e2-132">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="fe7e2-133">Actie</span><span class="sxs-lookup"><span data-stu-id="fe7e2-133">Action</span></span> | <span data-ttu-id="fe7e2-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fe7e2-134">Description</span></span> | <span data-ttu-id="fe7e2-135">Vereiste velden voor elk document</span><span class="sxs-lookup"><span data-stu-id="fe7e2-135">Necessary fields for each document</span></span> | <span data-ttu-id="fe7e2-136">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="fe7e2-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="fe7e2-137">Een `Upload` actie is vergelijkbaar tooan "upsert", waarbij Hallo document wordt ingevoegd als het nieuwe en bijgewerkt/vervangen als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-137">An `Upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="fe7e2-138">sleutel, plus andere velden die u wenst dat toodefine</span><span class="sxs-lookup"><span data-stu-id="fe7e2-138">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="fe7e2-139">Wanneer het bijwerken/vervangen van een bestaand document wordt elk veld dat niet is opgegeven in de aanvraag Hallo hebt ingesteld te`null`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-139">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="fe7e2-140">Dit gebeurt zelfs als Hallo veld eerder tooa null-waarde is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-140">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `Merge` |<span data-ttu-id="fe7e2-141">Een bestaand document met het Hallo updates opgegeven velden.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-141">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="fe7e2-142">Als Hallo document niet in de index hello bestaat, mislukt de Hallo samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-142">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="fe7e2-143">sleutel, plus andere velden die u wenst dat toodefine</span><span class="sxs-lookup"><span data-stu-id="fe7e2-143">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="fe7e2-144">Elk veld dat u in een samenvoeging opgeeft wordt vervangen door Hallo bestaand veld in Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-144">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="fe7e2-145">ook velden van het type `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="fe7e2-146">Bijvoorbeeld, als hello document bevat een veld `tags` met waarde `["budget"]` en u een samenvoeging met de waarde `["economy", "pool"]` voor `tags`, uiteindelijke waarde van Hallo Hallo `tags` veld `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-146">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="fe7e2-147">Het wordt dus niet `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="fe7e2-148">Deze bewerking gedraagt zich als `Merge` wanneer een document met de opgegeven sleutel al Hallo in Hallo index bestaat.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-148">This action behaves like `Merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="fe7e2-149">Als het Hallo-document niet bestaat, gedraagt zich als `Upload` met een nieuw document.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-149">If hello document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="fe7e2-150">sleutel, plus andere velden die u wenst dat toodefine</span><span class="sxs-lookup"><span data-stu-id="fe7e2-150">key, plus any other fields you wish toodefine</span></span> |- |
| `Delete` |<span data-ttu-id="fe7e2-151">Verwijdert het opgegeven document Hallo van Hallo index.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-151">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="fe7e2-152">alleen sleutel</span><span class="sxs-lookup"><span data-stu-id="fe7e2-152">key only</span></span> |<span data-ttu-id="fe7e2-153">Alle velden die u opgeeft dan Hallo sleutelveld worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-153">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="fe7e2-154">Als u wilt dat tooremove een afzonderlijk veld uit een document, gebruikt u `Merge` en stelt u Hallo veld expliciet toonull.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-154">If you want tooremove an individual field from a document, use `Merge` instead and simply set hello field explicitly toonull.</span></span> |

<span data-ttu-id="fe7e2-155">U kunt opgeven welke actie wilt u toouse met verschillende statische methoden van Hallo Hallo `IndexBatch` en `IndexAction` klassen, zoals wordt weergegeven in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-155">You can specify what action you want toouse with hello various static methods of hello `IndexBatch` and `IndexAction` classes, as shown in hello next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="fe7e2-156">Uw IndexBatch maken</span><span class="sxs-lookup"><span data-stu-id="fe7e2-156">Construct your IndexBatch</span></span>
<span data-ttu-id="fe7e2-157">Nu u weet welke tooperform acties op uw documenten, bent u klaar tooconstruct hello `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-157">Now that you know which actions tooperform on your documents, you are ready tooconstruct hello `IndexBatch`.</span></span> <span data-ttu-id="fe7e2-158">voorbeeld hieronder toont hoe Hallo toocreate een batch met verschillende bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-158">hello example below shows how toocreate a batch with a few different actions.</span></span> <span data-ttu-id="fe7e2-159">Dit voorbeeld wordt een aangepaste klasse aangeroepen Opmerking `Hotel` die tooa document in de index "hotels" hello wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-159">Note that our example uses a custom class called `Hotel` that maps tooa document in hello "hotels" index.</span></span>

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

<span data-ttu-id="fe7e2-160">In dit geval gebruiken we `Upload`, `MergeOrUpload`, en `Delete` als onze zoekacties, zoals opgegeven door Hallo methoden aangeroepen op Hallo `IndexAction` klasse.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by hello methods called on hello `IndexAction` class.</span></span>

<span data-ttu-id="fe7e2-161">We gaan ervan uit dat deze voorbeeldindex "hotels" al is gevuld met een aantal documenten.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="fe7e2-162">Hoe we hoefden niet toospecify alle mogelijke documentvelden Hallo bij gebruik van `MergeOrUpload` en hoe we alleen opgegeven Hallo documentsleutel (`HotelId`) bij gebruik van `Delete`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-162">Note how we did not have toospecify all hello possible document fields when using `MergeOrUpload` and how we only specified hello document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="fe7e2-163">Merk ook op die u kunt alleen too1000 documenten in een enkele indexeringsaanvraag opnemen.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-163">Also, note that you can only include up too1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="fe7e2-164">In dit voorbeeld passen we verschillende bewerkingen toodifferent documenten.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-164">In this example, we are applying different actions toodifferent documents.</span></span> <span data-ttu-id="fe7e2-165">Als u deze wilde tooperform dezelfde bewerkingen op alle documenten in Hallo batch, in plaats van aanroepen Hallo `IndexBatch.New`, kunt u andere statische methode van Hallo `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-165">If you wanted tooperform hello same actions across all documents in hello batch, instead of calling `IndexBatch.New`, you could use hello other static methods of `IndexBatch`.</span></span> <span data-ttu-id="fe7e2-166">U kunt bijvoorbeeld batches maken door `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, of `IndexBatch.Delete` aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="fe7e2-167">Deze methoden maken gebruik van een verzameling van documenten (objecten van het type `Hotel` in dit voorbeeld) in plaats van `IndexAction`-objecten.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-toohello-index"></a><span data-ttu-id="fe7e2-168">Index van toohello importeren</span><span class="sxs-lookup"><span data-stu-id="fe7e2-168">Import data toohello index</span></span>
<span data-ttu-id="fe7e2-169">Nu dat u een geïnitialiseerd hebt `IndexBatch` object, kunt u deze verzenden toohello index door aan te roepen `Documents.Index` op uw `SearchIndexClient` object.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-169">Now that you have an initialized `IndexBatch` object, you can send it toohello index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="fe7e2-170">Hallo volgende voorbeeld wordt getoond hoe toocall `Index`, plus een aantal extra stappen die u moet tooperform:</span><span class="sxs-lookup"><span data-stu-id="fe7e2-170">hello following example shows how toocall `Index`, as well as some extra steps you will need tooperform:</span></span>

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

<span data-ttu-id="fe7e2-171">Opmerking Hallo `try` / `catch` omringende Hallo aanroep toohello `Index` methode.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-171">Note hello `try`/`catch` surrounding hello call toohello `Index` method.</span></span> <span data-ttu-id="fe7e2-172">Hallo catch-blok verwerkt een belangrijke foutaanvraag voor indexering.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-172">hello catch block handles an important error case for indexing.</span></span> <span data-ttu-id="fe7e2-173">Als uw Azure Search-service geen tooindex aantal Hallo documenten in batch Hallo, een `IndexBatchException` verstuurd door `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-173">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="fe7e2-174">Dit kan gebeuren als u documenten indexeert terwijl uw service zwaar wordt belast.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="fe7e2-175">**Wij raden u aan deze aanvraag expliciet in uw code te behandelen.**</span><span class="sxs-lookup"><span data-stu-id="fe7e2-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="fe7e2-176">U kunt vertraging en probeer het vervolgens opnieuw indexeren Hallo-documenten die niet of u kunt zich aanmelden en doorgaan zoals Hallo voorbeeld, of kunt u iets anders, afhankelijk van de gegevensvereisten consistentie van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-176">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="fe7e2-177">Ten slotte Hallo code in de vorige twee seconden vertraagd Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-177">Finally, hello code in hello example above delays for two seconds.</span></span> <span data-ttu-id="fe7e2-178">Het indexeren verloopt asynchroon op in uw Azure Search-service, zodat het Hallo-voorbeeldtoepassing moet toowait een korte tijd tooensure dat Hallo documenten beschikbaar voor zoeken zijn.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-178">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="fe7e2-179">Dergelijke vertragingen zijn doorgaans alleen nodig is demo’s, testen en voorbeeldtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="fe7e2-180">Hoe documenten worden verwerkt door Hallo .NET SDK</span><span class="sxs-lookup"><span data-stu-id="fe7e2-180">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="fe7e2-181">U vraagt zich misschien af hoe hello Azure Search .NET SDK is kunnen tooupload exemplaren van een gebruiker gedefinieerde klasse zoals `Hotel` toohello index.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-181">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="fe7e2-182">toohelp deze vraag te beantwoorden, bekijken we Hallo `Hotel` klasse, die wordt toegewezen toohello indexschema dat is gedefinieerd in [een Azure Search index maken met .NET SDK Hallo](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="fe7e2-182">toohelp answer that question, let's look at hello `Hotel` class, which maps toohello index schema defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="fe7e2-183">Hallo eerst te beginnen toonotice is dat elke openbare eigenschap van `Hotel` overeenkomt met tooa veld in de indexdefinitie hello, maar met een cruciaal verschil: Hallo-naam van elk veld begint met een kleine letter ("kamelen"), terwijl Hallo-naam van elke bevolking de eigenschap van `Hotel` begint met een hoofdletter ("Pascal geval').</span><span class="sxs-lookup"><span data-stu-id="fe7e2-183">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="fe7e2-184">Dit is een veelvoorkomend scenario in .NET-toepassingen die gegevens koppelen waarbij Hallo doelschema buiten Hallo beheer van de ontwikkelaar van de toepassing hello is.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-184">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="fe7e2-185">In plaats van tooviolate Hallo .NET-naamgevingsregels door het maken van de eigenschap namen kamelen, kunt u zien Hallo SDK toomap Hallo eigenschap namen toocamel case automatisch met Hallo `[SerializePropertyNamesAsCamelCase]` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-185">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="fe7e2-186">Hello Azure Search .NET SDK maakt gebruik van Hallo [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) bibliotheek tooserialize en deserialiseren van uw aangepaste model objecten tooand van JSON.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-186">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="fe7e2-187">U kunt deze serialisatie indien nodig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="fe7e2-188">Meer informatie vindt u in [Aangepaste serialisatie met JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="fe7e2-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="fe7e2-189">Een voorbeeld hiervan is Hallo gebruik Hallo `[JsonProperty]` -kenmerk op Hallo `DescriptionFr` eigenschap in de bovenstaande Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-189">One example of this is hello use of hello `[JsonProperty]` attribute on hello `DescriptionFr` property in hello sample code above.</span></span>
> 
> 

<span data-ttu-id="fe7e2-190">Hallo wat belangrijk is over Hallo `Hotel` klasse, zijn de gegevenstypen Hallo van Hallo openbare eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-190">hello second important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="fe7e2-191">Hallo .NET-typen van deze eigenschappen worden toegewezen tootheir gelijkwaardige veldtypen in Hallo indexdefinitie.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-191">hello .NET types of these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="fe7e2-192">Bijvoorbeeld, Hallo `Category` tekenreekseigenschap toegewezen toohello `category` veld van het type `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-192">For example, hello `Category` string property maps toohello `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="fe7e2-193">Er zijn vergelijkbare type toewijzingen tussen `bool?` en `DataType.Boolean`, `DateTimeOffset?` en `DataType.DateTimeOffset`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="fe7e2-194">Hallo specifieke regels voor de toewijzing van Hallo type zijn gedocumenteerd in Hallo `Documents.Get` methode in Hallo [Azure Search .NET SDK verwijzing](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="fe7e2-194">hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="fe7e2-195">Deze mogelijkheid toouse uw eigen klassen als documenten werkt beide kanten; U kunt ook zoekresultaten ophalen en Hallo SDK automatisch deserialiseert tooa type van uw keuze, zoals wordt weergegeven in Hallo [volgende artikel](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="fe7e2-195">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as shown in hello [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fe7e2-196">Hello Azure Search .NET SDK biedt ook ondersteuning voor dynamisch getypeerde documenten met behulp van Hallo `Document` klasse, die een sleutel/waarde-aan veldwaarden namen toofield toewijst.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-196">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="fe7e2-197">Dit is nuttig in scenario's, indien u niet weet Hallo Indexeer schema op het moment van ontwerp of dat het onhandig toobind toospecific modelklassen normaal zou zijn.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-197">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="fe7e2-198">Alle Hallo methoden in Hallo SDK die met documenten werken hebben overloads die met Hallo werken `Document` klasse, evenals sterk getypeerde overloads die een generiek typeparameter moeten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-198">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="fe7e2-199">Alleen voor het laatste hello worden gebruikt in Hallo voorbeeldcode in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-199">Only hello latter are used in hello sample code in this article.</span></span>
> 
> 

<span data-ttu-id="fe7e2-200">**Waarom u nullable-gegevenstypen moet gebruiken**</span><span class="sxs-lookup"><span data-stu-id="fe7e2-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="fe7e2-201">Bij het ontwerpen van uw eigen model klassen toomap tooan Azure Search-index we raden u aan om eigenschappen van waardentypen zoals `bool` en `int` toobe null-waarden bevatten (bijvoorbeeld `bool?` in plaats van `bool`).</span><span class="sxs-lookup"><span data-stu-id="fe7e2-201">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="fe7e2-202">Als u een niet-nullbare eigenschap gebruikt, hebt u te**garanderen** dat de documenten in uw index geen null-waarde voor het betreffende veld Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-202">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="fe7e2-203">Hallo SDK noch hello Azure Search-service kunt u tooenforce dit.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-203">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="fe7e2-204">Dit is niet alleen een hypothetische probleem: Stel een scenario waarin het toevoegen van een nieuw veld tooan bestaande index van het type `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="fe7e2-205">Na het bijwerken van de indexdefinitie hello, moeten alle documenten een null-waarde voor het nieuwe veld (omdat alle typen null in Azure Search).</span><span class="sxs-lookup"><span data-stu-id="fe7e2-205">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="fe7e2-206">Als u vervolgens een modelklasse met een niet-nullbare `int` eigenschap voor dat veld gebruikt, ontvangt u een `JsonSerializationException` zoals deze bij het tooretrieve documenten:</span><span class="sxs-lookup"><span data-stu-id="fe7e2-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="fe7e2-207">Daarom wordt u aangeraden nullbare typen in uw modelklassen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe7e2-208">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fe7e2-208">Next steps</span></span>
<span data-ttu-id="fe7e2-209">Na het vullen van uw Azure Search-index, zult u gereed toostart uitgeven van query's toosearch voor documenten.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-209">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="fe7e2-210">Zie [Een query uitvoeren in uw Azure-zoekindex](search-query-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fe7e2-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

