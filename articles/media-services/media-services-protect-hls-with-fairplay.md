---
title: aaaProtect HLS inhoud met Microsoft PlayReady of Apple FairPlay - Azure | Microsoft Docs
description: Dit onderwerp een overzicht en ziet u hoe toouse Azure Media Services toodynamically uw HTTP Live Streaming (HLS)-inhoud met Apple FairPlay coderen. U ziet ook hoe toouse Hallo Media Services leveren service toodeliver FairPlay-licenties tooclients licentie.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Beveiligen van uw inhoud met Apple FairPlay of Microsoft PlayReady HLS
Azure Media Services kunt u toodynamically versleutelen uw HTTP Live Streaming (HLS)-inhoud met behulp van Hallo volgende indelingen:  

* **De lege sleutel envelop voor AES-128**

    Hallo gehele chunk is versleuteld met Hallo **AES-128 CBC** modus. Hallo-ontsleuteling van Hallo stroom wordt ondersteund door iOS en OS X-speler systeemeigen. Zie voor meer informatie [dynamische versleuteling met behulp van AES-128 en sleutellevering service](media-services-protect-with-aes128.md).
* **FairPlay van Apple**

    Hallo afzonderlijke video en audio-voorbeelden zijn versleuteld met behulp van Hallo **AES-128 CBC** modus. **FairPlay Streaming** (FPS) is geïntegreerd in Hallo besturingssystemen van apparaten, met systeemeigen ondersteuning op iOS- en Apple TV. Safari op OS X kunt FPS met behulp van de ondersteuning van de interface Hallo versleuteld Media extensies (EME).
* **Microsoft PlayReady**

Hallo volgende afbeelding toont Hallo **HLS + FairPlay of PlayReady dynamische versleuteling** werkstroom.

