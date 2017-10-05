---
title: Ontwikkelen voor Azure File storage met C++ | Microsoft Docs
description: Informatie over het ontwikkelen van C++-toepassingen en services die Azure File storage gebruiken voor het opslaan van gegevens uit een bestand.
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: fc0d8451442f1337db4a36718c3fc746f8eb5125
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="f3ebb-103">Ontwikkelen voor Azure File storage met C++</span><span class="sxs-lookup"><span data-stu-id="f3ebb-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="f3ebb-104">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="f3ebb-104">About this tutorial</span></span>

<span data-ttu-id="f3ebb-105">In deze zelfstudie leert u basisbewerkingen op Azure File storage uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-105">In this tutorial, you'll learn how to perform basic operations on Azure File storage.</span></span> <span data-ttu-id="f3ebb-106">Via voorbeelden die zijn geschreven in C++, leert u hoe u Maak shares en mappen, uploaden, weergeven en verwijderen van bestanden.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-106">Through samples written in C++, you'll learn how to create shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="f3ebb-107">Als u niet bekend met Azure File storage bent, wordt gaan via de concepten in de volgende secties nuttig zijn bij het begrijpen van de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-107">If you are new to Azure File storage , going through the concepts in the sections that follow will be helpful in understanding the samples.</span></span>


* <span data-ttu-id="f3ebb-108">Maken en verwijderen van de Azure-bestandsshares</span><span class="sxs-lookup"><span data-stu-id="f3ebb-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="f3ebb-109">Maken en verwijderen van mappen</span><span class="sxs-lookup"><span data-stu-id="f3ebb-109">Create and delete directories</span></span>
* <span data-ttu-id="f3ebb-110">Bestanden en mappen in een Azure-bestandsshare opsommen</span><span class="sxs-lookup"><span data-stu-id="f3ebb-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="f3ebb-111">Uploaden, downloaden en een bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="f3ebb-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="f3ebb-112">Stel een quotum (maximumgrootte) voor een Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="f3ebb-112">Set the quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="f3ebb-113">Een Shared Access Signature (SAS-sleutel) maken voor een bestand dat gebruikmaakt van een gedeeld toegangsbeleid dat voor de share is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>

> [!Note]  
> <span data-ttu-id="f3ebb-114">Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk om eenvoudige toepassingen die toegang hebben tot de Azure-bestandsshare met behulp van de standard C++-i/o-klassen en -functies te schrijven.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-114">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard C++ I/O classes and functions.</span></span> <span data-ttu-id="f3ebb-115">In dit artikel wordt beschreven hoe schrijven van toepassingen die gebruikmaken van de Azure Storage C++ SDK, die gebruikmaakt van de [Azure File storage REST-API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) voor communicatie met Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-115">This article will describe how to write applications that use the Azure Storage C++ SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="f3ebb-116">Een C++-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="f3ebb-116">Create a C++ application</span></span>
<span data-ttu-id="f3ebb-117">Als u wilt de voorbeelden bouwt, moet u de Azure Storage-clientbibliotheek 2.4.0 voor C++ installeren.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-117">To build the samples, you will need to install the Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="f3ebb-118">U moet hebt een Azure storage-account ook gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="f3ebb-119">De Azure Storage Client 2.4.0 voor C++ installeert, kunt u een van de volgende methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f3ebb-119">To install the Azure Storage Client 2.4.0 for C++, you can use one of the following methods:</span></span>

