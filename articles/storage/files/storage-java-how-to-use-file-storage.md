---
title: aaaDevelop voor Azure File storage met behulp van Java | Microsoft Docs
description: Meer informatie over hoe toodevelop Java-toepassingen en services die gebruikmaken van Azure File storage toostore bestandsgegevens.
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: be71a946604da8af0130f101f2eb6135c5e08abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="a1b54-103">Ontwikkelen voor Azure File storage met Java</span><span class="sxs-lookup"><span data-stu-id="a1b54-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="a1b54-104">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="a1b54-104">About this tutorial</span></span>
<span data-ttu-id="a1b54-105">Deze zelfstudie wordt gedemonstreerd Hallo grondbeginselen van het gebruik van Java-toodevelop toepassingen of services die gebruikmaken van Azure File storage toostore bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="a1b54-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="a1b54-106">In deze zelfstudie wordt een eenvoudige consoletoepassing maken en weergeven hoe tooperform basisbewerkingen uitvoeren met Java en Azure File storage:</span><span class="sxs-lookup"><span data-stu-id="a1b54-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="a1b54-107">Maken en verwijderen van de Azure-bestandsshares</span><span class="sxs-lookup"><span data-stu-id="a1b54-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="a1b54-108">Maken en verwijderen van mappen</span><span class="sxs-lookup"><span data-stu-id="a1b54-108">Create and delete directories</span></span>
* <span data-ttu-id="a1b54-109">Bestanden en mappen in een Azure-bestandsshare opsommen</span><span class="sxs-lookup"><span data-stu-id="a1b54-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="a1b54-110">Uploaden, downloaden en een bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="a1b54-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="a1b54-111">Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk toowrite eenvoudige toepassingen die toegang hebben tot hello Azure bestandsshare met behulp van Hallo standaard Java i/o-klassen.</span><span class="sxs-lookup"><span data-stu-id="a1b54-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="a1b54-112">In dit artikel wordt beschreven hoe toowrite toepassingen die gebruikmaken van Azure Storage Java SDK, die gebruikmaakt van Hallo Hallo [Azure File storage REST-API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span><span class="sxs-lookup"><span data-stu-id="a1b54-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="a1b54-113">Een Java-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="a1b54-113">Create a Java application</span></span>
<span data-ttu-id="a1b54-114">Voorbeelden van toobuild hello, moet u Hallo Java Development Kit (JDK) en Hallo [Azure-opslag-SDK voor Java] [].</span><span class="sxs-lookup"><span data-stu-id="a1b54-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="a1b54-115">U moet hebt een Azure storage-account ook gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a1b54-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="a1b54-116">Instellen van uw toepassing toouse Azure File storage</span><span class="sxs-lookup"><span data-stu-id="a1b54-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="a1b54-117">toouse hello Azure storage-API's, toevoegen Hallo instructie toohello boven in Hallo Java-bestand waarin u van plan bent tooaccess Hallo storage-service uit te volgen.</span><span class="sxs-lookup"><span data-stu-id="a1b54-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="a1b54-118">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="a1b54-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="a1b54-119">Azure File storage toouse, moet u tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="a1b54-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="a1b54-120">Hallo eerste stap zou zijn tooconfigure een verbindingsreeks die we gebruiken tooconnect tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="a1b54-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="a1b54-121">We gaan een statische variabele toodo definiëren die.</span><span class="sxs-lookup"><span data-stu-id="a1b54-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="a1b54-122">Your_storage_account_name en your_storage_account_key vervangen door feitelijke waarden Hallo voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="a1b54-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="a1b54-123">Verbinding maken met tooan Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="a1b54-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="a1b54-124">tooconnect tooyour storage-account, moet u toouse hello **CloudStorageAccount** -object doorgeven van een tekenreeks verbinding tooits **parseren** methode.</span><span class="sxs-lookup"><span data-stu-id="a1b54-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="a1b54-125">**CloudStorageAccount.parse** er wordt een InvalidKeyException dus u tooput moet in een trycatch blokkeren.</span><span class="sxs-lookup"><span data-stu-id="a1b54-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="a1b54-126">Een Azure-bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="a1b54-126">Create an Azure File share</span></span>
<span data-ttu-id="a1b54-127">Alle bestanden en mappen in Azure File storage bevinden zich in een zogenaamd een **Share**.</span><span class="sxs-lookup"><span data-stu-id="a1b54-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="a1b54-128">Uw storage-account kan net zoveel shares als de capaciteit van uw account kunt hebben.</span><span class="sxs-lookup"><span data-stu-id="a1b54-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="a1b54-129">tooobtain toegang tooa share en de inhoud ervan, moet u een Azure File storage client toouse.</span><span class="sxs-lookup"><span data-stu-id="a1b54-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="a1b54-130">U kunt vervolgens een verwijzing tooa share verkrijgen met behulp van hello Azure File storage client.</span><span class="sxs-lookup"><span data-stu-id="a1b54-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="a1b54-131">tooactually hello share maken, gebruikt u Hallo **createIfNotExists** methode van Hallo CloudFileShare-object.</span><span class="sxs-lookup"><span data-stu-id="a1b54-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="a1b54-132">Op dit moment **delen** bevat een verwijzing tooa share met de naam **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="a1b54-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="a1b54-133">Verwijderen van een Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="a1b54-133">Delete an Azure File share</span></span>
<span data-ttu-id="a1b54-134">Verwijderen van een share wordt uitgevoerd door de aanroepende Hallo **deleteIfExists** methode voor het object CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="a1b54-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="a1b54-135">Hier volgt voorbeeldcode die dat doet.</span><span class="sxs-lookup"><span data-stu-id="a1b54-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="a1b54-136">Een map maken</span><span class="sxs-lookup"><span data-stu-id="a1b54-136">Create a directory</span></span>
<span data-ttu-id="a1b54-137">U kunt ook opslag door de gegevens van de bestanden in submappen in plaats van ze allemaal in de hoofdmap Hallo indelen.</span><span class="sxs-lookup"><span data-stu-id="a1b54-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="a1b54-138">Azure File storage, kunt u toocreate veel mappen als uw account wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="a1b54-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="a1b54-139">Hallo-code hieronder maakt u een onderliggende map met de naam **sampledir** onder Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="a1b54-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="a1b54-140">Een map verwijderen</span><span class="sxs-lookup"><span data-stu-id="a1b54-140">Delete a directory</span></span>
<span data-ttu-id="a1b54-141">Als u een map is een redelijk eenvoudig taak, maar houd er rekening mee dat u een map met nog steeds bestanden of andere mappen niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a1b54-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="a1b54-142">Bestanden en mappen in een Azure-bestandsshare opsommen</span><span class="sxs-lookup"><span data-stu-id="a1b54-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="a1b54-143">Eenvoudig het verkrijgen van een lijst met bestanden en mappen in een share wordt gedaan door het aanroepen van **listFilesAndDirectories** op een CloudFileDirectory-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="a1b54-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="a1b54-144">Hallo-methode retourneert een lijst met ListFileItem-objecten die u kunt herhalen.</span><span class="sxs-lookup"><span data-stu-id="a1b54-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="a1b54-145">Als u bijvoorbeeld hello volgende code wordt een lijst bestanden en mappen in de hoofdmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="a1b54-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="a1b54-146">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="a1b54-146">Upload a file</span></span>
<span data-ttu-id="a1b54-147">Een Azure-File share op Hallo zeer minste bevat, een hoofdmap waarin de bestanden kunnen zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="a1b54-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="a1b54-148">In deze sectie leert u hoe een bestand van de lokale opslag op Hallo tooupload de hoofdmap van een share.</span><span class="sxs-lookup"><span data-stu-id="a1b54-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="a1b54-149">Hallo eerste stap bij het uploaden van een bestand is tooobtain een verwijzing toohello map waarin dit zich moet bevinden.</span><span class="sxs-lookup"><span data-stu-id="a1b54-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="a1b54-150">Dit doet u door de aanroepende Hallo **getRootDirectoryReference** methode van Hallo share-object.</span><span class="sxs-lookup"><span data-stu-id="a1b54-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="a1b54-151">Nu dat u de hoofdmap van een verwijzing toohello van Hallo-share hebt, kunt u een bestand op met behulp van de volgende code Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="a1b54-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="a1b54-152">Bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="a1b54-152">Download a file</span></span>
<span data-ttu-id="a1b54-153">Een van de Hallo frequentere bewerkingen die u op basis van Azure File storage uitvoeren wilt is toodownload bestanden.</span><span class="sxs-lookup"><span data-stu-id="a1b54-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="a1b54-154">In Hallo voorbeeld te volgen, Hallo code SampleFile.txt gedownload en wordt de inhoud weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a1b54-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="a1b54-155">Een bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="a1b54-155">Delete a file</span></span>
<span data-ttu-id="a1b54-156">Een andere algemene Azure File storage-bewerking wordt verwijderen van bestanden.</span><span class="sxs-lookup"><span data-stu-id="a1b54-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="a1b54-157">Hallo onderstaande code wordt een bestand met de naam SampleFile.txt opgeslagen in een map met de naam **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="a1b54-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="a1b54-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a1b54-158">Next steps</span></span>
<span data-ttu-id="a1b54-159">Als u meer informatie over andere Azure storage-API's toolearn, volgt u deze koppelingen.</span><span class="sxs-lookup"><span data-stu-id="a1b54-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* <span data-ttu-id="a1b54-160">[Azure voor Java-ontwikkelaars](/java/azure)/)</span><span class="sxs-lookup"><span data-stu-id="a1b54-160">[Azure for Java developers](/java/azure)/)</span></span>
* [<span data-ttu-id="a1b54-161">Azure-opslag-SDK voor Java</span><span class="sxs-lookup"><span data-stu-id="a1b54-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="a1b54-162">Azure-opslag-SDK voor Android</span><span class="sxs-lookup"><span data-stu-id="a1b54-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="a1b54-163">Azure Storage Client SDK-naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="a1b54-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="a1b54-164">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="a1b54-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="a1b54-165">Blog van het Azure Storage-team</span><span class="sxs-lookup"><span data-stu-id="a1b54-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="a1b54-166">[Gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span><span class="sxs-lookup"><span data-stu-id="a1b54-166">[Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span></span>