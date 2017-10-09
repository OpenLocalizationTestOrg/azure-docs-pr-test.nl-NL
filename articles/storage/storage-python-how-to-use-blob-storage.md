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
ms.openlocfilehash: 6efc61aa89e6d2544b7a18c80ce3546640f90462
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a><span data-ttu-id="22993-103">Hoe toouse Azure Blob storage met Python</span><span class="sxs-lookup"><span data-stu-id="22993-103">How toouse Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="22993-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="22993-104">Overview</span></span>
<span data-ttu-id="22993-105">Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat.</span><span class="sxs-lookup"><span data-stu-id="22993-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="22993-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="22993-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="22993-107">BLOB-opslag is ook bedoeld tooas vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="22993-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="22993-108">In dit artikel wordt uitgelegd hoe u tooperform algemene scenario's met behulp van Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="22993-108">This article will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="22993-109">Hallo-voorbeelden zijn geschreven in Python en gebruiken van Hallo [Microsoft Azure-opslag-SDK voor Python].</span><span class="sxs-lookup"><span data-stu-id="22993-109">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="22993-110">Hallo scenario's worden behandeld bevatten uploaden, aanbieding, downloaden en verwijderen van blobs.</span><span class="sxs-lookup"><span data-stu-id="22993-110">hello scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="22993-111">Een container maken</span><span class="sxs-lookup"><span data-stu-id="22993-111">Create a container</span></span>
<span data-ttu-id="22993-112">Op basis van Hallo type blob gewenst toouse, maak een **BlockBlobService**, **AppendBlobService**, of **PageBlobService** object.</span><span class="sxs-lookup"><span data-stu-id="22993-112">Based on hello type of blob you would like toouse, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="22993-113">Hallo volgende code wordt een **BlockBlobService** object.</span><span class="sxs-lookup"><span data-stu-id="22993-113">hello following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="22993-114">De volgende Hallo bij Hallo bovenkant van een Python-bestand waarin u tooprogrammatically access Azure blok-Blob-opslag wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="22993-114">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="22993-115">Hallo volgende code maakt een **BlockBlobService** -object op met de Hallo naam en opslagaccountsleutel.</span><span class="sxs-lookup"><span data-stu-id="22993-115">hello following code creates a **BlockBlobService** object using hello storage account name and account key.</span></span>  <span data-ttu-id="22993-116">'Myaccount' en 'mykey' vervangen door uw accountnaam en de sleutel.</span><span class="sxs-lookup"><span data-stu-id="22993-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="22993-117">In de Hallo volgende codevoorbeeld, kunt u een **BlockBlobService** toocreate Hallo objectcontainer als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="22993-117">In hello following code example, you can use a **BlockBlobService** object toocreate hello container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="22993-118">Hallo nieuwe container is standaard privé, dus u uw toegangssleutel voor opslag opgeven moet (zoals u eerder hebt gedaan) toodownload blobs uit deze container.</span><span class="sxs-lookup"><span data-stu-id="22993-118">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span> <span data-ttu-id="22993-119">U kunt desgewenst toomake Hallo blobs in hello container beschikbaar tooeveryone Hallo container maken en Hallo openbare toegangsniveau met behulp van de volgende code Hallo doorgeven.</span><span class="sxs-lookup"><span data-stu-id="22993-119">If you want toomake hello blobs within hello container available tooeveryone, you can create hello container and pass hello public access level using hello following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="22993-120">U kunt ook een container wijzigen nadat u hebt gemaakt met behulp van de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="22993-120">Alternatively, you can modify a container after you have created it using hello following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="22993-121">Na deze wijziging kan iedereen op Internet Hallo blobs in een openbare container zien, maar u kunt alleen wijzigen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="22993-121">After this change, anyone on hello Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="22993-122">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="22993-122">Upload a blob into a container</span></span>
<span data-ttu-id="22993-123">toocreate een blok-blob en het van uploadgegevens, gebruikt u Hallo **maken\_blob\_van\_pad**, **maken\_blob\_van\_stroom**, **maken\_blob\_van\_bytes** of **maken\_blob\_van\_tekst** methoden.</span><span class="sxs-lookup"><span data-stu-id="22993-123">toocreate a block blob and upload data, use hello **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="22993-124">Op hoog niveau van de methoden die Hallo nodig verdeling in segmenten uitvoeren wanneer Hallo Hallo gegevens groter zijn dan 64 MB zijn.</span><span class="sxs-lookup"><span data-stu-id="22993-124">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="22993-125">**Maak\_blob\_van\_pad** uploads Hallo inhoud van een bestand uit het opgegeven pad Hallo, en **maken\_blob\_van\_stroom** uploads Hallo inhoud uit een al geopend bestandsstroom.</span><span class="sxs-lookup"><span data-stu-id="22993-125">**create\_blob\_from\_path** uploads hello contents of a file from hello specified path, and **create\_blob\_from\_stream** uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="22993-126">**maken\_blob\_van\_bytes** een bytematrix, uploadt en **maken\_blob\_van\_tekst** uploadt Hallo opgegeven tekstwaarde met Hallo opgegeven codering (standaardwaarden tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="22993-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="22993-127">Hallo volgende voorbeeld wordt geüpload Hallo inhoud Hallo **sunset.png** -bestand in Hallo **myblob** blob.</span><span class="sxs-lookup"><span data-stu-id="22993-127">hello following example uploads hello contents of hello **sunset.png** file into hello **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="22993-128">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="22993-128">List hello blobs in a container</span></span>
<span data-ttu-id="22993-129">toolist hello blobs in een container gebruiken Hallo **lijst\_blobs** methode.</span><span class="sxs-lookup"><span data-stu-id="22993-129">toolist hello blobs in a container, use hello **list\_blobs** method.</span></span> <span data-ttu-id="22993-130">Deze methode retourneert een generator.</span><span class="sxs-lookup"><span data-stu-id="22993-130">This method returns a generator.</span></span> <span data-ttu-id="22993-131">Hallo volgende code levert Hallo **naam** van elke blob in een container toohello-console.</span><span class="sxs-lookup"><span data-stu-id="22993-131">hello following code outputs hello **name** of each blob in a container toohello console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="22993-132">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="22993-132">Download blobs</span></span>
<span data-ttu-id="22993-133">toodownload gegevens van een blob gebruiken **ophalen\_blob\_naar\_pad**, **ophalen\_blob\_naar\_stroom**, **ophalen\_blob\_naar\_bytes**, of **ophalen\_blob\_naar\_tekst**.</span><span class="sxs-lookup"><span data-stu-id="22993-133">toodownload data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="22993-134">Op hoog niveau van de methoden die Hallo nodig verdeling in segmenten uitvoeren wanneer Hallo Hallo gegevens groter zijn dan 64 MB zijn.</span><span class="sxs-lookup"><span data-stu-id="22993-134">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="22993-135">Hallo volgende voorbeeld worden **ophalen\_blob\_naar\_pad** toodownload Hallo inhoud Hallo **myblob** blob en sla het toohello **out sunset.png** bestand.</span><span class="sxs-lookup"><span data-stu-id="22993-135">hello following example demonstrates using **get\_blob\_to\_path** toodownload hello contents of hello **myblob** blob and store it toohello **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="22993-136">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="22993-136">Delete a blob</span></span>
<span data-ttu-id="22993-137">Tenslotte toodelete een blob roept **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="22993-137">Finally, toodelete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="22993-138">Schrijven tooan toevoeg-blob</span><span class="sxs-lookup"><span data-stu-id="22993-138">Writing tooan append blob</span></span>
<span data-ttu-id="22993-139">Een toevoeg-blob is geoptimaliseerd voor toevoegbewerkingen, zoals logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="22993-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="22993-140">Zoals een blok-blob bestaat een toevoeg-blob uit blokken, maar wanneer u een nieuw blok tooan toevoeg-blob toevoegt, wordt het altijd toegevoegde toohello einde van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="22993-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="22993-141">U kunt een bestaand blok in een toevoeg-blob niet bijwerken of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="22993-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="22993-142">Hallo blok-id's voor een toevoeg-blob worden niet weergegeven zoals ze zijn voor een blok-blob.</span><span class="sxs-lookup"><span data-stu-id="22993-142">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="22993-143">Elk blok in een toevoeg-blob kan een andere grootte, up tooa maximaal 4 MB en een toevoeg-blob kan maximaal 50.000 blokken bevatten.</span><span class="sxs-lookup"><span data-stu-id="22993-143">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="22993-144">Hallo maximale grootte van een toevoeg-blob is daarom iets meer dan 195 GB (4 MB X 50.000 blokken).</span><span class="sxs-lookup"><span data-stu-id="22993-144">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="22993-145">Hallo in het volgende voorbeeld maakt u een nieuwe toevoeg-blob en voegt sommige gegevens tooit, een bewerking voor eenvoudige logboekregistratie simuleren.</span><span class="sxs-lookup"><span data-stu-id="22993-145">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="22993-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22993-146">Next steps</span></span>
<span data-ttu-id="22993-147">Nu u Hallo basisprincipes van Blob storage hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="22993-147">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="22993-148">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="22993-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="22993-149">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="22993-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="22993-150">[Blog van het Azure Storage-team]</span><span class="sxs-lookup"><span data-stu-id="22993-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="22993-151">[Microsoft Azure-opslag-SDK voor Python]</span><span class="sxs-lookup"><span data-stu-id="22993-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog van het Azure Storage-team]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure-opslag-SDK voor Python]: https://github.com/Azure/azure-storage-python
