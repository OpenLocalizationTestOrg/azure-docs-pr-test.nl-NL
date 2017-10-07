---
title: aaaGet gestart met het leveren van inhoud on demand met .NET | Microsoft Docs
description: Deze zelfstudie leert u Hallo van een on demand leveren van inhoud toepassing implementeren met Azure Media Services met .NET.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a>Aan de slag met het leveren van inhoud on demand met .NET SDK
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Deze zelfstudie leert u Hallo van een eenvoudige Video-on-Demand (VoD) leveren van inhoud service implementeren met Azure Media Services (AMS)-toepassing hello Azure Media Services .NET SDK gebruiken.

## <a name="prerequisites"></a>Vereisten

Hallo volgen vereist toocomplete Hallo-zelfstudie:

* Een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.
* Een Media Services-account. een Media Services-account toocreate Zie [hoe tooCreate een Media Services-Account](media-services-portal-create-account.md).
* .NET framework 4.0 of hoger.
* Visual Studio.

Deze zelfstudie bevat Hallo taken te volgen:

1. Start de streaming-eindpunt (met behulp van hello Azure-portal).
2. Een Visual Studio-project maken en configureren.
3. Toohello Media Services-account koppelen.
2. Een videobestand uploaden.
3. Hallo-bronbestand coderen in een set adaptive bitrate MP4-bestanden.
4. Hallo asset publiceren en get streamen en progressief downloaden van URL's.  
5. Uw inhoud afspelen.

## <a name="overview"></a>Overzicht
In deze zelfstudie wordt u begeleid Hallo stappen voor het implementeren van een eenvoudige (VoD) leveren van inhoud toepassing met Azure Media Services (AMS) SDK voor .NET.

Hallo-zelfstudie introduceert Hallo basiswerkstroom Media Services en de meest algemene programmeerobjecten Hallo en taken die zijn vereist voor het ontwikkelen van Media Services. Bij voltooiing Hallo Hallo zelfstudie, wordt u kunnen toostream of progressief downloaden van media met een voorbeeldbestand die geüpload, gecodeerd en gedownload.

### <a name="ams-model"></a>AMS-model

Hello volgende afbeelding ziet u enkele van de meest gebruikte Hallo objecten wanneer VoD toepassingen ontwikkelt voor Hallo Media Services OData-model.

Klik op Hallo installatiekopie tooview het maximale grootte.  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

U kunt hele model Hallo weergeven [hier](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Start de streaming-eindpunten met hello Azure-portal

Als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo leveren van video via adaptive bitrate streaming. Media Services biedt dynamische pakketten zodat u toodeliver uw adaptive bitrate MP4-inhoud in de streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, zonder dat u vooraf verpakte toostore hoeft versies van elk van deze streaming-indelingen.

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.

toostart Hallo streaming-eindpunt, Hallo te volgen:

1. Aanmelden op Hallo [Azure-portal](https://portal.azure.com/).
2. Klik in het venster Instellingen Hallo, Streaming-eindpunten.
3. Klik op Hallo standaardstreaming-eindpunt.

    Hallo DEFAULT STREAMING ENDPOINT DETAILS venster wordt weergegeven.

4. Klik op Hallo Start pictogram.
5. Klik op Hallo opslaan knop toosave uw wijzigingen.

## <a name="create-and-configure-a-visual-studio-project"></a>Maak en configureer een Visual Studio-project.

1. Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md). 
2. Maak een nieuwe map (map kan zich ergens op uw lokale schijf) en kopieer een MP4-bestand dat u tooencode en streamen wilt of progressief te downloaden. In dit voorbeeld wordt Hallo 'C:\VideoFiles' pad gebruikt.

## <a name="connect-toohello-media-services-account"></a>Verbinding maken met toohello Media Services-account

Wanneer u Media Services met .NET, moet u Hallo **CloudMediaContext** klasse voor de meeste Media Services-programmeertaken: verbinding maken met tooMedia Services-account; maken, bijwerken, gebruiken en verwijderen van de volgende Hallo objecten: assets, assetbestanden, taken, toegangsbeleid, locators, enzovoort.

Hallo standaardklasse Program met Hallo volgende code worden overschreven. Hallo code laat zien hoe tooread hello uit Hallo App.config-bestand verbindingswaarden en hoe toocreate hello **CloudMediaContext** Services-object in de volgorde tooconnect tooMedia. Zie voor meer informatie [toohello Media Services-API verbinden](media-services-use-aad-auth-to-access-ams-api.md).

Zorg ervoor dat tooupdate Hallo bestand naam en pad toowhere die u hebt uw mediabestand.

Hallo **Main** functie methoden aangeroepen die worden gedefinieerd in deze sectie verder.

> [!NOTE]
> U wordt worden ophalen compilatiefouten totdat u de definities voor alle Hallo functies toevoegt.

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a>Een nieuwe asset maken en een videobestand uploaden

In Media Services moet u uw digitale bestanden uploaden naar (of opnemen in) een asset. Hallo **Asset** entiteit kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.)  Zodra het Hallo-bestanden zijn geüpload, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming. Hallo-bestanden in Hallo asset heten **Assetbestanden**.

