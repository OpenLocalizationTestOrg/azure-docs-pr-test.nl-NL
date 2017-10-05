---
title: Ontwikkelen voor Azure File storage met behulp van Java | Microsoft Docs
description: Informatie over het ontwikkelen van Java-toepassingen en services die gebruikmaken van Azure File storage voor het opslaan van gegevens uit een bestand.
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
ms.openlocfilehash: 16924599e49990265e07f7a58613756d93c46942
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="189f9-103">Ontwikkelen voor Azure File storage met Java</span><span class="sxs-lookup"><span data-stu-id="189f9-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="189f9-104">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="189f9-104">About this tutorial</span></span>
<span data-ttu-id="189f9-105">Deze zelfstudie wordt gedemonstreerd de basisbeginselen van het gebruik van Java voor het ontwikkelen van toepassingen of services die Azure File storage gebruiken voor het opslaan van gegevens uit een bestand.</span><span class="sxs-lookup"><span data-stu-id="189f9-105">This tutorial will demonstrate the basics of using Java to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="189f9-106">In deze zelfstudie wordt een eenvoudige consoletoepassing maken en het uitvoeren van basisbewerkingen uitvoeren met Java en Azure File storage weergeven:</span><span class="sxs-lookup"><span data-stu-id="189f9-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="189f9-107">Maken en verwijderen van de Azure-bestandsshares</span><span class="sxs-lookup"><span data-stu-id="189f9-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="189f9-108">Maken en verwijderen van mappen</span><span class="sxs-lookup"><span data-stu-id="189f9-108">Create and delete directories</span></span>
* <span data-ttu-id="189f9-109">Bestanden en mappen in een Azure-bestandsshare opsommen</span><span class="sxs-lookup"><span data-stu-id="189f9-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="189f9-110">Uploaden, downloaden en een bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="189f9-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="189f9-111">Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk om eenvoudige toepassingen die toegang hebben tot de bestandsshare in Azure met behulp van de standaard Java-i/o-klassen te schrijven.</span><span class="sxs-lookup"><span data-stu-id="189f9-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Java I/O classes.</span></span> <span data-ttu-id="189f9-112">In dit artikel wordt beschreven hoe schrijven van toepassingen die gebruikmaken van de Azure Storage Java SDK, die gebruikmaakt van de [Azure File storage REST-API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) voor communicatie met Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="189f9-112">This article will describe how to write applications that use the Azure Storage Java SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="189f9-113">Een Java-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="189f9-113">Create a Java application</span></span>
<span data-ttu-id="189f9-114">Als u wilt de voorbeelden bouwt, moet u Java Development Kit (JDK) en de [Azure-opslag-SDK voor Java] [].</span><span class="sxs-lookup"><span data-stu-id="189f9-114">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="189f9-115">U moet hebt een Azure storage-account ook gemaakt.</span><span class="sxs-lookup"><span data-stu-id="189f9-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-to-use-azure-file-storage"></a><span data-ttu-id="189f9-116">Uw toepassing Azure File storage gebruiken instellen</span><span class="sxs-lookup"><span data-stu-id="189f9-116">Setup your application to use Azure File storage</span></span>
<span data-ttu-id="189f9-117">Voor het gebruik van de Azure storage-API's de volgende instructie toe te voegen aan het begin van de Java-bestand waarin u van plan bent voor toegang tot de storage-service uit.</span><span class="sxs-lookup"><span data-stu-id="189f9-117">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="189f9-118">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="189f9-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="189f9-119">U moet verbinding maken met uw Azure storage-account voor het gebruik van Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="189f9-119">To use Azure File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="189f9-120">De eerste stap is om een verbindingsreeks die we gebruiken om verbinding maken met uw storage-account te configureren.</span><span class="sxs-lookup"><span data-stu-id="189f9-120">The first step would be to configure a connection string which we'll use to connect to your storage account.</span></span> <span data-ttu-id="189f9-121">We gaan een statische variabele hiervoor definiëren.</span><span class="sxs-lookup"><span data-stu-id="189f9-121">Let's define a static variable to do that.</span></span>

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="189f9-122">Your_storage_account_name en your_storage_account_key vervangen door de werkelijke waarden voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="189f9-122">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="189f9-123">Verbinding maken met een Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="189f9-123">Connecting to an Azure storage account</span></span>
<span data-ttu-id="189f9-124">Voor verbinding met uw storage-account, moet u gebruiken de **CloudStorageAccount** -object doorgeven van een verbindingsreeks voor de **parseren** methode.</span><span class="sxs-lookup"><span data-stu-id="189f9-124">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span></span>

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

