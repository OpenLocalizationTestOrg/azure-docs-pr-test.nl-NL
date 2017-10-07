---
title: aaaUpload bestanden naar een Media Services-account met .NET | Microsoft Docs
description: Meer informatie over hoe tooget media van inhoud in Media Services door het maken en uploaden van activa.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a>Bestanden uploaden naar een Media Services-account met .NET
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

In Media Services moet u uw digitale bestanden uploaden naar (of opnemen in) een asset. Hallo **Asset** entiteit kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.)  Zodra het Hallo-bestanden zijn geüpload, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.

Hallo-bestanden in Hallo asset heten **Assetbestanden**. Hallo **AssetFile** exemplaar en de werkelijke mediabestand Hallo zijn twee verschillende objecten. Hallo AssetFile exemplaar bevat metagegevens over mediabestand hello, terwijl het mediabestand Hallo Hallo echte media-inhoud bevat.

> [!NOTE]
> Hallo overwegingen volgende van toepassing:
> 
> * Media Services gebruikt Hallo-waarde van Hallo IAssetFile.Name eigenschap tijdens het bouwen van URL's voor Hallo streaming-inhoud (bijvoorbeeld http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Om deze reden is procent codering niet toegestaan. waarde van Hallo Hallo **naam** eigenschap kan niet een van de volgende Hallo hebben [procent-encoding-gereserveerde tekens](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] '. Bovendien kunnen alleen er een '.' hello bestandsnaamextensie.
> * Hallo-lengte van Hallo-naam mag niet groter zijn dan 260 tekens zijn.
> * Er is een limiet toohello maximale bestandsgrootte voor de verwerking van Media Services wordt ondersteund. Zie [dit](media-services-quotas-and-limitations.md) onderwerp voor meer informatie over Hallo beperking voor de bestandsgrootte.
> * Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn). Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.
> 

Wanneer u activa maakt, kunt u Hallo versleutelingsopties te volgen. 

* **Geen**: er wordt geen versleuteling gebruikt. Dit is de standaardwaarde Hallo. Houd er rekening mee dat wanneer u deze optie uw inhoud wordt niet beveiligd tijdens de overdracht of in rust in de opslag.
  Als u van plan toodeliver een MP4 via progressief downloaden bent, moet u deze optie gebruiken. 
* **CommonEncryption** -Gebruik deze optie als u inhoud uploadt die al is versleuteld en beveiligd met Common Encryption of PlayReady DRM (bijvoorbeeld Smooth Streaming beveiligd met PlayReady DRM).
* **EnvelopeEncrypted** – Gebruik deze optie als u HLS versleuteld met AES uploaden wilt. Houd er rekening mee dat Hallo bestanden moeten zijn gecodeerd en versleuteld door Transform Manager.
* **StorageEncrypted** - versleutelde inhoud lokaal met AES-256-bitsversleuteling versleuteld en geüpload en tooAzure opslag wordt bewaard in rust versleuteld. Automatisch worden beveiligd met Storage Encryption activa niet-versleuteld en geplaatst in een versleuteld bestand system eerdere tooencoding en eventueel opnieuw versleutelde voorafgaande toouploading weer als een nieuwe uitvoerasset. Hallo primaire gebruiksvoorbeeld voor versleuteling van opslag is dat u wilt toosecure uw invoer mediabestanden van hoge kwaliteit met sterke versleuteling-op schijf rest.
  
    Media Services biedt versleuteling van opslag op schijf voor de activa, niet over-the-wire zoals Manager van digitale rechten (DRM).
  
    Als uw asset opslag versleuteld is, moet u het leveringsbeleid voor Assets configureren. Zie voor meer informatie [leveringsbeleid voor Assets configureren](media-services-dotnet-configure-asset-delivery-policy.md).

Als u opgeeft voor uw asset toobe versleuteld met een **CommonEncrypted** optie, of een **EnvelopeEncypted** optie, moet u tooassociate uw asset met een **ContentKey**. Zie voor meer informatie [hoe toocreate een ContentKey](media-services-dotnet-create-contentkey.md). 

Als u opgeeft voor uw asset toobe versleuteld met een **StorageEncrypted** optie, Hallo Media Services SDK voor .NET maakt een **StorateEncrypted** **ContentKey** voor uw Asset.

Dit onderwerp wordt beschreven hoe toouse Media Services .NET SDK, evenals de Media Services .NET SDK extensions tooupload bestanden naar een Media Services-asset.

## <a name="upload-a-single-file-with-media-services-net-sdk"></a>Uploaden van één bestand met Media Services .NET SDK
Hallo voorbeeldcode hieronder gebruikt .NET SDK tooupload één bestand. Hallo AccessPolicy en Locator worden gemaakt en vernietigd door Hallo uploaden functie. 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a>Uploaden van meerdere bestanden met Media Services .NET SDK
Hallo van de volgende code wordt getoond hoe toocreate een asset en meerdere bestanden te uploaden.

Hallo-code Hallo te volgen:

* Maakt een lege asset Hallo CreateEmptyAsset methode die is gedefinieerd in de vorige stap hello gebruiken.
* Maakt een **AccessPolicy** -exemplaar dat Hallo machtigingen en de duur van toegang toohello asset definieert.
* Maakt een **Locator** exemplaar waarmee toegang toohello asset.
* Maakt een **BlobTransferClient** exemplaar. Dit type vertegenwoordigt een client die wordt toegepast op Hallo die Azure blobs. In dit voorbeeld gebruiken we Hallo client toomonitor Hallo-uploadvoortgang. 
* Via de bestanden in de opgegeven map Hallo inventariseren en maakt een **AssetFile** exemplaar voor elk bestand.
* Uploaden van bestanden in Media Services met behulp van Hallo Hallo **UploadAsync** methode. 

