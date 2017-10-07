---
title: aaaHow toouse Blob storage (objectopslag) met Ruby | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
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
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="c915c-103">Hoe toouse Blob-opslag met Ruby</span><span class="sxs-lookup"><span data-stu-id="c915c-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="c915c-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c915c-104">Overview</span></span>
<span data-ttu-id="c915c-105">Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat.</span><span class="sxs-lookup"><span data-stu-id="c915c-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="c915c-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c915c-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="c915c-107">BLOB-opslag is ook bedoeld tooas vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="c915c-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="c915c-108">Deze handleiding leert u hoe tooperform algemene scenario's met behulp van Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="c915c-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="c915c-109">Hallo-voorbeelden zijn geschreven met behulp van Hallo Ruby-API.</span><span class="sxs-lookup"><span data-stu-id="c915c-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="c915c-110">Hallo scenario's worden behandeld: **uploaden, aanbieding, gedownload,** en **verwijderen** blobs.</span><span class="sxs-lookup"><span data-stu-id="c915c-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="c915c-111">Een Ruby-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="c915c-111">Create a Ruby application</span></span>
<span data-ttu-id="c915c-112">Maak een Ruby toepassing.</span><span class="sxs-lookup"><span data-stu-id="c915c-112">Create a Ruby application.</span></span> <span data-ttu-id="c915c-113">Zie voor instructies [Ruby op Rails webtoepassing op een virtuele machine in Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="c915c-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="c915c-114">Uw toepassing tooaccess opslag configureren</span><span class="sxs-lookup"><span data-stu-id="c915c-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="c915c-115">toouse Azure Storage, moet u toodownload en gebruik Hallo Ruby azure, dit pakket bevat een set met gemak bibliotheken die met de Hallo storage REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="c915c-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="c915c-116">RubyGems tooobtain Hallo pakket gebruiken</span><span class="sxs-lookup"><span data-stu-id="c915c-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="c915c-117">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="c915c-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="c915c-118">Typ 'gem installeren azure' hello opdracht venster tooinstall Hallo gem en afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="c915c-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="c915c-119">Hallo-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="c915c-119">Import hello package</span></span>
<span data-ttu-id="c915c-120">Met uw favoriete teksteditor toevoegen Hallo toohello bovenaan Hallo Ruby bestand waarin u van plan toouse opslag bent te volgen:</span><span class="sxs-lookup"><span data-stu-id="c915c-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="c915c-121">Een Azure Storage-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="c915c-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="c915c-122">Hello azure module lezen Hallo omgevingsvariabelen **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_ACCESS_KEY** voor informatie vereist tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="c915c-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c915c-123">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo voordat u **Azure::Blob::BlobService** Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="c915c-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="c915c-124">tooobtain deze waarden van een klassiek of Resource Manager-storage-account in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="c915c-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="c915c-125">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c915c-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c915c-126">Navigeer toohello gewenste toouse storage-account.</span><span class="sxs-lookup"><span data-stu-id="c915c-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="c915c-127">Klik op Hallo instellingenblade op Hallo rechts **toegangstoetsen**.</span><span class="sxs-lookup"><span data-stu-id="c915c-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="c915c-128">Hallo toegang sleutels blade die wordt weergegeven, ziet u Hallo toegangssleutel 1 en toegangssleutel 2.</span><span class="sxs-lookup"><span data-stu-id="c915c-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="c915c-129">U kunt een van beide gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c915c-129">You can use either of these.</span></span>
5. <span data-ttu-id="c915c-130">Klik op Hallo kopiëren pictogram toocopy Hallo sleutel toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="c915c-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="c915c-131">Een container maken</span><span class="sxs-lookup"><span data-stu-id="c915c-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="c915c-132">Hallo **Azure::Blob::BlobService** object kunt u samenwerken met containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="c915c-132">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="c915c-133">toocreate een container gebruiken Hallo **maken\_container()** methode.</span><span class="sxs-lookup"><span data-stu-id="c915c-133">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="c915c-134">Hallo volgende codevoorbeeld maakt een container of afdrukken Hallo fout indien deze aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="c915c-134">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="c915c-135">Als u toomake Hallo bestanden in de container Hallo openbare wilt, kunt u Hallo-container machtigingen instellen.</span><span class="sxs-lookup"><span data-stu-id="c915c-135">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="c915c-136">U kunt alleen Hallo wijzigen <strong>maken\_container()</strong> aanroep toopass hello **: openbare\_toegang\_niveau** optie:</span><span class="sxs-lookup"><span data-stu-id="c915c-136">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="c915c-137">Geldige waarden voor Hallo **: openbare\_toegang\_niveau** optie zijn:</span><span class="sxs-lookup"><span data-stu-id="c915c-137">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="c915c-138">**BLOB:** geeft openbare leestoegang voor blobs.</span><span class="sxs-lookup"><span data-stu-id="c915c-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="c915c-139">BLOB-gegevens in deze container via anonieme aanvragen kunnen worden gelezen, maar de containergegevens is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="c915c-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="c915c-140">Clients kunnen blobs in de container Hallo via anonieme aanvragen niet opsommen.</span><span class="sxs-lookup"><span data-stu-id="c915c-140">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="c915c-141">**container:** Hiermee geeft u op volledige openbare leestoegang voor container en de blob-gegevens.</span><span class="sxs-lookup"><span data-stu-id="c915c-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="c915c-142">Clients kunnen opsommen blobs in de container Hallo via anonieme aanvraag, maar kunnen de containers in Hallo storage-account niet inventariseren.</span><span class="sxs-lookup"><span data-stu-id="c915c-142">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="c915c-143">U kunt ook Hallo openbare toegangsniveau van een container wijzigen met behulp van **ingesteld\_container\_acl()** methode toospecify Hallo openbare toegangsniveau.</span><span class="sxs-lookup"><span data-stu-id="c915c-143">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="c915c-144">Hallo met het volgende codevoorbeeld wijzigingen Hallo openbare toegangsniveau te**container**:</span><span class="sxs-lookup"><span data-stu-id="c915c-144">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="c915c-145">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="c915c-145">Upload a blob into a container</span></span>
<span data-ttu-id="c915c-146">tooupload inhoud tooa blob, gebruik Hallo **maken\_blok\_blob()** methode toocreate Hallo blob, gebruikt u een bestand of een tekenreekstype als Hallo inhoud van het Hallo-blob.</span><span class="sxs-lookup"><span data-stu-id="c915c-146">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="c915c-147">Hallo volgende code Hallo bestand geüpload **test.png** als een nieuwe blob met de naam 'installatiekopie-blob' in het Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="c915c-147">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="c915c-148">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="c915c-148">List hello blobs in a container</span></span>
<span data-ttu-id="c915c-149">Gebruik toolist Hallo containers **list_containers()** methode.</span><span class="sxs-lookup"><span data-stu-id="c915c-149">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="c915c-150">toolist hello blobs binnen een container gebruiken **lijst\_blobs()** methode.</span><span class="sxs-lookup"><span data-stu-id="c915c-150">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="c915c-151">Dit levert Hallo-URL's van alle Hallo blobs in alle Hallo containers voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="c915c-151">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="c915c-152">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="c915c-152">Download blobs</span></span>
<span data-ttu-id="c915c-153">toodownload blobs, gebruik Hallo **ophalen\_blob()** methode tooretrieve Hallo inhoud.</span><span class="sxs-lookup"><span data-stu-id="c915c-153">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="c915c-154">Hallo volgende voorbeeldcode laat zien met **ophalen\_blob()** toodownload inhoud van 'installatiekopie-blob' Hallo en het lokale bestand tooa schrijven.</span><span class="sxs-lookup"><span data-stu-id="c915c-154">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="c915c-155">Verwijderen van een Blob</span><span class="sxs-lookup"><span data-stu-id="c915c-155">Delete a Blob</span></span>
<span data-ttu-id="c915c-156">Een blob toodelete gebruik tot slot Hallo **verwijderen\_blob()** methode.</span><span class="sxs-lookup"><span data-stu-id="c915c-156">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="c915c-157">Hallo volgende voorbeeldcode laat zien hoe toodelete een blob.</span><span class="sxs-lookup"><span data-stu-id="c915c-157">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="c915c-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c915c-158">Next steps</span></span>
<span data-ttu-id="c915c-159">toolearn over complexere opslagtaken, volgt u deze koppelingen:</span><span class="sxs-lookup"><span data-stu-id="c915c-159">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="c915c-160">Blog van het Azure Storage-team</span><span class="sxs-lookup"><span data-stu-id="c915c-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="c915c-161">[Azure SDK voor Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) opslagplaats op GitHub</span><span class="sxs-lookup"><span data-stu-id="c915c-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="c915c-162">Gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo</span><span class="sxs-lookup"><span data-stu-id="c915c-162">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

