---
title: aaaDevelop voor Azure File storage met C++ | Microsoft Docs
description: Meer informatie over hoe toodevelop C++-toepassingen en services die gebruikmaken van Azure File storage toostore bestandsgegevens.
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
ms.openlocfilehash: 48f668cf9359f88baeaaa08ee0d44e70bd0f5f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="19781-103">Ontwikkelen voor Azure File storage met C++</span><span class="sxs-lookup"><span data-stu-id="19781-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="19781-104">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="19781-104">About this tutorial</span></span>

<span data-ttu-id="19781-105">In deze zelfstudie leert u hoe tooperform basisbewerkingen op Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="19781-105">In this tutorial, you'll learn how tooperform basic operations on Azure File storage.</span></span> <span data-ttu-id="19781-106">Door steekproeven geschreven in C++, leert u hoe toocreate deelt en mappen, uploaden, weergeven en verwijderen van bestanden.</span><span class="sxs-lookup"><span data-stu-id="19781-106">Through samples written in C++, you'll learn how toocreate shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="19781-107">Als u nieuwe tooAzure File storage, wordt gaan via Hallo concepten Hallo die in volgende secties nuttig zijn Hallo voorbeelden begrijpen.</span><span class="sxs-lookup"><span data-stu-id="19781-107">If you are new tooAzure File storage , going through hello concepts in hello sections that follow will be helpful in understanding hello samples.</span></span>


* <span data-ttu-id="19781-108">Maken en verwijderen van de Azure-bestandsshares</span><span class="sxs-lookup"><span data-stu-id="19781-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="19781-109">Maken en verwijderen van mappen</span><span class="sxs-lookup"><span data-stu-id="19781-109">Create and delete directories</span></span>
* <span data-ttu-id="19781-110">Bestanden en mappen in een Azure-bestandsshare opsommen</span><span class="sxs-lookup"><span data-stu-id="19781-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="19781-111">Uploaden, downloaden en een bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="19781-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="19781-112">Hallo quotum (maximumgrootte) voor een Azure-bestandsshare instellen</span><span class="sxs-lookup"><span data-stu-id="19781-112">Set hello quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="19781-113">Maak een shared access signature (SAS-sleutel) voor een bestand dat gebruikmaakt van een gedeeld toegangsbeleid dat is gedefinieerd op Hallo-share.</span><span class="sxs-lookup"><span data-stu-id="19781-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>

