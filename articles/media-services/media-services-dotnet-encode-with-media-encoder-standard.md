---
title: aaaEncode een asset met Media Encoder Standard met .NET | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toouse .NET tooencode Media Encoder Strandard wordt gebruikt.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>Een asset coderen met Media Encoder Standard met .NET
Codering taken zijn een van de meest voorkomende verwerkingen Hallo in Media Services. U maakt codering taken tooconvert media-bestanden vanuit een codering tooanother. Wanneer u codeert, kunt u Hallo Media Services ingebouwde Media Encoder. U kunt ook een encoder geleverd door een partner Media Services; coderingsprogramma's van derden zijn beschikbaar via hello Azure Marketplace. 

Dit onderwerp wordt beschreven hoe toouse .NET tooencode uw assets met Media Encoder Standard (MES). Media Encoder Standard is geconfigureerd met behulp van een Hallo encoder standaardinstellingen beschreven [hier](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

Het is raadzaam tooalways de bronbestanden in een adaptive bitrate MP4-set coderen en vervolgens weer converteren Hallo set toohello gewenste indeling met behulp van Hallo [dynamische pakketten](media-services-dynamic-packaging-overview.md). 

Als uw uitvoerasset opslag versleuteld is, moet u het leveringsbeleid voor Assets configureren. Zie voor meer informatie [leveringsbeleid voor Assets configureren](media-services-dotnet-configure-asset-delivery-policy.md).

> [!NOTE]
> MES produceert een bestand voor uitvoer met een naam die bevat Hallo eerste 32 tekens van de naam van het bestand voor invoer Hallo. Hallo-naam is gebaseerd op wat is opgegeven in de vooraf ingestelde bestand Hallo. Bijvoorbeeld 'bestandsnaam': '{Basename} _ {Index} {extensie}'. {Basename} wordt vervangen door Hallo eerste 32 tekens van Hallo bestand voor invoer op.
> 
> 

### <a name="mes-formats"></a>MES indelingen
[Indelingen en codecs](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>MES-standaardinstellingen
Media Encoder Standard is geconfigureerd met behulp van een Hallo encoder standaardinstellingen beschreven [hier](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Invoer en uitvoer van metagegevens
Als u een invoer asset (of activa) met behulp van MES codeert, krijgt u een uitvoerasset op Hallo coderen voltooid die taak. Hallo uitvoerasset bevat video, audio, miniaturen, het manifest, enz. op basis van Hallo codering voorinstelling die u gebruikt.

Hallo uitvoerasset bevat ook een bestand met metagegevens over Hallo invoer asset. Hallo naam van XML-bestand met metagegevens Hallo heeft Hallo volgende indeling: < asset_id > _metadata.xml (bijvoorbeeld 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), waarbij < asset_id > Hallo item-id hebt waarde van de invoer actief Hallo is. Hallo-schema van deze invoer XML met metagegevens is beschreven [hier](media-services-input-metadata-schema.md).

Hallo uitvoerasset bevat ook een bestand met metagegevens over Hallo uitvoerasset. Hallo naam van XML-bestand met metagegevens Hallo heeft Hallo volgende indeling: < source_file_name > _manifest.xml (bijvoorbeeld BigBuckBunny_manifest.xml). Hallo-schema van deze uitvoer metagegevens XML wordt beschreven [hier](media-services-output-metadata-schema.md).

Als u tooexamine ofwel Hallo twee bestanden met metagegevens wilt, kunt u een SAS-locator te maken en Hallo bestand tooyour lokale computer downloaden. U vindt een voorbeeld van hoe toocreate een SAS-locator en downloaden van een bestand met Hallo Media Services .NET SDK Extensions.

## <a name="download-sample"></a>Voorbeeld downloaden
U kunt ophalen en uitvoeren van een steekproef die laat zien hoe tooencode met MES van [hier](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="net-sample-code"></a>Voorbeeldcode voor .NET

Hallo volgende codevoorbeeld maakt gebruik van Media Services .NET SDK tooperform Hallo taken te volgen:

* Maak een codeertaak.
* Een verwijzing toohello Media Encoder Standard encoder ophalen.
* Geef toouse hello [adaptief streamen](media-services-autogen-bitrate-ladder-with-mes.md) vooraf ingestelde. 
* Een codering taak toohello van de taak niet toevoegen. 
* Geef Hallo invoer asset toobe gecodeerd.
* Maak een uitvoerasset met Hallo gecodeerde asset.
* Toevoegen van een gebeurtenis-handler toocheck Hallo taak uitgevoerd.
* Verzenden van Hallo-taak.

#### <a name="create-and-configure-a-visual-studio-project"></a>Maak en configureer een Visual Studio-project.

Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Voorbeeld 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

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

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Volgende stappen
[Hoe toogenerate miniatuur met Media Encoder Standard met .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[overzicht van Media Services-codering](media-services-encode-asset.md)

