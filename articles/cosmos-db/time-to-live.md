---
title: aaaExpire gegevens in Azure Cosmos DB met tijd toolive | Microsoft Docs
description: De TTL biedt Microsoft Azure Cosmos DB Hallo mogelijkheid toohave documenten automatisch opgeschoond van Hallo systeem na een bepaalde periode.
services: cosmos-db
documentationcenter: 
keywords: tijd toolive
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a><span data-ttu-id="3a152-104">Gegevens in Azure Cosmos DB verzamelingen automatisch met tijd toolive verloopt</span><span class="sxs-lookup"><span data-stu-id="3a152-104">Expire data in Azure Cosmos DB collections automatically with time toolive</span></span>
<span data-ttu-id="3a152-105">Toepassingen kunnen maken en opslaan van de enorme hoeveelheden gegevens.</span><span class="sxs-lookup"><span data-stu-id="3a152-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="3a152-106">Sommige van deze gegevens, zoals machine gegenereerde gegevens, logboeken en gebruiker gebeurtenissessie informatie is alleen nuttig voor een beperkte periode.</span><span class="sxs-lookup"><span data-stu-id="3a152-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="3a152-107">Zodra Hallo gegevens wordt overtollige toohello behoeften van de toepassing hello veilige toopurge is deze gegevens en verminderen het Hallo-opslagbehoeften van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="3a152-107">Once hello data becomes surplus toohello needs of hello application it is safe toopurge this data and reduce hello storage needs of an application.</span></span>

