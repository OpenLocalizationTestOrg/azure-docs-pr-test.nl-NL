---
title: aaaHow toouse Blob-opslag met Node.js | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e405eecdc60cd1eaa77510e7b29b41269372b65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>Hoe toouse Blob-opslag met Node.js
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Overzicht
Dit artikel ziet u hoe tooperform algemene scenario's met behulp van Blob-opslag. Hallo-voorbeelden zijn geschreven via Hallo Node.js-API. Hallo scenario's worden behandeld bevatten hoe tooupload, weergeven, downloaden en verwijderen van blobs.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Een Node.js-toepassing maken
Voor instructies over het toocreate een Node.js-toepassing Zie [een Node.js-web-app maken in Azure App Service], [bouwen en implementeren van een Node.js-toepassing tooan Azure Cloud Service] --met Windows PowerShell , of [bouwen en implementeren van een Node.js web-app tooAzure met behulp van Web Matrix].

## <a name="configure-your-application-tooaccess-storage"></a>Uw toepassing tooaccess opslag configureren
toouse Azure-opslag, moet u hello Azure-opslag-SDK voor Node.js, waaronder een set van gemak bibliotheken die met de Hallo storage REST-services communiceren.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Knooppunt Package Manager (NPM) tooobtain Hallo pakket gebruiken
1. Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix) toonavigate toohello map waar u uw voorbeeld hebt gemaakt. de toepassing.
2. Type **npm Installeer azure-opslag** in Hallo-opdrachtvenster. Uitvoer van de opdracht Hallo is vergelijkbaar toohello volgende codevoorbeeld.

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. U kunt handmatig uitvoeren Hallo **ls** tooverify opdracht die een **knooppunt\_modules** map is gemaakt. Hallo zoeken in die map **azure-opslag** , dit pakket bevat, moet u tooaccess opslag Hallo-bibliotheken.

### <a name="import-hello-package"></a>Hallo-pakket importeren
Hallo toohello bovenaan hello te volgen in Kladblok of een andere teksteditor toevoegen **server.js** -bestand van de toepassing hello waar u van plan toouse opslag bent:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Een Azure Storage-verbinding instellen
Hello Azure-module lezen Hallo omgevingsvariabelen `AZURE_STORAGE_ACCOUNT` en `AZURE_STORAGE_ACCESS_KEY`, of `AZURE_STORAGE_CONNECTION_STRING`, vereist tooconnect tooyour Azure storage-account voor meer informatie. Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo opgeven bij het aanroepen van **createBlobService**.

