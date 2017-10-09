---
title: aaaHow toouse blob storage (objectopslag) met PHP | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
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
ms.openlocfilehash: 331405e583c17c4f71acacdc0078b2bc71efbef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="02f79-103">Hoe toouse blob-opslag met PHP</span><span class="sxs-lookup"><span data-stu-id="02f79-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="02f79-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="02f79-104">Overview</span></span>
<span data-ttu-id="02f79-105">Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat.</span><span class="sxs-lookup"><span data-stu-id="02f79-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="02f79-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="02f79-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="02f79-107">BLOB-opslag is ook bedoeld tooas vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="02f79-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="02f79-108">Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van hello Azure blob-service.</span><span class="sxs-lookup"><span data-stu-id="02f79-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="02f79-109">Hallo-voorbeelden zijn geschreven in PHP en gebruiken van Hallo [Azure SDK voor PHP][download].</span><span class="sxs-lookup"><span data-stu-id="02f79-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="02f79-110">Hallo scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs.</span><span class="sxs-lookup"><span data-stu-id="02f79-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="02f79-111">Zie voor meer informatie over blobs Hallo [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="02f79-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="02f79-112">Een PHP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="02f79-112">Create a PHP application</span></span>
<span data-ttu-id="02f79-113">alleen de vereiste voor het maken van een PHP-toepassing die toegang heeft tot hello Azure blob-service is Hallo Hallo verwijst naar klassen in hello Azure SDK voor PHP vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="02f79-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="02f79-114">U kunt extra ontwikkeling toocreate uw toepassing, met inbegrip van Kladblok gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02f79-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="02f79-115">In deze handleiding gebruikt u servicefuncties, die kunnen worden aangeroepen binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.</span><span class="sxs-lookup"><span data-stu-id="02f79-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="02f79-116">Hello Azure-clientbibliotheken ophalen</span><span class="sxs-lookup"><span data-stu-id="02f79-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="02f79-117">Uw toepassing tooaccess Hallo blob-service configureren</span><span class="sxs-lookup"><span data-stu-id="02f79-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="02f79-118">toouse hello Azure blob-service API's, moet u:</span><span class="sxs-lookup"><span data-stu-id="02f79-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="02f79-119">Hallo autoloader referentiebestand Hallo met [require_once] -instructie en</span><span class="sxs-lookup"><span data-stu-id="02f79-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="02f79-120">Verwijst naar alle klassen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02f79-120">Reference any classes you might use.</span></span>

<span data-ttu-id="02f79-121">Hallo volgende voorbeeld laat zien hoe tooinclude autoloader bestands- en Hallo Hallo **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="02f79-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="02f79-122">Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u Hallo PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="02f79-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="02f79-123">Als u handmatig Hallo bibliotheken geïnstalleerd, moet u tooreference hello `WindowsAzure.php` autoloader-bestand.</span><span class="sxs-lookup"><span data-stu-id="02f79-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="02f79-124">In onderstaande Hallo voorbeelden, Hallo `require_once` instructie altijd worden weergegeven, maar alleen Hallo klassen nodig zijn voor Hallo voorbeeld tooexecute wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="02f79-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="02f79-125">Een Azure-opslag-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="02f79-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="02f79-126">een Azure blob-serviceclient tooinstantiate, moet u eerst een geldige verbindingsreeks hebben.</span><span class="sxs-lookup"><span data-stu-id="02f79-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="02f79-127">Hallo-indeling voor Hallo blob-service-verbindingsreeks is:</span><span class="sxs-lookup"><span data-stu-id="02f79-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="02f79-128">Voor toegang tot een service voor live:</span><span class="sxs-lookup"><span data-stu-id="02f79-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="02f79-129">Voor toegang tot Hallo-opslagemulator:</span><span class="sxs-lookup"><span data-stu-id="02f79-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="02f79-130">toocreate een Azure-service-client, moet u toouse hello **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="02f79-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="02f79-131">U kunt:</span><span class="sxs-lookup"><span data-stu-id="02f79-131">You can:</span></span>

* <span data-ttu-id="02f79-132">Hallo verbinding doorgeven string rechtstreeks tooit of</span><span class="sxs-lookup"><span data-stu-id="02f79-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="02f79-133">Gebruik Hallo **CloudConfigurationManager (CCM)** toocheck meerdere externe voor Hallo-verbindingsreeks gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="02f79-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="02f79-134">Standaard wordt geleverd met ondersteuning voor een externe bron - omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="02f79-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="02f79-135">U kunt nieuwe bronnen toevoegen door uit te breiden Hallo **ConnectionStringSource** klasse.</span><span class="sxs-lookup"><span data-stu-id="02f79-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="02f79-136">Voor Hallo voorbeelden die hier wordt beschreven, worden de verbindingsreeks Hallo rechtstreeks doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="02f79-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="02f79-137">Een container maken</span><span class="sxs-lookup"><span data-stu-id="02f79-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="02f79-138">Een **BlobRestProxy** object kunt u een blob-container maken met de Hallo **createContainer** methode.</span><span class="sxs-lookup"><span data-stu-id="02f79-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="02f79-139">Bij het maken van een container, kunt u opties voor Hallo-container instellen, maar dit is dus niet vereist.</span><span class="sxs-lookup"><span data-stu-id="02f79-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="02f79-140">(Hallo voorbeeld hieronder ziet u hoe tooset Hallo container toegang tot de toegangsbeheerlijst (ACL) en metagegevens van de container.)</span><span class="sxs-lookup"><span data-stu-id="02f79-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

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
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
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

