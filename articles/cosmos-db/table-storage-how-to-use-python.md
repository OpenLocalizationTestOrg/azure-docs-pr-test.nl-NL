---
title: Azure Table storage gebruiken met behulp van Python | Microsoft Docs
description: Sla gestructureerde gegevens op in de cloud met Azure Table Storage, een oplossing voor NoSQL-gegevensopslag.
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: mimig
ms.openlocfilehash: 0c46f04786ba4b62bd7ca22c5e25643123e6e136
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-in-python"></a><span data-ttu-id="c1da7-103">Table storage gebruiken in Python</span><span class="sxs-lookup"><span data-stu-id="c1da7-103">How to use Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="c1da7-104">Deze handleiding wordt beschreven hoe u veelvoorkomende scenario's voor Azure Table-opslag om in te voeren met behulp van Python de [Microsoft Azure-opslag-SDK voor Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="c1da7-104">This guide shows you how to perform common Azure Table storage scenarios in Python using the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="c1da7-105">De scenario's worden behandeld bevatten maken en verwijderen van een tabel en het invoegen en het opvragen van entiteiten.</span><span class="sxs-lookup"><span data-stu-id="c1da7-105">The scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="c1da7-106">Tijdens het werken met de scenario's in deze zelfstudie kunt u desgewenst om te verwijzen naar de [Azure-opslag-SDK voor Python-API-referentiemateriaal](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="c1da7-106">While working through the scenarios in this tutorial, you may wish to refer to the [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a><span data-ttu-id="c1da7-107">De Azure Storage-SDK voor Python installeren</span><span class="sxs-lookup"><span data-stu-id="c1da7-107">Install the Azure Storage SDK for Python</span></span>

