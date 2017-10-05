---
title: Lijst met Azure Storage-resources met de Opslagclientbibliotheek voor C++ | Microsoft Docs
description: Informatie over het gebruik van de aanbieding API's in Microsoft Azure Storage-clientbibliotheek voor C++ opsommen containers, blobs, wachtrijen, tabellen en entiteiten.
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: 9844412739f4f6f95416f81347f0f2eeeca62bea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="06f58-103">Lijst van Azure Storage-resources in C++</span><span class="sxs-lookup"><span data-stu-id="06f58-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="06f58-104">Aanbieding-bewerkingen zijn sleutel naar veel ontwikkelscenario's met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06f58-104">Listing operations are key to many development scenarios with Azure Storage.</span></span> <span data-ttu-id="06f58-105">Dit artikel wordt beschreven hoe u zo efficiënt mogelijk opsommen objecten in Azure Storage met behulp van de aanbieding beschikbaar in de Microsoft Azure Storage-clientbibliotheek voor C++ API's.</span><span class="sxs-lookup"><span data-stu-id="06f58-105">This article describes how to most efficiently enumerate objects in Azure Storage using the listing APIs provided in the Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="06f58-106">Deze handleiding is bedoeld voor de Azure Storage-clientbibliotheek voor C++ versie 2.x die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="06f58-106">This guide targets the Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="06f58-107">De Opslagclientbibliotheek biedt diverse methoden om de lijst of query-objecten in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06f58-107">The Storage Client Library provides a variety of methods to list or query objects in Azure Storage.</span></span> <span data-ttu-id="06f58-108">In dit artikel worden de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="06f58-108">This article addresses the following scenarios:</span></span>

* <span data-ttu-id="06f58-109">Lijst containers in een account</span><span class="sxs-lookup"><span data-stu-id="06f58-109">List containers in an account</span></span>
* <span data-ttu-id="06f58-110">Lijst met blobs in een container of blob virtuele map</span><span class="sxs-lookup"><span data-stu-id="06f58-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="06f58-111">Lijst met wachtrijen in een account</span><span class="sxs-lookup"><span data-stu-id="06f58-111">List queues in an account</span></span>
* <span data-ttu-id="06f58-112">Lijst met tabellen in een account</span><span class="sxs-lookup"><span data-stu-id="06f58-112">List tables in an account</span></span>
* <span data-ttu-id="06f58-113">Query-entiteiten in een tabel</span><span class="sxs-lookup"><span data-stu-id="06f58-113">Query entities in a table</span></span>

