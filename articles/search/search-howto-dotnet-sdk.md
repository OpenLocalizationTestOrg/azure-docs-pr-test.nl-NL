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
# <a name="how-toouse-azure-search-from-a-net-application"></a><span data-ttu-id="eb9e7-103">Hoe toouse Azure zoeken vanuit een .NET-toepassing</span><span class="sxs-lookup"><span data-stu-id="eb9e7-103">How toouse Azure Search from a .NET Application</span></span>
<span data-ttu-id="eb9e7-104">In dit artikel wordt een overzicht tooget u snel Hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-104">This article is a walkthrough tooget you up and running with hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="eb9e7-105">U kunt Hallo .NET SDK tooimplement een uitgebreide ervaring van uw toepassing met behulp van Azure Search zoeken.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-105">You can use hello .NET SDK tooimplement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-hello-azure-search-sdk"></a><span data-ttu-id="eb9e7-106">Wat is er in hello Azure Search SDK</span><span class="sxs-lookup"><span data-stu-id="eb9e7-106">What's in hello Azure Search SDK</span></span>
<span data-ttu-id="eb9e7-107">Hallo SDK bestaat uit een clientbibliotheek `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-107">hello SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="eb9e7-108">Deze maakt u toomanage uw indexen, gegevensbronnen en indexeerfuncties, evenals uploaden documenten beheren en uitvoeren van query's zonder te hoeven toodeal met details op Hallo van HTTP- en JSON.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-108">It enables you toomanage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having toodeal with hello details of HTTP and JSON.</span></span>

<span data-ttu-id="eb9e7-109">Hallo-clientbibliotheek definieert klassen als `Index`, `Field`, en `Document`, evenals bewerkingen, zoals `Indexes.Create` en `Documents.Search` op Hallo `SearchServiceClient` en `SearchIndexClient` klassen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-109">hello client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on hello `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="eb9e7-110">Deze klassen zijn ingedeeld in Hallo volgende naamruimten:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-110">These classes are organized into hello following namespaces:</span></span>

