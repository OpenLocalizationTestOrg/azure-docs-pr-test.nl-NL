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
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>Ontwikkelen voor Azure File storage met Java
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>Over deze zelfstudie
Deze zelfstudie wordt gedemonstreerd Hallo grondbeginselen van het gebruik van Java-toodevelop toepassingen of services die gebruikmaken van Azure File storage toostore bestandsgegevens. In deze zelfstudie wordt een eenvoudige consoletoepassing maken en weergeven hoe tooperform basisbewerkingen uitvoeren met Java en Azure File storage:

* Maken en verwijderen van de Azure-bestandsshares
* Maken en verwijderen van mappen
* Bestanden en mappen in een Azure-bestandsshare opsommen
* Uploaden, downloaden en een bestand verwijderen

> [!Note]  
> Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk toowrite eenvoudige toepassingen die toegang hebben tot hello Azure bestandsshare met behulp van Hallo standaard Java i/o-klassen. In dit artikel wordt beschreven hoe toowrite toepassingen die gebruikmaken van Azure Storage Java SDK, die gebruikmaakt van Hallo Hallo [Azure File storage REST-API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.

## <a name="create-a-java-application"></a>Een Java-toepassing maken
Voorbeelden van toobuild hello, moet u Hallo Java Development Kit (JDK) en Hallo [Azure-opslag-SDK voor Java] []. U moet hebt een Azure storage-account ook gemaakt.

## <a name="setup-your-application-toouse-azure-file-storage"></a>Instellen van uw toepassing toouse Azure File storage
toouse hello Azure storage-API's, toevoegen Hallo instructie toohello boven in Hallo Java-bestand waarin u van plan bent tooaccess Hallo storage-service uit te volgen.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Een Azure-opslag-verbindingsreeks instellen
Azure File storage toouse, moet u tooconnect tooyour Azure storage-account. Hallo eerste stap zou zijn tooconfigure een verbindingsreeks die we gebruiken tooconnect tooyour storage-account. We gaan een statische variabele toodo definiëren die.

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Your_storage_account_name en your_storage_account_key vervangen door feitelijke waarden Hallo voor uw opslagaccount.
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>Verbinding maken met tooan Azure storage-account
tooconnect tooyour storage-account, moet u toouse hello **CloudStorageAccount** -object doorgeven van een tekenreeks verbinding tooits **parseren** methode.

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse** er wordt een InvalidKeyException dus u tooput moet in een trycatch blokkeren.

## <a name="create-an-azure-file-share"></a>Een Azure-bestandsshare maken
Alle bestanden en mappen in Azure File storage bevinden zich in een zogenaamd een **Share**. Uw storage-account kan net zoveel shares als de capaciteit van uw account kunt hebben. tooobtain toegang tooa share en de inhoud ervan, moet u een Azure File storage client toouse.

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

U kunt vervolgens een verwijzing tooa share verkrijgen met behulp van hello Azure File storage client.

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually hello share maken, gebruikt u Hallo **createIfNotExists** methode van Hallo CloudFileShare-object.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

Op dit moment **delen** bevat een verwijzing tooa share met de naam **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Verwijderen van een Azure-bestandsshare
Verwijderen van een share wordt uitgevoerd door de aanroepende Hallo **deleteIfExists** methode voor het object CloudFileShare. Hier volgt voorbeeldcode die dat doet.

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

## <a name="create-a-directory"></a>Een map maken
U kunt ook opslag door de gegevens van de bestanden in submappen in plaats van ze allemaal in de hoofdmap Hallo indelen. Azure File storage, kunt u toocreate veel mappen als uw account wordt toegestaan. Hallo-code hieronder maakt u een onderliggende map met de naam **sampledir** onder Hallo-hoofdmap.

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

## <a name="delete-a-directory"></a>Een map verwijderen
Als u een map is een redelijk eenvoudig taak, maar houd er rekening mee dat u een map met nog steeds bestanden of andere mappen niet verwijderen.

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Bestanden en mappen in een Azure-bestandsshare opsommen
Eenvoudig het verkrijgen van een lijst met bestanden en mappen in een share wordt gedaan door het aanroepen van **listFilesAndDirectories** op een CloudFileDirectory-verwijzing. Hallo-methode retourneert een lijst met ListFileItem-objecten die u kunt herhalen. Als u bijvoorbeeld hello volgende code wordt een lijst bestanden en mappen in de hoofdmap Hallo.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Bestand uploaden
Een Azure-File share op Hallo zeer minste bevat, een hoofdmap waarin de bestanden kunnen zich bevinden. In deze sectie leert u hoe een bestand van de lokale opslag op Hallo tooupload de hoofdmap van een share.

Hallo eerste stap bij het uploaden van een bestand is tooobtain een verwijzing toohello map waarin dit zich moet bevinden. Dit doet u door de aanroepende Hallo **getRootDirectoryReference** methode van Hallo share-object.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Nu dat u de hoofdmap van een verwijzing toohello van Hallo-share hebt, kunt u een bestand op met behulp van de volgende code Hallo uploaden.

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Bestand downloaden
Een van de Hallo frequentere bewerkingen die u op basis van Azure File storage uitvoeren wilt is toodownload bestanden. In Hallo voorbeeld te volgen, Hallo code SampleFile.txt gedownload en wordt de inhoud weergegeven.

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

## <a name="delete-a-file"></a>Een bestand verwijderen
Een andere algemene Azure File storage-bewerking wordt verwijderen van bestanden. Hallo onderstaande code wordt een bestand met de naam SampleFile.txt opgeslagen in een map met de naam **sampledir**.

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

## <a name="next-steps"></a>Volgende stappen
Als u meer informatie over andere Azure storage-API's toolearn, volgt u deze koppelingen.

* [Java Developer Center](http://azure.microsoft.com/develop/java/)
* [Azure-opslag-SDK voor Java](https://github.com/azure/azure-storage-java)
* [Azure-opslag-SDK voor Android](https://github.com/azure/azure-storage-android)
* [Azure Storage Client SDK-naslaginformatie](http://dl.windowsazure.com/storage/javadoc/)
* [REST-API voor Azure Storage-services](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog van het Azure Storage-team](http://blogs.msdn.com/b/windowsazurestorage/)
* [Gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md)
