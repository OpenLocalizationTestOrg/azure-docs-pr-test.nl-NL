---
title: aaaRequest eenheden & schatten van doorvoer - Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe toounderstand, geef en vereisten voor aanvraag-eenheid in Azure Cosmos DB schatten.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="9ef09-103">Aanvraageenheden in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9ef09-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="9ef09-104">Nu beschikbaar: Azure Cosmos DB [aanvraag eenheid Rekenmachine](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="9ef09-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="9ef09-105">Meer informatie [schatting van de doorvoer moet](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="9ef09-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Doorvoer Rekenmachine][5]

## <a name="introduction"></a><span data-ttu-id="9ef09-107">Inleiding</span><span class="sxs-lookup"><span data-stu-id="9ef09-107">Introduction</span></span>
<span data-ttu-id="9ef09-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) van Microsoft wereldwijd gedistribueerde database voor meerdere model is.</span><span class="sxs-lookup"><span data-stu-id="9ef09-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="9ef09-109">Met Azure Cosmos DB niet u toorent virtuele machines hebt, software implementeren of databases bewaken.</span><span class="sxs-lookup"><span data-stu-id="9ef09-109">With Azure Cosmos DB, you don't have toorent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="9ef09-110">Azure Cosmos DB wordt beheerd en continu bewaakt door Microsoft bovenste engineers toodeliver world klasse beschikbaarheid, prestaties en beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9ef09-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers toodeliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="9ef09-111">U toegang hebt tot uw gegevens met behulp van API's van uw keuze als [DocumentDB SQL](documentdb-sql-query.md) (document) MongoDB (document) [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (sleutel-waarde), en [Gremlin](https://tinkerpop.apache.org/gremlin.html) (grafiek) worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="9ef09-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="9ef09-112">Hallo valuta van Azure DB die Cosmos is Hallo aanvragen Unit (RU).</span><span class="sxs-lookup"><span data-stu-id="9ef09-112">hello currency of Azure Cosmos DB is hello Request Unit (RU).</span></span> <span data-ttu-id="9ef09-113">Met RUs hoeft u niet tooreserve lezen/schrijven capaciteiten of het inrichten CPU, geheugen en IOPS.</span><span class="sxs-lookup"><span data-stu-id="9ef09-113">With RUs, you do not need tooreserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="9ef09-114">Azure Cosmos DB ondersteunt een aantal API's met verschillende bewerkingen, variërend van eenvoudige leest en schrijft toocomplex grafiek query's.</span><span class="sxs-lookup"><span data-stu-id="9ef09-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes toocomplex graph queries.</span></span> <span data-ttu-id="9ef09-115">Omdat niet alle aanvragen gelijk zijn, zijn ze een genormaliseerde hoeveelheid toegewezen **aanvraageenheden** op basis van Hallo hoeveelheid berekening vereist tooserve Hallo aanvraag.</span><span class="sxs-lookup"><span data-stu-id="9ef09-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on hello amount of computation required tooserve hello request.</span></span> <span data-ttu-id="9ef09-116">Hallo aantal aanvraageenheden voor een bewerking is deterministisch en kunt u het aantal aanvraageenheden verbruikt door elke bewerking in Azure Cosmos DB via een antwoordheader Hallo bijhouden.</span><span class="sxs-lookup"><span data-stu-id="9ef09-116">hello number of request units for an operation is deterministic, and you can track hello number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="9ef09-117">tooprovide voorspelbare prestaties, moet u tooreserve doorvoer in eenheden van 100 RU/seconde.</span><span class="sxs-lookup"><span data-stu-id="9ef09-117">tooprovide predictable performance, you need tooreserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="9ef09-118">Na het lezen van dit artikel, moet u kunnen tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9ef09-118">After reading this article, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="9ef09-119">Wat zijn aanvraageenheden en kosten aanvragen?</span><span class="sxs-lookup"><span data-stu-id="9ef09-119">What are request units and request charges?</span></span>
* <span data-ttu-id="9ef09-120">Hoe geef ik aanvraag eenheid capaciteit voor een verzameling?</span><span class="sxs-lookup"><span data-stu-id="9ef09-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="9ef09-121">Hoe u schat dat mijn toepassing aanvraag heeft?</span><span class="sxs-lookup"><span data-stu-id="9ef09-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="9ef09-122">Wat gebeurt er als ik aanvraag eenheid capaciteit voor een verzameling overschrijdt?</span><span class="sxs-lookup"><span data-stu-id="9ef09-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="9ef09-123">Zoals Azure Cosmos DB een database met meerdere modellen is, is het belangrijk toonote dat tooa verzameling/document voor een API-document, een grafiek/knooppunt voor de API van een grafiek en een Tabelentiteit voor tabel-API wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="9ef09-123">As Azure Cosmos DB is a multi-model database, it is important toonote that we will refer tooa collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="9ef09-124">Doorvoer in dit document wordt we toohello concepten van container item/generalize.</span><span class="sxs-lookup"><span data-stu-id="9ef09-124">Throughput this document we will generalize toohello concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="9ef09-125">Aanvraageenheden en kosten van de aanvraag</span><span class="sxs-lookup"><span data-stu-id="9ef09-125">Request units and request charges</span></span>
<span data-ttu-id="9ef09-126">Azure Cosmos DB biedt snelle en voorspelbare prestaties door *reserveren* resources toosatisfy doorvoer van uw toepassing nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="9ef09-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources toosatisfy your application's throughput needs.</span></span>  <span data-ttu-id="9ef09-127">Omdat de toepassing laden en toegang tot patronen wijzigen na verloop van tijd, wordt Azure Cosmos DB kunt u tooeasily toename of minder Hallo gereserveerde doorvoer beschikbaar tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="9ef09-127">Because application load and access patterns change over time, Azure Cosmos DB allows you tooeasily increase or decrease hello amount of reserved throughput available tooyour application.</span></span>

<span data-ttu-id="9ef09-128">Met Azure Cosmos DB is gereserveerde doorvoer opgegeven in termen van aanvraageenheden per seconde verwerkt.</span><span class="sxs-lookup"><span data-stu-id="9ef09-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="9ef09-129">U kunt zien aanvraageenheden als valuta doorvoer, waarbij u *reserveren* een hoeveelheid gegarandeerd aanvraageenheden beschikbaar tooyour toepassing op basis van per seconde.</span><span class="sxs-lookup"><span data-stu-id="9ef09-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available tooyour application on per second basis.</span></span>  <span data-ttu-id="9ef09-130">Elke bewerking in Azure Cosmos DB - schrijven, uitvoeren van een query, het bijwerken van een document - verbruikt CPU, geheugen en IOPS.</span><span class="sxs-lookup"><span data-stu-id="9ef09-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="9ef09-131">Dat wil zeggen, elke bewerking leidt ertoe dat een *aanvragen kosten*, die wordt uitgedrukt in *aanvraageenheden*.</span><span class="sxs-lookup"><span data-stu-id="9ef09-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="9ef09-132">Inzicht in Hallo factoren die van invloed zijn op aanvraag eenheid kosten, samen met de vereisten van de doorvoer van uw toepassing, kunt u toorun uw toepassing als de kosten-effectief mogelijk.</span><span class="sxs-lookup"><span data-stu-id="9ef09-132">Understanding hello factors which impact request unit charges, along with your application's throughput requirements, enables you toorun your application as cost effectively as possible.</span></span> <span data-ttu-id="9ef09-133">Hallo queryverkenner is ook een fantastische hulpprogramma tootest Hallo kern van een query.</span><span class="sxs-lookup"><span data-stu-id="9ef09-133">hello query explorer is also a wonderful tool tootest hello core of a query.</span></span>

<span data-ttu-id="9ef09-134">Het is raadzaam om aan de slag door bekijkt hello video te volgen waarbij Aravind Ramachandran wordt uitgelegd aanvraageenheden en voorspelbare prestaties met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9ef09-134">We recommend getting started by watching hello following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="9ef09-135">Capaciteit van de aanvraag-eenheid opgeven in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="9ef09-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="9ef09-136">Bij het starten van een nieuwe verzameling, de tabel of de grafiek, u Hallo-nummer opgeven aantal aanvraageenheden per seconde (ru/s per seconde) u wilt dat gereserveerd.</span><span class="sxs-lookup"><span data-stu-id="9ef09-136">When starting a new collection, table or graph, you specify hello number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="9ef09-137">Op basis van de ingerichte doorvoer hello, Azure Cosmos DB toegewezen fysieke partities toohost uw verzameling en splitsingen/rebalances gegevens meerdere partities wanneer deze groeit.</span><span class="sxs-lookup"><span data-stu-id="9ef09-137">Based on hello provisioned throughput, Azure Cosmos DB allocates physical partitions toohost your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="9ef09-138">Azure Cosmos DB moet dat een partitie sleutel toobe worden opgegeven wanneer een verzameling is ingericht met 2500 aanvraageenheden of hoger.</span><span class="sxs-lookup"><span data-stu-id="9ef09-138">Azure Cosmos DB requires a partition key toobe specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="9ef09-139">Een partitiesleutel is ook vereist tooscale doorvoer afgezien van 2500 aanvraageenheden in toekomstige Hallo van uw verzameling.</span><span class="sxs-lookup"><span data-stu-id="9ef09-139">A partition key is also required tooscale your collection's throughput beyond 2,500 request units in hello future.</span></span> <span data-ttu-id="9ef09-140">Daarom is het raadzaam tooconfigure een [partitiesleutel](partition-data.md) bij het maken van een container ongeacht uw eerste doorvoer.</span><span class="sxs-lookup"><span data-stu-id="9ef09-140">Therefore, it is highly recommended tooconfigure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="9ef09-141">Omdat de gegevens toobe verdelen over meerdere partities wellicht, is het nodig toopick een partitiesleutel met een hoge kardinaliteit (100 toomillions van afzonderlijke waarden) zodat uw tabel-verzameling/grafiek en aanvragen kunnen worden vergroot of verkleind gelijkmatig door Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9ef09-141">Since your data might have toobe split across multiple partitions, it is necessary toopick a partition key that has a high cardinality (100 toomillions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="9ef09-142">Een partitiesleutel is een grens van een logische en niet een fysieke.</span><span class="sxs-lookup"><span data-stu-id="9ef09-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="9ef09-143">U moet daarom niet toolimit Hallo aantal afzonderlijke partitie sleutelwaarden.</span><span class="sxs-lookup"><span data-stu-id="9ef09-143">Therefore, you do not need toolimit hello number of distinct partition key values.</span></span> <span data-ttu-id="9ef09-144">Het is in feite betere toohave duidelijker sleutelwaarden dan kleiner, partitie-als Azure Cosmos DB heeft meer opties voor taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="9ef09-144">It is in fact better toohave more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="9ef09-145">Hier volgt een codefragment voor het maken van een verzameling met 3000 aanvraag eenheden per met behulp van tweede Hallo .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="9ef09-145">Here is a code snippet for creating a collection with 3,000 request units per second using hello .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="9ef09-146">Azure Cosmos-database is van invloed op een model reservering op doorvoer.</span><span class="sxs-lookup"><span data-stu-id="9ef09-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="9ef09-147">Dat wil zeggen, u wordt gefactureerd voor Hallo hoeveelheid doorvoer *gereserveerde*, ongeacht hoeveel waarop doorvoer is actief *gebruikt*.</span><span class="sxs-lookup"><span data-stu-id="9ef09-147">That is, you are billed for hello amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="9ef09-148">Als uw toepassing werklast, gegevens en informatie over het gebruik patronen wijzigen kunt u eenvoudig de schaal omhoog en omlaag Hallo hoeveelheid gereserveerde RUs via SDK's of met behulp van Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9ef09-148">As your application's load, data, and usage patterns change you can easily scale up and down hello amount of reserved RUs through SDKs or using hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="9ef09-149">Elke verzameling, de tabel/het grafiek zijn toegewezen tooan `Offer` resource in Azure Cosmos DB met metagegevens over Hallo ingerichte doorvoer.</span><span class="sxs-lookup"><span data-stu-id="9ef09-149">Each collection/table/graph are mapped tooan `Offer` resource in Azure Cosmos DB, which has metadata about hello provisioned throughput.</span></span> <span data-ttu-id="9ef09-150">U kunt Hallo toegewezen doorvoer wijzigen door op Hallo bijbehorende aanbieding resource voor een container te zoeken en vervolgens bijgewerkt met nieuwe doorvoercapaciteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="9ef09-150">You can change hello allocated throughput by looking up hello corresponding offer resource for a container, then updating it with hello new throughput value.</span></span> <span data-ttu-id="9ef09-151">Hier volgt een codefragment voor het wijzigen van Hallo doorvoer van een verzameling too5, 000 aanvraageenheden per met behulp van tweede Hallo .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="9ef09-151">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second using hello .NET SDK:</span></span>

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="9ef09-152">Er is geen impact toohello beschikbaarheid van de container wanneer u Hallo doorvoer wijzigt.</span><span class="sxs-lookup"><span data-stu-id="9ef09-152">There is no impact toohello availability of your container when you change hello throughput.</span></span> <span data-ttu-id="9ef09-153">Hallo nieuwe gereserveerde doorvoer is doorgaans effectieve binnen enkele seconden op de toepassing van nieuwe Hallo-doorvoer.</span><span class="sxs-lookup"><span data-stu-id="9ef09-153">Typically hello new reserved throughput is effective within seconds on application of hello new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="9ef09-154">Overwegingen voor aanvraag-eenheid</span><span class="sxs-lookup"><span data-stu-id="9ef09-154">Request unit considerations</span></span>
<span data-ttu-id="9ef09-155">Bij schatten Hallo aantal aanvraag eenheden tooreserve voor uw Azure DB die Cosmos-container, is het belangrijk tootake Hallo variabelen in aanmerking te volgen:</span><span class="sxs-lookup"><span data-stu-id="9ef09-155">When estimating hello number of request units tooreserve for your Azure Cosmos DB container, it is important tootake hello following variables into consideration:</span></span>

* <span data-ttu-id="9ef09-156">**De grootte van item**.</span><span class="sxs-lookup"><span data-stu-id="9ef09-156">**Item size**.</span></span> <span data-ttu-id="9ef09-157">Als grootte toeneemt Hallo eenheden tooread verbruikt of Hallo-gegevens schrijven wordt ook vergroot.</span><span class="sxs-lookup"><span data-stu-id="9ef09-157">As size increases hello units consumed tooread or write hello data will also increase.</span></span>
* <span data-ttu-id="9ef09-158">**Aantal eigenschappen item**.</span><span class="sxs-lookup"><span data-stu-id="9ef09-158">**Item property count**.</span></span> <span data-ttu-id="9ef09-159">Ervan uitgaande dat standaard indexeren van alle eigenschappen, Hallo eenheden verbruikt toowrite een document, de knooppunt/het ntity wordt verhoogd als Hallo eigenschap count toeneemt.</span><span class="sxs-lookup"><span data-stu-id="9ef09-159">Assuming default indexing of all properties, hello units consumed toowrite a document/node/ntity will increase as hello property count increases.</span></span>
* <span data-ttu-id="9ef09-160">**Gegevensconsistentie**.</span><span class="sxs-lookup"><span data-stu-id="9ef09-160">**Data consistency**.</span></span> <span data-ttu-id="9ef09-161">Wanneer u gegevens consistentieniveaus van sterke of gebonden veroudering, worden aanvullende eenheden verbruikte tooread items.</span><span class="sxs-lookup"><span data-stu-id="9ef09-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed tooread items.</span></span>
* <span data-ttu-id="9ef09-162">**Geïndexeerde eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="9ef09-162">**Indexed properties**.</span></span> <span data-ttu-id="9ef09-163">Een index-beleid op elke container bepaalt welke eigenschappen standaard worden geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="9ef09-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="9ef09-164">Door het aantal geïndexeerde eigenschappen hello te beperken of doordat de vertraagde indexeren, kunt u uw aanvraag eenheidsverbruik verminderen.</span><span class="sxs-lookup"><span data-stu-id="9ef09-164">You can reduce your request unit consumption by limiting hello number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="9ef09-165">**Document indexeren**.</span><span class="sxs-lookup"><span data-stu-id="9ef09-165">**Document indexing**.</span></span> <span data-ttu-id="9ef09-166">Standaard die elk item wordt automatisch geïndexeerd, wordt u minder aanvraageenheden gebruiken als u ervoor geen tooindex aantal objecten kiest.</span><span class="sxs-lookup"><span data-stu-id="9ef09-166">By default each item is automatically indexed, you will consume fewer request units if you choose not tooindex some of your items.</span></span>
* <span data-ttu-id="9ef09-167">**Query uitvoeren op patronen**.</span><span class="sxs-lookup"><span data-stu-id="9ef09-167">**Query patterns**.</span></span> <span data-ttu-id="9ef09-168">Hallo complexiteit van een query heeft gevolgen voor het aantal eenheden van de aanvraag voor een bewerking worden verbruikt.</span><span class="sxs-lookup"><span data-stu-id="9ef09-168">hello complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="9ef09-169">aantal predicaten Hello, aard van Hallo predikaten, projecties, aantal UDF's en grootte van alle Hallo kosten van invloed zijn op bron-gegevensset voor Hallo Hallo query bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="9ef09-169">hello number of predicates, nature of hello predicates, projections, number of UDFs, and hello size of hello source data set all influence hello cost of query operations.</span></span>
* <span data-ttu-id="9ef09-170">**Gebruik een script**.</span><span class="sxs-lookup"><span data-stu-id="9ef09-170">**Script usage**.</span></span>  <span data-ttu-id="9ef09-171">Net als bij query's, opgeslagen procedures en triggers in beslag nemen aanvraageenheden op basis van Hallo complexiteit van het Hallo-bewerkingen die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ef09-171">As with queries, stored procedures and triggers consume request units based on hello complexity of hello operations being performed.</span></span> <span data-ttu-id="9ef09-172">Tijdens het ontwikkelen van uw toepassing hello aanvraag kosten inspecteren header toobetter begrijpen hoe elke bewerking aanvraag eenheid capaciteit is verbruikt.</span><span class="sxs-lookup"><span data-stu-id="9ef09-172">As you develop your application, inspect hello request charge header toobetter understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="9ef09-173">Schatten van doorvoerbehoeften</span><span class="sxs-lookup"><span data-stu-id="9ef09-173">Estimating throughput needs</span></span>
<span data-ttu-id="9ef09-174">Een aanvraag-eenheid is een genormaliseerde meting van de kosten voor aanvraagverwerking.</span><span class="sxs-lookup"><span data-stu-id="9ef09-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="9ef09-175">Een eenheid één aanvraag vertegenwoordigt Hallo verwerking vereiste capaciteit tooread (via self link- of -id) voor een enkele 1KB item dat bestaat uit 10 unieke eigenschapswaarden (met uitzondering van Systeemeigenschappen).</span><span class="sxs-lookup"><span data-stu-id="9ef09-175">A single request unit represents hello processing capacity required tooread (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="9ef09-176">Een aanvraag toocreate (invoegen), vervangen of verwijderen van hetzelfde item verbruikt meer verwerken van de service Hallo Hallo en waardoor meer aanvraageenheden.</span><span class="sxs-lookup"><span data-stu-id="9ef09-176">A request toocreate (insert), replace or delete hello same item will consume more processing from hello service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="9ef09-177">Hallo basislijn van de aanvraag 1 eenheid voor een 1KB item overeenkomt met eenvoudige tooa ophalen door self link- of -id van Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="9ef09-177">hello baseline of 1 request unit for a 1KB item corresponds tooa simple GET by self link or id of hello item.</span></span>
> 
> 

<span data-ttu-id="9ef09-178">Hier is bijvoorbeeld een tabel waarin het aantal aanvragen eenheden tooprovision op drie verschillende item grootten (1KB, 4KB en 64KB) en op twee verschillende prestatieniveaus (500 leesbewerkingen per seconde + 100 schrijfbewerkingen per seconde en 500 leesbewerkingen per seconde + 500 schrijfbewerkingen per seconde).</span><span class="sxs-lookup"><span data-stu-id="9ef09-178">For example, here's a table that shows how many request units tooprovision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="9ef09-179">Hallo gegevensconsistentie op sessie is geconfigureerd en Hallo indexeren beleid tooNone is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9ef09-179">hello data consistency was configured at Session, and hello indexing policy was set tooNone.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="9ef09-180"><strong>De grootte van artikel</strong></span><span class="sxs-lookup"><span data-stu-id="9ef09-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-181"><strong>Leesbewerkingen per seconde</strong></span><span class="sxs-lookup"><span data-stu-id="9ef09-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-182"><strong>Schrijfbewerkingen per seconde</strong></span><span class="sxs-lookup"><span data-stu-id="9ef09-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-183"><strong>Aanvraageenheden</strong></span><span class="sxs-lookup"><span data-stu-id="9ef09-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9ef09-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="9ef09-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-185">500</span><span class="sxs-lookup"><span data-stu-id="9ef09-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-186">100</span><span class="sxs-lookup"><span data-stu-id="9ef09-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-187">(500 * 1) + (100 * 5) = 1000 RU/s</span><span class="sxs-lookup"><span data-stu-id="9ef09-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9ef09-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="9ef09-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-189">500</span><span class="sxs-lookup"><span data-stu-id="9ef09-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-190">500</span><span class="sxs-lookup"><span data-stu-id="9ef09-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-191">(500 * 1) + (500 * 5) = 3.000 RU/s</span><span class="sxs-lookup"><span data-stu-id="9ef09-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9ef09-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="9ef09-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-193">500</span><span class="sxs-lookup"><span data-stu-id="9ef09-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-194">100</span><span class="sxs-lookup"><span data-stu-id="9ef09-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span><span class="sxs-lookup"><span data-stu-id="9ef09-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9ef09-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="9ef09-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-197">500</span><span class="sxs-lookup"><span data-stu-id="9ef09-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-198">500</span><span class="sxs-lookup"><span data-stu-id="9ef09-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span><span class="sxs-lookup"><span data-stu-id="9ef09-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9ef09-200">64 kB</span><span class="sxs-lookup"><span data-stu-id="9ef09-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-201">500</span><span class="sxs-lookup"><span data-stu-id="9ef09-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-202">100</span><span class="sxs-lookup"><span data-stu-id="9ef09-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span><span class="sxs-lookup"><span data-stu-id="9ef09-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9ef09-204">64 kB</span><span class="sxs-lookup"><span data-stu-id="9ef09-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-205">500</span><span class="sxs-lookup"><span data-stu-id="9ef09-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-206">500</span><span class="sxs-lookup"><span data-stu-id="9ef09-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9ef09-207">(500 * 10) + (500 * 48) = 29.000 RU/s</span><span class="sxs-lookup"><span data-stu-id="9ef09-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a><span data-ttu-id="9ef09-208">Hallo aanvraag eenheid Rekenmachine gebruiken</span><span class="sxs-lookup"><span data-stu-id="9ef09-208">Use hello request unit calculator</span></span>
<span data-ttu-id="9ef09-209">toohelp klanten fijn stemmen hun schattingen doorvoer, wordt er een op het web gebaseerd [aanvraag eenheid Rekenmachine](https://www.documentdb.com/capacityplanner) toohelp schatting Hallo aanvraag eenheid vereisten voor normale bewerkingen, inclusief:</span><span class="sxs-lookup"><span data-stu-id="9ef09-209">toohelp customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) toohelp estimate hello request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="9ef09-210">Item maakt (schrijft)</span><span class="sxs-lookup"><span data-stu-id="9ef09-210">Item creates (writes)</span></span>
* <span data-ttu-id="9ef09-211">Item leest</span><span class="sxs-lookup"><span data-stu-id="9ef09-211">Item reads</span></span>
* <span data-ttu-id="9ef09-212">Item wordt verwijderd</span><span class="sxs-lookup"><span data-stu-id="9ef09-212">Item deletes</span></span>
* <span data-ttu-id="9ef09-213">Item updates</span><span class="sxs-lookup"><span data-stu-id="9ef09-213">Item updates</span></span>

<span data-ttu-id="9ef09-214">Hallo hulpprogramma biedt tevens ondersteuning voor het schatten van opslagbehoeften op basis van Hallo voorbeelditems die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="9ef09-214">hello tool also includes support for estimating data storage needs based on hello sample items you provide.</span></span>

<span data-ttu-id="9ef09-215">Het hulpprogramma voor Hallo is eenvoudig:</span><span class="sxs-lookup"><span data-stu-id="9ef09-215">Using hello tool is simple:</span></span>

1. <span data-ttu-id="9ef09-216">Upload een of meer representatieve items.</span><span class="sxs-lookup"><span data-stu-id="9ef09-216">Upload one or more representative items.</span></span>
   
    ![Items toohello aanvraag eenheid Rekenmachine uploaden][2]
2. <span data-ttu-id="9ef09-218">vereisten voor gegevensopslag tooestimate, typ Hallo totaal aantal items u toostore verwacht.</span><span class="sxs-lookup"><span data-stu-id="9ef09-218">tooestimate data storage requirements, enter hello total number of items you expect toostore.</span></span>
3. <span data-ttu-id="9ef09-219">Voer Hallo aantal items maken, lezen, bijwerken en verwijderen van bewerkingen die u nodig (op basis van het per seconde hebt).</span><span class="sxs-lookup"><span data-stu-id="9ef09-219">Enter hello number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="9ef09-220">tooestimate hello aanvraag eenheid kosten van item update-bewerkingen, upload een kopie van Hallo voorbeeld item uit stap 1 bovenstaande typische veld updates bevat.</span><span class="sxs-lookup"><span data-stu-id="9ef09-220">tooestimate hello request unit charges of item update operations, upload a copy of hello sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="9ef09-221">Als updates objecten doorgaans twee eigenschappen met de naam lastLogin en userVisits wijzigen en vervolgens Hallo voorbeeld item te kopiëren, Hallo waarden voor deze twee eigenschappen bijwerken en Hallo gekopieerd item uploaden.</span><span class="sxs-lookup"><span data-stu-id="9ef09-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy hello sample item, update hello values for those two properties, and upload hello copied item.</span></span>
   
    ![Doorvoer vereisten invoeren in de Hallo aanvraag eenheid Rekenmachine][3]
4. <span data-ttu-id="9ef09-223">Klik op berekenen en bekijkt hello resultaten.</span><span class="sxs-lookup"><span data-stu-id="9ef09-223">Click calculate and examine hello results.</span></span>
   
    ![Eenheid Rekenmachine resultaten aanvragen][4]

> [!NOTE]
> <span data-ttu-id="9ef09-225">Als u itemtypen die aanzienlijk verschillen in termen van de grootte en Hallo aantal geïndexeerde eigenschappen hebt wordt, uploadt u een voorbeeld van elke *type* van typische item toohello hulpprogramma en Hallo resultaten vervolgens te berekenen.</span><span class="sxs-lookup"><span data-stu-id="9ef09-225">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then upload a sample of each *type* of typical item toohello tool and then calculate hello results.</span></span>
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="9ef09-226">Hello Azure Cosmos DB kosten antwoord aanvraagheader gebruiken</span><span class="sxs-lookup"><span data-stu-id="9ef09-226">Use hello Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="9ef09-227">Elke reactie van hello Azure DB die Cosmos-service bestaat uit een aangepaste header (`x-ms-request-charge`) die Hallo aanvraageenheden verbruikt voor Hallo-aanvraag bevat.</span><span class="sxs-lookup"><span data-stu-id="9ef09-227">Every response from hello Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains hello request units consumed for hello request.</span></span> <span data-ttu-id="9ef09-228">Deze header is ook toegankelijk via hello Azure Cosmos DB SDK's.</span><span class="sxs-lookup"><span data-stu-id="9ef09-228">This header is also accessible through hello Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="9ef09-229">Hallo .NET SDK is RequestCharge een eigenschap van Hallo ResourceResponse object.</span><span class="sxs-lookup"><span data-stu-id="9ef09-229">In hello .NET SDK, RequestCharge is a property of hello ResourceResponse object.</span></span>  <span data-ttu-id="9ef09-230">Hello Azure Cosmos DB Queryverkenner in hello Azure-portal biedt voor query's, kosten aanvraaggegevens voor uitgevoerde query's.</span><span class="sxs-lookup"><span data-stu-id="9ef09-230">For queries, hello Azure Cosmos DB Query Explorer in hello Azure portal provides request charge information for executed queries.</span></span>

![RU kosten in Hallo Queryverkenner onderzoeken][1]

<span data-ttu-id="9ef09-232">Met dat gegeven in gedachte, is een methode voor het schatten van de hoeveelheid gereserveerde doorvoer vereist door uw toepassing hello toorecord Hallo aanvraag eenheid kosten die zijn gekoppeld aan met het normale bewerkingen uitvoeren in een representatieve item gebruikt door de toepassing en vervolgens schatten Hallo aantal bewerkingen wilt u uitvoeren per seconde.</span><span class="sxs-lookup"><span data-stu-id="9ef09-232">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="9ef09-233">Ervoor toomeasure en typische query's en ook gebruik van Azure DB die Cosmos script bevatten.</span><span class="sxs-lookup"><span data-stu-id="9ef09-233">Be sure toomeasure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="9ef09-234">Als er itemtypen die aanzienlijk in termen van de grootte en Hallo aantal geïndexeerde eigenschappen verschillen wordt, en noteer vervolgens Hallo toepasselijke bewerking aanvraag eenheid kosten die zijn gekoppeld aan elk *type* van typische item.</span><span class="sxs-lookup"><span data-stu-id="9ef09-234">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="9ef09-235">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9ef09-235">For example:</span></span>

1. <span data-ttu-id="9ef09-236">Hallo aanvraag eenheid kosten voor het maken van (invoegen) opnemen een typische item.</span><span class="sxs-lookup"><span data-stu-id="9ef09-236">Record hello request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="9ef09-237">Record Hallo aanvraag eenheid kosten voor het lezen van een typische item.</span><span class="sxs-lookup"><span data-stu-id="9ef09-237">Record hello request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="9ef09-238">Record Hallo aanvraag eenheid kosten van het bijwerken van een typische item.</span><span class="sxs-lookup"><span data-stu-id="9ef09-238">Record hello request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="9ef09-239">Record Hallo aanvraag eenheid kosten van item gebruikelijke, algemene query's.</span><span class="sxs-lookup"><span data-stu-id="9ef09-239">Record hello request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="9ef09-240">Record Hallo aanvraag eenheid kosten van alle aangepaste scripts (opgeslagen procedures, triggers, gebruiker gedefinieerde functies) door de toepassing hello worden gebruikt</span><span class="sxs-lookup"><span data-stu-id="9ef09-240">Record hello request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by hello application</span></span>
6. <span data-ttu-id="9ef09-241">Berekenen Hallo vereiste aanvraag dat eenheden Hallo geschatte aantal bewerkingen verwacht toorun per seconde.</span><span class="sxs-lookup"><span data-stu-id="9ef09-241">Calculate hello required request units given hello estimated number of operations you anticipate toorun each second.</span></span>

### <span data-ttu-id="9ef09-242"><a id="GetLastRequestStatistics"></a>API voor van MongoDB GetLastRequestStatistics opdracht gebruiken</span><span class="sxs-lookup"><span data-stu-id="9ef09-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="9ef09-243">API voor MongoDB biedt ondersteuning voor een aangepaste opdracht *getLastRequestStatistics*, voor het ophalen van Hallo aanvraag kosten voor opgegeven bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="9ef09-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving hello request charge for specified operations.</span></span>

<span data-ttu-id="9ef09-244">Bijvoorbeeld in Hallo Mongo-Shell, gewenste tooverify Hallo aanvraag kosten voor Hallo-bewerking uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9ef09-244">For example, in hello Mongo Shell, execute hello operation you want tooverify hello request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="9ef09-245">Vervolgens Hallo-opdracht uitvoeren *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="9ef09-245">Next, execute hello command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="9ef09-246">Met dat gegeven in gedachte, is een methode voor het schatten van de hoeveelheid gereserveerde doorvoer vereist door uw toepassing hello toorecord Hallo aanvraag eenheid kosten die zijn gekoppeld aan met het normale bewerkingen uitvoeren in een representatieve item gebruikt door de toepassing en vervolgens schatten Hallo aantal bewerkingen wilt u uitvoeren per seconde.</span><span class="sxs-lookup"><span data-stu-id="9ef09-246">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="9ef09-247">Als er itemtypen die aanzienlijk in termen van de grootte en Hallo aantal geïndexeerde eigenschappen verschillen wordt, en noteer vervolgens Hallo toepasselijke bewerking aanvraag eenheid kosten die zijn gekoppeld aan elk *type* van typische item.</span><span class="sxs-lookup"><span data-stu-id="9ef09-247">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="9ef09-248">API gebruiken voor de portal metrieken van MongoDB</span><span class="sxs-lookup"><span data-stu-id="9ef09-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="9ef09-249">Hallo de eenvoudigste manier tooget een goede schatting van de aanvraag eenheid voor uw API berekent voor MongoDB-database toouse hello is [Azure-portal](https://portal.azure.com) metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="9ef09-249">hello simplest way tooget a good estimation of request unit charges for your API for MongoDB database is toouse hello [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="9ef09-250">Hello *aantal aanvragen* en *aanvraag kosten* grafieken, kunt u een schatting van het aantal aanvraageenheden elke bewerking is verbruikt en krijgen hoeveel aanvraageenheden ze relatieve tooone verbruiken een andere.</span><span class="sxs-lookup"><span data-stu-id="9ef09-250">With hello *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative tooone another.</span></span>

![API voor MongoDB portal metrische gegevens][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="9ef09-252">Een voorbeeld van een aanvraag eenheid schatting</span><span class="sxs-lookup"><span data-stu-id="9ef09-252">A request unit estimation example</span></span>
<span data-ttu-id="9ef09-253">Houd rekening met Hallo ~ 1KB document te volgen:</span><span class="sxs-lookup"><span data-stu-id="9ef09-253">Consider hello following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="9ef09-254">Documenten zijn in Azure Cosmos DB minified zodat Hallo systeem berekend grootte van de bovenstaande Hallo-document is iets minder dan 1KB.</span><span class="sxs-lookup"><span data-stu-id="9ef09-254">Documents are minified in Azure Cosmos DB, so hello system calculated size of hello document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="9ef09-255">Hallo volgende tabel ziet u een benadering aanvraag eenheid kosten voor normale bewerkingen op dit object (Hallo geschatte aanvraag eenheid kosten wordt ervan uitgegaan dat Hallo consistentieniveau-account te is ingesteld dat alle items automatisch worden geïndexeerd en 'Sessie'):</span><span class="sxs-lookup"><span data-stu-id="9ef09-255">hello following table shows approximate request unit charges for typical operations on this item (hello approximate request unit charge assumes that hello account consistency level is set too“Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="9ef09-256">Bewerking</span><span class="sxs-lookup"><span data-stu-id="9ef09-256">Operation</span></span> | <span data-ttu-id="9ef09-257">Aanvraag eenheid kosten</span><span class="sxs-lookup"><span data-stu-id="9ef09-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="9ef09-258">-Item maken</span><span class="sxs-lookup"><span data-stu-id="9ef09-258">Create item</span></span> |<span data-ttu-id="9ef09-259">~ 15 RU</span><span class="sxs-lookup"><span data-stu-id="9ef09-259">~15 RU</span></span> |
| <span data-ttu-id="9ef09-260">Item lezen</span><span class="sxs-lookup"><span data-stu-id="9ef09-260">Read item</span></span> |<span data-ttu-id="9ef09-261">~ 1 RU</span><span class="sxs-lookup"><span data-stu-id="9ef09-261">~1 RU</span></span> |
| <span data-ttu-id="9ef09-262">Query-item met id</span><span class="sxs-lookup"><span data-stu-id="9ef09-262">Query item by id</span></span> |<span data-ttu-id="9ef09-263">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="9ef09-263">~2.5 RU</span></span> |

<span data-ttu-id="9ef09-264">In deze tabel ziet een benadering aanvraag bovendien eenheid kosten voor typische query's in de toepassing hello gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9ef09-264">Additionally, this table shows approximate request unit charges for typical queries used in hello application:</span></span>

| <span data-ttu-id="9ef09-265">Query’s uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9ef09-265">Query</span></span> | <span data-ttu-id="9ef09-266">Aanvraag eenheid kosten</span><span class="sxs-lookup"><span data-stu-id="9ef09-266">Request Unit Charge</span></span> | <span data-ttu-id="9ef09-267">het aantal geretourneerde artikelen</span><span class="sxs-lookup"><span data-stu-id="9ef09-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9ef09-268">Selecteer voeding door-id</span><span class="sxs-lookup"><span data-stu-id="9ef09-268">Select food by id</span></span> |<span data-ttu-id="9ef09-269">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="9ef09-269">~2.5 RU</span></span> |<span data-ttu-id="9ef09-270">1</span><span class="sxs-lookup"><span data-stu-id="9ef09-270">1</span></span> |
| <span data-ttu-id="9ef09-271">Selecteer levensmiddelen op fabrikant</span><span class="sxs-lookup"><span data-stu-id="9ef09-271">Select foods by manufacturer</span></span> |<span data-ttu-id="9ef09-272">~ 7 RU</span><span class="sxs-lookup"><span data-stu-id="9ef09-272">~7 RU</span></span> |<span data-ttu-id="9ef09-273">7</span><span class="sxs-lookup"><span data-stu-id="9ef09-273">7</span></span> |
| <span data-ttu-id="9ef09-274">Selecteer door Voedingsgroep en de volgorde op basis van gewicht</span><span class="sxs-lookup"><span data-stu-id="9ef09-274">Select by food group and order by weight</span></span> |<span data-ttu-id="9ef09-275">~ 70 RU</span><span class="sxs-lookup"><span data-stu-id="9ef09-275">~70 RU</span></span> |<span data-ttu-id="9ef09-276">100</span><span class="sxs-lookup"><span data-stu-id="9ef09-276">100</span></span> |
| <span data-ttu-id="9ef09-277">Bovenste 10 levensmiddelen in een Voedingsgroep selecteren</span><span class="sxs-lookup"><span data-stu-id="9ef09-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="9ef09-278">~ 10 RU</span><span class="sxs-lookup"><span data-stu-id="9ef09-278">~10 RU</span></span> |<span data-ttu-id="9ef09-279">10</span><span class="sxs-lookup"><span data-stu-id="9ef09-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="9ef09-280">RU kosten variëren op basis van het aantal items geretourneerd Hallo.</span><span class="sxs-lookup"><span data-stu-id="9ef09-280">RU charges vary based on hello number of items returned.</span></span>
> 
> 

<span data-ttu-id="9ef09-281">Met deze informatie kunnen we verwachten Hallo RU vereisten voor deze toepassing opgegeven Hallo aantal bewerkingen en query's die we verwachten dat per seconde:</span><span class="sxs-lookup"><span data-stu-id="9ef09-281">With this information, we can estimate hello RU requirements for this application given hello number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="9ef09-282">Bewerking/Query</span><span class="sxs-lookup"><span data-stu-id="9ef09-282">Operation/Query</span></span> | <span data-ttu-id="9ef09-283">Het geschatte aantal per seconde</span><span class="sxs-lookup"><span data-stu-id="9ef09-283">Estimated number per second</span></span> | <span data-ttu-id="9ef09-284">Vereiste RUs</span><span class="sxs-lookup"><span data-stu-id="9ef09-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9ef09-285">-Item maken</span><span class="sxs-lookup"><span data-stu-id="9ef09-285">Create item</span></span> |<span data-ttu-id="9ef09-286">10</span><span class="sxs-lookup"><span data-stu-id="9ef09-286">10</span></span> |<span data-ttu-id="9ef09-287">150</span><span class="sxs-lookup"><span data-stu-id="9ef09-287">150</span></span> |
| <span data-ttu-id="9ef09-288">Item lezen</span><span class="sxs-lookup"><span data-stu-id="9ef09-288">Read item</span></span> |<span data-ttu-id="9ef09-289">100</span><span class="sxs-lookup"><span data-stu-id="9ef09-289">100</span></span> |<span data-ttu-id="9ef09-290">100</span><span class="sxs-lookup"><span data-stu-id="9ef09-290">100</span></span> |
| <span data-ttu-id="9ef09-291">Selecteer levensmiddelen op fabrikant</span><span class="sxs-lookup"><span data-stu-id="9ef09-291">Select foods by manufacturer</span></span> |<span data-ttu-id="9ef09-292">25</span><span class="sxs-lookup"><span data-stu-id="9ef09-292">25</span></span> |<span data-ttu-id="9ef09-293">175</span><span class="sxs-lookup"><span data-stu-id="9ef09-293">175</span></span> |
| <span data-ttu-id="9ef09-294">Selecteer door de Voedingsgroep</span><span class="sxs-lookup"><span data-stu-id="9ef09-294">Select by food group</span></span> |<span data-ttu-id="9ef09-295">10</span><span class="sxs-lookup"><span data-stu-id="9ef09-295">10</span></span> |<span data-ttu-id="9ef09-296">700</span><span class="sxs-lookup"><span data-stu-id="9ef09-296">700</span></span> |
| <span data-ttu-id="9ef09-297">Selecteer top 10</span><span class="sxs-lookup"><span data-stu-id="9ef09-297">Select top 10</span></span> |<span data-ttu-id="9ef09-298">15</span><span class="sxs-lookup"><span data-stu-id="9ef09-298">15</span></span> |<span data-ttu-id="9ef09-299">150 totaal</span><span class="sxs-lookup"><span data-stu-id="9ef09-299">150 Total</span></span> |

<span data-ttu-id="9ef09-300">In dit geval we verwachten dat de vereiste van een gemiddelde doorvoersnelheid van 1,275 RU/s.</span><span class="sxs-lookup"><span data-stu-id="9ef09-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="9ef09-301">Afronden up toohello dichtstbijzijnde 100, zouden we 1.300 RU/s voor de verzameling van deze toepassing inrichten.</span><span class="sxs-lookup"><span data-stu-id="9ef09-301">Rounding up toohello nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="9ef09-302"><a id="RequestRateTooLarge"></a>Overschrijding van gereserveerde doorvoer grenzen in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="9ef09-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="9ef09-303">Intrekken dat verzoek eenheidsverbruik wordt beoordeeld als een percentage per seconde als Hallo budget leeg is.</span><span class="sxs-lookup"><span data-stu-id="9ef09-303">Recall that request unit consumption is evaluated as a rate per second if hello budget is empty.</span></span> <span data-ttu-id="9ef09-304">Voor toepassingen die groter zijn dan Hallo aanvragen ingerichte aanvraagsnelheid eenheid voor een container toothat verzameling wordt beperkt pas Hallo snelheid Hallo gereserveerd niveau.</span><span class="sxs-lookup"><span data-stu-id="9ef09-304">For applications that exceed hello provisioned request unit rate for a container, requests toothat collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="9ef09-305">Wanneer er een vertraging optreedt, eindigen Hallo server optie preventief Hallo-aanvraag met RequestRateTooLargeException (HTTP-statuscode 429) en wordt geretourneerd Hallo-header x-ms-opnieuw-na-ms aangegeven hoeveelheid tijd in milliseconden die gebruiker Hallo Hallo moet wachten voordat Hallo-aanvraag nogmaals te proberen.</span><span class="sxs-lookup"><span data-stu-id="9ef09-305">When a throttle occurs, hello server will preemptively end hello request with RequestRateTooLargeException (HTTP status code 429) and return hello x-ms-retry-after-ms header indicating hello amount of time, in milliseconds, that hello user must wait before reattempting hello request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="9ef09-306">Als u gebruikmaakt van Client-SDK voor .NET en LINQ Hallo-query's en vervolgens Hallo tijd die u nooit toodeal met deze uitzondering als de huidige versie van de Hallo van Client-SDK voor .NET Hallo impliciet dit antwoord dat de meeste, respecteert server opgegeven opnieuw proberen na header Hallo en Hallo-aanvraag voor nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="9ef09-306">If you are using hello .NET Client SDK and LINQ queries, then most of hello time you never have toodeal with this exception, as hello current version of hello .NET Client SDK implicitly catches this response, respects hello server-specified retry-after header, and retries hello request.</span></span> <span data-ttu-id="9ef09-307">Tenzij uw account wordt door meerdere clients tegelijkertijd geopend, wordt een nieuwe poging gedaan Hallo slaagt.</span><span class="sxs-lookup"><span data-stu-id="9ef09-307">Unless your account is being accessed concurrently by multiple clients, hello next retry will succeed.</span></span>

<span data-ttu-id="9ef09-308">Als er meer dan één client cumulatief werken boven aanvraagsnelheid hello, hello standaardgedrag voor opnieuw proberen niet toereikend zijn en Hallo client genereert een DocumentClientException met status code 429 toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="9ef09-308">If you have more than one client cumulatively operating above hello request rate, hello default retry behavior may not suffice, and hello client will throw a DocumentClientException with status code 429 toohello application.</span></span> <span data-ttu-id="9ef09-309">In dergelijke gevallen overweegt u verwerken gedrag voor het opnieuw en logica in uw toepassing fout routines voor het afhandelen of een uitbreiding van Hallo gereserveerde doorvoer voor Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="9ef09-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing hello reserved throughput for hello container.</span></span>

## <span data-ttu-id="9ef09-310"><a id="RequestRateTooLargeAPIforMongoDB"></a>Gereserveerde doorvoerlimieten in API overschrijden voor MongoDB</span><span class="sxs-lookup"><span data-stu-id="9ef09-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="9ef09-311">Toepassingen die groter is dan de aanvraageenheden Hallo ingericht voor een verzameling wordt pas Hallo snelheid Hallo gereserveerd niveau worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="9ef09-311">Applications that exceed hello provisioned request units for a collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="9ef09-312">Wanneer er een vertraging optreedt, Hallo back-end optie preventief eindigt Hallo-aanvraag met een *16500* foutcode - *te veel aanvragen*.</span><span class="sxs-lookup"><span data-stu-id="9ef09-312">When a throttle occurs, hello backend will preemptively end hello request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="9ef09-313">API voor MongoDB wordt standaard automatisch opnieuw van too10 tijden voordat er een *te veel aanvragen* foutcode.</span><span class="sxs-lookup"><span data-stu-id="9ef09-313">By default, API for MongoDB will automatically retry up too10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="9ef09-314">Als er veel *te veel aanvragen* foutcodes, kunt u ook beide toe te voegen gedrag voor het opnieuw in routines voor foutafhandeling van uw toepassing of [Hallo gereserveerde doorvoer voor Hallo verzamelingverhogen](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="9ef09-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing hello reserved throughput for hello collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ef09-315">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9ef09-315">Next steps</span></span>
<span data-ttu-id="9ef09-316">toolearn meer informatie over gereserveerde doorvoer met Azure DB die Cosmos-databases, bekijk deze resources:</span><span class="sxs-lookup"><span data-stu-id="9ef09-316">toolearn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="9ef09-317">Prijzen van Azure DB Cosmos</span><span class="sxs-lookup"><span data-stu-id="9ef09-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="9ef09-318">Gegevens in Azure Cosmos DB te partitioneren</span><span class="sxs-lookup"><span data-stu-id="9ef09-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="9ef09-319">toolearn meer informatie over Azure Cosmos DB Zie hello Azure Cosmos DB [documentatie](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="9ef09-319">toolearn more about Azure Cosmos DB, see hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="9ef09-320">Zie tooget gestart met de schaal en prestaties testen met Azure Cosmos DB [prestaties en schaal testen met Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="9ef09-320">tooget started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
