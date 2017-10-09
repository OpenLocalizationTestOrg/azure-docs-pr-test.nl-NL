---
title: aaaHow toouse Azure Blob storage (objectopslag) met Java | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 6dd6efdf688161c32b9d73a65fa7f3a98f2fad74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a>Hoe toouse Blob-opslag met Java
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Overzicht
Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat. In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen. BLOB-opslag is ook bedoeld tooas vorm van objectopslag.

Dit artikel wordt beschreven hoe tooperform algemene scenario's met behulp van Microsoft Azure-blobopslag Hallo. Hallo-voorbeelden zijn geschreven in Java en gebruiken van Hallo [Azure-opslag-SDK voor Java][Azure Storage SDK for Java]. Hallo scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs. Zie voor meer informatie over blobs Hallo [Vervolgstappen](#Next-Steps) sectie.

> [!NOTE]
> Een SDK is beschikbaar voor ontwikkelaars die werken met Azure Storage op Android-apparaten. Zie voor meer informatie, Hallo [Azure-opslag-SDK voor Android][Azure Storage SDK for Android].
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Een Java-toepassing maken
In dit artikel gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een Java-toepassing lokaal of in de code die wordt uitgevoerd binnen een Webrol of worker-rol in Azure.

toodo geval is, moet u tooinstall Hallo Java Development Kit (JDK) en een Azure Storage-account maken in uw Azure-abonnement. Nadat u dit hebt gedaan, moet u tooverify dat uw ontwikkelsysteem voldoet aan de minimumvereisten Hallo en afhankelijkheden die worden vermeld in Hallo [Azure-opslag-SDK voor Java] [ Azure Storage SDK for Java] opslagplaats op GitHub. Als uw systeem aan deze vereisten voldoet, kunt u de instructies voor het downloaden en installeren van hello Azure Storage-bibliotheken voor Java op uw systeem vanuit die opslagplaats Hallo volgen. Nadat u deze taken hebt voltooid, kunt u zich kunt toocreate een Java-toepassing die gebruikmaakt van Hallo voorbeelden in dit artikel.

