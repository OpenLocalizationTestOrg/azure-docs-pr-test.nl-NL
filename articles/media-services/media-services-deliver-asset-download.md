---
title: aaaDownload Media Services activa tooyour computer - Azure | Microsoft Docs
description: Meer informatie over toodownload activa tooyour computer. Codevoorbeelden zijn geschreven in C# en gebruiken van Hallo Media Services SDK voor .NET.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 6c6e764720caa59d8371178a2682700345f7bc57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="45eaf-104">Procedure: een Asset door Download leveren</span><span class="sxs-lookup"><span data-stu-id="45eaf-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="45eaf-105">In dit onderwerp wordt beschreven opties voor tooMedia Services leveren van media-elementen worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="45eaf-105">This topic discusses options for delivering media assets uploaded tooMedia Services.</span></span> <span data-ttu-id="45eaf-106">U kunt inhoud in Media Services leveren in talloze scenario's van toepassing.</span><span class="sxs-lookup"><span data-stu-id="45eaf-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="45eaf-107">U kunt downloaden van media-elementen of toegang tot deze met behulp van een locator.</span><span class="sxs-lookup"><span data-stu-id="45eaf-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="45eaf-108">U kunt media-inhoud tooanother toepassing of tooanother inhoudsprovider verzenden.</span><span class="sxs-lookup"><span data-stu-id="45eaf-108">You can send media content tooanother application or tooanother content provider.</span></span> <span data-ttu-id="45eaf-109">U kunt ook inhoud met behulp van een inhoud Delivery Network (CDN) voor betere prestaties en schaalbaarheid leveren.</span><span class="sxs-lookup"><span data-stu-id="45eaf-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="45eaf-110">Dit voorbeeld ziet u hoe toodownload media-elementen van Media Services tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="45eaf-110">This example shows how toodownload media assets from Media Services tooyour local computer.</span></span> <span data-ttu-id="45eaf-111">Hallo code query's Hallo taken die zijn gekoppeld aan Hallo Media Services-account door de taak-ID en toegang tot de **OutputMediaAssets** verzameling (dit is Hallo set van een of meer uitvoer media-elementen die het resultaat is van een taak wordt uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="45eaf-111">hello code queries hello jobs associated with hello Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is hello set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="45eaf-112">Dit voorbeeld toont hoe toodownload uitvoermedia activa van een taak, maar u kunnen toepassen Hallo dezelfde benadering toodownload andere activa.</span><span class="sxs-lookup"><span data-stu-id="45eaf-112">This  example shows how toodownload output media assets from a job, but you can apply hello same approach toodownload other assets.</span></span>

>[!NOTE]
><span data-ttu-id="45eaf-113">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="45eaf-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="45eaf-114">Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn).</span><span class="sxs-lookup"><span data-stu-id="45eaf-114">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="45eaf-115">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="45eaf-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download hello output asset of hello specified job tooa local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how toodownload a single asset. 
        // However, you can iterate through hello OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference toohello job. 
        IJob job = GetJob(jobId);

        // Get a reference toohello first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator toodownload hello asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use hello following event handler toocheck download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="45eaf-116">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="45eaf-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="45eaf-117">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="45eaf-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="45eaf-118">Zie ook</span><span class="sxs-lookup"><span data-stu-id="45eaf-118">See Also</span></span>
[<span data-ttu-id="45eaf-119">Streaming inhoud leveren</span><span class="sxs-lookup"><span data-stu-id="45eaf-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

