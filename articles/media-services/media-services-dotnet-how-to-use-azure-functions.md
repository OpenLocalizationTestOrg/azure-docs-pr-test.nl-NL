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
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="91a61-103">Azure Functions met mediaservices te ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="91a61-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="91a61-104">Dit onderwerp leest u hoe tooget gestart met het Azure-functies die gebruikmaken van Media Services maken.</span><span class="sxs-lookup"><span data-stu-id="91a61-104">This topic shows you how tooget started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="91a61-105">Hello Azure-functie is gedefinieerd in dit onderwerp wordt een storage-account-container met de naam bewaakt **invoer** voor nieuwe MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="91a61-105">hello Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="91a61-106">Wanneer een bestand wordt verwijderd in de storage-container hello, kan Hallo blob trigger Hallo-functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="91a61-106">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>

<span data-ttu-id="91a61-107">Als u wilt dat tooexplore en bestaande Azure-functies die gebruikmaken van Azure Media Services te implementeren, Bekijk [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="91a61-107">If you want tooexplore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="91a61-108">Deze repository bevat voorbeelden die de Media Services tooshow werkstromen gerelateerde tooingesting inhoud rechtstreeks uit blob storage codering en -inhoud weggeschreven back tooblob opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="91a61-108">This repository contains examples that use Media Services tooshow workflows related tooingesting content directly from blob storage, encoding, and writing content back tooblob storage.</span></span> <span data-ttu-id="91a61-109">Dit omvat ook voorbeelden van hoe toomonitor taak meldingen via WebHooks en wachtrijen in Azure.</span><span class="sxs-lookup"><span data-stu-id="91a61-109">It also includes examples of how toomonitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="91a61-110">U kunt ook uw functies op basis van de voorbeelden in Hallo Hallo ontwikkelen [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="91a61-110">You can also develop your Functions based on hello examples in hello [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="91a61-111">toodeploy hello functies, drukt u op Hallo **tooAzure implementeren** knop.</span><span class="sxs-lookup"><span data-stu-id="91a61-111">toodeploy hello functions, press hello **Deploy tooAzure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91a61-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="91a61-112">Prerequisites</span></span>

- <span data-ttu-id="91a61-113">Voordat u uw eerste functie maken kunt, moet u toohave een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="91a61-113">Before you can create your first function, you need toohave an active Azure account.</span></span> <span data-ttu-id="91a61-114">Als u nog geen Azure-account hebt, zijn er [gratis accounts beschikbaar](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="91a61-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="91a61-115">Als u toocreate Azure Functions die acties uitvoeren op uw account voor Azure Media Services (AMS) of luisteren tooevents verzonden door Media Services gaat, moet u een AMS-account maken zoals beschreven [hier](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="91a61-115">If you are going toocreate Azure Functions that perform actions on your Azure Media Services (AMS) account or listen tooevents sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="91a61-116">Kennis van [hoe toouse Azure functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91a61-116">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="91a61-117">Bekijk ook:</span><span class="sxs-lookup"><span data-stu-id="91a61-117">Also, review:</span></span>
    - [<span data-ttu-id="91a61-118">HTTP- en webhook bindingen van Azure functions</span><span class="sxs-lookup"><span data-stu-id="91a61-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="91a61-119">Hoe tooconfigure Azure-functie app-instellingen</span><span class="sxs-lookup"><span data-stu-id="91a61-119">How tooconfigure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="91a61-120">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="91a61-120">Considerations</span></span>

-  <span data-ttu-id="91a61-121">Azure Functions uitgevoerd onder Hallo verbruik plan hebben 5 minuten time-out beperken.</span><span class="sxs-lookup"><span data-stu-id="91a61-121">Azure Functions running under hello Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="91a61-122">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="91a61-122">Create a function app</span></span>

1. <span data-ttu-id="91a61-123">Ga toohello [Azure-portal](http://portal.azure.com) en aanmelden met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="91a61-123">Go toohello [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="91a61-124">Maken van een functie-app, zoals wordt beschreven [hier](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="91a61-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="91a61-125">Een opslagaccount dat u in Hallo opgeeft **StorageConnection** omgevingsvariabele hello (Zie de volgende stap Hallo) moet dezelfde regio bevinden als uw app.</span><span class="sxs-lookup"><span data-stu-id="91a61-125">A storage account that you specify in hello **StorageConnection** environment variable (see hello next step) should be in hello same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="91a61-126">De functie app-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="91a61-126">Configure function app settings</span></span>

<span data-ttu-id="91a61-127">Bij het ontwikkelen van Media Services-functies, is het handig tooadd omgevingsvariabelen die worden gebruikt in uw functies.</span><span class="sxs-lookup"><span data-stu-id="91a61-127">When developing Media Services functions, it is handy tooadd environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="91a61-128">tooconfigure app-instellingen, klikt u op Hallo App-instellingen configureren koppeling.</span><span class="sxs-lookup"><span data-stu-id="91a61-128">tooconfigure app settings, click hello Configure App Settings link.</span></span> <span data-ttu-id="91a61-129">Zie voor meer informatie [hoe Azure-functie app-instellingen tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="91a61-129">For more information, see  [How tooconfigure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="91a61-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="91a61-130">For example:</span></span>

![Instellingen](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="91a61-132">Hallo-functie, gedefinieerd in dit artikel wordt ervan uitgegaan dat er Hallo omgevingsvariabelen in de instellingen van uw app te volgen:</span><span class="sxs-lookup"><span data-stu-id="91a61-132">hello function, defined in this article, assumes you have hello following environment variables in your app settings:</span></span>

<span data-ttu-id="91a61-133">**AMSAccount** : *AMS-accountnaam* (bijvoorbeeld testams)</span><span class="sxs-lookup"><span data-stu-id="91a61-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="91a61-134">**AMSKey** : *AMS accountsleutel* (bijvoorbeeld IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)</span><span class="sxs-lookup"><span data-stu-id="91a61-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="91a61-135">**MediaServicesStorageAccountName** : *opslagaccountnaam* (bijv, testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="91a61-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="91a61-136">**MediaServicesStorageAccountKey** : *opslagaccountsleutel* (bijv, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)</span><span class="sxs-lookup"><span data-stu-id="91a61-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="91a61-137">**StorageConnection** : *opslagverbinding* (bijv, DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey = xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX ==)</span><span class="sxs-lookup"><span data-stu-id="91a61-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="91a61-138">Een functie maken</span><span class="sxs-lookup"><span data-stu-id="91a61-138">Create a function</span></span>

<span data-ttu-id="91a61-139">Als de functie-app is geïmplementeerd, kunt u het vinden onder **App Services** Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="91a61-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="91a61-140">Selecteer de functie-app en klik op **nieuwe functie**.</span><span class="sxs-lookup"><span data-stu-id="91a61-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="91a61-141">Kies Hallo **C#** taal en **gegevensverwerking** scenario.</span><span class="sxs-lookup"><span data-stu-id="91a61-141">Choose hello **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="91a61-142">Kies **BlobTrigger** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="91a61-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="91a61-143">Deze functie wordt geactiveerd wanneer een blob is geüpload naar Hallo **invoer** container.</span><span class="sxs-lookup"><span data-stu-id="91a61-143">This function will be triggered whenever a blob is uploaded into hello **input** container.</span></span> <span data-ttu-id="91a61-144">Hallo **invoer** naam is opgegeven in Hallo **pad**, in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="91a61-144">hello **input** name is specified in hello **Path**, in hello next step.</span></span>

    ![Bestanden](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="91a61-146">Als u hebt geselecteerd **BlobTrigger**, sommige meer besturingselementen op Hallo pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="91a61-146">Once you select **BlobTrigger**, some more controls will appear on hello page.</span></span>

    ![Bestanden](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="91a61-148">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="91a61-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="91a61-149">Bestanden</span><span class="sxs-lookup"><span data-stu-id="91a61-149">Files</span></span>

<span data-ttu-id="91a61-150">Uw Azure-functie is gekoppeld aan het codebestanden en andere bestanden die in deze sectie worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="91a61-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="91a61-151">Een functie is standaard gekoppeld aan **function.json** en **run.csx** (C#)-bestanden.</span><span class="sxs-lookup"><span data-stu-id="91a61-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="91a61-152">U moet tooadd een **project.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="91a61-152">You will need tooadd a **project.json** file.</span></span> <span data-ttu-id="91a61-153">Hallo rest van deze sectie bevat de definities Hallo voor deze bestanden.</span><span class="sxs-lookup"><span data-stu-id="91a61-153">hello rest of this section shows hello definitions for these files.</span></span>

![Bestanden](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="91a61-155">Function.JSON</span><span class="sxs-lookup"><span data-stu-id="91a61-155">function.json</span></span>

<span data-ttu-id="91a61-156">Hallo function.json bestand definieert het Hallo-functiebindingen en andere configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="91a61-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="91a61-157">Hallo runtime maakt gebruik van dit bestand toodetermine Hallo gebeurtenissen toomonitor en hoe werken uitvoering toopass gegevens in en gegevens uit.</span><span class="sxs-lookup"><span data-stu-id="91a61-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="91a61-158">Zie voor meer informatie [HTTP- en webhook bindingen van Azure functions](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="91a61-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="91a61-159">Set Hallo **uitgeschakeld** eigenschap te**true** tooprevent Hallo functie uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="91a61-159">Set hello **disabled** property too**true** tooprevent hello function from being executed.</span></span> 


<span data-ttu-id="91a61-160">Hier volgt een voorbeeld van **function.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="91a61-160">Here is an example of **function.json** file.</span></span>

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

### <a name="projectjson"></a><span data-ttu-id="91a61-161">Project.JSON</span><span class="sxs-lookup"><span data-stu-id="91a61-161">project.json</span></span>

<span data-ttu-id="91a61-162">Hallo project.json bestand bevat de afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="91a61-162">hello project.json file contains dependencies.</span></span> <span data-ttu-id="91a61-163">Hier volgt een voorbeeld van **project.json** bestand met de Hallo vereist .NET Azure Media Services vanuit Nuget-pakketten.</span><span class="sxs-lookup"><span data-stu-id="91a61-163">Here is an example of **project.json** file that includes hello required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="91a61-164">Houd er rekening mee dat Hallo versienummers worden gewijzigd met de meest recente updates toohello pakketten, zodat u de meest recente versies hello te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="91a61-164">Note that hello version numbers will change with latest updates toohello packages, so you should confirm hello most recent versions.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="91a61-165">Run.csx</span><span class="sxs-lookup"><span data-stu-id="91a61-165">run.csx</span></span>

<span data-ttu-id="91a61-166">Dit is Hallo C#-code voor de functie.</span><span class="sxs-lookup"><span data-stu-id="91a61-166">This is hello C# code for your function.</span></span>  <span data-ttu-id="91a61-167">Hallo-functie zoals hieronder gedefinieerd, monitors een storage-account-container met de naam **invoer** (die is wat is opgegeven in het Hallo-pad) voor nieuwe MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="91a61-167">hello function defined below monitors a storage account container named **input** (that is what was specified in hello path) for new MP4 files.</span></span> <span data-ttu-id="91a61-168">Wanneer een bestand wordt verwijderd in de storage-container hello, kan Hallo blob trigger Hallo-functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="91a61-168">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>
    
<span data-ttu-id="91a61-169">Hallo-voorbeeld gedefinieerd in deze sectie bevat</span><span class="sxs-lookup"><span data-stu-id="91a61-169">hello example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="91a61-170">hoe tooingest activa in een Media Services-account (door een blob kopiëren naar een asset AMS) en</span><span class="sxs-lookup"><span data-stu-id="91a61-170">how tooingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="91a61-171">hoe toosubmit een codeertaak die gebruikmaakt van Media Encoder Standard van 'adaptief streamen' vooraf ingesteld.</span><span class="sxs-lookup"><span data-stu-id="91a61-171">how toosubmit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="91a61-172">In Hallo praktijk scenario hebt u waarschijnlijk wilt de voortgang van de taak tootrack en vervolgens de gecodeerde asset te publiceren.</span><span class="sxs-lookup"><span data-stu-id="91a61-172">In hello real life scenario, you most likely want tootrack job progress and then publish your encoded asset.</span></span> <span data-ttu-id="91a61-173">Zie voor meer informatie [gebruik Azure WebHooks toomonitor Media Services taak meldingen](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="91a61-173">For more information, see [Use Azure WebHooks toomonitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="91a61-174">Zie voor meer voorbeelden [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="91a61-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="91a61-175">Wanneer u klaar bent voor het definiëren van de functie klikt u op **opslaan en uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="91a61-175">Once you are done defining your function click **Save and Run**.</span></span>

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
##<a name="test-your-function"></a><span data-ttu-id="91a61-176">De functie testen</span><span class="sxs-lookup"><span data-stu-id="91a61-176">Test your function</span></span>

<span data-ttu-id="91a61-177">tootest uw functie, moet u een MP4-bestand naar Hallo tooupload **invoer** container van Hallo storage-account die u hebt opgegeven in de verbindingsreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="91a61-177">tootest your function, you need tooupload an MP4 file into hello **input** container of hello storage account that you specified in hello connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="91a61-178">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="91a61-178">Next step</span></span>

<span data-ttu-id="91a61-179">U bent nu klaar toostart ontwikkelen van een Media Services-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91a61-179">At this point, you are ready toostart developing a Media Services application.</span></span> 
 
<span data-ttu-id="91a61-180">Zie voor meer informatie en volledige samples/oplossingen van het gebruik van Azure Functions en Logic Apps met Azure Media Services toocreate maken van aangepaste inhoud werkstromen Hallo [Media Services .NET-functies Integraiton voorbeeld op GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="91a61-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services toocreate custom content creation workflows, see hello [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="91a61-181">Zie ook [gebruik Azure WebHooks toomonitor Media Services taak meldingen met .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="91a61-181">Also, see [Use Azure WebHooks toomonitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="91a61-182">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="91a61-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="91a61-183">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="91a61-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

