---
title: 'Azure Cosmos DB: DocumentDB Java API, SDK en Resources | Microsoft Docs'
description: Meer informatie over de Java-API en de SDK, inclusief release datums, buiten gebruik stellen datums en wijzigingen die zijn aangebracht tussen elke versie van de Azure Cosmos DB DocumentDB Java SDK.
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
ms.openlocfilehash: 15e3f7ef3bfd6b1f61fe6081a378bdb29e0a1aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="0e7e6-103">Azure Cosmos DB: DocumentDB Java SDK-releaseopmerkingen en resources</span><span class="sxs-lookup"><span data-stu-id="0e7e6-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e7e6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0e7e6-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="0e7e6-105">.NET-Feed van wijzigen</span><span class="sxs-lookup"><span data-stu-id="0e7e6-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="0e7e6-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0e7e6-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="0e7e6-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="0e7e6-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="0e7e6-108">Java</span><span class="sxs-lookup"><span data-stu-id="0e7e6-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="0e7e6-109">Python</span><span class="sxs-lookup"><span data-stu-id="0e7e6-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="0e7e6-110">REST</span><span class="sxs-lookup"><span data-stu-id="0e7e6-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="0e7e6-111">REST-resourceprovider</span><span class="sxs-lookup"><span data-stu-id="0e7e6-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="0e7e6-112">SQL</span><span class="sxs-lookup"><span data-stu-id="0e7e6-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="0e7e6-113">**SDK downloaden**</span><span class="sxs-lookup"><span data-stu-id="0e7e6-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="0e7e6-114">Maven</span><span class="sxs-lookup"><span data-stu-id="0e7e6-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="0e7e6-115">**API-documentatie**</span><span class="sxs-lookup"><span data-stu-id="0e7e6-115">**API documentation**</span></span></td><td>[<span data-ttu-id="0e7e6-116">Java-API-naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="0e7e6-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="0e7e6-117">**Bijdragen aan de SDK**</span><span class="sxs-lookup"><span data-stu-id="0e7e6-117">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="0e7e6-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="0e7e6-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="0e7e6-119">**Aan de slag**</span><span class="sxs-lookup"><span data-stu-id="0e7e6-119">**Get started**</span></span></td><td>[<span data-ttu-id="0e7e6-120">Aan de slag met de SDK voor Java</span><span class="sxs-lookup"><span data-stu-id="0e7e6-120">Get started with the Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="0e7e6-121">**Zelfstudie voor web-app**</span><span class="sxs-lookup"><span data-stu-id="0e7e6-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="0e7e6-122">Ontwikkeling van webtoepassing met Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="0e7e6-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="0e7e6-123">**Huidige ondersteunde runtime**</span><span class="sxs-lookup"><span data-stu-id="0e7e6-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="0e7e6-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="0e7e6-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="0e7e6-125">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="0e7e6-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="0e7e6-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="0e7e6-127">Kritieke problemen opgelost voor aanvraagverwerking tijdens splitsingen partitie.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-127">Critical bug fixes to request processing during partition splits.</span></span>
* <span data-ttu-id="0e7e6-128">Een probleem met de sterke en BoundedStaleness consistentieniveaus opgelost.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-128">Fixed an issue with the Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="0e7e6-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="0e7e6-130">Ondersteuning toegevoegd voor een nieuwe consistentieniveau ConsistentPrefix genoemd.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="0e7e6-131">Een fout bij het lezen van de verzameling in sessiemodus vast.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="0e7e6-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="0e7e6-133">Ingeschakelde ondersteuning voor gepartitioneerde verzameling met als geringe als 2500 RU per seconde en schalen in intervallen van 100 RU per seconde.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="0e7e6-134">Een fout in de native assembly waardoor NullRef uitzondering in sommige query's opgelost.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-134">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="0e7e6-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="0e7e6-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="0e7e6-136">De configuratie van de query-engine dat leiden uitzonderingen voor query's in de modus van de Gateway tot kan, een bug vast.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-136">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="0e7e6-137">Enkele fouten in de sessie-container die ertoe leiden een 'Eigenaar bron is niet gevonden'-uitzondering voor aanvragen onmiddellijk na het maken van een siteverzameling dat kan opgelost.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-137">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="0e7e6-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="0e7e6-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="0e7e6-139">Ondersteuning toegevoegd voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem).</span><span class="sxs-lookup"><span data-stu-id="0e7e6-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="0e7e6-140">Zie [aggregatie ondersteuning](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="0e7e6-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="0e7e6-141">Ondersteuning toegevoegd voor de feed wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-141">Added support for change feed.</span></span>
* <span data-ttu-id="0e7e6-142">Ondersteuning toegevoegd voor de verzameling quotum informatie via RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="0e7e6-143">Ondersteuning toegevoegd voor de opgeslagen procedure script logboekregistratie via RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="0e7e6-144">Een bug vast waar query in de modus DirectHttps loopt vast wanneer zich voordoen tijdens versnelling fouten.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="0e7e6-145">Heeft een fout in de sessiemodus consistentie.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="0e7e6-146">Vaste een bug wat leiden NullReferenceException in HttpContext tot kan wanneer aanvraagsnelheid hoog is.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="0e7e6-147">Verbeterde prestaties van DirectHttps-modus.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="0e7e6-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="0e7e6-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="0e7e6-149">Toegevoegde eenvoudige exemplaar, op basis van proxy clientondersteuning met ConnectionPolicy.setProxy()-API.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="0e7e6-150">Toegevoegde DocumentClient.close() API met correct afsluiten DocumentClient exemplaar.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-150">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="0e7e6-151">Verbeterde prestaties van query's in de modus voor directe verbinding met het queryplan die zijn afgeleid van de systeemeigen assembly in plaats van de Gateway.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-151">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span></span>
* <span data-ttu-id="0e7e6-152">Stel FAIL_ON_UNKNOWN_PROPERTIES = false zodat gebruikers hoeven niet te definiëren JsonIgnoreProperties in hun POJO.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="0e7e6-153">Logboekregistratie geherstructureerd SLF4J gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-153">Refactored logging to use SLF4J.</span></span>
* <span data-ttu-id="0e7e6-154">Enkele andere fouten opgelost in de lezer van de consistentie.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="0e7e6-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="0e7e6-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="0e7e6-156">Vaste een bug in het Verbindingsbeheer om te voorkomen dat connection lekken in directe verbinding-modus.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-156">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="0e7e6-157">Vaste een fout in de bovenste query waar deze NullReferenece uitzondering kan genereren.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-157">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="0e7e6-158">Verbeterde prestaties door het aantal netwerkaanroep voor het interne te verminderen.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-158">Improved performance by reducing the number of network call for the internal caches.</span></span>
* <span data-ttu-id="0e7e6-159">Toegevoegde statuscode ActivityID en aanvraag-URI in DocumentClientException als hulpmiddel bij probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="0e7e6-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="0e7e6-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="0e7e6-161">Een probleem opgelost in het Verbindingsbeheer van de voor de stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-161">Fixed an issue in the connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="0e7e6-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="0e7e6-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="0e7e6-163">Ondersteuning toegevoegd voor BoundedStaleness consistentieniveau.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="0e7e6-164">Ondersteuning toegevoegd voor directe verbinding voor CRUD-bewerkingen voor gepartitioneerde verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="0e7e6-165">Heeft een fout in de query voor de database met SQL.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="0e7e6-166">Vaste een fout in de sessiecache waar sessietoken misschien onjuist ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-166">Fixed a bug in the session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="0e7e6-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="0e7e6-168">Ondersteuning toegevoegd voor cross-partitie parallelle query's.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="0e7e6-169">Ondersteuning toegevoegd voor TOP/ORDER BY-query's voor gepartitioneerde verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="0e7e6-170">Toegevoegde ondersteuning voor sterke consistentie.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="0e7e6-171">Ondersteuning toegevoegd voor aanvragen van een naam op basis van wanneer u directe verbinding.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="0e7e6-172">Vaste aanbrengen ActivityId blijven consistent op alle nieuwe aanvraagpogingen.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-172">Fixed to make ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="0e7e6-173">Vaste een bug die betrekking hebben op de sessiecache bij het opnieuw genereren van een verzameling met dezelfde naam.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-173">Fixed a bug related to the session cache when recreating a collection with the same name.</span></span>
* <span data-ttu-id="0e7e6-174">Toegevoegde veelhoek en LineString DataTypes tijdens het opgeven van de verzameling beleid voor geofencing ruimtelijke query's te indexeren.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="0e7e6-175">Opgeloste problemen met Java Doc voor Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="0e7e6-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="0e7e6-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="0e7e6-177">Heeft een fout in de PartitionKeyDefinitionMap naar verzamelingen met één partitie in de cache en extra ophalen die sleutels aanvragen partitie te maken.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-177">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="0e7e6-178">Een fout bij het niet opnieuw uitgevoerd als een waarde voor de onjuiste partitiesleutel beschikbaar is opgelost.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-178">Fixed a bug to not retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="0e7e6-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="0e7e6-180">De ondersteuning voor meerdere landen/regio database accounts toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-180">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="0e7e6-181">Ondersteuning toegevoegd voor automatische nieuwe pogingen voor beperkte verzoeken met opties voor het maximale aantal pogingen en de maximale wachttijd aanpassen.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-181">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="0e7e6-182">Zie RetryOptions en ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="0e7e6-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="0e7e6-183">Afgeschafte IPartitionResolver op basis van aangepaste partitionering code.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="0e7e6-184">Gebruik gepartitioneerde verzamelingen voor hogere opslag en doorvoer.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="0e7e6-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="0e7e6-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="0e7e6-186">Toegevoegde opnieuw Beleidsondersteuning voor beperking.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="0e7e6-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="0e7e6-188">Toegevoegde tijd live (TTL) ondersteuning voor documenten.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-188">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="0e7e6-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="0e7e6-190">Geïmplementeerd [gepartitioneerde verzamelingen](partition-data.md) en [prestatieniveaus die door de gebruiker gedefinieerde](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e6-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="0e7e6-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="0e7e6-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="0e7e6-192">Heeft een fout in de HashPartitionResolver voor het genereren van hash-waarden in little endian consistent met andere SDK's.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-192">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="0e7e6-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="0e7e6-194">Toevoegen van hash- & bereik partitie-resolvers om te helpen bij sharding-toepassingen op verschillende partities.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-194">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="0e7e6-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="0e7e6-196">Upsert implementeren.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-196">Implement Upsert.</span></span> <span data-ttu-id="0e7e6-197">Nieuwe upsertXXX methoden toegevoegd ter ondersteuning van Upsert-functie.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-197">New upsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="0e7e6-198">ID gebaseerde routering wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-198">Implement ID Based Routing.</span></span> <span data-ttu-id="0e7e6-199">Er zijn geen openbare API-wijzigingen, worden alle wijzigingen interne.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="0e7e6-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="0e7e6-201">Release overgeslagen op te zetten versienummer in uitlijning met andere SDK</span><span class="sxs-lookup"><span data-stu-id="0e7e6-201">Release skipped to bring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="0e7e6-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="0e7e6-203">Ondersteunt georuimtelijke Index</span><span class="sxs-lookup"><span data-stu-id="0e7e6-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="0e7e6-204">De eigenschap id voor alle resources valideert.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-204">Validates id property for all resources.</span></span> <span data-ttu-id="0e7e6-205">Kunnen geen id's voor bronnen bevatten?, /, #, \, tekens of eindigen met een spatie.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="0e7e6-206">Voegt nieuwe header 'index transformatie uitgevoerd' aan ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-206">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="0e7e6-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="0e7e6-208">V2-indexeringsbeleid implementeert</span><span class="sxs-lookup"><span data-stu-id="0e7e6-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="0e7e6-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="0e7e6-210">GA SDK</span><span class="sxs-lookup"><span data-stu-id="0e7e6-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="0e7e6-211">Release & buiten gebruik stellen datums</span><span class="sxs-lookup"><span data-stu-id="0e7e6-211">Release & Retirement Dates</span></span>
<span data-ttu-id="0e7e6-212">Microsoft biedt melding ten minste **12 maanden** voordat het buiten gebruik stellen van een SDK om de overgang naar een nieuwere/ondersteunde versie vloeiend.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="0e7e6-213">Nieuwe functies en functionaliteit en optimalisaties alleen zijn toegevoegd aan de huidige SDK, als zodanig wordt aanbevolen dat u altijd een upgrade uitvoert naar de nieuwste SDK versie zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-213">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="0e7e6-214">Elk verzoek aan de Cosmos-database met behulp van een buiten gebruik gestelde SDK worden geweigerd door de service.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-214">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="0e7e6-215">Alle versies van de DocumentDB SDK voor Java voorafgaand aan versie **1.0.0** wordt buiten gebruik worden gesteld op **29 februari 2016**.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-215">All versions of the DocumentDB SDK for Java prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="0e7e6-216">Versie</span><span class="sxs-lookup"><span data-stu-id="0e7e6-216">Version</span></span> | <span data-ttu-id="0e7e6-217">Releasedatum</span><span class="sxs-lookup"><span data-stu-id="0e7e6-217">Release Date</span></span> | <span data-ttu-id="0e7e6-218">Vervaldatum</span><span class="sxs-lookup"><span data-stu-id="0e7e6-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="0e7e6-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="0e7e6-220">11 juli 2017</span><span class="sxs-lookup"><span data-stu-id="0e7e6-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="0e7e6-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="0e7e6-222">10 mei 2017</span><span class="sxs-lookup"><span data-stu-id="0e7e6-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="0e7e6-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="0e7e6-224">11 maart 2017</span><span class="sxs-lookup"><span data-stu-id="0e7e6-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="0e7e6-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="0e7e6-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="0e7e6-226">21 februari 2017</span><span class="sxs-lookup"><span data-stu-id="0e7e6-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="0e7e6-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="0e7e6-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="0e7e6-228">31 januari 2017</span><span class="sxs-lookup"><span data-stu-id="0e7e6-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="0e7e6-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="0e7e6-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="0e7e6-230">24 november 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="0e7e6-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="0e7e6-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="0e7e6-232">30 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="0e7e6-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="0e7e6-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="0e7e6-234">28 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="0e7e6-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="0e7e6-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="0e7e6-236">26 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="0e7e6-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="0e7e6-238">03 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="0e7e6-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="0e7e6-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="0e7e6-240">30 juni 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="0e7e6-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="0e7e6-242">14 juni 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="0e7e6-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="0e7e6-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="0e7e6-244">30 april 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="0e7e6-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="0e7e6-246">27 april 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="0e7e6-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="0e7e6-248">29 maart 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="0e7e6-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="0e7e6-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="0e7e6-250">31 december 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="0e7e6-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="0e7e6-252">04 december 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="0e7e6-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="0e7e6-254">05 oktober 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="0e7e6-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="0e7e6-256">05 oktober 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="0e7e6-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="0e7e6-258">05 augustus 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="0e7e6-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="0e7e6-260">09 juli 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="0e7e6-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="0e7e6-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="0e7e6-262">12 mei 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="0e7e6-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="0e7e6-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="0e7e6-264">07 april 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="0e7e6-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="0e7e6-265">0.9.5-prelease</span></span> |<span data-ttu-id="0e7e6-266">09 mrt 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-266">Mar 09, 2015</span></span> |<span data-ttu-id="0e7e6-267">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-267">February 29, 2016</span></span> |
| <span data-ttu-id="0e7e6-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="0e7e6-268">0.9.4-prelease</span></span> |<span data-ttu-id="0e7e6-269">17 februari 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-269">February 17, 2015</span></span> |<span data-ttu-id="0e7e6-270">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-270">February 29, 2016</span></span> |
| <span data-ttu-id="0e7e6-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="0e7e6-271">0.9.3-prelease</span></span> |<span data-ttu-id="0e7e6-272">13 januari 2015</span><span class="sxs-lookup"><span data-stu-id="0e7e6-272">January 13, 2015</span></span> |<span data-ttu-id="0e7e6-273">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-273">February 29, 2016</span></span> |
| <span data-ttu-id="0e7e6-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="0e7e6-274">0.9.2-prelease</span></span> |<span data-ttu-id="0e7e6-275">19 december 2014</span><span class="sxs-lookup"><span data-stu-id="0e7e6-275">December 19, 2014</span></span> |<span data-ttu-id="0e7e6-276">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-276">February 29, 2016</span></span> |
| <span data-ttu-id="0e7e6-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="0e7e6-277">0.9.1-prelease</span></span> |<span data-ttu-id="0e7e6-278">19 december 2014</span><span class="sxs-lookup"><span data-stu-id="0e7e6-278">December 19, 2014</span></span> |<span data-ttu-id="0e7e6-279">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-279">February 29, 2016</span></span> |
| <span data-ttu-id="0e7e6-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="0e7e6-280">0.9.0-prelease</span></span> |<span data-ttu-id="0e7e6-281">10 december 2014</span><span class="sxs-lookup"><span data-stu-id="0e7e6-281">December 10, 2014</span></span> |<span data-ttu-id="0e7e6-282">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="0e7e6-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="0e7e6-283">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="0e7e6-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="0e7e6-284">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0e7e6-284">See Also</span></span>
<span data-ttu-id="0e7e6-285">Zie voor meer informatie over Cosmos DB, [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) pagina van de service.</span><span class="sxs-lookup"><span data-stu-id="0e7e6-285">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

