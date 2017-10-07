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
ms.openlocfilehash: cc08b76b682537a9a51e970c76bd76c7c06a4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="c9cb3-103">Hoe toouse iOS Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="c9cb3-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="c9cb3-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c9cb3-104">Overview</span></span>
<span data-ttu-id="c9cb3-105">In dit artikel wordt uitgelegd hoe u tooperform algemene scenario's met behulp van Microsoft Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="c9cb3-106">Hallo-voorbeelden zijn geschreven in Objective-C en gebruiken van Hallo [Azure Storage-clientbibliotheek voor iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="c9cb3-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="c9cb3-107">Hallo scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="c9cb3-108">Zie voor meer informatie over blobs Hallo [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="c9cb3-109">U kunt ook downloaden Hallo [voorbeeldapp](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly Zie Hallo gebruik van Azure Storage in een iOS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="c9cb3-110">Hello Azure Storage iOS bibliotheek in uw toepassing importeren</span><span class="sxs-lookup"><span data-stu-id="c9cb3-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="c9cb3-111">U kunt importeren hello Azure Storage iOS bibliotheek in uw toepassing met behulp van Hallo [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) of door het importeren van Hallo **Framework** bestand.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="c9cb3-112">CocoaPod is hello manier aan te raden omdat deze gemakkelijker integreren Hallo-bibliotheek, maar importeren uit Hallo framework-bestand is minder Tussenkomende voor uw bestaand project.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="c9cb3-113">toouse deze bibliotheek, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="c9cb3-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="c9cb3-114">iOS 8 +</span><span class="sxs-lookup"><span data-stu-id="c9cb3-114">iOS 8+</span></span>
- <span data-ttu-id="c9cb3-115">Xcode 7 +</span><span class="sxs-lookup"><span data-stu-id="c9cb3-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="c9cb3-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="c9cb3-116">CocoaPod</span></span>
1. <span data-ttu-id="c9cb3-117">Als u dit nog niet hebt gedaan, [CocoaPods installeren](https://guides.cocoapods.org/using/getting-started.html#toc_3) op uw computer door het openen van een terminalvenster en Hallo na de opdracht</span><span class="sxs-lookup"><span data-stu-id="c9cb3-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="c9cb3-118">Maak vervolgens een nieuw bestand met de naam in de projectmap hello (Hallo directory met uw .xcodeproj-bestand), _Podfile_(zonder extensie).</span><span class="sxs-lookup"><span data-stu-id="c9cb3-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="c9cb3-119">Voeg Hallo too_Podfile_ te volgen en opslaan.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="c9cb3-120">Navigeer in terminalvenster hello, toohello projectmap en Voer Hallo na de opdracht</span><span class="sxs-lookup"><span data-stu-id="c9cb3-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="c9cb3-121">Als uw .xcodeproj geopend in Xcode is, sluiten.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="c9cb3-122">In het projectbestand directory open Hallo nieuw gemaakt project die Hallo .xcworkspace extensie zullen hebben.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="c9cb3-123">Dit is Hallo bestand werkt u uit voor nu aan.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="c9cb3-124">Framework</span><span class="sxs-lookup"><span data-stu-id="c9cb3-124">Framework</span></span>
<span data-ttu-id="c9cb3-125">Hallo andere manier toouse Hallo-bibliotheek toobuild Hallo framework handmatig is:</span><span class="sxs-lookup"><span data-stu-id="c9cb3-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="c9cb3-126">Eerste, downloaden of kloon Hallo [azure-opslag-i/o-opslagplaats](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="c9cb3-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="c9cb3-127">Ga naar de *azure-opslag-ios* -> *Lib* -> *Azure Storage-clientbibliotheek*, en open `AZSClient.xcodeproj` in Xcode.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="c9cb3-128">Op Hallo linksboven Xcode wijziging Hallo actieve schema van de 'Azure Storage-clientbibliotheek' te 'Framework'.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="c9cb3-129">Bouw Hallo-project (⌘ + B).</span><span class="sxs-lookup"><span data-stu-id="c9cb3-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="c9cb3-130">Hiermee maakt u een `AZSClient.framework` bestand op het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="c9cb3-131">U kunt Hallo framework-bestand vervolgens importeren in uw toepassing door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="c9cb3-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="c9cb3-132">Een nieuw project maken of openen van een bestaand project in Xcode.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="c9cb3-133">Slepen en neerzetten Hallo `AZSClient.framework` in uw Xcode-projectnavigator.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="c9cb3-134">Selecteer *items kopiëren indien nodig*, en klik op *voltooien*.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="c9cb3-135">Klik op het project in de linkernavigatiebalk Hallo en op Hallo *algemene* tabblad Hallo boven aan het Hallo-project-editor.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="c9cb3-136">Onder Hallo *gekoppelde Frameworks en bibliotheken* sectie, klikt u op Hallo toevoegen (+).</span><span class="sxs-lookup"><span data-stu-id="c9cb3-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="c9cb3-137">Zoek in de lijst Hallo van bibliotheken al opgegeven voor `libxml2.2.tbd` en toe te voegen tooyour project.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="c9cb3-138">Hallo bibliotheek importeren</span><span class="sxs-lookup"><span data-stu-id="c9cb3-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="c9cb3-139">Als u van Swift gebruikmaakt, wordt u toocreate een bridging header nodig hebt en er < AZSClient/AZSClient.h > importeren:</span><span class="sxs-lookup"><span data-stu-id="c9cb3-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="c9cb3-140">Maak een headerbestand `Bridging-Header.h`, en Hallo hierboven importinstructie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="c9cb3-141">Ga toohello *Build Settings* tabblad en zoek naar *Objective-C Bridging Header*.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="c9cb3-142">Dubbelklik op het veld Hallo van *Objective-C Bridging Header* en Hallo pad tooyour header-bestand toe te voegen:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="c9cb3-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="c9cb3-143">Build Hallo project (⌘ + B) tooverify die Hallo bridging header is opgehaald door Xcode.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="c9cb3-144">Aan de slag met Hallo bibliotheek rechtstreeks in een bestand Swift, is niet nodig voor importinstructies.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="c9cb3-145">Asynchrone bewerkingen</span><span class="sxs-lookup"><span data-stu-id="c9cb3-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="c9cb3-146">Alle methoden die een aanvraag in voor de service Hallo uitvoeren zijn asynchrone bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="c9cb3-147">In de codevoorbeelden hello vindt u dat deze methoden een handler is voltooid hebben.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="c9cb3-148">Code binnen Hallo voltooiing handler wordt uitgevoerd **nadat** Hallo-aanvraag is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="c9cb3-149">Code nadat Hallo voltooiing handler wordt uitgevoerd **terwijl** Hallo verzoek wordt gedaan.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="c9cb3-150">Een container maken</span><span class="sxs-lookup"><span data-stu-id="c9cb3-150">Create a container</span></span>
<span data-ttu-id="c9cb3-151">Elke blob in Azure Storage moet zich bevinden in een container.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="c9cb3-152">Hallo volgende voorbeeld laat zien hoe toocreate een container aangeroepen *newcontainer*, in uw opslagaccount als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="c9cb3-153">Bij het kiezen van een naam voor de container worden Houd ook rekening met de Hallo naamgevingsregels hierboven vermeld.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

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

<span data-ttu-id="c9cb3-154">U kunt bevestigen dat dit werkt door te kijken Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com) en te verifiëren dat *newcontainer* is in de lijst Hallo van containers voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="c9cb3-155">Container machtigingen instellen</span><span class="sxs-lookup"><span data-stu-id="c9cb3-155">Set Container Permissions</span></span>
<span data-ttu-id="c9cb3-156">Een container machtigingen zijn geconfigureerd voor **persoonlijke** wordt standaard.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="c9cb3-157">Containers bieden echter een aantal verschillende opties voor toegang tot de container:</span><span class="sxs-lookup"><span data-stu-id="c9cb3-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="c9cb3-158">**Persoonlijke**: Container en de blob-gegevens kunnen worden gelezen door alleen Hallo accounteigenaar.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="c9cb3-159">**BLOB**: Blob-gegevens in deze container via anonieme aanvragen kunnen worden gelezen, maar de containergegevens is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="c9cb3-160">Clients kunnen blobs in de container Hallo via anonieme aanvragen niet opsommen.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="c9cb3-161">**Container**: Container en de blob-gegevens kunnen worden gelezen via anonieme aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="c9cb3-162">Clients kunnen opsommen blobs in de container Hallo via anonieme aanvraag, maar kunnen de containers in Hallo storage-account niet inventariseren.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="c9cb3-163">Hallo volgende voorbeeld ziet u hoe toocreate een container met **Container** toegangsmachtigingen waardoor openbare, alleen-lezen toegang voor alle gebruikers op Hallo Internet:</span><span class="sxs-lookup"><span data-stu-id="c9cb3-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

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

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="c9cb3-164">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="c9cb3-164">Upload a blob into a container</span></span>
<span data-ttu-id="c9cb3-165">Zoals vermeld in Hallo [Blob-service concepten](#blob-service-concepts) sectie, Blob Storage biedt drie typen blobs: blok-blobs, toevoeg-blobs en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="c9cb3-166">Hello Azure Storage iOS bibliotheek ondersteunt alle drie typen blobs.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="c9cb3-167">In de meeste gevallen is de blok-blob Hallo type toouse aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="c9cb3-168">Hallo volgende voorbeeld ziet u hoe tooupload een blok-blob van een NSString.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="c9cb3-169">Als een blob met dezelfde naam al in deze container bestaat Hallo Hallo inhoud van deze blob overschreven.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

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

<span data-ttu-id="c9cb3-170">U kunt bevestigen dat dit werkt door te kijken Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com) en verifiëren van die container Hallo *containerpublic*, Hallo-blob bevat *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="c9cb3-171">In dit voorbeeld wordt een openbare container gebruikt, zodat u ook controleren kunt of deze toepassing heeft gewerkt door te gaan toohello blobs URI:</span><span class="sxs-lookup"><span data-stu-id="c9cb3-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="c9cb3-172">Bovendien toouploading een blok-blob van een NSString, vergelijkbaar bestaan methoden voor NSData, NSInputStream of een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="c9cb3-173">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="c9cb3-173">List hello blobs in a container</span></span>
<span data-ttu-id="c9cb3-174">Hallo volgende voorbeeld ziet u hoe toolist alle blobs in een container.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="c9cb3-175">Bij het uitvoeren van deze bewerking worden gelet op Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="c9cb3-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="c9cb3-176">**continuationToken** -Hallo voortzetting token vertegenwoordigt waar Hallo aanbieding bewerking moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="c9cb3-177">Als er geen token is opgegeven, wordt deze blobs Hallo vanaf een lijst.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="c9cb3-178">Een onbeperkt aantal blobs kan worden weergegeven, vanaf nul up tooa maximum instellen.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="c9cb3-179">Zelfs als deze methode nul resultaten retourneert als `results.continuationToken` is niet nul is, kunnen er meer blobs op Hallo-service die niet zijn opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="c9cb3-180">**voorvoegsel** -kunt u Hallo voorvoegsel toouse voor blob-aanbieding.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="c9cb3-181">Alleen de blobs die met dit voorvoegsel beginnen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="c9cb3-182">**useFlatBlobListing** - zoals vermeld in Hallo [Naming en verwijzen naar containers en blobs](#naming-and-referencing-containers-and-blobs) sectie Hoewel Hallo Blob-service een opslagschema platte is, kunt u een virtuele hiërarchie door de naam van de blobs met pad informatie.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](#naming-and-referencing-containers-and-blobs) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="c9cb3-183">Niet-platte aanbieding is echter momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="c9cb3-184">Deze functie is binnenkort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-184">This feature is coming soon.</span></span> <span data-ttu-id="c9cb3-185">Nu u deze waarde moet **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-185">For now, this value should be **YES**.</span></span>
* <span data-ttu-id="c9cb3-186">**blobListingDetails** -kunt u opgeven welke items tooinclude wanneer blobs</span><span class="sxs-lookup"><span data-stu-id="c9cb3-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="c9cb3-187">_AZSBlobListingDetailsNone_: lijst alleen doorgevoerde blobs en blobmetagegevens niet retourneren.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="c9cb3-188">_AZSBlobListingDetailsSnapshots_: lijst doorgevoerd blobs en blob-momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="c9cb3-189">_AZSBlobListingDetailsMetadata_: blobmetagegevens ophalen voor elke blob in Hallo aanbieding geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="c9cb3-190">_AZSBlobListingDetailsUncommittedBlobs_: lijst doorgevoerd en niet-doorgevoerde blobs.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="c9cb3-191">_AZSBlobListingDetailsCopy_: kopie opnemen eigenschappen in Hallo aanbieding.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="c9cb3-192">_AZSBlobListingDetailsAll_: lijst alle beschikbare doorgevoerd blobs, niet-doorgevoerde blobs en momentopnamen en de status van alle metagegevens en kopieert u voor deze blobs retourneren.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="c9cb3-193">**maxResults** -Hallo maximum aantal resultaten tooreturn voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="c9cb3-194">Gebruik-1 toonot een limiet ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="c9cb3-195">**completionHandler** -Hallo blok van code tooexecute met resultaten Hallo Hallo aanbieding bewerking.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="c9cb3-196">In dit voorbeeld is een Help-methode gebruikte toorecursively aanroep Hallo lijst blobs methode telkens wanneer een vervolgtoken wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="c9cb3-197">Een blob downloaden</span><span class="sxs-lookup"><span data-stu-id="c9cb3-197">Download a blob</span></span>
<span data-ttu-id="c9cb3-198">Hallo volgende voorbeeld wordt getoond hoe toodownload een blob tooa NSString-object.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="c9cb3-199">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="c9cb3-199">Delete a blob</span></span>
<span data-ttu-id="c9cb3-200">Hallo volgende voorbeeld wordt getoond hoe toodelete een blob.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-200">hello following example shows how toodelete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="c9cb3-201">Verwijderen van een blob-container</span><span class="sxs-lookup"><span data-stu-id="c9cb3-201">Delete a blob container</span></span>
<span data-ttu-id="c9cb3-202">Hallo volgende voorbeeld wordt getoond hoe toodelete een container.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-202">hello following example shows how toodelete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c9cb3-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9cb3-203">Next steps</span></span>
<span data-ttu-id="c9cb3-204">Nu dat u hebt geleerd hoe toouse Blob Storage van iOS-, volg deze koppelingen toolearn meer Hallo-bibliotheek voor iOS- en opslagservice Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9cb3-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="c9cb3-205">Azure Storage-clientbibliotheek voor iOS</span><span class="sxs-lookup"><span data-stu-id="c9cb3-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="c9cb3-206">Azure Storage iOS naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="c9cb3-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="c9cb3-207">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="c9cb3-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="c9cb3-208">Blog van het Azure Storage-team</span><span class="sxs-lookup"><span data-stu-id="c9cb3-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="c9cb3-209">Als u vragen over deze bibliotheek hebt, kunt u gratis toopost tooour [Azure MSDN-forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) of [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="c9cb3-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="c9cb3-210">Als u suggesties voor functies voor Azure Storage hebt, boek te[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="c9cb3-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

