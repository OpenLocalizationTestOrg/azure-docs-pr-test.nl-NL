---
title: Het gebruik van Azure Search vanuit een .NET-toepassing | Microsoft Docs
description: Het gebruik van Azure Search vanuit een .NET-toepassing
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
ms.openlocfilehash: 552a7ab193e12d2e72da494166d774e974c85d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-search-from-a-net-application"></a><span data-ttu-id="2d774-103">Het gebruik van Azure Search vanuit een .NET-toepassing</span><span class="sxs-lookup"><span data-stu-id="2d774-103">How to use Azure Search from a .NET Application</span></span>
<span data-ttu-id="2d774-104">In dit artikel is een overzicht krijgen van u actief en werkend met de [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="2d774-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="2d774-105">U kunt de .NET SDK gebruiken voor het implementeren van een uitgebreide zoekervaring in uw toepassing met behulp van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2d774-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-the-azure-search-sdk"></a><span data-ttu-id="2d774-106">Wat is er in de Azure SDK zoeken</span><span class="sxs-lookup"><span data-stu-id="2d774-106">What's in the Azure Search SDK</span></span>
<span data-ttu-id="2d774-107">De SDK bestaat uit een clientbibliotheek `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="2d774-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="2d774-108">Hiermee kunt u voor het beheren van uw indexen, gegevensbronnen en indexeerfuncties, evenals uploaden en documenten beheren en uitvoeren van query's zonder te hoeven te bekommeren om de details van HTTP- en JSON.</span><span class="sxs-lookup"><span data-stu-id="2d774-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span></span>

<span data-ttu-id="2d774-109">De clientbibliotheek definieert klassen als `Index`, `Field`, en `Document`, evenals bewerkingen, zoals `Indexes.Create` en `Documents.Search` op de `SearchServiceClient` en `SearchIndexClient` klassen.</span><span class="sxs-lookup"><span data-stu-id="2d774-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="2d774-110">Deze klassen zijn ingedeeld in de volgende naamruimten:</span><span class="sxs-lookup"><span data-stu-id="2d774-110">These classes are organized into the following namespaces:</span></span>

* [<span data-ttu-id="2d774-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="2d774-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="2d774-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="2d774-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="2d774-113">De huidige versie van de Azure Search .NET SDK is nu algemeen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="2d774-113">The current version of the Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="2d774-114">Als u uw feedback voor ons wilt opnemen in de volgende versie, een bezoek onze [feedbackpagina](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="2d774-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="2d774-115">De .NET SDK versie ondersteunt `2016-09-01` van de [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="2d774-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="2d774-116">Deze versie biedt nu ondersteuning voor aangepaste analyzers en ondersteuning van Azure-Blob en Azure Table-indexeerfunctie.</span><span class="sxs-lookup"><span data-stu-id="2d774-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="2d774-117">Preview-functies die zijn *niet* deel uitmaken van deze versie, zoals ondersteuning voor het indexeren van JSON en CSV-bestanden bevinden zich in [preview](search-api-2015-02-28-preview.md) en beschikbaar via de oudere [2.0-preview-versie van de .NET SDK](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="2d774-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="2d774-118">Deze SDK biedt geen ondersteuning voor [beheerbewerkingen](https://docs.microsoft.com/rest/api/searchmanagement/) zoals maken en schalen van de Search-services en API-sleutels beheren.</span><span class="sxs-lookup"><span data-stu-id="2d774-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="2d774-119">Als u zoeken in resources beheren vanuit een .NET-toepassing wilt, kunt u de [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="2d774-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-to-the-latest-version-of-the-sdk"></a><span data-ttu-id="2d774-120">Upgraden naar de meest recente versie van de SDK</span><span class="sxs-lookup"><span data-stu-id="2d774-120">Upgrading to the latest version of the SDK</span></span>
<span data-ttu-id="2d774-121">Als u al een oudere versie van de Azure Search .NET SDK en u wilt bijwerken naar de nieuwe versie van de algemeen beschikbaar [in dit artikel](search-dotnet-sdk-migration.md) wordt uitgelegd hoe.</span><span class="sxs-lookup"><span data-stu-id="2d774-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-the-sdk"></a><span data-ttu-id="2d774-122">Vereisten voor de SDK</span><span class="sxs-lookup"><span data-stu-id="2d774-122">Requirements for the SDK</span></span>
1. <span data-ttu-id="2d774-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2d774-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="2d774-124">Uw eigen Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="2d774-124">Your own Azure Search service.</span></span> <span data-ttu-id="2d774-125">Als u wilt gebruiken in de SDK, moet u de naam van uw service en een of meer API-sleutels.</span><span class="sxs-lookup"><span data-stu-id="2d774-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span></span> <span data-ttu-id="2d774-126">[Maken van een service in de portal](search-create-service-portal.md) helpt u bij deze stappen.</span><span class="sxs-lookup"><span data-stu-id="2d774-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="2d774-127">Download de Azure Search .NET SDK [NuGet-pakket](http://www.nuget.org/packages/Microsoft.Azure.Search) met behulp van 'NuGet-pakketten beheren' in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d774-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="2d774-128">Naam van het pakket zoeken `Microsoft.Azure.Search` op NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="2d774-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="2d774-129">De Azure Search .NET SDK biedt ondersteuning voor toepassingen die gericht is op de .NET Framework 4.6 en .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2d774-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="2d774-130">Belangrijkste scenario 's</span><span class="sxs-lookup"><span data-stu-id="2d774-130">Core scenarios</span></span>
<span data-ttu-id="2d774-131">Er zijn verschillende dingen die u moet in uw zoektoepassing.</span><span class="sxs-lookup"><span data-stu-id="2d774-131">There are several things you'll need to do in your search application.</span></span> <span data-ttu-id="2d774-132">In deze zelfstudie aan bod deze belangrijkste scenario's:</span><span class="sxs-lookup"><span data-stu-id="2d774-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="2d774-133">Een index te maken</span><span class="sxs-lookup"><span data-stu-id="2d774-133">Creating an index</span></span>
* <span data-ttu-id="2d774-134">De index met documenten in te vullen</span><span class="sxs-lookup"><span data-stu-id="2d774-134">Populating the index with documents</span></span>
* <span data-ttu-id="2d774-135">Zoeken naar documenten met behulp van de zoekopdracht in volledige tekst en filters</span><span class="sxs-lookup"><span data-stu-id="2d774-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="2d774-136">De volgende voorbeeldcode ziet u elk van deze.</span><span class="sxs-lookup"><span data-stu-id="2d774-136">The sample code that follows illustrates each of these.</span></span> <span data-ttu-id="2d774-137">U kunt de codefragmenten gebruiken in uw eigen toepassing.</span><span class="sxs-lookup"><span data-stu-id="2d774-137">Feel free to use the code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="2d774-138">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2d774-138">Overview</span></span>
<span data-ttu-id="2d774-139">De voorbeeldtoepassing we je worden verkennen maakt u een nieuwe index met de naam "hotels" gevuld met een paar documenten en vervolgens bepaalde zoekquery's worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2d774-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="2d774-140">Dit is het belangrijkste programma, de algemene stroom wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="2d774-140">Here is the main program, showing the overall flow:</span></span>

```csharp
// This sample shows how to delete, create, upload documents and query an index
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

    Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="2d774-141">U vindt de volledige broncode van de voorbeeldtoepassing die in deze walkthrough wordt gebruikt, op [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="2d774-141">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="2d774-142">We doorlopen deze stap voor stap.</span><span class="sxs-lookup"><span data-stu-id="2d774-142">We'll walk through this step by step.</span></span> <span data-ttu-id="2d774-143">Eerst moet u een nieuwe `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="2d774-143">First we need to create a new `SearchServiceClient`.</span></span> <span data-ttu-id="2d774-144">Dit object kunt u voor het beheren van indexen.</span><span class="sxs-lookup"><span data-stu-id="2d774-144">This object allows you to manage indexes.</span></span> <span data-ttu-id="2d774-145">U moet een samenstellen, geef de naam van uw Azure Search-service, evenals een beheer-API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="2d774-145">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="2d774-146">U kunt deze informatie invoeren in de `appsettings.json` -bestand van de [voorbeeldtoepassing](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="2d774-146">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="2d774-147">Als u een onjuist sleutel (bijvoorbeeld een query waarin een beheersleutel vereist is), bieden de `SearchServiceClient` genereert een `CloudException` bericht met de fout 'Verboden' de eerste keer dat u de bewerkingsmethode van een, zoals aanroepen `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="2d774-147">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="2d774-148">Als dit gebeurt aan u is, Controleer onze API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="2d774-148">If this happens to you, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="2d774-149">De volgende regels aanroepen methoden voor het maken van een index met de naam "hotels", eerst verwijderen als deze al bestaat.</span><span class="sxs-lookup"><span data-stu-id="2d774-149">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="2d774-150">We doorlopen die deze methoden enigszins hoger.</span><span class="sxs-lookup"><span data-stu-id="2d774-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="2d774-151">De index moet vervolgens worden ingevuld.</span><span class="sxs-lookup"><span data-stu-id="2d774-151">Next, the index needs to be populated.</span></span> <span data-ttu-id="2d774-152">Om dit te doen, moeten we een `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="2d774-152">To do this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="2d774-153">Er zijn twee manieren een ophalen: door deze samen te stellen of door het aanroepen van `Indexes.GetClient` op de `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="2d774-153">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span></span> <span data-ttu-id="2d774-154">We gebruiken deze laatste voor het gemak.</span><span class="sxs-lookup"><span data-stu-id="2d774-154">We use the latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="2d774-155">In een standaardzoektoepassing wordt het beheer van de index en de invulling daarvan afgehandeld door een afzonderlijk onderdeel van de zoekquery’s.</span><span class="sxs-lookup"><span data-stu-id="2d774-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="2d774-156">`Indexes.GetClient` is handig voor het vullen van een index, omdat u geen andere `SearchCredentials` hoeft op te geven.</span><span class="sxs-lookup"><span data-stu-id="2d774-156">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="2d774-157">Dit wordt uitgevoerd door de administratorsleutel die u hebt gebruikt om de `SearchServiceClient` te maken die u wilt doorgeven aan de nieuwe `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="2d774-157">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="2d774-158">In het gedeelte van uw toepassing waarmee u query's uitvoert, is het beter om de `SearchIndexClient` direct te maken, zodat u een querysleutel kunt toepassen in plaats van een administratorsleutel.</span><span class="sxs-lookup"><span data-stu-id="2d774-158">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="2d774-159">Dit is consistent zijn met het principe van minimale bevoegdheden en zorgt ervoor dat uw toepassing beter te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="2d774-159">This is consistent with the principle of least privilege and will help to make your application more secure.</span></span> <span data-ttu-id="2d774-160">U vindt meer informatie over administratorsleutels en querysleutels [hier](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="2d774-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="2d774-161">Nu dat we hebben een `SearchIndexClient`, kan de index vult.</span><span class="sxs-lookup"><span data-stu-id="2d774-161">Now that we have a `SearchIndexClient`, we can populate the index.</span></span> <span data-ttu-id="2d774-162">Dit wordt gedaan door een andere methode die u kunt later zien.</span><span class="sxs-lookup"><span data-stu-id="2d774-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="2d774-163">Ten slotte we enkele zoekopdrachten uitvoeren en de resultaten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="2d774-163">Finally, we execute a few search queries and display the results.</span></span> <span data-ttu-id="2d774-164">Nu we gebruiken een ander `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="2d774-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="2d774-165">We nader bekeken duurt de `RunQueries` methode later.</span><span class="sxs-lookup"><span data-stu-id="2d774-165">We will take a closer look at the `RunQueries` method later.</span></span> <span data-ttu-id="2d774-166">Dit is de code voor het maken van de nieuwe `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="2d774-166">Here is the code to create the new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="2d774-167">Nu we een querysleutel gebruiken aangezien er geen schrijftoegang tot de index hoeft.</span><span class="sxs-lookup"><span data-stu-id="2d774-167">This time we use a query key since we do not need write access to the index.</span></span> <span data-ttu-id="2d774-168">U kunt deze informatie invoeren in de `appsettings.json` -bestand van de [voorbeeldtoepassing](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="2d774-168">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="2d774-169">Als u deze toepassing met een geldige servicenaam en API-sleutels uitvoert, wordt de uitvoer ziet als volgt:</span><span class="sxs-lookup"><span data-stu-id="2d774-169">If you run this application with a valid service name and API keys, the output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents to be indexed...
    
    Search the entire index for the term 'budget' and return only the hotelName field:
    
    Name: Roach Motel
    
    Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river
    
    Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search the entire index for the term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key to end application...

<span data-ttu-id="2d774-170">De volledige broncode van de toepassing wordt verstrekt aan het einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2d774-170">The full source code of the application is provided at the end of this article.</span></span>

<span data-ttu-id="2d774-171">Vervolgens gaat we nader bekeken elk van de methoden aangeroepen door `Main`.</span><span class="sxs-lookup"><span data-stu-id="2d774-171">Next, we will take a closer look at each of the methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="2d774-172">Een index te maken</span><span class="sxs-lookup"><span data-stu-id="2d774-172">Creating an index</span></span>
<span data-ttu-id="2d774-173">Na het maken van een `SearchServiceClient`, het volgende dat `Main` biedt is verwijderd als deze al bestaat de index "hotels".</span><span class="sxs-lookup"><span data-stu-id="2d774-173">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span></span> <span data-ttu-id="2d774-174">Die wordt uitgevoerd door de volgende methode:</span><span class="sxs-lookup"><span data-stu-id="2d774-174">That is done by the following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="2d774-175">Deze methode maakt gebruik van de opgegeven `SearchServiceClient` om te controleren of de index bestaat, en zo ja, verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2d774-175">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="2d774-176">In de voorbeeldcode in dit artikel is voor het gemak gebruikgemaakt van de synchrone methoden van de Azure Search .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2d774-176">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="2d774-177">Het wordt aanbevolen in uw eigen toepassingen asynchrone methoden te gebruiken, zodat de toepassingen schaalbaar zijn en goed reageren.</span><span class="sxs-lookup"><span data-stu-id="2d774-177">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span></span> <span data-ttu-id="2d774-178">Bijvoorbeeld, in de bovenstaande methode kunt u `ExistsAsync` en `DeleteAsync` in plaats van `Exists` en `Delete`.</span><span class="sxs-lookup"><span data-stu-id="2d774-178">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="2d774-179">Vervolgens `Main` maakt een nieuwe index "hotels" door deze methode aanroept:</span><span class="sxs-lookup"><span data-stu-id="2d774-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="2d774-180">Deze methode maakt u een nieuwe `Index` object met een lijst met `Field` objecten die het schema van de nieuwe index definieert.</span><span class="sxs-lookup"><span data-stu-id="2d774-180">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span></span> <span data-ttu-id="2d774-181">Elk veld heeft een naam, gegevenstype en verschillende kenmerken die het zoekgedrag definiëren.</span><span class="sxs-lookup"><span data-stu-id="2d774-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="2d774-182">De `FieldBuilder` klasse reflectie gebruikt voor het maken van een lijst met `Field` objecten voor de index door in de openbare eigenschappen en kenmerken van de opgegeven `Hotel` modelklasse.</span><span class="sxs-lookup"><span data-stu-id="2d774-182">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span></span> <span data-ttu-id="2d774-183">We gaan die nader bekeken de `Hotel` klasse later op.</span><span class="sxs-lookup"><span data-stu-id="2d774-183">We'll take a closer look at the `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="2d774-184">U kunt de lijst met altijd maken `Field` objecten rechtstreeks in plaats van `FieldBuilder` indien nodig.</span><span class="sxs-lookup"><span data-stu-id="2d774-184">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="2d774-185">Bijvoorbeeld, u niet wilt gebruiken een modelklasse of mogelijk moet u een bestaande modelklasse die u niet wijzigen wilt door de kenmerken toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="2d774-185">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span></span>
>
> 

<span data-ttu-id="2d774-186">Naast velden, kunt u scoreprofiel profielen, suggestiefunctie of opties voor CORS ook toevoegen aan de Index (deze worden weggelaten uit het voorbeeld als beknopt alternatief bevat).</span><span class="sxs-lookup"><span data-stu-id="2d774-186">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span></span> <span data-ttu-id="2d774-187">U vindt meer informatie over het object Index en de samenstellende delen in de [SDK-naslaginformatie](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), alsmede in de [Azure Search REST API-verwijzing](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="2d774-187">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-the-index"></a><span data-ttu-id="2d774-188">De index te vullen</span><span class="sxs-lookup"><span data-stu-id="2d774-188">Populating the index</span></span>
<span data-ttu-id="2d774-189">De volgende stap in `Main` voor het vullen van de gemaakte index is.</span><span class="sxs-lookup"><span data-stu-id="2d774-189">The next step in `Main` is to populate the newly-created index.</span></span> <span data-ttu-id="2d774-190">Dit doet u in de volgende methode:</span><span class="sxs-lookup"><span data-stu-id="2d774-190">This is done in the following method:</span></span>

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
            Description = "Close to town hall and the river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

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
}
```

<span data-ttu-id="2d774-191">Deze methode heeft vier onderdelen.</span><span class="sxs-lookup"><span data-stu-id="2d774-191">This method has four parts.</span></span> <span data-ttu-id="2d774-192">De eerste maakt een matrix van `Hotel` objecten die als onze invoergegevens fungeert uploaden naar de index.</span><span class="sxs-lookup"><span data-stu-id="2d774-192">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span></span> <span data-ttu-id="2d774-193">Deze gegevens zijn vastgelegd voor eenvoud.</span><span class="sxs-lookup"><span data-stu-id="2d774-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="2d774-194">In uw eigen toepassing, wordt uw gegevens waarschijnlijk afkomstig zijn van een externe gegevensbron, zoals een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="2d774-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="2d774-195">Het tweede gedeelte maakt een `IndexBatch` met de documenten.</span><span class="sxs-lookup"><span data-stu-id="2d774-195">The second part creates an `IndexBatch` containing the documents.</span></span> <span data-ttu-id="2d774-196">Geef van de bewerking die u toepassen op de batch op het moment dat u dit hebt gemaakt, in dit geval wilt door het aanroepen van `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="2d774-196">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="2d774-197">De batch wordt vervolgens geüpload naar de Azure Search-index met de `Documents.Index` methode.</span><span class="sxs-lookup"><span data-stu-id="2d774-197">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="2d774-198">In dit voorbeeld zijn er alleen documenten te uploaden.</span><span class="sxs-lookup"><span data-stu-id="2d774-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="2d774-199">Als u wijzigingen in bestaande documenten samenvoegen of verwijderen van documenten wilt, kunt u batches maken door het aanroepen van `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, of `IndexBatch.Delete` in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="2d774-199">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="2d774-200">Ook kunt u verschillende bewerkingen in één batch elkaar door aan te roepen `IndexBatch.New`, wat een verzameling van duurt `IndexAction` objecten, die elk Azure Search, een bepaalde bewerking uitvoeren op een document wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="2d774-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span></span> <span data-ttu-id="2d774-201">U kunt elk maken `IndexAction` met een eigen bewerking door het aanroepen van de bijbehorende methode, zoals `IndexAction.Merge`, `IndexAction.Upload`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="2d774-201">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="2d774-202">Het derde deel van deze methode is een blok catch die verantwoordelijk is voor een belangrijke foutaanvraag voor indexering.</span><span class="sxs-lookup"><span data-stu-id="2d774-202">The third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="2d774-203">Als uw Azure Search-service geen index van een aantal documenten in de batch kan maken, wordt een `IndexBatchException` verstuurd door `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="2d774-203">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="2d774-204">Dit kan gebeuren als u documenten indexeert terwijl uw service zwaar wordt belast.</span><span class="sxs-lookup"><span data-stu-id="2d774-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="2d774-205">**Wij raden u aan deze aanvraag expliciet in uw code te behandelen.**</span><span class="sxs-lookup"><span data-stu-id="2d774-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="2d774-206">U kunt de indexering van documenten die niet zijn geïndexeerd vertragen en vervolgens opnieuw uitvoeren, maar u kunt ook een logboek maken en doorgaan zoals in het voorbeeld. U kunt ook een andere bewerking uitvoeren, afhankelijk van de vereisten omtrent de gegevensconsistentie van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2d774-206">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="2d774-207">U kunt de `FindFailedActionsToRetry` methode voor het maken van een nieuwe batch met alleen de acties die niet in een eerdere aanroep voor `Index`.</span><span class="sxs-lookup"><span data-stu-id="2d774-207">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span></span> <span data-ttu-id="2d774-208">De methode wordt beschreven [hier](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) en er is een beschrijving van hoe goed het [op StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="2d774-208">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="2d774-209">Ten slotte de `UploadDocuments` methode twee seconden vertraagd.</span><span class="sxs-lookup"><span data-stu-id="2d774-209">Finally, the `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="2d774-210">Het indexeren verloopt asynchroon in uw Azure Search-service. De voorbeeldtoepassing moet even wachten totdat de documenten beschikbaar zijn voor een zoekbewerking.</span><span class="sxs-lookup"><span data-stu-id="2d774-210">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="2d774-211">Dergelijke vertragingen zijn doorgaans alleen nodig is demo’s, testen en voorbeeldtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="2d774-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="2d774-212">De verwerking van documenten door .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2d774-212">How the .NET SDK handles documents</span></span>
<span data-ttu-id="2d774-213">U vraagt zich misschien af hoe de Azure Search .NET SDK instanties van een door een gebruiker gedefinieerde klasse zoals `Hotel` naar de index kan uploaden.</span><span class="sxs-lookup"><span data-stu-id="2d774-213">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="2d774-214">Als u wilt deze vraag te beantwoorden, bekijken we de `Hotel` klasse:</span><span class="sxs-lookup"><span data-stu-id="2d774-214">To help answer that question, let's look at the `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// The SerializePropertyNamesAsCamelCase attribute is defined in the Azure Search .NET SDK.
// It ensures that Pascal-case property names in the model class are mapped to camel-case
// field names in the index.
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

<span data-ttu-id="2d774-215">Het eerste dat opvalt, is dat elke openbare eigenschap van `Hotel` overeenkomt met een veld in de definitie van de index. Er is echter een cruciaal verschil: de naam van elk veld begint met een kleine letter ("kamelen"), terwijl de naam van elke openbare eigenschap van `Hotel` met een hoofdletter ("Pascal") begint.</span><span class="sxs-lookup"><span data-stu-id="2d774-215">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="2d774-216">Dit is een algemeen scenario in .NET-toepassingen die gegevens koppelen waarbij het doelschema buiten de controle van de ontwikkelaar van de toepassing valt.</span><span class="sxs-lookup"><span data-stu-id="2d774-216">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="2d774-217">In plaats van het schenden van de .NET-naamgevingsregels door een eigenschap met bijvoorbeeld de naam "kamelen" te maken, kunt u instellen dat de SDK de eigenschapsnamen automatisch moet toewijzen aan het `[SerializePropertyNamesAsCamelCase]`-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="2d774-217">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="2d774-218">De Azure Search .NET SDK maakt gebruik van de [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm)-bibliotheek voor het serialiseren en deserialiseren van uw aangepaste modelobjecten naar en van JSON.</span><span class="sxs-lookup"><span data-stu-id="2d774-218">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="2d774-219">U kunt deze serialisatie indien nodig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="2d774-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="2d774-220">Zie voor meer informatie [aangepaste serialisatie met JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="2d774-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="2d774-221">Het tweede dat opvalt zijn de kenmerken, zoals `IsFilterable`, `IsSearchable`, `Key`, en `Analyzer` dat elke openbare eigenschap opmaken.</span><span class="sxs-lookup"><span data-stu-id="2d774-221">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="2d774-222">Deze kenmerken toewijzen rechtstreeks naar de [overeenkomende kenmerken van de Azure Search-index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="2d774-222">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="2d774-223">De `FieldBuilder` klasse gebruikt deze velddefinities voor de index te maken.</span><span class="sxs-lookup"><span data-stu-id="2d774-223">The `FieldBuilder` class uses these to construct field definitions for the index.</span></span>

<span data-ttu-id="2d774-224">Het derde belangrijkste over de `Hotel` klasse, zijn de gegevenstypen van de openbare eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="2d774-224">The third important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="2d774-225">De .NET-typen van deze eigenschappen worden toegewezen aan de gelijkwaardige veldtypen in de definitie van de index.</span><span class="sxs-lookup"><span data-stu-id="2d774-225">The .NET types of  these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="2d774-226">De tekenreekseigenschap `Category` is bijvoorbeeld toegewezen aan het veld `category` van type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="2d774-226">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="2d774-227">Er zijn vergelijkbare type toewijzingen tussen `bool?` en `Edm.Boolean`, `DateTimeOffset?` en `Edm.DateTimeOffset`, enzovoort. De specifieke regels voor de toewijzing van het type worden gedocumenteerd met de methode `Documents.Get` in de [Azure Search .NET SDK-verwijzing](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="2d774-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="2d774-228">De `FieldBuilder` klasse zorgt voor deze toewijzing is voor u, maar kan nog steeds handig om te begrijpen als u problemen ondervindt serialisatie moet zijn.</span><span class="sxs-lookup"><span data-stu-id="2d774-228">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span></span>

<span data-ttu-id="2d774-229">Deze mogelijkheid aan uw eigen klassen te gebruiken als documenten werkt beide kanten; U kunt ook zoekresultaten ophalen en de SDK automatisch deserialiseert naar een type van uw keuze, zoals we in de volgende sectie ziet.</span><span class="sxs-lookup"><span data-stu-id="2d774-229">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="2d774-230">De Azure Search .NET SDK biedt ook ondersteuning voor dynamisch getypeerde documenten met behulp van de `Document`-klasse, die een sleutel/waarde-toewijst aan veldnamen naar waarden.</span><span class="sxs-lookup"><span data-stu-id="2d774-230">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="2d774-231">Dit is handig in situaties waar u het schema van de index op het moment van ontwerp nog niet weet of wanneer het niet handig zou zijn om verbinding te maken met specifieke modelklassen</span><span class="sxs-lookup"><span data-stu-id="2d774-231">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="2d774-232">Alle methoden in de SDK die werken met documenten hebben overloads die met werken de `Document`-klasse, evenals sterk getypeerde overloads die een generiek typeparameter moeten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2d774-232">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="2d774-233">Alleen de laatste worden gebruikt in de voorbeeldcode in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2d774-233">Only the latter are used in the sample code in this tutorial.</span></span> <span data-ttu-id="2d774-234">De `Document` klasse neemt over van `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="2d774-234">The `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="2d774-235">U vindt andere details [hier](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="2d774-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="2d774-236">**Waarom u nullable-gegevenstypen moet gebruiken**</span><span class="sxs-lookup"><span data-stu-id="2d774-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="2d774-237">Bij het ontwerpen van uw eigen modelklassen die u wilt toewijzen aan een Azure Search-index raden we u aan om eigenschappen van waardentypen `bool` en `int` in te stellen op null-waarden (bijvoorbeeld `bool?` in plaats van `bool`).</span><span class="sxs-lookup"><span data-stu-id="2d774-237">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="2d774-238">Als u een niet-nullbare eigenschap gebruikt, moet u **garanderen** dat de documenten in de index geen null-waarde voor het betreffende veld bevatten.</span><span class="sxs-lookup"><span data-stu-id="2d774-238">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="2d774-239">Noch de SDK noch de Azure Search-service helpt u om dit af te dwingen.</span><span class="sxs-lookup"><span data-stu-id="2d774-239">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="2d774-240">Dit is niet alleen een hypothetische probleem: Stel een scenario voor waarin u een nieuw veld toevoegt aan een bestaande index van het type `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="2d774-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="2d774-241">Na het bijwerken van de indexdefinitie hebben alle documenten een null-waarde voor het nieuwe veld (omdat alle typen null in Azure Search zijn).</span><span class="sxs-lookup"><span data-stu-id="2d774-241">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="2d774-242">Als u vervolgens een modelklasse met een niet-nullbare `int`-eigenschap voor dat veld gebruikt, ontvangt u een `JsonSerializationException` zoals deze bij het ophalen van documenten:</span><span class="sxs-lookup"><span data-stu-id="2d774-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="2d774-243">Daarom wordt u aangeraden nullbare typen in uw modelklassen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2d774-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="2d774-244">Aangepaste met JSON.NET-serialisatie</span><span class="sxs-lookup"><span data-stu-id="2d774-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="2d774-245">De SDK gebruikt JSON.NET voor het serialiseren en deserialiseren van documenten.</span><span class="sxs-lookup"><span data-stu-id="2d774-245">The SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="2d774-246">U kunt aanpassen serialisatie en deserialisatie indien nodig door het definiëren van uw eigen `JsonConverter` of `IContractResolver` (Zie de [JSON.NET documentatie](http://www.newtonsoft.com/json/help/html/Introduction.htm) voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="2d774-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="2d774-247">Dit kan nuttig zijn wanneer u wilt aanpassen van een bestaande modelklasse van uw toepassing voor gebruik met Azure Search en andere meer geavanceerde scenario's.</span><span class="sxs-lookup"><span data-stu-id="2d774-247">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="2d774-248">Met aangepaste serialisatie kunt u bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2d774-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="2d774-249">Opnemen of uitsluiten van bepaalde eigenschappen van uw modelklasse als documentvelden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2d774-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="2d774-250">Koppeling tussen de namen van eigenschappen in uw code en veldnamen in uw index.</span><span class="sxs-lookup"><span data-stu-id="2d774-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="2d774-251">Aangepaste kenmerken die kunnen worden gebruikt voor het toewijzen van eigenschappen aan documentvelden maken.</span><span class="sxs-lookup"><span data-stu-id="2d774-251">Create custom attributes that can be used for mapping properties to document fields.</span></span>

<span data-ttu-id="2d774-252">Hier vindt u voorbeelden van de implementatie van aangepaste serialisatie in de eenheidstests voor de Azure Search .NET SDK op GitHub.</span><span class="sxs-lookup"><span data-stu-id="2d774-252">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="2d774-253">Is een goed uitgangspunt [deze map](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span><span class="sxs-lookup"><span data-stu-id="2d774-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="2d774-254">Deze bevat klassen die worden gebruikt door de aangepaste serialisatie-tests.</span><span class="sxs-lookup"><span data-stu-id="2d774-254">It contains classes that are used by the custom serialization tests.</span></span>

### <a name="searching-for-documents-in-the-index"></a><span data-ttu-id="2d774-255">Zoeken naar documenten in de index</span><span class="sxs-lookup"><span data-stu-id="2d774-255">Searching for documents in the index</span></span>
<span data-ttu-id="2d774-256">De laatste stap in de voorbeeldtoepassing is om te zoeken naar een aantal documenten in de index.</span><span class="sxs-lookup"><span data-stu-id="2d774-256">The last step in the sample application is to search for some documents in the index.</span></span> <span data-ttu-id="2d774-257">De volgende methode doet dit:</span><span class="sxs-lookup"><span data-stu-id="2d774-257">The following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
    Console.WriteLine("and return the hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take the top two results, and show only hotelName and ");
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

    Console.WriteLine("Search the entire index for the term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="2d774-258">Telkens wanneer een query wordt uitgevoerd, wordt deze methode maakt eerst een nieuwe `SearchParameters` object.</span><span class="sxs-lookup"><span data-stu-id="2d774-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="2d774-259">Dit wordt gebruikt voor extra opties opgeven voor de query zoals sorteren en filteren van, paginering facetten.</span><span class="sxs-lookup"><span data-stu-id="2d774-259">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="2d774-260">Bij deze methode instelt we de `Filter`, `Select`, `OrderBy`, en `Top` eigenschap voor verschillende query's.</span><span class="sxs-lookup"><span data-stu-id="2d774-260">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="2d774-261">Alle de `SearchParameters` eigenschappen zijn gedocumenteerd [hier](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="2d774-261">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="2d774-262">De volgende stap is het daadwerkelijk uitvoeren van de zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="2d774-262">The next step is to actually execute the search query.</span></span> <span data-ttu-id="2d774-263">Dit wordt gedaan met behulp van de `Documents.Search` methode.</span><span class="sxs-lookup"><span data-stu-id="2d774-263">This is done using the `Documents.Search` method.</span></span> <span data-ttu-id="2d774-264">Voor elke query, geven we de zoektekst te gebruiken als een tekenreeks (of `"*"` als er geen zoektekst), plus de zoekparameters eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2d774-264">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span></span> <span data-ttu-id="2d774-265">We ook opgeven `Hotel` als het typeparameter voor `Documents.Search`, die de SDK voor het deserialiseren van documenten in de zoekresultaten in objecten van het type vertelt `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="2d774-265">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="2d774-266">U vindt meer informatie over de syntaxis van de zoekquery expressie [hier](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="2d774-266">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="2d774-267">Ten slotte na elke query doorlopen met deze methode alle overeenkomsten in de zoekresultaten elk document naar de console afdrukken:</span><span class="sxs-lookup"><span data-stu-id="2d774-267">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span></span>

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

<span data-ttu-id="2d774-268">U gaat nu een nader bekeken elk van de query's op zijn beurt.</span><span class="sxs-lookup"><span data-stu-id="2d774-268">Let's take a closer look at each of the queries in turn.</span></span> <span data-ttu-id="2d774-269">Dit is de code de eerste query uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="2d774-269">Here is the code to execute the first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="2d774-270">In dit geval we zoeken hotels die overeenkomen met het woord 'budget' en willen we weer toegang te krijgen alleen de namen van het hotel, zoals opgegeven door de `Select` parameter.</span><span class="sxs-lookup"><span data-stu-id="2d774-270">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span></span> <span data-ttu-id="2d774-271">Hier volgen de resultaten:</span><span class="sxs-lookup"><span data-stu-id="2d774-271">Here are the results:</span></span>

    Name: Roach Motel

<span data-ttu-id="2d774-272">We willen vervolgens zoekt de hotels met een elke nacht tarief van minder dan €150 en retourneert alleen de hotel-ID en de beschrijving:</span><span class="sxs-lookup"><span data-stu-id="2d774-272">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span></span>

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

<span data-ttu-id="2d774-273">Deze query gebruikt een OData `$filter` expressie, `baseRate lt 150`, voor het filteren van de documenten in de index.</span><span class="sxs-lookup"><span data-stu-id="2d774-273">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span></span> <span data-ttu-id="2d774-274">U vindt meer informatie over de syntaxis van de OData-die ondersteuning biedt voor Azure Search [hier](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="2d774-274">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="2d774-275">Hier volgen de resultaten van de query:</span><span class="sxs-lookup"><span data-stu-id="2d774-275">Here are the results of the query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river

<span data-ttu-id="2d774-276">We willen vervolgens om de eerste twee hotels die onlangs zijn renovated en ziet u de naam van hotel en datum van laatste renovatie.</span><span class="sxs-lookup"><span data-stu-id="2d774-276">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span></span> <span data-ttu-id="2d774-277">Dit is de code:</span><span class="sxs-lookup"><span data-stu-id="2d774-277">Here is the code:</span></span> 

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

<span data-ttu-id="2d774-278">In dit geval we opnieuw OData-syntaxis gebruiken om op te geven de `OrderBy` parameter als `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="2d774-278">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="2d774-279">We ook ingesteld `Top` op 2 om ervoor te zorgen we alleen de twee bovenste documenten ophalen.</span><span class="sxs-lookup"><span data-stu-id="2d774-279">We also set `Top` to 2 to ensure we only get the top two documents.</span></span> <span data-ttu-id="2d774-280">Net als voorheen kunt we ingesteld `Select` om op te geven welke velden moeten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="2d774-280">As before, we set `Select` to specify which fields should be returned.</span></span>

<span data-ttu-id="2d774-281">Hier volgen de resultaten:</span><span class="sxs-lookup"><span data-stu-id="2d774-281">Here are the results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="2d774-282">Ten slotte wordt er gezocht naar alle hotels die overeenkomen met het woord 'motel':</span><span class="sxs-lookup"><span data-stu-id="2d774-282">Finally, we want to find all hotels that match the word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="2d774-283">Hier zijn de resultaten die alle velden bevatten omdat er is geen opgegeven de `Select` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="2d774-283">And here are the results, which include all fields since we did not specify the `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="2d774-284">Deze stap is voltooid voor de zelfstudie, maar hier niet stoppen.</span><span class="sxs-lookup"><span data-stu-id="2d774-284">This step completes the tutorial, but don't stop here.</span></span> <span data-ttu-id="2d774-285">**Volgende stappen** bevat aanvullende bronnen voor meer informatie over Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2d774-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d774-286">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d774-286">Next steps</span></span>
* <span data-ttu-id="2d774-287">Neem de referenties voor de [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) en [REST API](https://docs.microsoft.com/rest/api/searchservice/) door.</span><span class="sxs-lookup"><span data-stu-id="2d774-287">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="2d774-288">Uw medeweten via verdiepen [video's en andere voorbeelden en zelfstudies](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="2d774-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="2d774-289">Bekijk [naamconventies](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) voor meer informatie over de regels voor het benoemen van verschillende objecten.</span><span class="sxs-lookup"><span data-stu-id="2d774-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span></span>
* <span data-ttu-id="2d774-290">Bekijk [ondersteunde gegevenstypen](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2d774-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
