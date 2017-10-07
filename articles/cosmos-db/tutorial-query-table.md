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
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a>Azure Cosmos DB: Hoe gegevens in een tabel met behulp van tooquery Hallo tabel-API (preview)?

Hello Azure Cosmos DB [tabel API](table-introduction.md) (preview) biedt ondersteuning voor OData en [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) een query uitgevoerd op gegevens van de sleutelwaarde (tabel).  

Dit artikel behandelt Hallo taken te volgen: 

> [!div class="checklist"]
> * Een query met Hallo tabel-API

Hallo query's in dit artikel gebruiken Hallo voorbeeld te volgen `People` tabel:

| PartitionKey | RowKey | E-mail | Telefoonnummer |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

Omdat Azure Cosmos DB compatibel met hello Azure Table storage-API's is, Zie [opvragen van tabellen en entiteiten] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) voor meer informatie over hoe tooquery met behulp van Hallo Tabel-API. 

Zie voor meer informatie over Hallo premium mogelijkheden die Azure Cosmos DB biedt [Azure Cosmos DB: tabel API](table-introduction.md) en [ontwikkelen met Hallo tabel API in .NET](tutorial-develop-table-dotnet.md). 

## <a name="prerequisites"></a>Vereisten

Voor deze toowork query's moet u een Azure DB die Cosmos-account hebt en entiteitsgegevens in Hallo container hebt. Geen van deze? Volledige Hallo [vijf minuten Quick Start](https://aka.ms/acdbtnetqs) of Hallo [developer-zelfstudie](https://aka.ms/acdbtabletut) toocreate een account en vul uw database.

## <a name="query-on-partitionkey-and-rowkey"></a>Query op PartitionKey en RowKey
Omdat Hallo PartitionKey en RowKey eigenschappen primaire sleutel van een entiteit vormen, kunt u Hallo speciale syntaxis tooidentify Hallo entiteit te volgen: 

**Query**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**Resultaten**

| PartitionKey | RowKey | E-mail | Telefoonnummer |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

U kunt deze eigenschappen ook opgeven als onderdeel van Hallo `$filter` optie, zoals wordt weergegeven in de volgende sectie Hallo. Houd er rekening mee dat Hallo sleuteleigenschap namen en constante waarden hoofdlettergevoelig zijn. Hallo PartitionKey zowel RowKey eigenschappen zijn van het type String. 

## <a name="query-by-using-an-odata-filter"></a>Query uitvoeren met behulp van een OData-filter
Wanneer u een filtertekenreeks construeren bent, houd er rekening mee deze regels: 

* Hallo logische operators gedefinieerd door Hallo OData Protocol Specification toocompare een eigenschapswaarde tooa gebruiken. Houd er rekening mee dat u een dynamische waarde van eigenschap tooa kan niet worden vergeleken. Een-zijde van Hallo-expressie moet een constante zijn. 
* naam van de eigenschap Hello, operator en constante waarde moeten worden gescheiden door spaties URL-codering. Een spatie is het URL-codering als `%20`. 
* Alle onderdelen van de filtertekenreeks Hallo zijn hoofdlettergevoelig. 
* Hallo constante waarde moet van het Hallo hetzelfde gegevenstype als de eigenschap hello om Hallo filter tooreturn geldige resultaten. Zie voor meer informatie over ondersteunde eigenschaptypen [Understanding Hallo Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model). 

Hier volgt een voorbeeldquery die laat zien hoe toofilter door PartitionKey Hallo en e-eigenschappen met behulp van een OData `$filter`.

**Query**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Zie voor meer informatie over hoe tooconstruct Filterexpressies voor verschillende soorten gegevens, [opvragen van tabellen en entiteiten](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).

**Resultaten**

| PartitionKey | RowKey | E-mail | Telefoonnummer |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>Query uitvoeren met behulp van LINQ 
U kunt ook een query met behulp van LINQ, die toohello bijbehorende de OData-query-expressies omzet. Hier volgt een voorbeeld van hoe toobuild query's met .NET SDK Hallo:

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

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Hebt u geleerd hoe tooquery met behulp van Hallo tabel-API (preview) 

U kunt nu de volgende zelfstudie toolearn toohello hoe doorgaan toodistribute uw gegevens globaal.

> [!div class="nextstepaction"]
> [Uw gegevens globaal distribueren](tutorial-global-distribution-documentdb.md)
