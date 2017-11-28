---
title: aaaAzure Cosmos DB Node.js-API SDK & Resources | Microsoft Docs
description: Meer informatie over Hallo Node.js-API en SDK, inclusief release datums, buiten gebruik stellen datums en wijzigingen die zijn aangebracht tussen elke versie van hello Azure Cosmos DB Node.js SDK.
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
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="d1ae4-103">Azure DB Cosmos Node.js SDK: Releaseopmerkingen en resources</span><span class="sxs-lookup"><span data-stu-id="d1ae4-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1ae4-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d1ae4-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="d1ae4-105">.NET-Feed van wijzigen</span><span class="sxs-lookup"><span data-stu-id="d1ae4-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="d1ae4-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d1ae4-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="d1ae4-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="d1ae4-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="d1ae4-108">Java</span><span class="sxs-lookup"><span data-stu-id="d1ae4-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="d1ae4-109">Python</span><span class="sxs-lookup"><span data-stu-id="d1ae4-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="d1ae4-110">REST</span><span class="sxs-lookup"><span data-stu-id="d1ae4-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="d1ae4-111">REST-resourceprovider</span><span class="sxs-lookup"><span data-stu-id="d1ae4-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="d1ae4-112">SQL</span><span class="sxs-lookup"><span data-stu-id="d1ae4-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="d1ae4-113">**SDK downloaden**</span><span class="sxs-lookup"><span data-stu-id="d1ae4-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="d1ae4-114">NPM</span><span class="sxs-lookup"><span data-stu-id="d1ae4-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="d1ae4-115">**API-documentatie**</span><span class="sxs-lookup"><span data-stu-id="d1ae4-115">**API documentation**</span></span></td><td>[<span data-ttu-id="d1ae4-116">Node.js-API-naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="d1ae4-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="d1ae4-117">**SDK-installatie-instructies**</span><span class="sxs-lookup"><span data-stu-id="d1ae4-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="d1ae4-118">Installatie-instructies</span><span class="sxs-lookup"><span data-stu-id="d1ae4-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="d1ae4-119">**Bijdragen tooSDK**</span><span class="sxs-lookup"><span data-stu-id="d1ae4-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="d1ae4-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="d1ae4-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="d1ae4-121">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="d1ae4-121">**Samples**</span></span></td><td>[<span data-ttu-id="d1ae4-122">Node.js-codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="d1ae4-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="d1ae4-123">**Zelfstudie Aan de slag**</span><span class="sxs-lookup"><span data-stu-id="d1ae4-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="d1ae4-124">Aan de slag met Hallo Node.js-SDK</span><span class="sxs-lookup"><span data-stu-id="d1ae4-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="d1ae4-125">**Zelfstudie voor web-app**</span><span class="sxs-lookup"><span data-stu-id="d1ae4-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="d1ae4-126">Een Node.js-webtoepassing met behulp van Azure DB die Cosmos bouwen</span><span class="sxs-lookup"><span data-stu-id="d1ae4-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="d1ae4-127">**Huidige ondersteund platform**</span><span class="sxs-lookup"><span data-stu-id="d1ae4-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="d1ae4-128">Node.js versie 6.x</span><span class="sxs-lookup"><span data-stu-id="d1ae4-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="d1ae4-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="d1ae4-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="d1ae4-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="d1ae4-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="d1ae4-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="d1ae4-132">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="d1ae4-132">Release notes</span></span>

### <span data-ttu-id="d1ae4-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="d1ae4-134">npm documentatie is opgelost.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-134">npm documentation fixed.</span></span>

### <span data-ttu-id="d1ae4-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="d1ae4-136">Heeft een fout in de executeStoredProcedure documenten die betrokken zijn waar speciale Unicode-tekens (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="d1ae4-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="d1ae4-137">Een fout bij het verwerken van documenten met Unicode-tekens in de partitiesleutel Hallo vast.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="d1ae4-138">Vaste ondersteuning voor het maken van verzamelingen met Hallo naam media.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="d1ae4-139">Github probleem #114.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-139">Github issue #114.</span></span>
* <span data-ttu-id="d1ae4-140">Vaste ondersteuning voor machtiging verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="d1ae4-141">Github probleem #178.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-141">Github issue #178.</span></span>

### <span data-ttu-id="d1ae4-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="d1ae4-143">Ondersteuning toegevoegd voor een nieuwe [consistentieniveau](consistency-levels.md) ConsistentPrefix aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="d1ae4-144">Ondersteuning toegevoegd voor UriFactory.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="d1ae4-145">Vaste een bug Unicode-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="d1ae4-146">GitHub probleem #171.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-146">GitHub issue #171.</span></span>

### <span data-ttu-id="d1ae4-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="d1ae4-148">Hallo toegevoegde ondersteuning voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem.).</span><span class="sxs-lookup"><span data-stu-id="d1ae4-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="d1ae4-149">Toegevoegde Hallo-optie voor het beheren van de mate van parallelle uitvoering voor cross-partitie query's.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="d1ae4-150">Toegevoegde Hallo-optie voor het uitschakelen van SSL-verificatie bij het uitvoeren in Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="d1ae4-151">Minimaal doorvoer voor gepartitioneerde verzamelingen uit 10,100 RU/s too2500 RU/s verlaagd.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="d1ae4-152">Vaste Hallo voortzetting token oplossingen voor de verzameling van één partitie.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="d1ae4-153">Github probleem #107.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-153">Github issue #107.</span></span>
* <span data-ttu-id="d1ae4-154">Vaste Hallo executeStoredProcedure fout bij het verwerken van 0 als één param.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="d1ae4-155">Github probleem #155.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-155">Github issue #155.</span></span>

### <span data-ttu-id="d1ae4-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="d1ae4-157">Vaste gebruikersagent header tooinclude Hallo SDK-versie.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="d1ae4-158">Het opruimen van de secundaire code.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-158">Minor code cleanup.</span></span>

### <span data-ttu-id="d1ae4-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="d1ae4-160">SSL-verificatie wordt uitgeschakeld wanneer u Hallo SDK tootarget hello emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="d1ae4-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="d1ae4-161">Ondersteuning toegevoegd voor het inschakelen van logboekregistratie script tijdens het uitvoeren van de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="d1ae4-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="d1ae4-163">Ondersteuning toegevoegd voor cross-partitie parallelle query's.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="d1ae4-164">Ondersteuning toegevoegd voor TOP/ORDER BY-query's voor gepartitioneerde verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="d1ae4-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="d1ae4-166">Toegevoegde opnieuw Beleidsondersteuning voor beperkte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="d1ae4-167">(Beperkte aanvragen ontvangen van een aanvraag snelheid te groot uitzondering, foutcode 429.) Standaard Azure Cosmos DB pogingen negen keer voor elke aanvraag wanneer foutcode 429 is opgetreden, Hallo retryAfter tijd in Hallo antwoordheader naleven.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="d1ae4-168">Een vaste opnieuw tijdsinterval kan nu worden ingesteld als onderdeel van Hallo RetryOptions-eigenschap op Hallo ConnectionPolicy object als u wilt dat tooignore hello retryAfter tijd geretourneerd door server tussen nieuwe pogingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="d1ae4-169">Azure Cosmos-DB wordt nu gewacht op maximaal 30 seconden voor elke aanvraag die wordt beperkt (ongeacht het aantal pogingen) en het Hallo-antwoord met foutcode 429 retourneert.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="d1ae4-170">Deze tijd kan ook worden overschreven in Hallo RetryOptions-eigenschap op ConnectionPolicy-object.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="d1ae4-171">Cosmos DB retourneert nu x-ms-versnelling-aantal nieuwe pogingen en x-ms-throttle-retry-wait-time-ms Hallo antwoordheaders in elke aanvraag toodenote Hallo versnelling probeer telling en het Hallo cumulatieve tijd Hallo aanvragen tussen nieuwe pogingen Hallo gewacht.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="d1ae4-172">Hallo RetryOptions klasse werd toegevoegd, Hallo RetryOptions eigenschap blootstellen op Hallo ConnectionPolicy klasse die gebruikt toooverride worden kan Hallo standaard aantal opties voor nieuw pogingen.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="d1ae4-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="d1ae4-174">Hallo toegevoegde ondersteuning voor meerdere landen/regio database accounts.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="d1ae4-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="d1ae4-176">Toegevoegde Hallo ondersteuning voor de functie voor tooLive(TTL) voor documenten.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="d1ae4-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="d1ae4-178">Geïmplementeerd [gepartitioneerde verzamelingen](partition-data.md) en [prestatieniveaus die door de gebruiker gedefinieerde](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d1ae4-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="d1ae4-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="d1ae4-180">Vaste RangePartitionResolver.resolveForRead bug waar koppelingen vanwege ongeldige concat tooa resultaten is niet geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="d1ae4-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="d1ae4-182">Vaste hashParitionResolver resolveForRead(): wanneer geen partitiesleutel opgegeven is er uitzondering is opgetreden, in plaats van een lijst met alle geregistreerde koppelingen retourneren.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="d1ae4-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="d1ae4-184">Probleem opgelost [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -Agent voor HTTPS-specifieke: voorkomen Hallo globale agent voor Azure Cosmos DB doeleinden wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="d1ae4-185">Een speciale agent gebruiken voor alle aanvragen van Hallo lib.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="d1ae4-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="d1ae4-187">Probleem opgelost [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - goed streepjes in de media-ID's verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="d1ae4-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="d1ae4-189">Probleem opgelost [#95](https://github.com/Azure/azure-documentdb-node/issues/95) -listener EventEmitter lekken waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="d1ae4-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="d1ae4-191">Probleem opgelost [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -Wijzig de naam van Hash-toohash map voor systemen die hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="d1ae4-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="d1ae4-193">Implementeer sharding ondersteuning door hash & bereik partitie resolvers toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="d1ae4-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="d1ae4-195">Upsert implementeren.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-195">Implement Upsert.</span></span> <span data-ttu-id="d1ae4-196">Nieuwe upsertXXX-methoden op documentClient.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="d1ae4-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="d1ae4-198">Overgeslagen toobring versienummers realistisch met andere SDK's.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="d1ae4-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="d1ae4-200">Gesplitste Q belooft wrapper toonew opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="d1ae4-201">Update toopackage-bestand voor de npm-register.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="d1ae4-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="d1ae4-203">Implements-ID gebaseerde routering.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="d1ae4-204">Probleem opgelost [#49](https://github.com/Azure/azure-documentdb-node/issues/49) -eigenschap current veroorzaakt een conflict met de methode current().</span><span class="sxs-lookup"><span data-stu-id="d1ae4-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="d1ae4-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="d1ae4-206">Ondersteuning toegevoegd voor georuimtelijke index.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="d1ae4-207">De eigenschap id voor alle resources valideert.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-207">Validates id property for all resources.</span></span> <span data-ttu-id="d1ae4-208">Kunnen geen id's voor bronnen bevatten?, /, #, &#47; &#47; tekens of eindigen met een spatie.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="d1ae4-209">Voegt nieuwe header 'index transformatie uitgevoerd' tooResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="d1ae4-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="d1ae4-211">V2-indexeringsbeleid implementeert.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="d1ae4-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="d1ae4-213">Probleem [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - eslint geïmplementeerd en configuraties in Hallo core knorvis en beloven SDK.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="d1ae4-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="d1ae4-215">Probleem [#45](https://github.com/Azure/azure-documentdb-node/issues/45) -pas wrapper bevat geen header met de fout.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="d1ae4-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="d1ae4-217">Mogelijkheid tooquery voor conflicten door toe te voegen readConflicts readConflictAsync en queryConflicts geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="d1ae4-218">Bijgewerkte API-documentatie.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-218">Updated API documentation.</span></span>
* <span data-ttu-id="d1ae4-219">Probleem [#41](https://github.com/Azure/azure-documentdb-node/issues/41) -client.createDocumentAsync-fout.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="d1ae4-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="d1ae4-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="d1ae4-221">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="d1ae4-222">Release & buiten gebruik stellen datums</span><span class="sxs-lookup"><span data-stu-id="d1ae4-222">Release & Retirement Dates</span></span>
<span data-ttu-id="d1ae4-223">Microsoft biedt melding ten minste **12 maanden** voordat het buiten gebruik stellen van een SDK in de volgorde toosmooth Hallo overgang tooa nieuwere/ondersteunde versie.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="d1ae4-224">Nieuwe functies en functionaliteit en optimalisaties worden alleen toegevoegd toohello huidige SDK, omdat het wordt aanbevolen dat u altijd upgrade toohello nieuwste SDK-versie zo spoedig mogelijk.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="d1ae4-225">Elk verzoek tooCosmos DB met een buiten gebruik gestelde SDK is geweigerd door Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="d1ae4-226">Versie</span><span class="sxs-lookup"><span data-stu-id="d1ae4-226">Version</span></span> | <span data-ttu-id="d1ae4-227">Releasedatum</span><span class="sxs-lookup"><span data-stu-id="d1ae4-227">Release Date</span></span> | <span data-ttu-id="d1ae4-228">Vervaldatum</span><span class="sxs-lookup"><span data-stu-id="d1ae4-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="d1ae4-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="d1ae4-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="d1ae4-230">10 augustus 2017</span><span class="sxs-lookup"><span data-stu-id="d1ae4-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="d1ae4-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="d1ae4-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="d1ae4-232">10 augustus 2017</span><span class="sxs-lookup"><span data-stu-id="d1ae4-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="d1ae4-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="d1ae4-234">10 mei 2017</span><span class="sxs-lookup"><span data-stu-id="d1ae4-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="d1ae4-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="d1ae4-236">16 maart 2017</span><span class="sxs-lookup"><span data-stu-id="d1ae4-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="d1ae4-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="d1ae4-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="d1ae4-238">27 januari 2017</span><span class="sxs-lookup"><span data-stu-id="d1ae4-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="d1ae4-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="d1ae4-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="d1ae4-240">22 december 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="d1ae4-242">03 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="d1ae4-244">07 juli 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="d1ae4-246">14 juni 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="d1ae4-248">26 april 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="d1ae4-250">29 maart 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="d1ae4-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="d1ae4-252">08 maart 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="d1ae4-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="d1ae4-254">02 februari 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="d1ae4-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="d1ae4-256">01 februari 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="d1ae4-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="d1ae4-258">26 januari 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="d1ae4-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="d1ae4-260">22 januari 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="d1ae4-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="d1ae4-262">4 januari 2016</span><span class="sxs-lookup"><span data-stu-id="d1ae4-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="d1ae4-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="d1ae4-264">31 december 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="d1ae4-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="d1ae4-266">06 oktober 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="d1ae4-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="d1ae4-268">06 oktober 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="d1ae4-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="d1ae4-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="d1ae4-270">10 september 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="d1ae4-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="d1ae4-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="d1ae4-272">15 augustus 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="d1ae4-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="d1ae4-274">05 augustus 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="d1ae4-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="d1ae4-276">09 juli 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="d1ae4-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="d1ae4-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="d1ae4-278">04 juni 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="d1ae4-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="d1ae4-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="d1ae4-280">23 mei 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="d1ae4-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="d1ae4-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="d1ae4-282">Op 15 mei 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="d1ae4-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="d1ae4-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="d1ae4-284">08 april 2015</span><span class="sxs-lookup"><span data-stu-id="d1ae4-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="d1ae4-285">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="d1ae4-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="d1ae4-286">Zie ook</span><span class="sxs-lookup"><span data-stu-id="d1ae4-286">See also</span></span>
<span data-ttu-id="d1ae4-287">Zie toolearn meer informatie over de Cosmos-DB [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) pagina van de service.</span><span class="sxs-lookup"><span data-stu-id="d1ae4-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

