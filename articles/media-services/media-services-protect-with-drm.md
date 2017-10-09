---
title: aaaUsing PlayReady en/of Widevine dynamic common encryption | Microsoft Docs
description: Microsoft Azure Media Services kunt u toodeliver MPEG DASH, Smooth Streaming- en Http-Live-Streaming (HLS) streams beveiligd met Microsoft PlayReady DRM. Ook kunt u toodelivery DASH versleuteld met Widevine DRM. Dit onderwerp leest hoe toodynamically versleutelen met PlayReady en Widevine DRM.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a>PlayReady en/of Widevine Dynamic Common Encryption gebruiken

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

Microsoft Azure Media Services kunt u toodeliver MPEG DASH, Smooth Streaming en beveiligd met HTTP-Live-Streaming (HLS)-streams [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). Ook kunt u DASH-streams toodeliver versleuteld met Widevine DRM-licenties. Zowel PlayReady als Widevine zijn versleuteld volgens de specificatie Common Encryption (ISO/IEC 23001-7 CENC) Hallo. U kunt [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (te beginnen met Hallo versie 3.5.1) of REST-API tooconfigure uw AssetDeliveryConfiguration toouse Widevine.

Media Services voorziet in een service voor het leveren van PlayReady- en Widevine DRM-licenties. Media Services biedt ook API's waarmee u Hallo rechten configureren en beperkingen voor Hallo PlayReady of Widevine DRM runtime tooenforce wanneer een gebruiker gewenste afspeelt beveiligde inhoud. Wanneer een gebruiker DRM beveiligde inhoud aanvraagt, wordt de Hallo spelertoepassing een licentie aangevraagd bij Hallo AMS-licentieservice. Hallo AMS-licentieservice verstrekt een licentie toohello player als dit is toegestaan. Een PlayReady of Widevine-licentie bevat Hallo ontsleutelingssleutel die kan worden gebruikt door Hallo client player toodecrypt en stream Hallo-inhoud.

U kunt ook Hallo AMS-partners toohelp u leveren met Widevine-licenties te volgen: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Zie integratie met [Axinom](media-services-axinom-integration.md) en [castLabs](media-services-castlabs-integration.md) voor meer informatie.

Media Services ondersteunt meerdere manieren om gebruikers te autoriseren die sleutels aanvragen. Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: openen of tokenbeperking beperking. Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS). Media Services ondersteunt tokens in Hallo [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) -indeling (SWT) en [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT)-indeling. Zie voor meer informatie verificatiebeleid configureren Hallo de inhoudssleutel.

tootake profiteren van dynamische versleuteling hoeft u toohave een asset die een set multi-bitrate MP4-bestanden of multi-bitrate Smooth Streaming-bronbestanden bevat. U moet ook tooconfigure Hallo leveringsbeleid voor Hallo asset (Zie verderop in dit onderwerp). Vervolgens, op basis van opgegeven in de streaming-URL Hallo Hallo-indeling, Hallo On-Demand Streaming server zorgt ervoor dat Hallo-stream wordt geleverd in Hallo protocol dat u hebt gekozen. Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in een één opslagindeling en Media Services bouwt en levert de juiste HTTP-antwoord Hallo op basis van elke aanvraag van een client.

In dit onderwerp is nuttig toodevelopers die werken aan toepassingen die media die zijn beveiligd met meerdere DRM's, zoals PlayReady en Widevine leveren. Hallo onderwerp leest u hoe tooconfigure PlayReady-licentieservice levering met een autorisatiebeleid Hallo zodat alleen geautoriseerde clients PlayReady of Widevine-licenties kunnen ontvangen. U ziet ook hoe toouse dynamische versleuteling met PlayReady of Widevine DRM via DASH.

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 

