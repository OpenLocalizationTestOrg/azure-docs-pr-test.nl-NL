---
title: beleid voor de levering van aaaConfigure asset met .NET SDK | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe beleid voor de levering van tooconfigure verschillende asset met Azure Media Services .NET SDK.
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>Beleid voor de levering asset configureren met .NET SDK
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>Overzicht
Als u van plan toodelivery versleuteld activa bent, stappen een Hallo Hallo Media Services content delivery werkstroom is leveringsbeleid voor assets configureren. Hallo-leveringsbeleid voor Assets wordt Media Services uitgelegd hoe u wilt voor uw asset toobe geleverd: in welke streaming protocol moet uw asset worden dynamisch verpakt (voor bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), al dan niet de gewenste toodynamically uw asset coderen en hoe (envelop of common encryption).

Dit onderwerp wordt beschreven waarom en hoe toocreate en beleid voor de levering asset configureren.

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 
>
>Bovendien toobe kunnen toouse dynamische pakketten en dynamische versleuteling uw asset moet bevatten een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden.


U kunt ook verschillende beleidsregels toohello toepassen dezelfde asset. U kunt bijvoorbeeld PlayReady-versleuteling tooSmooth Streaming en AES Envelope versleuteling tooMPEG toepassen DASH- en HLS. Alle protocollen die niet zijn gedefinieerd in een leveringsbeleid (bijvoorbeeld, u toevoegen één beleid waarmee alleen HLS als protocol Hallo) van streaming wordt geblokkeerd. Hallo uitzondering toothis is als u geen leveringsbeleid voor Assets helemaal gedefinieerd. Vervolgens zijn alle protocollen toegestaan in Hallo wissen.

Als u toodeliver een gecodeerde asset opslag wilt, moet u beleid voor de levering van Hallo actief configureren. Voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid voor. Bijvoorbeeld toodeliver uw asset versleuteld met Advanced Encryption Standard (AES) envelop versleutelingssleutel, stelt u het beleidstype hello te**DynamicEnvelopeEncryption**. versleuteling van opslag tooremove en stroom Hallo asset in Hallo wissen, stelt u Hallo beleidstype te**NoDynamicEncryption**. Voorbeelden van hoe tooconfigure deze beleidstypen volgen.

Afhankelijk van hoe u Hallo-leveringsbeleid voor Assets configureren die u zou kunnen toodynamically pakket worden dynamisch versleutelen en stream Hallo streaming protocollen te volgen: Smooth Streaming, HLS en MPEG DASH-streams.

Hallo volgende lijst bevat Hallo indelingen toostream Smooth, HLS en DASH te gebruiken.

Smooth Streaming:

{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest

HLS:

{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


## <a name="considerations"></a>Overwegingen
* U kunt een AssetDeliveryPolicy die zijn gekoppeld aan een asset, terwijl een (streaming) OnDemand-locator voor de activa bestaat niet verwijderen. Hallo-aanbeveling is tooremove Hallo beleid uit Hallo actief voordat Hallo beleid wordt verwijderd.
* Een streaming-locator kan niet worden gemaakt op een versleutelde actief opslag wanneer geen leveringsbeleid voor Assets is ingesteld.  Als Hallo Asset niet opslag versleuteld, kunt Hallo-systeem u een locator en stream Hallo-asset maken in Hallo wissen zonder een leveringsbeleid voor Assets.
* U kunt meerdere asset levering beleidsregels die zijn gekoppeld aan één element hebben maar u kunt alleen eenrichtingssessie toohandle een bepaalde AssetDeliveryProtocol opgeven.  Dit betekent dat als u toolink twee leveringsbeleid die Hallo AssetDeliveryProtocol.SmoothStreaming protocol die resulteren in een fout opgetreden probeert opgeeft omdat Hallo systeem welke niet weet u dat wilt tooapply wanneer een client een Smooth Streaming-aanvraag indient.
* Als u een asset met een bestaande streaming-locator hebt, kunt u een nieuw beleid toohello activum (u kunt ontkoppelen van een bestaand beleid uit Hallo actief of bijwerken van een leveringsbeleid die zijn gekoppeld aan asset Hallo) niet koppelen.  U eerst tooremove Hallo streaming-locator hebben, Hallo beleid aanpassen en streaming-locator Hallo opnieuw maken.  U kunt Hallo dezelfde locatorId wanneer u opnieuw Hallo streaming maakt-locator, maar u moet ervoor zorgen dat niet toe leiden problemen voor clients dat omdat inhoud kan worden in het cachegeheugen van de oorsprong hello of een downstream CDN gebruiken.

## <a name="clear-asset-delivery-policy"></a>Leveringsbeleid voor Assets wissen

Hallo volgende **ConfigureClearAssetDeliveryPolicy** methode specificeert toonot toepassen dynamische versleuteling en toodeliver Hallo stream in een van volgende Hallo protocollen: MPEG DASH, HLS en Smooth Streaming-protocollen. U kunt dit beleid tooyour opslag versleuteld activa tooapply.

Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>DynamicCommonEncryption-leveringsbeleid voor Assets

Hallo volgende **CreateAssetDeliveryPolicy** methode maakt u Hallo **AssetDeliveryPolicy** die geconfigureerde tooapply dynamische common encryption (**DynamicCommonEncryption**) tooa smooth streaming-protocol (andere protocollen worden geblokkeerd van streaming). Hallo-methode heeft twee parameters: **Asset** (Hallo asset toowhich gewenste tooapply Hallo leveringsbeleid voor) en **IContentKey** (inhoudssleutel Hallo Hallo **CommonEncryption**type voor meer informatie, Zie: [maken van een inhoudssleutel](media-services-dotnet-create-contentkey.md#common_contentkey)).

Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

Azure Media Services kunt u ook tooadd Widevine-versleuteling. Hallo volgende voorbeeld bevat zowel PlayReady als Widevine toohello-leveringsbeleid voor Assets wordt toegevoegd.

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
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> Bij het versleutelen met Widevine, zou u alleen kunnen toodeliver met STREEPJES zijn. Zorg ervoor toospecify DASH in Hallo asset leveringsprotocol.
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>DynamicEnvelopeEncryption-leveringsbeleid voor Assets
Hallo volgende **CreateAssetDeliveryPolicy** methode maakt u Hallo **AssetDeliveryPolicy** die geconfigureerde tooapply dynamische versleuteling (**DynamicEnvelopeEncryption** ) tooSmooth-protocollen voor Streaming, HLS en STREEPJES (als u besluit toonot sommige protocollen opgeeft, worden ze streaming worden geblokkeerd). Hallo-methode heeft twee parameters: **Asset** (Hallo asset toowhich gewenste tooapply Hallo leveringsbeleid voor) en **IContentKey** (inhoudssleutel Hallo Hallo **EnvelopeEncryption**type voor meer informatie, Zie: [maken van een inhoudssleutel](media-services-dotnet-create-contentkey.md#envelope_contentkey)).

Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
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
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <a id="types"></a>Typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

Hallo beschrijft volgende enum waarden die u voor Hallo asset leveringsprotocol instellen kunt.

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType

Hallo beschrijft volgende enum waarden die u voor Hallo asset bezorgingstype beleid instellen kunt.  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType

Hallo beschrijft volgende enum waarden kunt u tooconfigure Hallo leveringsmethode van Hallo inhoud sleutel toohello client.
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }

### <a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey

Hallo na enum beschrijft waarden kunt u tooget specifieke configuratie van tooconfigure sleutels die worden gebruikt voor een leveringsbeleid voor Assets instellen.

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