<span data-ttu-id="3a152-108">Microsoft Azure Cosmos DB biedt 'keer toolive' of TTL Hallo mogelijkheid toohave documenten automatisch opgeschoond uit Hallo database na een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="3a152-108">With "time toolive" or TTL, Microsoft Azure Cosmos DB provides hello ability toohave documents automatically purged from hello database after a period of time.</span></span> <span data-ttu-id="3a152-109">Hallo standaardtijd toolive worden ingesteld op niveau van de verzameling Hallo en op basis van per document wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="3a152-109">hello default time toolive can be set at hello collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="3a152-110">Zodra TTL is ingesteld, de standaardwaarde voor een verzameling of op het documentniveau van een, wordt Cosmos DB documenten die bestaan na die periode, in seconden, omdat ze het laatst zijn gewijzigd automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3a152-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="3a152-111">Tijd toolive in Cosmos-database maakt gebruik van een offset tegen wanneer Hallo-document voor het laatst is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3a152-111">Time toolive in Cosmos DB uses an offset against when hello document was last modified.</span></span> <span data-ttu-id="3a152-112">toodo hello maakt gebruik van deze deze `_ts` veld dat op elk document bestaat.</span><span class="sxs-lookup"><span data-stu-id="3a152-112">toodo this it uses hello `_ts` field which exists on every document.</span></span> <span data-ttu-id="3a152-113">Hallo _ts veld is een unix-stijl-epoche tijdstempel die Hallo datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="3a152-113">hello _ts field is a unix-style epoch timestamp representing hello date and time.</span></span> <span data-ttu-id="3a152-114">Hallo `_ts` veld wordt telkens bijgewerkt wanneer een document wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3a152-114">hello `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="3a152-115">TTL gedrag</span><span class="sxs-lookup"><span data-stu-id="3a152-115">TTL behavior</span></span>
<span data-ttu-id="3a152-116">Hallo TTL functie wordt bepaald door de TTL-eigenschappen op twee niveaus - Hallo verzameling niveau en Hallo document.</span><span class="sxs-lookup"><span data-stu-id="3a152-116">hello TTL feature is controlled by TTL properties at two levels - hello collection level and hello document level.</span></span> <span data-ttu-id="3a152-117">Hallo-waarden worden ingesteld in seconden en worden behandeld als een delta van Hallo `_ts` dat document Hallo voor het laatst is gewijzigd op.</span><span class="sxs-lookup"><span data-stu-id="3a152-117">hello values are set in seconds and are treated as a delta from hello `_ts` that hello document was last modified at.</span></span>

1. <span data-ttu-id="3a152-118">DefaultTTL voor Hallo-verzameling</span><span class="sxs-lookup"><span data-stu-id="3a152-118">DefaultTTL for hello collection</span></span>
   
   * <span data-ttu-id="3a152-119">Als u documenten ontbreekt (of set toonull) worden niet automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3a152-119">If missing (or set toonull), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="3a152-120">Als deze aanwezig is en het Hallo-waarde is '-' 1 = oneindige – documenten verloopt niet standaard</span><span class="sxs-lookup"><span data-stu-id="3a152-120">If present and hello value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="3a152-121">Als deze aanwezig is en Hallo-waarde is een nummer ("n") – documenten laten verlopen "n" seconden na de laatste wijziging</span><span class="sxs-lookup"><span data-stu-id="3a152-121">If present and hello value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="3a152-122">De TTL voor Hallo documenten:</span><span class="sxs-lookup"><span data-stu-id="3a152-122">TTL for hello documents:</span></span> 
   
   * <span data-ttu-id="3a152-123">Eigenschap is alleen van toepassing als DefaultTTL voor Hallo bovenliggende verzameling aanwezig.</span><span class="sxs-lookup"><span data-stu-id="3a152-123">Property is applicable only if DefaultTTL is present for hello parent collection.</span></span>
   * <span data-ttu-id="3a152-124">Hallo DefaultTTL waarde voor de verzameling van bovenliggende Hallo overschrijft.</span><span class="sxs-lookup"><span data-stu-id="3a152-124">Overrides hello DefaultTTL value for hello parent collection.</span></span>

<span data-ttu-id="3a152-125">Zodra het Hallo-document is verlopen (`ttl`  +  `_ts` > = huidige servertijd), Hallo document is gemarkeerd als 'verlopen'.</span><span class="sxs-lookup"><span data-stu-id="3a152-125">As soon as hello document has expired (`ttl` + `_ts` >= current server time), hello document is marked as "expired”.</span></span> <span data-ttu-id="3a152-126">Er is geen bewerking is toegestaan op deze documenten na deze tijd en ze zullen worden uitgesloten van Hallo resultaten van alle query's uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3a152-126">No operation will be allowed on these documents after this time and they will be excluded from hello results of any queries performed.</span></span> <span data-ttu-id="3a152-127">Hallo-documenten in Hallo-systeem fysiek zijn verwijderd en worden verwijderd op de achtergrond Hallo optioneel wordt op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="3a152-127">hello documents are physically deleted in hello system, and are deleted in hello background opportunistically at a later time.</span></span> <span data-ttu-id="3a152-128">Dit verbruikt geen een [Aanvraageenheden (RUs)](request-units.md) uit Hallo verzameling budget.</span><span class="sxs-lookup"><span data-stu-id="3a152-128">This does not consume any [Request Units (RUs)](request-units.md) from hello collection budget.</span></span>

<span data-ttu-id="3a152-129">Hallo hierboven logica kan worden weergegeven in Hallo matrix te volgen:</span><span class="sxs-lookup"><span data-stu-id="3a152-129">hello above logic can be shown in hello following matrix:</span></span>

|  | <span data-ttu-id="3a152-130">DefaultTTL ontbreekt of niet is ingesteld op Hallo-verzameling</span><span class="sxs-lookup"><span data-stu-id="3a152-130">DefaultTTL missing/not set on hello collection</span></span> | <span data-ttu-id="3a152-131">DefaultTTL = -1 op verzameling</span><span class="sxs-lookup"><span data-stu-id="3a152-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="3a152-132">DefaultTTL = "n" voor verzameling</span><span class="sxs-lookup"><span data-stu-id="3a152-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="3a152-133">TTL ontbreekt op document</span><span class="sxs-lookup"><span data-stu-id="3a152-133">TTL Missing on document</span></span> |<span data-ttu-id="3a152-134">Er is niets toooverride op documentniveau omdat zowel de Hallo-document als de verzameling hebt geen concept van TTL.</span><span class="sxs-lookup"><span data-stu-id="3a152-134">Nothing toooverride at document level since both hello document and collection have no concept of TTL.</span></span> |<span data-ttu-id="3a152-135">Er zijn geen documenten in deze verzameling verloopt.</span><span class="sxs-lookup"><span data-stu-id="3a152-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="3a152-136">Hallo-documenten in deze verzameling verlopen wanneer n interval is verstreken.</span><span class="sxs-lookup"><span data-stu-id="3a152-136">hello documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="3a152-137">TTL = -1 op document</span><span class="sxs-lookup"><span data-stu-id="3a152-137">TTL = -1 on document</span></span> |<span data-ttu-id="3a152-138">Niets toooverride op documentniveau Hallo omdat Hallo verzameling bevat geen definitie van Hallo DefaultTTL-eigenschap die een document kunt negeren.</span><span class="sxs-lookup"><span data-stu-id="3a152-138">Nothing toooverride at hello document level since hello collection doesn’t define hello DefaultTTL property that a document can override.</span></span> <span data-ttu-id="3a152-139">TTL voor een document is niet geïnterpreteerde door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="3a152-139">TTL on a document is un-interpreted by hello system.</span></span> |<span data-ttu-id="3a152-140">Er zijn geen documenten in deze verzameling verloopt.</span><span class="sxs-lookup"><span data-stu-id="3a152-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="3a152-141">Hallo-document met TTL =-1 in deze verzameling verloopt nooit.</span><span class="sxs-lookup"><span data-stu-id="3a152-141">hello document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="3a152-142">Alle andere documenten verloopt na "n" interval.</span><span class="sxs-lookup"><span data-stu-id="3a152-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="3a152-143">TTL = n op document</span><span class="sxs-lookup"><span data-stu-id="3a152-143">TTL = n on document</span></span> |<span data-ttu-id="3a152-144">Er is niets toooverride op documentniveau Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a152-144">Nothing toooverride at hello document level.</span></span> <span data-ttu-id="3a152-145">TTL voor een document in niet geïnterpreteerde door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="3a152-145">TTL on a document in un-interpreted by hello system.</span></span> |<span data-ttu-id="3a152-146">Hallo-document met TTL = n verloopt na interval n, in seconden.</span><span class="sxs-lookup"><span data-stu-id="3a152-146">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="3a152-147">Andere documenten wordt overgenomen van het interval van -1 en nooit verlopen.</span><span class="sxs-lookup"><span data-stu-id="3a152-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="3a152-148">Hallo-document met TTL = n verloopt na interval n, in seconden.</span><span class="sxs-lookup"><span data-stu-id="3a152-148">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="3a152-149">Andere documenten overneemt "n" interval van Hallo verzameling.</span><span class="sxs-lookup"><span data-stu-id="3a152-149">Other documents will inherit "n" interval from hello collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="3a152-150">TTL configureren</span><span class="sxs-lookup"><span data-stu-id="3a152-150">Configuring TTL</span></span>
<span data-ttu-id="3a152-151">Standaard is de tijd toolive standaard in alle Cosmos DB verzamelingen en op alle documenten uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3a152-151">By default, time toolive is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="3a152-152">TTL inschakelen</span><span class="sxs-lookup"><span data-stu-id="3a152-152">Enabling TTL</span></span>
<span data-ttu-id="3a152-153">tooenable TTL op een verzameling of Hallo documenten binnen een verzameling, moet u tooset Hallo DefaultTTL eigenschap van een verzameling tooeither -1 of een positief getal zijn dan nul.</span><span class="sxs-lookup"><span data-stu-id="3a152-153">tooenable TTL on a collection, or hello documents within a collection, you need tooset hello DefaultTTL property of a collection tooeither -1 or a non-zero positive number.</span></span> <span data-ttu-id="3a152-154">Instelling Hallo DefaultTTL te-1 betekent dat standaard alle documenten in de verzameling Hallo permanent wordt live maar Hallo Cosmos-DB-service moet worden gecontroleerd door deze verzameling voor documenten waarvoor deze standaardinstelling worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="3a152-154">Setting hello DefaultTTL too-1 means that by default all documents in hello collection will live forever but hello Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="3a152-155">Standaard-TTL op een verzameling configureren</span><span class="sxs-lookup"><span data-stu-id="3a152-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="3a152-156">U bent een toolive standaardtijd kunnen tooconfigure op het niveau van een verzameling.</span><span class="sxs-lookup"><span data-stu-id="3a152-156">You are able tooconfigure a default time toolive at a collection level.</span></span> <span data-ttu-id="3a152-157">tooset hello TTL op een verzameling, moet u een niet-nul positief getal dat Hallo-outperiode in seconden, tooexpire aangeeft tooprovide alle documenten in de verzameling Hallo nadat Hallo tijdstempel van Hallo document laatst gewijzigd (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="3a152-157">tooset hello TTL on a collection, you need tooprovide a non-zero positive number that indicates hello period, in seconds, tooexpire all documents in hello collection after hello last modified timestamp of hello document (`_ts`).</span></span> <span data-ttu-id="3a152-158">Of u Hallo standaard te-1, wat betekent dat dat alle documenten die worden ingevoegd in de verzameling toohello voor onbepaalde tijd standaard wordt live kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="3a152-158">Or, you can set hello default too-1, which implies that all documents inserted in toohello collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="3a152-159">De instelling van TTL op een document</span><span class="sxs-lookup"><span data-stu-id="3a152-159">Setting TTL on a document</span></span>
<span data-ttu-id="3a152-160">Bovendien toosetting een standaard TTL-waarde op een verzameling kunt u instellen specifieke TTL op het documentniveau van een.</span><span class="sxs-lookup"><span data-stu-id="3a152-160">In addition toosetting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="3a152-161">Hierdoor wordt standaard Hallo van Hallo verzameling overschreven.</span><span class="sxs-lookup"><span data-stu-id="3a152-161">Doing this will override hello default of hello collection.</span></span>

* <span data-ttu-id="3a152-162">tooset hello TTL op een document, moet u een niet-nul positief getal waarmee wordt aangegeven Hallo periode, in seconden, tooexpire Hallo document nadat Hallo laatst gewijzigd tijdstempel van Hallo document tooprovide (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="3a152-162">tooset hello TTL on a document, you need tooprovide a non-zero positive number which indicates hello period, in seconds, tooexpire hello document after hello last modified timestamp of hello document (`_ts`).</span></span>
* <span data-ttu-id="3a152-163">Als een document geen TTL-veld heeft, vervolgens Hallo standaard van Hallo-verzameling van toepassing.</span><span class="sxs-lookup"><span data-stu-id="3a152-163">If a document has no TTL field, then hello default of hello collection will apply.</span></span>
* <span data-ttu-id="3a152-164">Als TTL is uitgeschakeld op niveau van de verzameling hello, worden Hallo TTL op Hallo document genegeerd totdat de TTL opnieuw is ingeschakeld op Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="3a152-164">If TTL is disabled at hello collection level, hello TTL field on hello document will be ignored until TTL is enabled again on hello collection.</span></span>

<span data-ttu-id="3a152-165">Hier volgt een codefragment die laat zien hoe tooset Hallo TTL verloopt op een document:</span><span class="sxs-lookup"><span data-stu-id="3a152-165">Here's a snippet showing how tooset hello TTL expiration on a document:</span></span>

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="3a152-166">TTL op een bestaand document uitbreiden</span><span class="sxs-lookup"><span data-stu-id="3a152-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="3a152-167">U kunt Hallo TTL voor een document opnieuw instellen als volgt een schrijfbewerking voor Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="3a152-167">You can reset hello TTL on a document by doing any write operation on hello document.</span></span> <span data-ttu-id="3a152-168">Hierdoor wordt ingesteld Hallo `_ts` toohello huidige tijd en Hallo aftelling toohello document verloop, zoals ingesteld door Hallo `ttl`, opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="3a152-168">Doing this will set hello `_ts` toohello current time, and hello countdown toohello document expiry, as set by hello `ttl`, will begin again.</span></span> <span data-ttu-id="3a152-169">U kunt eventueel toochange hello `ttl` van een document, kunt u Hallo veld bijwerken zoals u met een ander veld worden ingesteld doen kunt.</span><span class="sxs-lookup"><span data-stu-id="3a152-169">If you wish toochange hello `ttl` of a document, you can update hello field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="3a152-170">TTL verwijderen uit een document</span><span class="sxs-lookup"><span data-stu-id="3a152-170">Removing TTL from a document</span></span>
<span data-ttu-id="3a152-171">Als een TTL-waarde is ingesteld op een document en niet langer dat document tooexpire wilt, kunt vervolgens u Hallo-document ophalen, verwijder Hallo TTL-veld en vervang Hallo-document op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="3a152-171">If a TTL has been set on a document and you no longer want that document tooexpire, then you can retrieve hello document, remove hello TTL field and replace hello document on hello server.</span></span> <span data-ttu-id="3a152-172">Wanneer de TTL-veld Hallo van Hallo document wordt verwijderd, wordt standaard Hallo van Hallo verzameling worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="3a152-172">When hello TTL field is removed from hello document, hello default of hello collection will be applied.</span></span> <span data-ttu-id="3a152-173">toostop een document verlopen en niet overgenomen van Hallo-verzameling moet u tooset Hallo TTL-waarde te-1.</span><span class="sxs-lookup"><span data-stu-id="3a152-173">toostop a document from expiring and not inherit from hello collection then you need tooset hello TTL value too-1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="3a152-174">TTL uitschakelen</span><span class="sxs-lookup"><span data-stu-id="3a152-174">Disabling TTL</span></span>
<span data-ttu-id="3a152-175">toodisable TTL volledig op een verzameling en stop Hallo achtergrond verwerken van zoekt verlopen documenten Hallo DefaultTTL eigenschap op Hallo-verzameling moet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3a152-175">toodisable TTL entirely on a collection and stop hello background process from looking for expired documents hello DefaultTTL property on hello collection should be deleted.</span></span> <span data-ttu-id="3a152-176">Als u deze eigenschap verschilt van de instelling voor het te-1.</span><span class="sxs-lookup"><span data-stu-id="3a152-176">Deleting this property is different from setting it too-1.</span></span> <span data-ttu-id="3a152-177">Toohello verzameling permanent wordt live, maar u kunt deze waarschuwing negeren op specifieke documenten in de verzameling Hallo instellen te-1 betekent dat nieuwe documenten worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3a152-177">Setting too-1 means new documents added toohello collection will live forever but you can override this on specific documents in hello collection.</span></span> <span data-ttu-id="3a152-178">Verwijderen van deze eigenschap volledig uit verzameling Hallo betekent dat er geen documenten verloopt, zelfs als er documenten waarvoor een eerdere standaard expliciet worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="3a152-178">Removing this property entirely from hello collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="3a152-179">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="3a152-179">FAQ</span></span>
<span data-ttu-id="3a152-180">**Wat TTL kost mij?**</span><span class="sxs-lookup"><span data-stu-id="3a152-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="3a152-181">Er is geen extra kosten toosetting TTL voor een document.</span><span class="sxs-lookup"><span data-stu-id="3a152-181">There is no additional cost toosetting a TTL on a document.</span></span>

<span data-ttu-id="3a152-182">**Hoe lang duurt toodelete mijn document zodra Hallo TTL is?**</span><span class="sxs-lookup"><span data-stu-id="3a152-182">**How long will it take toodelete my document once hello TTL is up?**</span></span>

<span data-ttu-id="3a152-183">Hallo-documenten zijn verlopen onmiddellijk nadat Hallo TTL opgestart is, en niet meer toegankelijk via CRUD of de query API's.</span><span class="sxs-lookup"><span data-stu-id="3a152-183">hello documents are expired immediately once hello TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="3a152-184">**Wordt de TTL voor een document invloed hebben op RU kosten**</span><span class="sxs-lookup"><span data-stu-id="3a152-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="3a152-185">Nee, er zijn geen gevolgen op RU kosten voor verwijderingen van verlopen documenten via TTL in Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="3a152-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="3a152-186">**Hallo TTL functie alleen geldt tooentire documenten of kan ik afzonderlijke document eigenschapswaarden verloopt?**</span><span class="sxs-lookup"><span data-stu-id="3a152-186">**Does hello TTL feature only apply tooentire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="3a152-187">TTL geldt toohello hele document.</span><span class="sxs-lookup"><span data-stu-id="3a152-187">TTL applies toohello entire document.</span></span> <span data-ttu-id="3a152-188">Als u tooexpire wilt wordt slechts een deel van een document, dan wordt aanbevolen Hallo gedeelte extraheren uit de belangrijkste document Hallo in tooa afzonderlijk 'gekoppelde' document uit te voeren en gebruik vervolgens de TTL op het uitgepakte document.</span><span class="sxs-lookup"><span data-stu-id="3a152-188">If you would like tooexpire just a portion of a document, then it is recommended that you extract hello portion from hello main document in tooa separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="3a152-189">**Heeft Hallo TTL functie ook specifieke vereisten voor indexering?**</span><span class="sxs-lookup"><span data-stu-id="3a152-189">**Does hello TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="3a152-190">Ja.</span><span class="sxs-lookup"><span data-stu-id="3a152-190">Yes.</span></span> <span data-ttu-id="3a152-191">Hallo-verzameling moet hebben [indexeren groepsbeleid](indexing-policies.md) tooeither consistente of Lazy.</span><span class="sxs-lookup"><span data-stu-id="3a152-191">hello collection must have [indexing policy set](indexing-policies.md) tooeither Consistent or Lazy.</span></span> <span data-ttu-id="3a152-192">Probeert tooset DefaultTTL op een verzameling met indexeren set tooNone leidt tot een fout als poging tooturn uitschakelen indexeren op een verzameling met een DefaultTTL al ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3a152-192">Trying tooset DefaultTTL on a collection with indexing set tooNone will result in an error, as will trying tooturn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a152-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a152-193">Next steps</span></span>
<span data-ttu-id="3a152-194">toolearn meer informatie over Azure Cosmos DB verwijzen toohello service [ *documentatie* ](https://azure.microsoft.com/documentation/services/cosmos-db/) pagina.</span><span class="sxs-lookup"><span data-stu-id="3a152-194">toolearn more about Azure Cosmos DB, refer toohello service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

