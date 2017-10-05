---
title: Het gebruik van Blob storage (objectopslag) met Ruby | Microsoft Docs
description: Sla niet-gestructureerde gegevens op in de cloud met Azure Blob Storage (objectopslag).
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: d27cf1594d6a31a746ca85b5c3184f8a5dbbaa54
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="634db-103">Blob Storage gebruiken met Ruby</span><span class="sxs-lookup"><span data-stu-id="634db-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="634db-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="634db-104">Overview</span></span>
<span data-ttu-id="634db-105">Azure Blob Storage is een service waarmee ongestructureerde gegevens als objecten/blobs worden opgeslagen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="634db-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="634db-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="634db-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="634db-107">U kunt Blob Storage zien als een vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="634db-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="634db-108">Deze handleiding wordt beschreven hoe u veelvoorkomende scenario's met behulp van Blob-opslag uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="634db-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="634db-109">De voorbeelden zijn geschreven met behulp van de Ruby-API.</span><span class="sxs-lookup"><span data-stu-id="634db-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="634db-110">De scenario's worden behandeld: **uploaden, aanbieding, gedownload,** en **verwijderen** blobs.</span><span class="sxs-lookup"><span data-stu-id="634db-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="634db-111">Een Ruby-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="634db-111">Create a Ruby application</span></span>
<span data-ttu-id="634db-112">Maak een Ruby toepassing.</span><span class="sxs-lookup"><span data-stu-id="634db-112">Create a Ruby application.</span></span> <span data-ttu-id="634db-113">Zie voor instructies [Ruby op Rails webtoepassing op een virtuele machine in Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="634db-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="634db-114">Uw toepassing configureren voor toegang tot opslag</span><span class="sxs-lookup"><span data-stu-id="634db-114">Configure your application to access Storage</span></span>
<span data-ttu-id="634db-115">Voor het gebruik van Azure Storage, die u wilt downloaden en gebruiken van het Ruby azure pakket bevat een set met gemak bibliotheken die met de storage REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="634db-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="634db-116">RubyGems gebruiken om het pakket te verkrijgen</span><span class="sxs-lookup"><span data-stu-id="634db-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="634db-117">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="634db-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="634db-118">Typ 'azure gem installeren' in het opdrachtvenster voor het installeren van de gem en afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="634db-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="634db-119">Het pakket importeren</span><span class="sxs-lookup"><span data-stu-id="634db-119">Import the package</span></span>
<span data-ttu-id="634db-120">Met behulp van uw favoriete teksteditor, voeg de volgende boven aan het Ruby bestand waarop u wilt opslag gebruiken:</span><span class="sxs-lookup"><span data-stu-id="634db-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="634db-121">Een Azure Storage-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="634db-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="634db-122">De azure-module leest de omgevingsvariabelen **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_ACCESS_KEY** voor meer informatie verbinding maken met uw Azure storage-account vereist.</span><span class="sxs-lookup"><span data-stu-id="634db-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="634db-123">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens voordat u **Azure::Blob::BlobService** met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="634db-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="634db-124">Als u deze waarden van een klassiek of Resource Manager-opslagaccount in de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="634db-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="634db-125">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="634db-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="634db-126">Ga naar het opslagaccount dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="634db-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="634db-127">Klik op de blade instellingen aan de rechterkant **toegangstoetsen**.</span><span class="sxs-lookup"><span data-stu-id="634db-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="634db-128">In de blade van de toegang tot sleutels die wordt weergegeven, ziet u de toegangssleutel 1 en toegangssleutel 2.</span><span class="sxs-lookup"><span data-stu-id="634db-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="634db-129">U kunt een van beide gebruiken.</span><span class="sxs-lookup"><span data-stu-id="634db-129">You can use either of these.</span></span>
5. <span data-ttu-id="634db-130">Klik op het pictogram kopiëren om de sleutel naar het Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="634db-130">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="634db-131">Een container maken</span><span class="sxs-lookup"><span data-stu-id="634db-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="634db-132">De **Azure::Blob::BlobService** object kunt u samenwerken met containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="634db-132">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="634db-133">Gebruik voor het maken van een container de **maken\_container()** methode.</span><span class="sxs-lookup"><span data-stu-id="634db-133">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="634db-134">Het volgende codevoorbeeld maakt een container of de fout wordt afgedrukt indien deze aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="634db-134">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="634db-135">Als u de bestanden in de container openbaar maken wilt, kunt u de container machtigingen instellen.</span><span class="sxs-lookup"><span data-stu-id="634db-135">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="634db-136">U kunt alleen de <strong>maken\_container()</strong> aanroep om door te geven de **: openbare\_toegang\_niveau** optie:</span><span class="sxs-lookup"><span data-stu-id="634db-136">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="634db-137">Geldige waarden voor de **: openbare\_toegang\_niveau** optie zijn:</span><span class="sxs-lookup"><span data-stu-id="634db-137">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="634db-138">**BLOB:** geeft openbare leestoegang voor blobs.</span><span class="sxs-lookup"><span data-stu-id="634db-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="634db-139">BLOB-gegevens in deze container via anonieme aanvragen kunnen worden gelezen, maar de containergegevens is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="634db-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="634db-140">Clients kunnen blobs in de container via anonieme aanvragen niet opsommen.</span><span class="sxs-lookup"><span data-stu-id="634db-140">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="634db-141">**container:** Hiermee geeft u op volledige openbare leestoegang voor container en de blob-gegevens.</span><span class="sxs-lookup"><span data-stu-id="634db-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="634db-142">Clients kunnen inventariseren blobs in de container via anonieme aanvraag, maar kunnen containers in het opslagaccount niet inventariseren.</span><span class="sxs-lookup"><span data-stu-id="634db-142">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="634db-143">U kunt ook het niveau van de openbare toegang van een container wijzigen met behulp van **ingesteld\_container\_acl()** methode om de openbare toegang op te geven.</span><span class="sxs-lookup"><span data-stu-id="634db-143">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="634db-144">Het volgende codevoorbeeld verandert het openbare toegangsniveau voor **container**:</span><span class="sxs-lookup"><span data-stu-id="634db-144">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="634db-145">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="634db-145">Upload a blob into a container</span></span>
<span data-ttu-id="634db-146">Als u wilt uploaden inhoud naar een blob, gebruiken de **maken\_blok\_blob()** methode voor het maken van de blob, een bestand of tekenreeks gebruiken als de inhoud van de blob.</span><span class="sxs-lookup"><span data-stu-id="634db-146">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="634db-147">De volgende code wordt het bestand geüpload **test.png** als een nieuwe blob met de naam 'installatiekopie-blob' in de container.</span><span class="sxs-lookup"><span data-stu-id="634db-147">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="634db-148">De blobs in een container in een lijst weergeven</span><span class="sxs-lookup"><span data-stu-id="634db-148">List the blobs in a container</span></span>
<span data-ttu-id="634db-149">U kunt de containers gebruiken **list_containers()** methode.</span><span class="sxs-lookup"><span data-stu-id="634db-149">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="634db-150">U kunt de blobs in een container gebruiken **lijst\_blobs()** methode.</span><span class="sxs-lookup"><span data-stu-id="634db-150">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="634db-151">Hiermee wordt de uitvoer de URL's van de blobs in de containers voor het account.</span><span class="sxs-lookup"><span data-stu-id="634db-151">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="634db-152">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="634db-152">Download blobs</span></span>
<span data-ttu-id="634db-153">Om blobs te downloaden, gebruiken de **ophalen\_blob()** methode voor het ophalen van de inhoud.</span><span class="sxs-lookup"><span data-stu-id="634db-153">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="634db-154">De volgende voorbeeldcode laat zien met **ophalen\_blob()** voor het downloaden van de inhoud van 'installatiekopie-blob' en schrijven naar een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="634db-154">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="634db-155">Verwijderen van een Blob</span><span class="sxs-lookup"><span data-stu-id="634db-155">Delete a Blob</span></span>
<span data-ttu-id="634db-156">Gebruik tot slot voor het verwijderen van een blob, de **verwijderen\_blob()** methode.</span><span class="sxs-lookup"><span data-stu-id="634db-156">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="634db-157">De volgende voorbeeldcode laat zien hoe u van een blob.</span><span class="sxs-lookup"><span data-stu-id="634db-157">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="634db-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="634db-158">Next steps</span></span>
<span data-ttu-id="634db-159">Voor meer informatie over complexere opslagtaken, volgt u deze koppelingen:</span><span class="sxs-lookup"><span data-stu-id="634db-159">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="634db-160">Blog van het Azure Storage-team</span><span class="sxs-lookup"><span data-stu-id="634db-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="634db-161">[Azure SDK voor Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) opslagplaats op GitHub</span><span class="sxs-lookup"><span data-stu-id="634db-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="634db-162">Gegevensoverdracht met het AzCopy-opdrachtregelprogramma</span><span class="sxs-lookup"><span data-stu-id="634db-162">Transfer data with the AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