<span data-ttu-id="02f79-141">Het aanroepen van **setPublicAccess (PublicAccessType::CONTAINER\_en\_BLOBS)** maakt Hallo-container en blob gegevens toegankelijk via anonieme aanvragen.</span><span class="sxs-lookup"><span data-stu-id="02f79-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="02f79-142">Het aanroepen van **setPublicAccess(PublicAccessType::BLOBS_ONLY)** zorgt ervoor dat alleen blob-gegevens toegankelijk via anonieme aanvragen.</span><span class="sxs-lookup"><span data-stu-id="02f79-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="02f79-143">Zie voor meer informatie over de container-ACL's, [Set container-ACL (REST-API)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="02f79-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="02f79-144">Zie voor meer informatie over foutcodes voor Blob-service [foutcodes voor Blob-Service][error-codes].</span><span class="sxs-lookup"><span data-stu-id="02f79-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="02f79-145">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="02f79-145">Upload a blob into a container</span></span>
<span data-ttu-id="02f79-146">een bestand op als een blob, gebruik Hallo tooupload **BlobRestProxy -> createBlockBlob** methode.</span><span class="sxs-lookup"><span data-stu-id="02f79-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="02f79-147">Deze bewerking wordt Hallo blob gemaakt als deze niet bestaat, of deze wordt overschreven als dit het geval is.</span><span class="sxs-lookup"><span data-stu-id="02f79-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="02f79-148">Hallo voorbeeld hieronder wordt ervan uitgegaan dat Hallo-container is al gemaakt en gebruikt [fopen] [ fopen] tooopen Hallo-bestand als een stroom.</span><span class="sxs-lookup"><span data-stu-id="02f79-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

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

<span data-ttu-id="02f79-149">Houd er rekening mee dat Hallo vorige voorbeeld een blob als een stream uploadt.</span><span class="sxs-lookup"><span data-stu-id="02f79-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="02f79-150">Een blob kan echter ook worden geüpload als een tekenreeks met bijvoorbeeld Hallo [bestand\_ophalen\_inhoud] [ file_get_contents] functie.</span><span class="sxs-lookup"><span data-stu-id="02f79-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="02f79-151">toodo deze wijzigen met behulp van het vorige voorbeeld Hallo `$content = fopen("c:\myfile.txt", "r");` te`$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="02f79-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="02f79-152">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="02f79-152">List hello blobs in a container</span></span>
<span data-ttu-id="02f79-153">toolist hello blobs in een container gebruiken Hallo **BlobRestProxy -> listBlobs** methode met een **foreach** tooloop via Hallo resultaat in een lus.</span><span class="sxs-lookup"><span data-stu-id="02f79-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="02f79-154">Hallo volgende code Hallo-naam van elke blob weergegeven als u in een container en de URI toohello browser wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02f79-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="02f79-155">Een blob downloaden</span><span class="sxs-lookup"><span data-stu-id="02f79-155">Download a blob</span></span>
<span data-ttu-id="02f79-156">toodownload een blob aanroep Hallo **BlobRestProxy -> getBlob** methode en vervolgens aanroep Hallo **getContentStream** methode op Hallo resulterende **GetBlobResult** object.</span><span class="sxs-lookup"><span data-stu-id="02f79-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="02f79-157">Houd er rekening mee dat bovenstaande Hallo-voorbeeld een blob opgehaald als een resource stroom (Hallo standaardgedrag).</span><span class="sxs-lookup"><span data-stu-id="02f79-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="02f79-158">U kunt echter hello gebruiken [stroom\_ophalen\_inhoud] [ stream-get-contents] functie tooconvert Hallo stroom tooa tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="02f79-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="02f79-159">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="02f79-159">Delete a blob</span></span>
<span data-ttu-id="02f79-160">toodelete een blob Hallo containernaam en blob-naam te geven**BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="02f79-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="02f79-161">Verwijderen van een blob-container</span><span class="sxs-lookup"><span data-stu-id="02f79-161">Delete a blob container</span></span>
<span data-ttu-id="02f79-162">Ten slotte doorgeven toodelete een blob-container Hallo containernaam te**BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="02f79-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="02f79-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02f79-163">Next steps</span></span>
<span data-ttu-id="02f79-164">Nu u de basisbeginselen Hallo van hello Azure blob-service hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="02f79-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="02f79-165">Ga naar Hallo [Azure Storage-teamblog](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="02f79-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="02f79-166">Zie Hallo [PHP blok-blob voorbeeld](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="02f79-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="02f79-167">Zie Hallo [PHP pagina-blob voorbeeld](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="02f79-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="02f79-168">Gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo</span><span class="sxs-lookup"><span data-stu-id="02f79-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="02f79-169">Zie voor meer informatie, ook Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="02f79-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
