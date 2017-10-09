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
# <a name="how-toouse-table-storage-in-python"></a>Hoe toouse Table storage in Python

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

Deze handleiding wordt getoond hoe tooperform veelvoorkomende Azure Table storage scenario's in met behulp van Python Hallo [Microsoft Azure-opslag-SDK voor Python](https://github.com/Azure/azure-storage-python). Hallo scenario's worden behandeld bevatten maken en verwijderen van een tabel en het invoegen en het opvragen van entiteiten.

Tijdens het werken met Hallo scenario's in deze zelfstudie kunt u desgewenst toorefer toohello [Azure-opslag-SDK voor Python-API-referentiemateriaal](https://azure-storage.readthedocs.io/en/latest/index.html).

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a>Hello Azure-opslag-SDK voor Python installeren

Als u een opslagaccount hebt gemaakt, de volgende stap is het tooinstall hello [Microsoft Azure-opslag-SDK voor Python](https://github.com/Azure/azure-storage-python). Voor meer informatie over het installeren van hello SDK, Raadpleeg toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) bestand in Hallo opslag-SDK voor Python-opslagplaats op GitHub.

## <a name="create-a-table"></a>Een tabel maken

toowork Hello Azure Table-service in Python, moet u Hallo importeren [TableService] [ py_TableService] module. Omdat u met tabelentiteiten werken gaat, moet u ook Hallo [entiteit] [ py_Entity] klasse. Voeg deze code aan de bovenkant Hallo uw Python-bestand tooimport beide:

```python
from azure.storage.table import TableService, Entity
```

Maak een [TableService] [ py_TableService] -object doorgeven in een naam en sleutel van uw opslagaccount. Vervang `myaccount` en `mykey` met uw accountnaam en -sleutel en aanroep [create_table] [ py_create_table] toocreate Hallo tabel in Azure Storage.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a>Een entiteit tooa tabel toevoegen

tooadd een entiteit eerst maakt u een object dat uw entiteit, klikt u vervolgens op te geven Hallo object toohello vertegenwoordigt [TableService][py_TableService].[ insert_entity] [ py_insert_entity] methode. Hallo entiteitsobject mag een woordenboek of een object van type [entiteit][py_Entity], en de namen en waarden van uw entiteit definieert. Elke entiteit moet bevatten Hallo vereist [PartitionKey en RowKey](#partitionkey-and-rowkey) eigenschappen in toevoeging tooany andere eigenschappen u definieert voor Hallo entiteit.

In dit voorbeeld maakt u een dictionary-object dat een entiteit vertegenwoordigt stuurt vervolgens deze toohello [insert_entity] [ py_insert_entity] methode tooadd deze toohello tabel:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

In dit voorbeeld wordt een [entiteit] [ py_Entity] object en geeft vervolgens het toohello [insert_entity] [ py_insert_entity] methode tooadd deze toohello tabel:

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey en RowKey

U moet opgeven dat zowel een **PartitionKey** en een **RowKey** eigenschap voor elke entiteit. Dit als samen Hallo unieke id's van uw entiteiten, zijn ze Hallo primaire sleutel van een entiteit vormen. U kunt een query met deze waarden veel sneller dan u kunt een andere entiteitseigenschappen query omdat alleen deze eigenschappen zijn geïndexeerd.

Tabel-service gebruikt Hallo **PartitionKey** toointelligently tabelentiteiten verdelen over de configuratie voor opslagknooppunten. Entiteiten met dezelfde Hallo **PartitionKey** zijn opgeslagen op Hallo hetzelfde knooppunt. **RowKey** is de unieke ID Hallo van Hallo entiteit binnen deze tot behoort Hallo-partitie.

## <a name="update-an-entity"></a>Bijwerken van een entiteit

alle tooupdate aanroepen van een entiteit eigenschapswaarden, Hallo [update_entity] [ py_update_entity] methode. Dit voorbeeld ziet u hoe tooreplace een bestaande entiteit met een bijgewerkte versie:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

Als Hallo-entiteit die wordt bijgewerkt, niet al bestaat, mislukken Hallo updatebewerking. Als u toostore een entiteit wilt of het of niet bestaat, gebruikt [insert_or_replace_entity][py_insert_or_replace_entity]. In Hallo voorbeeld te volgen, wordt de eerste aanroep Hallo Hallo bestaande entiteit vervangen. Hallo tweede aanroep wordt een nieuwe entiteit invoegen, omdat er geen entiteit Hello opgegeven PartitionKey en RowKey bestaat in tabel Hallo.

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> Hallo [update_entity] [ py_update_entity] methode vervangt alle eigenschappen en waarden van een bestaande entiteit, u ook kunt tooremove eigenschappen uit een bestaande entiteit gebruiken. U kunt Hallo [merge_entity] [ py_merge_entity] methode tooupdate een bestaande entiteit met nieuwe of gewijzigde eigenschapswaarden zonder Hallo entiteit volledig te vervangen.

## <a name="modify-multiple-entities"></a>Meerdere entiteiten wijzigen

tooensure Hallo atomic verwerking van een aanvraag door Hallo tabel-service, kunt u meerdere bewerkingen samen in een batch indienen. Gebruik eerst Hallo [TableBatch] [ py_TableBatch] klasse tooadd meerdere bewerkingen tooa één batch. Daarna roept [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit Hallo bewerkingen in een atomic-bewerking. Alle entiteiten toobe gewijzigd in een batch moet Hallo dezelfde partitie.

In dit voorbeeld voegt twee entiteiten samen in een batch:

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

Batches kunnen ook worden gebruikt met Hallo context manager syntaxis:

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>Query voor een entiteit

tooquery voor een entiteit in een tabel, geeft de PartitionKey en RowKey toohello [TableService][py_TableService].[ get_entity] [ py_get_entity] methode.

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>Query uitvoeren op een verzameling entiteiten

U kunt een query voor een aantal entiteiten door het opgeven van een filtertekenreeks Hello **filter** parameter. In dit voorbeeld worden alle taken in Haarlem gevonden door een filter toepassen op PartitionKey:

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>Een query uitvoeren op een subset van entiteitseigenschappen

U kunt ook beperken welke eigenschappen voor elke entiteit in een query zijn geretourneerd. Deze methode, aangeroepen *projectie*, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral voor grote entiteiten of resultatensets. Gebruik Hallo **Selecteer** parameter en pass Hallo-namen van Hallo-eigenschappen die u wilt toohello client geretourneerd.

Hallo-query in de volgende code Hallo retourneert alleen Hallo beschrijvingen van entiteiten in Hallo tabel.

> [!NOTE]
> Hallo codefragment werkt alleen voor hello Azure Storage te volgen. Dit wordt niet ondersteund door de opslagemulator Hallo.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>Een entiteit verwijderen

Een entiteit verwijderen door de PartitionKey en RowKey toohello [delete_entity] [ py_delete_entity] methode.

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>Een tabel verwijderen

Als u een tabel of Hallo entiteiten binnen deze niet langer nodig hebt, belt Hallo [delete_table] [ py_delete_table] methode toopermanently Hallo tabel verwijderen uit Azure Storage.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>Volgende stappen

* [Azure-opslag-SDK voor Python-API-referentiemateriaal](https://azure-storage.readthedocs.io/en/latest/index.html)
* [Azure-opslag-SDK voor Python](https://github.com/Azure/azure-storage-python)
* [Python Developer Center](https://azure.microsoft.com/develop/python/)
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): een gratis, platformoverschrijdende-toepassing voor visueel werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux.

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
