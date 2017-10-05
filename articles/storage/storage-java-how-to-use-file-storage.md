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
# <a name="develop-for-azure-file-storage-with-java"></a>Ontwikkelen voor Azure File storage met Java
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>Over deze zelfstudie
Deze zelfstudie wordt gedemonstreerd de basisbeginselen van het gebruik van Java voor het ontwikkelen van toepassingen of services die Azure File storage gebruiken voor het opslaan van gegevens uit een bestand. In deze zelfstudie wordt een eenvoudige consoletoepassing maken en het uitvoeren van basisbewerkingen uitvoeren met Java en Azure File storage weergeven:

* Maken en verwijderen van de Azure-bestandsshares
* Maken en verwijderen van mappen
* Bestanden en mappen in een Azure-bestandsshare opsommen
* Uploaden, downloaden en een bestand verwijderen

> [!Note]  
> Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk om eenvoudige toepassingen die toegang hebben tot de bestandsshare in Azure met behulp van de standaard Java-i/o-klassen te schrijven. In dit artikel wordt beschreven hoe schrijven van toepassingen die gebruikmaken van de Azure Storage Java SDK, die gebruikmaakt van de [Azure File storage REST-API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) voor communicatie met Azure File storage.

## <a name="create-a-java-application"></a>Een Java-toepassing maken
Als u wilt de voorbeelden bouwt, moet u Java Development Kit (JDK) en de [Azure-opslag-SDK voor Java] []. U moet hebt een Azure storage-account ook gemaakt.

## <a name="setup-your-application-to-use-azure-file-storage"></a>Uw toepassing Azure File storage gebruiken instellen
Voor het gebruik van de Azure storage-API's de volgende instructie toe te voegen aan het begin van de Java-bestand waarin u van plan bent voor toegang tot de storage-service uit.

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Een Azure-opslag-verbindingsreeks instellen
U moet verbinding maken met uw Azure storage-account voor het gebruik van Azure File storage. De eerste stap is om een verbindingsreeks die we gebruiken om verbinding maken met uw storage-account te configureren. We gaan een statische variabele hiervoor definiëren.

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Your_storage_account_name en your_storage_account_key vervangen door de werkelijke waarden voor uw opslagaccount.
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a>Verbinding maken met een Azure storage-account
Voor verbinding met uw storage-account, moet u gebruiken de **CloudStorageAccount** -object doorgeven van een verbindingsreeks voor de **parseren** methode.

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

**CloudStorageAccount.parse** genereert een InvalidKeyException zodat u wilt plaatsen in een try/catch-blok.

## <a name="create-an-azure-file-share"></a>Een Azure-bestandsshare maken
Alle bestanden en mappen in Azure File storage bevinden zich in een zogenaamd een **Share**. Uw storage-account kan net zoveel shares als de capaciteit van uw account kunt hebben. Als u wilt toegang krijgen tot een share en de inhoud ervan, moet u een Azure File storage-client gebruiken.

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

U kunt vervolgens een een verwijzing naar een share ophalen met behulp van de Azure File storage-client.

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

Gebruik voor het daadwerkelijk maken van de share de **createIfNotExists** methode van het object CloudFileShare.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

Op dit moment **delen** bevat een verwijzing naar een share met de naam **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Verwijderen van een Azure-bestandsshare
Verwijderen van een share wordt gedaan door het aanroepen van de **deleteIfExists** methode voor het object CloudFileShare. Hier volgt voorbeeldcode die dat doet.

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

## <a name="create-a-directory"></a>Een map maken
U kunt ook de opslag indelen door de gegevens van de bestanden in submappen in plaats van ze allemaal in de hoofdmap. Azure File storage kunt u net zoveel mappen maken als uw account krijgt. De code hieronder maakt u een onderliggende map met de naam **sampledir** onder de hoofdmap.

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

## <a name="delete-a-directory"></a>Een map verwijderen
Als u een map is een redelijk eenvoudig taak, maar houd er rekening mee dat u een map met nog steeds bestanden of andere mappen niet verwijderen.

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Bestanden en mappen in een Azure-bestandsshare opsommen
Eenvoudig het verkrijgen van een lijst met bestanden en mappen in een share wordt gedaan door het aanroepen van **listFilesAndDirectories** op een CloudFileDirectory-verwijzing. De methode retourneert een lijst met ListFileItem-objecten die u kunt herhalen. Als u bijvoorbeeld geeft de volgende code bestanden en mappen in de hoofdmap.

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Bestand uploaden
Een Azure-File share tenminste bevat, een hoofdmap waarin de bestanden kunnen zich bevinden. In deze sectie leert u hoe een bestand van de lokale opslag naar de hoofdmap van een share te uploaden.

De eerste stap bij het uploaden van een bestand is te halen van een verwijzing naar de map waarin dit zich moet bevinden. U doet dit door de **getRootDirectoryReference** methode van de shareobject.

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Nu dat u een verwijzing naar de hoofdmap van de share hebt, kunt u een bestand op met behulp van de volgende code kunt uploaden.

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Bestand downloaden
Een van de vaker bewerkingen die u op basis van Azure File storage uitvoeren wilt is om bestanden te downloaden. In het volgende voorbeeld wordt de code SampleFile.txt gedownload en wordt de inhoud weergegeven.

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

## <a name="delete-a-file"></a>Een bestand verwijderen
Een andere algemene Azure File storage-bewerking wordt verwijderen van bestanden. De volgende code verwijdert een bestand met de naam SampleFile.txt opgeslagen in een map met de naam **sampledir**.

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

## <a name="next-steps"></a>Volgende stappen
Als u meer informatie over andere Azure storage-API's wilt, volgt u deze koppelingen.

* [Java Developer Center](http://azure.microsoft.com/develop/java/)
* [Azure-opslag-SDK voor Java](https://github.com/azure/azure-storage-java)
* [Azure-opslag-SDK voor Android](https://github.com/azure/azure-storage-android)
* [Azure Storage Client SDK-naslaginformatie](http://dl.windowsazure.com/storage/javadoc/)
* [REST-API voor Azure Storage-services](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog van het Azure Storage-team](http://blogs.msdn.com/b/windowsazurestorage/)
* [Gegevensoverdracht met het AzCopy-opdrachtregelprogramma](storage-use-azcopy.md)