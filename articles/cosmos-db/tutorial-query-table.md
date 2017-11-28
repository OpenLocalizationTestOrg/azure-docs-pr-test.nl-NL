---
title: aaaHow tooquery tabelgegevens in Azure Cosmos DB? | Microsoft Docs
description: Meer informatie over tooquery tabelgegevens in Azure Cosmos-DB
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a><span data-ttu-id="48ed1-104">Azure Cosmos DB: Hoe gegevens in een tabel met behulp van tooquery Hallo tabel-API (preview)?</span><span class="sxs-lookup"><span data-stu-id="48ed1-104">Azure Cosmos DB: How tooquery table data by using hello Table API (preview)?</span></span>

<span data-ttu-id="48ed1-105">Hello Azure Cosmos DB [tabel API](table-introduction.md) (preview) biedt ondersteuning voor OData en [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) een query uitgevoerd op gegevens van de sleutelwaarde (tabel).</span><span class="sxs-lookup"><span data-stu-id="48ed1-105">hello Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="48ed1-106">Dit artikel behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="48ed1-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="48ed1-107">Een query met Hallo tabel-API</span><span class="sxs-lookup"><span data-stu-id="48ed1-107">Querying data with hello Table API</span></span>

<span data-ttu-id="48ed1-108">Hallo query's in dit artikel gebruiken Hallo voorbeeld te volgen `People` tabel:</span><span class="sxs-lookup"><span data-stu-id="48ed1-108">hello queries in this article use hello following sample `People` table:</span></span>

| <span data-ttu-id="48ed1-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="48ed1-109">PartitionKey</span></span> | <span data-ttu-id="48ed1-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="48ed1-110">RowKey</span></span> | <span data-ttu-id="48ed1-111">E-mail</span><span class="sxs-lookup"><span data-stu-id="48ed1-111">Email</span></span> | <span data-ttu-id="48ed1-112">Telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="48ed1-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="48ed1-113">Harp</span><span class="sxs-lookup"><span data-stu-id="48ed1-113">Harp</span></span> | <span data-ttu-id="48ed1-114">Walter</span><span class="sxs-lookup"><span data-stu-id="48ed1-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="48ed1-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="48ed1-115">425-555-0101</span></span> |
| <span data-ttu-id="48ed1-116">Smith</span><span class="sxs-lookup"><span data-stu-id="48ed1-116">Smith</span></span> | <span data-ttu-id="48ed1-117">Ben</span><span class="sxs-lookup"><span data-stu-id="48ed1-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="48ed1-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="48ed1-118">425-555-0102</span></span> |
| <span data-ttu-id="48ed1-119">Smith</span><span class="sxs-lookup"><span data-stu-id="48ed1-119">Smith</span></span> | <span data-ttu-id="48ed1-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="48ed1-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="48ed1-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="48ed1-121">425-555-0104</span></span> | 

<span data-ttu-id="48ed1-122">Omdat Azure Cosmos DB compatibel met hello Azure Table storage-API's is, Zie [opvragen van tabellen en entiteiten] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) voor meer informatie over hoe tooquery met behulp van Hallo Tabel-API.</span><span class="sxs-lookup"><span data-stu-id="48ed1-122">Because Azure Cosmos DB is compatible with hello Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how tooquery by using hello Table API.</span></span> 