> [!NOTE]
> Hallo UploadAsync methode tooensure die Hallo aanroepen niet worden geblokkeerd en Hallo bestanden zijn geüpload parallel gebruiken.
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



Overweeg de volgende Hallo tijdens het uploaden van een groot aantal activa.

* Maak een nieuwe **CloudMediaContext** object per thread. Hallo **CloudMediaContext** klasse is niet thread-veilig.
* NumberOfConcurrentTransfers van Hallo standaardwaarde van 2 tooa hogere waarde zoals 5 verhogen. Als u deze eigenschap is van invloed op alle exemplaren van **CloudMediaContext**. 
* Houd ParallelTransferThreadCount Hallo standaardwaarde van 10.

## <a id="ingest_in_bulk"></a>Het opnemen van de activa in Bulk met Media Services .NET SDK
Grote assetbestanden uploaden, kan een knelpunt zijn tijdens het maken van asset. Omvat het opnemen van activa in Bulk of 'Opnemen van grote hoeveelheden' asset maken via het uploadproces Hallo ontkoppeling. toouse een ingesting benadering bulksgewijs maken een manifest (IngestManifest) die worden beschreven Hallo asset en de bijbehorende bestanden. Gebruik vervolgens Hallo Uploadmethode van uw keuze tooupload Hallo gekoppelde bestanden toohello manifest van blob-container. Microsoft Azure Media Services bewaakt Hallo blob-container die is gekoppeld aan Hallo manifest. Als een bestand geüpload toohello blob-container is, is Microsoft Azure Media Services voltooid Hallo asset maken op basis van de configuratie Hallo van Hallo actief in het Hallo-manifest (IngestManifestAsset).

een nieuwe IngestManifest toocreate Hallo maken methode die worden weergegeven door Hallo IngestManifests verzameling op Hallo CloudMediaContext aanroepen. Deze methode maakt een nieuwe IngestManifest met Hallo manifest die u opgeeft.

    IIngestManifest manifest = context.IngestManifests.Create(name);

Hallo-assets die gekoppeld aan Hallo bulksgewijs IngestManifest zijn maken. Opties voor Hallo gewenst versleuteling op Hallo actief voor het opnemen van grote hoeveelheden configureren.

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

Een Asset koppelt een IngestManifestAsset aan een bulksgewijs IngestManifest voor het opnemen van grote hoeveelheden. Ook wordt gekoppeld Hallo AssetFiles waaruit alle activa. de methode Create Hallo toocreate een IngestManifestAsset gebruiken op Hallo servercontext.

Hallo volgende voorbeeld bevat toe te voegen twee nieuwe IngestManifestAssets die Hallo twee activa eerder gemaakte toohello bulksgewijs koppelt manifest opnemen. Elke IngestManifestAsset koppelt ook een set van bestanden die worden geüpload voor elk actief tijdens het opnemen van grote hoeveelheden.  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

U kunt een clienttoepassing hoge snelheid kunnen uploaden Hallo asset bestanden toohello blob storage-container URI dat is opgegeven door Hallo **IIngestManifest.BlobStorageUriForUpload** eigenschap Hallo IngestManifest. Een opmerkelijke hoge snelheid uploaden service [Aspera On Demand voor Azure-toepassing](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6). U kunt ook programmacode schrijven tooupload Hallo activa bestanden zoals weergegeven in het volgende codevoorbeeld Hallo.

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

Hallo-code voor het uploaden van bestanden van de Hallo asset voor Hallo-voorbeeld gebruikt in dit onderwerp wordt weergegeven in het volgende codevoorbeeld Hallo.

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


U kunt bepalen Hallo voortgang van Hallo bulksgewijs opnemen voor alle activa die zijn gekoppeld aan een **IngestManifest** door Hallo statistieken eigenschap Hallo **IngestManifest**. In de volgorde tooupdate voortgangsinformatie, moet u een nieuwe **CloudMediaContext** telkens wanneer u Hallo statistieken eigenschap opvragen.

Hallo volgende voorbeeld toont een IngestManifest door polling de **Id**.

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a>Uploaden van bestanden met behulp van de .NET SDK Extensions
Hallo voorbeeld hieronder ziet u hoe tooupload een bestand met behulp van de .NET SDK Extensions. In dit geval Hallo **CreateFromFile** methode wordt gebruikt, maar de asynchrone versie Hallo is ook beschikbaar (**CreateFromFileAsync**). Hallo **CreateFromFile** methode kunt u opgeven Hallo-bestandsnaam, versleutelingsoptie en een retouraanroep in volgorde tooreport Hallo voortgang van Hallo-bestand uploaden.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

Hallo volgende voorbeeld UploadFile functie aanroept en versleuteling van opslag geeft als Hallo-optie voor het maken van asset.  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a>Volgende stappen

U kunt nu de geüploade assets coderen. Zie [Assets coderen](media-services-portal-encode.md) voor meer informatie.

U kunt ook Azure Functions tootrigger een codeertaak op basis van een bestand in container Hallo geconfigureerd die binnenkomen. Zie [dit voorbeeld](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) voor meer informatie.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Volgende stap
Nu dat u hebt een actief geüpload tooMedia Services, gaat u toohello [hoe tooGet een Processor Media] [ How tooGet a Media Processor] onderwerp.

[How tooGet a Media Processor]: media-services-get-media-processor.md

