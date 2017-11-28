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
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="e7c1f-103">Beleid voor de levering asset configureren met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e7c1f-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="e7c1f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e7c1f-104">Overview</span></span>
<span data-ttu-id="e7c1f-105">Als u van plan toodelivery versleuteld activa bent, stappen een Hallo Hallo Media Services content delivery werkstroom is leveringsbeleid voor assets configureren.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-105">If you plan toodelivery encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="e7c1f-106">Hallo-leveringsbeleid voor Assets wordt Media Services uitgelegd hoe u wilt voor uw asset toobe geleverd: in welke streaming protocol moet uw asset worden dynamisch verpakt (voor bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), al dan niet de gewenste toodynamically uw asset coderen en hoe (envelop of common encryption).</span><span class="sxs-lookup"><span data-stu-id="e7c1f-106">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="e7c1f-107">Dit onderwerp wordt beschreven waarom en hoe toocreate en beleid voor de levering asset configureren.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-107">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="e7c1f-108">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-108">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="e7c1f-109">uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-109">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="e7c1f-110">Bovendien toobe kunnen toouse dynamische pakketten en dynamische versleuteling uw asset moet bevatten een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-110">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="e7c1f-111">U kunt ook verschillende beleidsregels toohello toepassen dezelfde asset.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-111">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="e7c1f-112">U kunt bijvoorbeeld PlayReady-versleuteling tooSmooth Streaming en AES Envelope versleuteling tooMPEG toepassen DASH- en HLS.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-112">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="e7c1f-113">Alle protocollen die niet zijn gedefinieerd in een leveringsbeleid (bijvoorbeeld, u toevoegen één beleid waarmee alleen HLS als protocol Hallo) van streaming wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="e7c1f-114">Hallo uitzondering toothis is als u geen leveringsbeleid voor Assets helemaal gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-114">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="e7c1f-115">Vervolgens zijn alle protocollen toegestaan in Hallo wissen.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-115">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="e7c1f-116">Als u toodeliver een gecodeerde asset opslag wilt, moet u beleid voor de levering van Hallo actief configureren.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-116">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="e7c1f-117">Voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid voor.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-117">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="e7c1f-118">Bijvoorbeeld toodeliver uw asset versleuteld met Advanced Encryption Standard (AES) envelop versleutelingssleutel, stelt u het beleidstype hello te**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-118">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="e7c1f-119">versleuteling van opslag tooremove en stroom Hallo asset in Hallo wissen, stelt u Hallo beleidstype te**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-119">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="e7c1f-120">Voorbeelden van hoe tooconfigure deze beleidstypen volgen.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-120">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="e7c1f-121">Afhankelijk van hoe u Hallo-leveringsbeleid voor Assets configureren die u zou kunnen toodynamically pakket worden dynamisch versleutelen en stream Hallo streaming protocollen te volgen: Smooth Streaming, HLS en MPEG DASH-streams.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-121">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="e7c1f-122">Hallo volgende lijst bevat Hallo indelingen toostream Smooth, HLS en DASH te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-122">hello following list shows hello formats that you use toostream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="e7c1f-123">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="e7c1f-123">Smooth Streaming:</span></span>

