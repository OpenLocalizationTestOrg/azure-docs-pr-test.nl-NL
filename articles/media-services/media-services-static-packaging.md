---
title: aaaUsing Azure Media Packager tooaccomplish statische verpakking taken | Microsoft Docs
description: Dit onderwerp bevat diverse taken die worden uitgevoerd met Azure Media Packager.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0582628e-a525-4a78-90ac-9f7fc1cd909f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 64e8ba217bcd3074f5819ac3b74d2969432db5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-media-packager-tooaccomplish-static-packaging-tasks"></a><span data-ttu-id="11628-103">Het gebruik van Azure Media Packager tooaccomplish statische verpakking taken</span><span class="sxs-lookup"><span data-stu-id="11628-103">Using Azure Media Packager tooaccomplish static packaging tasks</span></span>
> [!NOTE]
> <span data-ttu-id="11628-104">Hallo-einde van de datum valt voor Microsoft Azure Media Packager en Microsoft Azure Media Encryptor uitgebreid tooMarch 1, 2017.</span><span class="sxs-lookup"><span data-stu-id="11628-104">hello end of life date for Microsoft Azure Media Packager and Microsoft Azure Media Encryptor has been extended tooMarch 1, 2017.</span></span> <span data-ttu-id="11628-105">Voordat u deze datum worden Hallo-functionaliteiten van deze processors toegevoegd tooMedia codering-standaard (MES).</span><span class="sxs-lookup"><span data-stu-id="11628-105">Before that date, hello functionalities of these processors will be added tooMedia Encoder Standard (MES).</span></span> <span data-ttu-id="11628-106">Klanten wordt aangeboden met instructies voor het toomigrate hun tooMES werkstromen toosend taken.</span><span class="sxs-lookup"><span data-stu-id="11628-106">Customers will be provided with instructions on how toomigrate their workflows toosend Jobs tooMES.</span></span> <span data-ttu-id="11628-107">Indeling conversie en versleuteling mogelijkheden zijn mogelijk ook beschikbaar via dynamische pakketten en dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="11628-107">Format conversion and encryption capabilities may also be available through dynamic packaging and dynamic encryption.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="11628-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="11628-108">Overview</span></span>
<span data-ttu-id="11628-109">In de volgorde toodeliver digitale video via Hallo internet, moet u comprimeren Hallo media.</span><span class="sxs-lookup"><span data-stu-id="11628-109">In order toodeliver digital video over hello internet you must compress hello media.</span></span> <span data-ttu-id="11628-110">Digitale video's zijn behoorlijk groot en mogelijk te groot toodeliver via Hallo internet of voor uw klanten apparaten toodisplay goed.</span><span class="sxs-lookup"><span data-stu-id="11628-110">Digital video files are quite large and may be too big toodeliver over hello internet or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="11628-111">Codering is Hallo-proces van het comprimeren van video en audio zodat uw klanten het medium kunnen bekijken.</span><span class="sxs-lookup"><span data-stu-id="11628-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span> <span data-ttu-id="11628-112">Zodra een video is gecodeerd worden geplaatst in een ander bestand containers.</span><span class="sxs-lookup"><span data-stu-id="11628-112">Once a video has been encoded it can be placed into different file containers.</span></span> <span data-ttu-id="11628-113">Hallo-proces brengen gecodeerde media naar een container wordt verpakking genoemd.</span><span class="sxs-lookup"><span data-stu-id="11628-113">hello process of placing encoded media into a container is called packaging.</span></span> <span data-ttu-id="11628-114">U kunt bijvoorbeeld een MP4-bestand en deze vervolgens converteren naar Smooth Streaming of HLS inhoud met behulp van Azure Media Packager Hallo.</span><span class="sxs-lookup"><span data-stu-id="11628-114">For example, you can take an MP4 file and convert it into Smooth Streaming or HLS content by using hello Azure Media Packager.</span></span> 

<span data-ttu-id="11628-115">Media Services biedt ondersteuning voor dynamische en statische pakketten.</span><span class="sxs-lookup"><span data-stu-id="11628-115">Media Services supports dynamic and static packaging.</span></span> <span data-ttu-id="11628-116">Als u statische verpakking moet u een kopie van uw inhoud in elke gewenste indeling van uw klanten toocreate.</span><span class="sxs-lookup"><span data-stu-id="11628-116">When using static packaging you need toocreate a copy of your content in each format required by your customers.</span></span> <span data-ttu-id="11628-117">Met dynamische verpakking alles wat die u nodig is toocreate een actief dat een set adaptive bitrate MP4- of Smooth Streaming-bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="11628-117">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 or Smooth Streaming files.</span></span> <span data-ttu-id="11628-118">Vervolgens, op basis van de opgegeven indeling in het manifest Hallo Hallo of fragment aanvraag, Hallo On-Demand Streaming server zorgt ervoor dat uw gebruikers Hallo stream ontvangt in Hallo protocol die ze hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="11628-118">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that your users receive hello stream in hello protocol they have chosen.</span></span> <span data-ttu-id="11628-119">Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services-service bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client.</span><span class="sxs-lookup"><span data-stu-id="11628-119">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

> [!NOTE]
> <span data-ttu-id="11628-120">Het verdient aanbeveling toouse [dynamische pakketten](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11628-120">It is recommended toouse [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>
> 
> 

<span data-ttu-id="11628-121">Er zijn echter enkele scenario's waarvoor statische pakketten:</span><span class="sxs-lookup"><span data-stu-id="11628-121">However, there are some scenarios that require static packaging:</span></span> 

* <span data-ttu-id="11628-122">Valideren van adaptive bitrate MP4s gecodeerd met externe coderingsprogramma's (bijvoorbeeld met behulp van derden coderingsprogramma's).</span><span class="sxs-lookup"><span data-stu-id="11628-122">Validating adaptive bitrate MP4s encoded with external encoders (for example, using third party encoders).</span></span>

