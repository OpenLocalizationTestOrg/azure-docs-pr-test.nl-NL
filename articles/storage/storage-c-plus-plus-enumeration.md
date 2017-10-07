---
title: Azure Storage-resources aaaList Hello Opslagclientbibliotheek voor C++ | Microsoft Docs
description: Meer informatie over hoe toouse Hallo aanbieding API's in Microsoft Azure Storage-clientbibliotheek voor C++ tooenumerate containers, blobs, wachtrijen, tabellen en entiteiten.
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
ms.openlocfilehash: d20a86688938704c24339aa9a1145786783fea5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="db69e-103">Lijst van Azure Storage-resources in C++</span><span class="sxs-lookup"><span data-stu-id="db69e-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="db69e-104">Aanbieding-bewerkingen zijn toomany belangrijke ontwikkelscenario's met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="db69e-104">Listing operations are key toomany development scenarios with Azure Storage.</span></span> <span data-ttu-id="db69e-105">Dit artikel wordt beschreven hoe toomost efficiënt objecten in Azure Storage met API's die zijn opgegeven in Microsoft Azure Storage-clientbibliotheek Hallo voor C++ aanbieding Hallo inventariseren.</span><span class="sxs-lookup"><span data-stu-id="db69e-105">This article describes how toomost efficiently enumerate objects in Azure Storage using hello listing APIs provided in hello Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="db69e-106">Deze handleiding is bedoeld voor hello Azure Storage-clientbibliotheek voor C++ versie 2.x die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="db69e-106">This guide targets hello Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="db69e-107">Hallo Storage-clientbibliotheek biedt tal van manieren toolist of query-objecten in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="db69e-107">hello Storage Client Library provides a variety of methods toolist or query objects in Azure Storage.</span></span> <span data-ttu-id="db69e-108">In dit artikel komen Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="db69e-108">This article addresses hello following scenarios:</span></span>

* <span data-ttu-id="db69e-109">Lijst containers in een account</span><span class="sxs-lookup"><span data-stu-id="db69e-109">List containers in an account</span></span>
* <span data-ttu-id="db69e-110">Lijst met blobs in een container of blob virtuele map</span><span class="sxs-lookup"><span data-stu-id="db69e-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="db69e-111">Lijst met wachtrijen in een account</span><span class="sxs-lookup"><span data-stu-id="db69e-111">List queues in an account</span></span>
* <span data-ttu-id="db69e-112">Lijst met tabellen in een account</span><span class="sxs-lookup"><span data-stu-id="db69e-112">List tables in an account</span></span>
* <span data-ttu-id="db69e-113">Query-entiteiten in een tabel</span><span class="sxs-lookup"><span data-stu-id="db69e-113">Query entities in a table</span></span>

