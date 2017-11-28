---
title: Het gebruik van blob storage (objectopslag) van C++ | Microsoft Docs
description: Sla niet-gestructureerde gegevens op in de cloud met Azure Blob Storage (objectopslag).
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
ms.openlocfilehash: daf480b7be78dc001712010eac6386d4744c3c1d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="1e9ad-103">Het Blob Storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="1e9ad-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="1e9ad-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1e9ad-104">Overview</span></span>
<span data-ttu-id="1e9ad-105">Azure Blob Storage is een service waarmee ongestructureerde gegevens als objecten/blobs worden opgeslagen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="1e9ad-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="1e9ad-107">U kunt Blob Storage zien als een vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="1e9ad-108">Deze handleiding wordt gedemonstreerd hoe u veelvoorkomende scenario's met behulp van de Azure Blob storage-service uitvoert.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="1e9ad-109">De voorbeelden zijn geschreven in C++ en gebruik de [Azure Storage-clientbibliotheek voor C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="1e9ad-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="1e9ad-110">De scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="1e9ad-111">Deze handleiding is bedoeld voor de Azure Storage-clientbibliotheek voor C++ versie 1.0.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="1e9ad-112">De aanbevolen versie is Storage-clientbibliotheek 2.2.0, die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="1e9ad-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="1e9ad-113">Een C++-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="1e9ad-113">Create a C++ application</span></span>
<span data-ttu-id="1e9ad-114">In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een C++-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="1e9ad-115">Om dit te doen, moet u voor het installeren van de Azure Storage-clientbibliotheek voor C++ en een Azure storage-account maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="1e9ad-116">Voor het installeren van de Azure Storage-clientbibliotheek voor C++, kunt u de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="1e9ad-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="1e9ad-117">**Linux:** Volg de instructies in de [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="1e9ad-118">**Windows:** In Visual Studio, klikt u op **Extra > NuGet Package Manager > Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="1e9ad-119">Typ de volgende opdracht in de [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="1e9ad-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="1e9ad-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="1e9ad-121">Uw toepassing configureren voor toegang tot Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="1e9ad-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="1e9ad-122">Toevoegen aan dat de volgende instructies toe aan de bovenkant van het bestand C++ is waar u de Azure storage-API's gebruiken voor toegang tot blobs instructies bevatten:</span><span class="sxs-lookup"><span data-stu-id="1e9ad-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="1e9ad-123">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="1e9ad-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="1e9ad-124">Een Azure-opslag-client gebruikt een verbindingsreeks voor opslag voor het opslaan van eindpunten en referenties voor toegang tot gegevens beheerservices.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="1e9ad-125">Wanneer u in een clienttoepassing uitvoert, moet u opgeven de verbindingsreeks voor opslag in de volgende indeling met de naam van uw opslagaccount en de toegangssleutel voor opslag voor de storage-account wordt vermeld in de [Azure Portal](https://portal.azure.com) voor de *AccountName* en *AccountKey* waarden.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="1e9ad-126">Zie voor informatie over de storage-accounts en toegangstoetsen, [over Azure Storage-Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e9ad-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="1e9ad-127">Dit voorbeeld ziet hoe u een statisch veld voor het opslaan van de verbindingsreeks kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="1e9ad-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="1e9ad-128">Testen van uw toepassing in uw lokale Windows-computer, kunt u de Microsoft Azure [opslagemulator](../storage-use-emulator.md) die is geïnstalleerd met de [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1e9ad-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="1e9ad-129">De opslagemulator is een hulpprogramma dat de services Blob, wachtrijen en tabellen beschikbaar zijn in Azure op uw lokale ontwikkelcomputer simuleert.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="1e9ad-130">Het volgende voorbeeld ziet u hoe u een statisch veld voor het opslaan van de verbindingsreeks naar uw lokale opslagemulator kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="1e9ad-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="1e9ad-131">Voor het starten van de Azure-opslagemulator, selecteer de **Start** of drukt u op de **Windows** sleutel.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="1e9ad-132">Begint te typen **Azure-Opslagemulator**, en selecteer **Microsoft Azure-Opslagemulator** uit de lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="1e9ad-133">De volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden hebt gebruikt om op te halen van de verbindingsreeks voor opslag.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="1e9ad-134">De verbindingsreeks ophalen</span><span class="sxs-lookup"><span data-stu-id="1e9ad-134">Retrieve your connection string</span></span>
<span data-ttu-id="1e9ad-135">U kunt de **cloud_storage_account** klasse vertegenwoordigt de informatie van uw Opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="1e9ad-136">Voor het ophalen van gegevens over uw storage-account van de verbindingsreeks voor opslag, kunt u de **parseren** methode.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="1e9ad-137">Vervolgens maakt geen verwijzing ophalen naar een **cloud_blob_client** klasse omdat u objecten die vertegenwoordigen containers en blobs die zijn opgeslagen in de Blob Storage-Service ophalen.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="1e9ad-138">De volgende code maakt een **cloud_blob_client** object met het account opslagobject we hierboven opgehaald:</span><span class="sxs-lookup"><span data-stu-id="1e9ad-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="1e9ad-139">Procedure: een container maken</span><span class="sxs-lookup"><span data-stu-id="1e9ad-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="1e9ad-140">In dit voorbeeld ziet u hoe u een container kunt maken als deze nog niet bestaat:</span><span class="sxs-lookup"><span data-stu-id="1e9ad-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="1e9ad-141">Standaard is de nieuwe container privé en moet u uw toegangssleutel voor opslag om blobs te downloaden uit deze container.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="1e9ad-142">Als u wilt dat de bestanden (BLOB's) in de container beschikbaar maken voor iedereen, kunt u de container openbaar met de volgende code instellen:</span><span class="sxs-lookup"><span data-stu-id="1e9ad-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="1e9ad-143">Iedereen op Internet kan blobs in een openbare container zien, maar u kunt wijzigen of ze alleen verwijderen als u de juiste sleutel hebt.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="1e9ad-144">Procedure: een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="1e9ad-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="1e9ad-145">Azure Blob Storage ondersteunt blok-blobs en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="1e9ad-146">In de meeste gevallen is een blok-blob het aangewezen type om te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="1e9ad-147">Om een bestand naar een blok-blob te uploaden, haalt u een containerverwijzing op en gebruikt u deze om een blok-blobverwijzing op te halen.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="1e9ad-148">Zodra u een blobverwijzing hebt, kunt u een stream met gegevens uploaden naar het door het aanroepen van de **upload_from_stream** methode.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="1e9ad-149">Met deze bewerking wordt de blob gemaakt (als deze nog niet bestaat) of overschreven (als deze wel al bestaat).</span><span class="sxs-lookup"><span data-stu-id="1e9ad-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="1e9ad-150">Het volgende voorbeeld laat zien hoe u een blob uploadt naar een container. Hierbij wordt ervan uitgegaan dat de container al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="1e9ad-151">U kunt ook de **upload_from_file** methode voor het uploaden van een bestand naar een blok-blob.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="1e9ad-152">Procedure: lijst van de blobs in een container</span><span class="sxs-lookup"><span data-stu-id="1e9ad-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="1e9ad-153">Als u een lijst van de blobs in een container wilt weergeven, moet u eerst een containerverwijzing ophalen.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="1e9ad-154">Vervolgens kunt u de container **list_blobs** methode voor het ophalen van de blobs en/of de mappen hierin.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="1e9ad-155">Voor toegang tot de uitgebreide set eigenschappen en methoden voor een geretourneerde **list_blob_item**, moet u aanroepen de **list_blob_item.as_blob** methode om op te halen een **cloud_blob** object, of de **list_blob.as_directory** methode een cloud_blob_directory-object niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="1e9ad-156">De volgende code laat zien hoe ophalen en de uitvoer van de URI van elk item in de **mijn-voorbeeld-container** container:</span><span class="sxs-lookup"><span data-stu-id="1e9ad-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
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

