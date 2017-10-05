---
title: Hoe kan ik een query over tabelgegevens in Azure Cosmos DB? | Microsoft Docs
description: Informatie over het query-tabelgegevens in Azure Cosmos-DB
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
ms.openlocfilehash: e59cfa85c6bf584e44bdc6e88cc19d67df390041
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a><span data-ttu-id="92458-104">Azure Cosmos DB: Hoe een query over tabelgegevens met behulp van de tabel-API (preview)?</span><span class="sxs-lookup"><span data-stu-id="92458-104">Azure Cosmos DB: How to query table data by using the Table API (preview)?</span></span>

<span data-ttu-id="92458-105">De Azure DB die Cosmos [tabel API](table-introduction.md) (preview) biedt ondersteuning voor OData en [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) een query uitgevoerd op gegevens van de sleutelwaarde (tabel).</span><span class="sxs-lookup"><span data-stu-id="92458-105">The Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="92458-106">In dit artikel bevat informatie over de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="92458-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="92458-107">Een query met de tabel-API</span><span class="sxs-lookup"><span data-stu-id="92458-107">Querying data with the Table API</span></span>

<span data-ttu-id="92458-108">De query's in dit artikel gebruik het volgende voorbeeld `People` tabel:</span><span class="sxs-lookup"><span data-stu-id="92458-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="92458-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="92458-109">PartitionKey</span></span> | <span data-ttu-id="92458-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="92458-110">RowKey</span></span> | <span data-ttu-id="92458-111">E-mail</span><span class="sxs-lookup"><span data-stu-id="92458-111">Email</span></span> | <span data-ttu-id="92458-112">Telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="92458-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="92458-113">Harp</span><span class="sxs-lookup"><span data-stu-id="92458-113">Harp</span></span> | <span data-ttu-id="92458-114">Walter</span><span class="sxs-lookup"><span data-stu-id="92458-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="92458-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="92458-115">425-555-0101</span></span> |
| <span data-ttu-id="92458-116">Smith</span><span class="sxs-lookup"><span data-stu-id="92458-116">Smith</span></span> | <span data-ttu-id="92458-117">Ben</span><span class="sxs-lookup"><span data-stu-id="92458-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="92458-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="92458-118">425-555-0102</span></span> |
| <span data-ttu-id="92458-119">Smith</span><span class="sxs-lookup"><span data-stu-id="92458-119">Smith</span></span> | <span data-ttu-id="92458-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="92458-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="92458-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="92458-121">425-555-0104</span></span> | 

<span data-ttu-id="92458-122">Omdat Azure Cosmos DB compatibel met de Azure Table storage-API's is, Zie [opvragen van tabellen en entiteiten] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) voor meer informatie over de query met behulp van de tabel API.</span><span class="sxs-lookup"><span data-stu-id="92458-122">Because Azure Cosmos DB is compatible with the Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="92458-123">Zie voor meer informatie over de premium-mogelijkheden die Azure Cosmos DB biedt [Azure Cosmos DB: tabel API](table-introduction.md) en [ontwikkelen met de API van de tabel in .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="92458-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="92458-124">Vereisten</span><span class="sxs-lookup"><span data-stu-id="92458-124">Prerequisites</span></span>

