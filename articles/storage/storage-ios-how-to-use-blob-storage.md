---
title: aaaHow toouse Azure Blob-opslag iOS | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 474c4263a4bfbd61bfa39e4fdb01ddd9c3829c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a>Hoe toouse iOS Blob-opslag
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Overzicht
In dit artikel wordt uitgelegd hoe u tooperform algemene scenario's met behulp van Microsoft Azure Blob-opslag. Hallo-voorbeelden zijn geschreven in Objective-C en gebruiken van Hallo [Azure Storage-clientbibliotheek voor iOS](https://github.com/Azure/azure-storage-ios). Hallo scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs. Zie voor meer informatie over blobs Hallo [Vervolgstappen](#next-steps) sectie. U kunt ook downloaden Hallo [voorbeeldapp](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly Zie Hallo gebruik van Azure Storage in een iOS-toepassing.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>Hello Azure Storage iOS bibliotheek in uw toepassing importeren
U kunt importeren hello Azure Storage iOS bibliotheek in uw toepassing met behulp van Hallo [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) of door het importeren van Hallo **Framework** bestand. CocoaPod is hello manier aan te raden omdat deze gemakkelijker integreren Hallo-bibliotheek, maar importeren uit Hallo framework-bestand is minder Tussenkomende voor uw bestaand project.

toouse deze bibliotheek, moet u hello te volgen:
- iOS 8 +
- Xcode 7 +