* <span data-ttu-id="f3ebb-120">**Linux:** Volg de instructies in de [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-120">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="f3ebb-121">**Windows:** In Visual Studio, klikt u op **extra &gt; NuGet Package Manager &gt; Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="f3ebb-122">Typ de volgende opdracht in de [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-122">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="f3ebb-123">Instellen van uw toepassing Azure File storage gebruiken</span><span class="sxs-lookup"><span data-stu-id="f3ebb-123">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="f3ebb-124">Toevoegen aan dat de volgende instructies toe aan de bovenkant van het bronbestand voor C++ waar u wilt bewerken Azure File storage instructies bevatten:</span><span class="sxs-lookup"><span data-stu-id="f3ebb-124">Add the following include statements to the top of the C++ source file where you want to manipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="f3ebb-125">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="f3ebb-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="f3ebb-126">U moet verbinding maken met uw Azure storage-account voor het gebruik van File storage.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-126">To use File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="f3ebb-127">De eerste stap is om een verbindingsreeks die we gebruiken om verbinding maken met uw storage-account te configureren.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-127">The first step would be to configure a connection string, which we'll use to connect to your storage account.</span></span> <span data-ttu-id="f3ebb-128">We gaan een statische variabele hiervoor definiëren.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-128">Let's define a static variable to do that.</span></span>

```cpp
// Define the connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="f3ebb-129">Verbinding maken met een Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="f3ebb-129">Connecting to an Azure storage account</span></span>
<span data-ttu-id="f3ebb-130">U kunt de **cloud_storage_account** klasse vertegenwoordigt de informatie van uw Opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-130">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="f3ebb-131">Voor het ophalen van gegevens over uw storage-account van de verbindingsreeks voor opslag, kunt u de **parseren** methode.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-131">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="f3ebb-132">Een Azure-bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="f3ebb-132">Create an Azure File share</span></span>
<span data-ttu-id="f3ebb-133">Alle bestanden en mappen in Azure File storage bevinden zich in een zogenaamd een **Share**.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="f3ebb-134">Uw storage-account kan als veel shares als de capaciteit van uw account kunt hebben.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="f3ebb-135">Als u wilt toegang krijgen tot een share en de inhoud ervan, moet u een Azure File storage-client gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-135">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```cpp
// Create the Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="f3ebb-136">U kunt vervolgens een een verwijzing naar een share ophalen met behulp van de Azure File storage-client.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-136">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```cpp
// Get a reference to the file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="f3ebb-137">Gebruik voor het maken van de share de **create_if_not_exists** methode van de **cloud_file_share** object.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-137">To create the share, use the **create_if_not_exists** method of the **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="f3ebb-138">Op dit moment **delen** bevat een verwijzing naar een share met de naam **mijn-voorbeeld-share**.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-138">At this point, **share** holds a reference to a share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="f3ebb-139">Verwijderen van een Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="f3ebb-139">Delete an Azure File share</span></span>
<span data-ttu-id="f3ebb-140">Verwijderen van een share wordt gedaan door het aanroepen van de **delete_if_exists** methode voor het object cloud_file_share.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-140">Deleting a share is done by calling the **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="f3ebb-141">Hier volgt voorbeeldcode die dat doet.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete the share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="f3ebb-142">Een map maken</span><span class="sxs-lookup"><span data-stu-id="f3ebb-142">Create a directory</span></span>
<span data-ttu-id="f3ebb-143">U kunt opslag indelen door de gegevens van de bestanden in submappen in plaats van ze allemaal in de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-143">You can organize storage by putting files inside subdirectories instead of having all of them in the root directory.</span></span> <span data-ttu-id="f3ebb-144">Azure File storage kunt u zoveel mappen als uw account kunt maken.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-144">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="f3ebb-145">De code hieronder maakt u een map met de naam **mijn-voorbeeld-directory** onder de hoofdmap, evenals een submap met de naam **mijn-voorbeeld-submap**.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-145">The code below will create a directory named **my-sample-directory** under the root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference to a directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if the share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="f3ebb-146">Een map verwijderen</span><span class="sxs-lookup"><span data-stu-id="f3ebb-146">Delete a directory</span></span>
<span data-ttu-id="f3ebb-147">Als u een map is een eenvoudige taak, maar houd er rekening mee dat u een map met nog steeds bestanden of andere mappen niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference to the directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference to the subdirectory you want to delete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete the subdirectory and the sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="f3ebb-148">Bestanden en mappen in een Azure-bestandsshare opsommen</span><span class="sxs-lookup"><span data-stu-id="f3ebb-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="f3ebb-149">Eenvoudig het verkrijgen van een lijst met bestanden en mappen in een share wordt gedaan door het aanroepen van **list_files_and_directories** op een **cloud_file_directory** verwijzing.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="f3ebb-150">Voor toegang tot de uitgebreide set eigenschappen en methoden voor een geretourneerde **list_file_and_directory_item**, belt u het **list_file_and_directory_item.as_file** methode voor het ophalen van een **cloud_file**  object, of de **list_file_and_directory_item.as_directory** methode voor het ophalen van een **cloud_file_directory** object.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-150">To access the rich set of properties and methods for a returned **list_file_and_directory_item**, you must call the **list_file_and_directory_item.as_file** method to get a **cloud_file** object, or the **list_file_and_directory_item.as_directory** method to get a **cloud_file_directory** object.</span></span>

<span data-ttu-id="f3ebb-151">De volgende code laat zien hoe ophalen en de uitvoer van de URI van elk item in de hoofdmap van de share.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-151">The following code demonstrates how to retrieve and output the URI of each item in the root directory of the share.</span></span>

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a><span data-ttu-id="f3ebb-152">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="f3ebb-152">Upload a file</span></span>
<span data-ttu-id="f3ebb-153">Op de minst bevat een bestandsshare in Azure een hoofdmap waarin de bestanden kunnen zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-153">At the very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="f3ebb-154">In deze sectie leert u hoe een bestand van de lokale opslag naar de hoofdmap van een share te uploaden.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-154">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="f3ebb-155">De eerste stap bij het uploaden van een bestand is te halen van een verwijzing naar de map waarin dit zich moet bevinden.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-155">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="f3ebb-156">U doet dit door de **get_root_directory_reference** methode van de shareobject.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-156">You do this by calling the **get_root_directory_reference** method of the share object.</span></span>

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="f3ebb-157">Nu dat u een verwijzing naar de hoofdmap van de share hebt, kunt u een bestand op deze uploaden.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-157">Now that you have a reference to the root directory of the share, you can upload a file onto it.</span></span> <span data-ttu-id="f3ebb-158">In dit voorbeeld bestandsuploads uit een bestand, tekst en een stroom.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-158">This example uploads from a file, from text, and from a stream.</span></span>

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a><span data-ttu-id="f3ebb-159">Bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="f3ebb-159">Download a file</span></span>
<span data-ttu-id="f3ebb-160">Om bestanden te downloaden, eerst ophalen van een bestandsverwijzing en roept u vervolgens de **download_to_stream** methode inhoud van het bestand overdragen naar een stroomobject dat u vervolgens blijven in een lokaal bestand behouden kunt.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-160">To download files, first retrieve a file reference and then call the **download_to_stream** method to transfer the file contents to a stream object, which you can then persist to a local file.</span></span> <span data-ttu-id="f3ebb-161">U kunt ook de **download_to_file** methode voor het downloaden van de inhoud van een bestand naar een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-161">Alternatively, you can use the **download_to_file** method to download the contents of a file to a local file.</span></span> <span data-ttu-id="f3ebb-162">U kunt de **download_text** methode voor het downloaden van de inhoud van een bestand op als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-162">You can use the **download_text** method to download the contents of a file as a text string.</span></span>

<span data-ttu-id="f3ebb-163">Het volgende voorbeeld wordt de **download_to_stream** en **download_text** methoden voor het demonstreren van downloaden van de bestanden die zijn gemaakt in de vorige secties.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-163">The following example uses the **download_to_stream** and **download_text** methods to demonstrate downloading the files, which were created in previous sections.</span></span>

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a><span data-ttu-id="f3ebb-164">Een bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="f3ebb-164">Delete a file</span></span>
<span data-ttu-id="f3ebb-165">Een andere algemene Azure File storage-bewerking wordt verwijderen van bestanden.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="f3ebb-166">De volgende code verwijdert een bestand met de naam my-voorbeeld-bestand-3 opgeslagen onder de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-166">The following code deletes a file named my-sample-file-3 stored under the root directory.</span></span>

```cpp
// Get a reference to the root directory for the share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-the-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="f3ebb-167">Stel een quotum (maximumgrootte) voor een Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="f3ebb-167">Set the quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="f3ebb-168">U kunt het quotum (of de maximale grootte) instellen voor een bestandsshare, in gigabytes.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-168">You can set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="f3ebb-169">U kunt ook controleren hoeveel gegevens er momenteel zijn opgeslagen in de share.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-169">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="f3ebb-170">Door het quotum voor een share in te stellen, kunt u de totale grootte instellen van de bestanden die zijn opgeslagen in de share.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-170">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="f3ebb-171">Als de totale grootte van de bestanden in de share het quotum voor de share overschrijdt, kunnen clients bestaande bestanden niet meer vergroten en geen nieuwe bestanden meer maken, tenzij deze bestanden leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-171">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="f3ebb-172">In onderstaand voorbeeld ziet u hoe u het huidige gebruik voor een share controleert en een quotum voor de share instelt.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-172">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets the quota to 2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="f3ebb-173">Een Shared Access Signature genereren voor een bestand of bestandsshare</span><span class="sxs-lookup"><span data-stu-id="f3ebb-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="f3ebb-174">U kunt een shared access signature (SAS) voor een bestandsshare of voor een afzonderlijk bestand genereren.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="f3ebb-175">U kunt op een bestandsshare ook een beleid voor gedeelde toegang maken om handtekeningen voor gedeelde toegang te beheren.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-175">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="f3ebb-176">Het maken van een beleid voor gedeelde toegang wordt aanbevolen omdat dit een manier biedt om de SAS in te trekken als deze verdacht is.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-176">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="f3ebb-177">In het volgende voorbeeld wordt een beleid voor gedeelde toegang gemaakt op een share en wordt dat beleid vervolgens gebruikt om de beperkingen te verstrekken voor een SAS voor een bestand in de share.</span><span class="sxs-lookup"><span data-stu-id="f3ebb-177">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client and get a reference to the share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions to expire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for the share
    azure::storage::file_share_permissions permissions;    

    //retrieve the current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add the new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save the updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve the root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in the share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from the SAS, and write some text to the file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="f3ebb-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f3ebb-178">Next steps</span></span>
<span data-ttu-id="f3ebb-179">Zie de volgende bronnen voor meer informatie over Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="f3ebb-179">To learn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="f3ebb-180">Opslagclientbibliotheek voor C++</span><span class="sxs-lookup"><span data-stu-id="f3ebb-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="f3ebb-181">[Azure Storage-Service bestandsvoorbeelden in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="f3ebb-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="f3ebb-182">Azure-opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="f3ebb-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="f3ebb-183">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f3ebb-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)