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
# <a name="how-toouse-blob-storage-from-php"></a>Hoe toouse blob-opslag met PHP
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Overzicht
Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat. In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen. BLOB-opslag is ook bedoeld tooas vorm van objectopslag.

Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van hello Azure blob-service. Hallo-voorbeelden zijn geschreven in PHP en gebruiken van Hallo [Azure SDK voor PHP][download]. Hallo scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs. Zie voor meer informatie over blobs Hallo [Vervolgstappen](#next-steps) sectie.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Een PHP-toepassing maken
alleen de vereiste voor het maken van een PHP-toepassing die toegang heeft tot hello Azure blob-service is Hallo Hallo verwijst naar klassen in hello Azure SDK voor PHP vanuit uw code. U kunt extra ontwikkeling toocreate uw toepassing, met inbegrip van Kladblok gebruiken.

In deze handleiding gebruikt u servicefuncties, die kunnen worden aangeroepen binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure-clientbibliotheken ophalen
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>Uw toepassing tooaccess Hallo blob-service configureren
toouse hello Azure blob-service API's, moet u:

1. Hallo autoloader referentiebestand Hallo met [require_once] -instructie en
2. Verwijst naar alle klassen die u kunt gebruiken.

Hallo volgende voorbeeld laat zien hoe tooinclude autoloader bestands- en Hallo Hallo **ServicesBuilder** klasse.

> [!NOTE]
> Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u Hallo PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd. Als u handmatig Hallo bibliotheken geïnstalleerd, moet u tooreference hello `WindowsAzure.php` autoloader-bestand.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

In onderstaande Hallo voorbeelden, Hallo `require_once` instructie altijd worden weergegeven, maar alleen Hallo klassen nodig zijn voor Hallo voorbeeld tooexecute wordt verwezen.

## <a name="set-up-an-azure-storage-connection"></a>Een Azure-opslag-verbinding instellen
een Azure blob-serviceclient tooinstantiate, moet u eerst een geldige verbindingsreeks hebben. Hallo-indeling voor Hallo blob-service-verbindingsreeks is:

Voor toegang tot een service voor live:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Voor toegang tot Hallo-opslagemulator:

```php
UseDevelopmentStorage=true
```

toocreate een Azure-service-client, moet u toouse hello **ServicesBuilder** klasse. U kunt:

* Hallo verbinding doorgeven string rechtstreeks tooit of
* Gebruik Hallo **CloudConfigurationManager (CCM)** toocheck meerdere externe voor Hallo-verbindingsreeks gegevensbronnen:
  * Standaard wordt geleverd met ondersteuning voor een externe bron - omgevingsvariabelen.
  * U kunt nieuwe bronnen toevoegen door uit te breiden Hallo **ConnectionStringSource** klasse.

Voor Hallo voorbeelden die hier wordt beschreven, worden de verbindingsreeks Hallo rechtstreeks doorgegeven.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>Een container maken
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Een **BlobRestProxy** object kunt u een blob-container maken met de Hallo **createContainer** methode. Bij het maken van een container, kunt u opties voor Hallo-container instellen, maar dit is dus niet vereist. (Hallo voorbeeld hieronder ziet u hoe tooset Hallo container toegang tot de toegangsbeheerlijst (ACL) en metagegevens van de container.)

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

Het aanroepen van **setPublicAccess (PublicAccessType::CONTAINER\_en\_BLOBS)** maakt Hallo-container en blob gegevens toegankelijk via anonieme aanvragen. Het aanroepen van **setPublicAccess(PublicAccessType::BLOBS_ONLY)** zorgt ervoor dat alleen blob-gegevens toegankelijk via anonieme aanvragen. Zie voor meer informatie over de container-ACL's, [Set container-ACL (REST-API)][container-acl].

Zie voor meer informatie over foutcodes voor Blob-service [foutcodes voor Blob-Service][error-codes].

## <a name="upload-a-blob-into-a-container"></a>Een blob uploaden naar een container
een bestand op als een blob, gebruik Hallo tooupload **BlobRestProxy -> createBlockBlob** methode. Deze bewerking wordt Hallo blob gemaakt als deze niet bestaat, of deze wordt overschreven als dit het geval is. Hallo voorbeeld hieronder wordt ervan uitgegaan dat Hallo-container is al gemaakt en gebruikt [fopen] [ fopen] tooopen Hallo-bestand als een stroom.

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

Houd er rekening mee dat Hallo vorige voorbeeld een blob als een stream uploadt. Een blob kan echter ook worden geüpload als een tekenreeks met bijvoorbeeld Hallo [bestand\_ophalen\_inhoud] [ file_get_contents] functie. toodo deze wijzigen met behulp van het vorige voorbeeld Hallo `$content = fopen("c:\myfile.txt", "r");` te`$content = file_get_contents("c:\myfile.txt");`.

## <a name="list-hello-blobs-in-a-container"></a>Lijst Hallo blobs in een container
toolist hello blobs in een container gebruiken Hallo **BlobRestProxy -> listBlobs** methode met een **foreach** tooloop via Hallo resultaat in een lus. Hallo volgende code Hallo-naam van elke blob weergegeven als u in een container en de URI toohello browser wordt weergegeven.

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

## <a name="download-a-blob"></a>Een blob downloaden
toodownload een blob aanroep Hallo **BlobRestProxy -> getBlob** methode en vervolgens aanroep Hallo **getContentStream** methode op Hallo resulterende **GetBlobResult** object.

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

Houd er rekening mee dat bovenstaande Hallo-voorbeeld een blob opgehaald als een resource stroom (Hallo standaardgedrag). U kunt echter hello gebruiken [stroom\_ophalen\_inhoud] [ stream-get-contents] functie tooconvert Hallo stroom tooa tekenreeks geretourneerd.

## <a name="delete-a-blob"></a>Een blob verwijderen
toodelete een blob Hallo containernaam en blob-naam te geven**BlobRestProxy -> deleteBlob**.

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

## <a name="delete-a-blob-container"></a>Verwijderen van een blob-container
Ten slotte doorgeven toodelete een blob-container Hallo containernaam te**BlobRestProxy -> deleteContainer**.

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

## <a name="next-steps"></a>Volgende stappen
Nu u de basisbeginselen Hallo van hello Azure blob-service hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.

* Ga naar Hallo [Azure Storage-teamblog](http://blogs.msdn.com/b/windowsazurestorage/)
* Zie Hallo [PHP blok-blob voorbeeld](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).
* Zie Hallo [PHP pagina-blob voorbeeld](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).
* [Gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md)

Zie voor meer informatie, ook Hallo [PHP-ontwikkelaarscentrum](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