<span data-ttu-id="48ed1-123">Zie voor meer informatie over Hallo premium mogelijkheden die Azure Cosmos DB biedt [Azure Cosmos DB: tabel API](table-introduction.md) en [ontwikkelen met Hallo tabel API in .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="48ed1-123">For more information on hello premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with hello Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="48ed1-124">Vereisten</span><span class="sxs-lookup"><span data-stu-id="48ed1-124">Prerequisites</span></span>

<span data-ttu-id="48ed1-125">Voor deze toowork query's moet u een Azure DB die Cosmos-account hebt en entiteitsgegevens in Hallo container hebt.</span><span class="sxs-lookup"><span data-stu-id="48ed1-125">For these queries toowork, you must have an Azure Cosmos DB account and have entity data in hello container.</span></span> <span data-ttu-id="48ed1-126">Geen van deze?</span><span class="sxs-lookup"><span data-stu-id="48ed1-126">Don't have any of those?</span></span> <span data-ttu-id="48ed1-127">Volledige Hallo [vijf minuten Quick Start](https://aka.ms/acdbtnetqs) of Hallo [developer-zelfstudie](https://aka.ms/acdbtabletut) toocreate een account en vul uw database.</span><span class="sxs-lookup"><span data-stu-id="48ed1-127">Complete hello [five-minute quickstart](https://aka.ms/acdbtnetqs) or hello [developer tutorial](https://aka.ms/acdbtabletut) toocreate an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="48ed1-128">Query op PartitionKey en RowKey</span><span class="sxs-lookup"><span data-stu-id="48ed1-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="48ed1-129">Omdat Hallo PartitionKey en RowKey eigenschappen primaire sleutel van een entiteit vormen, kunt u Hallo speciale syntaxis tooidentify Hallo entiteit te volgen:</span><span class="sxs-lookup"><span data-stu-id="48ed1-129">Because hello PartitionKey and RowKey properties form an entity's primary key, you can use hello following special syntax tooidentify hello entity:</span></span> 

<span data-ttu-id="48ed1-130">**Query**</span><span class="sxs-lookup"><span data-stu-id="48ed1-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="48ed1-131">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="48ed1-131">**Results**</span></span>

| <span data-ttu-id="48ed1-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="48ed1-132">PartitionKey</span></span> | <span data-ttu-id="48ed1-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="48ed1-133">RowKey</span></span> | <span data-ttu-id="48ed1-134">E-mail</span><span class="sxs-lookup"><span data-stu-id="48ed1-134">Email</span></span> | <span data-ttu-id="48ed1-135">Telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="48ed1-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="48ed1-136">Harp</span><span class="sxs-lookup"><span data-stu-id="48ed1-136">Harp</span></span> | <span data-ttu-id="48ed1-137">Walter</span><span class="sxs-lookup"><span data-stu-id="48ed1-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="48ed1-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="48ed1-138">425-555-0104</span></span> |

<span data-ttu-id="48ed1-139">U kunt deze eigenschappen ook opgeven als onderdeel van Hallo `$filter` optie, zoals wordt weergegeven in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="48ed1-139">Alternatively, you can specify these properties as part of hello `$filter` option, as shown in hello following section.</span></span> <span data-ttu-id="48ed1-140">Houd er rekening mee dat Hallo sleuteleigenschap namen en constante waarden hoofdlettergevoelig zijn.</span><span class="sxs-lookup"><span data-stu-id="48ed1-140">Note that hello key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="48ed1-141">Hallo PartitionKey zowel RowKey eigenschappen zijn van het type String.</span><span class="sxs-lookup"><span data-stu-id="48ed1-141">Both hello PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="48ed1-142">Query uitvoeren met behulp van een OData-filter</span><span class="sxs-lookup"><span data-stu-id="48ed1-142">Query by using an OData filter</span></span>
<span data-ttu-id="48ed1-143">Wanneer u een filtertekenreeks construeren bent, houd er rekening mee deze regels:</span><span class="sxs-lookup"><span data-stu-id="48ed1-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="48ed1-144">Hallo logische operators gedefinieerd door Hallo OData Protocol Specification toocompare een eigenschapswaarde tooa gebruiken.</span><span class="sxs-lookup"><span data-stu-id="48ed1-144">Use hello logical operators defined by hello OData Protocol Specification toocompare a property tooa value.</span></span> <span data-ttu-id="48ed1-145">Houd er rekening mee dat u een dynamische waarde van eigenschap tooa kan niet worden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="48ed1-145">Note that you can't compare a property tooa dynamic value.</span></span> <span data-ttu-id="48ed1-146">Een-zijde van Hallo-expressie moet een constante zijn.</span><span class="sxs-lookup"><span data-stu-id="48ed1-146">One side of hello expression must be a constant.</span></span> 
* <span data-ttu-id="48ed1-147">naam van de eigenschap Hello, operator en constante waarde moeten worden gescheiden door spaties URL-codering.</span><span class="sxs-lookup"><span data-stu-id="48ed1-147">hello property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="48ed1-148">Een spatie is het URL-codering als `%20`.</span><span class="sxs-lookup"><span data-stu-id="48ed1-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="48ed1-149">Alle onderdelen van de filtertekenreeks Hallo zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="48ed1-149">All parts of hello filter string are case-sensitive.</span></span> 
* <span data-ttu-id="48ed1-150">Hallo constante waarde moet van het Hallo hetzelfde gegevenstype als de eigenschap hello om Hallo filter tooreturn geldige resultaten.</span><span class="sxs-lookup"><span data-stu-id="48ed1-150">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="48ed1-151">Zie voor meer informatie over ondersteunde eigenschaptypen [Understanding Hallo Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="48ed1-151">For more information about supported property types, see [Understanding hello Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="48ed1-152">Hier volgt een voorbeeldquery die laat zien hoe toofilter door PartitionKey Hallo en e-eigenschappen met behulp van een OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="48ed1-152">Here's an example query that shows how toofilter by hello PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="48ed1-153">**Query**</span><span class="sxs-lookup"><span data-stu-id="48ed1-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="48ed1-154">Zie voor meer informatie over hoe tooconstruct Filterexpressies voor verschillende soorten gegevens, [opvragen van tabellen en entiteiten](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="48ed1-154">For more information on how tooconstruct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="48ed1-155">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="48ed1-155">**Results**</span></span>

| <span data-ttu-id="48ed1-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="48ed1-156">PartitionKey</span></span> | <span data-ttu-id="48ed1-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="48ed1-157">RowKey</span></span> | <span data-ttu-id="48ed1-158">E-mail</span><span class="sxs-lookup"><span data-stu-id="48ed1-158">Email</span></span> | <span data-ttu-id="48ed1-159">Telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="48ed1-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="48ed1-160">Ben</span><span class="sxs-lookup"><span data-stu-id="48ed1-160">Ben</span></span> |<span data-ttu-id="48ed1-161">Smith</span><span class="sxs-lookup"><span data-stu-id="48ed1-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="48ed1-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="48ed1-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="48ed1-163">Query uitvoeren met behulp van LINQ</span><span class="sxs-lookup"><span data-stu-id="48ed1-163">Query by using LINQ</span></span> 
<span data-ttu-id="48ed1-164">U kunt ook een query met behulp van LINQ, die toohello bijbehorende de OData-query-expressies omzet.</span><span class="sxs-lookup"><span data-stu-id="48ed1-164">You can also query by using LINQ, which translates toohello corresponding OData query expressions.</span></span> <span data-ttu-id="48ed1-165">Hier volgt een voorbeeld van hoe toobuild query's met .NET SDK Hallo:</span><span class="sxs-lookup"><span data-stu-id="48ed1-165">Here's an example of how toobuild queries by using hello .NET SDK:</span></span>

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a><span data-ttu-id="48ed1-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48ed1-166">Next steps</span></span>

<span data-ttu-id="48ed1-167">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="48ed1-167">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="48ed1-168">Hebt u geleerd hoe tooquery met behulp van Hallo tabel-API (preview)</span><span class="sxs-lookup"><span data-stu-id="48ed1-168">Learned how tooquery by using hello Table API (preview)</span></span> 

<span data-ttu-id="48ed1-169">U kunt nu de volgende zelfstudie toolearn toohello hoe doorgaan toodistribute uw gegevens globaal.</span><span class="sxs-lookup"><span data-stu-id="48ed1-169">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="48ed1-170">Uw gegevens globaal distribueren</span><span class="sxs-lookup"><span data-stu-id="48ed1-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
