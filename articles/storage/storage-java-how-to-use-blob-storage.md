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
# <a name="how-toouse-blob-storage-from-java"></a><span data-ttu-id="8e74a-103">Hoe toouse Blob-opslag met Java</span><span class="sxs-lookup"><span data-stu-id="8e74a-103">How toouse Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="8e74a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8e74a-104">Overview</span></span>
<span data-ttu-id="8e74a-105">Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat.</span><span class="sxs-lookup"><span data-stu-id="8e74a-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="8e74a-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8e74a-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="8e74a-107">BLOB-opslag is ook bedoeld tooas vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="8e74a-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="8e74a-108">Dit artikel wordt beschreven hoe tooperform algemene scenario's met behulp van Microsoft Azure-blobopslag Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e74a-108">This article will show you how tooperform common scenarios using hello Microsoft Azure Blob storage.</span></span> <span data-ttu-id="8e74a-109">Hallo-voorbeelden zijn geschreven in Java en gebruiken van Hallo [Azure-opslag-SDK voor Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="8e74a-109">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="8e74a-110">Hallo scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs.</span><span class="sxs-lookup"><span data-stu-id="8e74a-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="8e74a-111">Zie voor meer informatie over blobs Hallo [Vervolgstappen](#Next-Steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="8e74a-111">For more information on blobs, see hello [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="8e74a-112">Een SDK is beschikbaar voor ontwikkelaars die werken met Azure Storage op Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="8e74a-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="8e74a-113">Zie voor meer informatie, Hallo [Azure-opslag-SDK voor Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="8e74a-113">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="8e74a-114">Een Java-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="8e74a-114">Create a Java application</span></span>
<span data-ttu-id="8e74a-115">In dit artikel gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een Java-toepassing lokaal of in de code die wordt uitgevoerd binnen een Webrol of worker-rol in Azure.</span><span class="sxs-lookup"><span data-stu-id="8e74a-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="8e74a-116">toodo geval is, moet u tooinstall Hallo Java Development Kit (JDK) en een Azure Storage-account maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8e74a-116">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="8e74a-117">Nadat u dit hebt gedaan, moet u tooverify dat uw ontwikkelsysteem voldoet aan de minimumvereisten Hallo en afhankelijkheden die worden vermeld in Hallo [Azure-opslag-SDK voor Java] [ Azure Storage SDK for Java] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="8e74a-117">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="8e74a-118">Als uw systeem aan deze vereisten voldoet, kunt u de instructies voor het downloaden en installeren van hello Azure Storage-bibliotheken voor Java op uw systeem vanuit die opslagplaats Hallo volgen.</span><span class="sxs-lookup"><span data-stu-id="8e74a-118">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="8e74a-119">Nadat u deze taken hebt voltooid, kunt u zich kunt toocreate een Java-toepassing die gebruikmaakt van Hallo voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8e74a-119">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="8e74a-120">Uw toepassing tooaccess Blob-opslag configureren</span><span class="sxs-lookup"><span data-stu-id="8e74a-120">Configure your application tooaccess Blob storage</span></span>
<span data-ttu-id="8e74a-121">Hallo na importeren instructies toohello boven in Hallo Java bestand waar u toouse hello Azure Storage-API's tooaccess blobs wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8e74a-121">Add hello following import statements toohello top of hello Java file where you want toouse hello Azure Storage APIs tooaccess blobs.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="8e74a-122">Een Azure Storage-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="8e74a-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="8e74a-123">Een Azure Storage-client maakt gebruik van een storage connection string toostore eindpunten en referenties voor toegang tot gegevens beheerservices.</span><span class="sxs-lookup"><span data-stu-id="8e74a-123">An Azure Storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="8e74a-124">Wanneer een client-toepassing wordt uitgevoerd, moet u bieden Hallo verbindingsreeks voor opslag in Hallo indeling te volgen, met behulp van Hallo-naam van uw opslagaccount en primaire toegangssleutel voor opslagaccount Hallo die worden vermeld in Hallo Hallo [Azure-portal](https://portal.azure.com)voor Hallo *AccountName* en *AccountKey* waarden.</span><span class="sxs-lookup"><span data-stu-id="8e74a-124">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="8e74a-125">Hallo volgende voorbeeld ziet u hoe u een statisch veld toohold Hallo-verbindingsreeks kunt declareren.</span><span class="sxs-lookup"><span data-stu-id="8e74a-125">hello following example shows how you can declare a static field toohold hello connection string.</span></span>

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="8e74a-126">In een toepassing in een rol in Microsoft Azure wordt uitgevoerd, kan deze tekenreeks worden opgeslagen in Hallo serviceconfiguratiebestand, *ServiceConfiguration.cscfg*, en kunnen worden geopend met een aanroep van toohello  **RoleEnvironment.getConfigurationSettings** methode.</span><span class="sxs-lookup"><span data-stu-id="8e74a-126">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="8e74a-127">Hallo volgende voorbeeld wordt de verbindingsreeks Hallo uit een **instelling** element met de naam *StorageConnectionString* in Hallo serviceconfiguratiebestand.</span><span class="sxs-lookup"><span data-stu-id="8e74a-127">hello following example gets hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="8e74a-128">Hallo volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden tooget Hallo-opslagverbindingsreeks hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e74a-128">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="8e74a-129">Een container maken</span><span class="sxs-lookup"><span data-stu-id="8e74a-129">Create a container</span></span>
<span data-ttu-id="8e74a-130">Een **CloudBlobClient** object kunt u profiteren van reference-objecten voor containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="8e74a-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="8e74a-131">Hallo volgende code maakt een **CloudBlobClient** object.</span><span class="sxs-lookup"><span data-stu-id="8e74a-131">hello following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="8e74a-132">Er zijn extra manieren toocreate **CloudStorageAccount** objecten; voor meer informatie Zie **CloudStorageAccount** in Hallo [naslaginformatie over Azure Storage Client SDK].</span><span class="sxs-lookup"><span data-stu-id="8e74a-132">There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="8e74a-133">Gebruik Hallo **CloudBlobClient** tooget een verwijzing toohello-container die u wilt dat toouse object.</span><span class="sxs-lookup"><span data-stu-id="8e74a-133">Use hello **CloudBlobClient** object tooget a reference toohello container you want toouse.</span></span> <span data-ttu-id="8e74a-134">U kunt Hallo container maken als deze niet Hello bestaat **createIfNotExists** methode, waarbij bestaande container Hallo anders retourneert.</span><span class="sxs-lookup"><span data-stu-id="8e74a-134">You can create hello container if it doesn't exist with hello **createIfNotExists** method, which will otherwise return hello existing container.</span></span> <span data-ttu-id="8e74a-135">Hallo nieuwe container is standaard privé, dus u uw toegangssleutel voor opslag opgeven moet (zoals u eerder hebt gedaan) toodownload blobs uit deze container.</span><span class="sxs-lookup"><span data-stu-id="8e74a-135">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span>

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

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="8e74a-136">Optioneel: Een container voor openbare toegang configureren</span><span class="sxs-lookup"><span data-stu-id="8e74a-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="8e74a-137">Een container machtigingen zijn standaard geconfigureerd voor persoonlijke toegang, maar u kunt gemakkelijk een container machtigingen tooallow openbare, alleen-lezen toegang voor alle gebruikers op Hallo Internet configureren:</span><span class="sxs-lookup"><span data-stu-id="8e74a-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions tooallow public, read-only access for all users on hello Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="8e74a-138">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="8e74a-138">Upload a blob into a container</span></span>
<span data-ttu-id="8e74a-139">een bestand tooa blob tooupload een containerverwijzing ophalen en deze tooget een blobverwijzing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8e74a-139">tooupload a file tooa blob, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="8e74a-140">Zodra u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom door het aanroepen van uploaden op Hallo blobverwijzing uploaden.</span><span class="sxs-lookup"><span data-stu-id="8e74a-140">Once you have a blob reference, you can upload any stream by calling upload on hello blob reference.</span></span> <span data-ttu-id="8e74a-141">Deze bewerking wordt Hallo blob gemaakt als deze niet bestaat of overschrijven als dit het geval is.</span><span class="sxs-lookup"><span data-stu-id="8e74a-141">This operation will create hello blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="8e74a-142">Hallo volgende codevoorbeeld ziet u dit en wordt ervan uitgegaan dat Hallo-container al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8e74a-142">hello following code sample shows this, and assumes that hello container has already been created.</span></span>

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

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="8e74a-143">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="8e74a-143">List hello blobs in a container</span></span>
<span data-ttu-id="8e74a-144">toolist hello blobs in een container, eerst ophalen een containerverwijzing net zoals tooupload een blob.</span><span class="sxs-lookup"><span data-stu-id="8e74a-144">toolist hello blobs in a container, first get a container reference like you did tooupload a blob.</span></span> <span data-ttu-id="8e74a-145">U kunt Hallo-container **listBlobs** methode met een **voor** lus.</span><span class="sxs-lookup"><span data-stu-id="8e74a-145">You can use hello container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="8e74a-146">Hallo volgende code wordt de uitvoer Hallo-Uri van elke blob in een container toohello-console.</span><span class="sxs-lookup"><span data-stu-id="8e74a-146">hello following code outputs hello Uri of each blob in a container toohello console.</span></span>

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

<span data-ttu-id="8e74a-147">Houd er rekening mee dat kunt u de naam blobs met informatie over het pad in hun naam.</span><span class="sxs-lookup"><span data-stu-id="8e74a-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="8e74a-148">Hiermee maakt u een virtuele mapstructuur die u kunt ordenen en kunt doorlopen als een traditioneel bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="8e74a-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="8e74a-149">Houd er rekening mee dat Hallo mapstructuur alleen virtueel is: hello alleen bronnen beschikbaar zijn in Blob storage containers en blobs zijn.</span><span class="sxs-lookup"><span data-stu-id="8e74a-149">Note that hello directory structure is virtual only - hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="8e74a-150">Hallo-clientbibliotheek biedt echter een **CloudBlobDirectory** object toorefer tooa virtuele map en Hallo vereenvoudigen van het werken met blobs die op deze manier zijn ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="8e74a-150">However, hello client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="8e74a-151">U kan bijvoorbeeld een container met de naam 'foto's ', waarin u uploaden mogelijk blobs met de naam 'rootphoto1', ' 2010/photo1', ' 2010/photo2' en ' 2011/photo1' hebben.</span><span class="sxs-lookup"><span data-stu-id="8e74a-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="8e74a-152">Dit zou Hallo virtuele mappen '2010' en '2011' in Hallo 'foto's ' container maken.</span><span class="sxs-lookup"><span data-stu-id="8e74a-152">This would create hello virtual directories "2010" and "2011" within hello "photos" container.</span></span> <span data-ttu-id="8e74a-153">Als u aanroept **listBlobs** op Hallo 'foto's ' container, Hallo verzameling geretourneerd bevat **CloudBlobDirectory** en **CloudBlob** -objecten die Hallo vertegenwoordigen mappen en blobs op het hoogste niveau Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="8e74a-153">When you call **listBlobs** on hello "photos" container, hello collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="8e74a-154">In dit geval zou mappen '2010' en '2011', evenals photo 'rootphoto1' worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8e74a-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="8e74a-155">U kunt Hallo **instanceof** operator toodistinguish deze objecten.</span><span class="sxs-lookup"><span data-stu-id="8e74a-155">You can use hello **instanceof** operator toodistinguish these objects.</span></span>

<span data-ttu-id="8e74a-156">U kunt eventueel doorgeven in parameters toohello **listBlobs** methode Hello **useFlatBlobListing** parameter tootrue ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8e74a-156">Optionally, you can pass in parameters toohello **listBlobs** method with hello **useFlatBlobListing** parameter set tootrue.</span></span> <span data-ttu-id="8e74a-157">Dit leidt ertoe dat elke blob wordt geretourneerd, ongeacht de directory.</span><span class="sxs-lookup"><span data-stu-id="8e74a-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="8e74a-158">Zie voor meer informatie **CloudBlobContainer.listBlobs** in Hallo [naslaginformatie over Azure Storage Client SDK].</span><span class="sxs-lookup"><span data-stu-id="8e74a-158">For more information, see **CloudBlobContainer.listBlobs** in hello [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="8e74a-159">Een blob downloaden</span><span class="sxs-lookup"><span data-stu-id="8e74a-159">Download a blob</span></span>
<span data-ttu-id="8e74a-160">toodownload blobs, volgt u dezelfde stappen als u dit hebt gedaan voor het uploaden van een blob in volgorde tooget een blobverwijzing Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e74a-160">toodownload blobs, follow hello same steps as you did for uploading a blob in order tooget a blob reference.</span></span> <span data-ttu-id="8e74a-161">In Hallo voorbeeld uploaden, kunt u uploaden voor Hallo blob-object aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8e74a-161">In hello uploading example, you called upload on hello blob object.</span></span> <span data-ttu-id="8e74a-162">In de Hallo voorbeeld te volgen, roept downloaden tootransfer Hallo blob inhoud tooa stroomobject zoals een **FileOutputStream** waarmee u toopersist Hallo blob tooa lokaal bestand kunt.</span><span class="sxs-lookup"><span data-stu-id="8e74a-162">In hello following example, call download tootransfer hello blob contents tooa stream object such as a **FileOutputStream** that you can use toopersist hello blob tooa local file.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="8e74a-163">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="8e74a-163">Delete a blob</span></span>
<span data-ttu-id="8e74a-164">een blob toodelete ophalen van een blob naar verwijzen, en roept **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="8e74a-164">toodelete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="8e74a-165">Verwijderen van een blob-container</span><span class="sxs-lookup"><span data-stu-id="8e74a-165">Delete a blob container</span></span>
<span data-ttu-id="8e74a-166">Ten slotte toodelete een blobcontainer een blob ophalen containerverwijzing en aanroep **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="8e74a-166">Finally, toodelete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8e74a-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e74a-167">Next steps</span></span>
<span data-ttu-id="8e74a-168">Nu u Hallo basisprincipes van Blob storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="8e74a-168">Now that you've learned hello basics of Blob storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="8e74a-169">[Azure-opslag-SDK voor Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="8e74a-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="8e74a-170">[naslaginformatie over Azure Storage Client SDK][naslaginformatie over Azure Storage Client SDK]</span><span class="sxs-lookup"><span data-stu-id="8e74a-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="8e74a-171">[REST API van Azure Storage][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="8e74a-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="8e74a-172">[Azure Storage-teamblog][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="8e74a-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="8e74a-173">Zie voor meer informatie, ook Hallo [Java Developer Center](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="8e74a-173">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[naslaginformatie over Azure Storage Client SDK]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
