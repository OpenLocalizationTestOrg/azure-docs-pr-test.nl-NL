---
title: aaaHow toouse blob storage (objectopslag) van C++ | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="01e2c-103">Hoe toouse C++ Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="01e2c-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="01e2c-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="01e2c-104">Overview</span></span>
<span data-ttu-id="01e2c-105">Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat.</span><span class="sxs-lookup"><span data-stu-id="01e2c-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="01e2c-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="01e2c-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="01e2c-107">BLOB-opslag is ook bedoeld tooas vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="01e2c-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="01e2c-108">Deze handleiding wordt gedemonstreerd hoe tooperform algemene scenario's met behulp van hello Azure Blob storage-service.</span><span class="sxs-lookup"><span data-stu-id="01e2c-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="01e2c-109">Hallo-voorbeelden zijn geschreven in C++ en gebruiken van Hallo [Azure Storage-clientbibliotheek voor C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="01e2c-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="01e2c-110">Hallo scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs.</span><span class="sxs-lookup"><span data-stu-id="01e2c-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="01e2c-111">Doel is van deze handleiding hello Azure Storage-clientbibliotheek voor C++ versie 1.0.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="01e2c-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="01e2c-112">Hallo aanbevolen versie is Storage-clientbibliotheek 2.2.0, die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="01e2c-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="01e2c-113">Een C++-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="01e2c-113">Create a C++ application</span></span>
<span data-ttu-id="01e2c-114">In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een C++-toepassing.</span><span class="sxs-lookup"><span data-stu-id="01e2c-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="01e2c-115">toodo geval is, moet u tooinstall hello Azure Storage-clientbibliotheek voor C++ en een Azure storage-account maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="01e2c-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="01e2c-116">tooinstall hello Azure Storage-clientbibliotheek voor C++, kunt u Hallo volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="01e2c-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="01e2c-117">**Linux:** Hallo instructies gegeven in Hallo [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="01e2c-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="01e2c-118">**Windows:** In Visual Studio, klikt u op **Extra > NuGet Package Manager > Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="01e2c-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="01e2c-119">Type Hallo volgende opdracht in Hallo [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="01e2c-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="01e2c-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="01e2c-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="01e2c-121">Uw toepassing tooaccess Blob-opslag configureren</span><span class="sxs-lookup"><span data-stu-id="01e2c-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="01e2c-122">Toegevoegd Hallo volgende overzichten toohello boven in Hallo C++ bestand waar u toouse hello Azure storage-API's tooaccess blobs bevatten:</span><span class="sxs-lookup"><span data-stu-id="01e2c-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="01e2c-123">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="01e2c-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="01e2c-124">Een Azure-opslag-client maakt gebruik van een storage connection string toostore eindpunten en referenties voor toegang tot gegevens beheerservices.</span><span class="sxs-lookup"><span data-stu-id="01e2c-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="01e2c-125">Wanneer een client-toepassing wordt uitgevoerd, moet u opgeven Hallo verbindingsreeks voor opslag in Hallo indeling te volgen, met behulp van Hallo-naam van uw storage-account en Hallo toegangssleutel voor opslag voor Hallo storage-account die worden vermeld in Hallo [Azure Portal](https://portal.azure.com)voor Hallo *AccountName* en *AccountKey* waarden.</span><span class="sxs-lookup"><span data-stu-id="01e2c-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="01e2c-126">Zie voor informatie over de storage-accounts en toegangstoetsen, [over Azure Storage-Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01e2c-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="01e2c-127">Dit voorbeeld ziet hoe u een statisch veld toohold Hallo-verbindingsreeks kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="01e2c-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="01e2c-128">tootest uw toepassing in de lokale Windows-computer, kunt u Microsoft Azure Hallo [opslagemulator](../storage-use-emulator.md) die is geïnstalleerd met Hallo [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="01e2c-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="01e2c-129">Hallo-opslagemulator is een hulpprogramma dat Hallo Blob, wachtrijen en tabellen services beschikbaar zijn in Azure op uw lokale ontwikkelcomputer simuleert.</span><span class="sxs-lookup"><span data-stu-id="01e2c-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="01e2c-130">Hallo volgende voorbeeld ziet u hoe u een statisch veld toohold Hallo connection string tooyour lokale opslagemulator kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="01e2c-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="01e2c-131">toostart hello Azure-opslagemulator Selecteer Hallo **Start** of drukt u op Hallo **Windows** sleutel.</span><span class="sxs-lookup"><span data-stu-id="01e2c-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="01e2c-132">Begint te typen **Azure-Opslagemulator**, en selecteer **Microsoft Azure-Opslagemulator** in Hallo lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="01e2c-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="01e2c-133">Hallo volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden tooget Hallo-opslagverbindingsreeks hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="01e2c-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="01e2c-134">De verbindingsreeks ophalen</span><span class="sxs-lookup"><span data-stu-id="01e2c-134">Retrieve your connection string</span></span>
<span data-ttu-id="01e2c-135">U kunt Hallo **cloud_storage_account** klasse toorepresent uw Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="01e2c-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="01e2c-136">tooretrieve uw opslag accountgegevens van de opslagverbindingsreeks hello, kunt u Hallo **parseren** methode.</span><span class="sxs-lookup"><span data-stu-id="01e2c-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="01e2c-137">Vervolgens wordt een verwijzing tooa ophalen **cloud_blob_client** klasse omdat u tooretrieve-objecten die containers en blobs die zijn opgeslagen in Blob Storage-Service Hallo vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="01e2c-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="01e2c-138">Hallo volgende code maakt een **cloud_blob_client** -object op met de Hallo account opslagobject we hierboven opgehaald:</span><span class="sxs-lookup"><span data-stu-id="01e2c-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="01e2c-139">Procedure: een container maken</span><span class="sxs-lookup"><span data-stu-id="01e2c-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="01e2c-140">Dit voorbeeld ziet u hoe toocreate een container als deze niet al bestaat:</span><span class="sxs-lookup"><span data-stu-id="01e2c-140">This example shows how toocreate a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="01e2c-141">Standaard Hallo nieuwe container privé is en u uw opslag toegang tot belangrijke toodownload blobs uit deze container moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="01e2c-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="01e2c-142">Als u toomake Hallo-bestanden (BLOB's) binnen hello container beschikbaar tooeveryone wilt, kunt u Hallo container toobe openbare met behulp van de volgende code Hallo instellen:</span><span class="sxs-lookup"><span data-stu-id="01e2c-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="01e2c-143">Iedereen op Internet Hallo blobs in een openbare container kunt zien, maar u kunt wijzigen of ze alleen verwijderen als u de juiste toegangssleutel Hallo hebt.</span><span class="sxs-lookup"><span data-stu-id="01e2c-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="01e2c-144">Procedure: een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="01e2c-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="01e2c-145">Azure Blob Storage ondersteunt blok-blobs en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="01e2c-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="01e2c-146">In Hallo meeste gevallen is het blok-blob Hallo type toouse aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="01e2c-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="01e2c-147">een bestand tooa blok-blob tooupload een containerverwijzing ophalen en deze tooget een blok-blobverwijzing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="01e2c-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="01e2c-148">Zodra u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom tooit gegevens uploaden door de aanroepende Hallo **upload_from_stream** methode.</span><span class="sxs-lookup"><span data-stu-id="01e2c-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="01e2c-149">Deze bewerking wordt Hallo blob gemaakt als deze niet eerder bestaat of overschrijven als het bestand bestaat.</span><span class="sxs-lookup"><span data-stu-id="01e2c-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="01e2c-150">Hallo volgende voorbeeld wordt getoond hoe tooupload een blob naar een container en wordt ervan uitgegaan dat Hallo-container al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="01e2c-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="01e2c-151">U kunt ook hello gebruiken **upload_from_file** methode tooupload een bestand tooa blok-blob.</span><span class="sxs-lookup"><span data-stu-id="01e2c-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="01e2c-152">Procedure: lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="01e2c-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="01e2c-153">toolist hello blobs in een container, eerst ophalen een containerverwijzing.</span><span class="sxs-lookup"><span data-stu-id="01e2c-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="01e2c-154">Vervolgens kunt u Hallo-container **list_blobs** methode tooretrieve Hallo blobs en/of mappen hierin.</span><span class="sxs-lookup"><span data-stu-id="01e2c-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="01e2c-155">tooaccess Hallo uitgebreide set eigenschappen en methoden voor een geretourneerde **list_blob_item**, moet u Hallo aanroepen **list_blob_item.as_blob** methode tooget een **cloud_blob** -object of Hallo **list_blob.as_directory** methode tooget een cloud_blob_directory-object.</span><span class="sxs-lookup"><span data-stu-id="01e2c-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="01e2c-156">Hallo volgende code laat zien hoe tooretrieve en uitvoer URI van elk item in Hallo Hallo **mijn-voorbeeld-container** container:</span><span class="sxs-lookup"><span data-stu-id="01e2c-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

<span data-ttu-id="01e2c-157">Zie voor meer informatie over het weergeven van bewerkingen [lijst Azure Storage-Resources in C++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="01e2c-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="01e2c-158">Hoe: blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="01e2c-158">How to: Download blobs</span></span>
<span data-ttu-id="01e2c-159">toodownload blobs, eerst een blobverwijzing ophalen en vervolgens aanroepen Hallo **download_to_stream** methode.</span><span class="sxs-lookup"><span data-stu-id="01e2c-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="01e2c-160">Hallo volgende voorbeeld wordt Hallo **download_to_stream** methode tootransfer Hallo blob inhoud tooa stroomobject dat u vervolgens blijven tooa lokaal bestand behouden kunt.</span><span class="sxs-lookup"><span data-stu-id="01e2c-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="01e2c-161">U kunt ook hello gebruiken **download_to_file** methode toodownload Hallo inhoud van een blob tooa-bestand.</span><span class="sxs-lookup"><span data-stu-id="01e2c-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="01e2c-162">Bovendien kunt u ook hello gebruiken **download_text** methode toodownload Hallo inhoud van een blob als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="01e2c-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="01e2c-163">Hoe: blobs verwijderen</span><span class="sxs-lookup"><span data-stu-id="01e2c-163">How to: Delete blobs</span></span>
<span data-ttu-id="01e2c-164">een blob toodelete eerst een blobverwijzing ophalen en vervolgens aanroepen Hallo **delete_blob** methode erop.</span><span class="sxs-lookup"><span data-stu-id="01e2c-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="01e2c-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01e2c-165">Next steps</span></span>
<span data-ttu-id="01e2c-166">Nu u Hallo basisprincipes van blob storage hebt geleerd, volgt u deze koppelingen toolearn meer over Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="01e2c-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="01e2c-167">Hoe toouse Queue Storage vanuit C++</span><span class="sxs-lookup"><span data-stu-id="01e2c-167">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="01e2c-168">Hoe toouse Table Storage uit het C++</span><span class="sxs-lookup"><span data-stu-id="01e2c-168">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="01e2c-169">Lijst met Azure Storage-Resources in C++</span><span class="sxs-lookup"><span data-stu-id="01e2c-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="01e2c-170">Opslagclientbibliotheek voor C++-verwijzing</span><span class="sxs-lookup"><span data-stu-id="01e2c-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="01e2c-171">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="01e2c-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="01e2c-172">Gegevensoverdracht met Hallo AzCopy-opdrachtregelprogramma</span><span class="sxs-lookup"><span data-stu-id="01e2c-172">Transfer data with hello AzCopy command-line utility</span></span>](../storage-use-azcopy.md)