![Diagram van de dynamische versleuteling werkstroom](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

Dit onderwerp wordt beschreven hoe toouse Media Services toodynamically uw inhoud HLS met Apple FairPlay coderen. U ziet ook hoe toouse Hallo Media Services leveren service toodeliver FairPlay-licenties tooclients licentie.

> [!NOTE]
> Als u ook tooencrypt uw HLS inhoud met PlayReady wilt, u moet een algemene inhoudssleutel toocreate en deze koppelen aan uw asset. U moet ook tooconfigure Hallo voor de inhoudssleutel autorisatie, zoals beschreven in [PlayReady met behulp van dynamische algemene versleuteling](media-services-protect-with-drm.md).
>
>

## <a name="requirements-and-considerations"></a>Vereisten en overwegingen

Hallo volgende is vereist wanneer u Media Services toodeliver die HLS versleuteld met FairPlay en toodeliver FairPlay-licenties:

  * Een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) voor meer informatie.
  * Een Media Services-account. toocreate, Zie [een Azure Media Services-account maken met Azure-portal Hallo](media-services-portal-create-account.md).
  * Aanmelden bij [Apple Development Program](https://developer.apple.com/).
  * Apple vereist Hallo inhoudseigenaar tooobtain hello [implementatiepakket](https://developer.apple.com/contact/fps/). Staat u sleutel Security Module (KSM) met Media Services al geïmplementeerd en dat u Hallo laatste FPS pakket aanvraagt. Er zijn instructies in Hallo laatste FPS toogenerate certificeringsinstantie van het pakket en verkrijgen Hallo toepassing geheime sleutel (vraag). U vraag tooconfigure FairPlay gebruiken.
  * Azure Media Services .NET SDK versie **3.6.0** of hoger.

Hallo dingen volgende moet zijn ingesteld op Media Services sleutellevering kant:

  * **App-certificaat (AC)**: dit is een .pfx-bestand dat Hallo persoonlijke sleutel bevat. Dit bestand te maken en versleuteld met een wachtwoord.

       Wanneer u een sleutel leveringsbeleid configureert, moet u opgeven dat wachtwoord en Hallo pfx-bestand in Base64-indeling.

      Hallo stappen wordt beschreven hoe toogenerate een pfx-certificaat voor FairPlay bestand:

    1. OpenSSL van https://slproweb.com/products/Win32OpenSSL.html installeren.

        Ga toohello map Hallo FairPlay certificaat en andere bestanden die door Apple worden geleverd.
    2. Hallo volgende opdracht uit vanaf de opdrachtregel Hallo worden uitgevoerd. Dit converteert Hallo .cer-bestand tooa .pem-bestand.

        'C:\OpenSSL-Win32\bin\openssl.exe' x509-informeren der-in fairplay.cer-out fairplay out.pem
    3. Hallo volgende opdracht uit vanaf de opdrachtregel Hallo worden uitgevoerd. Dit converteert Hallo .pem-bestand tooa pfx-bestand met de persoonlijke sleutel Hallo. Hallo-wachtwoord voor Hallo pfx-bestand wordt vervolgens door OpenSSL gevraagd.

        'C:\OpenSSL-Win32\bin\openssl.exe' pkcs12-Exporteer - fairplay out.pfx-inkey privatekey.pem-in fairplay out.pem - passin file:privatekey-pem-pass.txt
  * **Certificaat van de App-wachtwoord**: Hallo wachtwoord voor het maken van Hallo pfx-bestand.
  * **App-Cert wachtwoord ID**: U moet uploaden Hallo wachtwoord, vergelijkbare toohow uploaden van andere sleutels Media Services. Gebruik Hallo **ContentKeyType.FairPlayPfxPassword** enum-waarde tooget Hallo Media Services-ID. Dit is wat ze moeten toouse binnen Hallo sleutellevering beleidsoptie.
  * **IV**: dit is een willekeurige waarde van 16 bytes. Moet overeenkomen met iv Hallo in Hallo-leveringsbeleid voor Assets. U genereert Hallo iv en plaatsen op beide plaatsen: Hallo-leveringsbeleid voor Assets en Hallo sleutellevering beleidsoptie.
  * **VRAAG**: deze sleutel wordt ontvangen bij het genereren van Hallo certificering met behulp van Hallo Apple Developer portal. Elke ontwikkelteam ontvangt een unieke vraag. Sla een kopie van Hallo vraag en sla deze op een veilige plaats. U moet tooconfigure vraag later als FairPlayAsk tooMedia Services.
  * **Vraag-ID**: deze ID wordt verkregen tijdens het uploaden van vraag in Media Services. U moet de vraag uploaden via Hallo **ContentKeyType.FairPlayAsk** enum-waarde. Hallo Media Services-ID wordt geretourneerd als resultaat Hallo en dit is wat moet worden gebruikt bij het instellen van Hallo sleutellevering beleidsoptie.

Hallo moeten volgende bewerkingen worden ingesteld door Hallo FPS clientzijde:

  * **App-certificaat (AC)**: dit is een.cer/.der-bestand dat Hallo openbare sleutel, welke Hallo-besturingssysteem tooencrypt gebruikt sommige nettolading bevat. Media Services moet tooknow erover omdat deze is vereist door Hallo player. Hallo sleutellevering service ontsleutelt met behulp van de bijbehorende persoonlijke sleutel Hallo.

een versleutelde gegevensstroom FairPlay back tooplay, een echte vraag eerste ophalen en vervolgens een echte certificaat genereren. Dit proces wordt gemaakt van alle drie onderdelen:

  * der-bestand
  * PFX-bestand
  * wachtwoord voor pfx Hallo

Hallo volgende clients ondersteunen HLS met **AES-128 CBC** versleuteling: Safari op OS X, Apple TV iOS.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>FairPlay dynamische versleuteling en licentie levering van services configureren
Hallo hieronder vindt u algemene stappen voor het beveiligen van uw assets met FairPlay met behulp van Hallo Media Services-licentieservice levering en met behulp van dynamische versleuteling.

1. Maak een asset en upload bestanden in Hallo asset.
2. Hallo asset met Hallo bestand toohello adaptive bitrate die MP4-set coderen.
3. Maak een inhoudssleutel en deze koppelen aan Hallo gecodeerde asset.  
4. Hallo de inhoudssleutel verificatiebeleid configureren. Hallo volgende opgeven:

   * Hallo leveringsmethode (in dit geval FairPlay).
   * FairPlay opties beleidsconfiguratie. Voor meer informatie over het tooconfigure FairPlay, Zie Hallo **ConfigureFairPlayPolicyOptions()** methode in Hallo voorbeeld hieronder.

     > [!NOTE]
     > Meestal kunt u opties voor tooconfigure FairPlay beleid slechts één keer omdat er slechts één set van een certificeringsinstantie en een vraag.
     >
     >
   * Beperkingen (openen of token).
   * Informatie specifieke toohello type sleutellevering waarmee wordt gedefinieerd hoe Hallo sleutel toohello client wordt geleverd.
5. Hallo-leveringsbeleid voor Assets configureren. configuratie van Hallo een leveringsbeleid omvat:

   * Hallo leveringsprotocol (HLS).
   * Hallo type dynamische versleuteling (algemene CBC versleuteling).
   * Hallo-URL voor het verkrijgen van licentie.

     > [!NOTE]
     > Als u wilt dat toodeliver een stroom die is versleuteld met FairPlay en een ander systeem voor beheer van digitale rechten (DRM), hebt u beleid voor de afzonderlijke levering tooconfigure:
     >
     > * Een IAssetDeliveryPolicy tooconfigure dynamische adaptief streamen via HTTP-(KOPPELTEKEN) met Common Encryption (CENC) (PlayReady en Widevine) en Smooth met PlayReady
     > * Een andere IAssetDeliveryPolicy tooconfigure FairPlay voor HLS
     >
     >
6. Maak een OnDemand-locator tooget een streaming-URL.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>FairPlay-sleutellevering door player apps gebruiken
U kunt player apps ontwikkelen met behulp van Hallo iOS SDK. toobe kunnen tooplay FairPlay inhoud, hebt u tooimplement Hallo licentie exchange-protocol. Dit protocol is niet opgegeven door Apple. Het is tooeach-app wordt ingesteld hoe toosend sleutellevering aanvragen. Hallo Media Services FairPlay sleutellevering service verwacht Hallo SPC toocome als een bericht www-form-url gecodeerde post in Hallo formulier te volgen:

    spc=<Base64 encoded SPC>

> [!NOTE]
> FairPlay afspelen out of box Hallo biedt geen ondersteuning voor Azure Media Player. Hallo voorbeeld player tooget FairPlay af te spelen op MAC OS X verkrijgen van Hallo Apple developer-account.
>
>

## <a name="streaming-urls"></a>Streaming-URL 's
Als uw asset is versleuteld met meer dan één DRM, moet u een tag versleuteling in Hallo streaming-URL: (format = 'm3u8-aapl', versleuteling = 'xxx').

Hallo overwegingen volgende van toepassing:

* Alleen nul of één versleutelingstype kan worden opgegeven.
* Hallo versleutelingstype heeft geen toobe opgegeven in Hallo URL als er slechts één versleuteling toegepaste toohello actief is.
* Hallo versleutelingstype is niet hoofdlettergevoelig.
* Hallo na versleutelingstypen kan worden opgegeven:  
  * **cenc**: Common encryption (PlayReady of Widevine)
  * **cbcs-aapl**: FairPlay
  * **CBC**: AES envelope-versleuteling

## <a name="create-and-configure-a-visual-studio-project"></a>Maak en configureer een Visual Studio-project.

1. Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md). 
2. Hallo elementen te volgen toevoegen**appSettings** gedefinieerd in het bestand app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld ziet u uw inhoud die is versleuteld met FairPlay Hallo mogelijkheid toouse toodeliver Media Services. Deze functionaliteit werd geïntroduceerd in hello Azure Media Services SDK voor .NET versie 3.6.0. 

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
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

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

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

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

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
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


## <a name="next-steps-media-services-learning-paths"></a>Volgende stappen: Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