<span data-ttu-id="e7c1f-124">{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="e7c1f-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="e7c1f-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="e7c1f-125">HLS:</span></span>

<span data-ttu-id="e7c1f-126">{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="e7c1f-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="e7c1f-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="e7c1f-127">MPEG DASH</span></span>

<span data-ttu-id="e7c1f-128">{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="e7c1f-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="e7c1f-129">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="e7c1f-129">Considerations</span></span>
* <span data-ttu-id="e7c1f-130">U kunt een AssetDeliveryPolicy die zijn gekoppeld aan een asset, terwijl een (streaming) OnDemand-locator voor de activa bestaat niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="e7c1f-131">Hallo-aanbeveling is tooremove Hallo beleid uit Hallo actief voordat Hallo beleid wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="e7c1f-132">Een streaming-locator kan niet worden gemaakt op een versleutelde actief opslag wanneer geen leveringsbeleid voor Assets is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="e7c1f-133">Als Hallo Asset niet opslag versleuteld, kunt Hallo-systeem u een locator en stream Hallo-asset maken in Hallo wissen zonder een leveringsbeleid voor Assets.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="e7c1f-134">U kunt meerdere asset levering beleidsregels die zijn gekoppeld aan één element hebben maar u kunt alleen eenrichtingssessie toohandle een bepaalde AssetDeliveryProtocol opgeven.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="e7c1f-135">Dit betekent dat als u toolink twee leveringsbeleid die Hallo AssetDeliveryProtocol.SmoothStreaming protocol die resulteren in een fout opgetreden probeert opgeeft omdat Hallo systeem welke niet weet u dat wilt tooapply wanneer een client een Smooth Streaming-aanvraag indient.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="e7c1f-136">Als u een asset met een bestaande streaming-locator hebt, kunt u een nieuw beleid toohello activum (u kunt ontkoppelen van een bestaand beleid uit Hallo actief of bijwerken van een leveringsbeleid die zijn gekoppeld aan asset Hallo) niet koppelen.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset (you can either unlink an existing policy from hello asset, or update a delivery policy associated with hello asset).</span></span>  <span data-ttu-id="e7c1f-137">U eerst tooremove Hallo streaming-locator hebben, Hallo beleid aanpassen en streaming-locator Hallo opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="e7c1f-138">U kunt Hallo dezelfde locatorId wanneer u opnieuw Hallo streaming maakt-locator, maar u moet ervoor zorgen dat niet toe leiden problemen voor clients dat omdat inhoud kan worden in het cachegeheugen van de oorsprong hello of een downstream CDN gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="e7c1f-139">Leveringsbeleid voor Assets wissen</span><span class="sxs-lookup"><span data-stu-id="e7c1f-139">Clear asset delivery policy</span></span>

<span data-ttu-id="e7c1f-140">Hallo volgende **ConfigureClearAssetDeliveryPolicy** methode specificeert toonot toepassen dynamische versleuteling en toodeliver Hallo stream in een van volgende Hallo protocollen: MPEG DASH, HLS en Smooth Streaming-protocollen.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-140">hello following **ConfigureClearAssetDeliveryPolicy** method specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="e7c1f-141">U kunt dit beleid tooyour opslag versleuteld activa tooapply.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-141">You might want tooapply this policy tooyour storage encrypted assets.</span></span>

<span data-ttu-id="e7c1f-142">Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="e7c1f-143">DynamicCommonEncryption-leveringsbeleid voor Assets</span><span class="sxs-lookup"><span data-stu-id="e7c1f-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="e7c1f-144">Hallo volgende **CreateAssetDeliveryPolicy** methode maakt u Hallo **AssetDeliveryPolicy** die geconfigureerde tooapply dynamische common encryption (**DynamicCommonEncryption**) tooa smooth streaming-protocol (andere protocollen worden geblokkeerd van streaming).</span><span class="sxs-lookup"><span data-stu-id="e7c1f-144">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="e7c1f-145">Hallo-methode heeft twee parameters: **Asset** (Hallo asset toowhich gewenste tooapply Hallo leveringsbeleid voor) en **IContentKey** (inhoudssleutel Hallo Hallo **CommonEncryption**type voor meer informatie, Zie: [maken van een inhoudssleutel](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="e7c1f-145">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="e7c1f-146">Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

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

<span data-ttu-id="e7c1f-147">Azure Media Services kunt u ook tooadd Widevine-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-147">Azure Media Services also enables you tooadd Widevine encryption.</span></span> <span data-ttu-id="e7c1f-148">Hallo volgende voorbeeld bevat zowel PlayReady als Widevine toohello-leveringsbeleid voor Assets wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-148">hello following example demonstrates both PlayReady and Widevine being added toohello asset delivery policy.</span></span>

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
> <span data-ttu-id="e7c1f-149">Bij het versleutelen met Widevine, zou u alleen kunnen toodeliver met STREEPJES zijn.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-149">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="e7c1f-150">Zorg ervoor toospecify DASH in Hallo asset leveringsprotocol.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-150">Make sure toospecify DASH in hello asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="e7c1f-151">DynamicEnvelopeEncryption-leveringsbeleid voor Assets</span><span class="sxs-lookup"><span data-stu-id="e7c1f-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="e7c1f-152">Hallo volgende **CreateAssetDeliveryPolicy** methode maakt u Hallo **AssetDeliveryPolicy** die geconfigureerde tooapply dynamische versleuteling (**DynamicEnvelopeEncryption** ) tooSmooth-protocollen voor Streaming, HLS en STREEPJES (als u besluit toonot sommige protocollen opgeeft, worden ze streaming worden geblokkeerd).</span><span class="sxs-lookup"><span data-stu-id="e7c1f-152">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) tooSmooth Streaming, HLS, and DASH protocols (if you decide toonot specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="e7c1f-153">Hallo-methode heeft twee parameters: **Asset** (Hallo asset toowhich gewenste tooapply Hallo leveringsbeleid voor) en **IContentKey** (inhoudssleutel Hallo Hallo **EnvelopeEncryption**type voor meer informatie, Zie: [maken van een inhoudssleutel](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="e7c1f-153">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="e7c1f-154">Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

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


## <span data-ttu-id="e7c1f-155"><a id="types"></a>Typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="e7c1f-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="e7c1f-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="e7c1f-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="e7c1f-157">Hallo beschrijft volgende enum waarden die u voor Hallo asset leveringsprotocol instellen kunt.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-157">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <span data-ttu-id="e7c1f-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="e7c1f-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="e7c1f-159">Hallo beschrijft volgende enum waarden die u voor Hallo asset bezorgingstype beleid instellen kunt.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-159">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <span data-ttu-id="e7c1f-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="e7c1f-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="e7c1f-161">Hallo beschrijft volgende enum waarden kunt u tooconfigure Hallo leveringsmethode van Hallo inhoud sleutel toohello client.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-161">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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

### <span data-ttu-id="e7c1f-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="e7c1f-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="e7c1f-163">Hallo na enum beschrijft waarden kunt u tooget specifieke configuratie van tooconfigure sleutels die worden gebruikt voor een leveringsbeleid voor Assets instellen.</span><span class="sxs-lookup"><span data-stu-id="e7c1f-163">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="e7c1f-164">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="e7c1f-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e7c1f-165">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="e7c1f-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