## <a name="download-sample"></a>Voorbeeld downloaden
U kunt downloaden Hallo voorbeeld beschreven in dit artikel [hier](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a>Dynamic Common Encryption en DRM-services voor het leveren van licenties configureren

Hallo hieronder vindt u algemene stappen zou u tooperform moet bij het beveiligen van uw assets met PlayReady met Hallo Media Services-licentieservice levering en dynamische versleuteling.

1. Maak een asset en upload bestanden in Hallo asset.
2. Hallo asset met Hallo bestand toohello adaptive bitrate die MP4-set coderen.
3. Maak een inhoudssleutel en deze koppelen aan Hallo gecodeerde asset. Hallo inhoudssleutel bevat in Media Services de versleutelingssleutel van Hallo actief.
4. Hallo de inhoudssleutel verificatiebeleid configureren. Hallo autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en door de client Hallo Hallo inhoud sleutel toobe geleverde toohello client zodat wordt voldaan.

    Wanneer u Hallo autorisatiebeleid voor inhoudssleutels maakt, hebt u toospecify Hallo volgende nodig: leveringsmethode (PlayReady of Widevine), beperkingen (openen of token) en informatie specifieke toohello type sleutellevering waarmee wordt gedefinieerd hoe Hallo-sleutel wordt geleverd toohello client ([PlayReady](media-services-playready-license-template-overview.md) of [Widevine](media-services-widevine-license-template-overview.md) licentiesjabloon).

5. Configureer het leveringsbeleid Hallo voor een asset. Hallo levering-beleidsconfiguratie omvat: leveringsprotocol (bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), Hallo type dynamische versleuteling (bijvoorbeeld Common Encryption), PlayReady of Widevine-URL voor het verkrijgen van licentie.

    U kunt verschillende beleid tooeach protocol toepassen op Hallo dezelfde asset. U kunt bijvoorbeeld PlayReady-versleuteling tooSmooth/DASH en AES Envelope tooHLS toepassen. Alle protocollen die niet zijn gedefinieerd in een leveringsbeleid (bijvoorbeeld, u toevoegen één beleid waarmee alleen HLS als protocol Hallo) van streaming wordt geblokkeerd. Hallo uitzondering toothis is als u geen leveringsbeleid voor Assets helemaal gedefinieerd. Vervolgens zijn alle protocollen toegestaan in Hallo wissen.

6. Maak een OnDemand-locator in volgorde tooget een streaming-URL.

U ziet een voorbeeld van een volledige .NET achter Hallo Hallo onderwerp.

Hallo volgende afbeelding ziet u Hallo werkstroom die hierboven worden beschreven. Hallo-token wordt hier gebruikt voor verificatie.

![Beveiligen met PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

Hallo rest van dit onderwerp bevat gedetailleerde uitleg, codevoorbeelden en koppelingen tootopics waarin u kunt hoe tooachieve Hallo zien hierboven beschreven taken.

## <a name="current-limitations"></a>Huidige beperkingen
Als u toevoegen of bijwerken van een leveringsbeleid voor Assets, moet u verwijderen die zijn gekoppeld Hallo locator (indien aanwezig) en een nieuwe locator maken.

Momenteel kunnen bij het versleutelen met Widevine via Azure Media Services niet meerdere inhoudssleutels worden ondersteund.

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a>Maak een asset en upload bestanden in Hallo asset
In de volgorde toomanage, coderen en streamen video's, moet u eerst uw inhoud uploaden naar Microsoft Azure Media Services. Na het uploaden, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.

Zie [Upload Files into a Media Services account](media-services-dotnet-upload-files.md) (Bestanden uploaden naar een Media Services-account) voor gedetailleerde informatie.

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a>Hallo asset met Hallo bestand toohello adaptive bitrate die MP4-set coderen
Bij dynamische versleuteling hoeft u toocreate een asset die een set multi-bitrate MP4-bestanden of multi-bitrate Smooth Streaming-bronbestanden bevat. Vervolgens, op basis van de opgegeven indeling in het manifest Hallo Hallo en fragment aanvraag, Hallo On-Demand Streaming server zorgt ervoor dat u Hallo stream ontvangt in Hallo protocol dat u hebt gekozen. Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services-service bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client. Zie voor meer informatie, Hallo [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) onderwerp.

Voor instructies over het tooencode, Zie [hoe tooencode een asset met Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Maak een inhoudssleutel en deze koppelen aan Hallo gecodeerde asset
In Media Services bevat inhoudssleutel Hallo Hallo-sleutel die u een asset tooencrypt wilt met.

Zie [Create content key](media-services-dotnet-create-contentkey.md) (Inhoudssleutel maken) voor gedetailleerde informatie.

## <a id="configure_key_auth_policy"></a>Autorisatiebeleid Hallo de inhoudssleutel configureren
Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen. Hallo autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en voldaan door Hallo-client (speler) om Hallo sleutel toobe toohello client geleverd. Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: openen of tokenbeperking beperking.

Zie [Autorisatiebeleid voor inhoudssleutels configureren](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption) voor gedetailleerde informatie.

## <a id="configure_asset_delivery_policy"></a>Leveringsbeleid voor assets configureren
Configureer Hallo leveringsbeleid voor uw asset. Een aantal zaken die Hallo asset configuratie van een leveringsbeleid omvat:

* Hallo DRM URL voor het verkrijgen van licentie.
* Hallo asset leveringsprotocol (bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle).
* Hallo type dynamische versleuteling (in dit geval Common Encryption).

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

## <a name="create-and-configure-a-visual-studio-project"></a>Maak en configureer een Visual Studio-project.

1. Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md). 
2. Hallo elementen te volgen toevoegen**appSettings** gedefinieerd in het bestand app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld demonstreert de functionaliteit die is geïntroduceerd in Azure Media Services SDK voor .net-versie 3.5.2 (met name Hallo mogelijkheid toodefine een Widevine licentiëren sjabloon en een Widevine-licentie aangevraagd bij Azure Media Services).

Hallo-code in uw Program.cs-bestand met de Hallo-code die wordt weergegeven in deze sectie worden overschreven.

>[!NOTE]
>Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn). Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.

Zorg ervoor dat tooupdate variabelen toopoint toofolders waar uw invoerbestanden zich bevinden.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
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

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
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

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
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

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
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

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // hello following code configures PlayReady License Template using .NET classes
            // and returns hello XML string.

            //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user.
            //It contains a field for a custom data string between hello license server and hello application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // toobe returned toohello end users.
            //It contains hello data on hello content key in hello license and any rights or restrictions toobe
            //enforced by hello PlayReady DRM runtime when using hello content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether hello license is persistent (saved in persistent storage on hello client)
            //or non-persistent (only held in memory while hello player is using hello license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use hello license or not.  
            // If true, hello MinimumSecurityLevel property of hello license
            // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class.
            // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions
            // configured in hello license and on hello PlayRight itself (for playback specific policy).
            // Much of hello policy on hello PlayRight has toodo with output restrictions
            // which control hello types of outputs that hello content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if hello DigitalVideoOnlyContentRestriction is enabled,
            //then hello DRM runtime will only allow hello video toobe displayed over digital outputs
            //(analog video outputs won’t be allowed toopass hello content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience.
            // If hello output protections are configured too restrictive,
            // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
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


## <a name="next-step"></a>Volgende stap
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zie ook
[CENC met Multi-DRM en Toegangsbeheer](media-services-cenc-with-multidrm-access-control.md)

[Widevine-verpakking met AMS configureren](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[Google Widevine-services voor het leveren van licenties in Azure Media Services aankondigen](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