<span data-ttu-id="11628-123">U kunt ook statische verpakking tooperform Hallo taken te volgen.</span><span class="sxs-lookup"><span data-stu-id="11628-123">You can also use static packaging tooperform hello following tasks.</span></span> <span data-ttu-id="11628-124">Het wordt echter aanbevolen toouse dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="11628-124">However it is recommended toouse dynamic encryption.</span></span>

* <span data-ttu-id="11628-125">Gebruik van statische versleuteling tooprotect uw Smooth en MPEG DASH met PlayReady</span><span class="sxs-lookup"><span data-stu-id="11628-125">Using static encryption tooprotect your Smooth and MPEG DASH with PlayReady</span></span>
* <span data-ttu-id="11628-126">Gebruik van statische versleuteling tooprotect HLSv3 met AES-128</span><span class="sxs-lookup"><span data-stu-id="11628-126">Using static encryption tooprotect HLSv3 with AES-128</span></span>
* <span data-ttu-id="11628-127">Gebruik van statische versleuteling tooprotect HLSv3 met PlayReady</span><span class="sxs-lookup"><span data-stu-id="11628-127">Using static encryption tooprotect HLSv3 with PlayReady</span></span>

## <a name="validating-adaptive-bitrate-mp4s-encoded-with-external-encoders"></a><span data-ttu-id="11628-128">Valideren Adaptive Bitrate MP4s gecodeerd met externe coderingsprogramma 's</span><span class="sxs-lookup"><span data-stu-id="11628-128">Validating Adaptive Bitrate MP4s Encoded with External Encoders</span></span>
<span data-ttu-id="11628-129">Als u toouse een set adaptive bitrate (multi-bitrate) MP4-bestanden die niet zijn gecodeerd met Media Services coderingsprogramma's wilt, moet u uw bestanden valideren voordat het verdere verwerking.</span><span class="sxs-lookup"><span data-stu-id="11628-129">If you want toouse a set of adaptive bitrate (multi-bitrate) MP4 files that were not encoded with Media Services' encoders, you should validate your files before further processing.</span></span> <span data-ttu-id="11628-130">Hallo Media Services Packager kan een asset die bestaat uit een set MP4-bestanden valideren en controleer of Hallo asset verpakte tooSmooth Streaming of HLS kan worden.</span><span class="sxs-lookup"><span data-stu-id="11628-130">hello Media Services Packager can validate an asset that contains a set of MP4 files and check whether hello asset can be packaged tooSmooth Streaming or HLS.</span></span> <span data-ttu-id="11628-131">Als Hallo validatietaak mislukt, wordt Hallo-taak die is verwerken Hallo taak voltooid met een fout.</span><span class="sxs-lookup"><span data-stu-id="11628-131">If hello validation task fails, hello job that was processing hello task will complete with an error.</span></span> <span data-ttu-id="11628-132">Hallo XML waarmee de definitie voor validatietaak op Hallo u in Hallo vindt Hallo [taak vooraf ingestelde voor Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="11628-132">hello XML that defines hello preset for hello validation task can be found in hello [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

> [!NOTE]
> <span data-ttu-id="11628-133">Gebruik Hallo Media Encoder Standard tooproduce of Hallo Media Services Packager toovalidate uw inhoud in de volgorde tooavoid runtime-problemen.</span><span class="sxs-lookup"><span data-stu-id="11628-133">Use hello Media Encoder Standard tooproduce or hello Media Services Packager toovalidate your content in order tooavoid runtime issues.</span></span> <span data-ttu-id="11628-134">Als Hallo On-Demand Streaming server is niet kunnen tooparse uw bronbestanden tijdens runtime, ontvangt u HTTP 1.1-fout '415 niet-ondersteund mediatype'.</span><span class="sxs-lookup"><span data-stu-id="11628-134">If hello On-Demand Streaming server is not able tooparse your source files at runtime, you will receive HTTP 1.1 error “415 Unsupported Media Type”.</span></span> <span data-ttu-id="11628-135">Hallo server toofail tooparse herhaaldelijk waardoor de bronbestanden is van invloed op prestaties van On-Demand Streaming Hallo-server en Hallo bandbreedte beschikbaar tooserving andere aanvragen kan verminderen.</span><span class="sxs-lookup"><span data-stu-id="11628-135">Repeatedly causing hello server toofail tooparse your source files affects performance of hello On-Demand Streaming server and may reduce hello bandwidth available tooserving other requests.</span></span> <span data-ttu-id="11628-136">Azure Media Services biedt een Service Level Agreement (SLA) van de services On-Demand Streaming; Deze SERVICEOVEREENKOMST, echter niet worden uitgevoerd als het Hallo-server is misbruikt op Hallo wijze die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="11628-136">Azure Media Services offers a Service Level Agreement (SLA) on its On-Demand Streaming services; however, this SLA cannot be honored if hello server is misused in hello fashion described above.</span></span>
> 
> 

<span data-ttu-id="11628-137">Deze sectie wordt beschreven hoe tooprocess validatietaak Hallo.</span><span class="sxs-lookup"><span data-stu-id="11628-137">This section shows how tooprocess hello validation task.</span></span> <span data-ttu-id="11628-138">U ziet ook hoe toosee status en Hallo foutbericht van Hallo-taak is voltooid met JobStatus.Error Hallo.</span><span class="sxs-lookup"><span data-stu-id="11628-138">It also shows how toosee hello status and hello error message of hello job that completes with JobStatus.Error.</span></span>

<span data-ttu-id="11628-139">toovalidate uw MP4-met Media Services Packager bestanden, moet u uw eigen manifest (ISM)-bestand maken en deze samen met de bronbestanden hello te uploaden naar Hallo Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="11628-139">toovalidate your MP4 files with Media Services Packager, you must create your own manifest (.ism) file and upload it together with hello source files into hello Media Services account.</span></span> <span data-ttu-id="11628-140">Hieronder volgt een voorbeeld van Hallo ISM-bestand die wordt geproduceerd door Hallo Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="11628-140">Below is a sample of hello .ism file produced by hello Media Encoder Standard.</span></span> <span data-ttu-id="11628-141">Hallo-bestandsnamen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="11628-141">hello file names are case sensitive.</span></span> <span data-ttu-id="11628-142">Controleer ook of de tekst hello in Hallo ISM-bestand is gecodeerd met UTF-8.</span><span class="sxs-lookup"><span data-stu-id="11628-142">Also, make sure hello text in hello .ism file is encoded with UTF-8.</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
    <!-- Tells hello server that these input files are MP4s – specific tooDynamic Packaging -->
        <meta name="formats" content="mp4" /> 
      </head>
      <body>
        <switch>
          <video src="BigBuckBunny_1000.mp4" />
          <video src="BigBuckBunny_1500.mp4" />
          <video src="BigBuckBunny_2250.mp4" />
          <video src="BigBuckBunny_3400.mp4" />
          <video src="BigBuckBunny_400.mp4" />
          <video src="BigBuckBunny_650.mp4" />
          <audio src="BigBuckBunny_400.mp4" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="11628-143">Zodra u hebt kan Hallo adaptive bitrate die MP4-set profiteren van dynamische pakketten.</span><span class="sxs-lookup"><span data-stu-id="11628-143">Once you have hello adaptive bitrate MP4 set you can take advantage of Dynamic Packaging.</span></span> <span data-ttu-id="11628-144">Dynamische pakketten kunt u toodeliver stromen in Hallo opgegeven protocol zonder verdere verpakken.</span><span class="sxs-lookup"><span data-stu-id="11628-144">Dynamic Packaging allows you toodeliver streams in hello specified protocol without further packaging.</span></span> <span data-ttu-id="11628-145">Zie voor meer informatie [dynamische pakketten](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11628-145">For more information, see [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="11628-146">Hallo code voorbeeld gebruikt Azure Media Services .NET SDK Extensions te volgen.</span><span class="sxs-lookup"><span data-stu-id="11628-146">hello following code sample uses Azure Media Services .NET SDK Extensions.</span></span>  <span data-ttu-id="11628-147">Zorg ervoor tooupdate Hallo code toopoint toohello map waarin uw invoer MP4-bestanden en ISM-bestand zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="11628-147">Make sure tooupdate hello code toopoint toohello folder where your input MP4 files and .ism file are located.</span></span> <span data-ttu-id="11628-148">En ook toowhere uw MediaPackager_ValidateTask.xml bestand zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="11628-148">And also toowhere your MediaPackager_ValidateTask.xml file is located.</span></span> <span data-ttu-id="11628-149">Dit XML-bestand is gedefinieerd in [taak vooraf voor Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="11628-149">This XML file is defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Xml.Linq;

    namespace MediaServicesStaticPackaging
    {
        class Program
        {
            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            // hello MultibitrateMP4Files folder should also
            // contain hello .ism manifest file.
            private static readonly string _multibitrateMP4s =
                Path.Combine(_mediaFiles, @"MultibitrateMP4Files");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations";

            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServicesAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServicesAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Ingest a set of multibitrate MP4s.
                //
                // Use hello SDK extension method toocreate a new asset by 
                // uploading files from a local directory.
                IAsset multibitrateMP4sAsset = _context.Assets.CreateFromFolder(
                    _multibitrateMP4s,
                    AssetCreationOptions.None,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                // Use Azure Media Packager toovalidate hello files.
                IAsset validatedMP4s =
                    ValidateMultibitrateMP4s(multibitrateMP4sAsset);

                // Publish hello asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    validatedMP4s,
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                                     // Get hello streaming URLs.
                Console.WriteLine("Smooth Streaming URL:");
                Console.WriteLine(validatedMP4s.GetSmoothStreamingUri().ToString());
                Console.WriteLine("MPEG DASH URL:");
                Console.WriteLine(validatedMP4s.GetMpegDashUri().ToString());
                Console.WriteLine("HLS URL:");
                Console.WriteLine(validatedMP4s.GetHlsUri().ToString());
            }

            public static IAsset ValidateMultibitrateMP4s(IAsset multibitrateMP4sAsset)
            {
                // Set .ism as a primary file 
                // in a multibitrate MP4 set.
                SetISMFileAsPrimary(multibitrateMP4sAsset);

                // Create a new job.
                IJob job = _context.Jobs.Create("MP4 validation and converstion tooSmooth Stream job.");

                // Read hello task configuration data into a string. 
                string configMp4Validation = File.ReadAllText(Path.Combine(
                        _configurationXMLFiles,
                        "MediaPackager_ValidateTask.xml"));

                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Create a task with hello conversion details, using hello configuration data. 
                ITask task = job.Tasks.AddNew("Mp4 Validation Task",
                    processor,
                    configMp4Validation,
                    TaskOptions.None);

                // Specify hello input asset toobe validated.
                task.InputAssets.Add(multibitrateMP4sAsset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted). 
                task.OutputAssets.AddNew("Validated output asset",
                        AssetCreationOptions.None);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // If hello validation task fails and job completes with JobState.Error,
                // display hello error message and throw an exception.
                if (job.State == JobState.Error)
                {
                    Console.WriteLine("  Job ID: " + job.Id);
                    Console.WriteLine("  Name: " + job.Name);
                    Console.WriteLine("  State: " + job.State);

                    foreach (var jobTask in job.Tasks)
                    {
                        Console.WriteLine("  Task Id: " + jobTask.Id);
                        Console.WriteLine("  Name: " + jobTask.Name);
                        Console.WriteLine("  Progress: " + jobTask.Progress);
                        Console.WriteLine("  Configuration: " + jobTask.Configuration);
                        Console.WriteLine("  Running time: " + jobTask.RunningDuration);
                        if (jobTask.ErrorDetails != null)
                        {
                            foreach (var errordetail in jobTask.ErrorDetails)
                            {

                                Console.WriteLine("  Error Message:" + errordetail.Message);
                                Console.WriteLine("  Error Code:" + errordetail.Code);
                            }
                        }
                    }
                    throw new Exception("hello specified multi-bitrate MP4 set is not valid.");
                }


                return job.OutputMediaAssets[0];
            }

            static void SetISMFileAsPrimary(IAsset asset)
            {
                var ismAssetFiles = asset.AssetFiles.ToList().
                    Where(f => f.Name.EndsWith(".ism", StringComparison.OrdinalIgnoreCase)).ToArray();

                // hello following code assigns hello first .ism file as hello primary file in hello asset.
                // An asset should have one .ism file.  
                ismAssetFiles.First().IsPrimary = true;
                ismAssetFiles.First().Update();
            }
        }
    }

## <a name="using-static-encryption-tooprotect-your-smooth-and-mpeg-dash-with-playready"></a><span data-ttu-id="11628-150">Gebruik van statische versleuteling tooProtect uw Smooth en MPEG DASH met PlayReady</span><span class="sxs-lookup"><span data-stu-id="11628-150">Using Static Encryption tooProtect your Smooth and MPEG DASH with PlayReady</span></span>
<span data-ttu-id="11628-151">Als u uw inhoud met PlayReady tooprotect wilt, hebt u een keuze uit met behulp van [dynamische versleuteling](media-services-protect-with-drm.md) (hello aanbevolen optie) of statische versleuteling (zoals beschreven in deze sectie).</span><span class="sxs-lookup"><span data-stu-id="11628-151">If you want tooprotect your content with PlayReady, you have a choice of using [dynamic encryption](media-services-protect-with-drm.md) (hello recommended option) or static encryption (as described in this section).</span></span>

<span data-ttu-id="11628-152">Hallo-voorbeeld in deze sectie codeert een tussentijds bestand (in dit geval MP4) in adaptive bitrate MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="11628-152">hello example in this section encodes a mezzanine file (in this case MP4) into adaptive bitrate MP4 files.</span></span> <span data-ttu-id="11628-153">Deze vervolgens MP4s worden verpakt in Smooth Streaming en vervolgens versleutelt Smooth Streaming met PlayReady.</span><span class="sxs-lookup"><span data-stu-id="11628-153">It then packages MP4s into Smooth Streaming and then encrypts Smooth Streaming with PlayReady.</span></span> <span data-ttu-id="11628-154">U bent als gevolg hiervan kunnen toostream Smooth Streaming of MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="11628-154">As a result you are able toostream Smooth Streaming or MPEG DASH.</span></span>

<span data-ttu-id="11628-155">Media Services biedt nu een service voor het leveren van Microsoft PlayReady-licenties.</span><span class="sxs-lookup"><span data-stu-id="11628-155">Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="11628-156">Hallo voorbeeld in dit artikel laat zien hoe tooconfigure Hallo Media Services PlayReady service voor het leveren van licentie (Zie Hallo ConfigureLicenseDeliveryService methode gedefinieerd in het Hallo-code hieronder).</span><span class="sxs-lookup"><span data-stu-id="11628-156">hello example in this article shows how tooconfigure hello Media Services PlayReady license delivery service (see hello ConfigureLicenseDeliveryService method defined in hello code below).</span></span> <span data-ttu-id="11628-157">Zie voor meer informatie over Media Services PlayReady-service voor het leveren van licenties [met behulp van dynamische PlayReady-versleuteling en de Service voor het leveren van licenties](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="11628-157">For more information about Media Services PlayReady license delivery service, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11628-158">toodeliver MPEG DASH versleuteld met PlayReady Zorg ervoor dat toouse CENC opties door Hallo useSencBox en adjustSubSamples (beschreven in Hallo [taak vooraf voor Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) onderwerp) tootrue.</span><span class="sxs-lookup"><span data-stu-id="11628-158">toodeliver MPEG DASH encrypted with PlayReady, make sure toouse CENC options by setting hello useSencBox and adjustSubSamples properties (described in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic) tootrue.</span></span>  
> 
> 

<span data-ttu-id="11628-159">Zorg ervoor dat tooupdate Hallo code toopoint toohello map bevindt de invoer MP4-bestand te volgen.</span><span class="sxs-lookup"><span data-stu-id="11628-159">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span>

<span data-ttu-id="11628-160">En ook toowhere MediaPackager_MP4ToSmooth.xml en MediaEncryptor_PlayReadyProtection.xml bestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="11628-160">And also toowhere your MediaPackager_MP4ToSmooth.xml and MediaEncryptor_PlayReadyProtection.xml files are located.</span></span> <span data-ttu-id="11628-161">MediaPackager_MP4ToSmooth.xml is gedefinieerd in [taak vooraf voor Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) en MediaEncryptor_PlayReadyProtection.xml wordt gedefinieerd in Hallo [taak vooraf voor Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="11628-161">MediaPackager_MP4ToSmooth.xml is defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) and MediaEncryptor_PlayReadyProtection.xml is defined in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic.</span></span> 

<span data-ttu-id="11628-162">Hallo voorbeeld definieert Hallo UpdatePlayReadyConfigurationXMLFile methode waarmee u Hallo toodynamically-MediaEncryptor_PlayReadyProtection.xml updatebestand kunt.</span><span class="sxs-lookup"><span data-stu-id="11628-162">hello example defines hello UpdatePlayReadyConfigurationXMLFile method that you can use toodynamically update hello MediaEncryptor_PlayReadyProtection.xml file.</span></span> <span data-ttu-id="11628-163">Als u belangrijke seed Hallo beschikbaar hebt, kunt u Hallo CommonEncryption.GeneratePlayReadyContentKey methode toogenerate hello inhoudssleutel op basis van Hallo keySeedValue en KeyId waarden.</span><span class="sxs-lookup"><span data-stu-id="11628-163">If you have hello key seed available, you can use hello CommonEncryption.GeneratePlayReadyContentKey method toogenerate hello content key based on hello keySeedValue and KeyId values.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace PlayReadyStaticEncryptAndKeyDeliverySvc
    {
        class Program
        {

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";


            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Encoding and encrypting assets //////////////////////
                // Load a single MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset =
                    ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create a common encryption content key that is used 
                // a) tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
                //    that is used for encryption.
                // b) tooconfigure hello license delivery service and 
                //
                Guid keyId;
                byte[] contentKey;

                IContentKey key = CreateCommonEncryptionKey(out keyId, out contentKey);

                // hello content key authorization policy must be configured by you 
                // and met by hello client in order for hello PlayReady license
                // toobe delivered toohello client. 
                // In this example hello Media Services PlayReady license delivery service is used.
                ConfigureLicenseDeliveryService(key);

                // Get hello Media Services PlayReady license delivery URL.
                // This URL will be assigned toohello licenseAcquisitionUrl property 
                // of hello MediaEncryptor_PlayReadyProtection.xml file.
                Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

                // Update hello MediaEncryptor_PlayReadyProtection.xml file with hello key and URL info.
                UpdatePlayReadyConfigurationXMLFile(keyId, contentKey, acquisitionUrl);


                // Encrypt your clear Smooth Streaming tooSmooth Streaming with PlayReady.
                IAsset outputAsset = CreateSmoothStreamEncryptedWithPlayReady(clearSmoothStreamAsset);


                // You can use hello http://smf.cloudapp.net/healthmonitor player 
                // tootest hello smoothStreamURL URL.
                string smoothStreamURL = outputAsset.GetSmoothStreamingUri().ToString();
                Console.WriteLine("Smooth Streaming URL:");
                Console.WriteLine(smoothStreamURL);

                // You can use hello http://dashif.org/reference/players/javascript/ player 
                // tootest hello dashURL URL.
                string dashURL = outputAsset.GetMpegDashUri().ToString();
                Console.WriteLine("MPEG DASH URL:");
                Console.WriteLine(dashURL);
            }

            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Stream.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains hello Smooth Streaming asset.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Encrypts Smooth Stream with PlayReady.
            /// Then creates a Smooth Streaming Url.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateSmoothStreamEncryptedWithPlayReady(IAsset clearSmoothStreamAsset)
            {
                // Create a job.
                IJob job = _context.Jobs.Create("Encrypt tooPlayReady Smooth Streaming.");

                // Add task 1 - Encrypt Smooth Streaming with PlayReady 
                IAsset encryptedSmoothAsset =
                    EncryptSmoothStreamWithPlayReadyTask(job, clearSmoothStreamAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // hello OutputMediaAssets[0] contains hello desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[0],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[0];
            }

            /// <summary>
            /// Create a common encryption content key that is used 
            /// tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
            /// that is used for encryption.
            /// </summary>
            /// <param name="keyId"></param>
            /// <param name="contentKey"></param>
            /// <returns></returns>
            public static IContentKey CreateCommonEncryptionKey(out Guid keyId, out byte[] contentKey)
            {
                keyId = Guid.NewGuid();
                contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            /// <summary>
            /// Update your configuration .xml file dynamically.
            /// </summary>
            public static void UpdatePlayReadyConfigurationXMLFile(Guid keyId, byte[] keyValue, Uri licenseAcquisitionUrl)
            {
                string xmlFileName = Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml");

                XNamespace xmlns = "http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#";

                // Prepare hello encryption task template
                XDocument doc = XDocument.Load(xmlFileName);

                var licenseAcquisitionUrlEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "licenseAcquisitionUrl")
                        .FirstOrDefault();
                var contentKeyEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "contentKey")
                        .FirstOrDefault();
                var keyIdEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "keyId")
                        .FirstOrDefault();

                // Update hello "value" property.
                if (licenseAcquisitionUrlEl != null)
                    licenseAcquisitionUrlEl.Attribute("value").SetValue(licenseAcquisitionUrl.ToString());

                if (contentKeyEl != null)
                    contentKeyEl.Attribute("value").SetValue(Convert.ToBase64String(keyValue));

                if (keyIdEl != null)
                    keyIdEl.Attribute("value").SetValue(keyId);

                doc.Save(xmlFileName);
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                return asset;
            }

            /// <summary>
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s",
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles,
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset =
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Stream",
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }


            /// <summary>
            /// Creates a task tooencrypt Smooth Streaming with PlayReady.
            /// Note: toodeliver DASH, make sure tooset hello useSencBox and adjustSubSamples 
            /// configuration properties tootrue. 
            /// In this example, MediaEncryptor_PlayReadyProtection.xml contains configuration.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncryptSmoothStreamWithPlayReadyTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Encryptor.
                IMediaProcessor playreadyProcessor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaEncryptor);

                // Read hello configuration XML.
                //
                // Note that hello configuration defined in MediaEncryptor_PlayReadyProtection.xml
                // is using keySeedValue. It is recommended that you do this only for testing 
                // and not in production. For more information, see 
                // http://msdn.microsoft.com/library/windowsazure/dn189154.aspx.
                //
                string configPlayReady = File.ReadAllText(Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml"));

                ITask playreadyTask = job.Tasks.AddNew("My PlayReady Task",
                   playreadyProcessor,
                   configPlayReady,
                   TaskOptions.ProtectedConfiguration);

                playreadyTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.CommonEncryptionProtected.
                IAsset playreadyAsset = playreadyTask.OutputAssets.AddNew(
                                                "PlayReady Smooth Streaming",
                                                AssetCreationOptions.CommonEncryptionProtected);

                return playreadyAsset;
            }

            /// <summary>
            /// Configures authorization policy for hello content key. 
            /// </summary>
            /// <param name="contentKey">hello content key.</param>
            static public void ConfigureLicenseDeliveryService(IContentKey contentKey)
            {
                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                    new ContentKeyAuthorizationPolicyRestriction 
                    { 
                        Name = "Open", 
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                        Requirements = null
                    }
                };

                // Configure PlayReady license template.
                string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                IContentKeyAuthorizationPolicyOption policyOption =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, newLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(policyOption);

                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // hello following code configures PlayReady License Template using .NET classes
                // and returns hello XML string.

                PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }

            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }
        }
    }

