---
title: aaaGet gestart met blob-opslag- en Visual Studio verbonden services (cloudservices) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure Blob-opslag in een cloud service-project in Visual Studio nadat tooa storage-account met Visual Studio verbinding services verbonden
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Aan de slag met Azure Blob Storage en Visual Studio verbonden services (cloud services-projecten)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe de tooget slag met Azure Blob Storage nadat u hebt gemaakt of een Azure Storage-account waarnaar wordt verwezen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster in een Visual Studio-cloud services-project. Leert u hoe tooaccess blob-containers en hoe tooperform algemene taken, zoals uploaden, weergeven en downloaden van blobs en maken. Hallo-voorbeelden zijn geschreven in C\# en gebruik Hallo [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Azure Blob Storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS. Één blob kan elke grootte zijn. BLOBs kunnen worden items zoals afbeeldingen, audio en video-bestanden, onbewerkte gegevens en bestanden.

Net als bestanden bevinden zich in mappen, live storage-blobs in containers. Nadat u een opslagruimte hebt gemaakt, kunt u een of meer containers maken in Hallo-opslag. Bijvoorbeeld in een opslag 'Plakboek' genoemd, kunt u containers maken in de opslag van Hallo aangeroepen 'afbeeldingen' toostore afbeeldingen en andere 'audio' toostore aangeroepen audio-bestanden. Nadat u Hallo containers maken, kunt u afzonderlijke blob bestanden toothem uploaden.

* Zie voor meer informatie over het bewerken van programmatisch blobs [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).
* Raadpleeg voor algemene informatie over Azure Storage [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/).
* Raadpleeg voor algemene informatie over Azure Cloud Services [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/).
* Zie voor meer informatie over het programmeren van ASP.NET-toepassingen [ASP.NET](http://www.asp.net).

## <a name="access-blob-containers-in-code"></a>Toegang tot blob-containers in code
tooprogrammatically toegang tot blobs in cloudserviceprojecten, moet u tooadd Hallo items, te volgen als ze nog niet aanwezig is.

1. Hallo na code naamruimte declaraties toohello boven aan elk C#-bestand waarin u tooprogrammatically toegang tot Azure Storage wilt toevoegen.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo na code tooget Hallo uw verbindingsreeks voor opslag en de accountgegevens van de opslag van Azure Hallo-serviceconfiguratie.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. Ophalen van een **CloudBlobClient** object tooreference een bestaande container in uw opslagaccount.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. Ophalen van een **CloudBlobContainer** object tooreference een specifieke blob-container.
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> Alle weergegeven in de vorige procedure Hallo voor Hallo-code die wordt weergegeven in de volgende secties Hallo Hallo-code gebruiken.
> 
> 

## <a name="create-a-container-in-code"></a>Een container in code maken
> [!NOTE]
> Sommige API's die het uitvoeren van aanroepen uit tooAzure opslag in ASP.NET zijn asynchroon. Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie. Hallo-code in Hallo volgende voorbeeld wordt ervan uitgegaan dat u van programming async-methoden gebruikmaakt.
> 
> 

een container in uw opslagaccount toocreate, hoeft u toodo is Voeg een aanroep toe te**CreateIfNotExistsAsync** zoals Hallo na de code in:

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


toomake hello bestanden binnen hello container beschikbaar tooeveryone, u kunt instellen Hallo container toobe openbare met behulp van de volgende code Hallo.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Iedereen op Internet Hallo blobs in een openbare container kunt zien, maar u kunt wijzigen of ze alleen verwijderen als u de juiste toegangssleutel Hallo hebt.

## <a name="upload-a-blob-into-a-container"></a>Een blob uploaden naar een container
Azure Storage ondersteunt blok-blobs en pagina-blobs. In Hallo meeste gevallen is het blok-blob Hallo type toouse aanbevolen.

een bestand tooa blok-blob tooupload een containerverwijzing ophalen en deze tooget een blok-blobverwijzing gebruiken. Zodra u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom tooit gegevens uploaden door de aanroepende Hallo **UploadFromStream** methode. Deze bewerking wordt Hallo blob gemaakt als deze niet eerder bestond, of deze wordt overschreven als deze bestaat. Hallo volgende voorbeeld wordt getoond hoe tooupload een blob naar een container en wordt ervan uitgegaan dat Hallo-container al is gemaakt.

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Lijst Hallo blobs in een container
toolist hello blobs in een container, eerst ophalen een containerverwijzing. Vervolgens kunt u Hallo-container **ListBlobs** methode tooretrieve Hallo blobs en/of mappen hierin. tooaccess Hallo uitgebreide set eigenschappen en methoden voor een geretourneerde **IListBlobItem**, u dit casten tooa **CloudBlockBlob**, **CloudPageBlob**, of  **CloudBlobDirectory** object. Als Hallo type onbekend is, kunt u een type selectievakje toodetermine welke toocast naar. Hallo volgende code laat zien hoe tooretrieve en uitvoer URI van elk item in Hallo Hallo **foto's** container:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;

            Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob pageBlob = (CloudPageBlob)item;

            Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory directory = (CloudBlobDirectory)item;

            Console.WriteLine("Directory: {0}", directory.Uri);
        }
    }