Hallo **UploadFile** methode die is gedefinieerd onder aanroepen **CreateFromFile** (gedefinieerd in .NET SDK Extensions). **CreateFromFile** maakt een nieuwe asset in welke Hallo opgegeven bestand is geüpload.

Hallo **CreateFromFile** methode vergt **AssetCreationOptions** waarmee u kunt een van de volgende opties voor het maken van asset Hallo opgeven:

* **Geen**: er wordt geen versleuteling gebruikt. Dit is de standaardwaarde Hallo. Houd er rekening mee dat bij gebruik van deze optie de inhoud tijdens de overdracht of in de opslag niet is beveiligd.
  Als u van plan toodeliver een MP4 via progressief downloaden bent, moet u deze optie gebruiken.
* **StorageEncrypted** -Gebruik deze optie tooencrypt versleutelde inhoud lokaal met Advanced Encryption Standard (AES) 256-bitsversleuteling, die geüpload en tooAzure opslag wordt bewaard in rust versleuteld. Automatisch worden beveiligd met Storage Encryption activa niet-versleuteld en geplaatst in een versleuteld bestand system eerdere tooencoding en eventueel opnieuw versleutelde voorafgaande toouploading weer als een nieuwe uitvoerasset. Hallo primaire gebruiksvoorbeeld voor versleuteling van opslag is wanneer u dat deze toosecure invoer van hoge kwaliteit mediabestanden met een sterke codering in rust op schijf.
* **CommonEncryptionProtected**: gebruik deze optie als u inhoud uploadt die al is versleuteld en beveiligd met Common Encryption of PlayReady DRM (bijvoorbeeld Smooth Streaming beveiligd met PlayReady DRM).
* **EnvelopeEncryptionProtected**: gebruik deze optie als u een HLS-stream uploadt die is versleuteld met AES. Houd er rekening mee dat Hallo bestanden moeten zijn gecodeerd en versleuteld door Transform Manager.

Hallo **CreateFromFile** methode kunt u een retouraanroep opgeven in de volgorde tooreport hello uploadvoortgang van Hallo-bestand.

In Hallo voorbeeld te volgen, geven we **geen** voor Hallo assetopties.

Hallo na methode toohello programma klasse toevoegen.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a>Hallo-bronbestand coderen in een set adaptive bitrate MP4-bestanden
Nadat assets in Media Services, kan de media worden gecodeerd, transmuxed, een watermerk, enzovoort, voordat deze tooclients wordt afgeleverd. Deze activiteiten worden gepland en uitgevoerd op meerdere achtergrond rol exemplaren tooensure hoge prestaties en beschikbaarheid. Deze activiteiten worden taken genoemd, en elke taak bestaat uit atomische taken die daadwerkelijk werken op Hallo assetbestand Hallo.

