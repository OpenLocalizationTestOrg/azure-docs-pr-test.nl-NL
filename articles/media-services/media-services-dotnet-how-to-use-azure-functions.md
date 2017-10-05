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
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="35e34-103">Azure Functions met mediaservices te ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="35e34-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="35e34-104">Dit onderwerp leest u hoe u aan de slag met Azure-functies die gebruikmaken van Media Services maken.</span><span class="sxs-lookup"><span data-stu-id="35e34-104">This topic shows you how to get started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="35e34-105">De Azure-functie die is gedefinieerd in dit onderwerp wordt een storage-account-container met de naam bewaakt **invoer** voor nieuwe MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="35e34-105">The Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="35e34-106">Wanneer een bestand in de storage-container is verbroken, kan de blob-trigger de functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="35e34-106">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>

<span data-ttu-id="35e34-107">Als u wilt verkennen en implementeren van de bestaande Azure-functies die gebruikmaken van Azure Media Services, Bekijk [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="35e34-107">If you want to explore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="35e34-108">Deze repository bevat voorbeelden van Media Services gebruiken om werkstromen die betrekking hebben op het opnemen van inhoud rechtstreeks uit blob storage codering en -inhoud weggeschreven terug naar blob-opslag weer te geven.</span><span class="sxs-lookup"><span data-stu-id="35e34-108">This repository contains examples that use Media Services to show workflows related to ingesting content directly from blob storage, encoding, and writing content back to blob storage.</span></span> <span data-ttu-id="35e34-109">Dit omvat ook voorbeelden van het bewaken van de taak meldingen via WebHooks en wachtrijen in Azure.</span><span class="sxs-lookup"><span data-stu-id="35e34-109">It also includes examples of how to monitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="35e34-110">U kunt ook uw functies op basis van de voorbeelden in ontwikkelen de [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="35e34-110">You can also develop your Functions based on the examples in the [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="35e34-111">Voor het implementeren van de functies, drukt u op de **implementeren in Azure** knop.</span><span class="sxs-lookup"><span data-stu-id="35e34-111">To deploy the functions, press the **Deploy to Azure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35e34-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="35e34-112">Prerequisites</span></span>

- <span data-ttu-id="35e34-113">Voordat u uw eerste functie kunt maken, moet u een actief Azure-account hebben.</span><span class="sxs-lookup"><span data-stu-id="35e34-113">Before you can create your first function, you need to have an active Azure account.</span></span> <span data-ttu-id="35e34-114">Als u nog geen Azure-account hebt, zijn er [gratis accounts beschikbaar](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="35e34-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="35e34-115">Als u maken van Azure Functions die acties uitvoeren op uw account voor Azure Media Services (AMS) of gebeurtenissen die door Media Services wordt verzonden wilt, moet u een AMS-account maken zoals beschreven [hier](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="35e34-115">If you are going to create Azure Functions that perform actions on your Azure Media Services (AMS) account or listen to events sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="35e34-116">Kennis van [het gebruik van Azure functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="35e34-116">Understanding of [how to use Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="35e34-117">Bekijk ook:</span><span class="sxs-lookup"><span data-stu-id="35e34-117">Also, review:</span></span>
    - [<span data-ttu-id="35e34-118">HTTP- en webhook bindingen van Azure functions</span><span class="sxs-lookup"><span data-stu-id="35e34-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="35e34-119">Het Azure-functie app-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="35e34-119">How to configure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="35e34-120">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="35e34-120">Considerations</span></span>

-  <span data-ttu-id="35e34-121">Azure Functions uitgevoerd onder het plan verbruik hebben 5 minuten time-out beperken.</span><span class="sxs-lookup"><span data-stu-id="35e34-121">Azure Functions running under the Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="35e34-122">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="35e34-122">Create a function app</span></span>

1. <span data-ttu-id="35e34-123">Ga naar de [Azure-portal](http://portal.azure.com) en meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="35e34-123">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="35e34-124">Maken van een functie-app, zoals wordt beschreven [hier](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35e34-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="35e34-125">Een opslagaccount dat u opgeeft in de **StorageConnection** omgevingsvariabele (Zie de volgende stap) moet in dezelfde regio bevinden als uw app.</span><span class="sxs-lookup"><span data-stu-id="35e34-125">A storage account that you specify in the **StorageConnection** environment variable (see the next step) should be in the same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="35e34-126">De functie app-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="35e34-126">Configure function app settings</span></span>

<span data-ttu-id="35e34-127">Bij het ontwikkelen van Media Services-functies, is het handig om toe te voegen omgevingsvariabelen die worden gebruikt in uw functies.</span><span class="sxs-lookup"><span data-stu-id="35e34-127">When developing Media Services functions, it is handy to add environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="35e34-128">Klik op de koppeling instellingen van de App appinstellingen configureren.</span><span class="sxs-lookup"><span data-stu-id="35e34-128">To configure app settings, click the Configure App Settings link.</span></span> <span data-ttu-id="35e34-129">Zie voor meer informatie [Azure-functie app-instellingen configureren](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="35e34-129">For more information, see  [How to configure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="35e34-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="35e34-130">For example:</span></span>

![Instellingen](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="35e34-132">De functie, gedefinieerd in dit artikel wordt ervan uitgegaan dat u hebt de volgende omgevingsvariabelen in de instellingen van uw app:</span><span class="sxs-lookup"><span data-stu-id="35e34-132">The function, defined in this article, assumes you have the following environment variables in your app settings:</span></span>

<span data-ttu-id="35e34-133">**AMSAccount** : *AMS-accountnaam* (bijvoorbeeld testams)</span><span class="sxs-lookup"><span data-stu-id="35e34-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="35e34-134">**AMSKey** : *AMS accountsleutel* (bijvoorbeeld IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)</span><span class="sxs-lookup"><span data-stu-id="35e34-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="35e34-135">**MediaServicesStorageAccountName** : *opslagaccountnaam* (bijv, testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="35e34-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="35e34-136">**MediaServicesStorageAccountKey** : *opslagaccountsleutel* (bijv, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)</span><span class="sxs-lookup"><span data-stu-id="35e34-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="35e34-137">**StorageConnection** : *opslagverbinding* (bijv, DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey = xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX ==)</span><span class="sxs-lookup"><span data-stu-id="35e34-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="35e34-138">Een functie maken</span><span class="sxs-lookup"><span data-stu-id="35e34-138">Create a function</span></span>

<span data-ttu-id="35e34-139">Als de functie-app is geïmplementeerd, kunt u het vinden onder **App Services** Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="35e34-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="35e34-140">Selecteer de functie-app en klik op **nieuwe functie**.</span><span class="sxs-lookup"><span data-stu-id="35e34-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="35e34-141">Kies de **C#** taal en **gegevensverwerking** scenario.</span><span class="sxs-lookup"><span data-stu-id="35e34-141">Choose the **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="35e34-142">Kies **BlobTrigger** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="35e34-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="35e34-143">Deze functie wordt geactiveerd wanneer een blob is geüpload naar de **invoer** container.</span><span class="sxs-lookup"><span data-stu-id="35e34-143">This function will be triggered whenever a blob is uploaded into the **input** container.</span></span> <span data-ttu-id="35e34-144">De **invoer** naam is opgegeven in de **pad**, in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="35e34-144">The **input** name is specified in the **Path**, in the next step.</span></span>

    ![Bestanden](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="35e34-146">Als u hebt geselecteerd **BlobTrigger**, sommige meer besturingselementen op de pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="35e34-146">Once you select **BlobTrigger**, some more controls will appear on the page.</span></span>

    ![Bestanden](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="35e34-148">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="35e34-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="35e34-149">Bestanden</span><span class="sxs-lookup"><span data-stu-id="35e34-149">Files</span></span>

<span data-ttu-id="35e34-150">Uw Azure-functie is gekoppeld aan het codebestanden en andere bestanden die in deze sectie worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="35e34-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="35e34-151">Een functie is standaard gekoppeld aan **function.json** en **run.csx** (C#)-bestanden.</span><span class="sxs-lookup"><span data-stu-id="35e34-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="35e34-152">U moet toevoegen een **project.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="35e34-152">You will need to add a **project.json** file.</span></span> <span data-ttu-id="35e34-153">De rest van deze sectie bevat de definities voor deze bestanden.</span><span class="sxs-lookup"><span data-stu-id="35e34-153">The rest of this section shows the definitions for these files.</span></span>

![Bestanden](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="35e34-155">Function.JSON</span><span class="sxs-lookup"><span data-stu-id="35e34-155">function.json</span></span>

<span data-ttu-id="35e34-156">Het bestand function.json definieert de functiebindingen en andere configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="35e34-156">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="35e34-157">De runtime maakt gebruik van dit bestand om te bepalen welke gebeurtenissen u wilt bewaken en het doorgeven van gegevens in en gegevens retourneren van een functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="35e34-157">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="35e34-158">Zie voor meer informatie [HTTP- en webhook bindingen van Azure functions](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="35e34-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="35e34-159">Stel de **uitgeschakeld** eigenschap **true** om te voorkomen dat de functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="35e34-159">Set the **disabled** property to **true** to prevent the function from being executed.</span></span> 


<span data-ttu-id="35e34-160">Hier volgt een voorbeeld van **function.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="35e34-160">Here is an example of **function.json** file.</span></span>

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

### <a name="projectjson"></a><span data-ttu-id="35e34-161">Project.JSON</span><span class="sxs-lookup"><span data-stu-id="35e34-161">project.json</span></span>

<span data-ttu-id="35e34-162">Het bestand project.json bevat afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="35e34-162">The project.json file contains dependencies.</span></span> <span data-ttu-id="35e34-163">Hier volgt een voorbeeld van **project.json** bestand met de vereiste .NET Azure Media Services-pakketten vanuit Nuget.</span><span class="sxs-lookup"><span data-stu-id="35e34-163">Here is an example of **project.json** file that includes the required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="35e34-164">Houd er rekening mee dat de versienummers worden gewijzigd met de meest recente updates op de pakketten, zodat de meest recente versies dient u te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="35e34-164">Note that the version numbers will change with latest updates to the packages, so you should confirm the most recent versions.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="35e34-165">Run.csx</span><span class="sxs-lookup"><span data-stu-id="35e34-165">run.csx</span></span>

<span data-ttu-id="35e34-166">Dit is de C#-code voor de functie.</span><span class="sxs-lookup"><span data-stu-id="35e34-166">This is the C# code for your function.</span></span>  <span data-ttu-id="35e34-167">De functie zoals hieronder gedefinieerd, monitors een storage-account-container met de naam **invoer** (die is opgegeven in het pad) voor nieuwe MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="35e34-167">The function defined below monitors a storage account container named **input** (that is what was specified in the path) for new MP4 files.</span></span> <span data-ttu-id="35e34-168">Wanneer een bestand in de storage-container is verbroken, kan de blob-trigger de functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="35e34-168">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>
    
<span data-ttu-id="35e34-169">Het voorbeeld dat is gedefinieerd in deze sectie bevat</span><span class="sxs-lookup"><span data-stu-id="35e34-169">The example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="35e34-170">het opnemen van een actief naar een Media Services-account (door een blob kopiëren naar een asset AMS) en</span><span class="sxs-lookup"><span data-stu-id="35e34-170">how to ingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="35e34-171">hoe naar een codeertaak verzendt die gebruikmaakt van Media Encoder Standard van 'Adaptief streamen' vooraf ingesteld.</span><span class="sxs-lookup"><span data-stu-id="35e34-171">how to submit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="35e34-172">In het scenario praktijk wilt u waarschijnlijk taak voortgang volgen en vervolgens de gecodeerde asset te publiceren.</span><span class="sxs-lookup"><span data-stu-id="35e34-172">In the real life scenario, you most likely want to track job progress and then publish your encoded asset.</span></span> <span data-ttu-id="35e34-173">Zie voor meer informatie [gebruik Azure WebHooks voor het bewaken van Media Services taak meldingen](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="35e34-173">For more information, see [Use Azure WebHooks to monitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="35e34-174">Zie voor meer voorbeelden [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="35e34-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="35e34-175">Wanneer u klaar bent voor het definiëren van de functie klikt u op **opslaan en uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="35e34-175">Once you are done defining your function click **Save and Run**.</span></span>

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
##<a name="test-your-function"></a><span data-ttu-id="35e34-176">De functie testen</span><span class="sxs-lookup"><span data-stu-id="35e34-176">Test your function</span></span>

<span data-ttu-id="35e34-177">Als u wilt uw functie testen, moet u voor het uploaden van een MP4-bestand in de **invoer** container van het opslagaccount dat u hebt opgegeven in de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="35e34-177">To test your function, you need to upload an MP4 file into the **input** container of the storage account that you specified in the connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="35e34-178">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="35e34-178">Next step</span></span>

<span data-ttu-id="35e34-179">U bent nu klaar om te beginnen met het ontwikkelen van een Media Services-toepassing.</span><span class="sxs-lookup"><span data-stu-id="35e34-179">At this point, you are ready to start developing a Media Services application.</span></span> 
 
<span data-ttu-id="35e34-180">Zie voor meer informatie en volledige samples/oplossingen van het gebruik van Azure Functions en Logic Apps met Azure Media Services voor het maken van aangepaste inhoud werkstromen maken, de [Media Services .NET-functies Integraiton voorbeeld op GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="35e34-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services to create custom content creation workflows, see the [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="35e34-181">Zie ook [WebHooks van gebruik Azure Media Services taak meldingen met .NET bewaken](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="35e34-181">Also, see [Use Azure WebHooks to monitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="35e34-182">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="35e34-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="35e34-183">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="35e34-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