Zoals u in het vorige codevoorbeeld hello, heeft Hallo blob-service Hallo concept van mappen in containers, evenals. Dit is zodat u kunt uw blobs in een map achtige structuur indelen. Denk bijvoorbeeld de volgende set blok-blobs in een container met de naam Hallo **foto's**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

Als u aanroept **ListBlobs** op Hallo-container (zoals in het vorige voorbeeld Hallo), Hallo verzameling geretourneerd bevat **CloudBlobDirectory** en **CloudBlockBlob** objecten Hallo mappen en blobs die zijn opgenomen op het hoogste niveau Hallo die. Dit is de resulterende uitvoer Hallo:

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


Desgewenst kunt u instellen Hallo **UseFlatBlobListing** parameter van Hallo **ListBlobs** methode **true**. Dit resulteert in elke blob wordt geretourneerd als een **CloudBlockBlob**, ongeacht van de directory. Hier is Hallo aanroep te**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

en hier vindt u Hallo resultaten:

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

Zie voor meer informatie [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).

## <a name="download-blobs"></a>Blobs downloaden
toodownload blobs, eerst een blobverwijzing ophalen en vervolgens aanroepen Hallo **DownloadToStream** methode. Hallo volgende voorbeeld wordt Hallo **DownloadToStream** methode tootransfer Hallo blob inhoud tooa stroomobject dat u vervolgens blijven tooa lokaal bestand behouden kunt.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

U kunt ook Hallo **DownloadToStream** methode toodownload Hallo inhoud van een blob als een tekenreeks.

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>Blobs verwijderen
een blob toodelete eerst een blobverwijzing ophalen en roept u vervolgens de **verwijderen** methode.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>Blobs asynchroon op pagina's weergeven
Als u een groot aantal blobs aanbiedt of u toocontrol Hallo aantal u in één aanbieding bewerking retourneren resultaten wilt, kunt u op pagina's met resultaten kunt weergeven. Dit voorbeeld toont tooreturn hoe resultaten op pagina's asynchroon, zodat de uitvoering niet wordt geblokkeerd tijdens het wachten op tooreturn een groot aantal resultaten.

Dit voorbeeld ziet u een platte blob weergeven, maar u kunt ook een hiërarchische lijst uitvoeren door de instelling Hallo **useFlatBlobListing** parameter Hallo **ListBlobsSegmentedAsync** methode te **ONWAAR**.

Omdat Hallo voorbeeldmethode een asynchrone methode wordt aangeroepen, moet deze worden voorafgegaan door hello **asynchrone** sleutelwoord en deze moet retourneren een **taak** object. Hallo await trefwoord opgegeven voor Hallo **ListBlobsSegmentedAsync** methode onderbreekt de uitvoering van Hallo voorbeeldmethode totdat de taak in de lijst Hallo is voltooid.

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get hello continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

