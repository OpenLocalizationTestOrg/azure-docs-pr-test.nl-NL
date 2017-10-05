---
title: Azure Functions met mediaservices te ontwikkelen
description: In dit onderwerp laat zien hoe de ontwikkeling van Azure Functions met Media Services met Azure portal.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a>Azure Functions met mediaservices te ontwikkelen

Dit onderwerp leest u hoe u aan de slag met Azure-functies die gebruikmaken van Media Services maken. De Azure-functie die is gedefinieerd in dit onderwerp wordt een storage-account-container met de naam bewaakt **invoer** voor nieuwe MP4-bestanden. Wanneer een bestand in de storage-container is verbroken, kan de blob-trigger de functie wordt uitgevoerd.

Als u wilt verkennen en implementeren van de bestaande Azure-functies die gebruikmaken van Azure Media Services, Bekijk [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Deze repository bevat voorbeelden van Media Services gebruiken om werkstromen die betrekking hebben op het opnemen van inhoud rechtstreeks uit blob storage codering en -inhoud weggeschreven terug naar blob-opslag weer te geven. Dit omvat ook voorbeelden van het bewaken van de taak meldingen via WebHooks en wachtrijen in Azure. U kunt ook uw functies op basis van de voorbeelden in ontwikkelen de [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) opslagplaats. Voor het implementeren van de functies, drukt u op de **implementeren in Azure** knop.

## <a name="prerequisites"></a>Vereisten

- Voordat u uw eerste functie kunt maken, moet u een actief Azure-account hebben. Als u nog geen Azure-account hebt, zijn er [gratis accounts beschikbaar](https://azure.microsoft.com/free/).
- Als u maken van Azure Functions die acties uitvoeren op uw account voor Azure Media Services (AMS) of gebeurtenissen die door Media Services wordt verzonden wilt, moet u een AMS-account maken zoals beschreven [hier](media-services-portal-create-account.md).
- Kennis van [het gebruik van Azure functions](../azure-functions/functions-overview.md). Bekijk ook:
    - [HTTP- en webhook bindingen van Azure functions](../azure-functions/functions-triggers-bindings.md)
    - [Het Azure-functie app-instellingen configureren](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Overwegingen

-  Azure Functions uitgevoerd onder het plan verbruik hebben 5 minuten time-out beperken.

## <a name="create-a-function-app"></a>Een functie-app maken

1. Ga naar de [Azure-portal](http://portal.azure.com) en meld u aan met uw Azure-account.
2. Maken van een functie-app, zoals wordt beschreven [hier](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Een opslagaccount dat u opgeeft in de **StorageConnection** omgevingsvariabele (Zie de volgende stap) moet in dezelfde regio bevinden als uw app.

## <a name="configure-function-app-settings"></a>De functie app-instellingen configureren

Bij het ontwikkelen van Media Services-functies, is het handig om toe te voegen omgevingsvariabelen die worden gebruikt in uw functies. Klik op de koppeling instellingen van de App appinstellingen configureren. Zie voor meer informatie [Azure-functie app-instellingen configureren](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

Bijvoorbeeld:

![Instellingen](./media/media-services-azure-functions/media-services-azure-functions001.png)

De functie, gedefinieerd in dit artikel wordt ervan uitgegaan dat u hebt de volgende omgevingsvariabelen in de instellingen van uw app:

**AMSAccount** : *AMS-accountnaam* (bijvoorbeeld testams)

**AMSKey** : *AMS accountsleutel* (bijvoorbeeld IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)

**MediaServicesStorageAccountName** : *opslagaccountnaam* (bijv, testamsstorage)

**MediaServicesStorageAccountKey** : *opslagaccountsleutel* (bijv, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)

**StorageConnection** : *opslagverbinding* (bijv, DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey = xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX ==)

## <a name="create-a-function"></a>Een functie maken

Als de functie-app is geïmplementeerd, kunt u het vinden onder **App Services** Azure Functions.

1. Selecteer de functie-app en klik op **nieuwe functie**.
2. Kies de **C#** taal en **gegevensverwerking** scenario.
3. Kies **BlobTrigger** sjabloon. Deze functie wordt geactiveerd wanneer een blob is geüpload naar de **invoer** container. De **invoer** naam is opgegeven in de **pad**, in de volgende stap.

    ![Bestanden](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. Als u hebt geselecteerd **BlobTrigger**, sommige meer besturingselementen op de pagina wordt weergegeven.

    ![Bestanden](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. Klik op **Create**. 


## <a name="files"></a>Bestanden

Uw Azure-functie is gekoppeld aan het codebestanden en andere bestanden die in deze sectie worden beschreven. Een functie is standaard gekoppeld aan **function.json** en **run.csx** (C#)-bestanden. U moet toevoegen een **project.json** bestand. De rest van deze sectie bevat de definities voor deze bestanden.

![Bestanden](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>Function.JSON

Het bestand function.json definieert de functiebindingen en andere configuratie-instellingen. De runtime maakt gebruik van dit bestand om te bepalen welke gebeurtenissen u wilt bewaken en het doorgeven van gegevens in en gegevens retourneren van een functie wordt uitgevoerd. Zie voor meer informatie [HTTP- en webhook bindingen van Azure functions](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Stel de **uitgeschakeld** eigenschap **true** om te voorkomen dat de functie wordt uitgevoerd. 


Hier volgt een voorbeeld van **function.json** bestand.

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a>Project.JSON

Het bestand project.json bevat afhankelijkheden. Hier volgt een voorbeeld van **project.json** bestand met de vereiste .NET Azure Media Services-pakketten vanuit Nuget. Houd er rekening mee dat de versienummers worden gewijzigd met de meest recente updates op de pakketten, zodat de meest recente versies dient u te bevestigen. 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a>Run.csx

Dit is de C#-code voor de functie.  De functie zoals hieronder gedefinieerd, monitors een storage-account-container met de naam **invoer** (die is opgegeven in het pad) voor nieuwe MP4-bestanden. Wanneer een bestand in de storage-container is verbroken, kan de blob-trigger de functie wordt uitgevoerd.
    
Het voorbeeld dat is gedefinieerd in deze sectie bevat 

1. het opnemen van een actief naar een Media Services-account (door een blob kopiëren naar een asset AMS) en 
2. hoe naar een codeertaak verzendt die gebruikmaakt van Media Encoder Standard van 'Adaptief streamen' vooraf ingesteld.

In het scenario praktijk wilt u waarschijnlijk taak voortgang volgen en vervolgens de gecodeerde asset te publiceren. Zie voor meer informatie [gebruik Azure WebHooks voor het bewaken van Media Services taak meldingen](media-services-dotnet-check-job-progress-with-webhooks.md). Zie voor meer voorbeelden [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

Wanneer u klaar bent voor het definiëren van de functie klikt u op **opslaan en uitvoeren**.

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get the destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of the destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a>De functie testen

Als u wilt uw functie testen, moet u voor het uploaden van een MP4-bestand in de **invoer** container van het opslagaccount dat u hebt opgegeven in de verbindingsreeks.  

## <a name="next-step"></a>Volgende stap

U bent nu klaar om te beginnen met het ontwikkelen van een Media Services-toepassing. 
 
Zie voor meer informatie en volledige samples/oplossingen van het gebruik van Azure Functions en Logic Apps met Azure Media Services voor het maken van aangepaste inhoud werkstromen maken, de [Media Services .NET-functies Integraiton voorbeeld op GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Zie ook [WebHooks van gebruik Azure Media Services taak meldingen met .NET bewaken](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

