---
title: dynamische aaaUsing AES-128-versleuteling en de sleutel service voor het leveren | Microsoft Docs
description: Microsoft Azure Media Services kunt u toodeliver uw inhoud die is versleuteld met AES-128-bits versleutelingssleutels. Media Services biedt ook een service voor het leveren van de sleutel Hallo die zorgt voor versleuteling sleutels tooauthorized gebruikers. Dit onderwerp wordt beschreven hoe toodynamically versleutelen met AES-128 en Hallo sleutellevering service gebruiken.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a>Met behulp van dynamische AES-128-versleuteling en sleutellevering service
> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-aes128.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Overzicht
> [!NOTE]
> Zie [dit](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video voor een overzicht van hoe tooprotect uw Media Content met AES-versleuteling.
> 
> 

Microsoft Azure Media Services kunt u toodeliver Http-Live-Streaming (HLS) en Smooth Streams versleuteld met Advanced Encryption Standard (AES) (met behulp van coderingssleutels 128-bits). Media Services biedt ook een service voor het leveren van de sleutel Hallo die zorgt voor versleuteling sleutels tooauthorized gebruikers. Als u voor Media Services tooencrypt een asset wilt, u moet een versleutelingssleutel met Hallo asset tooassociate en autorisatiebeleid voor Hallo sleutel ook configureren. Wanneer een stream is aangevraagd door een speler, Media Services gebruikt Hallo opgegeven sleutel toodynamically versleutelen van uw inhoud met behulp van AES-versleuteling. toodecrypt hello stream, Hallo player vraagt de Hallo sleutel van Hallo sleutellevering-service. toodecide of Hallo gebruiker is gemachtigd tooget Hallo sleutel, Hallo service beoordeelt Hallo autorisatiebeleid die u hebt opgegeven voor Hallo-sleutel.

Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen. Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: openen of tokenbeperking beperking. Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS). Media Services ondersteunt tokens in Hallo [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) -indeling (SWT) en [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT)-indeling. Zie voor meer informatie [autorisatiebeleid Hallo de inhoudssleutel configureren](media-services-protect-with-aes128.md#configure_key_auth_policy).

tootake profiteren van dynamische versleuteling hoeft u toohave een asset die een set multi-bitrate MP4-bestanden of multi-bitrate Smooth Streaming-bronbestanden bevat. U moet ook tooconfigure Hallo leveringsbeleid voor Hallo asset (Zie verderop in dit onderwerp). Vervolgens, op basis van opgegeven in de streaming-URL Hallo Hallo-indeling, Hallo On-Demand Streaming server zorgt ervoor dat Hallo-stream wordt geleverd in Hallo protocol dat u hebt gekozen. Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services-service bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client.

In dit onderwerp is nuttig toodevelopers die werken aan toepassingen die beveiligde media leveren. Hallo onderwerp leest u hoe tooconfigure sleutellevering service met een autorisatiebeleid Hallo zodat alleen geautoriseerde clients Hallo versleutelingssleutels kunnen ontvangen. U ziet ook hoe toouse dynamische versleuteling.


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a>Sleutellevering servicewerkstroom en dynamische AES-128-versleuteling

Hallo hieronder vindt u algemene stappen zou u tooperform moet bij het versleutelen van uw assets met AES, met behulp van Hallo Media Services sleutellevering service en dynamische versleuteling.

1. [Maak een asset en upload bestanden in Hallo asset](media-services-protect-with-aes128.md#create_asset).
2. [Hallo asset met Hallo bestand toohello adaptive bitrate MP4-set coderen](media-services-protect-with-aes128.md#encode_asset).
3. [Maak een inhoudssleutel en deze koppelen aan Hallo gecodeerde asset](media-services-protect-with-aes128.md#create_contentkey). Hallo inhoudssleutel bevat in Media Services de versleutelingssleutel van Hallo actief.
4. [Hallo de inhoudssleutel verificatiebeleid configureren](media-services-protect-with-aes128.md#configure_key_auth_policy). Hallo autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en door de client Hallo Hallo inhoud sleutel toobe geleverde toohello client zodat wordt voldaan.
5. [Configureer het leveringsbeleid Hallo voor een asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy). Hallo levering-beleidsconfiguratie omvat:-URL voor het verkrijgen en initialisatie-Vector (IV) (AES 128 vereist Hallo dezelfde IV toobe opgegeven bij het versleutelen en ontsleutelen), leveringsprotocol (bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), Hallo type dynamische versleuteling (bijvoorbeeld envelop of er geen dynamische versleuteling).

    U kunt verschillende beleid tooeach protocol toepassen op Hallo dezelfde asset. U kunt bijvoorbeeld PlayReady-versleuteling tooSmooth/DASH en AES Envelope tooHLS toepassen. Alle protocollen die niet zijn gedefinieerd in een leveringsbeleid (bijvoorbeeld, u toevoegen één beleid waarmee alleen HLS als protocol Hallo) van streaming wordt geblokkeerd. Hallo uitzondering toothis is als u geen leveringsbeleid voor Assets helemaal gedefinieerd. Vervolgens zijn alle protocollen toegestaan in Hallo wissen.

6. [Maak een OnDemand-locator](media-services-protect-with-aes128.md#create_locator) in volgorde tooget een streaming-URL.

Hallo-onderwerp bevat ook [hoe een clienttoepassing kan aanvragen voor een sleutel van Hallo sleutellevering service](media-services-protect-with-aes128.md#client_request).

Vindt u een volledige .NET [voorbeeld](media-services-protect-with-aes128.md#example) achter Hallo Hallo onderwerp.

Hallo volgende afbeelding ziet u Hallo werkstroom die hierboven worden beschreven. Hallo-token wordt hier gebruikt voor verificatie.

![Beschermen met AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

Hallo rest van dit onderwerp bevat gedetailleerde uitleg, codevoorbeelden en koppelingen tootopics waarin u kunt hoe tooachieve Hallo zien hierboven beschreven taken.

## <a name="current-limitations"></a>Huidige beperkingen
Als u het leveringsbeleid voor uw asset toevoegt of bijwerkt, moet u een bestaande locator (indien aanwezig) verwijderen en een nieuwe locator maken.

## <a id="create_asset"></a>Maak een asset en upload bestanden in Hallo asset
In de volgorde toomanage, coderen en streamen video's, moet u eerst uw inhoud uploaden naar Microsoft Azure Media Services. Na het uploaden, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming. 

Zie [Upload Files into a Media Services account](media-services-dotnet-upload-files.md) (Bestanden uploaden naar een Media Services-account) voor gedetailleerde informatie.

## <a id="encode_asset"></a>Hallo asset met Hallo bestand toohello adaptive bitrate die MP4-set coderen
Bij dynamische versleuteling hoeft u toocreate een asset die een set multi-bitrate MP4-bestanden of multi-bitrate Smooth Streaming-bronbestanden bevat. Vervolgens, op basis van de opgegeven indeling in het manifest Hallo Hallo of fragment aanvraag, Hallo On-Demand Streaming server zorgt ervoor dat u Hallo stream ontvangt in Hallo protocol dat u hebt gekozen. Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services-service bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client. Zie voor meer informatie, Hallo [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) onderwerp.

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 
>
>Bovendien toobe kunnen toouse dynamische pakketten en dynamische versleuteling uw asset moet bevatten een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden.

Voor instructies over het tooencode, Zie [hoe tooencode een asset met Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Maak een inhoudssleutel en deze koppelen aan Hallo gecodeerde asset
In Media Services bevat inhoudssleutel Hallo Hallo-sleutel die u een asset tooencrypt wilt met.

Zie [Create content key](media-services-dotnet-create-contentkey.md) (Inhoudssleutel maken) voor gedetailleerde informatie.

## <a id="configure_key_auth_policy"></a>Autorisatiebeleid Hallo de inhoudssleutel configureren
Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen. Hallo autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en voldaan door Hallo-client (speler) om Hallo sleutel toobe toohello client geleverd. Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: open, token beperking of IP-beperking.

Zie [Autorisatiebeleid voor inhoudssleutels configureren](media-services-dotnet-configure-content-key-auth-policy.md) voor gedetailleerde informatie.

## <a id="configure_asset_delivery_policy"></a>Leveringsbeleid voor assets configureren
Configureer Hallo leveringsbeleid voor uw asset. Een aantal zaken die Hallo asset configuratie van een leveringsbeleid omvat:

* Hallo-URL voor het verkrijgen van sleutel. 
* Hallo initialisatie Vector (IV) toouse voor Hallo envelop versleuteling. AES-128 vereist Hallo dezelfde IV toobe opgegeven bij het versleutelen en ontsleutelen. 
* Hallo asset leveringsprotocol (bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle).
* Hallo type dynamische versleuteling (bijvoorbeeld AES envelope) of er geen dynamische versleuteling. 

Zie [Leveringsbeleid voor assets configureren](media-services-rest-configure-asset-delivery-policy.md) voor gedetailleerde informatie.

## <a id="create_locator"></a>Maak een OnDemand-streaminglocator in volgorde tooget een streaming-URL
U moet tooprovide uw gebruiker Hello streaming-URL voor Smooth, DASH of HLS.

> [!NOTE]
> Als u het leveringsbeleid voor uw asset toevoegt of bijwerkt, moet u een bestaande locator (indien aanwezig) verwijderen en een nieuwe locator maken.
> 
> 

Voor instructies over hoe toopublish een asset en bouwen van een streaming-URL, Zie [bouwen van een streaming-URL](media-services-deliver-streaming-content.md).

## <a name="get-a-test-token"></a>Een test-token ophalen
Een test-token ophalen op basis van de tokenbeperking Hallo die werd gebruikt voor het sleutelautorisatiebeleid Hallo.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);

U kunt Hallo [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest uw stream.

## <a id="client_request"></a>Hoe kan de client een sleutel van Hallo sleutellevering service aanvragen?
In de vorige stap hello, moet u Hallo-URL die tooa manifestbestand verwijst samengesteld. De client moet tooextract Hallo benodigde gegevens van de manifest-bestanden in de volgorde toomake een aanvraag toohello sleutellevering service streaming Hallo.

### <a name="manifest-files"></a>Manifestbestanden
Hallo client tooextract Hallo URL (dat ook bevat inhoudssleutel Id (kid)) moet de waarde van het manifestbestand Hallo. Hallo-client wordt en probeer het tooget Hallo versleutelingssleutel van Hallo sleutellevering-service. Hallo client moet ook tooextract Hallo IV waarde en gebruik het Hallo stream.hello volgende codefragment ontsleutelen toont Hallo <Protection> element van Hallo Smooth Streaming manifest.

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

In geval van HLS Hallo is Hallo hoofdmap manifest onderverdeeld in segment bestanden. 

Hallo hoofdmap manifest is bijvoorbeeld: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) en het bevat een lijst met bestandsnamen segment.

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

Als u een van Hallo segment bestanden in de teksteditor (bijvoorbeeld http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should openen bevatten #EXT-X-sleutel, waarmee wordt aangegeven dat Hallo-bestand is versleuteld.

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
>Als u van plan bent tooplay een AES HLS in Safari versleuteld, Zie [deze blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

### <a name="request-hello-key-from-hello-key-delivery-service"></a>Hallo-sleutel van Hallo sleutellevering service aanvragen

Hallo volgende code toont hoe toosend een aanvraag toohello Media Services sleutel service voor het leveren met behulp van een sleutel levering Uri (dat is opgehaald uit Hallo manifest) en een token (in dit onderwerp spreekt niet over hoe tooget Simple Web Tokens uit een Secure Token Service).

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a>De inhoud beveiligen met AES-128 met .NET

### <a name="create-and-configure-a-visual-studio-project"></a>Maak en configureer een Visual Studio-project.

1. Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md). 
2. Hallo elementen te volgen toevoegen**appSettings** gedefinieerd in het bestand app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <a id="example"></a>Voorbeeld

Hallo-code in uw Program.cs-bestand met de Hallo-code die wordt weergegeven in deze sectie worden overschreven.
 
>[!NOTE]
>Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn). Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.

Zorg ervoor dat tooupdate variabelen toopoint toofolders waar uw invoerbestanden zich bevinden.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
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
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin. 
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file. 
            return originLocator.Path + assetFile.Name;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

