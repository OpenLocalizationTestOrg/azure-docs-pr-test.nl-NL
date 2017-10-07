---
title: Media-bestanden met Azure Media Hyperlapse aaaHyperlapse | Microsoft Docs
description: Azure Media Hyperlapse maakt smooth verstreken tijd video's van de eerste persoon of actie camera inhoud. Dit onderwerp wordt beschreven hoe toouse Media indexeerfunctie.
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a>Hyperlapse Media-bestanden met Azure Media Hyperlapse
Azure Media Hyperlapse is een Media Processor (MP) die u smooth video's verstreken tijd van eerste persoon of actie camera inhoud maakt.  cloud-gebaseerd op hetzelfde niveau te Hallo[van Microsoft Research bureaublad Hyperlapse Pro en Hyperlapse mobiele telefoon](http://aka.ms/hyperlapse), Hallo grootschalige Hallo Azure Media Services Media maakt gebruik van Microsoft Hyperlapse voor Azure Media Services De verwerking van platform toohorizontally schalen en bulksgewijs parallelize Hyperlapse verwerking.

> [!IMPORTANT]
> Microsoft Hyperlapse is ontworpen toowork geschikt is voor de eerste persoon inhoud met een zwevend camera.  Hoewel u nog steeds camerabeelden kunt nog steeds werken, kunnen niet Hallo prestaties en kwaliteit van hello Azure Media Hyperlapse Media-Processor worden gegarandeerd voor andere typen inhoud.  meer informatie over Microsoft Hyperlapse voor Azure Media Services toolearn en bekijk enkele voorbeeld-video's, bekijk Hallo [inleidende blogbericht](http://aka.ms/azurehyperlapseblog) van Hallo openbare preview.
> 
> 

Een Azure Media Hyperlapse taak als neemt invoer een MP4, MOV of WMV assetbestand samen met een configuratiebestand dat Hiermee wordt aangegeven welke frames van video moeten verstreken tijd en toowhat snelheid (bijvoorbeeld de eerste 10.000 frames 2 x).  Hallo-uitvoer is een weergave gestabiliseerd en verstreken tijd van Hallo invoervideo.

Zie voor de meest recente Azure Media Hyperlapse updates hello, [Media Services-blogs](https://azure.microsoft.com/blog/topics/media-services/).

## <a name="hyperlapse-an-asset"></a>Hyperlapse een asset
Eerst moet u tooupload uw gewenste invoerbestand tooAzure Media Services.  Hallo toolearn informatie over concepten die betrokken zijn bij het uploaden en beheren van inhoud, Hallo lezen [inhoudsbeheer artikel](media-services-portal-vod-get-started.md).

### <a id="configuration"></a>Definitie van de configuratie voor Hyperlapse
Nadat de inhoud van uw Media Services-account is, moet u uw configuratie voorinstelling tooconstruct.  Hallo volgende tabel wordt uitgelegd Hallo gebruiker opgegeven velden:

| Veld | Beschrijving |
| --- | --- |
| StartFrame |Hallo-frame bij welke Hallo Microsoft Hyperlapse verwerking moet beginnen. |
| NumFrames |aantal frames tooprocess Hallo |
| Snelheid |Hallo factor met welke toospeed Hallo invoer video bestaat. |

Hallo Hieronder volgt een voorbeeld van een configuratiebestand overeenstemmende in XML en JSON:

**XML-definitie:**

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

**JSON-definitie:**

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <a id="sample_code"></a>Microsoft Hyperlapse Hello AMS .NET SDK
Hallo volgende methode uploadt een mediabestand als een actief en maakt een taak Hello Azure Media Hyperlapse Media-Processor.

> [!NOTE]
> U hebt al een CloudMediaContext binnen het bereik met Hallo-naam 'context' van deze toowork code.  meer informatie over deze, lees Hallo toolearn [inhoudsbeheer artikel](media-services-dotnet-get-started.md).
> 
> [!NOTE]
> tekenreeksargument Hallo 'hyperConfig' is een verwachte toobe een overeenstemmende configuratie vooraf in JSON of XML zoals hierboven is beschreven.
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
            progressJobTask.Wait();

            // If job state is Error, hello event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                Console.WriteLine(string.Format("Error: {0}. {1}",
                                                error.Code,
                                                error.Message));  
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <a id="file_types"></a>Ondersteunde bestandstypen
* MP4
* MOV
* WMV

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Verwante koppelingen
[Azure Media Services Analytics-overzicht](media-services-analytics-overview.md)

[Azure Media Analytics-demo 's](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