<span data-ttu-id="db69e-114">Elk van deze methoden wordt weergegeven als u verschillende overbelastingen voor verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="db69e-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="db69e-115">Asynchrone en synchrone</span><span class="sxs-lookup"><span data-stu-id="db69e-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="db69e-116">Omdat Hallo Opslagclientbibliotheek voor C++ is gebouwd boven op Hallo [REST C++-bibliotheek](https://github.com/Microsoft/cpprestsdk), we inherent bieden ondersteuning voor asynchrone bewerkingen met behulp van [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="db69e-116">Because hello Storage Client Library for C++ is built on top of hello [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="db69e-117">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="db69e-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="db69e-118">Synchrone bewerkingen teruglopen Hallo corresponderende asynchrone bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="db69e-118">Synchronous operations wrap hello corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="db69e-119">Als u met meerdere threads toepassingen of services werkt, raden wij aan dat u Hallo async API's rechtstreeks in plaats van het maken van een thread toocall Hallo synchronisatie API's, die aanzienlijk heeft impact op de prestaties van uw.</span><span class="sxs-lookup"><span data-stu-id="db69e-119">If you are working with multiple threading applications or services, we recommend that you use hello async APIs directly instead of creating a thread toocall hello sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="db69e-120">Gesegmenteerde aanbieding</span><span class="sxs-lookup"><span data-stu-id="db69e-120">Segmented listing</span></span>
<span data-ttu-id="db69e-121">Hallo schaal van cloud-opslag vereist gesegmenteerde aanbieding.</span><span class="sxs-lookup"><span data-stu-id="db69e-121">hello scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="db69e-122">U kunt bijvoorbeeld via een miljoen blobs in een Azure blob-container of via een miljard entiteiten in een Azure-tabel hebben.</span><span class="sxs-lookup"><span data-stu-id="db69e-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="db69e-123">Dit zijn geen theoretische cijfers, maar de informatie over het gebruik van echte klantaanvragen.</span><span class="sxs-lookup"><span data-stu-id="db69e-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="db69e-124">Daarom is het niet praktisch toolist alle objecten in een enkel antwoord.</span><span class="sxs-lookup"><span data-stu-id="db69e-124">It is therefore impractical toolist all objects in a single response.</span></span> <span data-ttu-id="db69e-125">In plaats daarvan kunt u objecten met behulp van paginering aanbieden.</span><span class="sxs-lookup"><span data-stu-id="db69e-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="db69e-126">Elk van de API's aanbieding Hallo heeft een *gesegmenteerde* overbelasting.</span><span class="sxs-lookup"><span data-stu-id="db69e-126">Each of hello listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="db69e-127">Hallo-antwoord voor het uitvoeren van een gesegmenteerde aanbieding omvat:</span><span class="sxs-lookup"><span data-stu-id="db69e-127">hello response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="db69e-128"><i>_Segment</i>, die Hallo set resultaten geretourneerd voor een enkele aanroep toohello aanbieding API bevat.</span><span class="sxs-lookup"><span data-stu-id="db69e-128"><i>_segment</i>, which contains hello set of results returned for a single call toohello listing API.</span></span>
* <span data-ttu-id="db69e-129">*continuation_token*, die de volgende oproep toohello wordt doorgegeven in volgorde tooget Hallo volgende pagina van de resultaten.</span><span class="sxs-lookup"><span data-stu-id="db69e-129">*continuation_token*, which is passed toohello next call in order tooget hello next page of results.</span></span> <span data-ttu-id="db69e-130">Wanneer er geen meer resultaten tooreturn, is Hallo vervolgtoken null.</span><span class="sxs-lookup"><span data-stu-id="db69e-130">When there are no more results tooreturn, hello continuation token is null.</span></span>

<span data-ttu-id="db69e-131">Bijvoorbeeld, een aanroep van typische toolist alle blobs in een container eruit als Hallo codefragment te volgen.</span><span class="sxs-lookup"><span data-stu-id="db69e-131">For example, a typical call toolist all blobs in a container may look like hello following code snippet.</span></span> <span data-ttu-id="db69e-132">Hallo-code is beschikbaar in onze [voorbeelden](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="db69e-132">hello code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in hello blob container
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

<span data-ttu-id="db69e-133">Houd er rekening mee dat het aantal resultaten in een pagina Hallo kan worden beheerd door Hallo parameter *max_results* in Hallo overbelasting van elke API, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="db69e-133">Note that hello number of results returned in a page can be controlled by hello parameter *max_results* in hello overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="db69e-134">Als u geen Hallo opgeeft *max_results* parameter, Hallo standaard maximale waarde van too5000 resultaten wordt geretourneerd als één pagina.</span><span class="sxs-lookup"><span data-stu-id="db69e-134">If you do not specify hello *max_results* parameter, hello default maximum value of up too5000 results is returned in a single page.</span></span>

<span data-ttu-id="db69e-135">Let ook op een query op Azure Table storage kan geen records of minder records zijn dan de waarde van Hallo Hallo retourneren *max_results* parameter die u hebt opgegeven, zelfs als Hallo vervolgtoken niet leeg is.</span><span class="sxs-lookup"><span data-stu-id="db69e-135">Also note that a query against Azure Table storage may return no records, or fewer records than hello value of hello *max_results* parameter that you specified, even if hello continuation token is not empty.</span></span> <span data-ttu-id="db69e-136">Een reden hiervoor is mogelijk dat Hallo-query kan niet worden voltooid in de vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="db69e-136">One reason might be that hello query could not complete in five seconds.</span></span> <span data-ttu-id="db69e-137">Zolang Hallo vervolgtoken niet leeg is, Hallo query moet worden voortgezet en uw code mogen niet Hallo-grootte van het resultaat van een segment aannemen.</span><span class="sxs-lookup"><span data-stu-id="db69e-137">As long as hello continuation token is not empty, hello query should continue, and your code should not assume hello size of segment results.</span></span>

<span data-ttu-id="db69e-138">Hallo aanbevolen coderen patroon voor de meeste scenario is onderverdeeld op te nemen, waarmee u expliciete voortgang van de aanbieding of uitvoeren van query's en hoe Hallo service tooeach aanvraag reageert.</span><span class="sxs-lookup"><span data-stu-id="db69e-138">hello recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how hello service responds tooeach request.</span></span> <span data-ttu-id="db69e-139">Met name voor C++-toepassingen of services kunt lager niveau besturingselement Hallo aanbieding voortgang besturingselement geheugen en de prestaties.</span><span class="sxs-lookup"><span data-stu-id="db69e-139">Particularly for C++ applications or services, lower-level control of hello listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="db69e-140">Greedy aanbieding</span><span class="sxs-lookup"><span data-stu-id="db69e-140">Greedy listing</span></span>
<span data-ttu-id="db69e-141">Eerdere versies van Hallo Opslagclientbibliotheek voor C++ (Preview-versies 0.5.0 en eerder) niet-gesegmenteerde aanbieding API's voor tabellen en wachtrijen, zoals in het volgende voorbeeld Hallo opgenomen:</span><span class="sxs-lookup"><span data-stu-id="db69e-141">Earlier versions of hello Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in hello following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="db69e-142">Deze methoden zijn geïmplementeerd als wrappers gesegmenteerde API's.</span><span class="sxs-lookup"><span data-stu-id="db69e-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="db69e-143">Voor elke reactie van gesegmenteerde aanbieding Hallo code Hallo resultaten tooa vector toegevoegd en alle resultaten geretourneerd nadat de volledige containers Hallo zijn gescand.</span><span class="sxs-lookup"><span data-stu-id="db69e-143">For each response of segmented listing, hello code appended hello results tooa vector and returned all results after hello full containers were scanned.</span></span>

<span data-ttu-id="db69e-144">Deze methode werkt mogelijk wanneer Hallo storage-account of de tabel een klein aantal objecten bevat.</span><span class="sxs-lookup"><span data-stu-id="db69e-144">This approach might work when hello storage account or table contains a small number of objects.</span></span> <span data-ttu-id="db69e-145">Echter met een toename in aantal objecten Hallo kan Hallo geheugen vereist verhogen zonder beperking, omdat alle resultaten bleef in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="db69e-145">However, with an increase in hello number of objects, hello memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="db69e-146">Één aanbieding bewerking kan erg lang duren, tijdens welke Hallo aanroeper geen informatie over de voortgang heeft.</span><span class="sxs-lookup"><span data-stu-id="db69e-146">One listing operation can take a very long time, during which hello caller had no information about its progress.</span></span>

<span data-ttu-id="db69e-147">Deze greedy aanbieding API's in Hallo SDK niet bestaan in C#, Java, of Hallo JavaScript Node.js-omgeving.</span><span class="sxs-lookup"><span data-stu-id="db69e-147">These greedy listing APIs in hello SDK do not exist in C#, Java, or hello JavaScript Node.js environment.</span></span> <span data-ttu-id="db69e-148">tooavoid hello potentiële problemen van het gebruik van deze greedy API's, wordt deze verwijderd in versie 0.6.0 Preview.</span><span class="sxs-lookup"><span data-stu-id="db69e-148">tooavoid hello potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="db69e-149">Als uw code deze greedy API's aanroept:</span><span class="sxs-lookup"><span data-stu-id="db69e-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="db69e-150">Vervolgens moet u uw code wijzigen toouse Hallo gesegmenteerde aanbieding API's:</span><span class="sxs-lookup"><span data-stu-id="db69e-150">Then you should modify your code toouse hello segmented listing APIs:</span></span>

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

<span data-ttu-id="db69e-151">Door op te geven Hallo *max_results* parameter van Hallo segment kan verdeeld tussen Hallo aantallen aanvragen en geheugen gebruik toomeet prestatie-overwegingen voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="db69e-151">By specifying hello *max_results* parameter of hello segment, you can balance between hello numbers of requests and memory usage toomeet performance considerations for your application.</span></span>

<span data-ttu-id="db69e-152">Bovendien, als u gesegmenteerde aanbieding API's gebruiken, maar Hallo gegevens opslaan in een lokale verzameling in een style 'greedy', wordt ook aangeraden dat u uw code toohandle opslaan van gegevens in een lokale verzameling zorgvuldig op grote schaal opsplitsen.</span><span class="sxs-lookup"><span data-stu-id="db69e-152">Additionally, if you're using segmented listing APIs, but store hello data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code toohandle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="db69e-153">Vertraagde aanbieding</span><span class="sxs-lookup"><span data-stu-id="db69e-153">Lazy listing</span></span>
<span data-ttu-id="db69e-154">Hoewel greedy aanbieding potentiële problemen gegenereerd, is het handig als er niet te veel objecten in het Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="db69e-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in hello container.</span></span>

<span data-ttu-id="db69e-155">Als u ook C# of Oracle Java SDK's gebruikt, kunt u moet bekend bent met Hallo inventariseerbare programming model een vertraagde--stijl op te nemen biedt, waarbij Hallo gegevens bij een bepaalde offset worden alleen opgehaald als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="db69e-155">If you're also using C# or Oracle Java SDKs, you should be familiar with hello Enumerable programming model, which offers a lazy-style listing, where hello data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="db69e-156">In C++ kunt biedt Hallo iterator gebaseerde sjabloon ook een soortgelijke benadering.</span><span class="sxs-lookup"><span data-stu-id="db69e-156">In C++, hello iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="db69e-157">Een typische vertraagde aanbieding API, met behulp van **list_blobs** bijvoorbeeld zo uitziet:</span><span class="sxs-lookup"><span data-stu-id="db69e-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="db69e-158">Een typische codefragment dat Hallo vertraagde aanbieding patroon gebruikt uitzien als volgt:</span><span class="sxs-lookup"><span data-stu-id="db69e-158">A typical code snippet that uses hello lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in hello blob container
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

<span data-ttu-id="db69e-159">Houd er rekening mee vertraagde aanbieding is alleen beschikbaar in synchrone modus.</span><span class="sxs-lookup"><span data-stu-id="db69e-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="db69e-160">Vergeleken met greedy aanbieding, haalt vertraagde aanbieding gegevens alleen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="db69e-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="db69e-161">Onder Hallo dekt ophaalt het gegevens uit Azure Storage alleen wanneer de volgende iterator Hallo is verplaatst naar de volgende segment.</span><span class="sxs-lookup"><span data-stu-id="db69e-161">Under hello covers, it fetches data from Azure Storage only when hello next iterator moves into next segment.</span></span> <span data-ttu-id="db69e-162">Daarom geheugengebruik wordt beheerd met een begrensde grootte en Hallo-bewerking is snel.</span><span class="sxs-lookup"><span data-stu-id="db69e-162">Therefore, memory usage is controlled with a bounded size, and hello operation is fast.</span></span>

<span data-ttu-id="db69e-163">Vertraagde aanbieding API's worden opgenomen in Hallo Opslagclientbibliotheek voor C++ in versie 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="db69e-163">Lazy listing APIs are included in hello Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="db69e-164">Conclusie</span><span class="sxs-lookup"><span data-stu-id="db69e-164">Conclusion</span></span>
<span data-ttu-id="db69e-165">In dit artikel wordt besproken verschillende overbelastingen voor het aanbieden van API's voor verschillende objecten in Hallo Opslagclientbibliotheek voor C++.</span><span class="sxs-lookup"><span data-stu-id="db69e-165">In this article, we discussed different overloads for listing APIs for various objects in hello Storage Client Library for C++ .</span></span> <span data-ttu-id="db69e-166">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="db69e-166">toosummarize:</span></span>

* <span data-ttu-id="db69e-167">Asynchrone APIs ten sterkste aangeraden onder scenario's met meerdere threads.</span><span class="sxs-lookup"><span data-stu-id="db69e-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="db69e-168">Gesegmenteerde aanbieding wordt aanbevolen voor de meeste scenario's.</span><span class="sxs-lookup"><span data-stu-id="db69e-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="db69e-169">Vertraagde aanbieding is opgegeven in de bibliotheek Hallo als een handige wrapper in synchrone scenario's.</span><span class="sxs-lookup"><span data-stu-id="db69e-169">Lazy listing is provided in hello library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="db69e-170">Greedy aanbieding wordt niet aanbevolen en is verwijderd uit het Hallo-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="db69e-170">Greedy listing is not recommended and has been removed from hello library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db69e-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="db69e-171">Next steps</span></span>
<span data-ttu-id="db69e-172">Zie voor meer informatie over Azure Storage en -clientbibliotheek voor C++ Hallo resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="db69e-172">For more information about Azure Storage and Client Library for C++, see hello following resources.</span></span>

* [<span data-ttu-id="db69e-173">Hoe toouse C++ Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="db69e-173">How toouse Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="db69e-174">Hoe toouse Table Storage uit het C++</span><span class="sxs-lookup"><span data-stu-id="db69e-174">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="db69e-175">Hoe toouse Queue Storage vanuit C++</span><span class="sxs-lookup"><span data-stu-id="db69e-175">How toouse Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="db69e-176">Azure Storage-clientbibliotheek voor C++ API-documentatie.</span><span class="sxs-lookup"><span data-stu-id="db69e-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="db69e-177">Blog van het Azure Storage-team</span><span class="sxs-lookup"><span data-stu-id="db69e-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="db69e-178">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="db69e-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

