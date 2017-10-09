---
title: aaaDevelop Azure Functions met Media Services
description: Dit onderwerp leest hoe toostart ontwikkelen van Azure Functions met het gebruik van Media Services hello Azure-portal.
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
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a>Azure Functions met mediaservices te ontwikkelen

Dit onderwerp leest u hoe tooget gestart met het Azure-functies die gebruikmaken van Media Services maken. Hello Azure-functie is gedefinieerd in dit onderwerp wordt een storage-account-container met de naam bewaakt **invoer** voor nieuwe MP4-bestanden. Wanneer een bestand wordt verwijderd in de storage-container hello, kan Hallo blob trigger Hallo-functie wordt uitgevoerd.

Als u wilt dat tooexplore en bestaande Azure-functies die gebruikmaken van Azure Media Services te implementeren, Bekijk [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Deze repository bevat voorbeelden die de Media Services tooshow werkstromen gerelateerde tooingesting inhoud rechtstreeks uit blob storage codering en -inhoud weggeschreven back tooblob opslag gebruiken. Dit omvat ook voorbeelden van hoe toomonitor taak meldingen via WebHooks en wachtrijen in Azure. U kunt ook uw functies op basis van de voorbeelden in Hallo Hallo ontwikkelen [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) opslagplaats. toodeploy hello functies, drukt u op Hallo **tooAzure implementeren** knop.

## <a name="prerequisites"></a>Vereisten

- Voordat u uw eerste functie maken kunt, moet u toohave een actief Azure-account. Als u nog geen Azure-account hebt, zijn er [gratis accounts beschikbaar](https://azure.microsoft.com/free/).
- Als u toocreate Azure Functions die acties uitvoeren op uw account voor Azure Media Services (AMS) of luisteren tooevents verzonden door Media Services gaat, moet u een AMS-account maken zoals beschreven [hier](media-services-portal-create-account.md).
- Kennis van [hoe toouse Azure functions](../azure-functions/functions-overview.md). Bekijk ook:
    - [HTTP- en webhook bindingen van Azure functions](../azure-functions/functions-triggers-bindings.md)
    - [Hoe tooconfigure Azure-functie app-instellingen](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Overwegingen

-  Azure Functions uitgevoerd onder Hallo verbruik plan hebben 5 minuten time-out beperken.

## <a name="create-a-function-app"></a>Een functie-app maken

1. Ga toohello [Azure-portal](http://portal.azure.com) en aanmelden met uw Azure-account.
2. Maken van een functie-app, zoals wordt beschreven [hier](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Een opslagaccount dat u in Hallo opgeeft **StorageConnection** omgevingsvariabele hello (Zie de volgende stap Hallo) moet dezelfde regio bevinden als uw app.

## <a name="configure-function-app-settings"></a>De functie app-instellingen configureren

Bij het ontwikkelen van Media Services-functies, is het handig tooadd omgevingsvariabelen die worden gebruikt in uw functies. tooconfigure app-instellingen, klikt u op Hallo App-instellingen configureren koppeling. Zie voor meer informatie [hoe Azure-functie app-instellingen tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

Bijvoorbeeld:

![Instellingen](./media/media-services-azure-functions/media-services-azure-functions001.png)

Hallo-functie, gedefinieerd in dit artikel wordt ervan uitgegaan dat er Hallo omgevingsvariabelen in de instellingen van uw app te volgen:

**AMSAccount** : *AMS-accountnaam* (bijvoorbeeld testams)

**AMSKey** : *AMS accountsleutel* (bijvoorbeeld IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)

**MediaServicesStorageAccountName** : *opslagaccountnaam* (bijv, testamsstorage)

**MediaServicesStorageAccountKey** : *opslagaccountsleutel* (bijv, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)

**StorageConnection** : *opslagverbinding* (bijv, DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey = xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX ==)

## <a name="create-a-function"></a>Een functie maken

Als de functie-app is geïmplementeerd, kunt u het vinden onder **App Services** Azure Functions.

1. Selecteer de functie-app en klik op **nieuwe functie**.
2. Kies Hallo **C#** taal en **gegevensverwerking** scenario.
3. Kies **BlobTrigger** sjabloon. Deze functie wordt geactiveerd wanneer een blob is geüpload naar Hallo **invoer** container. Hallo **invoer** naam is opgegeven in Hallo **pad**, in de volgende stap Hallo.

    ![Bestanden](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. Als u hebt geselecteerd **BlobTrigger**, sommige meer besturingselementen op Hallo pagina wordt weergegeven.

    ![Bestanden](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. Klik op **Create**. 


## <a name="files"></a>Bestanden

Uw Azure-functie is gekoppeld aan het codebestanden en andere bestanden die in deze sectie worden beschreven. Een functie is standaard gekoppeld aan **function.json** en **run.csx** (C#)-bestanden. U moet tooadd een **project.json** bestand. Hallo rest van deze sectie bevat de definities Hallo voor deze bestanden.

![Bestanden](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>Function.JSON

Hallo function.json bestand definieert het Hallo-functiebindingen en andere configuratie-instellingen. Hallo runtime maakt gebruik van dit bestand toodetermine Hallo gebeurtenissen toomonitor en hoe werken uitvoering toopass gegevens in en gegevens uit. Zie voor meer informatie [HTTP- en webhook bindingen van Azure functions](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Set Hallo **uitgeschakeld** eigenschap te**true** tooprevent Hallo functie uit te voeren. 


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

Hallo project.json bestand bevat de afhankelijkheden. Hier volgt een voorbeeld van **project.json** bestand met de Hallo vereist .NET Azure Media Services vanuit Nuget-pakketten. Houd er rekening mee dat Hallo versienummers worden gewijzigd met de meest recente updates toohello pakketten, zodat u de meest recente versies hello te bevestigen. 

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

Dit is Hallo C#-code voor de functie.  Hallo-functie zoals hieronder gedefinieerd, monitors een storage-account-container met de naam **invoer** (die is wat is opgegeven in het Hallo-pad) voor nieuwe MP4-bestanden. Wanneer een bestand wordt verwijderd in de storage-container hello, kan Hallo blob trigger Hallo-functie wordt uitgevoerd.
    
Hallo-voorbeeld gedefinieerd in deze sectie bevat 

1. hoe tooingest activa in een Media Services-account (door een blob kopiëren naar een asset AMS) en 
2. hoe toosubmit een codeertaak die gebruikmaakt van Media Encoder Standard van 'adaptief streamen' vooraf ingesteld.

In Hallo praktijk scenario hebt u waarschijnlijk wilt de voortgang van de taak tootrack en vervolgens de gecodeerde asset te publiceren. Zie voor meer informatie [gebruik Azure WebHooks toomonitor Media Services taak meldingen](media-services-dotnet-check-job-progress-with-webhooks.md). Zie voor meer voorbeelden [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

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
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
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
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
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

        // Get hello destination asset container reference
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

        // Get hold of hello destination blob
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

tootest uw functie, moet u een MP4-bestand naar Hallo tooupload **invoer** container van Hallo storage-account die u hebt opgegeven in de verbindingsreeks Hallo.  

## <a name="next-step"></a>Volgende stap

U bent nu klaar toostart ontwikkelen van een Media Services-toepassing. 
 
Zie voor meer informatie en volledige samples/oplossingen van het gebruik van Azure Functions en Logic Apps met Azure Media Services toocreate maken van aangepaste inhoud werkstromen Hallo [Media Services .NET-functies Integraiton voorbeeld op GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Zie ook [gebruik Azure WebHooks toomonitor Media Services taak meldingen met .NET](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

