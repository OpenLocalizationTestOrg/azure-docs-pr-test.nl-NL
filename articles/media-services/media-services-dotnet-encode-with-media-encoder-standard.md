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
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="4b852-103">Een asset coderen met Media Encoder Standard met .NET</span><span class="sxs-lookup"><span data-stu-id="4b852-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="4b852-104">Codering taken zijn een van de meest voorkomende verwerkingen Hallo in Media Services.</span><span class="sxs-lookup"><span data-stu-id="4b852-104">Encoding jobs are one of hello most common processing operations in Media Services.</span></span> <span data-ttu-id="4b852-105">U maakt codering taken tooconvert media-bestanden vanuit een codering tooanother.</span><span class="sxs-lookup"><span data-stu-id="4b852-105">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="4b852-106">Wanneer u codeert, kunt u Hallo Media Services ingebouwde Media Encoder.</span><span class="sxs-lookup"><span data-stu-id="4b852-106">When you encode, you can use hello Media Services built-in Media Encoder.</span></span> <span data-ttu-id="4b852-107">U kunt ook een encoder geleverd door een partner Media Services; coderingsprogramma's van derden zijn beschikbaar via hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4b852-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through hello Azure Marketplace.</span></span> 

<span data-ttu-id="4b852-108">Dit onderwerp wordt beschreven hoe toouse .NET tooencode uw assets met Media Encoder Standard (MES).</span><span class="sxs-lookup"><span data-stu-id="4b852-108">This topic shows how toouse .NET tooencode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="4b852-109">Media Encoder Standard is geconfigureerd met behulp van een Hallo encoder standaardinstellingen beschreven [hier](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="4b852-109">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="4b852-110">Het is raadzaam tooalways de bronbestanden in een adaptive bitrate MP4-set coderen en vervolgens weer converteren Hallo set toohello gewenste indeling met behulp van Hallo [dynamische pakketten](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4b852-110">It is recommended tooalways encode your source files into an adaptive bitrate MP4 set and then convert hello set toohello desired format using hello [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="4b852-111">Als uw uitvoerasset opslag versleuteld is, moet u het leveringsbeleid voor Assets configureren.</span><span class="sxs-lookup"><span data-stu-id="4b852-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="4b852-112">Zie voor meer informatie [leveringsbeleid voor Assets configureren](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4b852-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4b852-113">MES produceert een bestand voor uitvoer met een naam die bevat Hallo eerste 32 tekens van de naam van het bestand voor invoer Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b852-113">MES produces an output file with a name that contains hello first 32 characters of hello input file name.</span></span> <span data-ttu-id="4b852-114">Hallo-naam is gebaseerd op wat is opgegeven in de vooraf ingestelde bestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b852-114">hello name is based on what is specified in hello preset file.</span></span> <span data-ttu-id="4b852-115">Bijvoorbeeld 'bestandsnaam': '{Basename} _ {Index} {extensie}'.</span><span class="sxs-lookup"><span data-stu-id="4b852-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="4b852-116">{Basename} wordt vervangen door Hallo eerste 32 tekens van Hallo bestand voor invoer op.</span><span class="sxs-lookup"><span data-stu-id="4b852-116">{Basename} is replaced by hello first 32 characters of hello input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="4b852-117">MES indelingen</span><span class="sxs-lookup"><span data-stu-id="4b852-117">MES Formats</span></span>
[<span data-ttu-id="4b852-118">Indelingen en codecs</span><span class="sxs-lookup"><span data-stu-id="4b852-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="4b852-119">MES-standaardinstellingen</span><span class="sxs-lookup"><span data-stu-id="4b852-119">MES Presets</span></span>
<span data-ttu-id="4b852-120">Media Encoder Standard is geconfigureerd met behulp van een Hallo encoder standaardinstellingen beschreven [hier](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="4b852-120">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="4b852-121">Invoer en uitvoer van metagegevens</span><span class="sxs-lookup"><span data-stu-id="4b852-121">Input and output metadata</span></span>
<span data-ttu-id="4b852-122">Als u een invoer asset (of activa) met behulp van MES codeert, krijgt u een uitvoerasset op Hallo coderen voltooid die taak.</span><span class="sxs-lookup"><span data-stu-id="4b852-122">When you encode an input asset (or assets) using MES, you get an output asset at hello successful completion of that encode task.</span></span> <span data-ttu-id="4b852-123">Hallo uitvoerasset bevat video, audio, miniaturen, het manifest, enz. op basis van Hallo codering voorinstelling die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4b852-123">hello output asset contains video, audio, thumbnails, manifest, etc. based on hello encoding preset you use.</span></span>

<span data-ttu-id="4b852-124">Hallo uitvoerasset bevat ook een bestand met metagegevens over Hallo invoer asset.</span><span class="sxs-lookup"><span data-stu-id="4b852-124">hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="4b852-125">Hallo naam van XML-bestand met metagegevens Hallo heeft Hallo volgende indeling: < asset_id > _metadata.xml (bijvoorbeeld 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), waarbij < asset_id > Hallo item-id hebt waarde van de invoer actief Hallo is.</span><span class="sxs-lookup"><span data-stu-id="4b852-125">hello name of hello metadata XML file has hello following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is hello AssetId value of hello input asset.</span></span> <span data-ttu-id="4b852-126">Hallo-schema van deze invoer XML met metagegevens is beschreven [hier](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4b852-126">hello schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="4b852-127">Hallo uitvoerasset bevat ook een bestand met metagegevens over Hallo uitvoerasset.</span><span class="sxs-lookup"><span data-stu-id="4b852-127">hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="4b852-128">Hallo naam van XML-bestand met metagegevens Hallo heeft Hallo volgende indeling: < source_file_name > _manifest.xml (bijvoorbeeld BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="4b852-128">hello name of hello metadata XML file has hello following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="4b852-129">Hallo-schema van deze uitvoer metagegevens XML wordt beschreven [hier](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4b852-129">hello schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="4b852-130">Als u tooexamine ofwel Hallo twee bestanden met metagegevens wilt, kunt u een SAS-locator te maken en Hallo bestand tooyour lokale computer downloaden.</span><span class="sxs-lookup"><span data-stu-id="4b852-130">If you want tooexamine either of hello two metadata files, you can create a SAS locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="4b852-131">U vindt een voorbeeld van hoe toocreate een SAS-locator en downloaden van een bestand met Hallo Media Services .NET SDK Extensions.</span><span class="sxs-lookup"><span data-stu-id="4b852-131">You can find an example on how toocreate a SAS locator and download a file Using hello Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="4b852-132">Voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="4b852-132">Download sample</span></span>
<span data-ttu-id="4b852-133">U kunt ophalen en uitvoeren van een steekproef die laat zien hoe tooencode met MES van [hier](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="4b852-133">You can get and run a sample that shows how tooencode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="4b852-134">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="4b852-134">.NET sample code</span></span>

<span data-ttu-id="4b852-135">Hallo volgende codevoorbeeld maakt gebruik van Media Services .NET SDK tooperform Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b852-135">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="4b852-136">Maak een codeertaak.</span><span class="sxs-lookup"><span data-stu-id="4b852-136">Create an encoding job.</span></span>
* <span data-ttu-id="4b852-137">Een verwijzing toohello Media Encoder Standard encoder ophalen.</span><span class="sxs-lookup"><span data-stu-id="4b852-137">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="4b852-138">Geef toouse hello [adaptief streamen](media-services-autogen-bitrate-ladder-with-mes.md) vooraf ingestelde.</span><span class="sxs-lookup"><span data-stu-id="4b852-138">Specify toouse hello [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="4b852-139">Een codering taak toohello van de taak niet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4b852-139">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="4b852-140">Geef Hallo invoer asset toobe gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="4b852-140">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="4b852-141">Maak een uitvoerasset met Hallo gecodeerde asset.</span><span class="sxs-lookup"><span data-stu-id="4b852-141">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="4b852-142">Toevoegen van een gebeurtenis-handler toocheck Hallo taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4b852-142">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="4b852-143">Verzenden van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="4b852-143">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4b852-144">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="4b852-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="4b852-145">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4b852-145">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="4b852-146">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="4b852-146">Example</span></span> 

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="4b852-147">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="4b852-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4b852-148">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="4b852-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4b852-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b852-149">Next steps</span></span>
<span data-ttu-id="4b852-150">[Hoe toogenerate miniatuur met Media Encoder Standard met .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[overzicht van Media Services-codering](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="4b852-150">[How toogenerate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