## <a name="using-static-encryption-tooprotect-hlsv3-with-aes-128"></a><span data-ttu-id="11628-164">Gebruik van statische versleuteling tooProtect HLSv3 met AES-128</span><span class="sxs-lookup"><span data-stu-id="11628-164">Using Static Encryption tooProtect HLSv3 with AES-128</span></span>
<span data-ttu-id="11628-165">Als u wilt dat tooencrypt uw HLS met AES-128, hebt u een keuze van het gebruik van dynamische versleuteling (hello aanbevolen optie) of statische versleuteling (zoals in deze sectie).</span><span class="sxs-lookup"><span data-stu-id="11628-165">If you want tooencrypt your HLS with AES-128, you have a choice of using dynamic encryption (hello recommended option) or static encryption (as shown in this section).</span></span> <span data-ttu-id="11628-166">Als u dynamische versleuteling toouse, Zie [met behulp van dynamische AES-128-versleuteling en de Service voor het leveren van sleutel](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="11628-166">If you decide toouse dynamic encryption, see [Using AES-128 Dynamic Encryption and Key Delivery Service](media-services-protect-with-aes128.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11628-167">In volgorde tooconvert uw inhoud in HLS, u moet eerst worden geconverteerd/uw inhoud codeert in Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="11628-167">In order tooconvert your content into HLS, you must first convert/encode your content into Smooth Streaming.</span></span>
> <span data-ttu-id="11628-168">Voor Hallo HLS tooget versleuteld met AES Controleer ook of tooset Hallo volgende eigenschappen in uw bestand MediaPackager_SmoothToHLS.xml: set Hallo eigenschap tootrue set Hallo sleutelwaarde en Hallo keyuri waarde toopoint tooyour authentication\ versleutelen autorisatie-server.</span><span class="sxs-lookup"><span data-stu-id="11628-168">Also, for hello HLS tooget encrypted with AES make sure tooset hello following properties in your MediaPackager_SmoothToHLS.xml file: set hello encrypt property tootrue, set hello key value, and hello keyuri value toopoint tooyour authentication\authorization server.</span></span>
> <span data-ttu-id="11628-169">Media Services maakt een sleutelbestand en deze in Hallo asset container te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="11628-169">Media Services will create a key file and place it in hello asset container.</span></span> <span data-ttu-id="11628-170">U moet Hallo /asset-containerguid/*.key bestandsserver tooyour kopiëren (of uw eigen sleutelbestand maken) en verwijder Hallo *.key bestand uit Hallo asset container.</span><span class="sxs-lookup"><span data-stu-id="11628-170">You should copy hello /asset-containerguid/*.key file tooyour server (or create your own key file) and then delete hello *.key file from hello asset container.</span></span>
> 
> 

<span data-ttu-id="11628-171">Hallo-voorbeeld in deze sectie codeert een tussentijds bestand (in dit geval MP4) in multibitrate MP4-bestanden en vervolgens MP4s worden verpakt in Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="11628-171">hello example in this section encodes a mezzanine file (in this case MP4) into multibitrate MP4 files and then packages MP4s into Smooth Streaming.</span></span> <span data-ttu-id="11628-172">Deze vervolgens pakketten Smooth Streaming in Live Streaming HLS (HTTP) versleuteld met Advanced Encryption Standard (AES) stroom 128-bits versleuteling.</span><span class="sxs-lookup"><span data-stu-id="11628-172">It then packages Smooth Streaming into HTTP Live Streaming (HLS) encrypted with Advanced Encryption Standard (AES) 128-bit stream encryption.</span></span> <span data-ttu-id="11628-173">Zorg ervoor dat tooupdate Hallo code toopoint toohello map bevindt de invoer MP4-bestand te volgen.</span><span class="sxs-lookup"><span data-stu-id="11628-173">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span> <span data-ttu-id="11628-174">En ook toowhere configuratiebestanden MediaPackager_MP4ToSmooth.xml en MediaPackager_SmoothToHLS.xml zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="11628-174">And also toowhere your MediaPackager_MP4ToSmooth.xml and MediaPackager_SmoothToHLS.xml configuration files are located.</span></span> <span data-ttu-id="11628-175">U vindt Hallo definitie voor deze bestanden in Hallo [taak vooraf voor Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="11628-175">You can find hello definition for these files in hello [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;

    namespace MediaServicesContentProtection
    {
        class Program
        {
            // Paths toosupport files (within hello above base path). You can use 
            // hello provided sample media files from hello "SupportFiles" folder, or 
            // provide paths tooyour own media files below toorun these samples.

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"SingleMP4\BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";

            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName = 
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey = 
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName, 
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Encoding and encrypting assets //////////////////////

                // Load an MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset = ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create HLS encrypted with AES.
                IAsset HLSEncryptedWithAESAsset = CreateHLSEncryptedWithAES(clearSmoothStreamAsset);

                // You can use hello following player tootest hello HLS with AES stream.
                // http://apps.microsoft.com/windows/app/3ivx-hls-player/f79ce7d0-2993-4658-bc4e-83dc182a0614 
                string hlsWithAESURL = HLSEncryptedWithAESAsset.GetHlsUri().ToString();
                Console.WriteLine("HLS with AES URL:");
                Console.WriteLine(hlsWithAESURL);
            }


            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeSingleMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Streaming.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains Smooth Streaming.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Encrypts an HLS with AES-128.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateHLSEncryptedWithAES(IAsset clearSmoothStreamAsset)
            {
                IJob job = _context.Jobs.Create("Encrypt tooHLS with AES.");

                // Add task 1 - Package clear Smooth Streaming tooHLS with AES.
                PackageSmoothStreamToHLS(job, clearSmoothStreamAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // hello OutputMediaAssets[0] contains hello desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[0],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[0];
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                return asset;
            }

            /// <summary>
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeSingleMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s", 
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles, 
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset = 
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Streaming", 
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }

            /// <summary>
            /// Converts Smooth Streaming tooHLS.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello Smooth Streaming asset.</param>
            /// <returns>hello asset that was packaged tooHLS.</returns>
            private static IAsset PackageSmoothStreamToHLS(IJob job, IAsset smoothStreamAsset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Read hello configuration data into a string. 
                // For hello HLS tooget encrypted with AES make sure tooset the
                // encrypt configuration property tootrue.
                //
                // In production, it is recommended toodo hello following:
                //    Set a Key url for your authn/authz server.
                //    Copy hello /asset-containerguid/*.key file tooyour server (or craft a key file for yourself).
                //    Delete *.key from hello asset container.
                //
                string configuration = File.ReadAllText(Path.Combine(_configurationXMLFiles, @"MediaPackager_SmoothToHLS.xml"));

                // Create a task with hello encoding details, using a configuration file.
                ITask task = job.Tasks.AddNew("My Smooth Streaming tooHLS Task",
                   processor,
                   configuration,
                   TaskOptions.ProtectedConfiguration);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(smoothStreamAsset);

                // Add an output asset toocontain hello results of hello job. 
                IAsset outputAsset = 
                    task.OutputAssets.AddNew("HLS asset", AssetCreationOptions.None);


                return outputAsset;
            }
        }
    }

## <a name="using-static-encryption-tooprotect-hlsv3-with-playready"></a><span data-ttu-id="11628-176">Gebruik van statische versleuteling tooProtect HLSv3 met PlayReady</span><span class="sxs-lookup"><span data-stu-id="11628-176">Using Static Encryption tooProtect HLSv3 with PlayReady</span></span>
<span data-ttu-id="11628-177">Als u uw inhoud met PlayReady tooprotect wilt, hebt u een keuze uit met behulp van [dynamische versleuteling](media-services-protect-with-drm.md) (hello aanbevolen optie) of statische versleuteling (zoals beschreven in deze sectie).</span><span class="sxs-lookup"><span data-stu-id="11628-177">If you want tooprotect your content with PlayReady, you have a choice of using [dynamic encryption](media-services-protect-with-drm.md) (hello recommended option) or static encryption (as described in this section).</span></span>

> [!NOTE]
> <span data-ttu-id="11628-178">In de volgorde tooprotect inhoud met PlayReady u moet eerst worden geconverteerd/uw inhoud codeert naar een indeling Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="11628-178">In order tooprotect your content using PlayReady you must first convert/encode your content into a Smooth Streaming format.</span></span>
> 
> 

<span data-ttu-id="11628-179">Hallo-voorbeeld in deze sectie codeert een tussentijds bestand (in dit geval MP4) naar multibitrate MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="11628-179">hello example in this section encodes a mezzanine file (in this case MP4) into multibitrate MP4 files.</span></span> <span data-ttu-id="11628-180">En vervolgens MP4s worden verpakt in Smooth Streaming en versleutelt Smooth Streaming met PlayReady.</span><span class="sxs-lookup"><span data-stu-id="11628-180">It then packages MP4s into Smooth Streaming and encrypts Smooth Streaming with PlayReady.</span></span> <span data-ttu-id="11628-181">tooproduce HTTP Live Streaming (HLS) versleuteld met PlayReady, Hallo PlayReady Smooth Streaming asset moet toobe in HLS verpakt.</span><span class="sxs-lookup"><span data-stu-id="11628-181">tooproduce HTTP Live Streaming (HLS) encrypted with PlayReady, hello PlayReady Smooth Streaming asset needs toobe packaged into HLS.</span></span> <span data-ttu-id="11628-182">Dit onderwerp wordt beschreven hoe tooperform al deze stappen.</span><span class="sxs-lookup"><span data-stu-id="11628-182">This topic demonstrates how tooperform all these steps.</span></span>

<span data-ttu-id="11628-183">Media Services biedt nu een service voor het leveren van Microsoft PlayReady-licenties.</span><span class="sxs-lookup"><span data-stu-id="11628-183">Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="11628-184">Hallo voorbeeld in dit artikel laat zien hoe tooconfigure Hallo Media Services PlayReady service voor het leveren van licentie (Zie Hallo **ConfigureLicenseDeliveryService** methode die is gedefinieerd in het Hallo-code hieronder).</span><span class="sxs-lookup"><span data-stu-id="11628-184">hello example in this article shows how tooconfigure hello Media Services PlayReady license delivery service (see hello **ConfigureLicenseDeliveryService** method defined in hello code below).</span></span> 

<span data-ttu-id="11628-185">Zorg ervoor dat tooupdate Hallo code toopoint toohello map bevindt de invoer MP4-bestand te volgen.</span><span class="sxs-lookup"><span data-stu-id="11628-185">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span> <span data-ttu-id="11628-186">En ook toowhere MediaPackager_MP4ToSmooth.xml MediaPackager_SmoothToHLS.xml en MediaEncryptor_PlayReadyProtection.xml bestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="11628-186">And also toowhere your MediaPackager_MP4ToSmooth.xml, MediaPackager_SmoothToHLS.xml, and MediaEncryptor_PlayReadyProtection.xml files are located.</span></span> <span data-ttu-id="11628-187">MediaPackager_MP4ToSmooth.xml en MediaPackager_SmoothToHLS.xml zijn gedefinieerd in [taak vooraf voor Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) en MediaEncryptor_PlayReadyProtection.xml wordt gedefinieerd in Hallo [taak definitie voor Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="11628-187">MediaPackager_MP4ToSmooth.xml and MediaPackager_SmoothToHLS.xml are defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) and MediaEncryptor_PlayReadyProtection.xml is defined in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace MediaServicesContentProtection
    {
        class Program
        {
            // Paths toosupport files (within hello above base path). You can use 
            // hello provided sample media files from hello "SupportFiles" folder, or 
            // provide paths tooyour own media files below toorun these samples.

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"SingleMP4\BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";


            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Used hello chached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Load an MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset = ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create a common encryption content key that is used 
                // a) tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
                //    that is used for encryption.
                // b) tooconfigure hello license delivery service and 
                //
                Guid keyId;
                byte[] contentKey;

                IContentKey key = CreateCommonEncryptionKey(out keyId, out contentKey);

                // hello content key authorization policy must be configured by you 
                // and met by hello client in order for hello PlayReady license
                // toobe delivered toohello client. 
                // In this example hello Media Services PlayReady license delivery service is used.
                ConfigureLicenseDeliveryService(key);

                // Get hello Media Services PlayReady license delivery URL.
                // This URL will be assigned toohello licenseAcquisitionUrl property 
                // of hello MediaEncryptor_PlayReadyProtection.xml file.
                Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

                // Update hello MediaEncryptor_PlayReadyProtection.xml file with hello key and URL info.
                UpdatePlayReadyConfigurationXMLFile(keyId, contentKey, acquisitionUrl);

                // Create HLS encrypted with PlayReady.
                IAsset playReadyHLSAsset = CreateHLSEncryptedWithPlayReady(clearSmoothStreamAsset);
                //
                string hlsWithPlayReadyURL = playReadyHLSAsset.GetHlsUri().ToString();
                Console.WriteLine("HLS with PlayReady URL:");
                Console.WriteLine(hlsWithPlayReadyURL);
            }

            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeSingleMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Streaming.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains Smooth Streaming.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Create a common encryption content key that is used 
            /// tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
            /// that is used for encryption.
            /// </summary>
            /// <param name="keyId"></param>
            /// <param name="contentKey"></param>
            /// <returns></returns>
            public static IContentKey CreateCommonEncryptionKey(out Guid keyId, out byte[] contentKey)
            {
                keyId = Guid.NewGuid();
                contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            /// <summary>
            /// Update your configuration .xml file dynamically.
            /// </summary>
            public static void UpdatePlayReadyConfigurationXMLFile(Guid keyId, byte[] keyValue, Uri licenseAcquisitionUrl)
            {
                string xmlFileName = Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml");

                XNamespace xmlns = "http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#";

                // Prepare hello encryption task template
                XDocument doc = XDocument.Load(xmlFileName);

                var licenseAcquisitionUrlEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "licenseAcquisitionUrl")
                        .FirstOrDefault();
                var contentKeyEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "contentKey")
                        .FirstOrDefault();
                var keyIdEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "keyId")
                        .FirstOrDefault();

                // Update hello "value" property.
                if (licenseAcquisitionUrlEl != null)
                    licenseAcquisitionUrlEl.Attribute("value").SetValue(licenseAcquisitionUrl.ToString());

                if (contentKeyEl != null)
                    contentKeyEl.Attribute("value").SetValue(Convert.ToBase64String(keyValue));

                if (keyIdEl != null)
                    keyIdEl.Attribute("value").SetValue(keyId);

                doc.Save(xmlFileName);
            }

            /// <summary>
            // Encrypts clear Smooth Streaming tooSmooth Streaming with PlayReady.
            // Then, packages hello PlayReady Smooth Streaming tooHLS with PlayReady.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateHLSEncryptedWithPlayReady(IAsset clearSmoothStreamAsset)
            {
                IJob job = _context.Jobs.Create("Encrypt tooHLS with PlayReady.");

                // Add task 1 - Encrypt Smooth Streaming with PlayReady 
                IAsset encryptedSmoothAsset =
                    EncryptSmoothStreamWithPlayReadyTask(job, clearSmoothStreamAsset);

                // Add task 2 - Package tooHLS with PlayReady.
                PackageSmoothStreamToHLS(job, encryptedSmoothAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Since we had two tasks, hello OutputMediaAssets[1]
                // contains hello desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[1],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });


                return asset;

            }
            /// <summary>
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeSingleMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s",
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles,
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset =
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Streaming",
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }


            /// <summary>
            /// Converts Smooth Stream tooHLS.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello Smooth Stream asset.</param>
            /// <returns>hello asset that was packaged tooHLS.</returns>
            private static IAsset PackageSmoothStreamToHLS(IJob job, IAsset smoothStreamAsset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Read hello configuration data into a string. 
                //
                string configuration = File.ReadAllText(
                            Path.Combine(_configurationXMLFiles,
                                        @"MediaPackager_SmoothToHLS.xml"));

                // Create a task with hello encoding details, using a configuration file.
                ITask task = job.Tasks.AddNew("My Smooth tooHLS Task",
                   processor,
                   configuration,
                   TaskOptions.ProtectedConfiguration);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(smoothStreamAsset);

                // Add an output asset toocontain hello results of hello job. 
                IAsset outputAsset =
                    task.OutputAssets.AddNew("HLS asset", AssetCreationOptions.None);


                return outputAsset;
            }

            /// <summary>
            /// Creates a task tooencrypt Smooth Streaming with PlayReady.
            /// Note: Do deliver DASH, make sure tooset hello useSencBox and adjustSubSamples 
            /// configuration properties tootrue.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncryptSmoothStreamWithPlayReadyTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Encryptor.
                IMediaProcessor playreadyProcessor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaEncryptor);

                // Read hello configuration XML.
                //
                // Note that hello configuration defined in MediaEncryptor_PlayReadyProtection.xml
                // is using keySeedValue. It is recommended that you do this only for testing 
                // and not in production. For more information, see 
                // http://msdn.microsoft.com/library/windowsazure/dn189154.aspx.
                //
                string configPlayReady = File.ReadAllText(Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml"));

                ITask playreadyTask = job.Tasks.AddNew("My PlayReady Task",
                   playreadyProcessor,
                   configPlayReady,
                   TaskOptions.ProtectedConfiguration);

                playreadyTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.CommonEncryptionProtected.
                IAsset playreadyAsset = playreadyTask.OutputAssets.AddNew(
                                                "PlayReady Smooth Streaming",
                                                AssetCreationOptions.CommonEncryptionProtected);


                return playreadyAsset;
            }


            /// <summary>
            /// Configures authorization policy for hello content key. 
            /// </summary>
            /// <param name="contentKey">hello content key.</param>
            static public void ConfigureLicenseDeliveryService(IContentKey contentKey)
            {
                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                    new ContentKeyAuthorizationPolicyRestriction 
                    { 
                        Name = "Open", 
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                        Requirements = null
                    }
                };

                // Configure PlayReady license template.
                string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                IContentKeyAuthorizationPolicyOption policyOption =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, newLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(policyOption);

                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // hello following code configures PlayReady License Template using .NET classes
                // and returns hello XML string.

                PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }
            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }

        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="11628-188">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="11628-188">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="11628-189">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="11628-189">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