## <a name="cocoapod"></a>CocoaPod
1. Als u dit nog niet hebt gedaan, [CocoaPods installeren](https://guides.cocoapods.org/using/getting-started.html#toc_3) op uw computer door het openen van een terminalvenster en Hallo na de opdracht
    
    ```shell   
    sudo gem install cocoapods
    ```

2. Maak vervolgens een nieuw bestand met de naam in de projectmap hello (Hallo directory met uw .xcodeproj-bestand), _Podfile_(zonder extensie). Voeg Hallo too_Podfile_ te volgen en opslaan.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. Navigeer in terminalvenster hello, toohello projectmap en Voer Hallo na de opdracht

    ```shell    
    pod install
    ```

4. Als uw .xcodeproj geopend in Xcode is, sluiten. In het projectbestand directory open Hallo nieuw gemaakt project die Hallo .xcworkspace extensie zullen hebben. Dit is Hallo bestand werkt u uit voor nu aan.

## <a name="framework"></a>Framework
Hallo andere manier toouse Hallo-bibliotheek toobuild Hallo framework handmatig is:

1. Eerste, downloaden of kloon Hallo [azure-opslag-i/o-opslagplaats](https://github.com/azure/azure-storage-ios).
2. Ga naar de *azure-opslag-ios* -> *Lib* -> *Azure Storage-clientbibliotheek*, en open `AZSClient.xcodeproj` in Xcode.
3. Op Hallo linksboven Xcode wijziging Hallo actieve schema van de 'Azure Storage-clientbibliotheek' te 'Framework'.
4. Bouw Hallo-project (⌘ + B). Hiermee maakt u een `AZSClient.framework` bestand op het bureaublad.

U kunt Hallo framework-bestand vervolgens importeren in uw toepassing door Hallo volgende te doen:

1. Een nieuw project maken of openen van een bestaand project in Xcode.
2. Slepen en neerzetten Hallo `AZSClient.framework` in uw Xcode-projectnavigator.
3. Selecteer *items kopiëren indien nodig*, en klik op *voltooien*.
4. Klik op het project in de linkernavigatiebalk Hallo en op Hallo *algemene* tabblad Hallo boven aan het Hallo-project-editor.
5. Onder Hallo *gekoppelde Frameworks en bibliotheken* sectie, klikt u op Hallo toevoegen (+).
6. Zoek in de lijst Hallo van bibliotheken al opgegeven voor `libxml2.2.tbd` en toe te voegen tooyour project.

## <a name="import-hello-library"></a>Hallo bibliotheek importeren 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

Als u van Swift gebruikmaakt, wordt u toocreate een bridging header nodig hebt en er < AZSClient/AZSClient.h > importeren:

1. Maak een headerbestand `Bridging-Header.h`, en Hallo hierboven importinstructie toe te voegen.
2. Ga toohello *Build Settings* tabblad en zoek naar *Objective-C Bridging Header*.
3. Dubbelklik op het veld Hallo van *Objective-C Bridging Header* en Hallo pad tooyour header-bestand toe te voegen:`ProjectName/Bridging-Header.h`
4. Build Hallo project (⌘ + B) tooverify die Hallo bridging header is opgehaald door Xcode.
5. Aan de slag met Hallo bibliotheek rechtstreeks in een bestand Swift, is niet nodig voor importinstructies.

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>Asynchrone bewerkingen
> [!NOTE]
> Alle methoden die een aanvraag in voor de service Hallo uitvoeren zijn asynchrone bewerkingen. In de codevoorbeelden hello vindt u dat deze methoden een handler is voltooid hebben. Code binnen Hallo voltooiing handler wordt uitgevoerd **nadat** Hallo-aanvraag is voltooid. Code nadat Hallo voltooiing handler wordt uitgevoerd **terwijl** Hallo verzoek wordt gedaan.
> 
> 

## <a name="create-a-container"></a>Een container maken
Elke blob in Azure Storage moet zich bevinden in een container. Hallo volgende voorbeeld laat zien hoe toocreate een container aangeroepen *newcontainer*, in uw opslagaccount als deze niet al bestaat. Bij het kiezen van een naam voor de container worden Houd ook rekening met de Hallo naamgevingsregels hierboven vermeld.

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

U kunt bevestigen dat dit werkt door te kijken Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com) en te verifiëren dat *newcontainer* is in de lijst Hallo van containers voor uw opslagaccount.

## <a name="set-container-permissions"></a>Container machtigingen instellen
Een container machtigingen zijn geconfigureerd voor **persoonlijke** wordt standaard. Containers bieden echter een aantal verschillende opties voor toegang tot de container:

* **Persoonlijke**: Container en de blob-gegevens kunnen worden gelezen door alleen Hallo accounteigenaar.
* **BLOB**: Blob-gegevens in deze container via anonieme aanvragen kunnen worden gelezen, maar de containergegevens is niet beschikbaar. Clients kunnen blobs in de container Hallo via anonieme aanvragen niet opsommen.
* **Container**: Container en de blob-gegevens kunnen worden gelezen via anonieme aanvraag. Clients kunnen opsommen blobs in de container Hallo via anonieme aanvraag, maar kunnen de containers in Hallo storage-account niet inventariseren.

Hallo volgende voorbeeld ziet u hoe toocreate een container met **Container** toegangsmachtigingen waardoor openbare, alleen-lezen toegang voor alle gebruikers op Hallo Internet:

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a>Een blob uploaden naar een container
Zoals vermeld in Hallo [Blob-service concepten](#blob-service-concepts) sectie, Blob Storage biedt drie typen blobs: blok-blobs, toevoeg-blobs en pagina-blobs. Hello Azure Storage iOS bibliotheek ondersteunt alle drie typen blobs. In de meeste gevallen is de blok-blob Hallo type toouse aanbevolen.

Hallo volgende voorbeeld ziet u hoe tooupload een blok-blob van een NSString. Als een blob met dezelfde naam al in deze container bestaat Hallo Hallo inhoud van deze blob overschreven.

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

U kunt bevestigen dat dit werkt door te kijken Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com) en verifiëren van die container Hallo *containerpublic*, Hallo-blob bevat *sampleblob*. In dit voorbeeld wordt een openbare container gebruikt, zodat u ook controleren kunt of deze toepassing heeft gewerkt door te gaan toohello blobs URI:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

Bovendien toouploading een blok-blob van een NSString, vergelijkbaar bestaan methoden voor NSData, NSInputStream of een lokaal bestand.

## <a name="list-hello-blobs-in-a-container"></a>Lijst Hallo blobs in een container
Hallo volgende voorbeeld ziet u hoe toolist alle blobs in een container. Bij het uitvoeren van deze bewerking worden gelet op Hallo volgende parameters:     

* **continuationToken** -Hallo voortzetting token vertegenwoordigt waar Hallo aanbieding bewerking moet worden gestart. Als er geen token is opgegeven, wordt deze blobs Hallo vanaf een lijst. Een onbeperkt aantal blobs kan worden weergegeven, vanaf nul up tooa maximum instellen. Zelfs als deze methode nul resultaten retourneert als `results.continuationToken` is niet nul is, kunnen er meer blobs op Hallo-service die niet zijn opgenomen.
* **voorvoegsel** -kunt u Hallo voorvoegsel toouse voor blob-aanbieding. Alleen de blobs die met dit voorvoegsel beginnen wordt weergegeven.
* **useFlatBlobListing** - zoals vermeld in Hallo [Naming en verwijzen naar containers en blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) sectie Hoewel Hallo Blob-service een opslagschema platte is, kunt u een virtuele hiërarchie door de naam van de blobs met pad informatie. Niet-platte aanbieding is echter momenteel niet ondersteund. Deze functie is binnenkort beschikbaar. Nu u deze waarde moet **Ja**.

* **blobListingDetails** -kunt u opgeven welke items tooinclude wanneer blobs
  * _AZSBlobListingDetailsNone_: lijst alleen doorgevoerde blobs en blobmetagegevens niet retourneren.
  * _AZSBlobListingDetailsSnapshots_: lijst doorgevoerd blobs en blob-momentopnamen.
  * _AZSBlobListingDetailsMetadata_: blobmetagegevens ophalen voor elke blob in Hallo aanbieding geretourneerd.
  * _AZSBlobListingDetailsUncommittedBlobs_: lijst doorgevoerd en niet-doorgevoerde blobs.
  * _AZSBlobListingDetailsCopy_: kopie opnemen eigenschappen in Hallo aanbieding.
  * _AZSBlobListingDetailsAll_: lijst alle beschikbare doorgevoerd blobs, niet-doorgevoerde blobs en momentopnamen en de status van alle metagegevens en kopieert u voor deze blobs retourneren.
* **maxResults** -Hallo maximum aantal resultaten tooreturn voor deze bewerking. Gebruik-1 toonot een limiet ingesteld.
* **completionHandler** -Hallo blok van code tooexecute met resultaten Hallo Hallo aanbieding bewerking.

In dit voorbeeld is een Help-methode gebruikte toorecursively aanroep Hallo lijst blobs methode telkens wanneer een vervolgtoken wordt geretourneerd.

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a>Een blob downloaden
Hallo volgende voorbeeld wordt getoond hoe toodownload een blob tooa NSString-object.

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a>Een blob verwijderen
Hallo volgende voorbeeld wordt getoond hoe toodelete een blob.

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a>Verwijderen van een blob-container
Hallo volgende voorbeeld wordt getoond hoe toodelete een container.

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a>Volgende stappen
Nu dat u hebt geleerd hoe toouse Blob Storage van iOS-, volg deze koppelingen toolearn meer Hallo-bibliotheek voor iOS- en opslagservice Hallo.

* [Azure Storage-clientbibliotheek voor iOS](https://github.com/azure/azure-storage-ios)
* [Azure Storage iOS naslagdocumentatie](http://azure.github.io/azure-storage-ios/)
* [REST-API voor Azure Storage-services](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog van het Azure Storage-team](http://blogs.msdn.com/b/windowsazurestorage)

Als u vragen over deze bibliotheek hebt, kunt u gratis toopost tooour [Azure MSDN-forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) of [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).
Als u suggesties voor functies voor Azure Storage hebt, boek te[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).

