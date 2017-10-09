---
title: aaaHow toouse Azure Table storage met behulp van Python | Microsoft Docs
description: Gestructureerde gegevens opslaan in Hallo cloud met Azure Table storage, een NoSQL-gegevensarchief.
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: marsma
ms.openlocfilehash: fd0e1b05cc12618f348eaf2d85d0dce5ac32702a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a><span data-ttu-id="fac5a-103">Hoe toouse Table storage in Python</span><span class="sxs-lookup"><span data-stu-id="fac5a-103">How toouse Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="fac5a-104">Deze handleiding wordt getoond hoe tooperform veelvoorkomende Azure Table storage scenario's in met behulp van Python Hallo [Microsoft Azure-opslag-SDK voor Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="fac5a-104">This guide shows you how tooperform common Azure Table storage scenarios in Python using hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="fac5a-105">Hallo scenario's worden behandeld bevatten maken en verwijderen van een tabel en het invoegen en het opvragen van entiteiten.</span><span class="sxs-lookup"><span data-stu-id="fac5a-105">hello scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="fac5a-106">Tijdens het werken met Hallo scenario's in deze zelfstudie kunt u desgewenst toorefer toohello [Azure-opslag-SDK voor Python-API-referentiemateriaal](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="fac5a-106">While working through hello scenarios in this tutorial, you may wish toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a><span data-ttu-id="fac5a-107">Hello Azure-opslag-SDK voor Python installeren</span><span class="sxs-lookup"><span data-stu-id="fac5a-107">Install hello Azure Storage SDK for Python</span></span>

