---
title: Azure Cosmos DB Node.js-API, SDK en Resources | Microsoft Docs
description: Meer informatie over de Node.js-API en de SDK, inclusief release datums, buiten gebruik stellen datums en wijzigingen die zijn aangebracht tussen elke versie van de Azure-SDK voor Node.js Cosmos DB.
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4376a5c07b5f00311ce0fe3c0056efdf79c273f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="d6454-103">Azure DB Cosmos Node.js SDK: Releaseopmerkingen en resources</span><span class="sxs-lookup"><span data-stu-id="d6454-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6454-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d6454-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="d6454-105">.NET-Feed van wijzigen</span><span class="sxs-lookup"><span data-stu-id="d6454-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="d6454-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d6454-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="d6454-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="d6454-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="d6454-108">Java</span><span class="sxs-lookup"><span data-stu-id="d6454-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="d6454-109">Python</span><span class="sxs-lookup"><span data-stu-id="d6454-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="d6454-110">REST</span><span class="sxs-lookup"><span data-stu-id="d6454-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="d6454-111">REST-resourceprovider</span><span class="sxs-lookup"><span data-stu-id="d6454-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="d6454-112">SQL</span><span class="sxs-lookup"><span data-stu-id="d6454-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="d6454-113">**SDK downloaden**</span><span class="sxs-lookup"><span data-stu-id="d6454-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="d6454-114">NPM</span><span class="sxs-lookup"><span data-stu-id="d6454-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="d6454-115">**API-documentatie**</span><span class="sxs-lookup"><span data-stu-id="d6454-115">**API documentation**</span></span></td><td>[<span data-ttu-id="d6454-116">Node.js-API-naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="d6454-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="d6454-117">**SDK-installatie-instructies**</span><span class="sxs-lookup"><span data-stu-id="d6454-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="d6454-118">Installatie-instructies</span><span class="sxs-lookup"><span data-stu-id="d6454-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="d6454-119">**Bijdragen aan de SDK**</span><span class="sxs-lookup"><span data-stu-id="d6454-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="d6454-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="d6454-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="d6454-121">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="d6454-121">**Samples**</span></span></td><td>[<span data-ttu-id="d6454-122">Node.js-codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="d6454-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="d6454-123">**Zelfstudie Aan de slag**</span><span class="sxs-lookup"><span data-stu-id="d6454-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="d6454-124">Aan de slag met de Node.js-SDK</span><span class="sxs-lookup"><span data-stu-id="d6454-124">Get started with the Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="d6454-125">**Zelfstudie voor web-app**</span><span class="sxs-lookup"><span data-stu-id="d6454-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="d6454-126">Een Node.js-webtoepassing met behulp van Azure DB die Cosmos bouwen</span><span class="sxs-lookup"><span data-stu-id="d6454-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="d6454-127">**Huidige ondersteund platform**</span><span class="sxs-lookup"><span data-stu-id="d6454-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="d6454-128">Node.js versie 6.x</span><span class="sxs-lookup"><span data-stu-id="d6454-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="d6454-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="d6454-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="d6454-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="d6454-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="d6454-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="d6454-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="d6454-132">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="d6454-132">Release notes</span></span>

### <span data-ttu-id="d6454-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="d6454-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="d6454-134">npm documentatie is opgelost.</span><span class="sxs-lookup"><span data-stu-id="d6454-134">npm documentation fixed.</span></span>

### <span data-ttu-id="d6454-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="d6454-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="d6454-136">Heeft een fout in de executeStoredProcedure documenten die betrokken zijn waar speciale Unicode-tekens (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="d6454-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="d6454-137">Een fout bij het verwerken van documenten met Unicode-tekens in de partitiesleutel vast.</span><span class="sxs-lookup"><span data-stu-id="d6454-137">Fixed a bug in handling documents with Unicode characters in the partition key.</span></span>
* <span data-ttu-id="d6454-138">Vaste ondersteuning voor het maken van verzamelingen met de naam van media.</span><span class="sxs-lookup"><span data-stu-id="d6454-138">Fixed support for creating collections with the name media.</span></span> <span data-ttu-id="d6454-139">Github probleem #114.</span><span class="sxs-lookup"><span data-stu-id="d6454-139">Github issue #114.</span></span>
* <span data-ttu-id="d6454-140">Vaste ondersteuning voor machtiging verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="d6454-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="d6454-141">Github probleem #178.</span><span class="sxs-lookup"><span data-stu-id="d6454-141">Github issue #178.</span></span>

### <span data-ttu-id="d6454-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="d6454-143">Ondersteuning toegevoegd voor een nieuwe [consistentieniveau](consistency-levels.md) ConsistentPrefix aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d6454-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="d6454-144">Ondersteuning toegevoegd voor UriFactory.</span><span class="sxs-lookup"><span data-stu-id="d6454-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="d6454-145">Vaste een bug Unicode-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="d6454-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="d6454-146">GitHub probleem #171.</span><span class="sxs-lookup"><span data-stu-id="d6454-146">GitHub issue #171.</span></span>

### <span data-ttu-id="d6454-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="d6454-148">Het is ondersteuning toegevoegd voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem).</span><span class="sxs-lookup"><span data-stu-id="d6454-148">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="d6454-149">De optie voor het beheren van de mate van parallelle uitvoering voor cross-partitie query's toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d6454-149">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="d6454-150">De optie voor het uitschakelen van SSL-verificatie bij het uitvoeren in Azure Cosmos DB Emulator toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d6454-150">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="d6454-151">Minimaal doorvoer voor gepartitioneerde verzamelingen uit 10,100 RU/s tot 2500 RU/s verlaagd.</span><span class="sxs-lookup"><span data-stu-id="d6454-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="d6454-152">De voortzetting token oplossingen voor de verzameling van één partitie vast.</span><span class="sxs-lookup"><span data-stu-id="d6454-152">Fixed the continuation token bug for single partition collection.</span></span> <span data-ttu-id="d6454-153">Github probleem #107.</span><span class="sxs-lookup"><span data-stu-id="d6454-153">Github issue #107.</span></span>
* <span data-ttu-id="d6454-154">De executeStoredProcedure-fout bij het verwerken van 0 als één param vast.</span><span class="sxs-lookup"><span data-stu-id="d6454-154">Fixed the executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="d6454-155">Github probleem #155.</span><span class="sxs-lookup"><span data-stu-id="d6454-155">Github issue #155.</span></span>

### <span data-ttu-id="d6454-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="d6454-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="d6454-157">Vaste gebruikersagent header om op te nemen van de SDK-versie.</span><span class="sxs-lookup"><span data-stu-id="d6454-157">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="d6454-158">Het opruimen van de secundaire code.</span><span class="sxs-lookup"><span data-stu-id="d6454-158">Minor code cleanup.</span></span>

### <span data-ttu-id="d6454-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="d6454-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="d6454-160">SSL-verificatie wordt uitgeschakeld wanneer u de SDK toe te passen de emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="d6454-160">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="d6454-161">Ondersteuning toegevoegd voor het inschakelen van logboekregistratie script tijdens het uitvoeren van de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="d6454-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="d6454-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="d6454-163">Ondersteuning toegevoegd voor cross-partitie parallelle query's.</span><span class="sxs-lookup"><span data-stu-id="d6454-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="d6454-164">Ondersteuning toegevoegd voor TOP/ORDER BY-query's voor gepartitioneerde verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="d6454-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="d6454-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="d6454-166">Toegevoegde opnieuw Beleidsondersteuning voor beperkte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="d6454-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="d6454-167">(Beperkte aanvragen ontvangen van een aanvraag snelheid te groot uitzondering, foutcode 429.) Standaard Azure Cosmos DB pogingen negen keer voor elke aanvraag wanneer foutcode 429 is opgetreden, de tijd retryAfter in de antwoordheader naleven.</span><span class="sxs-lookup"><span data-stu-id="d6454-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="d6454-168">Een vaste opnieuw tijdsinterval kan nu worden ingesteld als onderdeel van de eigenschap RetryOptions op het object ConnectionPolicy als u wilt de retryAfter tijd geretourneerd door server tussen de pogingen negeren.</span><span class="sxs-lookup"><span data-stu-id="d6454-168">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="d6454-169">Azure Cosmos-DB wordt nu gewacht op maximaal 30 seconden voor elke aanvraag die wordt beperkt (ongeacht het aantal pogingen) en het antwoord met foutcode 429 retourneert.</span><span class="sxs-lookup"><span data-stu-id="d6454-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="d6454-170">Deze tijd kan ook worden overschreven in de eigenschap RetryOptions in ConnectionPolicy-object.</span><span class="sxs-lookup"><span data-stu-id="d6454-170">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="d6454-171">Cosmos DB retourneert nu x-ms-versnelling-aantal nieuwe pogingen en x-ms-throttle-retry-wait-time-ms de antwoordheaders in elke aanvraag om aan te geven van de beperking probeer aantal en de cumulatieve tijd dat de aanvraag worden gewacht tussen de nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="d6454-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="d6454-172">De klasse RetryOptions is toegevoegd, blootstellen van de eigenschap RetryOptions in de klasse ConnectionPolicy die kan worden gebruikt voor het onderdrukken van enkele van de standaardopties voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="d6454-172">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="d6454-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="d6454-174">De ondersteuning voor meerdere landen/regio database accounts toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d6454-174">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="d6454-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="d6454-176">De ondersteuning voor de functie tijd-Live(TTL) voor documenten toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d6454-176">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="d6454-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="d6454-178">Geïmplementeerd [gepartitioneerde verzamelingen](partition-data.md) en [prestatieniveaus die door de gebruiker gedefinieerde](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d6454-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="d6454-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="d6454-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="d6454-180">Vaste RangePartitionResolver.resolveForRead bug waar koppelingen vanwege een onjuiste concat resultaten is niet geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="d6454-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="d6454-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="d6454-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="d6454-182">Vaste hashParitionResolver resolveForRead(): wanneer geen partitiesleutel opgegeven is er uitzondering is opgetreden, in plaats van een lijst met alle geregistreerde koppelingen retourneren.</span><span class="sxs-lookup"><span data-stu-id="d6454-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="d6454-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="d6454-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="d6454-184">Probleem opgelost [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -Agent voor HTTPS-specifieke: voorkomen wijzigen van de globale agent voor Azure Cosmos DB doeleinden.</span><span class="sxs-lookup"><span data-stu-id="d6454-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="d6454-185">Een speciale agent gebruiken voor alle aanvragen van de lib.</span><span class="sxs-lookup"><span data-stu-id="d6454-185">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="d6454-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="d6454-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="d6454-187">Probleem opgelost [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - goed streepjes in de media-ID's verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d6454-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="d6454-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="d6454-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="d6454-189">Probleem opgelost [#95](https://github.com/Azure/azure-documentdb-node/issues/95) -listener EventEmitter lekken waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="d6454-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="d6454-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="d6454-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="d6454-191">Probleem opgelost [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -naam wijzigen van de map Hash op hash voor systemen die hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="d6454-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span></span>

### <span data-ttu-id="d6454-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="d6454-193">Implementeer sharding ondersteuning door hash & bereik partitie resolvers toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d6454-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="d6454-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="d6454-195">Upsert implementeren.</span><span class="sxs-lookup"><span data-stu-id="d6454-195">Implement Upsert.</span></span> <span data-ttu-id="d6454-196">Nieuwe upsertXXX-methoden op documentClient.</span><span class="sxs-lookup"><span data-stu-id="d6454-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="d6454-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="d6454-198">Overgeslagen zodat versienummers realistisch met andere SDK's.</span><span class="sxs-lookup"><span data-stu-id="d6454-198">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="d6454-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="d6454-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="d6454-200">Gesplitste Q belooft wrapper naar nieuwe opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d6454-200">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="d6454-201">Bijwerken naar pakketbestand voor serverregister npm.</span><span class="sxs-lookup"><span data-stu-id="d6454-201">Update to package file for npm registry.</span></span>

### <span data-ttu-id="d6454-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="d6454-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="d6454-203">Implements-ID gebaseerde routering.</span><span class="sxs-lookup"><span data-stu-id="d6454-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="d6454-204">Probleem opgelost [#49](https://github.com/Azure/azure-documentdb-node/issues/49) -eigenschap current veroorzaakt een conflict met de methode current().</span><span class="sxs-lookup"><span data-stu-id="d6454-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="d6454-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="d6454-206">Ondersteuning toegevoegd voor georuimtelijke index.</span><span class="sxs-lookup"><span data-stu-id="d6454-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="d6454-207">De eigenschap id voor alle resources valideert.</span><span class="sxs-lookup"><span data-stu-id="d6454-207">Validates id property for all resources.</span></span> <span data-ttu-id="d6454-208">Kunnen geen id's voor bronnen bevatten?, /, #, &#47; &#47; tekens of eindigen met een spatie.</span><span class="sxs-lookup"><span data-stu-id="d6454-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="d6454-209">Voegt nieuwe header 'index transformatie uitgevoerd' aan ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="d6454-209">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="d6454-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="d6454-211">V2-indexeringsbeleid implementeert.</span><span class="sxs-lookup"><span data-stu-id="d6454-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="d6454-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="d6454-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="d6454-213">Probleem [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - eslint geïmplementeerd en configuraties in de kern knorvis en beloven SDK.</span><span class="sxs-lookup"><span data-stu-id="d6454-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="d6454-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="d6454-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="d6454-215">Probleem [#45](https://github.com/Azure/azure-documentdb-node/issues/45) -pas wrapper bevat geen header met de fout.</span><span class="sxs-lookup"><span data-stu-id="d6454-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="d6454-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="d6454-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="d6454-217">Geïmplementeerde mogelijkheid om de query voor conflicten door toe te voegen readConflicts readConflictAsync en queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="d6454-217">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="d6454-218">Bijgewerkte API-documentatie.</span><span class="sxs-lookup"><span data-stu-id="d6454-218">Updated API documentation.</span></span>
* <span data-ttu-id="d6454-219">Probleem [#41](https://github.com/Azure/azure-documentdb-node/issues/41) -client.createDocumentAsync-fout.</span><span class="sxs-lookup"><span data-stu-id="d6454-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="d6454-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="d6454-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="d6454-221">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="d6454-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="d6454-222">Release & buiten gebruik stellen datums</span><span class="sxs-lookup"><span data-stu-id="d6454-222">Release & Retirement Dates</span></span>
<span data-ttu-id="d6454-223">Microsoft biedt melding ten minste **12 maanden** voordat het buiten gebruik stellen van een SDK om de overgang naar een nieuwere/ondersteunde versie vloeiend.</span><span class="sxs-lookup"><span data-stu-id="d6454-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="d6454-224">Nieuwe functies en functionaliteit en optimalisaties alleen zijn toegevoegd aan de huidige SDK, als zodanig wordt aanbevolen dat u altijd een upgrade uitvoert naar de nieuwste SDK versie zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="d6454-224">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="d6454-225">Een aanvraag voor het gebruik van de Cosmos-DB dat een buiten gebruik gestelde SDK is geweigerd door de service.</span><span class="sxs-lookup"><span data-stu-id="d6454-225">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="d6454-226">Versie</span><span class="sxs-lookup"><span data-stu-id="d6454-226">Version</span></span> | <span data-ttu-id="d6454-227">Releasedatum</span><span class="sxs-lookup"><span data-stu-id="d6454-227">Release Date</span></span> | <span data-ttu-id="d6454-228">Vervaldatum</span><span class="sxs-lookup"><span data-stu-id="d6454-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="d6454-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="d6454-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="d6454-230">10 augustus 2017</span><span class="sxs-lookup"><span data-stu-id="d6454-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="d6454-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="d6454-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="d6454-232">10 augustus 2017</span><span class="sxs-lookup"><span data-stu-id="d6454-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="d6454-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="d6454-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="d6454-234">10 mei 2017</span><span class="sxs-lookup"><span data-stu-id="d6454-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="d6454-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="d6454-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="d6454-236">16 maart 2017</span><span class="sxs-lookup"><span data-stu-id="d6454-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="d6454-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="d6454-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="d6454-238">27 januari 2017</span><span class="sxs-lookup"><span data-stu-id="d6454-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="d6454-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="d6454-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="d6454-240">22 december 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="d6454-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="d6454-242">03 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="d6454-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="d6454-244">07 juli 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="d6454-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="d6454-246">14 juni 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="d6454-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="d6454-248">26 april 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="d6454-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="d6454-250">29 maart 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="d6454-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="d6454-252">08 maart 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="d6454-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="d6454-254">02 februari 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="d6454-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="d6454-256">01 februari 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="d6454-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="d6454-258">26 januari 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="d6454-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="d6454-260">22 januari 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="d6454-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="d6454-262">4 januari 2016</span><span class="sxs-lookup"><span data-stu-id="d6454-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="d6454-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="d6454-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="d6454-264">31 december 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="d6454-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="d6454-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="d6454-266">06 oktober 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="d6454-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="d6454-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="d6454-268">06 oktober 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="d6454-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="d6454-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="d6454-270">10 september 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="d6454-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="d6454-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="d6454-272">15 augustus 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="d6454-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="d6454-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="d6454-274">05 augustus 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="d6454-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="d6454-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="d6454-276">09 juli 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="d6454-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="d6454-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="d6454-278">04 juni 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="d6454-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="d6454-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="d6454-280">23 mei 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="d6454-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="d6454-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="d6454-282">Op 15 mei 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="d6454-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="d6454-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="d6454-284">08 april 2015</span><span class="sxs-lookup"><span data-stu-id="d6454-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="d6454-285">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="d6454-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="d6454-286">Zie ook</span><span class="sxs-lookup"><span data-stu-id="d6454-286">See also</span></span>
<span data-ttu-id="d6454-287">Zie voor meer informatie over Cosmos DB, [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) pagina van de service.</span><span class="sxs-lookup"><span data-stu-id="d6454-287">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

