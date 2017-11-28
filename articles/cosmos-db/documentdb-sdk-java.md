---
title: 'Azure Cosmos DB: DocumentDB Java API, SDK en Resources | Microsoft Docs'
description: Meer informatie over Hallo Java API- en SDK, inclusief release datums, buiten gebruik stellen datums en wijzigingen die zijn aangebracht tussen elke versie van hello Azure Cosmos DB DocumentDB Java SDK.
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="2ac5a-103">Azure Cosmos DB: DocumentDB Java SDK-releaseopmerkingen en resources</span><span class="sxs-lookup"><span data-stu-id="2ac5a-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ac5a-104">.NET</span><span class="sxs-lookup"><span data-stu-id="2ac5a-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="2ac5a-105">.NET-Feed van wijzigen</span><span class="sxs-lookup"><span data-stu-id="2ac5a-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="2ac5a-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2ac5a-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="2ac5a-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="2ac5a-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="2ac5a-108">Java</span><span class="sxs-lookup"><span data-stu-id="2ac5a-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="2ac5a-109">Python</span><span class="sxs-lookup"><span data-stu-id="2ac5a-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="2ac5a-110">REST</span><span class="sxs-lookup"><span data-stu-id="2ac5a-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="2ac5a-111">REST-resourceprovider</span><span class="sxs-lookup"><span data-stu-id="2ac5a-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="2ac5a-112">SQL</span><span class="sxs-lookup"><span data-stu-id="2ac5a-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="2ac5a-113">**SDK downloaden**</span><span class="sxs-lookup"><span data-stu-id="2ac5a-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="2ac5a-114">Maven</span><span class="sxs-lookup"><span data-stu-id="2ac5a-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="2ac5a-115">**API-documentatie**</span><span class="sxs-lookup"><span data-stu-id="2ac5a-115">**API documentation**</span></span></td><td>[<span data-ttu-id="2ac5a-116">Java-API-naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="2ac5a-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="2ac5a-117">**Bijdragen tooSDK**</span><span class="sxs-lookup"><span data-stu-id="2ac5a-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="2ac5a-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="2ac5a-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="2ac5a-119">**Aan de slag**</span><span class="sxs-lookup"><span data-stu-id="2ac5a-119">**Get started**</span></span></td><td>[<span data-ttu-id="2ac5a-120">Aan de slag met Hallo Java SDK</span><span class="sxs-lookup"><span data-stu-id="2ac5a-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="2ac5a-121">**Zelfstudie voor web-app**</span><span class="sxs-lookup"><span data-stu-id="2ac5a-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="2ac5a-122">Ontwikkeling van webtoepassing met Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="2ac5a-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="2ac5a-123">**Huidige ondersteunde runtime**</span><span class="sxs-lookup"><span data-stu-id="2ac5a-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="2ac5a-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="2ac5a-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="2ac5a-125">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="2ac5a-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="2ac5a-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="2ac5a-127">Kritieke bugfixes toorequest verwerken tijdens de partitie wordt gesplitst.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="2ac5a-128">Een probleem met Hallo sterke en BoundedStaleness consistentieniveaus opgelost.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="2ac5a-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="2ac5a-130">Ondersteuning toegevoegd voor een nieuwe consistentieniveau ConsistentPrefix genoemd.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="2ac5a-131">Een fout bij het lezen van de verzameling in sessiemodus vast.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="2ac5a-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="2ac5a-133">Ingeschakelde ondersteuning voor gepartitioneerde verzameling met als geringe als 2500 RU per seconde en schalen in intervallen van 100 RU per seconde.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="2ac5a-134">Heeft een fout in de Hallo systeemeigen assembly waardoor NullRef uitzondering in sommige query's.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="2ac5a-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="2ac5a-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="2ac5a-136">Heeft een fout in de Hallo query-engine-configuratie waardoor uitzonderingen voor query's in de modus van de Gateway.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="2ac5a-137">Enkele fouten in Hallo sessie container dat leiden een 'Eigenaar bron is niet gevonden'-uitzondering voor aanvragen onmiddellijk na het maken van een siteverzameling tot kan opgelost.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="2ac5a-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="2ac5a-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="2ac5a-139">Ondersteuning toegevoegd voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem).</span><span class="sxs-lookup"><span data-stu-id="2ac5a-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="2ac5a-140">Zie [aggregatie ondersteuning](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="2ac5a-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="2ac5a-141">Ondersteuning toegevoegd voor de feed wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-141">Added support for change feed.</span></span>
* <span data-ttu-id="2ac5a-142">Ondersteuning toegevoegd voor de verzameling quotum informatie via RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="2ac5a-143">Ondersteuning toegevoegd voor de opgeslagen procedure script logboekregistratie via RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="2ac5a-144">Een bug vast waar query in de modus DirectHttps loopt vast wanneer zich voordoen tijdens versnelling fouten.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="2ac5a-145">Heeft een fout in de sessiemodus consistentie.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="2ac5a-146">Vaste een bug wat leiden NullReferenceException in HttpContext tot kan wanneer aanvraagsnelheid hoog is.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="2ac5a-147">Verbeterde prestaties van DirectHttps-modus.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="2ac5a-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="2ac5a-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="2ac5a-149">Toegevoegde eenvoudige exemplaar, op basis van proxy clientondersteuning met ConnectionPolicy.setProxy()-API.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="2ac5a-150">Toegevoegde DocumentClient.close() API tooproperly afsluiten DocumentClient-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="2ac5a-151">Verbeterde queryprestaties in de modus voor directe verbinding door het queryplan Hallo die zijn afgeleid van Hallo systeemeigen assembly in plaats van Hallo Gateway.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="2ac5a-152">Stel FAIL_ON_UNKNOWN_PROPERTIES = false zodat gebruikers niet toodefine JsonIgnoreProperties in hun POJO hoeven.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="2ac5a-153">Logboekregistratie toouse SLF4J geherstructureerd.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="2ac5a-154">Enkele andere fouten opgelost in de lezer van de consistentie.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="2ac5a-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="2ac5a-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="2ac5a-156">Heeft een fout in de Hallo verbinding management tooprevent verbinding lekken in de modus voor directe verbinding.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="2ac5a-157">Vaste een fout in de meeste query Hallo waar deze NullReferenece uitzondering kan genereren.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="2ac5a-158">Verbeterde prestaties door het aantal netwerkaanroep voor interne caches Hallo Hallo te verminderen.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="2ac5a-159">Toegevoegde statuscode ActivityID en aanvraag-URI in DocumentClientException als hulpmiddel bij probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="2ac5a-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="2ac5a-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="2ac5a-161">Een probleem opgelost in Verbindingsbeheer Hallo voor stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="2ac5a-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="2ac5a-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="2ac5a-163">Ondersteuning toegevoegd voor BoundedStaleness consistentieniveau.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="2ac5a-164">Ondersteuning toegevoegd voor directe verbinding voor CRUD-bewerkingen voor gepartitioneerde verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="2ac5a-165">Heeft een fout in de query voor de database met SQL.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="2ac5a-166">Heeft een fout in de Hallo sessiecache waar sessietoken misschien onjuist ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="2ac5a-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="2ac5a-168">Ondersteuning toegevoegd voor cross-partitie parallelle query's.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="2ac5a-169">Ondersteuning toegevoegd voor TOP/ORDER BY-query's voor gepartitioneerde verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="2ac5a-170">Toegevoegde ondersteuning voor sterke consistentie.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="2ac5a-171">Ondersteuning toegevoegd voor aanvragen van een naam op basis van wanneer u directe verbinding.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="2ac5a-172">Vaste toomake ActivityId blijven consistent op alle nieuwe aanvraagpogingen.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="2ac5a-173">Een bug vast over de sessiecache toohello bij opnieuw maken van een verzameling met Hallo dezelfde naam.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="2ac5a-174">Toegevoegde veelhoek en LineString DataTypes tijdens het opgeven van de verzameling beleid voor geofencing ruimtelijke query's te indexeren.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="2ac5a-175">Opgeloste problemen met Java Doc voor Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="2ac5a-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="2ac5a-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="2ac5a-177">Heeft een fout in de PartitionKeyDefinitionMap ophalen toocache verzamelingen met één partitie en niet Maak extra partitie sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="2ac5a-178">Een bug toonot opnieuw vast als een waarde voor de onjuiste partitiesleutel beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="2ac5a-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="2ac5a-180">Hallo toegevoegde ondersteuning voor meerdere landen/regio database accounts.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="2ac5a-181">Ondersteuning toegevoegd voor automatische nieuwe pogingen voor beperkte verzoeken met opties toocustomize Hallo max nieuwe pogingen en max wachttijd.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="2ac5a-182">Zie RetryOptions en ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="2ac5a-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="2ac5a-183">Afgeschafte IPartitionResolver op basis van aangepaste partitionering code.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="2ac5a-184">Gebruik gepartitioneerde verzamelingen voor hogere opslag en doorvoer.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="2ac5a-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="2ac5a-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="2ac5a-186">Toegevoegde opnieuw Beleidsondersteuning voor beperking.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="2ac5a-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="2ac5a-188">Tijd toolive (TTL) is ondersteuning toegevoegd voor documenten.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="2ac5a-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="2ac5a-190">Geïmplementeerd [gepartitioneerde verzamelingen](partition-data.md) en [prestatieniveaus die door de gebruiker gedefinieerde](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="2ac5a-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="2ac5a-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="2ac5a-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="2ac5a-192">Heeft een fout in de HashPartitionResolver toogenerate hash-waarden in little endian toobe consistent met andere SDK.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="2ac5a-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="2ac5a-194">Toevoegen van hash- & bereik partitie resolvers tooassist met sharding-toepassingen op verschillende partities.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="2ac5a-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="2ac5a-196">Upsert implementeren.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-196">Implement Upsert.</span></span> <span data-ttu-id="2ac5a-197">Nieuwe upsertXXX methoden toosupport Upsert functie toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="2ac5a-198">ID gebaseerde routering wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-198">Implement ID Based Routing.</span></span> <span data-ttu-id="2ac5a-199">Er zijn geen openbare API-wijzigingen, worden alle wijzigingen interne.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="2ac5a-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="2ac5a-201">Release overgeslagen toobring versienummer in uitlijning met andere SDK</span><span class="sxs-lookup"><span data-stu-id="2ac5a-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="2ac5a-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="2ac5a-203">Ondersteunt georuimtelijke Index</span><span class="sxs-lookup"><span data-stu-id="2ac5a-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="2ac5a-204">De eigenschap id voor alle resources valideert.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-204">Validates id property for all resources.</span></span> <span data-ttu-id="2ac5a-205">Kunnen geen id's voor bronnen bevatten?, /, #, \, tekens of eindigen met een spatie.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="2ac5a-206">Voegt nieuwe header 'index transformatie uitgevoerd' tooResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="2ac5a-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="2ac5a-208">V2-indexeringsbeleid implementeert</span><span class="sxs-lookup"><span data-stu-id="2ac5a-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="2ac5a-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="2ac5a-210">GA SDK</span><span class="sxs-lookup"><span data-stu-id="2ac5a-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="2ac5a-211">Release & buiten gebruik stellen datums</span><span class="sxs-lookup"><span data-stu-id="2ac5a-211">Release & Retirement Dates</span></span>
<span data-ttu-id="2ac5a-212">Microsoft biedt melding ten minste **12 maanden** voordat het buiten gebruik stellen van een SDK in de volgorde toosmooth Hallo overgang tooa nieuwere/ondersteunde versie.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="2ac5a-213">Nieuwe functies en functionaliteit en optimalisaties worden alleen toegevoegd toohello huidige SDK als zodanig verdient het voorkeur dat u altijd upgrade toohello nieuwste SDK versie zo spoedig mogelijk.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="2ac5a-214">Een aanvraag tooCosmos DB met een buiten gebruik gestelde SDK worden geweigerd door Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="2ac5a-215">Alle versies van Hallo DocumentDB SDK voor Java voorafgaande tooversion **1.0.0** wordt buiten gebruik worden gesteld op **29 februari 2016**.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="2ac5a-216">Versie</span><span class="sxs-lookup"><span data-stu-id="2ac5a-216">Version</span></span> | <span data-ttu-id="2ac5a-217">Releasedatum</span><span class="sxs-lookup"><span data-stu-id="2ac5a-217">Release Date</span></span> | <span data-ttu-id="2ac5a-218">Vervaldatum</span><span class="sxs-lookup"><span data-stu-id="2ac5a-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="2ac5a-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="2ac5a-220">11 juli 2017</span><span class="sxs-lookup"><span data-stu-id="2ac5a-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="2ac5a-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="2ac5a-222">10 mei 2017</span><span class="sxs-lookup"><span data-stu-id="2ac5a-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="2ac5a-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="2ac5a-224">11 maart 2017</span><span class="sxs-lookup"><span data-stu-id="2ac5a-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="2ac5a-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="2ac5a-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="2ac5a-226">21 februari 2017</span><span class="sxs-lookup"><span data-stu-id="2ac5a-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="2ac5a-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="2ac5a-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="2ac5a-228">31 januari 2017</span><span class="sxs-lookup"><span data-stu-id="2ac5a-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="2ac5a-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="2ac5a-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="2ac5a-230">24 november 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="2ac5a-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="2ac5a-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="2ac5a-232">30 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="2ac5a-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="2ac5a-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="2ac5a-234">28 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="2ac5a-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="2ac5a-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="2ac5a-236">26 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="2ac5a-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="2ac5a-238">03 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="2ac5a-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="2ac5a-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="2ac5a-240">30 juni 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="2ac5a-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="2ac5a-242">14 juni 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="2ac5a-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="2ac5a-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="2ac5a-244">30 april 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="2ac5a-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="2ac5a-246">27 april 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="2ac5a-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="2ac5a-248">29 maart 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="2ac5a-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="2ac5a-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="2ac5a-250">31 december 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="2ac5a-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="2ac5a-252">04 december 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="2ac5a-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="2ac5a-254">05 oktober 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="2ac5a-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="2ac5a-256">05 oktober 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="2ac5a-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="2ac5a-258">05 augustus 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="2ac5a-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="2ac5a-260">09 juli 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="2ac5a-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="2ac5a-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="2ac5a-262">12 mei 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="2ac5a-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="2ac5a-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="2ac5a-264">07 april 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="2ac5a-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="2ac5a-265">0.9.5-prelease</span></span> |<span data-ttu-id="2ac5a-266">09 mrt 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-266">Mar 09, 2015</span></span> |<span data-ttu-id="2ac5a-267">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-267">February 29, 2016</span></span> |
| <span data-ttu-id="2ac5a-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="2ac5a-268">0.9.4-prelease</span></span> |<span data-ttu-id="2ac5a-269">17 februari 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-269">February 17, 2015</span></span> |<span data-ttu-id="2ac5a-270">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-270">February 29, 2016</span></span> |
| <span data-ttu-id="2ac5a-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="2ac5a-271">0.9.3-prelease</span></span> |<span data-ttu-id="2ac5a-272">13 januari 2015</span><span class="sxs-lookup"><span data-stu-id="2ac5a-272">January 13, 2015</span></span> |<span data-ttu-id="2ac5a-273">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-273">February 29, 2016</span></span> |
| <span data-ttu-id="2ac5a-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="2ac5a-274">0.9.2-prelease</span></span> |<span data-ttu-id="2ac5a-275">19 december 2014</span><span class="sxs-lookup"><span data-stu-id="2ac5a-275">December 19, 2014</span></span> |<span data-ttu-id="2ac5a-276">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-276">February 29, 2016</span></span> |
| <span data-ttu-id="2ac5a-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="2ac5a-277">0.9.1-prelease</span></span> |<span data-ttu-id="2ac5a-278">19 december 2014</span><span class="sxs-lookup"><span data-stu-id="2ac5a-278">December 19, 2014</span></span> |<span data-ttu-id="2ac5a-279">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-279">February 29, 2016</span></span> |
| <span data-ttu-id="2ac5a-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="2ac5a-280">0.9.0-prelease</span></span> |<span data-ttu-id="2ac5a-281">10 december 2014</span><span class="sxs-lookup"><span data-stu-id="2ac5a-281">December 10, 2014</span></span> |<span data-ttu-id="2ac5a-282">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="2ac5a-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="2ac5a-283">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="2ac5a-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="2ac5a-284">Zie ook</span><span class="sxs-lookup"><span data-stu-id="2ac5a-284">See Also</span></span>
<span data-ttu-id="2ac5a-285">Zie toolearn meer informatie over de Cosmos-DB [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) pagina van de service.</span><span class="sxs-lookup"><span data-stu-id="2ac5a-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

