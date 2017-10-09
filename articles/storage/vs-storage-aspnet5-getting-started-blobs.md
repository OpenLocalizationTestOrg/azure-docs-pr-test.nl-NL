---
title: aaaGet gestart met blob-opslag- en Visual Studio verbonden services (ASP.NET Core) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure Blob-opslag in een project voor Visual Studio ASP.NET Core nadat u een opslagaccount met Visual Studio hebt gemaakt, verbonden services
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: a4c31c08c38d99eb9c66fe2af72ca42fa3804688
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Aan de slag met Azure Blob storage en Visual Studio verbonden services (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe het gebruik van Azure Blob-opslag in Visual Studio, nadat u hebt gemaakt of een Azure storage-account in een ASP.NET Core-project waarnaar wordt verwezen met behulp van Visual Studio verbonden Services toevoegen-dialoogvenster Hallo van tooget wordt gestart.

Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS. Één blob kan elke grootte zijn. BLOBs kunnen worden items zoals afbeeldingen, audio en video-bestanden, onbewerkte gegevens en bestanden. Dit artikel wordt beschreven hoe tooget gestart met blob storage nadat u een Azure storage-account hebt gemaakt met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster in een project ASP.NET Core.

Net als bestanden bevinden zich in mappen, live storage-blobs in containers. Nadat u een opslagruimte hebt gemaakt, kunt u een of meer containers maken in Hallo-opslag. Bijvoorbeeld in een opslag 'Plakboek' genoemd, kunt u containers maken in de opslag van Hallo aangeroepen 'afbeeldingen' toostore afbeeldingen en andere 'audio' toostore aangeroepen audio-bestanden. Nadat u Hallo containers maken, kunt u afzonderlijke blob bestanden toothem uploaden. Zie [aan de slag met Azure Blob storage met .NET](storage-dotnet-how-to-use-blobs.md) voor meer informatie over het bewerken van programmatisch blobs.

## <a name="access-blob-containers-in-code"></a>Toegang tot blob-containers in code
tooprogrammatically toegang tot blobs in ASP.NET Core projecten, moet u tooadd Hallo volgende items, als ze nog niet aanwezig is.

1. Hallo na code naamruimte declaraties toohello boven aan elk C#-bestand waarin u tooprogrammatically toegang tot Azure-opslag wilt toevoegen.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo code tooget na uw verbindingsreeks voor opslag en de accountgegevens van de opslag van Azure Hallo-serviceconfiguratie.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **Opmerking:** alle Hallo bovenstaande code voor Hallo code gebruiken in Hallo uit te voeren.
3. Gebruik een **CloudBlobClient** object tooget een **CloudBlobContainer** verwijzing tooan bestaande container in uw opslagaccount.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Een container in code maken
U kunt ook Hallo **CloudBlobClient** toocreate een container in uw opslagaccount. Alles wat u nodig hebt toodo is een aanroep van tooadd te**CreateIfNotExistsAsync** zoals Hallo na de code in:

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**Opmerking:** Hallo API's die aanroepen tooAzure opslag in ASP.NET Core uitvoeren zijn asynchroon. Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie. Hallo-code hieronder wordt ervan uitgegaan programming async-methoden worden gebruikt.

toomake hello bestanden binnen hello container beschikbaar tooeveryone, u kunt instellen Hallo container toobe openbare met behulp van de volgende code Hallo.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Een blob uploaden naar een container
tooupload een blob-bestand naar een container een containerverwijzing ophalen en deze tooget een blobverwijzing gebruiken. Nadat u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom tooit gegevens uploaden door de aanroepende Hallo **UploadFromStreamAsync** methode. Deze bewerking wordt Hallo blob gemaakt als deze nog niet is gebeurd, of deze wordt overschreven als deze bestaat. Hallo volgende voorbeeld wordt getoond hoe tooupload een blob naar een container en wordt ervan uitgegaan dat Hallo-container al is gemaakt.

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Lijst Hallo blobs in een container
toolist hello blobs in een container, eerst ophalen een containerverwijzing. Vervolgens kunt u Hallo-container aanroepen **ListBlobsSegmentedAsync** methode tooretrieve Hallo blobs en/of mappen hierin. tooaccess Hallo uitgebreide set eigenschappen en methoden voor een geretourneerde **IListBlobItem**, u dit casten tooa **CloudBlockBlob**, **CloudPageBlob**, of  **CloudBlobDirectory** object. Als u Hallo blob, typt u niet weet, kunt u een type selectievakje toodetermine welke toocast naar. Hallo volgende code laat zien hoe tooretrieve en uitvoer Hallo URI van elk item in een container.

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
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
    } while (token != null);

Er zijn andere manieren toolist Hallo inhoud van een blob-container. Zie [aan de slag met Azure Blob storage met .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) voor meer informatie.

## <a name="download-a-blob"></a>Een blob downloaden
toodownload een blob eerst een verwijzing toohello blob ophalen en deze vervolgens aanroepen Hallo **DownloadToStreamAsync** methode. Hallo volgende voorbeeld wordt Hallo **DownloadToStreamAsync** methode tootransfer Hallo blob inhoud tooa stroomobject dat u kunt vervolgens opslaan als een lokaal bestand.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

Er zijn andere manieren toosave blobs als bestanden. Zie [aan de slag met Azure Blob storage met .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) voor meer informatie.

## <a name="delete-a-blob"></a>Een blob verwijderen
toodelete een blob eerst een verwijzing toohello blob ophalen en deze vervolgens aanroepen Hallo **DeleteAsync** methode erop.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