<span data-ttu-id="06f58-114">Elk van deze methoden wordt weergegeven als u verschillende overbelastingen voor verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="06f58-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="06f58-115">Asynchrone en synchrone</span><span class="sxs-lookup"><span data-stu-id="06f58-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="06f58-116">Omdat de Opslagclientbibliotheek voor C++ is gebouwd boven de [REST C++-bibliotheek](https://github.com/Microsoft/cpprestsdk), we inherent bieden ondersteuning voor asynchrone bewerkingen met behulp van [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="06f58-116">Because the Storage Client Library for C++ is built on top of the [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="06f58-117">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="06f58-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="06f58-118">Synchrone bewerkingen teruglopen de corresponderende asynchrone bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="06f58-118">Synchronous operations wrap the corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="06f58-119">Als u met meerdere threads toepassingen of services werkt, wordt u aangeraden dat u het async-API's rechtstreeks in plaats van het maken van een thread om aan te roepen de synchronisatie-API's, die aanzienlijk heeft impact op de prestaties van uw.</span><span class="sxs-lookup"><span data-stu-id="06f58-119">If you are working with multiple threading applications or services, we recommend that you use the async APIs directly instead of creating a thread to call the sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="06f58-120">Gesegmenteerde aanbieding</span><span class="sxs-lookup"><span data-stu-id="06f58-120">Segmented listing</span></span>
<span data-ttu-id="06f58-121">De schaal van cloud-opslag vereist gesegmenteerde aanbieding.</span><span class="sxs-lookup"><span data-stu-id="06f58-121">The scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="06f58-122">U kunt bijvoorbeeld via een miljoen blobs in een Azure blob-container of via een miljard entiteiten in een Azure-tabel hebben.</span><span class="sxs-lookup"><span data-stu-id="06f58-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="06f58-123">Dit zijn geen theoretische cijfers, maar de informatie over het gebruik van echte klantaanvragen.</span><span class="sxs-lookup"><span data-stu-id="06f58-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="06f58-124">Daarom is het niet praktisch voor een lijst met alle objecten in een enkel antwoord.</span><span class="sxs-lookup"><span data-stu-id="06f58-124">It is therefore impractical to list all objects in a single response.</span></span> <span data-ttu-id="06f58-125">In plaats daarvan kunt u objecten met behulp van paginering aanbieden.</span><span class="sxs-lookup"><span data-stu-id="06f58-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="06f58-126">Elk van de aanbieding API's heeft een *gesegmenteerde* overbelasting.</span><span class="sxs-lookup"><span data-stu-id="06f58-126">Each of the listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="06f58-127">Het antwoord voor het uitvoeren van een gesegmenteerde aanbieding omvat:</span><span class="sxs-lookup"><span data-stu-id="06f58-127">The response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="06f58-128"><i>_Segment</i>, die de verzameling resultaten geretourneerd voor één aanroep van de aanbieding API bevat.</span><span class="sxs-lookup"><span data-stu-id="06f58-128"><i>_segment</i>, which contains the set of results returned for a single call to the listing API.</span></span>
* <span data-ttu-id="06f58-129">*continuation_token*, die wordt doorgegeven aan de volgende oproep om op te halen van de volgende pagina van de resultaten.</span><span class="sxs-lookup"><span data-stu-id="06f58-129">*continuation_token*, which is passed to the next call in order to get the next page of results.</span></span> <span data-ttu-id="06f58-130">Wanneer er geen verdere resultaten te retourneren, is het vervolgtoken is null.</span><span class="sxs-lookup"><span data-stu-id="06f58-130">When there are no more results to return, the continuation token is null.</span></span>

<span data-ttu-id="06f58-131">Een typische aanroep voor een lijst met alle blobs in een container kan bijvoorbeeld het volgende codefragment eruit.</span><span class="sxs-lookup"><span data-stu-id="06f58-131">For example, a typical call to list all blobs in a container may look like the following code snippet.</span></span> <span data-ttu-id="06f58-132">De code is beschikbaar in onze [voorbeelden](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="06f58-132">The code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in the blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="06f58-133">Houd er rekening mee dat het aantal resultaten in een pagina kan worden beheerd door de parameter *max_results* in de overbelasting van elke API, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="06f58-133">Note that the number of results returned in a page can be controlled by the parameter *max_results* in the overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="06f58-134">Als u niet geeft de *max_results* parameter, worden de standaardinstellingen in één pagina maximumwaarde van maximaal 5.000 resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="06f58-134">If you do not specify the *max_results* parameter, the default maximum value of up to 5000 results is returned in a single page.</span></span>

<span data-ttu-id="06f58-135">Let ook op dat een query op Azure Table storage geen records, of minder dan de waarde van retourneren kan de *max_results* parameter die u hebt opgegeven, zelfs als het vervolgtoken niet leeg is.</span><span class="sxs-lookup"><span data-stu-id="06f58-135">Also note that a query against Azure Table storage may return no records, or fewer records than the value of the *max_results* parameter that you specified, even if the continuation token is not empty.</span></span> <span data-ttu-id="06f58-136">Een reden hiervoor is mogelijk dat de query kan niet worden voltooid in de vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="06f58-136">One reason might be that the query could not complete in five seconds.</span></span> <span data-ttu-id="06f58-137">De query moet worden voortgezet, zolang het vervolgtoken niet leeg is, en uw code mogen niet de grootte van het resultaat van een segment aannemen.</span><span class="sxs-lookup"><span data-stu-id="06f58-137">As long as the continuation token is not empty, the query should continue, and your code should not assume the size of segment results.</span></span>

<span data-ttu-id="06f58-138">Het aanbevolen codering patroon voor de meeste scenario is onderverdeeld op te nemen, waarmee u expliciete voortgang van de aanbieding of uitvoeren van query's en hoe de service reageert op elke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="06f58-138">The recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how the service responds to each request.</span></span> <span data-ttu-id="06f58-139">Met name voor C++-toepassingen of services kunt lager niveau controle over de voortgang van de aanbieding besturingselement geheugen en de prestaties.</span><span class="sxs-lookup"><span data-stu-id="06f58-139">Particularly for C++ applications or services, lower-level control of the listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="06f58-140">Greedy aanbieding</span><span class="sxs-lookup"><span data-stu-id="06f58-140">Greedy listing</span></span>
<span data-ttu-id="06f58-141">Eerdere versies van de Opslagclientbibliotheek voor C++ (Preview-versies 0.5.0 en eerder) opgenomen van niet-gesegmenteerde aanbieding API's voor tabellen en wachtrijen, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="06f58-141">Earlier versions of the Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in the following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="06f58-142">Deze methoden zijn geïmplementeerd als wrappers gesegmenteerde API's.</span><span class="sxs-lookup"><span data-stu-id="06f58-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="06f58-143">Voor elke reactie van gesegmenteerde aanbieding, worden de code de resultaten toegevoegd aan een vector en alle resultaten geretourneerd nadat de volledige-containers zijn gescand.</span><span class="sxs-lookup"><span data-stu-id="06f58-143">For each response of segmented listing, the code appended the results to a vector and returned all results after the full containers were scanned.</span></span>

<span data-ttu-id="06f58-144">Deze methode werkt mogelijk wanneer het opslagaccount of de tabel een klein aantal objecten bevat.</span><span class="sxs-lookup"><span data-stu-id="06f58-144">This approach might work when the storage account or table contains a small number of objects.</span></span> <span data-ttu-id="06f58-145">Echter, met een toename in het aantal objecten, het geheugen dat nodig kan vergroten zonder beperking, omdat alle resultaten bleef in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="06f58-145">However, with an increase in the number of objects, the memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="06f58-146">Één aanbieding bewerking kan erg lang duren, gedurende welke de aanroeper geen informatie over de voortgang heeft.</span><span class="sxs-lookup"><span data-stu-id="06f58-146">One listing operation can take a very long time, during which the caller had no information about its progress.</span></span>

<span data-ttu-id="06f58-147">Deze greedy aanbieding API's in de SDK niet bestaan in C#, Java of de JavaScript-Node.js-omgeving.</span><span class="sxs-lookup"><span data-stu-id="06f58-147">These greedy listing APIs in the SDK do not exist in C#, Java, or the JavaScript Node.js environment.</span></span> <span data-ttu-id="06f58-148">Om te voorkomen de potentiële problemen van het gebruik van deze greedy API's, wordt deze verwijderd in versie 0.6.0 Preview.</span><span class="sxs-lookup"><span data-stu-id="06f58-148">To avoid the potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="06f58-149">Als uw code deze greedy API's aanroept:</span><span class="sxs-lookup"><span data-stu-id="06f58-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="06f58-150">Wijzig vervolgens de code voor het gebruik van de gesegmenteerde aanbieding API's:</span><span class="sxs-lookup"><span data-stu-id="06f58-150">Then you should modify your code to use the segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="06f58-151">Door op te geven de *max_results* parameter van het segment kan verdeeld tussen het aantal aanvragen en geheugengebruik om te voldoen aan de prestatie-overwegingen voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="06f58-151">By specifying the *max_results* parameter of the segment, you can balance between the numbers of requests and memory usage to meet performance considerations for your application.</span></span>

<span data-ttu-id="06f58-152">Bovendien, als u gesegmenteerde aanbieding API's gebruikt, maar de gegevens opslaan in een lokale verzameling in een style 'greedy', wordt ook aangeraden dat u uw code voor het opslaan van gegevens in een lokale verzameling zorgvuldig op grote schaal afhandelen opsplitsen.</span><span class="sxs-lookup"><span data-stu-id="06f58-152">Additionally, if you're using segmented listing APIs, but store the data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code to handle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="06f58-153">Vertraagde aanbieding</span><span class="sxs-lookup"><span data-stu-id="06f58-153">Lazy listing</span></span>
<span data-ttu-id="06f58-154">Hoewel greedy aanbieding potentiële problemen gegenereerd, is het handig als er niet te veel objecten in de container.</span><span class="sxs-lookup"><span data-stu-id="06f58-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in the container.</span></span>

<span data-ttu-id="06f58-155">Als u ook C# of Oracle Java SDK's gebruikt, kunt u moet bekend bent met het inventariseerbare programming model een vertraagde--stijl op te nemen biedt, waar de gegevens op een bepaalde offset alleen worden opgehaald als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="06f58-155">If you're also using C# or Oracle Java SDKs, you should be familiar with the Enumerable programming model, which offers a lazy-style listing, where the data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="06f58-156">In C++ kunt biedt de sjabloon op basis van een iterator ook een soortgelijke benadering.</span><span class="sxs-lookup"><span data-stu-id="06f58-156">In C++, the iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="06f58-157">Een typische vertraagde aanbieding API, met behulp van **list_blobs** bijvoorbeeld zo uitziet:</span><span class="sxs-lookup"><span data-stu-id="06f58-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="06f58-158">Een typische codefragment die gebruikmaakt van het patroon vertraagde aanbieding uitzien als volgt:</span><span class="sxs-lookup"><span data-stu-id="06f58-158">A typical code snippet that uses the lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in the blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="06f58-159">Houd er rekening mee vertraagde aanbieding is alleen beschikbaar in synchrone modus.</span><span class="sxs-lookup"><span data-stu-id="06f58-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="06f58-160">Vergeleken met greedy aanbieding, haalt vertraagde aanbieding gegevens alleen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="06f58-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="06f58-161">Onder de behandelt ophaalt het gegevens uit Azure Storage alleen wanneer de volgende iterator is verplaatst naar de volgende segment.</span><span class="sxs-lookup"><span data-stu-id="06f58-161">Under the covers, it fetches data from Azure Storage only when the next iterator moves into next segment.</span></span> <span data-ttu-id="06f58-162">Daarom geheugengebruik wordt beheerd met een begrensde grootte en de bewerking is snel.</span><span class="sxs-lookup"><span data-stu-id="06f58-162">Therefore, memory usage is controlled with a bounded size, and the operation is fast.</span></span>

<span data-ttu-id="06f58-163">Vertraagde aanbieding API's worden opgenomen in de Opslagclientbibliotheek voor C++ in versie 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="06f58-163">Lazy listing APIs are included in the Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="06f58-164">Conclusie</span><span class="sxs-lookup"><span data-stu-id="06f58-164">Conclusion</span></span>
<span data-ttu-id="06f58-165">In dit artikel wordt besproken verschillende overbelastingen voor het aanbieden van API's voor verschillende objecten in de Opslagclientbibliotheek voor C++.</span><span class="sxs-lookup"><span data-stu-id="06f58-165">In this article, we discussed different overloads for listing APIs for various objects in the Storage Client Library for C++ .</span></span> <span data-ttu-id="06f58-166">Samengevat:</span><span class="sxs-lookup"><span data-stu-id="06f58-166">To summarize:</span></span>

* <span data-ttu-id="06f58-167">Asynchrone APIs ten sterkste aangeraden onder scenario's met meerdere threads.</span><span class="sxs-lookup"><span data-stu-id="06f58-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="06f58-168">Gesegmenteerde aanbieding wordt aanbevolen voor de meeste scenario's.</span><span class="sxs-lookup"><span data-stu-id="06f58-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="06f58-169">Vertraagde aanbieding is opgegeven in de bibliotheek als een handige wrapper in synchrone scenario's.</span><span class="sxs-lookup"><span data-stu-id="06f58-169">Lazy listing is provided in the library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="06f58-170">Greedy aanbieding wordt niet aanbevolen en is verwijderd uit de bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="06f58-170">Greedy listing is not recommended and has been removed from the library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06f58-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="06f58-171">Next steps</span></span>
<span data-ttu-id="06f58-172">Zie de volgende bronnen voor meer informatie over Azure Storage en -clientbibliotheek voor C++.</span><span class="sxs-lookup"><span data-stu-id="06f58-172">For more information about Azure Storage and Client Library for C++, see the following resources.</span></span>

* [<span data-ttu-id="06f58-173">Het Blob Storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="06f58-173">How to use Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="06f58-174">Hoe Table Storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="06f58-174">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="06f58-175">Hoe Queue Storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="06f58-175">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="06f58-176">Azure Storage-clientbibliotheek voor C++ API-documentatie.</span><span class="sxs-lookup"><span data-stu-id="06f58-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="06f58-177">Blog van het Azure Storage-team</span><span class="sxs-lookup"><span data-stu-id="06f58-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="06f58-178">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="06f58-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