Voor een voorbeeld van het Hallo-omgevingsvariabelen instellen in Hallo [Azure-portal](https://portal.azure.com) Zie voor een Azure-web-app [Node.js web app met behulp van hello Azure Table-Service].

## <a name="create-a-container"></a>Een container maken
Hallo **BlobService** object kunt u samenwerken met containers en blobs. Hallo volgende code maakt een **BlobService** object. Voeg de volgende Hallo aan de bovenkant Hallo van **server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> U kunt toegang tot een blob anoniem met **createBlobServiceAnonymous** en het adres van de host Hallo geven. Bijvoorbeeld: `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Gebruik een nieuwe container toocreate **createContainerIfNotExists**. Hallo maakt volgende codevoorbeeld een nieuwe container met de naam 'mycontainer':

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

Als het Hallo-container pas is gemaakt, `result.created` is ingesteld op true. Als het Hallo-container bestaat al, `result.created` is ingesteld op false. `response`bevat informatie over het Hallo-bewerking, inclusief Hallo ETag-informatie voor Hallo-container.

### <a name="container-security"></a>Beveiliging van de container
Standaard worden nieuwe containers privé zijn en kunnen niet anoniem worden gebruikt. toomake hello container openbare zodat u toegang hebt tot het anoniem, kunt u instellen toegangsniveau Hallo-container te**blob** of **container**.

* **BLOB** -kunnen anonieme leestoegang tooblob inhoud en metagegevens in deze container, maar niet toocontainer metagegevens zoals het weergeven van alle blobs in een container
* **container** -kunnen anonieme leestoegang tooblob inhoud en metagegevens, evenals de metagegevens van de container

Hallo volgende codevoorbeeld toont instelling Hallo toegangsniveau te**blob**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

U kunt ook Hallo toegangsniveau van een container wijzigen met behulp van **setContainerAcl** toospecify Hallo-toegangsniveau. Hallo volgende code voorbeeld wijzigingen Hallo toegang niveau toocontainer:

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

Hallo resultaat bevat informatie over het Hallo-bewerking, met inbegrip van Hallo stroom **ETag** voor Hallo-container.

### <a name="filters"></a>Filters
U kunt toepassen optionele filteren operations toooperations uitgevoerd met behulp van **BlobService**. Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met Hallo handtekening te implementeren:

```nodejs
function handle (requestOptions, next)
```

Hierna moet u de voorverwerking op Hallo aanvraag opties, moet Hallo-methode toocall 'volgende' doorgeven van een retouraanroep Hello handtekening te volgen:

```nodejs
function (returnObject, finalCallback, next)
```

In deze retouraanroep en na het verwerken van Hallo returnObject (Hallo reactie van Hallo aanvraag toohello server), Hallo callback tooeither moet vervolgens aanroepen als deze bestaat toocontinue verwerking van andere filters of gewoon finalCallback tooend Hallo service aanroepen aanroep.

Twee filters die Pogingslogica implementeren zijn opgenomen in hello Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**. Hallo volgende maakt een **BlobService** object dat gebruikmaakt van Hallo **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>Een blob uploaden naar een container
Er zijn drie typen blobs: blok-blobs, pagina-blobs en toevoeg-blobs. Blok-blobs kunnen u toomore efficiënt grote hoeveelheden gegevens te uploaden. Toevoeg-blobs zijn geoptimaliseerd voor toevoegbewerkingen. Pagina-blobs zijn geoptimaliseerd voor lees-en schrijfbewerkingen. Zie voor meer informatie [blok-Blobs, toevoeg-Blobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).

### <a name="block-blobs"></a>Blok-blobs
tooupload gegevens tooa blok-blob, gebruik hello te volgen:

* **createBlockBlobFromLocalFile** - maakt een nieuw blok-blob en uploadt Hallo inhoud van een bestand
* **createBlockBlobFromStream** - maakt een nieuw blok-blob en uploadt Hallo inhoud van een stream
* **createBlockBlobFromText** - maakt een nieuw blok-blob en uploadt Hallo inhoud van een tekenreeks
* **createWriteStreamToBlockBlob** -biedt een schrijven stroom tooa blok-blob

Hallo volgende codevoorbeeld uploadt Hallo inhoud Hallo **test.txt** bestand naar **myblob**.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

Hallo `result` geretourneerd door deze methoden bevat informatie over het Hallo-bewerking, zoals Hallo **ETag** van Hallo blob.

### <a name="append-blobs"></a>Toevoeg-blobs
tooupload gegevens tooa nieuwe toevoeg-blob, Hallo volgende gebruiken:

* **createAppendBlobFromLocalFile** - maakt een nieuwe toevoeg-blob en uploadt Hallo inhoud van een bestand
* **createAppendBlobFromStream** - maakt een nieuwe toevoeg-blob en uploadt Hallo inhoud van een stream
* **createAppendBlobFromText** - maakt een nieuwe toevoeg-blob en uploadt Hallo inhoud van een tekenreeks
* **createWriteStreamToNewAppendBlob** - maakt een nieuwe toevoeg-blob en geeft vervolgens een stroom toowrite tooit

Hallo volgende codevoorbeeld uploadt Hallo inhoud Hallo **test.txt** bestand naar **myappendblob**.

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend een blok tooan bestaande toevoeg-blob, gebruik hello te volgen:

* **appendFromLocalFile** -Hallo inhoud toevoegen van een bestand tooan bestaande toevoeg-blob
* **appendFromStream** -Hallo inhoud toevoegen van een stroom tooan bestaande toevoeg-blob
* **appendFromText** -Hallo inhoud toevoegen van een tekenreeks tooan bestaande toevoeg-blob
* **appendBlockFromStream** -Hallo inhoud toevoegen van een stroom tooan bestaande toevoeg-blob
* **appendBlockFromText** -Hallo inhoud toevoegen van een tekenreeks tooan bestaande toevoeg-blob

> [!NOTE]
> appendFromXXX API's worden sommige clientzijde validatie toofail snelle tooavoid onnodige server aanroepen doen. appendBlockFromXXX niet het geval.
>
>

Hallo volgende codevoorbeeld uploadt Hallo inhoud Hallo **test.txt** bestand naar **myappendblob**.

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>Pagina-blobs
tooupload gegevens tooa pagina-blob, gebruik hello te volgen:

* **createPageBlob** -maakt een nieuwe pagina-blob met een specifieke lengte
* **createPageBlobFromLocalFile** - maakt een nieuwe pagina-blob en uploadt Hallo inhoud van een bestand
* **createPageBlobFromStream** - maakt een nieuwe pagina-blob en uploadt Hallo inhoud van een stream
* **createWriteStreamToExistingPageBlob** -biedt een schrijven stroom tooan bestaande pagina-blob
* **createWriteStreamToNewPageBlob** - maakt een nieuwe pagina-blob en geeft vervolgens een stroom toowrite tooit

Hallo volgende codevoorbeeld uploadt Hallo inhoud Hallo **test.txt** bestand naar **mypageblob**.

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> Pagina-blobs bestaan uit 512-byte 'pages'. U ontvangt een fout opgetreden tijdens het uploaden van gegevens met een grootte die is geen veelvoud van 512 bytes.
>
>

## <a name="list-hello-blobs-in-a-container"></a>Lijst Hallo blobs in een container
toolist hello blobs in een container gebruiken Hallo **listBlobsSegmented** methode. Als u de blobs tooreturn met een specifieke voorvoegsel wilt, gebruik **listBlobsSegmentedWithPrefix**.

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

Hallo `result` bevat een `entries` verzameling, die is een matrix met objecten die een beschrijving van elke blob. Als u alle blobs kunnen niet worden geretourneerd, Hallo `result` biedt ook een `continuationToken`, die u kunt als Hallo tweede parameter tooretrieve extra vermeldingen.

## <a name="download-blobs"></a>Blobs downloaden
toodownload gegevens van een blob Hallo volgende gebruiken:

* **getBlobToLocalFile** -Hallo blob-inhoud toofile schrijft
* **getBlobToStream** -schrijft Hallo blob inhoud tooa stroom
* **getBlobToText** -schrijft Hallo blob-inhoud tooa tekenreeks
* **createReadStream** -biedt een tooread stroom van Hallo blob

Hallo volgende voorbeeldcode laat zien met **getBlobToStream** toodownload Hallo inhoud Hallo **myblob** blob en sla het toohello **uitvoer.txt** bestand met behulp van een Stream:

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

Hallo `result` bevat informatie over Hallo blob, met inbegrip van **ETag** informatie.

## <a name="delete-a-blob"></a>Een blob verwijderen
Tenslotte toodelete een blob roept **deleteBlob**. Hallo met het volgende codevoorbeeld verwijderingen Hallo blob met de naam **myblob**.

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>Gelijktijdige toegang
toosupport gelijktijdige toegang tooa blob van meerdere clients of meerdere procesexemplaren, kunt u **ETags** of **leases**.

* **ETag** -biedt een manier toodetect die Hallo blob of de container is gewijzigd door een ander proces
* **Lease** : biedt een manier tooobtain exclusieve, verlengd, schrijven of verwijderen van toegang tooa blob voor een bepaalde periode

### <a name="etag"></a>ETag
ETags gebruiken als u meerdere clients of exemplaren toowrite toohello blok Blob of pagina-Blob tegelijkertijd tooallow nodig. Hallo kunt ETag u toodetermine als hello container of blob is gewijzigd, omdat u in eerste instantie lezen of deze is gemaakt, zodat u tooavoid overschrijven wijzigingen doorgevoerd door een andere client of een ander proces.

U kunt voorwaarden ETag instellen via Hallo optionele `options.accessConditions` parameter. Hallo volgende codevoorbeeld alleen uploadt Hallo **test.txt** bestand als Hallo blob bestaat al en ETag-waarde Hallo is opgenomen door `etagToMatch`.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

Wanneer u ETags gebruikt, is het Hallo algemene patroon:

1. Hallo ETag verkrijgen als resultaat Hallo van maken, lijst of get-bewerking.
2. Een actie uitgevoerd, controleren dat die Hallo ETag-waarde is niet gewijzigd.

Als het Hallo-waarde is gewijzigd, betekent dit dat een andere client of exemplaar gewijzigd Hallo blob of container nadat u hebt verkregen Hallo ETag-waarde.

### <a name="lease"></a>Lease
U kunt een nieuwe lease verkrijgen met behulp van Hallo **acquireLease** methode Hallo blob of de container die u wilt dat tooobtain een lease op te geven. Bijvoorbeeld, Hallo code na een lease verkrijgt op **myblob**.

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

Verdere bewerkingen op **myblob** Hallo moet opgeven `options.leaseId` parameter. Hallo lease ID wordt geretourneerd als `result.id` van **acquireLease**.

> [!NOTE]
> Standaard is de leaseduur Hallo oneindig. U kunt een duur niet oneindig (tussen 15 en 60 seconden) opgeven door Hallo `options.leaseDuration` parameter.
>
>

gebruik van een lease tooremove **releaseLease**. een lease toobreak maar te voorkomen dat anderen gebruik van een nieuwe lease totdat Hallo oorspronkelijke duur is verlopen, **breakLease**.

## <a name="work-with-shared-access-signatures"></a>Werken met handtekeningen voor gedeelde toegang
Shared access signatures (SAS) zijn een veilige manier tooprovide gedetailleerde toegang tooblobs en containers zonder dat de naam van het opslagaccount of sleutels. Shared access signatures zijn vaak gebruikte tooprovide beperkte toegang tooyour gegevens, zoals het toestaan van een mobiele app tooaccess blobs.

> [!NOTE]
> Terwijl u kunt ook tooblobs voor anonieme toegang toestaan, handtekeningen voor gedeelde toegang ervoor zorgen dat u toegang tot het tooprovide meer wordt beheerd, moet u Hallo SAS genereren.
>
>

Een vertrouwde toepassing zoals een cloud-gebaseerde service genereert handtekeningen voor gedeelde toegang met behulp van Hallo **generateSharedAccessSignature** Hallo **BlobService**, en biedt dit tooan niet vertrouwd of semi vertrouwde toepassing zoals een mobiele app. Gedeelde toegang handtekeningen worden gegenereerd op basis van beleid, waarin wordt beschreven Hallo start en einddatum tijdens welke Hallo handtekeningen voor gedeelde toegang geldig zijn, evenals Hallo toegang krijgen tot niveau toegekende toohello gedeelde toegang handtekeningen houder.

Hallo volgende codevoorbeeld genereert een nieuw beleid voor gedeelde toegang waarmee Hallo shared access signatures houder tooperform leesbewerkingen op Hallo **myblob** blob en 100 minuten na aanmaak Hallo-tijd is verstreken.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

Houd er rekening mee dat Hallo hostinformatie worden moet verstrekt, zoals vereist is wanneer Hallo shared access signatures houder ook tooaccess Hallo container probeert.

Hallo vervolgens clienttoepassing maakt gebruik van handtekeningen voor gedeelde toegang met **BlobServiceWithSAS** tooperform bewerkingen op Hallo blob. Hallo volgende Hiermee haalt u informatie over **myblob**.

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

Omdat de handtekeningen voor gedeelde Hallo toegang zijn gegenereerd met alleen-lezen toegang als wordt geprobeerd toomodify Hallo blob, wordt er een fout geretourneerd.

### <a name="access-control-lists"></a>Toegangsbeheerlijsten
U kunt ook een toegangsbeheerlijst (ACL) tooset Hallo toegangsbeleid voor toegangsbeheer voor SA's gebruiken. Dit is handig als u tooallow meerdere clients tooaccess een container wilt, maar verschillende toegangsbeleid voor elke client bieden.

Een ACL die is geïmplementeerd met behulp van een matrix van toegangsbeleid, met een ID die is gekoppeld aan elk beleid. Hallo volgende codevoorbeeld definieert twee beleidsregels, één voor 'gebruiker1' en één voor 'gebruiker2':

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hallo volgende code voorbeeld opgehaald Hallo huidige ACL voor **mycontainer**, en wordt vervolgens toegevoegd Hallo nieuwe beleidsregels met behulp van **setBlobAcl**. Met deze aanpak kunt:

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Eenmaal Hallo die ACL is ingesteld, kunt u vervolgens maken op basis van Hallo-ID voor een beleid handtekeningen voor gedeelde toegang. Hallo volgende codevoorbeeld maakt nieuwe handtekeningen voor gedeelde toegang voor 'gebruiker2':

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>Volgende stappen
Zie Hallo volgende bronnen voor meer informatie.

* [Azure-opslag-SDK voor knooppunt API-referentiemateriaal][Azure Storage SDK for Node API Reference]
* [Azure Storage-teamblog][Azure Storage Team Blog]
* [Azure-opslag-SDK voor knooppunt] [ Azure Storage SDK for Node] opslagplaats op GitHub
* [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/)
* [Gegevensoverdracht met Hallo AzCopy-opdrachtregelprogramma](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[een Node.js-web-app maken in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js web app met behulp van hello Azure Table-Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[bouwen en implementeren van een Node.js web-app tooAzure met behulp van Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
[bouwen en implementeren van een Node.js-toepassing tooan Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
