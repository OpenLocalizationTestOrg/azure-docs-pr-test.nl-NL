---
title: aaaWorking met datums in Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe toowork met datums in Azure Cosmos DB.
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="504b6-103">Werken met datums in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="504b6-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="504b6-104">Azure Cosmos DB biedt schemaflexibiliteit en geavanceerde indexeermogelijkheden via een systeemeigen [JSON](http://www.json.org) gegevensmodel.</span><span class="sxs-lookup"><span data-stu-id="504b6-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="504b6-105">Alle Azure DB die Cosmos-bronnen, zoals databases, verzamelingen, documenten en opgeslagen procedures worden gemodelleerd en opgeslagen als JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="504b6-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="504b6-106">Als een vereiste voor draagbare wordt JSON (en Azure Cosmos DB) ondersteunt een kleine set basistypen: String, getal, Booleaanse waarde, Array, Object en Null.</span><span class="sxs-lookup"><span data-stu-id="504b6-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="504b6-107">Echter JSON is flexibel en ontwikkelaars en frameworks toorepresent meer complexe typen met behulp van deze primitieven en samenstellen van deze objecten of-matrices.</span><span class="sxs-lookup"><span data-stu-id="504b6-107">However, JSON is flexible and allow developers and frameworks toorepresent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="504b6-108">Veel toepassingen moeten toevoeging toohello basistypen, Hallo [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) typen toorepresent en tijdstempels.</span><span class="sxs-lookup"><span data-stu-id="504b6-108">In addition toohello basic types, many applications need hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type toorepresent dates and timestamps.</span></span> <span data-ttu-id="504b6-109">Dit artikel wordt beschreven hoe ontwikkelaars kunnen opslaan, ophalen en query datums in Azure Cosmos DB met Hallo .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="504b6-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using hello .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="504b6-110">Opslaan van datum/tijd</span><span class="sxs-lookup"><span data-stu-id="504b6-110">Storing DateTimes</span></span>
<span data-ttu-id="504b6-111">Standaard Hallo [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serialiseert datum/tijd-waarden als [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="504b6-111">By default, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="504b6-112">De meeste toepassingen kunnen Hallo standaard tekenreeksweergave voor datum/tijd gebruiken voor Hallo volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="504b6-112">Most applications can use hello default string representation for DateTime for hello following reasons:</span></span>

* <span data-ttu-id="504b6-113">Tekenreeksen kunnen worden vergeleken en Hallo relatieve ordening van Hallo DateTime-waarden behouden blijft wanneer ze getransformeerd toostrings zijn.</span><span class="sxs-lookup"><span data-stu-id="504b6-113">Strings can be compared, and hello relative ordering of hello DateTime values is preserved when they are transformed toostrings.</span></span> 
* <span data-ttu-id="504b6-114">Deze benadering vereist geen aangepaste code of -kenmerken voor JSON-conversie.</span><span class="sxs-lookup"><span data-stu-id="504b6-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="504b6-115">Hallo datums die is opgeslagen in JSON menselijke worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="504b6-115">hello dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="504b6-116">Deze aanpak kunt profiteren van Azure Cosmos DB index voor snelle queryprestaties.</span><span class="sxs-lookup"><span data-stu-id="504b6-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="504b6-117">Bijvoorbeeld Hallo volgende codefragment slaat een `Order` objecteigenschappen met twee DateTime - `ShipDate` en `OrderDate` als een document met behulp van Hallo .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="504b6-117">For example, hello following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using hello .NET SDK:</span></span>

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

<span data-ttu-id="504b6-118">Dit document wordt opgeslagen in Azure Cosmos DB als volgt:</span><span class="sxs-lookup"><span data-stu-id="504b6-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="504b6-119">U kunt ook kunt u de datum/tijd als Unix tijdstempels, dat wil zeggen, opslaan als een getal dat het aantal verstreken seconden sinds 1 januari 1970 Hallo vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="504b6-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing hello number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="504b6-120">Interne tijdstempel Azure Cosmos-DB (`_ts`) eigenschap deze aanpak volgt.</span><span class="sxs-lookup"><span data-stu-id="504b6-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="504b6-121">U kunt Hallo [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) klasse tooserialize datum/tijd as-nummers.</span><span class="sxs-lookup"><span data-stu-id="504b6-121">You can use hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class tooserialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="504b6-122">Indexeren van datum/tijd voor query's bereik</span><span class="sxs-lookup"><span data-stu-id="504b6-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="504b6-123">Bereik query's zijn veelvoorkomende met DateTime-waarden.</span><span class="sxs-lookup"><span data-stu-id="504b6-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="504b6-124">Als u toofind alle orders die zijn gemaakt sinds gisteren moet of zoeken naar alle bestellingen laatste vijf minuten in Hallo hebt verzonden, moet u bijvoorbeeld tooperform bereik query's.</span><span class="sxs-lookup"><span data-stu-id="504b6-124">For example, if you need toofind all orders created since yesterday, or find all orders shipped in hello last five minutes, you need tooperform range queries.</span></span> <span data-ttu-id="504b6-125">tooexecute deze efficiënt query's, moet u uw collectie bereik indexeren op tekenreeksen configureren.</span><span class="sxs-lookup"><span data-stu-id="504b6-125">tooexecute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="504b6-126">U kunt meer informatie over het tooconfigure beleid op indexeren [Azure Cosmos DB indexeren beleid](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="504b6-126">You can learn more about how tooconfigure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="504b6-127">Datum/tijd in LINQ opvragen</span><span class="sxs-lookup"><span data-stu-id="504b6-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="504b6-128">Hallo DocumentDB .NET SDK ondersteunt automatisch gegevens opgeslagen in Azure Cosmos DB via LINQ opvragen.</span><span class="sxs-lookup"><span data-stu-id="504b6-128">hello DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="504b6-129">Bijvoorbeeld: hello volgende fragment geeft een LINQ-query die filters weer die zijn verzonden in Hallo afgelopen drie dagen.</span><span class="sxs-lookup"><span data-stu-id="504b6-129">For example, hello following snippet shows a LINQ query that filters orders that were shipped in hello last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="504b6-130">U kunt meer informatie over Azure Cosmos DB SQL query taal en Hallo LINQ-provider op [Cosmos DB opvragen](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="504b6-130">You can learn more about Azure Cosmos DB's SQL query language and hello LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="504b6-131">In dit artikel, die we kijken hoe toostore, index en het opvragen van datum/tijd in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="504b6-131">In this article, we looked at how toostore, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="504b6-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="504b6-132">Next Steps</span></span>
* <span data-ttu-id="504b6-133">Downloaden en uitvoeren van Hallo [codevoorbeelden op GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="504b6-133">Download and run hello [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="504b6-134">Meer informatie over [DocumentDB API-Query](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="504b6-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="504b6-135">Meer informatie over [Azure Cosmos DB indexeren beleid](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="504b6-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