* [<span data-ttu-id="eb9e7-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="eb9e7-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="eb9e7-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="eb9e7-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="eb9e7-113">de huidige versie Hallo van hello Azure Search .NET SDK is nu algemeen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-113">hello current version of hello Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="eb9e7-114">Als u tooprovide feedback wilt voor ons tooincorporate in de volgende versie hello, gaat u naar onze [feedbackpagina](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-114">If you would like tooprovide feedback for us tooincorporate in hello next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="eb9e7-115">Hallo .NET SDK versie ondersteunt `2016-09-01` Hallo [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-115">hello .NET SDK supports version `2016-09-01` of hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="eb9e7-116">Deze versie biedt nu ondersteuning voor aangepaste analyzers en ondersteuning van Azure-Blob en Azure Table-indexeerfunctie.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="eb9e7-117">Preview-functies die zijn *niet* deel uitmaken van deze versie, zoals ondersteuning voor het indexeren van JSON en CSV-bestanden bevinden zich in [preview](search-api-2015-02-28-preview.md) en beschikbaar via Hallo oudere [2.0-preview-versie van Hallo .NET SDK ](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via hello older [2.0-preview version of hello .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="eb9e7-118">Deze SDK biedt geen ondersteuning voor [beheerbewerkingen](https://docs.microsoft.com/rest/api/searchmanagement/) zoals maken en schalen van de Search-services en API-sleutels beheren.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="eb9e7-119">Als u toomanage uw zoeken in resources van een .NET-toepassing moet, kunt u Hallo [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-119">If you need toomanage your Search resources from a .NET application, you can use hello [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a><span data-ttu-id="eb9e7-120">Bijwerken van de meest recente versie toohello van Hallo SDK</span><span class="sxs-lookup"><span data-stu-id="eb9e7-120">Upgrading toohello latest version of hello SDK</span></span>
<span data-ttu-id="eb9e7-121">Als u al een oudere versie van hello Azure Search .NET SDK en u tooupgrade toohello nieuwe algemeen beschikbaar versie dat wilt, [in dit artikel](search-dotnet-sdk-migration.md) wordt uitgelegd hoe.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-121">If you're already using an older version of hello Azure Search .NET SDK and you'd like tooupgrade toohello new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-hello-sdk"></a><span data-ttu-id="eb9e7-122">Vereisten voor Hallo SDK</span><span class="sxs-lookup"><span data-stu-id="eb9e7-122">Requirements for hello SDK</span></span>
1. <span data-ttu-id="eb9e7-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="eb9e7-124">Uw eigen Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-124">Your own Azure Search service.</span></span> <span data-ttu-id="eb9e7-125">In de volgorde toouse Hallo SDK moet u Hallo-naam van uw service en een of meer API-sleutels.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-125">In order toouse hello SDK, you will need hello name of your service and one or more API keys.</span></span> <span data-ttu-id="eb9e7-126">[Maken van een service in de portal Hallo](search-create-service-portal.md) helpt u bij deze stappen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-126">[Create a service in hello portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="eb9e7-127">Hello Azure Search .NET SDK downloaden [NuGet-pakket](http://www.nuget.org/packages/Microsoft.Azure.Search) met behulp van 'NuGet-pakketten beheren' in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-127">Download hello Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="eb9e7-128">Zoeken Hallo pakketnaam `Microsoft.Azure.Search` op NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-128">Just search for hello package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="eb9e7-129">Hello Azure Search .NET SDK biedt ondersteuning voor toepassingen die gericht is op Hallo .NET Framework 4.6 en .NET Core.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-129">hello Azure Search .NET SDK supports applications targeting hello .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="eb9e7-130">Belangrijkste scenario 's</span><span class="sxs-lookup"><span data-stu-id="eb9e7-130">Core scenarios</span></span>
<span data-ttu-id="eb9e7-131">Er zijn verschillende dingen die u moet toodo in uw zoektoepassing.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-131">There are several things you'll need toodo in your search application.</span></span> <span data-ttu-id="eb9e7-132">In deze zelfstudie aan bod deze belangrijkste scenario's:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="eb9e7-133">Een index te maken</span><span class="sxs-lookup"><span data-stu-id="eb9e7-133">Creating an index</span></span>
* <span data-ttu-id="eb9e7-134">Hallo-index met de documenten in te vullen</span><span class="sxs-lookup"><span data-stu-id="eb9e7-134">Populating hello index with documents</span></span>
* <span data-ttu-id="eb9e7-135">Zoeken naar documenten met behulp van de zoekopdracht in volledige tekst en filters</span><span class="sxs-lookup"><span data-stu-id="eb9e7-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="eb9e7-136">Hallo voorbeeldcode die volgt illustreert elk van deze.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-136">hello sample code that follows illustrates each of these.</span></span> <span data-ttu-id="eb9e7-137">U kunt gratis toouse Hallo codefragmenten in uw eigen toepassing.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-137">Feel free toouse hello code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="eb9e7-138">Overzicht</span><span class="sxs-lookup"><span data-stu-id="eb9e7-138">Overview</span></span>
<span data-ttu-id="eb9e7-139">Hallo voorbeeldtoepassing we je worden verkennen maakt u een nieuwe index met de naam "hotels" gevuld met een paar documenten en vervolgens bepaalde zoekquery's worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-139">hello sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="eb9e7-140">Hier volgt Hallo belangrijkste programma, met algemene stroom Hallo:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-140">Here is hello main program, showing hello overall flow:</span></span>

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
> <span data-ttu-id="eb9e7-141">U vindt de volledige broncode Hallo van Hallo-voorbeeldtoepassing die is gebruikt in deze doorloop op [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-141">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="eb9e7-142">We doorlopen deze stap voor stap.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-142">We'll walk through this step by step.</span></span> <span data-ttu-id="eb9e7-143">Eerst moet u toocreate een nieuwe `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-143">First we need toocreate a new `SearchServiceClient`.</span></span> <span data-ttu-id="eb9e7-144">Dit object maakt toomanage indexen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-144">This object allows you toomanage indexes.</span></span> <span data-ttu-id="eb9e7-145">In de volgorde tooconstruct een moet u tooprovide de naam van uw Azure Search-service, evenals een beheer-API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-145">In order tooconstruct one, you need tooprovide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="eb9e7-146">U kunt deze informatie invoeren in Hallo `appsettings.json` bestand Hallo [voorbeeldtoepassing](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-146">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="eb9e7-147">Als u een onjuist sleutel (bijvoorbeeld een query waarin een beheersleutel vereist is), Hallo `SearchServiceClient` genereert een `CloudException` Hallo fout bericht 'Verboden' Hello eerste keer dat u een bewerkingsmethode aanroepen, zoals `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-147">If you provide an incorrect key (for example, a query key where an admin key was required), hello `SearchServiceClient` will throw a `CloudException` with hello error message "Forbidden" hello first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="eb9e7-148">Als dit tooyou gebeurt, Controleer onze API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-148">If this happens tooyou, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="eb9e7-149">Hallo aanroepen volgende paar regels methoden toocreate index met de naam "hotels", eerst verwijderen als deze al bestaat.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-149">hello next few lines call methods toocreate an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="eb9e7-150">We doorlopen die deze methoden enigszins hoger.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="eb9e7-151">Hallo-index moet vervolgens toobe ingevuld.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-151">Next, hello index needs toobe populated.</span></span> <span data-ttu-id="eb9e7-152">toodo, moeten we een `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-152">toodo this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="eb9e7-153">Er zijn twee manieren tooobtain een: door deze samen te stellen of door het aanroepen van `Indexes.GetClient` op Hallo `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-153">There are two ways tooobtain one: by constructing it, or by calling `Indexes.GetClient` on hello `SearchServiceClient`.</span></span> <span data-ttu-id="eb9e7-154">We Hallo laatstgenoemde gebruiken voor het gemak.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-154">We use hello latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="eb9e7-155">In een standaardzoektoepassing wordt het beheer van de index en de invulling daarvan afgehandeld door een afzonderlijk onderdeel van de zoekquery’s.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="eb9e7-156">`Indexes.GetClient`is handig voor het invullen van een index, omdat u problemen van het bieden van een andere Hallo `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-156">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="eb9e7-157">Dit wordt uitgevoerd door Hallo beheersleutel doorgeeft die gebruikte toocreate u Hallo `SearchServiceClient` toohello nieuwe `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-157">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="eb9e7-158">Hallo deel van uw toepassing waarmee query's uitvoert, het is echter beter toocreate hello `SearchIndexClient` rechtstreeks zodat u in een querysleutel in plaats van een administratorsleutel doorgeven kunt.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-158">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="eb9e7-159">Dit is consistent met de Hallo principe van minimale bevoegdheden en helpt uw toepassing veiliger toomake.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-159">This is consistent with hello principle of least privilege and will help toomake your application more secure.</span></span> <span data-ttu-id="eb9e7-160">U vindt meer informatie over administratorsleutels en querysleutels [hier](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="eb9e7-161">Nu dat we hebben een `SearchIndexClient`, we Hallo index kunt vullen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-161">Now that we have a `SearchIndexClient`, we can populate hello index.</span></span> <span data-ttu-id="eb9e7-162">Dit wordt gedaan door een andere methode die u kunt later zien.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="eb9e7-163">Ten slotte we enkele zoekopdrachten uitvoeren en Hallo resultaten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-163">Finally, we execute a few search queries and display hello results.</span></span> <span data-ttu-id="eb9e7-164">Nu we gebruiken een ander `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="eb9e7-165">Laten we bekijkt hello `RunQueries` methode later.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-165">We will take a closer look at hello `RunQueries` method later.</span></span> <span data-ttu-id="eb9e7-166">Hier volgt Hallo code toocreate Hallo nieuwe `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-166">Here is hello code toocreate hello new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="eb9e7-167">Nu we een querysleutel gebruiken aangezien er geen schrijftoegang toohello index hoeft.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-167">This time we use a query key since we do not need write access toohello index.</span></span> <span data-ttu-id="eb9e7-168">U kunt deze informatie invoeren in Hallo `appsettings.json` bestand Hallo [voorbeeldtoepassing](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-168">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="eb9e7-169">Als u deze toepassing met een geldige servicenaam en API-sleutels uitvoert, er Hallo uitvoer als volgt:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-169">If you run this application with a valid service name and API keys, hello output should look like this:</span></span>

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

<span data-ttu-id="eb9e7-170">de volledige broncode Hallo van de toepassing hello wordt op Hallo einde van dit artikel aangeboden.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-170">hello full source code of hello application is provided at hello end of this article.</span></span>

<span data-ttu-id="eb9e7-171">We zullen Haal vervolgens bekijkt hello methoden aangeroepen door `Main`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-171">Next, we will take a closer look at each of hello methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="eb9e7-172">Een index te maken</span><span class="sxs-lookup"><span data-stu-id="eb9e7-172">Creating an index</span></span>
<span data-ttu-id="eb9e7-173">Na het maken van een `SearchServiceClient`, Hallo volgende dat `Main` biedt is delete Hallo "hotels" index als deze al bestaat.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-173">After creating a `SearchServiceClient`, hello next thing `Main` does is delete hello "hotels" index if it already exists.</span></span> <span data-ttu-id="eb9e7-174">Dat is gebeurd door Hallo methode te volgen:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-174">That is done by hello following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="eb9e7-175">Deze methode gebruikt Hallo gegeven `SearchServiceClient` toocheck als Hallo index bestaat, en zo ja, verwijderen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-175">This method uses hello given `SearchServiceClient` toocheck if hello index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9e7-176">Hallo voorbeeldcode in dit artikel gebruikt synchrone methoden Hallo Hallo Azure Search .NET SDK voor eenvoud.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-176">hello example code in this article uses hello synchronous methods of hello Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="eb9e7-177">Aangeraden Hallo asynchrone methoden te gebruiken in uw eigen toepassingen tookeep ze schaalbaar en responsief.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-177">We recommend that you use hello asynchronous methods in your own applications tookeep them scalable and responsive.</span></span> <span data-ttu-id="eb9e7-178">Bijvoorbeeld, in de Hallo methode boven gebruiken `ExistsAsync` en `DeleteAsync` in plaats van `Exists` en `Delete`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-178">For example, in hello method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="eb9e7-179">Vervolgens `Main` maakt een nieuwe index "hotels" door deze methode aanroept:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="eb9e7-180">Deze methode maakt u een nieuwe `Index` object met een lijst met `Field` objecten die Hallo-schema van de nieuwe Hallo-index definieert.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-180">This method creates a new `Index` object with a list of `Field` objects that defines hello schema of hello new index.</span></span> <span data-ttu-id="eb9e7-181">Elk veld heeft een naam, gegevenstype en verschillende kenmerken die het zoekgedrag definiëren.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="eb9e7-182">Hallo `FieldBuilder` reflectie toocreate een lijst met klasse gebruikt `Field` objecten voor index vindt van Hallo Hallo openbare eigenschappen en kenmerken van Hallo gegeven `Hotel` modelklasse.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-182">hello `FieldBuilder` class uses reflection toocreate a list of `Field` objects for hello index by examining hello public properties and attributes of hello given `Hotel` model class.</span></span> <span data-ttu-id="eb9e7-183">We gaan die nader bekeken Hallo `Hotel` klasse later op.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-183">We'll take a closer look at hello `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9e7-184">U kunt altijd Hallo lijst maken met `Field` objecten rechtstreeks in plaats van `FieldBuilder` indien nodig.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-184">You can always create hello list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="eb9e7-185">Bijvoorbeeld, kunt u niet een modelklasse toouse of moet u een bestaande modelklasse die u niet toomodify wilt door toe te voegen kenmerken toouse.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-185">For example, you may not want toouse a model class or you may need toouse an existing model class that you don't want toomodify by adding attributes.</span></span>
>
> 

<span data-ttu-id="eb9e7-186">Bovendien toofields, u kunt ook toevoegen scoreprofiel profielen, suggestiefunctie of CORS opties toohello Index (deze weggelaten van Hallo voorbeeld als beknopt alternatief bevat).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-186">In addition toofields, you can also add scoring profiles, suggesters, or CORS options toohello Index (these are omitted from hello sample for brevity).</span></span> <span data-ttu-id="eb9e7-187">U vindt meer informatie over Hallo indexobject en de samenstellende delen in Hallo [SDK-naslaginformatie](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), evenals als in Hallo [Azure Search REST API-verwijzing](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-187">You can find more information about hello Index object and its constituent parts in hello [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-hello-index"></a><span data-ttu-id="eb9e7-188">Hallo-index te vullen</span><span class="sxs-lookup"><span data-stu-id="eb9e7-188">Populating hello index</span></span>
<span data-ttu-id="eb9e7-189">de volgende stap Hallo in `Main` toopopulate Hallo gemaakte index is.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-189">hello next step in `Main` is toopopulate hello newly-created index.</span></span> <span data-ttu-id="eb9e7-190">Dit doet u in de volgende methode Hallo:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-190">This is done in hello following method:</span></span>

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

<span data-ttu-id="eb9e7-191">Deze methode heeft vier onderdelen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-191">This method has four parts.</span></span> <span data-ttu-id="eb9e7-192">Hallo maakt eerst een matrix van `Hotel` objecten die als onze invoergegevens tooupload toohello index fungeert.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-192">hello first creates an array of `Hotel` objects that will serve as our input data tooupload toohello index.</span></span> <span data-ttu-id="eb9e7-193">Deze gegevens zijn vastgelegd voor eenvoud.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="eb9e7-194">In uw eigen toepassing, wordt uw gegevens waarschijnlijk afkomstig zijn van een externe gegevensbron, zoals een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="eb9e7-195">het tweede gedeelte Hallo maakt een `IndexBatch` met Hallo documenten.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-195">hello second part creates an `IndexBatch` containing hello documents.</span></span> <span data-ttu-id="eb9e7-196">Geef van gewenste tooapply toohello batch tijdens Hallo, in dit geval door het aanroepen maken van Hallo-bewerking `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-196">You specify hello operation you want tooapply toohello batch at hello time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="eb9e7-197">Hallo batch is vervolgens geüploade toohello Azure Search indexeren met Hallo `Documents.Index` methode.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-197">hello batch is then uploaded toohello Azure Search index by hello `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9e7-198">In dit voorbeeld zijn er alleen documenten te uploaden.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="eb9e7-199">Indien u toomerge wijzigingen in bestaande documenten of verwijderen wenste, kunt u batches maken door het aanroepen van `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, of `IndexBatch.Delete` in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-199">If you wanted toomerge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="eb9e7-200">Ook kunt u verschillende bewerkingen in één batch elkaar door aan te roepen `IndexBatch.New`, wat een verzameling van duurt `IndexAction` objecten, die elk een bepaalde bewerking voor een document wordt Azure Search tooperform uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search tooperform a particular operation on a document.</span></span> <span data-ttu-id="eb9e7-201">U kunt elk maken `IndexAction` met een eigen bewerking door het aanroepen van de bijbehorende methode Hallo zoals `IndexAction.Merge`, `IndexAction.Upload`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-201">You can create each `IndexAction` with its own operation by calling hello corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="eb9e7-202">Hallo derde deel van deze methode is een blok catch die verantwoordelijk is voor een belangrijke foutaanvraag voor indexering.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-202">hello third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="eb9e7-203">Als uw Azure Search-service geen tooindex aantal Hallo documenten in batch Hallo, een `IndexBatchException` verstuurd door `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-203">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="eb9e7-204">Dit kan gebeuren als u documenten indexeert terwijl uw service zwaar wordt belast.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="eb9e7-205">**Wij raden u aan deze aanvraag expliciet in uw code te behandelen.**</span><span class="sxs-lookup"><span data-stu-id="eb9e7-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="eb9e7-206">U kunt vertraging en probeer het vervolgens opnieuw indexeren Hallo-documenten die niet of u kunt zich aanmelden en doorgaan zoals Hallo voorbeeld, of kunt u iets anders, afhankelijk van de gegevensvereisten consistentie van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-206">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9e7-207">U kunt Hallo `FindFailedActionsToRetry` methode tooconstruct een nieuwe batch met Hallo alleen acties die niet in een eerdere aanroep te`Index`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-207">You can use hello `FindFailedActionsToRetry` method tooconstruct a new batch containing only hello actions that failed in a previous call too`Index`.</span></span> <span data-ttu-id="eb9e7-208">Hallo-methode wordt beschreven [hier](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) en er is een beschrijving van hoe tooproperly gebruiken [op StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-208">hello method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how tooproperly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="eb9e7-209">Ten slotte Hallo `UploadDocuments` methode twee seconden vertraagd.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-209">Finally, hello `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="eb9e7-210">Het indexeren verloopt asynchroon op in uw Azure Search-service, zodat het Hallo-voorbeeldtoepassing moet toowait een korte tijd tooensure dat Hallo documenten beschikbaar voor zoeken zijn.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-210">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="eb9e7-211">Dergelijke vertragingen zijn doorgaans alleen nodig is demo’s, testen en voorbeeldtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="eb9e7-212">Hoe documenten worden verwerkt door Hallo .NET SDK</span><span class="sxs-lookup"><span data-stu-id="eb9e7-212">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="eb9e7-213">U vraagt zich misschien af hoe hello Azure Search .NET SDK is kunnen tooupload exemplaren van een gebruiker gedefinieerde klasse zoals `Hotel` toohello index.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-213">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="eb9e7-214">toohelp deze vraag te beantwoorden, bekijken we Hallo `Hotel` klasse:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-214">toohelp answer that question, let's look at hello `Hotel` class:</span></span>

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

<span data-ttu-id="eb9e7-215">Hallo eerst te beginnen toonotice is dat elke openbare eigenschap van `Hotel` overeenkomt met tooa veld in de indexdefinitie hello, maar met een cruciaal verschil: Hallo-naam van elk veld begint met een kleine letter ("kamelen"), terwijl Hallo-naam van elke bevolking de eigenschap van `Hotel` begint met een hoofdletter ("Pascal geval').</span><span class="sxs-lookup"><span data-stu-id="eb9e7-215">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="eb9e7-216">Dit is een veelvoorkomend scenario in .NET-toepassingen die gegevens koppelen waarbij Hallo doelschema buiten Hallo beheer van de ontwikkelaar van de toepassing hello is.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-216">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="eb9e7-217">In plaats van tooviolate Hallo .NET-naamgevingsregels door het maken van de eigenschap namen kamelen, kunt u zien Hallo SDK toomap Hallo eigenschap namen toocamel case automatisch met Hallo `[SerializePropertyNamesAsCamelCase]` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-217">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9e7-218">Hello Azure Search .NET SDK maakt gebruik van Hallo [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) bibliotheek tooserialize en deserialiseren van uw aangepaste model objecten tooand van JSON.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-218">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="eb9e7-219">U kunt deze serialisatie indien nodig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="eb9e7-220">Zie voor meer informatie [aangepaste serialisatie met JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="eb9e7-221">Hallo tweede ding toonotice zijn Hallo kenmerken zoals `IsFilterable`, `IsSearchable`, `Key`, en `Analyzer` dat elke openbare eigenschap opmaken.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-221">hello second thing toonotice are hello attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="eb9e7-222">Deze kenmerken toewijzen rechtstreeks toohello [overeenkomende kenmerken van hello Azure Search-index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-222">These attributes map directly toohello [corresponding attributes of hello Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="eb9e7-223">Hallo `FieldBuilder` klasse gebruikt deze tooconstruct velddefinities voor Hallo-index.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-223">hello `FieldBuilder` class uses these tooconstruct field definitions for hello index.</span></span>

<span data-ttu-id="eb9e7-224">Hallo derde wat ook belangrijk is Hallo `Hotel` klasse, zijn de gegevenstypen Hallo van Hallo openbare eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-224">hello third important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="eb9e7-225">Hallo .NET-typen van deze eigenschappen worden toegewezen tootheir gelijkwaardige veldtypen in Hallo indexdefinitie.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-225">hello .NET types of  these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="eb9e7-226">Bijvoorbeeld, Hallo `Category` tekenreekseigenschap toegewezen toohello `category` veld van het type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-226">For example, hello `Category` string property maps toohello `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="eb9e7-227">Er zijn vergelijkbare type toewijzingen tussen `bool?` en `Edm.Boolean`, `DateTimeOffset?` en `Edm.DateTimeOffset`, enz. Hallo specifieke regels voor de toewijzing van Hallo type zijn gedocumenteerd in Hallo `Documents.Get` methode in Hallo [Azure Search .NET SDK verwijzing](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="eb9e7-228">Hallo `FieldBuilder` klasse zorgt voor deze toewijzing is voor u, maar kan nog steeds handig toounderstand geval u eventuele problemen met de serialisatie tootroubleshoot nodig.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-228">hello `FieldBuilder` class takes care of this mapping for you, but it can still be helpful toounderstand in case you need tootroubleshoot any serialization issues.</span></span>

<span data-ttu-id="eb9e7-229">Deze mogelijkheid toouse uw eigen klassen als documenten werkt beide kanten; U kunt ook zoekresultaten ophalen en Hallo SDK automatisch deserialiseert tooa type van uw keuze, zoals we in de volgende sectie Hallo ziet.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-229">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as we will see in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9e7-230">Hello Azure Search .NET SDK biedt ook ondersteuning voor dynamisch getypeerde documenten met behulp van Hallo `Document` klasse, die een sleutel/waarde-aan veldwaarden namen toofield toewijst.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-230">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="eb9e7-231">Dit is nuttig in scenario's, indien u niet weet Hallo Indexeer schema op het moment van ontwerp of dat het onhandig toobind toospecific modelklassen normaal zou zijn.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-231">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="eb9e7-232">Alle Hallo methoden in Hallo SDK die met documenten werken hebben overloads die met Hallo werken `Document` klasse, evenals sterk getypeerde overloads die een generiek typeparameter moeten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-232">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="eb9e7-233">Alleen laatste hello worden gebruikt in de voorbeeldcode Hallo in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-233">Only hello latter are used in hello sample code in this tutorial.</span></span> <span data-ttu-id="eb9e7-234">Hallo `Document` klasse neemt over van `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-234">hello `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="eb9e7-235">U vindt andere details [hier](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="eb9e7-236">**Waarom u nullable-gegevenstypen moet gebruiken**</span><span class="sxs-lookup"><span data-stu-id="eb9e7-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="eb9e7-237">Bij het ontwerpen van uw eigen model klassen toomap tooan Azure Search-index we raden u aan om eigenschappen van waardentypen zoals `bool` en `int` toobe null-waarden bevatten (bijvoorbeeld `bool?` in plaats van `bool`).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-237">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="eb9e7-238">Als u een niet-nullbare eigenschap gebruikt, hebt u te**garanderen** dat de documenten in uw index geen null-waarde voor het betreffende veld Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-238">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="eb9e7-239">Hallo SDK noch hello Azure Search-service kunt u tooenforce dit.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-239">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="eb9e7-240">Dit is niet alleen een hypothetische probleem: Stel een scenario waarin het toevoegen van een nieuw veld tooan bestaande index van het type `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="eb9e7-241">Na het bijwerken van de indexdefinitie hello, moeten alle documenten een null-waarde voor het nieuwe veld (omdat alle typen null in Azure Search).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-241">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="eb9e7-242">Als u vervolgens een modelklasse met een niet-nullbare `int` eigenschap voor dat veld gebruikt, ontvangt u een `JsonSerializationException` zoals deze bij het tooretrieve documenten:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="eb9e7-243">Daarom wordt u aangeraden nullbare typen in uw modelklassen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="eb9e7-244">Aangepaste met JSON.NET-serialisatie</span><span class="sxs-lookup"><span data-stu-id="eb9e7-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="eb9e7-245">Hallo SDK maakt gebruik van JSON.NET voor het serialiseren en deserialiseren van documenten.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-245">hello SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="eb9e7-246">U kunt aanpassen serialisatie en deserialisatie indien nodig door het definiëren van uw eigen `JsonConverter` of `IContractResolver` (Zie Hallo [JSON.NET documentatie](http://www.newtonsoft.com/json/help/html/Introduction.htm) voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="eb9e7-247">Dit kan nuttig zijn wanneer u een bestaande modelklasse tooadapt van uw toepassing voor gebruik met Azure Search en andere meer geavanceerde scenario's wilt.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-247">This can be useful when you want tooadapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="eb9e7-248">Met aangepaste serialisatie kunt u bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="eb9e7-249">Opnemen of uitsluiten van bepaalde eigenschappen van uw modelklasse als documentvelden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="eb9e7-250">Koppeling tussen de namen van eigenschappen in uw code en veldnamen in uw index.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="eb9e7-251">Aangepaste kenmerken die kunnen worden gebruikt voor de toewijzing van eigenschappen toodocument velden maken.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-251">Create custom attributes that can be used for mapping properties toodocument fields.</span></span>

<span data-ttu-id="eb9e7-252">Hier vindt u voorbeelden van de implementatie van aangepaste serialisatie in Hallo-controles voor hello Azure Search .NET SDK op GitHub.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-252">You can find examples of implementing custom serialization in hello unit tests for hello Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="eb9e7-253">Is een goed uitgangspunt [deze map](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="eb9e7-254">Deze bevat klassen die worden gebruikt door Hallo aangepaste serialisatie-tests.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-254">It contains classes that are used by hello custom serialization tests.</span></span>

### <a name="searching-for-documents-in-hello-index"></a><span data-ttu-id="eb9e7-255">Zoeken naar documenten in Hallo index</span><span class="sxs-lookup"><span data-stu-id="eb9e7-255">Searching for documents in hello index</span></span>
<span data-ttu-id="eb9e7-256">laatste stap in de voorbeeldtoepassing Hallo Hallo is toosearch voor een aantal documenten in Hallo index.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-256">hello last step in hello sample application is toosearch for some documents in hello index.</span></span> <span data-ttu-id="eb9e7-257">Hallo methode volgende gebeurt:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-257">hello following method does this:</span></span>

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

<span data-ttu-id="eb9e7-258">Telkens wanneer een query wordt uitgevoerd, wordt deze methode maakt eerst een nieuwe `SearchParameters` object.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="eb9e7-259">Dit is de gebruikte toospecify aanvullende opties voor Hallo query zoals sorteren en filteren van, paginering facetten.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-259">This is used toospecify additional options for hello query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="eb9e7-260">Bij deze methode instelt we Hallo `Filter`, `Select`, `OrderBy`, en `Top` eigenschap voor verschillende query's.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-260">In this method, we're setting hello `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="eb9e7-261">Alle Hallo `SearchParameters` eigenschappen zijn gedocumenteerd [hier](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-261">All hello `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="eb9e7-262">de volgende stap Hallo is tooactually Hallo zoekopdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-262">hello next step is tooactually execute hello search query.</span></span> <span data-ttu-id="eb9e7-263">Dit wordt gedaan met behulp van Hallo `Documents.Search` methode.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-263">This is done using hello `Documents.Search` method.</span></span> <span data-ttu-id="eb9e7-264">Voor elke query, geven we Hallo zoeken tekst toouse als tekenreeks (of `"*"` als er geen zoektekst), plus Hallo zoeken parameters eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-264">For each query, we pass hello search text toouse as a string (or `"*"` if there is no search text), plus hello search parameters created earlier.</span></span> <span data-ttu-id="eb9e7-265">We ook opgeven `Hotel` als Hallo typeparameter voor `Documents.Search`, waarin u Hallo SDK toodeserialize documenten in de zoekresultaten Hallo bepaald in objecten van het type `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-265">We also specify `Hotel` as hello type parameter for `Documents.Search`, which tells hello SDK toodeserialize documents in hello search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9e7-266">U vindt meer informatie over de syntaxis Hallo zoekquery expressie [hier](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-266">You can find more information about hello search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="eb9e7-267">Ten slotte na elke query doorlopen met deze methode alle Hallo treffers in zoekresultaten Hallo elke document toohello console afdrukken:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-267">Finally, after each query this method iterates through all hello matches in hello search results, printing each document toohello console:</span></span>

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

<span data-ttu-id="eb9e7-268">U gaat nu een nader bekeken Hallo query's op zijn beurt.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-268">Let's take a closer look at each of hello queries in turn.</span></span> <span data-ttu-id="eb9e7-269">Hier volgt Hallo code tooexecute Hallo eerste query:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-269">Here is hello code tooexecute hello first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="eb9e7-270">In dit geval we zoeken hotels die overeenkomen met de Hallo woord 'budget' en we willen tooget terug alleen Hallo hotel namen, zoals opgegeven door Hallo `Select` parameter.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-270">In this case, we're searching for hotels that match hello word "budget", and we want tooget back only hello hotel names, as specified by hello `Select` parameter.</span></span> <span data-ttu-id="eb9e7-271">Hier volgen Hallo resultaten:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-271">Here are hello results:</span></span>

    Name: Roach Motel

<span data-ttu-id="eb9e7-272">Vervolgens we wilt toofind Hallo hotels met een elke nacht tarief van minder dan €150 en alleen Hallo hotel-ID en een beschrijving geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-272">Next, we want toofind hello hotels with a nightly rate of less than $150, and return only hello hotel ID and description:</span></span>

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

<span data-ttu-id="eb9e7-273">Deze query gebruikt een OData `$filter` expressie, `baseRate lt 150`, toofilter Hallo documenten in Hallo index.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-273">This query uses an OData `$filter` expression, `baseRate lt 150`, toofilter hello documents in hello index.</span></span> <span data-ttu-id="eb9e7-274">U vindt meer informatie over Hallo OData-syntaxis die ondersteuning biedt voor Azure Search [hier](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-274">You can find out more about hello OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="eb9e7-275">Hier volgen Hallo resultaten van Hallo-query:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-275">Here are hello results of hello query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

<span data-ttu-id="eb9e7-276">We willen vervolgens toofind Hallo bovenste twee hotels die onlangs zijn renovated en Hallo hotel naam en de datum van laatste renovatie niet weergeven.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-276">Next, we want toofind hello top two hotels that have been most recently renovated, and show hello hotel name and last renovation date.</span></span> <span data-ttu-id="eb9e7-277">Dit is Hallo code:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-277">Here is hello code:</span></span> 

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

<span data-ttu-id="eb9e7-278">In dit geval opnieuw gebruiken we OData syntaxis toospecify hello `OrderBy` parameter als `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-278">In this case, we again use OData syntax toospecify hello `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="eb9e7-279">We ook ingesteld `Top` too2 tooensure alleen krijgen we Hallo twee bovenste documenten.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-279">We also set `Top` too2 tooensure we only get hello top two documents.</span></span> <span data-ttu-id="eb9e7-280">Net als voorheen kunt we ingesteld `Select` toospecify welke velden moeten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-280">As before, we set `Select` toospecify which fields should be returned.</span></span>

<span data-ttu-id="eb9e7-281">Hier volgen Hallo resultaten:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-281">Here are hello results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="eb9e7-282">Tot slot willen we toofind alle hotels die overeenkomen met Hallo woord 'motel':</span><span class="sxs-lookup"><span data-stu-id="eb9e7-282">Finally, we want toofind all hotels that match hello word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="eb9e7-283">En hier vindt u Hallo resultaten, die alle velden bevatten omdat er geen Hallo opgegeven is `Select` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="eb9e7-283">And here are hello results, which include all fields since we did not specify hello `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="eb9e7-284">Deze stap Hallo zelfstudie is voltooid, maar hier niet stoppen.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-284">This step completes hello tutorial, but don't stop here.</span></span> <span data-ttu-id="eb9e7-285">**Volgende stappen** bevat aanvullende bronnen voor meer informatie over Azure Search.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb9e7-286">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eb9e7-286">Next steps</span></span>
* <span data-ttu-id="eb9e7-287">Hallo-verwijzingen voor Hallo Bladeren [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) en [REST-API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-287">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="eb9e7-288">Uw medeweten via verdiepen [video's en andere voorbeelden en zelfstudies](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="eb9e7-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="eb9e7-289">Bekijk [naamconventies](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn Hallo regels voor het benoemen van verschillende objecten.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello rules for naming various objects.</span></span>
* <span data-ttu-id="eb9e7-290">Bekijk [ondersteunde gegevenstypen](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="eb9e7-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
