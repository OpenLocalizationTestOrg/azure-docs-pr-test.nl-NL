---
title: Het gebruik van Azure Blob storage (objectopslag) met Python | Microsoft Docs
description: Sla niet-gestructureerde gegevens op in de cloud met Azure Blob Storage (objectopslag).
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
ms.openlocfilehash: 968814db9496fd410162d482191592c8a56101f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-from-python"></a><span data-ttu-id="2f4b6-103">Hoe Azure Blob storage gebruiken met Python</span><span class="sxs-lookup"><span data-stu-id="2f4b6-103">How to use Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="2f4b6-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2f4b6-104">Overview</span></span>
<span data-ttu-id="2f4b6-105">Azure Blob Storage is een service waarmee ongestructureerde gegevens als objecten/blobs worden opgeslagen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="2f4b6-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="2f4b6-107">U kunt Blob Storage zien als een vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="2f4b6-108">In dit artikel wordt beschreven hoe u veelvoorkomende scenario's met behulp van Blob-opslag uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-108">This article will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="2f4b6-109">De voorbeelden zijn geschreven in Python en gebruik de [Microsoft Azure-opslag-SDK voor Python].</span><span class="sxs-lookup"><span data-stu-id="2f4b6-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="2f4b6-110">De scenario's worden behandeld bevatten uploaden, aanbieding, downloaden en verwijderen van blobs.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="2f4b6-111">Een container maken</span><span class="sxs-lookup"><span data-stu-id="2f4b6-111">Create a container</span></span>
<span data-ttu-id="2f4b6-112">Op basis van het type van de blob die u wilt gebruiken, maakt een **BlockBlobService**, **AppendBlobService**, of **PageBlobService** object.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="2f4b6-113">De volgende code wordt een **BlockBlobService** object.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-113">The following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="2f4b6-114">De volgende boven aan elk Python-bestand waarin u programmatisch toegang biedt tot Azure-blok-Blob-opslag wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="2f4b6-115">De volgende code maakt een **BlockBlobService** object met de naam en het account opslagaccountsleutel.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span></span>  <span data-ttu-id="2f4b6-116">'Myaccount' en 'mykey' vervangen door uw accountnaam en de sleutel.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="2f4b6-117">In het volgende voorbeeld, kunt u een **BlockBlobService** object te maken van de container als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="2f4b6-118">Standaard is de nieuwe container privé, dus u uw toegangssleutel voor opslag opgeven moet (zoals u eerder hebt gedaan) om blobs te downloaden uit deze container.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span> <span data-ttu-id="2f4b6-119">Als u de blobs in de container beschikbaar maken voor iedereen wilt, kunt u de container maken en geeft het niveau van de openbare toegang met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="2f4b6-120">U kunt ook een container wijzigen nadat u hebt gemaakt met behulp van de volgende code.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-120">Alternatively, you can modify a container after you have created it using the following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="2f4b6-121">Na deze wijziging iedereen op Internet kan blobs in een openbare container zien, maar u kunt alleen wijzigen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="2f4b6-122">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="2f4b6-122">Upload a blob into a container</span></span>
<span data-ttu-id="2f4b6-123">Voor het maken van een blok-blob en gegevens uploaden, gebruiken de **maken\_blob\_van\_pad**, **maken\_blob\_van\_stroom**, **maken\_blob\_van\_bytes** of **maken\_blob\_van\_tekst** methoden.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="2f4b6-124">Op hoog niveau methoden voor het uitvoeren van de benodigde verdeling in segmenten wanneer de grootte van de gegevens is groter dan 64 MB zijn.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="2f4b6-125">**maken\_blob\_van\_pad** uploadt u de inhoud van een bestand uit het opgegeven pad en **maken\_blob\_van\_stroom** de inhoud van een al geopend bestandsstroom uploadt.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="2f4b6-126">**maken\_blob\_van\_bytes** een bytematrix, uploadt en **maken\_blob\_van\_tekst** uploadt de opgegeven tekstwaarde met behulp van de opgegeven codering (standaard ingesteld op UTF-8).</span><span class="sxs-lookup"><span data-stu-id="2f4b6-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="2f4b6-127">Het volgende voorbeeld wordt de inhoud van geüpload de **sunset.png** bestand naar de **myblob** blob.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="2f4b6-128">De blobs in een container in een lijst weergeven</span><span class="sxs-lookup"><span data-stu-id="2f4b6-128">List the blobs in a container</span></span>
<span data-ttu-id="2f4b6-129">Als de blobs in een container wilt weergeven, gebruikt de **lijst\_blobs** methode.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-129">To list the blobs in a container, use the **list\_blobs** method.</span></span> <span data-ttu-id="2f4b6-130">Deze methode retourneert een generator.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-130">This method returns a generator.</span></span> <span data-ttu-id="2f4b6-131">De volgende code uitvoer de **naam** van elke blob in een container met de console.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-131">The following code outputs the **name** of each blob in a container to the console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="2f4b6-132">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="2f4b6-132">Download blobs</span></span>
<span data-ttu-id="2f4b6-133">Als u wilt downloaden van gegevens van een blob **ophalen\_blob\_naar\_pad**, **ophalen\_blob\_naar\_stroom**, **ophalen\_blob\_naar\_bytes**, of **ophalen\_blob\_naar\_tekst**.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="2f4b6-134">Op hoog niveau methoden voor het uitvoeren van de benodigde verdeling in segmenten wanneer de grootte van de gegevens is groter dan 64 MB zijn.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="2f4b6-135">Het volgende voorbeeld worden **ophalen\_blob\_naar\_pad** voor het downloaden van de inhoud van de **myblob** blob en op te slaan op de **out sunset.png** bestand.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="2f4b6-136">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="2f4b6-136">Delete a blob</span></span>
<span data-ttu-id="2f4b6-137">Tenslotte voor het verwijderen van een blob, roept **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-137">Finally, to delete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="2f4b6-138">Schrijven naar een toevoeg-blob</span><span class="sxs-lookup"><span data-stu-id="2f4b6-138">Writing to an append blob</span></span>
<span data-ttu-id="2f4b6-139">Een toevoeg-blob is geoptimaliseerd voor toevoegbewerkingen, zoals logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="2f4b6-140">Net als een blok-blob bestaat een toevoeg-blob uit blokken, maar wanneer u een nieuw blok aan een toevoeg-blob toevoegt, wordt het altijd toegevoegd aan het einde van de blob.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="2f4b6-141">U kunt een bestaand blok in een toevoeg-blob niet bijwerken of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="2f4b6-142">De blok-id's voor een toevoeg-blob worden niet weergegeven zoals voor een blok-blob.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-142">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="2f4b6-143">Alle blokken in een toevoeg-blob kunnen verschillend van grootte zijn. De maximale grootte is 4 MB. Een toevoeg-blob kan maximaal 50.000 blokken bevatten.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="2f4b6-144">De maximale grootte van een toevoeg-blob is daarom iets meer dan 195 GB (4 MB X 50.000 blokken).</span><span class="sxs-lookup"><span data-stu-id="2f4b6-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="2f4b6-145">In onderstaand voorbeeld wordt een nieuwe toevoeg-blob gemaakt en worden er enkele gegevens aan toegevoegd, waarmee een eenvoudige logboekregistratiebewerking wordt gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# The same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="2f4b6-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f4b6-146">Next steps</span></span>
<span data-ttu-id="2f4b6-147">U bent nu bekend met de basisprincipes van Blob Storage. Volg deze koppelingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2f4b6-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="2f4b6-148">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="2f4b6-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="2f4b6-149">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="2f4b6-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="2f4b6-150">[Blog van het Azure Storage-team]</span><span class="sxs-lookup"><span data-stu-id="2f4b6-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="2f4b6-151">[Microsoft Azure-opslag-SDK voor Python]</span><span class="sxs-lookup"><span data-stu-id="2f4b6-151">[Microsoft Azure Storage SDK for Python]</span></span>

<span data-ttu-id="2f4b6-152">[Blog van het Azure Storage-team]: http://blogs.msdn.com/b/windowsazurestorage/</span><span class="sxs-lookup"><span data-stu-id="2f4b6-152">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/</span></span>
<span data-ttu-id="2f4b6-153">[Microsoft Azure-opslag-SDK voor Python]: https://github.com/Azure/azure-storage-python</span><span class="sxs-lookup"><span data-stu-id="2f4b6-153">[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python</span></span>