<span data-ttu-id="1e9ad-157">Zie voor meer informatie over het weergeven van bewerkingen [lijst Azure Storage-Resources in C++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="1e9ad-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="1e9ad-158">Hoe: blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="1e9ad-158">How to: Download blobs</span></span>
<span data-ttu-id="1e9ad-159">Om blobs te downloaden, eerst een blobverwijzing ophalen en roept u vervolgens de **download_to_stream** methode.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="1e9ad-160">Het volgende voorbeeld wordt de **download_to_stream** methode voor het overdragen van de blobinhoud naar een stroomobject dat u vervolgens blijven in een lokaal bestand behouden kunt.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="1e9ad-161">U kunt ook de **download_to_file** methode voor het downloaden van de inhoud van een blob naar een bestand.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="1e9ad-162">Bovendien kunt u ook kunt u de **download_text** methode voor het downloaden van de inhoud van een blob als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="1e9ad-163">Hoe: blobs verwijderen</span><span class="sxs-lookup"><span data-stu-id="1e9ad-163">How to: Delete blobs</span></span>
<span data-ttu-id="1e9ad-164">U verwijdert een blob door eerst een blobverwijzing ophalen en roept u vervolgens de **delete_blob** methode erop.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="1e9ad-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e9ad-165">Next steps</span></span>
<span data-ttu-id="1e9ad-166">Nu u de basisprincipes van blob storage hebt geleerd, volgt u deze koppelingen voor meer informatie over Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="1e9ad-167">Hoe Queue Storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="1e9ad-167">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="1e9ad-168">Hoe Table Storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="1e9ad-168">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="1e9ad-169">Lijst met Azure Storage-Resources in C++</span><span class="sxs-lookup"><span data-stu-id="1e9ad-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="1e9ad-170">Opslagclientbibliotheek voor C++-verwijzing</span><span class="sxs-lookup"><span data-stu-id="1e9ad-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="1e9ad-171">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1e9ad-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="1e9ad-172">Gegevensoverdracht met het AzCopy-opdrachtregelprogramma</span><span class="sxs-lookup"><span data-stu-id="1e9ad-172">Transfer data with the AzCopy command-line utility</span></span>](../storage-use-azcopy.md)

