---
title: aaaAzure Cosmos DB .NET Core API SDK & Resources | Microsoft Docs
description: Meer informatie over Hallo .NET Core API en SDK, inclusief release datums, buiten gebruik stellen datums en wijzigingen die zijn aangebracht tussen elke versie van hello Azure Cosmos DB .NET Core SDK.
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="18b3f-103">Azure Cosmos DB .NET Core SDK: Releaseopmerkingen en resources</span><span class="sxs-lookup"><span data-stu-id="18b3f-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="18b3f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="18b3f-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="18b3f-105">.NET-Feed van wijzigen</span><span class="sxs-lookup"><span data-stu-id="18b3f-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="18b3f-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="18b3f-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="18b3f-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="18b3f-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="18b3f-108">Java</span><span class="sxs-lookup"><span data-stu-id="18b3f-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="18b3f-109">Python</span><span class="sxs-lookup"><span data-stu-id="18b3f-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="18b3f-110">REST</span><span class="sxs-lookup"><span data-stu-id="18b3f-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="18b3f-111">REST-resourceprovider</span><span class="sxs-lookup"><span data-stu-id="18b3f-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="18b3f-112">SQL</span><span class="sxs-lookup"><span data-stu-id="18b3f-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="18b3f-113">**SDK downloaden**</span><span class="sxs-lookup"><span data-stu-id="18b3f-113">**SDK download**</span></span></td><td>[<span data-ttu-id="18b3f-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="18b3f-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="18b3f-115">**API-documentatie**</span><span class="sxs-lookup"><span data-stu-id="18b3f-115">**API documentation**</span></span></td><td>[<span data-ttu-id="18b3f-116">.NET API-naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="18b3f-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="18b3f-117">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="18b3f-117">**Samples**</span></span></td><td>[<span data-ttu-id="18b3f-118">.NET-codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="18b3f-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="18b3f-119">**Aan de slag**</span><span class="sxs-lookup"><span data-stu-id="18b3f-119">**Get started**</span></span></td><td>[<span data-ttu-id="18b3f-120">Aan de slag met hello Azure Cosmos DB .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="18b3f-120">Get started with hello Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="18b3f-121">**Zelfstudie voor web-app**</span><span class="sxs-lookup"><span data-stu-id="18b3f-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="18b3f-122">Ontwikkeling van webtoepassing met Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="18b3f-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="18b3f-123">**Huidige ondersteunde framework**</span><span class="sxs-lookup"><span data-stu-id="18b3f-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="18b3f-124">.NET standaard 1.6 en .NET standaard 1.5</span><span class="sxs-lookup"><span data-stu-id="18b3f-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="18b3f-125">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="18b3f-125">Release Notes</span></span>

<span data-ttu-id="18b3f-126">Hello Azure Cosmos DB .NET Core SDK heeft functie pariteit met de meest recente versie Hallo Hallo [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="18b3f-126">hello Azure Cosmos DB .NET Core SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="18b3f-127">Hello Azure Cosmos DB .NET Core SDK is nog niet compatibel met Universal Windows Platform (UWP)-apps.</span><span class="sxs-lookup"><span data-stu-id="18b3f-127">hello Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="18b3f-128">Als u geïnteresseerd in Hallo .NET Core SDK die ondersteuning biedt voor UWP-apps bent, e-mail sturen te[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="18b3f-128">If you are interested in hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="18b3f-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="18b3f-130">Ondersteuning toegevoegd voor PartitionKeyRangeId als een FeedOption voor het vaststellen van de query resultaten tooa specifieke sleutel partitiebereikwaarde.</span><span class="sxs-lookup"><span data-stu-id="18b3f-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="18b3f-131">Ondersteuning toegevoegd voor StartTime als een ChangeFeedOption toostart Hallo wijzigingen zoekt na dit tijdstip.</span><span class="sxs-lookup"><span data-stu-id="18b3f-131">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="18b3f-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="18b3f-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="18b3f-133">Een probleem opgelost in Hallo JsonSerializable-klasse die een stackoverloopuitzondering kan veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="18b3f-133">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="18b3f-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="18b3f-135">Toegevoegde ondersteuning voor het opgeven van aangepaste JsonSerializerSettings tijdens het instantiëren van een [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) exemplaar.</span><span class="sxs-lookup"><span data-stu-id="18b3f-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="18b3f-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="18b3f-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="18b3f-137">Ondersteuning voor .NET standaard 1.5 als een van de doel-frameworks Hallo.</span><span class="sxs-lookup"><span data-stu-id="18b3f-137">Supporting .NET Standard 1.5 as one of hello target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="18b3f-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="18b3f-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="18b3f-139">Een probleem dat van invloed op een x64 vaste machines die geen SSE4 instructie ondersteunen en genereert SEHException bij het uitvoeren van query's Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="18b3f-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="18b3f-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="18b3f-141">Ondersteuning toegevoegd voor een nieuwe consistentieniveau ConsistentPrefix genoemd.</span><span class="sxs-lookup"><span data-stu-id="18b3f-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="18b3f-142">Ondersteuning toegevoegd voor query metrische gegevens voor afzonderlijke partities.</span><span class="sxs-lookup"><span data-stu-id="18b3f-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="18b3f-143">Ondersteuning toegevoegd voor het beperken van de grootte van de Hallo van Hallo vervolgtoken voor query's.</span><span class="sxs-lookup"><span data-stu-id="18b3f-143">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="18b3f-144">Ondersteuning toegevoegd voor meer gedetailleerde tracering van mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="18b3f-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="18b3f-145">Een aantal verbeteringen aangebracht in Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="18b3f-145">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="18b3f-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="18b3f-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="18b3f-147">Een probleem dat genegeerd Hallo PartitionKey waarde die is opgegeven in FeedOptions voor cumulatieve query's opgelost.</span><span class="sxs-lookup"><span data-stu-id="18b3f-147">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="18b3f-148">Een probleem opgelost in transparante verwerking van de partitie management tijdens de vlucht halverwege cross-partitie Order By queryuitvoering.</span><span class="sxs-lookup"><span data-stu-id="18b3f-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="18b3f-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="18b3f-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="18b3f-150">Een probleem waardoor impassen in een aantal asynchrone Hallo API's bij gebruik binnen de context van ASP.NET opgelost.</span><span class="sxs-lookup"><span data-stu-id="18b3f-150">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="18b3f-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="18b3f-152">Toomake SDK corrigeert meer robuuste tooautomatic failover onder bepaalde omstandigheden.</span><span class="sxs-lookup"><span data-stu-id="18b3f-152">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="18b3f-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="18b3f-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="18b3f-154">Herstel voor een probleem dat soms een WebException veroorzaakt: Hallo externe naam kan niet worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="18b3f-154">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="18b3f-155">Hallo toegevoegde ondersteuning voor het rechtstreeks lezen van een getypt document door nieuwe overloads tooReadDocumentAsync API toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="18b3f-155">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="18b3f-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="18b3f-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="18b3f-157">Toegevoegde ondersteuning voor LINQ voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem).</span><span class="sxs-lookup"><span data-stu-id="18b3f-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="18b3f-158">Herstel voor een probleem geheugen-geheugenlek voor Hallo ConnectionPolicy object veroorzaakt door Hallo gebruik van gebeurtenis-handler.</span><span class="sxs-lookup"><span data-stu-id="18b3f-158">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="18b3f-159">Herstel voor een probleem waarbij de UpsertAttachmentAsync niet werkt is wanneer ETag is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="18b3f-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="18b3f-160">Herstel voor een probleem waarin cross partitie volgorde door de voortzetting van de query niet werken is bij het sorteren van tekenreeksveld.</span><span class="sxs-lookup"><span data-stu-id="18b3f-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="18b3f-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="18b3f-162">Ondersteuning toegevoegd voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem).</span><span class="sxs-lookup"><span data-stu-id="18b3f-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="18b3f-163">Zie [aggregatie ondersteuning](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="18b3f-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="18b3f-164">Minimaal doorvoer voor gepartitioneerde verzamelingen uit 10,100 RU/s too2500 RU/s verlaagd.</span><span class="sxs-lookup"><span data-stu-id="18b3f-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="18b3f-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="18b3f-166">Hello Azure Cosmos DB .NET Core SDK kunt u toobuild snel, platformoverschrijdende [ASP.NET Core](https://www.asp.net/core) en [.NET Core](https://www.microsoft.com/net/core#windows) toorun apps op Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="18b3f-166">hello Azure Cosmos DB .NET Core SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span> <span data-ttu-id="18b3f-167">Hallo meest recente versie van hello Azure Cosmos DB .NET Core SDK is volledig [Xamarin](https://www.xamarin.com) compatibel en gebruikte toobuild toepassingen die zijn gericht op iOS-, Android- en Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="18b3f-167">hello latest release of hello Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used toobuild applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="18b3f-168"><a name="0.1.0-preview"/>0.1.0-Preview</span><span class="sxs-lookup"><span data-stu-id="18b3f-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="18b3f-169">Hello Azure Cosmos DB .NET Core Preview SDK kunt u toobuild snel, platformoverschrijdende [ASP.NET Core](https://www.asp.net/core) en [.NET Core](https://www.microsoft.com/net/core#windows) toorun apps op Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="18b3f-169">hello Azure Cosmos DB .NET Core Preview SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="18b3f-170">Hello Azure Cosmos DB .NET Core Preview SDK heeft functie pariteit met de meest recente versie Hallo Hallo [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) en ondersteunt de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="18b3f-170">hello Azure Cosmos DB .NET Core Preview SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports hello following:</span></span>
* <span data-ttu-id="18b3f-171">Alle [verbindingsmodus](performance-tips.md#networking): Gateway-modus, Direct TCP- en HTTPs Direct.</span><span class="sxs-lookup"><span data-stu-id="18b3f-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="18b3f-172">Alle [consistentieniveaus](consistency-levels.md): sterke, sessie, gebonden veroudering en Eventual.</span><span class="sxs-lookup"><span data-stu-id="18b3f-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="18b3f-173">[Gepartitioneerde verzamelingen](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="18b3f-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="18b3f-174">[Meerdere landen/regio database accounts en geo-replicatie](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="18b3f-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="18b3f-175">Als u vragen gerelateerde toothis SDK hebt, te posten[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), of het bestand is een probleem in Hallo [github-opslagplaats](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="18b3f-175">If you have questions related toothis SDK, post too[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in hello [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="18b3f-176">Release & buiten gebruik stellen datums</span><span class="sxs-lookup"><span data-stu-id="18b3f-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="18b3f-177">Versie</span><span class="sxs-lookup"><span data-stu-id="18b3f-177">Version</span></span> | <span data-ttu-id="18b3f-178">Releasedatum</span><span class="sxs-lookup"><span data-stu-id="18b3f-178">Release Date</span></span> | <span data-ttu-id="18b3f-179">Vervaldatum</span><span class="sxs-lookup"><span data-stu-id="18b3f-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="18b3f-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="18b3f-181">10 augustus 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="18b3f-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="18b3f-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="18b3f-183">07 augustus 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="18b3f-185">02 augustus 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="18b3f-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="18b3f-187">12 juni 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="18b3f-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="18b3f-189">23 mei 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="18b3f-191">10 mei 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="18b3f-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="18b3f-193">19 april 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="18b3f-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="18b3f-195">29 maart 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="18b3f-197">25 maart 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="18b3f-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="18b3f-199">20 maart 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="18b3f-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="18b3f-201">14 maart 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="18b3f-203">16 februari 2017</span><span class="sxs-lookup"><span data-stu-id="18b3f-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="18b3f-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="18b3f-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="18b3f-205">21 december 2016</span><span class="sxs-lookup"><span data-stu-id="18b3f-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="18b3f-206">0.1.0-Preview</span><span class="sxs-lookup"><span data-stu-id="18b3f-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="18b3f-207">15 november 2016</span><span class="sxs-lookup"><span data-stu-id="18b3f-207">November 15, 2016</span></span> |<span data-ttu-id="18b3f-208">31 december 2016</span><span class="sxs-lookup"><span data-stu-id="18b3f-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="18b3f-209">Zie ook</span><span class="sxs-lookup"><span data-stu-id="18b3f-209">See Also</span></span>
<span data-ttu-id="18b3f-210">Zie toolearn meer informatie over de Cosmos-DB [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) pagina van de service.</span><span class="sxs-lookup"><span data-stu-id="18b3f-210">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

