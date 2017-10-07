---
title: Azure Media Encoder Standard tooauto aaaUse-genereren van een ladder bitrate | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toouse Media Encoder Standard (MES) tooauto-een bitrate ladder op basis van Hallo invoer resolutie en bitrate genereren. Hallo invoer resolutie en bitrate wordt nooit worden overschreden. Bijvoorbeeld, als Hallo-invoer is 720p op 3 Mbps, uitvoer wordt met de beste 720p blijven en wordt gestart volgens de tarieven voor lager is dan 3 Mbps.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a>Gebruik Azure Media Encoder Standard tooauto-een ladder bitrate genereren

## <a name="overview"></a>Overzicht

Dit onderwerp wordt beschreven hoe toouse Media Encoder Standard (MES) tooauto-een bitrate ladder (bitrate resolutie paren) op basis van Hallo invoer resolutie en bitrate genereren. Hallo wordt automatisch gegenereerde voorinstelling nooit overschrijden, Hallo invoer resolutie en bitsnelheid. Bijvoorbeeld, als Hallo-invoer is 720p op 3 Mbps, uitvoer wordt met de beste 720p blijven en wordt gestart volgens de tarieven voor lager is dan 3 Mbps.

### <a name="encoding-for-streaming-only"></a>Voor Streaming alleen codering

Als uw bedoeling tooencode is vooraf de bron-alleen voor streaming video u moeten 'Adaptief streamen' hello gebruiken bij het maken van een taak die voor codering. Wanneer u Hallo **adaptief streamen** definitie Hallo MES codering wordt op intelligente wijze cap een ladder bitrate. Echter, u zich niet kunnen toocontrol Hallo codering kosten, aangezien hoeveel lagen toouse Hallo-service bepaalt en met welke resolutie. Ziet u voorbeelden van lagen van uitvoer geproduceerd door MES als gevolg van codering met Hallo **adaptief streamen** vooraf ingesteld op Hallo einde van dit onderwerp. Hallo uitvoer Asset MP4-bestanden bevat waar audio en video niet interleaved.

### <a name="encoding-for-streaming-and-progressive-download"></a>Codering in voor streamen en progressief downloaden

Als uw bedoeling tooencode is vooraf de bronvideo voor streaming en tooproduce MP4-bestanden voor progressieve download u moeten 'Inhoud adaptieve meerdere Bitrate MP4' hello gebruiken bij het maken van een taak die voor codering. Wanneer u Hallo **inhoud adaptieve meerdere Bitrate MP4** definitie Hallo MES encoder toepassing hello dezelfde codering logica als hierboven, maar nu Hallo uitvoerasset bevat MP4-bestanden waar audio en video interleaved zijn. U kunt een van deze MP4-bestanden (bijvoorbeeld Hallo hoogste bitrate versie) gebruiken als een bestand progressief downloaden.

## <a id="encoding_with_dotnet"></a>Codering met mediaservices .NET SDK

Hallo volgende codevoorbeeld maakt gebruik van Media Services .NET SDK tooperform Hallo taken te volgen:

- Maak een codeertaak.
- Een verwijzing toohello Media Encoder Standard encoder ophalen.
- Een codeertaak taak toohello toevoegen en geef toouse hello **adaptief streamen** vooraf ingestelde. 
- Maak een uitvoerasset met Hallo gecodeerde asset.
- Toevoegen van een gebeurtenis-handler toocheck Hallo taak uitgevoerd.
- Verzenden van Hallo-taak.

#### <a name="create-and-configure-a-visual-studio-project"></a>Maak en configureer een Visual Studio-project.

Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Voorbeeld

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using hello "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }
        private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:

                // Cast sender as a job.
                IJob job = (IJob)sender;

                // Display or log error details as needed.
                break;
            default:
                break;
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
        }
    }

## <a id="output"></a>Uitvoer

Deze sectie ziet u drie voorbeelden van lagen van uitvoer geproduceerd door MES als gevolg van codering met Hallo **adaptief streamen** vooraf ingestelde. 

### <a name="example-1"></a>Voorbeeld 1
Bron met hoogte '1080' en '29.970' framesnelheid produceert 6 video lagen:

|Laag|Hoogte|Breedte|Bitrate(kbps)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1280|3520|
|3|540|960|2210|
|4|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>Voorbeeld 2
Bron met hoogte '720' en '23.970' framesnelheid produceert 5 video lagen:

|Laag|Hoogte|Breedte|Bitrate(kbps)|
|---|---|---|---|
|1|720|1280|2940|
|2|540|960|1850|
|3|360|640|960|
|4|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>Voorbeeld 3
Bron met hoogte '360' en '29.970' framesnelheid produceert 3 video lagen:

|Laag|Hoogte|Breedte|Bitrate(kbps)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|
## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zie ook
[Media Services-codering overzicht](media-services-encode-asset.md)

