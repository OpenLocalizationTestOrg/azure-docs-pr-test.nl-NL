---
title: Gegevens uploaden (.NET - Azure Search) | Microsoft Docs
description: Informatie over het uploaden van gegevens naar een index in Azure Search met behulp van de .NET SDK.
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
ms.openlocfilehash: bdd952869143c6ca6374bb9264db5bcba1f32b50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-net-sdk"></a><span data-ttu-id="4dc47-103">Gegevens uploaden naar Azure Search met behulp van de .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4dc47-103">Upload data to Azure Search using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4dc47-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4dc47-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="4dc47-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4dc47-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="4dc47-106">REST</span><span class="sxs-lookup"><span data-stu-id="4dc47-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="4dc47-107">In dit artikel wordt beschreven hoe u met behulp van de [Azure Search .NET SDK](https://aka.ms/search-sdk) gegevens in een Azure Search-index importeert.</span><span class="sxs-lookup"><span data-stu-id="4dc47-107">This article will show you how to use the [Azure Search .NET SDK](https://aka.ms/search-sdk) to import data into an Azure Search index.</span></span>

<span data-ttu-id="4dc47-108">Voordat u deze procedure begint, moet u al [een Azure Search-index hebben gemaakt](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="4dc47-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="4dc47-109">In dit artikel wordt ervan uitgegaan dat u al een `SearchServiceClient`-object hebt gemaakt, zoals uiteengezet in [Een Azure Search-index maken met de.NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="4dc47-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="4dc47-110">Alle voorbeeldcode in dit artikel is geschreven in C#.</span><span class="sxs-lookup"><span data-stu-id="4dc47-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="4dc47-111">U vindt de volledige broncode [op GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="4dc47-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="4dc47-112">Voor een uitgebreidere walkthrough van de voorbeeldcode kunt ook meer lezen over de [.NET-SDK voor Azure Search](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4dc47-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

<span data-ttu-id="4dc47-113">Om documenten in uw index te pushen met behulp van de .NET SDK, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="4dc47-113">In order to push documents into your index using the .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="4dc47-114">Maak een `SearchIndexClient`-object om verbinding te maken met uw zoekindex.</span><span class="sxs-lookup"><span data-stu-id="4dc47-114">Create a `SearchIndexClient` object to connect to your search index.</span></span>
2. <span data-ttu-id="4dc47-115">Maak een `IndexBatch` met de documenten die moeten worden toegevoegd, gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4dc47-115">Create an `IndexBatch` containing the documents to be added, modified, or deleted.</span></span>
3. <span data-ttu-id="4dc47-116">Roep de `Documents.Index`-methode van uw `SearchIndexClient` aan om de `IndexBatch` naar uw zoekindex te verzenden.</span><span class="sxs-lookup"><span data-stu-id="4dc47-116">Call the `Documents.Index` method of your `SearchIndexClient` to send the `IndexBatch` to your search index.</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="4dc47-117">Een instantie van de klasse SearchIndexClient maken</span><span class="sxs-lookup"><span data-stu-id="4dc47-117">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="4dc47-118">Om de Azure Search .NET SDK te kunnen gebruiken om gegevens in uw index te importeren, moet u een instantie van klasse `SearchIndexClient` maken.</span><span class="sxs-lookup"><span data-stu-id="4dc47-118">To import data into your index using the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="4dc47-119">U kunt deze instantie zelf samenstellen, maar het is eenvoudiger als u al een `SearchServiceClient`-instantie hebt om de methode `Indexes.GetClient` aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="4dc47-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance to call its `Indexes.GetClient` method.</span></span> <span data-ttu-id="4dc47-120">U kunt bijvoorbeeld op de volgende manier een `SearchIndexClient` verkrijgen voor de index met de naam "hotels" van een `SearchServiceClient` met de naam `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="4dc47-120">For example, here is how you would obtain a `SearchIndexClient` for the index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="4dc47-121">In een standaardzoektoepassing wordt het beheer van de index en de invulling daarvan afgehandeld door een afzonderlijk onderdeel van de zoekquery’s.</span><span class="sxs-lookup"><span data-stu-id="4dc47-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="4dc47-122">`Indexes.GetClient` is handig voor het vullen van een index, omdat u geen andere `SearchCredentials` hoeft op te geven.</span><span class="sxs-lookup"><span data-stu-id="4dc47-122">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="4dc47-123">Dit wordt uitgevoerd door de administratorsleutel die u hebt gebruikt om de `SearchServiceClient` te maken die u wilt doorgeven aan de nieuwe `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="4dc47-123">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="4dc47-124">In het gedeelte van uw toepassing waarmee u query's uitvoert, is het beter om de `SearchIndexClient` direct te maken, zodat u een querysleutel kunt toepassen in plaats van een administratorsleutel.</span><span class="sxs-lookup"><span data-stu-id="4dc47-124">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="4dc47-125">Dit komt overeen met het [-principe van minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege) en zorgt ervoor dat uw toepassing veilig is.</span><span class="sxs-lookup"><span data-stu-id="4dc47-125">This is consistent with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help to make your application more secure.</span></span> <span data-ttu-id="4dc47-126">Meer informatie over administratorsleutels en querysleutels vindt u in [Azure Search REST-API-verwijzingen](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="4dc47-126">You can find out more about admin keys and query keys in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="4dc47-127">`SearchIndexClient` heeft een `Documents`-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="4dc47-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="4dc47-128">Deze eigenschap bevat de methoden die u wilt toevoegen, wijzigen, verwijderen, of om documenten in uw index op te vragen.</span><span class="sxs-lookup"><span data-stu-id="4dc47-128">This property provides all the methods you need to add, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="4dc47-129">Bepalen welke indexeerbewerking u moet gebruiken</span><span class="sxs-lookup"><span data-stu-id="4dc47-129">Decide which indexing action to use</span></span>
<span data-ttu-id="4dc47-130">Om gegevens te importeren met de .NET SDK, moet u uw gegevens in een `IndexBatch`-object verpakken.</span><span class="sxs-lookup"><span data-stu-id="4dc47-130">To import data using the .NET SDK, you will need to package up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="4dc47-131">Een `IndexBatch` omvat een verzameling van `IndexAction`-objecten, die een document en een eigenschap bevatten die Azure Search aansturen om een bewerking op het document uit te voeren (uploaden, samenvoegen, verwijderen, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="4dc47-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action to perform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="4dc47-132">Afhankelijk van welke van de onderstaande bewerkingen u kiest, moet u slechts bepaalde velden voor elk document opnemen:</span><span class="sxs-lookup"><span data-stu-id="4dc47-132">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="4dc47-133">Bewerking</span><span class="sxs-lookup"><span data-stu-id="4dc47-133">Action</span></span> | <span data-ttu-id="4dc47-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4dc47-134">Description</span></span> | <span data-ttu-id="4dc47-135">Vereiste velden voor elk document</span><span class="sxs-lookup"><span data-stu-id="4dc47-135">Necessary fields for each document</span></span> | <span data-ttu-id="4dc47-136">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4dc47-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="4dc47-137">Een `Upload`-actie is vergelijkbaar met een "upsert", waarbij het document wordt ingevoegd als het nieuw is en wordt bijgewerkt/vervangen als het al bestaat.</span><span class="sxs-lookup"><span data-stu-id="4dc47-137">An `Upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="4dc47-138">sleutel, plus andere velden die u wilt definiëren</span><span class="sxs-lookup"><span data-stu-id="4dc47-138">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="4dc47-139">Tijdens het bijwerken/vervangen van een bestaand document wordt elk veld dat niet is opgegeven in de aanvraag ingesteld op `null`.</span><span class="sxs-lookup"><span data-stu-id="4dc47-139">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="4dc47-140">Dit gebeurt zelfs als het veld eerder is ingesteld op een niet-null-waarde.</span><span class="sxs-lookup"><span data-stu-id="4dc47-140">This occurs even when the field was previously set to a non-null value.</span></span> |
| `Merge` |<span data-ttu-id="4dc47-141">Een bestaand document wordt bijgewerkt met de opgegeven velden.</span><span class="sxs-lookup"><span data-stu-id="4dc47-141">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="4dc47-142">Als het document niet in de index bestaat, mislukt de samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="4dc47-142">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="4dc47-143">sleutel, plus andere velden die u wilt definiëren</span><span class="sxs-lookup"><span data-stu-id="4dc47-143">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="4dc47-144">Alle velden die u in een samenvoeging opgeeft, vervangen de bestaande velden in het document,</span><span class="sxs-lookup"><span data-stu-id="4dc47-144">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="4dc47-145">ook velden van het type `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="4dc47-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="4dc47-146">Als het document bijvoorbeeld een veld `tags` bevat met de waarde `["budget"]` en u een samenvoeging doet met de waarde `["economy", "pool"]` voor `tags`, wordt de uiteindelijke waarde van het veld `tags` `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="4dc47-146">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="4dc47-147">Het wordt dus niet `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="4dc47-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="4dc47-148">Deze bewerking gedraagt zich als `Merge` wanneer een document met de opgegeven sleutel al in de index bestaat.</span><span class="sxs-lookup"><span data-stu-id="4dc47-148">This action behaves like `Merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="4dc47-149">Als het document niet bestaat, gedraagt deze bewerking zich als `Upload` met een nieuw document.</span><span class="sxs-lookup"><span data-stu-id="4dc47-149">If the document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="4dc47-150">sleutel, plus andere velden die u wilt definiëren</span><span class="sxs-lookup"><span data-stu-id="4dc47-150">key, plus any other fields you wish to define</span></span> |- |
| `Delete` |<span data-ttu-id="4dc47-151">Het opgegeven document wordt uit de index verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4dc47-151">Removes the specified document from the index.</span></span> |<span data-ttu-id="4dc47-152">alleen sleutel</span><span class="sxs-lookup"><span data-stu-id="4dc47-152">key only</span></span> |<span data-ttu-id="4dc47-153">Alle andere velden worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="4dc47-153">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="4dc47-154">Als u een afzonderlijk veld uit een document wilt verwijderen, gebruikt u `Merge` en stelt u het veld expliciet in op null.</span><span class="sxs-lookup"><span data-stu-id="4dc47-154">If you want to remove an individual field from a document, use `Merge` instead and simply set the field explicitly to null.</span></span> |

<span data-ttu-id="4dc47-155">U kunt opgeven welke actie u wilt gebruiken met de verschillende statische methoden van de klassen `IndexBatch` en `IndexAction`, zoals wordt weergegeven in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="4dc47-155">You can specify what action you want to use with the various static methods of the `IndexBatch` and `IndexAction` classes, as shown in the next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="4dc47-156">Uw IndexBatch maken</span><span class="sxs-lookup"><span data-stu-id="4dc47-156">Construct your IndexBatch</span></span>
<span data-ttu-id="4dc47-157">Nu u weet welke bewerkingen u wilt uitvoeren op uw documenten, bent u klaar om de `IndexBatch` samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="4dc47-157">Now that you know which actions to perform on your documents, you are ready to construct the `IndexBatch`.</span></span> <span data-ttu-id="4dc47-158">Het volgende voorbeeld laat zien hoe u een batch met verschillende bewerkingen kunt maken.</span><span class="sxs-lookup"><span data-stu-id="4dc47-158">The example below shows how to create a batch with a few different actions.</span></span> <span data-ttu-id="4dc47-159">In dit voorbeeld wordt een aangepaste klasse gebruikt met de naam `Hotel`, die wordt toegewezen aan een document in de index "hotels".</span><span class="sxs-lookup"><span data-stu-id="4dc47-159">Note that our example uses a custom class called `Hotel` that maps to a document in the "hotels" index.</span></span>

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
                Description = "Close to town hall and the river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="4dc47-160">In dit geval gebruiken we `Upload`, `MergeOrUpload`, en `Delete` als de zoekacties, zoals opgegeven door de methoden die worden aangeroepen voor de `IndexAction`-klasse.</span><span class="sxs-lookup"><span data-stu-id="4dc47-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by the methods called on the `IndexAction` class.</span></span>

<span data-ttu-id="4dc47-161">We gaan ervan uit dat deze voorbeeldindex "hotels" al is gevuld met een aantal documenten.</span><span class="sxs-lookup"><span data-stu-id="4dc47-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="4dc47-162">We hoefden niet alle mogelijke documentvelden op te geven voor het gebruik van `MergeOrUpload`. We hebben alleen de documentsleutel (`HotelId`) opgegeven voor het gebruik van `Delete`.</span><span class="sxs-lookup"><span data-stu-id="4dc47-162">Note how we did not have to specify all the possible document fields when using `MergeOrUpload` and how we only specified the document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="4dc47-163">U kunt tot 1000 documenten in een enkele indexeringsaanvraag opnemen.</span><span class="sxs-lookup"><span data-stu-id="4dc47-163">Also, note that you can only include up to 1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="4dc47-164">In dit voorbeeld passen we verschillende bewerkingen op verschillende documenten toe.</span><span class="sxs-lookup"><span data-stu-id="4dc47-164">In this example, we are applying different actions to different documents.</span></span> <span data-ttu-id="4dc47-165">Als u dezelfde bewerkingen op alle documenten in de batch wilt uitvoeren, kunt u in plaats van `IndexBatch.New` aan te roepen, een andere statische methode van `IndexBatch` gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4dc47-165">If you wanted to perform the same actions across all documents in the batch, instead of calling `IndexBatch.New`, you could use the other static methods of `IndexBatch`.</span></span> <span data-ttu-id="4dc47-166">U kunt bijvoorbeeld batches maken door `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, of `IndexBatch.Delete` aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="4dc47-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="4dc47-167">Deze methoden maken gebruik van een verzameling van documenten (objecten van het type `Hotel` in dit voorbeeld) in plaats van `IndexAction`-objecten.</span><span class="sxs-lookup"><span data-stu-id="4dc47-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-to-the-index"></a><span data-ttu-id="4dc47-168">Gegevens naar de index importeren</span><span class="sxs-lookup"><span data-stu-id="4dc47-168">Import data to the index</span></span>
<span data-ttu-id="4dc47-169">Nu u een geïnitialiseerd `IndexBatch`-object hebt, kunt u het object naar de index sturen door `Documents.Index` aan te roepen op uw `SearchIndexClient`-object.</span><span class="sxs-lookup"><span data-stu-id="4dc47-169">Now that you have an initialized `IndexBatch` object, you can send it to the index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="4dc47-170">Het volgende voorbeeld laat zien hoe u `Index` kunt aanroepen, plus een aantal extra stappen die u moet uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4dc47-170">The following example shows how to call `Index`, as well as some extra steps you will need to perform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of the documents in
    // the batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log the failed document keys and continue.
    Console.WriteLine(
        "Failed to index some of the documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents to be indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="4dc47-171">Let op de `try`/`catch` rond de aanroep van de `Index`-methode.</span><span class="sxs-lookup"><span data-stu-id="4dc47-171">Note the `try`/`catch` surrounding the call to the `Index` method.</span></span> <span data-ttu-id="4dc47-172">Het catch-blok verwerkt een belangrijke foutaanvraag voor indexering.</span><span class="sxs-lookup"><span data-stu-id="4dc47-172">The catch block handles an important error case for indexing.</span></span> <span data-ttu-id="4dc47-173">Als uw Azure Search-service geen index van een aantal documenten in de batch kan maken, wordt een `IndexBatchException` verstuurd door `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="4dc47-173">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="4dc47-174">Dit kan gebeuren als u documenten indexeert terwijl uw service zwaar wordt belast.</span><span class="sxs-lookup"><span data-stu-id="4dc47-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="4dc47-175">**Wij raden u aan deze aanvraag expliciet in uw code te behandelen.**</span><span class="sxs-lookup"><span data-stu-id="4dc47-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="4dc47-176">U kunt de indexering van documenten die niet zijn geïndexeerd vertragen en vervolgens opnieuw uitvoeren, maar u kunt ook een logboek maken en doorgaan zoals in het voorbeeld. U kunt ook een andere bewerking uitvoeren, afhankelijk van de vereisten omtrent de gegevensconsistentie van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="4dc47-176">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="4dc47-177">De code in bovenstaand voorbeeld wordt dan twee seconden vertraagd.</span><span class="sxs-lookup"><span data-stu-id="4dc47-177">Finally, the code in the example above delays for two seconds.</span></span> <span data-ttu-id="4dc47-178">Het indexeren verloopt asynchroon in uw Azure Search-service. De voorbeeldtoepassing moet even wachten totdat de documenten beschikbaar zijn voor een zoekbewerking.</span><span class="sxs-lookup"><span data-stu-id="4dc47-178">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="4dc47-179">Dergelijke vertragingen zijn doorgaans alleen nodig is demo’s, testen en voorbeeldtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="4dc47-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="4dc47-180">De verwerking van documenten door .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4dc47-180">How the .NET SDK handles documents</span></span>
<span data-ttu-id="4dc47-181">U vraagt zich misschien af hoe de Azure Search .NET SDK instanties van een door een gebruiker gedefinieerde klasse zoals `Hotel` naar de index kan uploaden.</span><span class="sxs-lookup"><span data-stu-id="4dc47-181">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="4dc47-182">Om deze vraag te beantwoorden, bekijken we de `Hotel`-klasse van dichtbij. Deze klasse is toegewezen aan het indexschema dat is gedefinieerd in [Een Azure Search-index maken met behulp van de .NET SDK](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="4dc47-182">To help answer that question, let's look at the `Hotel` class, which maps to the index schema defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="4dc47-183">Het eerste dat opvalt, is dat elke openbare eigenschap van `Hotel` overeenkomt met een veld in de definitie van de index. Er is echter een cruciaal verschil: de naam van elk veld begint met een kleine letter ("kamelen"), terwijl de naam van elke openbare eigenschap van `Hotel` met een hoofdletter ("Pascal") begint.</span><span class="sxs-lookup"><span data-stu-id="4dc47-183">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="4dc47-184">Dit is een algemeen scenario in .NET-toepassingen die gegevens koppelen waarbij het doelschema buiten de controle van de ontwikkelaar van de toepassing valt.</span><span class="sxs-lookup"><span data-stu-id="4dc47-184">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="4dc47-185">In plaats van het schenden van de .NET-naamgevingsregels door een eigenschap met bijvoorbeeld de naam "kamelen" te maken, kunt u instellen dat de SDK de eigenschapsnamen automatisch moet toewijzen aan het `[SerializePropertyNamesAsCamelCase]`-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="4dc47-185">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="4dc47-186">De Azure Search .NET SDK maakt gebruik van de [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm)-bibliotheek voor het serialiseren en deserialiseren van uw aangepaste modelobjecten naar en van JSON.</span><span class="sxs-lookup"><span data-stu-id="4dc47-186">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="4dc47-187">U kunt deze serialisatie indien nodig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="4dc47-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="4dc47-188">Meer informatie vindt u in [Aangepaste serialisatie met JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="4dc47-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="4dc47-189">Een voorbeeld hiervan is het gebruik van het `[JsonProperty]`-kenmerk in de eigenschap `DescriptionFr` in de bovenstaande voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="4dc47-189">One example of this is the use of the `[JsonProperty]` attribute on the `DescriptionFr` property in the sample code above.</span></span>
> 
> 

<span data-ttu-id="4dc47-190">Wat ook belangrijk is in de `Hotel`-klasse, zijn de gegevenstypen van de openbare eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4dc47-190">The second important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="4dc47-191">De .NET-typen van deze eigenschappen worden toegewezen aan de gelijkwaardige veldtypen in de definitie van de index.</span><span class="sxs-lookup"><span data-stu-id="4dc47-191">The .NET types of these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="4dc47-192">De tekenreekseigenschap `Category` is bijvoorbeeld toegewezen aan het veld `category` van type `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="4dc47-192">For example, the `Category` string property maps to the `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="4dc47-193">Er zijn vergelijkbare type toewijzingen tussen `bool?` en `DataType.Boolean`, `DateTimeOffset?` en `DataType.DateTimeOffset`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="4dc47-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="4dc47-194">De specifieke regels voor de toewijzing van het type worden gedocumenteerd met de methode `Documents.Get` in de [Azure Search .NET SDK-verwijzing](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="4dc47-194">The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="4dc47-195">De mogelijkheid om uw eigen klassen te gebruiken als documenten werkt beide kanten op: u kunt ook zoekresultaten ophalen en ervoor zorgen dat de SDK de resultaten automatisch deserialiseert naar een type dat u hebt ingesteld, zoals wordt uitgelegd in het [volgende artikel](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4dc47-195">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as shown in the [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4dc47-196">De Azure Search .NET SDK biedt ook ondersteuning voor dynamisch getypeerde documenten met behulp van de `Document`-klasse, die een sleutel/waarde-toewijst aan veldnamen naar waarden.</span><span class="sxs-lookup"><span data-stu-id="4dc47-196">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="4dc47-197">Dit is handig in situaties waar u het schema van de index op het moment van ontwerp nog niet weet of wanneer het niet handig zou zijn om verbinding te maken met specifieke modelklassen</span><span class="sxs-lookup"><span data-stu-id="4dc47-197">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="4dc47-198">Alle methoden in de SDK die werken met documenten hebben overloads die met werken de `Document`-klasse, evenals sterk getypeerde overloads die een generiek typeparameter moeten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4dc47-198">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="4dc47-199">Alleen de laatste worden in de voorbeeldcode in dit artikel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4dc47-199">Only the latter are used in the sample code in this article.</span></span>
> 
> 

<span data-ttu-id="4dc47-200">**Waarom u nullable-gegevenstypen moet gebruiken**</span><span class="sxs-lookup"><span data-stu-id="4dc47-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="4dc47-201">Bij het ontwerpen van uw eigen modelklassen die u wilt toewijzen aan een Azure Search-index raden we u aan om eigenschappen van waardentypen `bool` en `int` in te stellen op null-waarden (bijvoorbeeld `bool?` in plaats van `bool`).</span><span class="sxs-lookup"><span data-stu-id="4dc47-201">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="4dc47-202">Als u een niet-nullbare eigenschap gebruikt, moet u **garanderen** dat de documenten in de index geen null-waarde voor het betreffende veld bevatten.</span><span class="sxs-lookup"><span data-stu-id="4dc47-202">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="4dc47-203">Noch de SDK noch de Azure Search-service helpt u om dit af te dwingen.</span><span class="sxs-lookup"><span data-stu-id="4dc47-203">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="4dc47-204">Dit is niet alleen een hypothetische probleem: Stel een scenario voor waarin u een nieuw veld toevoegt aan een bestaande index van het type `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="4dc47-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="4dc47-205">Na het bijwerken van de indexdefinitie hebben alle documenten een null-waarde voor het nieuwe veld (omdat alle typen null in Azure Search zijn).</span><span class="sxs-lookup"><span data-stu-id="4dc47-205">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="4dc47-206">Als u vervolgens een modelklasse met een niet-nullbare `int`-eigenschap voor dat veld gebruikt, ontvangt u een `JsonSerializationException` zoals deze bij het ophalen van documenten:</span><span class="sxs-lookup"><span data-stu-id="4dc47-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="4dc47-207">Daarom wordt u aangeraden nullbare typen in uw modelklassen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4dc47-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dc47-208">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4dc47-208">Next steps</span></span>
<span data-ttu-id="4dc47-209">Na het vullen van uw Azure Search-index bent u gereed om query's uit te geven om te zoeken naar documenten.</span><span class="sxs-lookup"><span data-stu-id="4dc47-209">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="4dc47-210">Zie [Een query uitvoeren in uw Azure-zoekindex](search-query-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4dc47-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