> [!Note]  
> <span data-ttu-id="19781-114">Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk toowrite eenvoudige toepassingen die toegang hebben tot hello Azure bestandsshare met behulp van Hallo standard C++ i/o-klassen en -functies.</span><span class="sxs-lookup"><span data-stu-id="19781-114">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard C++ I/O classes and functions.</span></span> <span data-ttu-id="19781-115">In dit artikel wordt beschreven hoe toowrite toepassingen die gebruikmaken van Azure Storage C++ SDK, die gebruikmaakt van Hallo Hallo [Azure File storage REST-API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span><span class="sxs-lookup"><span data-stu-id="19781-115">This article will describe how toowrite applications that use hello Azure Storage C++ SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="19781-116">Een C++-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="19781-116">Create a C++ application</span></span>
<span data-ttu-id="19781-117">Voorbeelden van toobuild hello, moet u tooinstall hello Azure Storage-clientbibliotheek 2.4.0 voor C++.</span><span class="sxs-lookup"><span data-stu-id="19781-117">toobuild hello samples, you will need tooinstall hello Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="19781-118">U moet hebt een Azure storage-account ook gemaakt.</span><span class="sxs-lookup"><span data-stu-id="19781-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="19781-119">tooinstall hello Azure Storage Client 2.4.0 voor C++, kunt u een van de volgende methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="19781-119">tooinstall hello Azure Storage Client 2.4.0 for C++, you can use one of hello following methods:</span></span>

* <span data-ttu-id="19781-120">**Linux:** Hallo instructies gegeven in Hallo [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="19781-120">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="19781-121">**Windows:** In Visual Studio, klikt u op **extra &gt; NuGet Package Manager &gt; Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="19781-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="19781-122">Type Hallo volgende opdracht in Hallo [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="19781-122">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="19781-123">Instellen van uw toepassing toouse Azure File storage</span><span class="sxs-lookup"><span data-stu-id="19781-123">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="19781-124">Toegevoegd volgende Hallo bevatten instructies toohello bovenaan Hallo C++-bronbestand waar u toomanipulate Azure File storage:</span><span class="sxs-lookup"><span data-stu-id="19781-124">Add hello following include statements toohello top of hello C++ source file where you want toomanipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="19781-125">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="19781-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="19781-126">toouse opslag van bestanden, moet u tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="19781-126">toouse File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="19781-127">Hallo eerste stap zou zijn tooconfigure een verbindingsreeks, we gebruiken tooconnect tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="19781-127">hello first step would be tooconfigure a connection string, which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="19781-128">We gaan een statische variabele toodo definiëren die.</span><span class="sxs-lookup"><span data-stu-id="19781-128">Let's define a static variable toodo that.</span></span>

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="19781-129">Verbinding maken met tooan Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="19781-129">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="19781-130">U kunt Hallo **cloud_storage_account** klasse toorepresent uw Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="19781-130">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="19781-131">tooretrieve uw opslag accountgegevens van de opslagverbindingsreeks hello, kunt u Hallo **parseren** methode.</span><span class="sxs-lookup"><span data-stu-id="19781-131">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="19781-132">Een Azure-bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="19781-132">Create an Azure File share</span></span>
<span data-ttu-id="19781-133">Alle bestanden en mappen in Azure File storage bevinden zich in een zogenaamd een **Share**.</span><span class="sxs-lookup"><span data-stu-id="19781-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="19781-134">Uw storage-account kan als veel shares als de capaciteit van uw account kunt hebben.</span><span class="sxs-lookup"><span data-stu-id="19781-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="19781-135">tooobtain toegang tooa share en de inhoud ervan, moet u een Azure File storage client toouse.</span><span class="sxs-lookup"><span data-stu-id="19781-135">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="19781-136">U kunt vervolgens een verwijzing tooa share verkrijgen met behulp van hello Azure File storage client.</span><span class="sxs-lookup"><span data-stu-id="19781-136">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="19781-137">Gebruik Hallo-share Hallo toocreate **create_if_not_exists** methode Hallo **cloud_file_share** object.</span><span class="sxs-lookup"><span data-stu-id="19781-137">toocreate hello share, use hello **create_if_not_exists** method of hello **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="19781-138">Op dit moment **delen** bevat een verwijzing tooa share met de naam **mijn-voorbeeld-share**.</span><span class="sxs-lookup"><span data-stu-id="19781-138">At this point, **share** holds a reference tooa share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="19781-139">Verwijderen van een Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="19781-139">Delete an Azure File share</span></span>
<span data-ttu-id="19781-140">Verwijderen van een share wordt uitgevoerd door de aanroepende Hallo **delete_if_exists** methode voor het object cloud_file_share.</span><span class="sxs-lookup"><span data-stu-id="19781-140">Deleting a share is done by calling hello **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="19781-141">Hier volgt voorbeeldcode die dat doet.</span><span class="sxs-lookup"><span data-stu-id="19781-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="19781-142">Een map maken</span><span class="sxs-lookup"><span data-stu-id="19781-142">Create a directory</span></span>
<span data-ttu-id="19781-143">U kunt opslag indelen door de bestanden in submappen in plaats van ze allemaal in de hoofdmap Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="19781-143">You can organize storage by putting files inside subdirectories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="19781-144">Azure File storage, kunt u toocreate veel mappen als uw account wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="19781-144">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="19781-145">Hallo-code hieronder maakt u een map met de naam **mijn-voorbeeld-directory** onder de hoofdmap hello, evenals een submap met de naam **mijn-voorbeeld-submap**.</span><span class="sxs-lookup"><span data-stu-id="19781-145">hello code below will create a directory named **my-sample-directory** under hello root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="19781-146">Een map verwijderen</span><span class="sxs-lookup"><span data-stu-id="19781-146">Delete a directory</span></span>
<span data-ttu-id="19781-147">Als u een map is een eenvoudige taak, maar houd er rekening mee dat u een map met nog steeds bestanden of andere mappen niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="19781-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="19781-148">Bestanden en mappen in een Azure-bestandsshare opsommen</span><span class="sxs-lookup"><span data-stu-id="19781-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="19781-149">Eenvoudig het verkrijgen van een lijst met bestanden en mappen in een share wordt gedaan door het aanroepen van **list_files_and_directories** op een **cloud_file_directory** verwijzing.</span><span class="sxs-lookup"><span data-stu-id="19781-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="19781-150">tooaccess Hallo uitgebreide set eigenschappen en methoden voor een geretourneerde **list_file_and_directory_item**, moet u Hallo aanroepen **list_file_and_directory_item.as_file** methode tooget een **cloud_ bestand** object of Hallo **list_file_and_directory_item.as_directory** methode tooget een **cloud_file_directory** object.</span><span class="sxs-lookup"><span data-stu-id="19781-150">tooaccess hello rich set of properties and methods for a returned **list_file_and_directory_item**, you must call hello **list_file_and_directory_item.as_file** method tooget a **cloud_file** object, or hello **list_file_and_directory_item.as_directory** method tooget a **cloud_file_directory** object.</span></span>

<span data-ttu-id="19781-151">Hallo volgende code laat zien hoe tooretrieve en uitvoer Hallo URI van elk item in de hoofdmap Hallo Hallo-share.</span><span class="sxs-lookup"><span data-stu-id="19781-151">hello following code demonstrates how tooretrieve and output hello URI of each item in hello root directory of hello share.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
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

## <a name="upload-a-file"></a><span data-ttu-id="19781-152">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="19781-152">Upload a file</span></span>
<span data-ttu-id="19781-153">Op Hallo zeer minste, bevat een Azure-bestandsshare de hoofdmap waarin de bestanden kunnen zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="19781-153">At hello very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="19781-154">In deze sectie leert u hoe een bestand van de lokale opslag op Hallo tooupload de hoofdmap van een share.</span><span class="sxs-lookup"><span data-stu-id="19781-154">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="19781-155">Hallo eerste stap bij het uploaden van een bestand is tooobtain een verwijzing toohello map waarin dit zich moet bevinden.</span><span class="sxs-lookup"><span data-stu-id="19781-155">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="19781-156">Dit doet u door de aanroepende Hallo **get_root_directory_reference** methode van Hallo share-object.</span><span class="sxs-lookup"><span data-stu-id="19781-156">You do this by calling hello **get_root_directory_reference** method of hello share object.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="19781-157">Nu dat u de hoofdmap van een verwijzing toohello van Hallo-share hebt, kunt u een bestand op deze uploaden.</span><span class="sxs-lookup"><span data-stu-id="19781-157">Now that you have a reference toohello root directory of hello share, you can upload a file onto it.</span></span> <span data-ttu-id="19781-158">In dit voorbeeld bestandsuploads uit een bestand, tekst en een stroom.</span><span class="sxs-lookup"><span data-stu-id="19781-158">This example uploads from a file, from text, and from a stream.</span></span>

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

## <a name="download-a-file"></a><span data-ttu-id="19781-159">Bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="19781-159">Download a file</span></span>
<span data-ttu-id="19781-160">toodownload bestanden, eerst ophalen van een bestandsverwijzing en vervolgens aanroepen Hallo **download_to_stream** methode tootransfer Hallo bestand inhoud tooa stream-object, dat u vervolgens kunt blijven behouden tooa lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="19781-160">toodownload files, first retrieve a file reference and then call hello **download_to_stream** method tootransfer hello file contents tooa stream object, which you can then persist tooa local file.</span></span> <span data-ttu-id="19781-161">U kunt ook hello gebruiken **download_to_file** methode toodownload Hallo inhoud van een lokaal bestand tooa-bestand.</span><span class="sxs-lookup"><span data-stu-id="19781-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a file tooa local file.</span></span> <span data-ttu-id="19781-162">U kunt Hallo **download_text** methode toodownload Hallo inhoud van een bestand als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="19781-162">You can use hello **download_text** method toodownload hello contents of a file as a text string.</span></span>

<span data-ttu-id="19781-163">Hallo volgende voorbeeld wordt Hallo **download_to_stream** en **download_text** methoden toodemonstrate Hallo-bestanden die zijn gemaakt in de vorige secties downloaden.</span><span class="sxs-lookup"><span data-stu-id="19781-163">hello following example uses hello **download_to_stream** and **download_text** methods toodemonstrate downloading hello files, which were created in previous sections.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="19781-164">Een bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="19781-164">Delete a file</span></span>
<span data-ttu-id="19781-165">Een andere algemene Azure File storage-bewerking wordt verwijderen van bestanden.</span><span class="sxs-lookup"><span data-stu-id="19781-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="19781-166">Hallo verwijdert volgende code een bestand met de naam my-voorbeeld-bestand-3 opgeslagen onder Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="19781-166">hello following code deletes a file named my-sample-file-3 stored under hello root directory.</span></span>

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="19781-167">Hallo quotum (maximumgrootte) voor een Azure-bestandsshare instellen</span><span class="sxs-lookup"><span data-stu-id="19781-167">Set hello quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="19781-168">U kunt Hallo quotum (of de maximale grootte) instellen voor een bestandsshare, in gigabytes.</span><span class="sxs-lookup"><span data-stu-id="19781-168">You can set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="19781-169">U kunt ook controleren hoeveel gegevens er momenteel zijn opgeslagen op Hallo share toosee.</span><span class="sxs-lookup"><span data-stu-id="19781-169">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="19781-170">Door de instelling Hallo quotum voor een share, kunt u Hallo totale grootte van bestanden op Hallo share Hallo beperken.</span><span class="sxs-lookup"><span data-stu-id="19781-170">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="19781-171">Als Hallo totale grootte van bestanden op Hallo share overschrijdt Hallo quota ingesteld voor de share Hallo en clients worden niet kan tooincrease Hallo grootte van de bestaande bestanden of nieuwe bestanden maken, tenzij deze bestanden leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="19781-171">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="19781-172">Hallo voorbeeld hieronder ziet u hoe toocheck huidige gebruik voor een share Hallo en hoe tooset quotum voor de share Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="19781-172">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="19781-173">Een Shared Access Signature genereren voor een bestand of bestandsshare</span><span class="sxs-lookup"><span data-stu-id="19781-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="19781-174">U kunt een shared access signature (SAS) voor een bestandsshare of voor een afzonderlijk bestand genereren.</span><span class="sxs-lookup"><span data-stu-id="19781-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="19781-175">U kunt ook een gedeeld toegangsbeleid op een bestandsshare-toomanage gedeelde toegang handtekeningen maken.</span><span class="sxs-lookup"><span data-stu-id="19781-175">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="19781-176">Maken van een gedeeld toegangsbeleid wordt aanbevolen, aangezien deze een manier om Hallo SAS intrekken biedt als deze verdacht.</span><span class="sxs-lookup"><span data-stu-id="19781-176">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="19781-177">Hallo volgende voorbeeld wordt een beleid voor gedeelde toegang gemaakt op een bestandsshare op en gebruikt u vervolgens dat tooprovide Hallo beleidsbeperkingen voor een SAS voor een bestand in Hallo delen.</span><span class="sxs-lookup"><span data-stu-id="19781-177">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
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

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="19781-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19781-178">Next steps</span></span>
<span data-ttu-id="19781-179">toolearn meer informatie over Azure Storage, bekijk deze resources:</span><span class="sxs-lookup"><span data-stu-id="19781-179">toolearn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="19781-180">Opslagclientbibliotheek voor C++</span><span class="sxs-lookup"><span data-stu-id="19781-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="19781-181">[Azure Storage-Service bestandsvoorbeelden in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="19781-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="19781-182">Azure-opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="19781-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="19781-183">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="19781-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)