<span data-ttu-id="c1da7-108">Als u een opslagaccount hebt gemaakt, wordt de volgende stap is het installeren van de [Microsoft Azure-opslag-SDK voor Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="c1da7-108">Once you've created a storage account, your next step is to install the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="c1da7-109">Raadpleeg voor meer informatie over het installeren van de SDK de [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) bestand in de opslag-SDK voor Python-opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="c1da7-109">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in the Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="c1da7-110">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="c1da7-110">Create a table</span></span>

<span data-ttu-id="c1da7-111">Met de service Azure Table in Python wilt werken, moet u importeren de [TableService] [ py_TableService] module.</span><span class="sxs-lookup"><span data-stu-id="c1da7-111">To work with the Azure Table service in Python, you must import the [TableService][py_TableService] module.</span></span> <span data-ttu-id="c1da7-112">Omdat u met tabelentiteiten werken gaat, moet u ook de [entiteit] [ py_Entity] klasse.</span><span class="sxs-lookup"><span data-stu-id="c1da7-112">Since you'll be working with Table entities, you also need the [Entity][py_Entity] class.</span></span> <span data-ttu-id="c1da7-113">Voeg deze code boven uw Python-bestand voor het importeren van beide:</span><span class="sxs-lookup"><span data-stu-id="c1da7-113">Add this code near the top your Python file to import both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="c1da7-114">Maak een [TableService] [ py_TableService] -object doorgeven in een naam en sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c1da7-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="c1da7-115">Vervang `myaccount` en `mykey` met uw accountnaam en -sleutel en aanroep [create_table] [ py_create_table] naar de tabel maken in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c1da7-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] to create the table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="c1da7-116">Een entiteit toevoegen aan een tabel</span><span class="sxs-lookup"><span data-stu-id="c1da7-116">Add an entity to a table</span></span>

<span data-ttu-id="c1da7-117">Als u wilt een entiteit toevoegen, maakt u eerst een object die uw entiteit vertegenwoordigt, en vervolgens geeft het object de [TableService][py_TableService].[ insert_entity] [ py_insert_entity] methode.</span><span class="sxs-lookup"><span data-stu-id="c1da7-117">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="c1da7-118">Het entiteitsobject mag een woordenboek of een object van type [entiteit][py_Entity], en de namen en waarden van uw entiteit definieert.</span><span class="sxs-lookup"><span data-stu-id="c1da7-118">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="c1da7-119">Elke entiteit moet bevatten de vereiste [PartitionKey en RowKey](#partitionkey-and-rowkey) eigenschappen, naast de andere eigenschappen die u voor de entiteit definieert.</span><span class="sxs-lookup"><span data-stu-id="c1da7-119">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="c1da7-120">In dit voorbeeld maakt u een dictionary-object dat een entiteit vertegenwoordigt vervolgens doorgegeven aan de [insert_entity] [ py_insert_entity] methode toe te voegen aan de tabel:</span><span class="sxs-lookup"><span data-stu-id="c1da7-120">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="c1da7-121">In dit voorbeeld wordt een [entiteit] [ py_Entity] object en vervolgens doorgegeven aan de [insert_entity] [ py_insert_entity] methode toe te voegen aan de tabel:</span><span class="sxs-lookup"><span data-stu-id="c1da7-121">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="c1da7-122">PartitionKey en RowKey</span><span class="sxs-lookup"><span data-stu-id="c1da7-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="c1da7-123">U moet opgeven dat zowel een **PartitionKey** en een **RowKey** eigenschap voor elke entiteit.</span><span class="sxs-lookup"><span data-stu-id="c1da7-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="c1da7-124">Dit als samen de unieke id's van uw entiteiten, zijn ze de primaire sleutel van een entiteit vormen.</span><span class="sxs-lookup"><span data-stu-id="c1da7-124">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="c1da7-125">U kunt een query met deze waarden veel sneller dan u kunt een andere entiteitseigenschappen query omdat alleen deze eigenschappen zijn geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="c1da7-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="c1da7-126">De tabel-service wordt gebruikt **PartitionKey** voor de distributie op intelligente wijze tabelentiteiten over opslagknooppunten.</span><span class="sxs-lookup"><span data-stu-id="c1da7-126">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="c1da7-127">Entiteiten met dezelfde **PartitionKey** op hetzelfde knooppunt worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c1da7-127">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="c1da7-128">**RowKey** is de unieke ID van de entiteit in de partitie hoort bij.</span><span class="sxs-lookup"><span data-stu-id="c1da7-128">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="c1da7-129">Bijwerken van een entiteit</span><span class="sxs-lookup"><span data-stu-id="c1da7-129">Update an entity</span></span>

<span data-ttu-id="c1da7-130">Aanroepen voor het bijwerken van alle waarden van de eigenschap van een entiteit, de [update_entity] [ py_update_entity] methode.</span><span class="sxs-lookup"><span data-stu-id="c1da7-130">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="c1da7-131">In dit voorbeeld ziet u hoe u een bestaande entiteit vervangen door een bijgewerkte versie:</span><span class="sxs-lookup"><span data-stu-id="c1da7-131">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="c1da7-132">Als de entiteit die wordt bijgewerkt, niet al bestaat, wordt de update-bewerking mislukt.</span><span class="sxs-lookup"><span data-stu-id="c1da7-132">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="c1da7-133">Als u wilt opslaan van een entiteit of deze of niet bestaat, gebruiken [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="c1da7-133">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="c1da7-134">In het volgende voorbeeld wordt de eerste aanroep van de bestaande entiteit vervangen.</span><span class="sxs-lookup"><span data-stu-id="c1da7-134">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="c1da7-135">De tweede aanroep wordt een nieuwe entiteit worden ingevoegd omdat er geen entiteit met de opgegeven PartitionKey en RowKey bestaat in de tabel.</span><span class="sxs-lookup"><span data-stu-id="c1da7-135">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="c1da7-136">De [update_entity] [ py_update_entity] methode vervangt alle eigenschappen en waarden van een bestaande entiteit, u ook gebruiken kunt om eigenschappen te verwijderen uit een bestaande entiteit.</span><span class="sxs-lookup"><span data-stu-id="c1da7-136">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="c1da7-137">U kunt de [merge_entity] [ py_merge_entity] methode voor het bijwerken van een bestaande entiteit met nieuwe of gewijzigde eigenschapswaarden zonder de entiteit volledig te vervangen.</span><span class="sxs-lookup"><span data-stu-id="c1da7-137">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="c1da7-138">Meerdere entiteiten wijzigen</span><span class="sxs-lookup"><span data-stu-id="c1da7-138">Modify multiple entities</span></span>

<span data-ttu-id="c1da7-139">U kunt meerdere bewerkingen samen in een batch te verzenden zodat de atomic verwerking van een aanvraag door de tabel-service.</span><span class="sxs-lookup"><span data-stu-id="c1da7-139">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="c1da7-140">Gebruik eerst de [TableBatch] [ py_TableBatch] klasse meerdere bewerkingen toevoegen aan één batch.</span><span class="sxs-lookup"><span data-stu-id="c1da7-140">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="c1da7-141">Daarna roept [TableService][py_TableService].[ commit_batch] [ py_commit_batch] verzenden van de bewerkingen in een atomic-bewerking.</span><span class="sxs-lookup"><span data-stu-id="c1da7-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="c1da7-142">Alle entiteiten in batch worden gewijzigd, moeten zich in dezelfde partitie.</span><span class="sxs-lookup"><span data-stu-id="c1da7-142">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="c1da7-143">In dit voorbeeld voegt twee entiteiten samen in een batch:</span><span class="sxs-lookup"><span data-stu-id="c1da7-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="c1da7-144">Batches kunnen ook worden gebruikt met de syntaxis van de manager context:</span><span class="sxs-lookup"><span data-stu-id="c1da7-144">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="c1da7-145">Query voor een entiteit</span><span class="sxs-lookup"><span data-stu-id="c1da7-145">Query for an entity</span></span>

<span data-ttu-id="c1da7-146">Om te vragen voor een entiteit in een tabel, de PartitionKey en RowKey naar doorgeven de [TableService][py_TableService].[ get_entity] [ py_get_entity] methode.</span><span class="sxs-lookup"><span data-stu-id="c1da7-146">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="c1da7-147">Query uitvoeren op een verzameling entiteiten</span><span class="sxs-lookup"><span data-stu-id="c1da7-147">Query a set of entities</span></span>

<span data-ttu-id="c1da7-148">U kunt een query voor een aantal entiteiten door het opgeven van een filtertekenreeks in met de **filter** parameter.</span><span class="sxs-lookup"><span data-stu-id="c1da7-148">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="c1da7-149">In dit voorbeeld worden alle taken in Haarlem gevonden door een filter toepassen op PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="c1da7-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="c1da7-150">Een query uitvoeren op een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="c1da7-150">Query a subset of entity properties</span></span>

<span data-ttu-id="c1da7-151">U kunt ook beperken welke eigenschappen voor elke entiteit in een query zijn geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="c1da7-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="c1da7-152">Deze methode, aangeroepen *projectie*, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral voor grote entiteiten of resultatensets.</span><span class="sxs-lookup"><span data-stu-id="c1da7-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="c1da7-153">Gebruik de **Selecteer** parameter en de namen van de eigenschappen die u wilt dat wordt geretourneerd naar de client op te geven.</span><span class="sxs-lookup"><span data-stu-id="c1da7-153">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="c1da7-154">De query in de volgende code retourneert alleen de beschrijvingen van entiteiten in de tabel.</span><span class="sxs-lookup"><span data-stu-id="c1da7-154">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="c1da7-155">Het volgende fragment werkt alleen op basis van de Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="c1da7-155">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="c1da7-156">Dit wordt niet ondersteund door de opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="c1da7-156">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="c1da7-157">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="c1da7-157">Delete an entity</span></span>

<span data-ttu-id="c1da7-158">Een entiteit verwijderen door de PartitionKey en RowKey naar de [delete_entity] [ py_delete_entity] methode.</span><span class="sxs-lookup"><span data-stu-id="c1da7-158">Delete an entity by passing its PartitionKey and RowKey to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="c1da7-159">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="c1da7-159">Delete a table</span></span>

<span data-ttu-id="c1da7-160">Als u een tabel of een van de entiteiten in het niet meer nodig hebt, belt u het [delete_table] [ py_delete_table] methode voor de tabel permanent verwijderen uit Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c1da7-160">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="c1da7-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1da7-161">Next steps</span></span>

* [<span data-ttu-id="c1da7-162">Azure-opslag-SDK voor Python-API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="c1da7-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="c1da7-163">Azure-opslag-SDK voor Python</span><span class="sxs-lookup"><span data-stu-id="c1da7-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="c1da7-164">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="c1da7-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="c1da7-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): een gratis, platformoverschrijdende-toepassing voor visueel werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="c1da7-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch
