---
title: aaaHow toouse Azure Blob storage (objectopslag) met Python | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 8f9ca93e52b030384e28a739d2f1c6b610be094a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a>Hoe toouse Azure Blob storage met Python
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Overzicht
Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat. In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen. BLOB-opslag is ook bedoeld tooas vorm van objectopslag.

In dit artikel wordt uitgelegd hoe u tooperform algemene scenario's met behulp van Blob-opslag. Hallo-voorbeelden zijn geschreven in Python en gebruiken van Hallo [Microsoft Azure-opslag-SDK voor Python]. Hallo scenario's worden behandeld bevatten uploaden, aanbieding, downloaden en verwijderen van blobs.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a>Een container maken
Op basis van Hallo type blob gewenst toouse, maak een **BlockBlobService**, **AppendBlobService**, of **PageBlobService** object. Hallo volgende code wordt een **BlockBlobService** object. De volgende Hallo bij Hallo bovenkant van een Python-bestand waarin u tooprogrammatically access Azure blok-Blob-opslag wilt toevoegen.

```python
from azure.storage.blob import BlockBlobService
```

Hallo volgende code maakt een **BlockBlobService** -object op met de Hallo naam en opslagaccountsleutel.  'Myaccount' en 'mykey' vervangen door uw accountnaam en de sleutel.

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

In de Hallo volgende codevoorbeeld, kunt u een **BlockBlobService** toocreate Hallo objectcontainer als deze niet bestaat.

```python
block_blob_service.create_container('mycontainer')
```

Hallo nieuwe container is standaard privé, dus u uw toegangssleutel voor opslag opgeven moet (zoals u eerder hebt gedaan) toodownload blobs uit deze container. U kunt desgewenst toomake Hallo blobs in hello container beschikbaar tooeveryone Hallo container maken en Hallo openbare toegangsniveau met behulp van de volgende code Hallo doorgeven.

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

U kunt ook een container wijzigen nadat u hebt gemaakt met behulp van de volgende code Hallo.

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

Na deze wijziging kan iedereen op Internet Hallo blobs in een openbare container zien, maar u kunt alleen wijzigen of verwijderen.

## <a name="upload-a-blob-into-a-container"></a>Een blob uploaden naar een container
toocreate een blok-blob en het van uploadgegevens, gebruikt u Hallo **maken\_blob\_van\_pad**, **maken\_blob\_van\_stroom**, **maken\_blob\_van\_bytes** of **maken\_blob\_van\_tekst** methoden. Op hoog niveau van de methoden die Hallo nodig verdeling in segmenten uitvoeren wanneer Hallo Hallo gegevens groter zijn dan 64 MB zijn.

**Maak\_blob\_van\_pad** uploads Hallo inhoud van een bestand uit het opgegeven pad Hallo, en **maken\_blob\_van\_stroom** uploads Hallo inhoud uit een al geopend bestandsstroom. **maken\_blob\_van\_bytes** een bytematrix, uploadt en **maken\_blob\_van\_tekst** uploadt Hallo opgegeven tekstwaarde met Hallo opgegeven codering (standaardwaarden tooUTF-8).

Hallo volgende voorbeeld wordt geüpload Hallo inhoud Hallo **sunset.png** -bestand in Hallo **myblob** blob.

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a>Lijst Hallo blobs in een container
toolist hello blobs in een container gebruiken Hallo **lijst\_blobs** methode. Deze methode retourneert een generator. Hallo volgende code levert Hallo **naam** van elke blob in een container toohello-console.

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a>Blobs downloaden
toodownload gegevens van een blob gebruiken **ophalen\_blob\_naar\_pad**, **ophalen\_blob\_naar\_stroom**, **ophalen\_blob\_naar\_bytes**, of **ophalen\_blob\_naar\_tekst**. Op hoog niveau van de methoden die Hallo nodig verdeling in segmenten uitvoeren wanneer Hallo Hallo gegevens groter zijn dan 64 MB zijn.

Hallo volgende voorbeeld worden **ophalen\_blob\_naar\_pad** toodownload Hallo inhoud Hallo **myblob** blob en sla het toohello **out sunset.png** bestand.

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a>Een blob verwijderen
Tenslotte toodelete een blob roept **delete_blob**.

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a>Schrijven tooan toevoeg-blob
Een toevoeg-blob is geoptimaliseerd voor toevoegbewerkingen, zoals logboekregistratie. Zoals een blok-blob bestaat een toevoeg-blob uit blokken, maar wanneer u een nieuw blok tooan toevoeg-blob toevoegt, wordt het altijd toegevoegde toohello einde van Hallo blob. U kunt een bestaand blok in een toevoeg-blob niet bijwerken of verwijderen. Hallo blok-id's voor een toevoeg-blob worden niet weergegeven zoals ze zijn voor een blok-blob.

Elk blok in een toevoeg-blob kan een andere grootte, up tooa maximaal 4 MB en een toevoeg-blob kan maximaal 50.000 blokken bevatten. Hallo maximale grootte van een toevoeg-blob is daarom iets meer dan 195 GB (4 MB X 50.000 blokken).

Hallo in het volgende voorbeeld maakt u een nieuwe toevoeg-blob en voegt sommige gegevens tooit, een bewerking voor eenvoudige logboekregistratie simuleren.

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Blob storage hebt geleerd, volgt u deze koppelingen toolearn meer.

* [Python Developer Center](https://azure.microsoft.com/develop/python/)
* [REST-API voor Azure Storage-services](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog van het Azure Storage-team]
* [Microsoft Azure-opslag-SDK voor Python]

[Blog van het Azure Storage-team]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure-opslag-SDK voor Python]: https://github.com/Azure/azure-storage-python