<span data-ttu-id="92458-125">Voor deze query's werken, moet u een Azure DB die Cosmos-account hebt en entiteitsgegevens in de container hebt.</span><span class="sxs-lookup"><span data-stu-id="92458-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="92458-126">Geen van deze?</span><span class="sxs-lookup"><span data-stu-id="92458-126">Don't have any of those?</span></span> <span data-ttu-id="92458-127">Voltooi de [vijf minuten Quick Start](https://aka.ms/acdbtnetqs) of de [developer-zelfstudie](https://aka.ms/acdbtabletut) voor het maken van een account en vul uw database.</span><span class="sxs-lookup"><span data-stu-id="92458-127">Complete the [five-minute quickstart](https://aka.ms/acdbtnetqs) or the [developer tutorial](https://aka.ms/acdbtabletut) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="92458-128">Query op PartitionKey en RowKey</span><span class="sxs-lookup"><span data-stu-id="92458-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="92458-129">Omdat de eigenschappen PartitionKey en RowKey primaire sleutel van een entiteit vormen, kunt u de volgende specifieke syntaxis voor het identificeren van de entiteit:</span><span class="sxs-lookup"><span data-stu-id="92458-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="92458-130">**Query**</span><span class="sxs-lookup"><span data-stu-id="92458-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="92458-131">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="92458-131">**Results**</span></span>

| <span data-ttu-id="92458-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="92458-132">PartitionKey</span></span> | <span data-ttu-id="92458-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="92458-133">RowKey</span></span> | <span data-ttu-id="92458-134">E-mail</span><span class="sxs-lookup"><span data-stu-id="92458-134">Email</span></span> | <span data-ttu-id="92458-135">Telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="92458-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="92458-136">Harp</span><span class="sxs-lookup"><span data-stu-id="92458-136">Harp</span></span> | <span data-ttu-id="92458-137">Walter</span><span class="sxs-lookup"><span data-stu-id="92458-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="92458-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="92458-138">425-555-0104</span></span> |

<span data-ttu-id="92458-139">U kunt deze eigenschappen ook opgeven als onderdeel van de `$filter` optie, zoals wordt weergegeven in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="92458-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="92458-140">Houd er rekening mee dat de namen van de sleuteleigenschap en constante waarden hoofdlettergevoelig zijn.</span><span class="sxs-lookup"><span data-stu-id="92458-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="92458-141">De PartitionKey en de RowKey eigenschappen zijn van het type String.</span><span class="sxs-lookup"><span data-stu-id="92458-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="92458-142">Query uitvoeren met behulp van een OData-filter</span><span class="sxs-lookup"><span data-stu-id="92458-142">Query by using an OData filter</span></span>
<span data-ttu-id="92458-143">Wanneer u een filtertekenreeks construeren bent, houd er rekening mee deze regels:</span><span class="sxs-lookup"><span data-stu-id="92458-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="92458-144">De logische operators gedefinieerd door de specificatie van de OData-Protocol gebruiken om te vergelijken van een eigenschap een waarde.</span><span class="sxs-lookup"><span data-stu-id="92458-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="92458-145">Houd er rekening mee dat u een eigenschap aan een dynamische waarde kan niet worden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="92458-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="92458-146">Een-zijde van de expressie moet een constante zijn.</span><span class="sxs-lookup"><span data-stu-id="92458-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="92458-147">De eigenschapsnaam, een operator en een constante waarde moeten worden gescheiden door spaties URL-codering.</span><span class="sxs-lookup"><span data-stu-id="92458-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="92458-148">Een spatie is het URL-codering als `%20`.</span><span class="sxs-lookup"><span data-stu-id="92458-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="92458-149">Alle onderdelen van de filtertekenreeks zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="92458-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="92458-150">De constante waarde moet van hetzelfde gegevenstype als de eigenschap om het filter geldige resultaten retourneren.</span><span class="sxs-lookup"><span data-stu-id="92458-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="92458-151">Zie voor meer informatie over ondersteunde eigenschaptypen [inzicht in de tabel Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="92458-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="92458-152">Hier volgt een voorbeeldquery die laat hoe u de eigenschappen PartitionKey en e-mail filteren zien met behulp van een OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="92458-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="92458-153">**Query**</span><span class="sxs-lookup"><span data-stu-id="92458-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="92458-154">Zie voor meer informatie over het samenstellen van Filterexpressies voor verschillende soorten gegevens [opvragen van tabellen en entiteiten](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="92458-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="92458-155">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="92458-155">**Results**</span></span>

| <span data-ttu-id="92458-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="92458-156">PartitionKey</span></span> | <span data-ttu-id="92458-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="92458-157">RowKey</span></span> | <span data-ttu-id="92458-158">E-mail</span><span class="sxs-lookup"><span data-stu-id="92458-158">Email</span></span> | <span data-ttu-id="92458-159">Telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="92458-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="92458-160">Ben</span><span class="sxs-lookup"><span data-stu-id="92458-160">Ben</span></span> |<span data-ttu-id="92458-161">Smith</span><span class="sxs-lookup"><span data-stu-id="92458-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="92458-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="92458-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="92458-163">Query uitvoeren met behulp van LINQ</span><span class="sxs-lookup"><span data-stu-id="92458-163">Query by using LINQ</span></span> 
<span data-ttu-id="92458-164">U kunt ook een query met behulp van LINQ, die wordt vertaald naar de bijbehorende OData-query-expressies.</span><span class="sxs-lookup"><span data-stu-id="92458-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="92458-165">Hier volgt een voorbeeld van hoe u query's opbouwen met behulp van de .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="92458-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="92458-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92458-166">Next steps</span></span>

<span data-ttu-id="92458-167">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="92458-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="92458-168">Hebt geleerd hoe u een query met behulp van de tabel-API (preview)</span><span class="sxs-lookup"><span data-stu-id="92458-168">Learned how to query by using the Table API (preview)</span></span> 

<span data-ttu-id="92458-169">U kunt nu doorgaan met de volgende zelfstudie voor informatie over het distribueren van uw gegevens globaal.</span><span class="sxs-lookup"><span data-stu-id="92458-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="92458-170">Uw gegevens globaal distribueren</span><span class="sxs-lookup"><span data-stu-id="92458-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
