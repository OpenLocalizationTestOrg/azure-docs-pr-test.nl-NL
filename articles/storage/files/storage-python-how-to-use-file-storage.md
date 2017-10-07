---
title: aaaDevelop voor Azure File storage met behulp van Python | Microsoft Docs
description: Meer informatie over hoe toodevelop Python toepassingen en services die gebruikmaken van Azure File storage toostore bestandsgegevens.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 2adc5aac2765b98a8022ab1f706c1fcdbca1b43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="12833-103">Ontwikkelen voor Azure File storage met behulp van Python</span><span class="sxs-lookup"><span data-stu-id="12833-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="12833-104">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="12833-104">About this tutorial</span></span>
<span data-ttu-id="12833-105">Deze zelfstudie wordt gedemonstreerd Hallo grondbeginselen van het gebruik van Python toodevelop toepassingen of services die gebruikmaken van Azure File storage toostore bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="12833-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="12833-106">In deze zelfstudie wordt een eenvoudige consoletoepassing maken en weergeven hoe tooperform basisbewerkingen uitvoeren met Python en Azure File storage:</span><span class="sxs-lookup"><span data-stu-id="12833-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="12833-107">Azure-bestandsshares maken</span><span class="sxs-lookup"><span data-stu-id="12833-107">Create Azure File shares</span></span>
* <span data-ttu-id="12833-108">Mappen maken</span><span class="sxs-lookup"><span data-stu-id="12833-108">Create directories</span></span>
* <span data-ttu-id="12833-109">Bestanden en mappen in een Azure-bestandsshare opsommen</span><span class="sxs-lookup"><span data-stu-id="12833-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="12833-110">Uploaden, downloaden en een bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="12833-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="12833-111">Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk toowrite eenvoudige toepassingen die toegang hebben tot hello Azure bestandsshare met behulp van Hallo standaard Python i/o-klassen en -functies.</span><span class="sxs-lookup"><span data-stu-id="12833-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="12833-112">In dit artikel wordt beschreven hoe toowrite toepassingen die gebruikmaken van Azure Storage Python SDK, die gebruikmaakt van Hallo Hallo [Azure File storage REST-API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span><span class="sxs-lookup"><span data-stu-id="12833-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="12833-113">Instellen van uw toepassing toouse Azure File storage</span><span class="sxs-lookup"><span data-stu-id="12833-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="12833-114">De volgende Hallo aan de bovenkant Hallo van een Python-bronbestand waarin u tooprogrammatically toegang tot Azure Storage wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="12833-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="12833-115">Instellen van een verbinding tooAzure File storage</span><span class="sxs-lookup"><span data-stu-id="12833-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="12833-116">Hallo `FileService` object kunt u samenwerken met shares, mappen en bestanden.</span><span class="sxs-lookup"><span data-stu-id="12833-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="12833-117">Hallo volgende code maakt een `FileService` object met behulp van Hallo naam en opslagaccountsleutel.</span><span class="sxs-lookup"><span data-stu-id="12833-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="12833-118">Vervang `<myaccount>` en `<mykey>` met uw accountnaam en de sleutel.</span><span class="sxs-lookup"><span data-stu-id="12833-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="12833-119">Een Azure-bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="12833-119">Create an Azure File share</span></span>
<span data-ttu-id="12833-120">In de Hallo volgende codevoorbeeld, kunt u een `FileService` object toocreate Hallo share als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="12833-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="12833-121">Een map maken</span><span class="sxs-lookup"><span data-stu-id="12833-121">Create a directory</span></span>
<span data-ttu-id="12833-122">U kunt ook opslag door de gegevens van de bestanden in submappen in plaats van ze allemaal in de hoofdmap Hallo indelen.</span><span class="sxs-lookup"><span data-stu-id="12833-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="12833-123">Azure File storage, kunt u toocreate veel mappen als uw account wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="12833-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="12833-124">Hallo-code hieronder maakt u een onderliggende map met de naam **sampledir** onder Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="12833-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="12833-125">Bestanden en mappen in een Azure-bestandsshare opsommen</span><span class="sxs-lookup"><span data-stu-id="12833-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="12833-126">toolist hello bestanden en mappen in een share gebruiken Hallo **lijst\_mappen\_en\_bestanden** methode.</span><span class="sxs-lookup"><span data-stu-id="12833-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="12833-127">Deze methode retourneert een generator.</span><span class="sxs-lookup"><span data-stu-id="12833-127">This method returns a generator.</span></span> <span data-ttu-id="12833-128">Hallo volgende code levert Hallo **naam** van elk bestand en de map in een share toohello-console.</span><span class="sxs-lookup"><span data-stu-id="12833-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="12833-129">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="12833-129">Upload a file</span></span> 
<span data-ttu-id="12833-130">Azure File share op Hallo zeer minste bevat, een hoofdmap waarin de bestanden kunnen zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="12833-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="12833-131">In deze sectie leert u hoe een bestand van de lokale opslag op Hallo tooupload de hoofdmap van een share.</span><span class="sxs-lookup"><span data-stu-id="12833-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="12833-132">toocreate een bestand en het van uploadgegevens, gebruikt u Hallo `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` of `create_file_from_text` methoden.</span><span class="sxs-lookup"><span data-stu-id="12833-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="12833-133">Op hoog niveau van de methoden die Hallo nodig verdeling in segmenten uitvoeren wanneer Hallo Hallo gegevens groter zijn dan 64 MB zijn.</span><span class="sxs-lookup"><span data-stu-id="12833-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="12833-134">`create_file_from_path`uploads Hallo inhoud van een bestand uit Hallo opgegeven pad en `create_file_from_stream` uploads Hallo inhoud uit een al geopend bestandsstroom.</span><span class="sxs-lookup"><span data-stu-id="12833-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="12833-135">`create_file_from_bytes`een matrix met bytes, uploadt en `create_file_from_text` uploads Hallo opgegeven tekstwaarde met Hallo opgegeven codering (standaardwaarden tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="12833-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="12833-136">Hallo volgende voorbeeld wordt geüpload Hallo inhoud Hallo **sunset.png** -bestand in Hallo **mijnbestand** bestand.</span><span class="sxs-lookup"><span data-stu-id="12833-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="12833-137">Bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="12833-137">Download a file</span></span>
<span data-ttu-id="12833-138">gegevens uit een bestand toodownload gebruiken `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, of `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="12833-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="12833-139">Op hoog niveau van de methoden die Hallo nodig verdeling in segmenten uitvoeren wanneer Hallo Hallo gegevens groter zijn dan 64 MB zijn.</span><span class="sxs-lookup"><span data-stu-id="12833-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="12833-140">Hallo volgende voorbeeld worden `get_file_to_path` toodownload Hallo inhoud Hallo **mijnbestand** -bestand en sla het toohello **out sunset.png** bestand.</span><span class="sxs-lookup"><span data-stu-id="12833-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="12833-141">Een bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="12833-141">Delete a file</span></span>
<span data-ttu-id="12833-142">Tenslotte toodelete een bestand, roept `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="12833-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="12833-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12833-143">Next steps</span></span>
<span data-ttu-id="12833-144">Nu dat u hebt geleerd hoe toomanipulate Azure File storage met behulp van Python, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="12833-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="12833-145">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="12833-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="12833-146">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="12833-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="12833-147">Microsoft Azure-opslag-SDK voor Python</span><span class="sxs-lookup"><span data-stu-id="12833-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)