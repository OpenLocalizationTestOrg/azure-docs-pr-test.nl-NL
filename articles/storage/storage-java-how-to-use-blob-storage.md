---
title: Het gebruik van Azure Blob storage (objectopslag) met Java | Microsoft Docs
description: Sla niet-gestructureerde gegevens op in de cloud met Azure Blob Storage (objectopslag).
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
ms.openlocfilehash: b8a4eca600b458802a7a23851bb80ea4da2664ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-java"></a><span data-ttu-id="cf3fd-103">Blob Storage gebruiken met Java</span><span class="sxs-lookup"><span data-stu-id="cf3fd-103">How to use Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="cf3fd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="cf3fd-104">Overview</span></span>
<span data-ttu-id="cf3fd-105">Azure Blob Storage is een service waarmee ongestructureerde gegevens als objecten/blobs worden opgeslagen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="cf3fd-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="cf3fd-107">U kunt Blob Storage zien als een vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="cf3fd-108">In dit artikel wordt beschreven hoe u veelvoorkomende scenario's met behulp van de Microsoft Azure Blob-opslag uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-108">This article will show you how to perform common scenarios using the Microsoft Azure Blob storage.</span></span> <span data-ttu-id="cf3fd-109">De voorbeelden zijn geschreven in Java en gebruik de [Azure-opslag-SDK voor Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="cf3fd-109">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="cf3fd-110">De scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="cf3fd-111">Zie voor meer informatie over blobs de [Vervolgstappen](#Next-Steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-111">For more information on blobs, see the [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="cf3fd-112">Een SDK is beschikbaar voor ontwikkelaars die werken met Azure Storage op Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="cf3fd-113">Zie voor meer informatie de [Azure-opslag-SDK voor Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="cf3fd-113">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="cf3fd-114">Een Java-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="cf3fd-114">Create a Java application</span></span>
<span data-ttu-id="cf3fd-115">In dit artikel gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een Java-toepassing lokaal of in de code die wordt uitgevoerd binnen een Webrol of worker-rol in Azure.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="cf3fd-116">Om dit te doen, moet u Java Development Kit (JDK) installeren en een Azure Storage-account maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-116">To do so, you will need to install the Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="cf3fd-117">Als u dit hebt gedaan, moet u controleren of uw ontwikkelsysteem voldoet aan de minimale vereisten en afhankelijkheden die worden vermeld in de [Azure-opslag-SDK voor Java] [ Azure Storage SDK for Java] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-117">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="cf3fd-118">Als uw systeem aan deze vereisten voldoet, kunt u de instructies voor het downloaden en installeren van de Azure Storage-bibliotheken voor Java op uw systeem vanuit die opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-118">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="cf3fd-119">Nadat u deze taken hebt voltooid, kunt u zich kunt maken van een Java-toepassing die gebruikmaakt van de voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-119">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="cf3fd-120">Uw toepassing configureren voor toegang tot Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="cf3fd-120">Configure your application to access Blob storage</span></span>
<span data-ttu-id="cf3fd-121">De volgende importinstructies toevoegen aan het begin van de Java-bestand waar u de Azure Storage-API's gebruiken voor toegang tot blobs.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-121">Add the following import statements to the top of the Java file where you want to use the Azure Storage APIs to access blobs.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="cf3fd-122">Een Azure Storage-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="cf3fd-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="cf3fd-123">Een Azure Storage-client gebruikt een verbindingsreeks voor opslag voor het opslaan van eindpunten en referenties voor toegang tot gegevens beheerservices.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-123">An Azure Storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="cf3fd-124">Wanneer u in een clienttoepassing uitvoert, moet u opgeven de verbindingsreeks voor opslag in de volgende indeling met de naam van uw opslagaccount en de primaire toegangssleutel voor het opslagaccount vermeld in de [Azure-portal](https://portal.azure.com) voor de *AccountName* en *AccountKey* waarden.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-124">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="cf3fd-125">Het volgende voorbeeld ziet hoe u een statisch veld voor het opslaan van de verbindingsreeks kunt declareren.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-125">The following example shows how you can declare a static field to hold the connection string.</span></span>

```java
// Define the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="cf3fd-126">In een toepassing in een rol in Microsoft Azure wordt uitgevoerd, kan deze tekenreeks worden opgeslagen in het serviceconfiguratiebestand *ServiceConfiguration.cscfg*, en kunnen worden geopend met een aanroep naar de **RoleEnvironment.getConfigurationSettings** methode.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-126">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="cf3fd-127">Het volgende voorbeeld wordt de verbindingsreeks uit een **instelling** element met de naam *StorageConnectionString* in het configuratiebestand van de service.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-127">The following example gets the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="cf3fd-128">De volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden hebt gebruikt om op te halen van de verbindingsreeks voor opslag.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-128">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="cf3fd-129">Een container maken</span><span class="sxs-lookup"><span data-stu-id="cf3fd-129">Create a container</span></span>
<span data-ttu-id="cf3fd-130">Een **CloudBlobClient** object kunt u profiteren van reference-objecten voor containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="cf3fd-131">De volgende code maakt een **CloudBlobClient** object.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-131">The following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="cf3fd-132">Er zijn aanvullende manieren maken **CloudStorageAccount** objecten; voor meer informatie Zie **CloudStorageAccount** in de [naslaginformatie over Azure Storage Client SDK].</span><span class="sxs-lookup"><span data-stu-id="cf3fd-132">There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="cf3fd-133">Gebruik de **CloudBlobClient** object een verwijzing naar de container die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-133">Use the **CloudBlobClient** object to get a reference to the container you want to use.</span></span> <span data-ttu-id="cf3fd-134">U kunt de container maken als deze niet met bestaat de **createIfNotExists** methode, waarmee de bestaande container anders retourneert.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-134">You can create the container if it doesn't exist with the **createIfNotExists** method, which will otherwise return the existing container.</span></span> <span data-ttu-id="cf3fd-135">Standaard is de nieuwe container privé, dus u uw toegangssleutel voor opslag opgeven moet (zoals u eerder hebt gedaan) om blobs te downloaden uit deze container.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-135">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference to a container.
    // The container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create the container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="cf3fd-136">Optioneel: Een container voor openbare toegang configureren</span><span class="sxs-lookup"><span data-stu-id="cf3fd-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="cf3fd-137">Een container machtigingen zijn standaard geconfigureerd voor persoonlijke toegang, maar u kunt gemakkelijk een container machtigingen configureren voor openbare, alleen-lezen toegang toestaan voor alle gebruikers op Internet:</span><span class="sxs-lookup"><span data-stu-id="cf3fd-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions to allow public, read-only access for all users on the Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in the permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set the permissions on the container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="cf3fd-138">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="cf3fd-138">Upload a blob into a container</span></span>
<span data-ttu-id="cf3fd-139">Als u wilt een bestand naar een blob uploadt, een containerverwijzing ophalen en deze gebruiken een blobverwijzing ophalen.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-139">To upload a file to a blob, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="cf3fd-140">Zodra u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom uploaden door het aanroepen van het uploaden van de blobverwijzing.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-140">Once you have a blob reference, you can upload any stream by calling upload on the blob reference.</span></span> <span data-ttu-id="cf3fd-141">Deze bewerking wordt de blob gemaakt als deze niet bestaat of overschrijven als dit het geval is.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-141">This operation will create the blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="cf3fd-142">Het volgende codevoorbeeld ziet u dit en wordt ervan uitgegaan dat de container al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-142">The following code sample shows this, and assumes that the container has already been created.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define the path to a local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite the "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="cf3fd-143">De blobs in een container in een lijst weergeven</span><span class="sxs-lookup"><span data-stu-id="cf3fd-143">List the blobs in a container</span></span>
<span data-ttu-id="cf3fd-144">Als de blobs in een container wilt weergeven, moet u eerst een containerverwijzing net zoals een blob uploaden ophalen.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-144">To list the blobs in a container, first get a container reference like you did to upload a blob.</span></span> <span data-ttu-id="cf3fd-145">U kunt de container **listBlobs** methode met een **voor** lus.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-145">You can use the container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="cf3fd-146">De volgende code wordt de uitvoer de Uri van elke blob in een container met de console.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-146">The following code outputs the Uri of each blob in a container to the console.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within the container and output the URI to each of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="cf3fd-147">Houd er rekening mee dat kunt u de naam blobs met informatie over het pad in hun naam.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="cf3fd-148">Hiermee maakt u een virtuele mapstructuur die u kunt ordenen en kunt doorlopen als een traditioneel bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="cf3fd-149">Houd er rekening mee dat de mapstructuur alleen virtueel is: de enige beschikbare resources in Blob Storage zijn containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-149">Note that the directory structure is virtual only - the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="cf3fd-150">De clientbibliotheek biedt echter een **CloudBlobDirectory** -object om te verwijzen naar een virtuele map en het proces van het werken met blobs die op deze manier zijn ingedeeld vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-150">However, the client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="cf3fd-151">U kan bijvoorbeeld een container met de naam 'foto's ', waarin u uploaden mogelijk blobs met de naam 'rootphoto1', ' 2010/photo1', ' 2010/photo2' en ' 2011/photo1' hebben.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="cf3fd-152">Dit maakt de virtuele mappen '2010' en '2011' in de container 'foto's '.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-152">This would create the virtual directories "2010" and "2011" within the "photos" container.</span></span> <span data-ttu-id="cf3fd-153">Als u aanroept **listBlobs** op de container 'foto's ', de verzameling geretourneerd bevat **CloudBlobDirectory** en **CloudBlob** -objecten die de mappen en blobs die zijn opgenomen op het hoogste niveau.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-153">When you call **listBlobs** on the "photos" container, the collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="cf3fd-154">In dit geval zou mappen '2010' en '2011', evenals photo 'rootphoto1' worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="cf3fd-155">U kunt de **instanceof** operator om te onderscheiden van deze objecten.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-155">You can use the **instanceof** operator to distinguish these objects.</span></span>

<span data-ttu-id="cf3fd-156">U kunt eventueel doorgeven in parameters voor de **listBlobs** methode met de **useFlatBlobListing** parameter ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-156">Optionally, you can pass in parameters to the **listBlobs** method with the **useFlatBlobListing** parameter set to true.</span></span> <span data-ttu-id="cf3fd-157">Dit leidt ertoe dat elke blob wordt geretourneerd, ongeacht de directory.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="cf3fd-158">Zie voor meer informatie **CloudBlobContainer.listBlobs** in de [naslaginformatie over Azure Storage Client SDK].</span><span class="sxs-lookup"><span data-stu-id="cf3fd-158">For more information, see **CloudBlobContainer.listBlobs** in the [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="cf3fd-159">Een blob downloaden</span><span class="sxs-lookup"><span data-stu-id="cf3fd-159">Download a blob</span></span>
<span data-ttu-id="cf3fd-160">Om blobs te downloaden, volgt u dezelfde stappen als u dit hebt gedaan voor het uploaden van een blob om een blobverwijzing ophalen.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-160">To download blobs, follow the same steps as you did for uploading a blob in order to get a blob reference.</span></span> <span data-ttu-id="cf3fd-161">In het voorbeeld uploaden u uploaden voor de blob-object aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-161">In the uploading example, you called upload on the blob object.</span></span> <span data-ttu-id="cf3fd-162">In het volgende voorbeeld roept downloaden om over te dragen van de blobinhoud naar een stroomobject, zoals een **FileOutputStream** dat u gebruiken kunt om vast te leggen van de blob naar een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-162">In the following example, call download to transfer the blob contents to a stream object such as a **FileOutputStream** that you can use to persist the blob to a local file.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in the container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If the item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download the item and save it to a file with the same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="cf3fd-163">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="cf3fd-163">Delete a blob</span></span>
<span data-ttu-id="cf3fd-164">Verwijderen van een blob, een blobverwijzing ophalen en aanroep **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-164">To delete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference to a blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete the blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="cf3fd-165">Verwijderen van een blob-container</span><span class="sxs-lookup"><span data-stu-id="cf3fd-165">Delete a blob container</span></span>
<span data-ttu-id="cf3fd-166">Ten slotte voor het verwijderen van een blob-container ophalen van een blob containerverwijzing en aanroep **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-166">Finally, to delete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete the blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="cf3fd-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cf3fd-167">Next steps</span></span>
<span data-ttu-id="cf3fd-168">Nu dat u de basisprincipes van Blob storage hebt geleerd, volgt u deze koppelingen voor meer informatie over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="cf3fd-168">Now that you've learned the basics of Blob storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="cf3fd-169">[Azure-opslag-SDK voor Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="cf3fd-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="cf3fd-170">[naslaginformatie over Azure Storage Client SDK][naslaginformatie over Azure Storage Client SDK]</span><span class="sxs-lookup"><span data-stu-id="cf3fd-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="cf3fd-171">[REST API van Azure Storage][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="cf3fd-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="cf3fd-172">[Azure Storage-teamblog][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="cf3fd-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="cf3fd-173">Zie voor meer informatie, ook de [Java Developer Center](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="cf3fd-173">For more information, see also the [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="cf3fd-174">[naslaginformatie over Azure Storage Client SDK]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="cf3fd-174">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