<span data-ttu-id="189f9-125">**CloudStorageAccount.parse** genereert een InvalidKeyException zodat u wilt plaatsen in een try/catch-blok.</span><span class="sxs-lookup"><span data-stu-id="189f9-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="189f9-126">Een Azure-bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="189f9-126">Create an Azure File share</span></span>
<span data-ttu-id="189f9-127">Alle bestanden en mappen in Azure File storage bevinden zich in een zogenaamd een **Share**.</span><span class="sxs-lookup"><span data-stu-id="189f9-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="189f9-128">Uw storage-account kan net zoveel shares als de capaciteit van uw account kunt hebben.</span><span class="sxs-lookup"><span data-stu-id="189f9-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="189f9-129">Als u wilt toegang krijgen tot een share en de inhoud ervan, moet u een Azure File storage-client gebruiken.</span><span class="sxs-lookup"><span data-stu-id="189f9-129">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="189f9-130">U kunt vervolgens een een verwijzing naar een share ophalen met behulp van de Azure File storage-client.</span><span class="sxs-lookup"><span data-stu-id="189f9-130">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="189f9-131">Gebruik voor het daadwerkelijk maken van de share de **createIfNotExists** methode van het object CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="189f9-131">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="189f9-132">Op dit moment **delen** bevat een verwijzing naar een share met de naam **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="189f9-132">At this point, **share** holds a reference to a share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="189f9-133">Verwijderen van een Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="189f9-133">Delete an Azure File share</span></span>
<span data-ttu-id="189f9-134">Verwijderen van een share wordt gedaan door het aanroepen van de **deleteIfExists** methode voor het object CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="189f9-134">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="189f9-135">Hier volgt voorbeeldcode die dat doet.</span><span class="sxs-lookup"><span data-stu-id="189f9-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference to the file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="189f9-136">Een map maken</span><span class="sxs-lookup"><span data-stu-id="189f9-136">Create a directory</span></span>
<span data-ttu-id="189f9-137">U kunt ook de opslag indelen door de gegevens van de bestanden in submappen in plaats van ze allemaal in de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="189f9-137">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="189f9-138">Azure File storage kunt u net zoveel mappen maken als uw account krijgt.</span><span class="sxs-lookup"><span data-stu-id="189f9-138">Azure File storage allows you to create as much directories as your account will allow.</span></span> <span data-ttu-id="189f9-139">De code hieronder maakt u een onderliggende map met de naam **sampledir** onder de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="189f9-139">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="189f9-140">Een map verwijderen</span><span class="sxs-lookup"><span data-stu-id="189f9-140">Delete a directory</span></span>
<span data-ttu-id="189f9-141">Als u een map is een redelijk eenvoudig taak, maar houd er rekening mee dat u een map met nog steeds bestanden of andere mappen niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="189f9-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory you want to delete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete the directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="189f9-142">Bestanden en mappen in een Azure-bestandsshare opsommen</span><span class="sxs-lookup"><span data-stu-id="189f9-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="189f9-143">Eenvoudig het verkrijgen van een lijst met bestanden en mappen in een share wordt gedaan door het aanroepen van **listFilesAndDirectories** op een CloudFileDirectory-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="189f9-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="189f9-144">De methode retourneert een lijst met ListFileItem-objecten die u kunt herhalen.</span><span class="sxs-lookup"><span data-stu-id="189f9-144">The method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="189f9-145">Als u bijvoorbeeld geeft de volgende code bestanden en mappen in de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="189f9-145">As an example, the following code will list files and directories inside the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="189f9-146">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="189f9-146">Upload a file</span></span>
<span data-ttu-id="189f9-147">Een Azure-File share tenminste bevat, een hoofdmap waarin de bestanden kunnen zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="189f9-147">An Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="189f9-148">In deze sectie leert u hoe een bestand van de lokale opslag naar de hoofdmap van een share te uploaden.</span><span class="sxs-lookup"><span data-stu-id="189f9-148">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="189f9-149">De eerste stap bij het uploaden van een bestand is te halen van een verwijzing naar de map waarin dit zich moet bevinden.</span><span class="sxs-lookup"><span data-stu-id="189f9-149">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="189f9-150">U doet dit door de **getRootDirectoryReference** methode van de shareobject.</span><span class="sxs-lookup"><span data-stu-id="189f9-150">You do this by calling the **getRootDirectoryReference** method of the share object.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="189f9-151">Nu dat u een verwijzing naar de hoofdmap van de share hebt, kunt u een bestand op met behulp van de volgende code kunt uploaden.</span><span class="sxs-lookup"><span data-stu-id="189f9-151">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span></span>

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="189f9-152">Bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="189f9-152">Download a file</span></span>
<span data-ttu-id="189f9-153">Een van de vaker bewerkingen die u op basis van Azure File storage uitvoeren wilt is om bestanden te downloaden.</span><span class="sxs-lookup"><span data-stu-id="189f9-153">One of the more frequent operations you will perform against Azure File storage is to download files.</span></span> <span data-ttu-id="189f9-154">In het volgende voorbeeld wordt de code SampleFile.txt gedownload en wordt de inhoud weergegeven.</span><span class="sxs-lookup"><span data-stu-id="189f9-154">In the following example, the code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the directory that contains the file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference to the file you want to download
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write the contents of the file to the console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="189f9-155">Een bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="189f9-155">Delete a file</span></span>
<span data-ttu-id="189f9-156">Een andere algemene Azure File storage-bewerking wordt verwijderen van bestanden.</span><span class="sxs-lookup"><span data-stu-id="189f9-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="189f9-157">De volgende code verwijdert een bestand met de naam SampleFile.txt opgeslagen in een map met de naam **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="189f9-157">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory where the file to be deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="189f9-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="189f9-158">Next steps</span></span>
<span data-ttu-id="189f9-159">Als u meer informatie over andere Azure storage-API's wilt, volgt u deze koppelingen.</span><span class="sxs-lookup"><span data-stu-id="189f9-159">If you would like to learn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="189f9-160">Java Developer Center</span><span class="sxs-lookup"><span data-stu-id="189f9-160">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="189f9-161">Azure-opslag-SDK voor Java</span><span class="sxs-lookup"><span data-stu-id="189f9-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="189f9-162">Azure-opslag-SDK voor Android</span><span class="sxs-lookup"><span data-stu-id="189f9-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="189f9-163">Azure Storage Client SDK-naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="189f9-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="189f9-164">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="189f9-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="189f9-165">Blog van het Azure Storage-team</span><span class="sxs-lookup"><span data-stu-id="189f9-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="189f9-166">Gegevensoverdracht met het AzCopy-opdrachtregelprogramma</span><span class="sxs-lookup"><span data-stu-id="189f9-166">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)