## <a name="configure-your-application-tooaccess-blob-storage"></a>Uw toepassing tooaccess Blob-opslag configureren
Hallo na importeren instructies toohello boven in Hallo Java bestand waar u toouse hello Azure Storage-API's tooaccess blobs wilt toevoegen.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Een Azure Storage-verbindingsreeks instellen
Een Azure Storage-client maakt gebruik van een storage connection string toostore eindpunten en referenties voor toegang tot gegevens beheerservices. Wanneer een client-toepassing wordt uitgevoerd, moet u bieden Hallo verbindingsreeks voor opslag in Hallo indeling te volgen, met behulp van Hallo-naam van uw opslagaccount en primaire toegangssleutel voor opslagaccount Hallo die worden vermeld in Hallo Hallo [Azure-portal](https://portal.azure.com)voor Hallo *AccountName* en *AccountKey* waarden. Hallo volgende voorbeeld ziet u hoe u een statisch veld toohold Hallo-verbindingsreeks kunt declareren.

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

In een toepassing in een rol in Microsoft Azure wordt uitgevoerd, kan deze tekenreeks worden opgeslagen in Hallo serviceconfiguratiebestand, *ServiceConfiguration.cscfg*, en kunnen worden geopend met een aanroep van toohello  **RoleEnvironment.getConfigurationSettings** methode. Hallo volgende voorbeeld wordt de verbindingsreeks Hallo uit een **instelling** element met de naam *StorageConnectionString* in Hallo serviceconfiguratiebestand.

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hallo volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden tooget Hallo-opslagverbindingsreeks hebt gebruikt.

## <a name="create-a-container"></a>Een container maken
Een **CloudBlobClient** object kunt u profiteren van reference-objecten voor containers en blobs. Hallo volgende code maakt een **CloudBlobClient** object.

> [!NOTE]
> Er zijn extra manieren toocreate **CloudStorageAccount** objecten; voor meer informatie Zie **CloudStorageAccount** in Hallo [naslaginformatie over Azure Storage Client SDK].
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Gebruik Hallo **CloudBlobClient** tooget een verwijzing toohello-container die u wilt dat toouse object. U kunt Hallo container maken als deze niet Hello bestaat **createIfNotExists** methode, waarbij bestaande container Hallo anders retourneert. Hallo nieuwe container is standaard privé, dus u uw toegangssleutel voor opslag opgeven moet (zoals u eerder hebt gedaan) toodownload blobs uit deze container.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>Optioneel: Een container voor openbare toegang configureren
Een container machtigingen zijn standaard geconfigureerd voor persoonlijke toegang, maar u kunt gemakkelijk een container machtigingen tooallow openbare, alleen-lezen toegang voor alle gebruikers op Hallo Internet configureren:

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>Een blob uploaden naar een container
een bestand tooa blob tooupload een containerverwijzing ophalen en deze tooget een blobverwijzing gebruiken. Zodra u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom door het aanroepen van uploaden op Hallo blobverwijzing uploaden. Deze bewerking wordt Hallo blob gemaakt als deze niet bestaat of overschrijven als dit het geval is. Hallo volgende codevoorbeeld ziet u dit en wordt ervan uitgegaan dat Hallo-container al is gemaakt.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a>Lijst Hallo blobs in een container
toolist hello blobs in een container, eerst ophalen een containerverwijzing net zoals tooupload een blob. U kunt Hallo-container **listBlobs** methode met een **voor** lus. Hallo volgende code wordt de uitvoer Hallo-Uri van elke blob in een container toohello-console.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Houd er rekening mee dat kunt u de naam blobs met informatie over het pad in hun naam. Hiermee maakt u een virtuele mapstructuur die u kunt ordenen en kunt doorlopen als een traditioneel bestandssysteem. Houd er rekening mee dat Hallo mapstructuur alleen virtueel is: hello alleen bronnen beschikbaar zijn in Blob storage containers en blobs zijn. Hallo-clientbibliotheek biedt echter een **CloudBlobDirectory** object toorefer tooa virtuele map en Hallo vereenvoudigen van het werken met blobs die op deze manier zijn ingedeeld.

U kan bijvoorbeeld een container met de naam 'foto's ', waarin u uploaden mogelijk blobs met de naam 'rootphoto1', ' 2010/photo1', ' 2010/photo2' en ' 2011/photo1' hebben. Dit zou Hallo virtuele mappen '2010' en '2011' in Hallo 'foto's ' container maken. Als u aanroept **listBlobs** op Hallo 'foto's ' container, Hallo verzameling geretourneerd bevat **CloudBlobDirectory** en **CloudBlob** -objecten die Hallo vertegenwoordigen mappen en blobs op het hoogste niveau Hallo opgenomen. In dit geval zou mappen '2010' en '2011', evenals photo 'rootphoto1' worden geretourneerd. U kunt Hallo **instanceof** operator toodistinguish deze objecten.

U kunt eventueel doorgeven in parameters toohello **listBlobs** methode Hello **useFlatBlobListing** parameter tootrue ingesteld. Dit leidt ertoe dat elke blob wordt geretourneerd, ongeacht de directory. Zie voor meer informatie **CloudBlobContainer.listBlobs** in Hallo [naslaginformatie over Azure Storage Client SDK].

## <a name="download-a-blob"></a>Een blob downloaden
toodownload blobs, volgt u dezelfde stappen als u dit hebt gedaan voor het uploaden van een blob in volgorde tooget een blobverwijzing Hallo. In Hallo voorbeeld uploaden, kunt u uploaden voor Hallo blob-object aangeroepen. In de Hallo voorbeeld te volgen, roept downloaden tootransfer Hallo blob inhoud tooa stroomobject zoals een **FileOutputStream** waarmee u toopersist Hallo blob tooa lokaal bestand kunt.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>Een blob verwijderen
een blob toodelete ophalen van een blob naar verwijzen, en roept **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>Verwijderen van een blob-container
Ten slotte toodelete een blobcontainer een blob ophalen containerverwijzing en aanroep **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Blob storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.

* [Azure-opslag-SDK voor Java][Azure Storage SDK for Java]
* [naslaginformatie over Azure Storage Client SDK][naslaginformatie over Azure Storage Client SDK]
* [REST API van Azure Storage][Azure Storage REST API]
* [Azure Storage-teamblog][Azure Storage Team Blog]

Zie voor meer informatie, ook Hallo [Java Developer Center](/develop/java/).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[naslaginformatie over Azure Storage Client SDK]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