Zoals is eerder vermeld, als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo adaptive bitrate streaming-tooyour clients leveren. Media Services kunt u een dynamisch pakket een set adaptive bitrate MP4-bestanden in een van de volgende indelingen Hallo: HTTP Live Streaming (HLS), Smooth Streaming- en MPEG DASH.

tootake profiteren van dynamische pakketten hoeft u tooencode of transcodeer uw tussentijds (bron) bestand in een set adaptive bitrate MP4-bestanden of adaptive bitrate Smooth Streaming-bestanden.  

Hallo volgende code toont hoe een codering toosubmit taak. Hallo taak bevat één taak die aangeeft dat tootranscode Hallo tussentijds bestand in een set adaptive bitrate MP4s met behulp van **Media Encoder Standard**. Hallo code verzendt Hallo taak en wacht totdat deze is voltooid.

Als het Hallo-taak is voltooid, zou u kunnen toostream worden uw asset of MP4-bestanden die zijn gemaakt als gevolg van een transcodering progressief downloaden.

Hallo na methode toohello programma klasse toevoegen.

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a>Hallo asset publiceren en URL's voor streamen en progressief downloaden ophalen

toostream of download een asset, u eerst moet te 'publiceren' door een locator te maken. Locators bieden toegang toofiles opgenomen in Hallo asset. Media Services ondersteunt twee typen locators: OnDemandOrigin-locators, gebruikte toostream media (bijvoorbeeld MPEG DASH, HLS of Smooth Streaming) en Access Signature (SAS)-locators, gebruikt media-bestanden (voor meer informatie over SAS-locators Zie toodownload[dit](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).

### <a name="some-details-about-url-formats"></a>Details over URL-indelingen

Nadat u Hallo locators hebt gemaakt, kunt u Hallo-URL's die zouden worden gebruikte toostream of uw bestanden downloaden. Hallo voorbeeld in deze zelfstudie wordt de URL's die u in de juiste browsers plakken kunt uitvoer. Deze sectie bevat korte voorbeelden van hoe verschillende indelingen er uitzien.

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a>Een streaming-URL voor MPEG DASH heeft Hallo volgende indeling:

{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest**(format=mpd-time-csf)**

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a>Een streaming-URL voor HLS heeft Hallo volgende indeling:

{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest**(format=m3u8-aapl)**

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a>Een streaming-URL voor Smooth Streaming heeft Hallo volgende indeling:

{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a>Een SAS-URL gebruikt toodownload bestanden heeft Hallo volgende indeling:

{blobcontainernaam}/{assetname}/{bestandsnaam}/{SAS-handtekening}

Media Services .NET SDK extensions bieden handige Help-methoden dat return URL's voor Hallo indeling gepubliceerde asset.

Hallo volgende code gebruikt .NET SDK Extensions toocreate locators en tooget streamen en progressief downloaden van URL's. Hallo code toont u ook hoe toodownload bestanden tooa lokale map.

Hallo na methode toohello programma klasse toevoegen.

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a>Testen door uw inhoud af te spelen

Zodra u gedefinieerd in de vorige sectie Hallo Hallo-programma uitvoert, Hallo vergelijkbare toohello volgende wordt weergegeven in het consolevenster Hallo URL's.

URL's voor adaptief streamen:

Smooth Streaming

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

HLS

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

MPEG DASH

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

URL's voor progressief downloaden (audio en video).

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


toostream uw video plak de URL in Hallo URL textbox in Hallo [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest progressief downloaden, plakt u een URL in een browser (bijvoorbeeld Internet Explorer, Chrome of Safari).

Zie de volgende onderwerpen Hallo voor meer informatie:

- [Uw inhoud afspelen op bestaande spelers](media-services-playback-content-with-existing-players.md)
- [Videospelertoepassingen ontwikkelen](media-services-develop-video-players.md)
- [Een adaptieve MPEG-DASH-videostream insluiten in een HTML5-toepassing met DASH.js](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a>Voorbeeld downloaden
Hallo codevoorbeeld Hallo-code bevat die u hebt gemaakt in deze zelfstudie: [voorbeeld](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
