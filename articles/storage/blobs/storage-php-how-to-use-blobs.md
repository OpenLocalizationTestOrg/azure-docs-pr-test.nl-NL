---
title: Het gebruik van blob storage (objectopslag) met PHP | Microsoft Docs
description: Sla niet-gestructureerde gegevens op in de cloud met Azure Blob Storage (objectopslag).
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 4b68844c5d0553eaede3997bf09bff4fe570e850
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-php"></a><span data-ttu-id="5e6c3-103">Het blob storage gebruiken met PHP</span><span class="sxs-lookup"><span data-stu-id="5e6c3-103">How to use blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="5e6c3-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5e6c3-104">Overview</span></span>
<span data-ttu-id="5e6c3-105">Azure Blob Storage is een service waarmee ongestructureerde gegevens als objecten/blobs worden opgeslagen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="5e6c3-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="5e6c3-107">U kunt Blob Storage zien als een vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="5e6c3-108">Deze handleiding wordt getoond hoe u veelvoorkomende scenario's met behulp van de Azure blob-service uitvoert.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-108">This guide shows you how to perform common scenarios using the Azure blob service.</span></span> <span data-ttu-id="5e6c3-109">De voorbeelden zijn geschreven in PHP en gebruik de [Azure SDK voor PHP][download].</span><span class="sxs-lookup"><span data-stu-id="5e6c3-109">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="5e6c3-110">De scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="5e6c3-111">Zie voor meer informatie over blobs de [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-111">For more information on blobs, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="5e6c3-112">Een PHP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="5e6c3-112">Create a PHP application</span></span>
<span data-ttu-id="5e6c3-113">De enige vereiste voor het maken van een PHP-toepassing die toegang heeft tot de Azure blob-service is de verwijzende klassen in de Azure SDK voor PHP vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-113">The only requirement for creating a PHP application that accesses the Azure blob service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="5e6c3-114">Alle ontwikkelingsprogramma's kunt u uw toepassing, met inbegrip van Kladblok maken.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="5e6c3-115">In deze handleiding gebruikt u servicefuncties, die kunnen worden aangeroepen binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="5e6c3-116">De clientbibliotheken van Azure ophalen</span><span class="sxs-lookup"><span data-stu-id="5e6c3-116">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-blob-service"></a><span data-ttu-id="5e6c3-117">Uw toepassing configureren voor toegang tot de blob-service</span><span class="sxs-lookup"><span data-stu-id="5e6c3-117">Configure your application to access the blob service</span></span>
<span data-ttu-id="5e6c3-118">Voor het gebruik van de Azure blob-service API's, moet u:</span><span class="sxs-lookup"><span data-stu-id="5e6c3-118">To use the Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="5e6c3-119">Verwijst naar de autoloader-bestand met de [require_once] -instructie en</span><span class="sxs-lookup"><span data-stu-id="5e6c3-119">Reference the autoloader file using the [require_once] statement, and</span></span>
2. <span data-ttu-id="5e6c3-120">Verwijst naar alle klassen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-120">Reference any classes you might use.</span></span>

<span data-ttu-id="5e6c3-121">Het volgende voorbeeld laat zien hoe de autoloader-bestand en de verwijzing naar de **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-121">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="5e6c3-122">De voorbeelden in dit artikel wordt ervan uitgegaan dat u de PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-122">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="5e6c3-123">Als u handmatig de bibliotheken geïnstalleerd, moet u verwijzen naar de `WindowsAzure.php` autoloader-bestand.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-123">If you installed the libraries manually, you need to reference the `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="5e6c3-124">In de onderstaande voorbeelden de `require_once` instructie altijd worden weergegeven, maar alleen de klassen die nodig zijn voor het voorbeeld uit te voeren naar worden verwezen.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-124">In the examples below, the `require_once` statement will be shown always, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="5e6c3-125">Een Azure-opslag-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="5e6c3-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="5e6c3-126">U moet een geldige verbindingsreeks hebben voor het concretiseren van een Azure blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-126">To instantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="5e6c3-127">De indeling voor de verbindingsreeks van de blob-service is:</span><span class="sxs-lookup"><span data-stu-id="5e6c3-127">The format for the blob service connection string is:</span></span>

<span data-ttu-id="5e6c3-128">Voor toegang tot een service voor live:</span><span class="sxs-lookup"><span data-stu-id="5e6c3-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="5e6c3-129">Voor toegang tot de opslagemulator:</span><span class="sxs-lookup"><span data-stu-id="5e6c3-129">For accessing the storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="5e6c3-130">Voor het maken van een Azure-service-client die u wilt gebruiken, de **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-130">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="5e6c3-131">U kunt:</span><span class="sxs-lookup"><span data-stu-id="5e6c3-131">You can:</span></span>

* <span data-ttu-id="5e6c3-132">de verbindingsreeks rechtstreeks aan deze doorgeven of</span><span class="sxs-lookup"><span data-stu-id="5e6c3-132">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="5e6c3-133">Gebruik de **CloudConfigurationManager (CCM)** om te controleren van meerdere externe bronnen voor de verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="5e6c3-133">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="5e6c3-134">Standaard wordt geleverd met ondersteuning voor een externe bron - omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="5e6c3-135">U kunt nieuwe bronnen toevoegen door het uitbreiden van de **ConnectionStringSource** klasse.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-135">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="5e6c3-136">Voor de voorbeelden die hier wordt beschreven, worden de verbindingsreeks rechtstreeks doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-136">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="5e6c3-137">Een container maken</span><span class="sxs-lookup"><span data-stu-id="5e6c3-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="5e6c3-138">Een **BlobRestProxy** object maakt u een blob-container met de **createContainer** methode.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-138">A **BlobRestProxy** object lets you create a blob container with the **createContainer** method.</span></span> <span data-ttu-id="5e6c3-139">Bij het maken van een container, kunt u opties voor de container instellen, maar dit is dus niet vereist.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-139">When creating a container, you can set options on the container, but doing so is not required.</span></span> <span data-ttu-id="5e6c3-140">(Het voorbeeld hieronder ziet u het instellen van de container toegangsbeheerlijst (ACL) en de metagegevens van de container.)</span><span class="sxs-lookup"><span data-stu-id="5e6c3-140">(The example below shows how to set the container access control list (ACL) and container metadata.)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within the container via anonymous
// request, but cannot enumerate containers within the storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within the container via
// anonymous request.
// If this value is not specified in the request, container data is
// private to the account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="5e6c3-141">Het aanroepen van **setPublicAccess (PublicAccessType::CONTAINER\_en\_BLOBS)** toegankelijk via anonieme aanvragen maakt van de container en de blob-gegevens.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes the container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="5e6c3-142">Het aanroepen van **setPublicAccess(PublicAccessType::BLOBS_ONLY)** zorgt ervoor dat alleen blob-gegevens toegankelijk via anonieme aanvragen.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="5e6c3-143">Zie voor meer informatie over de container-ACL's, [Set container-ACL (REST-API)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="5e6c3-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="5e6c3-144">Zie voor meer informatie over foutcodes voor Blob-service [foutcodes voor Blob-Service][error-codes].</span><span class="sxs-lookup"><span data-stu-id="5e6c3-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="5e6c3-145">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="5e6c3-145">Upload a blob into a container</span></span>
<span data-ttu-id="5e6c3-146">Als u wilt een bestand als een blob uploadt, gebruiken de **BlobRestProxy -> createBlockBlob** methode.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-146">To upload a file as a blob, use the **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="5e6c3-147">Deze bewerking wordt de blob gemaakt als deze niet bestaat, of deze wordt overschreven als dit het geval is.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-147">This operation creates the blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="5e6c3-148">In het onderstaande voorbeeld wordt ervan uitgegaan dat de container al gemaakt is en maakt gebruik van [fopen] [ fopen] naar het bestand openen als een stroom.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-148">The code example below assumes that the container has already been created and uses [fopen][fopen] to open the file as a stream.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="5e6c3-149">Houd er rekening mee dat het vorige voorbeeld een blob als een stream uploadt.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-149">Note that the previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="5e6c3-150">Echter, een blob kan ook worden geüpload als een tekenreeks met bijvoorbeeld de [bestand\_ophalen\_inhoud] [ file_get_contents] functie.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-150">However, a blob can also be uploaded as a string using, for example, the [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="5e6c3-151">U doet dit met behulp van het vorige voorbeeld door wijzigen `$content = fopen("c:\myfile.txt", "r");` naar `$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-151">To do this using the previous sample, change `$content = fopen("c:\myfile.txt", "r");` to `$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="5e6c3-152">De blobs in een container in een lijst weergeven</span><span class="sxs-lookup"><span data-stu-id="5e6c3-152">List the blobs in a container</span></span>
<span data-ttu-id="5e6c3-153">Als de blobs in een container wilt weergeven, gebruikt de **BlobRestProxy -> listBlobs** methode met een **foreach** lus via het resultaat.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-153">To list the blobs in a container, use the **BlobRestProxy->listBlobs** method with a **foreach** loop to loop through the result.</span></span> <span data-ttu-id="5e6c3-154">De volgende code wordt de naam van elke blob als uitvoer in een container en wordt de URI voor de browser.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-154">The following code displays the name of each blob as output in a container and displays its URI to the browser.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a><span data-ttu-id="5e6c3-155">Een blob downloaden</span><span class="sxs-lookup"><span data-stu-id="5e6c3-155">Download a blob</span></span>
<span data-ttu-id="5e6c3-156">Aanroepen voor het downloaden van een blob, de **BlobRestProxy -> getBlob** methode, roept u vervolgens de **getContentStream** methode op de resulterende **GetBlobResult** object.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-156">To download a blob, call the **BlobRestProxy->getBlob** method, then call the **getContentStream** method on the resulting **GetBlobResult** object.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="5e6c3-157">Houd er rekening mee dat het bovenstaande voorbeeld een blob opgehaald als de bron van een stroom (de standaardinstelling).</span><span class="sxs-lookup"><span data-stu-id="5e6c3-157">Note that the example above gets a blob as a stream resource (the default behavior).</span></span> <span data-ttu-id="5e6c3-158">U kunt echter de [stroom\_ophalen\_inhoud] [ stream-get-contents] functioneren op de geretourneerde stroom niet converteren naar een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-158">However, you can use the [stream\_get\_contents][stream-get-contents] function to convert the returned stream to a string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="5e6c3-159">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="5e6c3-159">Delete a blob</span></span>
<span data-ttu-id="5e6c3-160">Geeft de containernaam en blob in voor het verwijderen van een blob **BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-160">To delete a blob, pass the container name and blob name to **BlobRestProxy->deleteBlob**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="5e6c3-161">Verwijderen van een blob-container</span><span class="sxs-lookup"><span data-stu-id="5e6c3-161">Delete a blob container</span></span>
<span data-ttu-id="5e6c3-162">Ten slotte voor het verwijderen van een blob-container, geeft de containernaam van de aan **BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-162">Finally, to delete a blob container, pass the container name to **BlobRestProxy->deleteContainer**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="5e6c3-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e6c3-163">Next steps</span></span>
<span data-ttu-id="5e6c3-164">Nu dat u de basisprincipes van de Azure blob-service hebt geleerd, volgt u deze koppelingen voor meer informatie over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="5e6c3-164">Now that you've learned the basics of the Azure blob service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="5e6c3-165">Ga naar de [Azure Storage-teamblog](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="5e6c3-165">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="5e6c3-166">Zie de [PHP blok-blob voorbeeld](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="5e6c3-166">See the [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="5e6c3-167">Zie de [PHP pagina-blob voorbeeld](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="5e6c3-167">See the [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="5e6c3-168">Gegevensoverdracht met het AzCopy-opdrachtregelprogramma</span><span class="sxs-lookup"><span data-stu-id="5e6c3-168">Transfer data with the AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

<span data-ttu-id="5e6c3-169">Zie voor meer informatie, ook de [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="5e6c3-169">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