<span data-ttu-id="fac5a-108">Als u een opslagaccount hebt gemaakt, de volgende stap is het tooinstall hello [Microsoft Azure-opslag-SDK voor Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="fac5a-108">Once you've created a storage account, your next step is tooinstall hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="fac5a-109">Voor meer informatie over het installeren van hello SDK, Raadpleeg toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) bestand in Hallo opslag-SDK voor Python-opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="fac5a-109">For details on installing hello SDK, refer toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="fac5a-110">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="fac5a-110">Create a table</span></span>

<span data-ttu-id="fac5a-111">toowork Hello Azure Table-service in Python, moet u Hallo importeren [TableService] [ py_TableService] module.</span><span class="sxs-lookup"><span data-stu-id="fac5a-111">toowork with hello Azure Table service in Python, you must import hello [TableService][py_TableService] module.</span></span> <span data-ttu-id="fac5a-112">Omdat u met tabelentiteiten werken gaat, moet u ook Hallo [entiteit] [ py_Entity] klasse.</span><span class="sxs-lookup"><span data-stu-id="fac5a-112">Since you'll be working with Table entities, you also need hello [Entity][py_Entity] class.</span></span> <span data-ttu-id="fac5a-113">Voeg deze code aan de bovenkant Hallo uw Python-bestand tooimport beide:</span><span class="sxs-lookup"><span data-stu-id="fac5a-113">Add this code near hello top your Python file tooimport both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="fac5a-114">Maak een [TableService] [ py_TableService] -object doorgeven in een naam en sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="fac5a-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="fac5a-115">Vervang `myaccount` en `mykey` met uw accountnaam en -sleutel en aanroep [create_table] [ py_create_table] toocreate Hallo tabel in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fac5a-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] toocreate hello table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="fac5a-116">Een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="fac5a-116">Add an entity tooa table</span></span>

<span data-ttu-id="fac5a-117">tooadd een entiteit eerst maakt u een object dat uw entiteit, klikt u vervolgens op te geven Hallo object toohello vertegenwoordigt [TableService][py_TableService].[ insert_entity] [ py_insert_entity] methode.</span><span class="sxs-lookup"><span data-stu-id="fac5a-117">tooadd an entity, you first create an object that represents your entity, then pass hello object toohello [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="fac5a-118">Hallo entiteitsobject mag een woordenboek of een object van type [entiteit][py_Entity], en de namen en waarden van uw entiteit definieert.</span><span class="sxs-lookup"><span data-stu-id="fac5a-118">hello entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="fac5a-119">Elke entiteit moet bevatten Hallo vereist [PartitionKey en RowKey](#partitionkey-and-rowkey) eigenschappen in toevoeging tooany andere eigenschappen u definieert voor Hallo entiteit.</span><span class="sxs-lookup"><span data-stu-id="fac5a-119">Every entity must include hello required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition tooany other properties you define for hello entity.</span></span>

<span data-ttu-id="fac5a-120">In dit voorbeeld maakt u een dictionary-object dat een entiteit vertegenwoordigt stuurt vervolgens deze toohello [insert_entity] [ py_insert_entity] methode tooadd deze toohello tabel:</span><span class="sxs-lookup"><span data-stu-id="fac5a-120">This example creates a dictionary object representing an entity, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="fac5a-121">In dit voorbeeld wordt een [entiteit] [ py_Entity] object en geeft vervolgens het toohello [insert_entity] [ py_insert_entity] methode tooadd deze toohello tabel:</span><span class="sxs-lookup"><span data-stu-id="fac5a-121">This example creates an [Entity][py_Entity] object, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="fac5a-122">PartitionKey en RowKey</span><span class="sxs-lookup"><span data-stu-id="fac5a-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="fac5a-123">U moet opgeven dat zowel een **PartitionKey** en een **RowKey** eigenschap voor elke entiteit.</span><span class="sxs-lookup"><span data-stu-id="fac5a-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="fac5a-124">Dit als samen Hallo unieke id's van uw entiteiten, zijn ze Hallo primaire sleutel van een entiteit vormen.</span><span class="sxs-lookup"><span data-stu-id="fac5a-124">These are hello unique identifiers of your entities, as together they form hello primary key of an entity.</span></span> <span data-ttu-id="fac5a-125">U kunt een query met deze waarden veel sneller dan u kunt een andere entiteitseigenschappen query omdat alleen deze eigenschappen zijn geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="fac5a-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="fac5a-126">Tabel-service gebruikt Hallo **PartitionKey** toointelligently tabelentiteiten verdelen over de configuratie voor opslagknooppunten.</span><span class="sxs-lookup"><span data-stu-id="fac5a-126">hello Table service uses **PartitionKey** toointelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="fac5a-127">Entiteiten met dezelfde Hallo **PartitionKey** zijn opgeslagen op Hallo hetzelfde knooppunt.</span><span class="sxs-lookup"><span data-stu-id="fac5a-127">Entities that have hello same  **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="fac5a-128">**RowKey** is de unieke ID Hallo van Hallo entiteit binnen deze tot behoort Hallo-partitie.</span><span class="sxs-lookup"><span data-stu-id="fac5a-128">**RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="fac5a-129">Bijwerken van een entiteit</span><span class="sxs-lookup"><span data-stu-id="fac5a-129">Update an entity</span></span>

<span data-ttu-id="fac5a-130">alle tooupdate aanroepen van een entiteit eigenschapswaarden, Hallo [update_entity] [ py_update_entity] methode.</span><span class="sxs-lookup"><span data-stu-id="fac5a-130">tooupdate all of an entity's property values, call hello [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="fac5a-131">Dit voorbeeld ziet u hoe tooreplace een bestaande entiteit met een bijgewerkte versie:</span><span class="sxs-lookup"><span data-stu-id="fac5a-131">This example shows how tooreplace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="fac5a-132">Als Hallo-entiteit die wordt bijgewerkt, niet al bestaat, mislukken Hallo updatebewerking.</span><span class="sxs-lookup"><span data-stu-id="fac5a-132">If hello entity that is being updated doesn't already exist, then hello update operation will fail.</span></span> <span data-ttu-id="fac5a-133">Als u toostore een entiteit wilt of het of niet bestaat, gebruikt [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="fac5a-133">If you want toostore an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="fac5a-134">In Hallo voorbeeld te volgen, wordt de eerste aanroep Hallo Hallo bestaande entiteit vervangen.</span><span class="sxs-lookup"><span data-stu-id="fac5a-134">In hello following example, hello first call will replace hello existing entity.</span></span> <span data-ttu-id="fac5a-135">Hallo tweede aanroep wordt een nieuwe entiteit invoegen, omdat er geen entiteit Hello opgegeven PartitionKey en RowKey bestaat in tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="fac5a-135">hello second call will insert a new entity, since no entity with hello specified PartitionKey and RowKey exists in hello table.</span></span>

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="fac5a-136">Hallo [update_entity] [ py_update_entity] methode vervangt alle eigenschappen en waarden van een bestaande entiteit, u ook kunt tooremove eigenschappen uit een bestaande entiteit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fac5a-136">hello [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use tooremove properties from an existing entity.</span></span> <span data-ttu-id="fac5a-137">U kunt Hallo [merge_entity] [ py_merge_entity] methode tooupdate een bestaande entiteit met nieuwe of gewijzigde eigenschapswaarden zonder Hallo entiteit volledig te vervangen.</span><span class="sxs-lookup"><span data-stu-id="fac5a-137">You can use hello [merge_entity][py_merge_entity] method tooupdate an existing entity with new or modified property values without completely replacing hello entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="fac5a-138">Meerdere entiteiten wijzigen</span><span class="sxs-lookup"><span data-stu-id="fac5a-138">Modify multiple entities</span></span>

<span data-ttu-id="fac5a-139">tooensure Hallo atomic verwerking van een aanvraag door Hallo tabel-service, kunt u meerdere bewerkingen samen in een batch indienen.</span><span class="sxs-lookup"><span data-stu-id="fac5a-139">tooensure hello atomic processing of a request by hello Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="fac5a-140">Gebruik eerst Hallo [TableBatch] [ py_TableBatch] klasse tooadd meerdere bewerkingen tooa één batch.</span><span class="sxs-lookup"><span data-stu-id="fac5a-140">First, use hello [TableBatch][py_TableBatch] class tooadd multiple operations tooa single batch.</span></span> <span data-ttu-id="fac5a-141">Daarna roept [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit Hallo bewerkingen in een atomic-bewerking.</span><span class="sxs-lookup"><span data-stu-id="fac5a-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] toosubmit hello operations in an atomic operation.</span></span> <span data-ttu-id="fac5a-142">Alle entiteiten toobe gewijzigd in een batch moet Hallo dezelfde partitie.</span><span class="sxs-lookup"><span data-stu-id="fac5a-142">All entities toobe modified in batch must be in hello same partition.</span></span>

<span data-ttu-id="fac5a-143">In dit voorbeeld voegt twee entiteiten samen in een batch:</span><span class="sxs-lookup"><span data-stu-id="fac5a-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="fac5a-144">Batches kunnen ook worden gebruikt met Hallo context manager syntaxis:</span><span class="sxs-lookup"><span data-stu-id="fac5a-144">Batches can also be used with hello context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="fac5a-145">Query voor een entiteit</span><span class="sxs-lookup"><span data-stu-id="fac5a-145">Query for an entity</span></span>

<span data-ttu-id="fac5a-146">tooquery voor een entiteit in een tabel, geeft de PartitionKey en RowKey toohello [TableService][py_TableService].[ get_entity] [ py_get_entity] methode.</span><span class="sxs-lookup"><span data-stu-id="fac5a-146">tooquery for an entity in a table, pass its PartitionKey and RowKey toohello [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="fac5a-147">Query uitvoeren op een verzameling entiteiten</span><span class="sxs-lookup"><span data-stu-id="fac5a-147">Query a set of entities</span></span>

<span data-ttu-id="fac5a-148">U kunt een query voor een aantal entiteiten door het opgeven van een filtertekenreeks Hello **filter** parameter.</span><span class="sxs-lookup"><span data-stu-id="fac5a-148">You can query for a set of entities by supplying a filter string with hello **filter** parameter.</span></span> <span data-ttu-id="fac5a-149">In dit voorbeeld worden alle taken in Haarlem gevonden door een filter toepassen op PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="fac5a-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="fac5a-150">Een query uitvoeren op een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="fac5a-150">Query a subset of entity properties</span></span>

<span data-ttu-id="fac5a-151">U kunt ook beperken welke eigenschappen voor elke entiteit in een query zijn geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="fac5a-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="fac5a-152">Deze methode, aangeroepen *projectie*, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral voor grote entiteiten of resultatensets.</span><span class="sxs-lookup"><span data-stu-id="fac5a-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="fac5a-153">Gebruik Hallo **Selecteer** parameter en pass Hallo-namen van Hallo-eigenschappen die u wilt toohello client geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="fac5a-153">Use hello **select** parameter and pass hello names of hello properties you want returned toohello client.</span></span>

<span data-ttu-id="fac5a-154">Hallo-query in de volgende code Hallo retourneert alleen Hallo beschrijvingen van entiteiten in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="fac5a-154">hello query in hello following code returns only hello descriptions of entities in hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="fac5a-155">Hallo codefragment werkt alleen voor hello Azure Storage te volgen.</span><span class="sxs-lookup"><span data-stu-id="fac5a-155">hello following snippet works only against hello Azure Storage.</span></span> <span data-ttu-id="fac5a-156">Dit wordt niet ondersteund door de opslagemulator Hallo.</span><span class="sxs-lookup"><span data-stu-id="fac5a-156">It is not supported by hello storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="fac5a-157">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="fac5a-157">Delete an entity</span></span>

<span data-ttu-id="fac5a-158">Een entiteit verwijderen door de PartitionKey en RowKey toohello [delete_entity] [ py_delete_entity] methode.</span><span class="sxs-lookup"><span data-stu-id="fac5a-158">Delete an entity by passing its PartitionKey and RowKey toohello [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="fac5a-159">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="fac5a-159">Delete a table</span></span>

<span data-ttu-id="fac5a-160">Als u een tabel of Hallo entiteiten binnen deze niet langer nodig hebt, belt Hallo [delete_table] [ py_delete_table] methode toopermanently Hallo tabel verwijderen uit Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fac5a-160">If you no longer need a table or any of hello entities within it, call hello [delete_table][py_delete_table] method toopermanently delete hello table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="fac5a-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fac5a-161">Next steps</span></span>

* [<span data-ttu-id="fac5a-162">Azure-opslag-SDK voor Python-API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="fac5a-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="fac5a-163">Azure-opslag-SDK voor Python</span><span class="sxs-lookup"><span data-stu-id="fac5a-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="fac5a-164">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="fac5a-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="fac5a-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): een gratis, platformoverschrijdende-toepassing voor visueel werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="fac5a-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

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
