---
title: aaaAzure Cosmos DB Python API SDK & Resources | Microsoft Docs
description: Meer informatie over Hallo Python-API en SDK, inclusief release datums, buiten gebruik stellen datums en wijzigingen die zijn aangebracht tussen elke versie van hello Azure Cosmos DB Python SDK.
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="f2a9c-103">Azure DB Cosmos Python SDK: Releaseopmerkingen en resources</span><span class="sxs-lookup"><span data-stu-id="f2a9c-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2a9c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f2a9c-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="f2a9c-105">.NET-Feed van wijzigen</span><span class="sxs-lookup"><span data-stu-id="f2a9c-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="f2a9c-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f2a9c-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="f2a9c-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f2a9c-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="f2a9c-108">Java</span><span class="sxs-lookup"><span data-stu-id="f2a9c-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="f2a9c-109">Python</span><span class="sxs-lookup"><span data-stu-id="f2a9c-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="f2a9c-110">REST</span><span class="sxs-lookup"><span data-stu-id="f2a9c-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="f2a9c-111">REST-resourceprovider</span><span class="sxs-lookup"><span data-stu-id="f2a9c-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="f2a9c-112">SQL</span><span class="sxs-lookup"><span data-stu-id="f2a9c-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="f2a9c-113">**SDK downloaden**</span><span class="sxs-lookup"><span data-stu-id="f2a9c-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="f2a9c-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="f2a9c-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="f2a9c-115">**API-documentatie**</span><span class="sxs-lookup"><span data-stu-id="f2a9c-115">**API documentation**</span></span></td><td>[<span data-ttu-id="f2a9c-116">Python-API-naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="f2a9c-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="f2a9c-117">**SDK-installatie-instructies**</span><span class="sxs-lookup"><span data-stu-id="f2a9c-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="f2a9c-118">Python SDK installatie-instructies</span><span class="sxs-lookup"><span data-stu-id="f2a9c-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="f2a9c-119">**Bijdragen tooSDK**</span><span class="sxs-lookup"><span data-stu-id="f2a9c-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="f2a9c-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="f2a9c-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="f2a9c-121">**Aan de slag**</span><span class="sxs-lookup"><span data-stu-id="f2a9c-121">**Get started**</span></span></td><td>[<span data-ttu-id="f2a9c-122">Aan de slag met Hallo Python SDK</span><span class="sxs-lookup"><span data-stu-id="f2a9c-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="f2a9c-123">**Huidige ondersteund platform**</span><span class="sxs-lookup"><span data-stu-id="f2a9c-123">**Current supported platform**</span></span></td><td><span data-ttu-id="f2a9c-124">[Python 2.7](https://www.python.org/downloads/) en [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="f2a9c-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="f2a9c-125">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="f2a9c-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="f2a9c-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="f2a9c-127">Ondersteuning toegevoegd voor een nieuwe consistentieniveau ConsistentPrefix genoemd.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="f2a9c-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="f2a9c-129">Ondersteuning toegevoegd voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem).</span><span class="sxs-lookup"><span data-stu-id="f2a9c-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="f2a9c-130">Een optie voor het uitschakelen van SSL-verificatie bij het uitvoeren in Cosmos DB Emulator toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="f2a9c-131">Hallo-beperking van de afhankelijke aanvragen module toobe exact 2.10.0 verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="f2a9c-132">Minimaal doorvoer voor gepartitioneerde verzamelingen uit 10,100 RU/s too2500 RU/s verlaagd.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="f2a9c-133">Ondersteuning toegevoegd voor het inschakelen van logboekregistratie script tijdens het uitvoeren van de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="f2a9c-134">REST-API-versie tegenaan te ' 2017-01-19' in deze versie.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="f2a9c-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="f2a9c-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="f2a9c-136">Redactionele wijzigingen aangebracht in toodocumentation opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="f2a9c-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="f2a9c-138">Ondersteuning toegevoegd voor Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="f2a9c-139">Ondersteuning toegevoegd voor verbindingsgroepering met een module aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="f2a9c-140">Ondersteuning toegevoegd voor sessieconsistentie.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-140">Added support for session consistency.</span></span>
* <span data-ttu-id="f2a9c-141">Ondersteuning toegevoegd voor TOP/ORDERBY-query's voor gepartitioneerde verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="f2a9c-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="f2a9c-143">Toegevoegde opnieuw Beleidsondersteuning voor beperkte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="f2a9c-144">(Beperkte aanvragen ontvangen van een aanvraag snelheid te groot uitzondering, foutcode 429.) Standaard Azure Cosmos DB pogingen negen keer voor elke aanvraag wanneer foutcode 429 is opgetreden, Hallo retryAfter tijd in Hallo antwoordheader naleven.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="f2a9c-145">Een vaste opnieuw tijdsinterval kan nu worden ingesteld als onderdeel van Hallo RetryOptions-eigenschap op Hallo ConnectionPolicy object als u wilt dat tooignore hello retryAfter tijd geretourneerd door server tussen nieuwe pogingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="f2a9c-146">Azure Cosmos-DB wordt nu gewacht op maximaal 30 seconden voor elke aanvraag die wordt beperkt (ongeacht het aantal pogingen) en het Hallo-antwoord met foutcode 429 retourneert.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="f2a9c-147">Deze tijd kan ook worden onderdrukt in Hallo RetryOptions-eigenschap op ConnectionPolicy-object.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="f2a9c-148">Cosmos DB retourneert nu x-ms-versnelling-aantal nieuwe pogingen en x-ms-throttle-retry-wait-time-ms Hallo antwoordheaders in elke aanvraag toodenote Hallo versnelling probeer telling en het Hallo cummulative keer Hallo gewacht tussen pogingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="f2a9c-149">Verwijderde Hallo RetryPolicy klasse en bijbehorende Hallo-eigenschap (retry_policy) op Hallo document_client klasse worden weergegeven en in plaats daarvan een RetryOptions klasse blootstellen Hallo RetryOptions eigenschap voor ConnectionPolicy-klasse die gebruikt toooverride worden kan geïntroduceerd Sommige van de standaard Hallo opties voor nieuw pogingen.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="f2a9c-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="f2a9c-151">Hallo toegevoegde ondersteuning voor meerdere landen/regio database accounts.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="f2a9c-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="f2a9c-153">Toegevoegde Hallo ondersteuning voor de functie voor tooLive(TTL) voor documenten.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="f2a9c-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="f2a9c-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="f2a9c-155">Oplossingen voor problemen die betrekking tooserver side tooallow speciale tekens in pad partitionkey partitioneren.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="f2a9c-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="f2a9c-157">Geïmplementeerd [gepartitioneerde verzamelingen](partition-data.md) en [prestatieniveaus die door de gebruiker gedefinieerde](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="f2a9c-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="f2a9c-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="f2a9c-159">Toevoegen van hash- & bereik partitie resolvers tooassist met sharding-toepassingen op verschillende partities.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="f2a9c-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="f2a9c-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="f2a9c-161">Upsert implementeren.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-161">Implement Upsert.</span></span> <span data-ttu-id="f2a9c-162">Nieuwe UpsertXXX methoden toosupport Upsert functie toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="f2a9c-163">ID gebaseerde routering wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-163">Implement ID Based Routing.</span></span> <span data-ttu-id="f2a9c-164">Er zijn geen openbare API-wijzigingen, worden alle wijzigingen interne.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="f2a9c-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="f2a9c-166">Ondersteunt georuimtelijke index.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="f2a9c-167">De eigenschap id voor alle resources valideert.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-167">Validates id property for all resources.</span></span> <span data-ttu-id="f2a9c-168">Kunnen geen id's voor bronnen bevatten?, /, #, \, tekens of eindigen met een spatie.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="f2a9c-169">Voegt nieuwe header 'index transformatie uitgevoerd' tooResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="f2a9c-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="f2a9c-171">V2-indexeringsbeleid implementeert.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="f2a9c-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="f2a9c-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="f2a9c-173">Ondersteunt proxyverbinding.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="f2a9c-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="f2a9c-175">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="f2a9c-176">Release & buiten gebruik stellen datums</span><span class="sxs-lookup"><span data-stu-id="f2a9c-176">Release & retirement dates</span></span>
<span data-ttu-id="f2a9c-177">Microsoft biedt melding ten minste **12 maanden** voordat het buiten gebruik stellen van een SDK in de volgorde toosmooth Hallo overgang tooa nieuwere/ondersteunde versie.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="f2a9c-178">Nieuwe functies en functionaliteit en optimalisaties worden alleen toegevoegd toohello huidige SDK als zodanig verdient het voorkeur dat u altijd upgrade toohello nieuwste SDK versie zo spoedig mogelijk.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="f2a9c-179">Een aanvraag tooCosmos DB met een buiten gebruik gestelde SDK worden geweigerd door Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="f2a9c-180">Alle versies van hello Azure DocumentDB SDK voor Python voorafgaande tooversion **1.0.0** wordt buiten gebruik worden gesteld op **29 februari 2016**.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="f2a9c-181">Versie</span><span class="sxs-lookup"><span data-stu-id="f2a9c-181">Version</span></span> | <span data-ttu-id="f2a9c-182">Releasedatum</span><span class="sxs-lookup"><span data-stu-id="f2a9c-182">Release Date</span></span> | <span data-ttu-id="f2a9c-183">Vervaldatum</span><span class="sxs-lookup"><span data-stu-id="f2a9c-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="f2a9c-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="f2a9c-185">10 mei 2017</span><span class="sxs-lookup"><span data-stu-id="f2a9c-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="f2a9c-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="f2a9c-187">01 mei 2017</span><span class="sxs-lookup"><span data-stu-id="f2a9c-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="f2a9c-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="f2a9c-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="f2a9c-189">30 oktober 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="f2a9c-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="f2a9c-191">29 september 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="f2a9c-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="f2a9c-193">07 juli 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="f2a9c-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="f2a9c-195">14 juni 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="f2a9c-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="f2a9c-197">26 april 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="f2a9c-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="f2a9c-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="f2a9c-199">08 april 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="f2a9c-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="f2a9c-201">29 maart 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="f2a9c-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="f2a9c-203">03 januari 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="f2a9c-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="f2a9c-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="f2a9c-205">06 oktober 2015</span><span class="sxs-lookup"><span data-stu-id="f2a9c-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="f2a9c-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="f2a9c-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="f2a9c-207">06 oktober 2015</span><span class="sxs-lookup"><span data-stu-id="f2a9c-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="f2a9c-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="f2a9c-209">06 augustus 2015</span><span class="sxs-lookup"><span data-stu-id="f2a9c-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="f2a9c-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="f2a9c-211">09 juli 2015</span><span class="sxs-lookup"><span data-stu-id="f2a9c-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="f2a9c-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="f2a9c-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="f2a9c-213">25 mei 2015</span><span class="sxs-lookup"><span data-stu-id="f2a9c-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="f2a9c-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f2a9c-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="f2a9c-215">07 april 2015</span><span class="sxs-lookup"><span data-stu-id="f2a9c-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="f2a9c-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="f2a9c-216">0.9.4-prelease</span></span> |<span data-ttu-id="f2a9c-217">14 januari 2015</span><span class="sxs-lookup"><span data-stu-id="f2a9c-217">January 14, 2015</span></span> |<span data-ttu-id="f2a9c-218">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-218">February 29, 2016</span></span> |
| <span data-ttu-id="f2a9c-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="f2a9c-219">0.9.3-prelease</span></span> |<span data-ttu-id="f2a9c-220">09 december 2014</span><span class="sxs-lookup"><span data-stu-id="f2a9c-220">December 09, 2014</span></span> |<span data-ttu-id="f2a9c-221">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-221">February 29, 2016</span></span> |
| <span data-ttu-id="f2a9c-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="f2a9c-222">0.9.2-prelease</span></span> |<span data-ttu-id="f2a9c-223">25 november 2014</span><span class="sxs-lookup"><span data-stu-id="f2a9c-223">November 25, 2014</span></span> |<span data-ttu-id="f2a9c-224">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-224">February 29, 2016</span></span> |
| <span data-ttu-id="f2a9c-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="f2a9c-225">0.9.1-prelease</span></span> |<span data-ttu-id="f2a9c-226">23 september 2014</span><span class="sxs-lookup"><span data-stu-id="f2a9c-226">September 23, 2014</span></span> |<span data-ttu-id="f2a9c-227">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-227">February 29, 2016</span></span> |
| <span data-ttu-id="f2a9c-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="f2a9c-228">0.9.0-prelease</span></span> |<span data-ttu-id="f2a9c-229">21 augustus 2014</span><span class="sxs-lookup"><span data-stu-id="f2a9c-229">August 21, 2014</span></span> |<span data-ttu-id="f2a9c-230">29 februari 2016</span><span class="sxs-lookup"><span data-stu-id="f2a9c-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="f2a9c-231">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="f2a9c-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="f2a9c-232">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f2a9c-232">See also</span></span>
<span data-ttu-id="f2a9c-233">Zie toolearn meer informatie over de Cosmos-DB [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) pagina van de service.</span><span class="sxs-lookup"><span data-stu-id="f2a9c-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

