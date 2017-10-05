---
title: Beleid voor de levering asset configureren met .NET SDK | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe verschillende asset levering-beleid configureren met Azure Media Services .NET SDK.
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
ms.openlocfilehash: 282fd9e24dc147e31613469926128894d48366f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="ec8e8-103">Beleid voor de levering asset configureren met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ec8e8-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="ec8e8-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ec8e8-104">Overview</span></span>
<span data-ttu-id="ec8e8-105">Als u van plan om levering versleuteld activa bent, is een van de stappen in de werkstroom van Media Services leveren van inhoud leveringsbeleid voor assets configureren.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-105">If you plan to delivery encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="ec8e8-106">Het leveringsbeleid voor Assets wordt Media Services uitgelegd hoe u wilt voor uw asset moet worden geleverd: in welke streaming protocol moet uw asset worden dynamisch verpakt (voor bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), of u wilt uw asset dynamisch versleutelen of niet, en hoe (envelop of common encryption).</span><span class="sxs-lookup"><span data-stu-id="ec8e8-106">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="ec8e8-107">Dit onderwerp wordt beschreven waarom en hoe u kunt maken en configureren van beleid voor de levering asset.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-107">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="ec8e8-108">Wanneer uw AMS-account is gemaakt, wordt er een **standaardstreaming-eindpunt** met de status **Gestopt** toegevoegd aan uw account.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-108">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="ec8e8-109">Als u inhoud wilt streamen en gebruik wilt maken van dynamische pakketten en dynamische versleuteling, moet het streaming-eindpunt van waar u inhoud wilt streamen, de status **Wordt uitgevoerd** hebben.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-109">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="ec8e8-110">Uw asset moet ook om het gebruik van dynamische pakketten en dynamische versleuteling te kunnen bevatten een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-110">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="ec8e8-111">U kunt verschillende beleidsregels aan dezelfde activa toepassen.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-111">You could apply different policies to the same asset.</span></span> <span data-ttu-id="ec8e8-112">U kan bijvoorbeeld PlayReady-versleuteling toepassen op Smooth Streaming en AES Envelope versleuteling MPEG DASH en HLS.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-112">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="ec8e8-113">Alle protocollen die niet zijn gedefinieerd in een leveringsbeleid (u voegt bijvoorbeeld één beleid toe waarmee alleen HLS als protocol wordt opgegeven), worden voor streaming geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="ec8e8-114">De uitzondering hierop is als u helemaal geen leveringsbeleid voor assets hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-114">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="ec8e8-115">In dat geval is streaming voor alle protocollen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-115">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="ec8e8-116">Als u een gecodeerde asset opslag leveren wilt, moet u de asset leveringsbeleid voor configureren.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-116">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="ec8e8-117">Voordat uw asset kan worden gestreamd, wordt de streaming-server verwijdert u de versleuteling van opslag en uw inhoud met behulp van het opgegeven leveringsbeleid streams.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-117">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="ec8e8-118">Bijvoorbeeld, voor het leveren van uw asset is versleuteld met Advanced Encryption Standard (AES) envelop versleutelingssleutel, het beleidstype instellen op **DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-118">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="ec8e8-119">Stel wilt verwijderen van de versleuteling van opslag en de activa in de stream, het type beleid dat op **NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-119">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="ec8e8-120">Hier volgen voorbeelden die laten zien hoe deze beleidstypen configureren.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-120">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="ec8e8-121">Afhankelijk van hoe u het leveringsbeleid voor Assets configureren u zou kunnen dynamisch inpakken, dynamisch coderen en streamen van de volgende protocollen voor streaming: Smooth Streaming, HLS en MPEG DASH-streams.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-121">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="ec8e8-122">De volgende lijst bevat de indelingen waarmee u kunt Smooth, HLS en DASH stream.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-122">The following list shows the formats that you use to stream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="ec8e8-123">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="ec8e8-123">Smooth Streaming:</span></span>

<span data-ttu-id="ec8e8-124">{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="ec8e8-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="ec8e8-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="ec8e8-125">HLS:</span></span>

<span data-ttu-id="ec8e8-126">{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="ec8e8-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="ec8e8-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="ec8e8-127">MPEG DASH</span></span>

<span data-ttu-id="ec8e8-128">{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="ec8e8-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="ec8e8-129">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="ec8e8-129">Considerations</span></span>
* <span data-ttu-id="ec8e8-130">U kunt een AssetDeliveryPolicy die zijn gekoppeld aan een asset, terwijl een (streaming) OnDemand-locator voor de activa bestaat niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="ec8e8-131">De aanbeveling is het beleid uit de asset verwijderen voordat u het beleid wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="ec8e8-132">Een streaming-locator kan niet worden gemaakt op een versleutelde actief opslag wanneer geen leveringsbeleid voor Assets is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="ec8e8-133">Als de Asset niet versleuteld opslag, kunt het systeem u een locator te maken en te streamen van de activa in het wissen zonder een leveringsbeleid voor Assets.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="ec8e8-134">U kunt meerdere asset levering beleidsregels die zijn gekoppeld aan één element hebben, maar u kunt slechts één manier voor het verwerken van een bepaalde AssetDeliveryProtocol opgeven.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="ec8e8-135">Dit betekent dat als u probeert te koppelen van twee leveringsbeleid die het protocol AssetDeliveryProtocol.SmoothStreaming die in een fout opgetreden resulteren omdat het systeem die u wilt toepassen wanneer een client een aanvraag Smooth Streaming doet niet weet opgeeft.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="ec8e8-136">Als u een asset met een bestaande streaming-locator hebt, kunt u een nieuw beleid niet koppelen aan de asset (u kunt een bestaand beleid uit de asset ontkoppelen of bijwerken van een leveringsbeleid die zijn gekoppeld aan de asset).</span><span class="sxs-lookup"><span data-stu-id="ec8e8-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset (you can either unlink an existing policy from the asset, or update a delivery policy associated with the asset).</span></span>  <span data-ttu-id="ec8e8-137">U moet eerst de streaming-locator verwijderen, aanpassen van het beleid en de streaming-locator opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="ec8e8-138">U kunt de dezelfde locatorId gebruiken wanneer u de streaming-locator opnieuw, maar u ervoor dat niet toe leiden dat problemen voor clients zorgen moet omdat inhoud kan worden in het cachegeheugen van de oorsprong of een downstream CDN.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="ec8e8-139">Leveringsbeleid voor Assets wissen</span><span class="sxs-lookup"><span data-stu-id="ec8e8-139">Clear asset delivery policy</span></span>

<span data-ttu-id="ec8e8-140">De volgende **ConfigureClearAssetDeliveryPolicy** methode geeft aan dynamische versleuteling niet van toepassing en worden de stroom in een van de volgende protocollen leveren: MPEG DASH, HLS en Smooth Streaming-protocollen.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-140">The following **ConfigureClearAssetDeliveryPolicy** method specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="ec8e8-141">Mogelijk wilt dit beleid toepast op uw assets opslag versleuteld.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-141">You might want to apply this policy to your storage encrypted assets.</span></span>

<span data-ttu-id="ec8e8-142">Zie voor meer informatie over welke waarden die u kunt opgeven bij het maken van een AssetDeliveryPolicy de [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="ec8e8-143">DynamicCommonEncryption-leveringsbeleid voor Assets</span><span class="sxs-lookup"><span data-stu-id="ec8e8-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="ec8e8-144">De volgende **CreateAssetDeliveryPolicy** methode maakt u de **AssetDeliveryPolicy** die is geconfigureerd om toe te passen dynamic common encryption (**DynamicCommonEncryption**) naar een smooth streaming-protocol (andere protocollen worden geblokkeerd van streaming).</span><span class="sxs-lookup"><span data-stu-id="ec8e8-144">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to a smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="ec8e8-145">De methode heeft twee parameters: **Asset** (de asset die u wilt het leveringsbeleid toepassen) en **IContentKey** (de inhoudssleutel van de **CommonEncryption** type voor meer informatie, Zie: [maken van een inhoudssleutel](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="ec8e8-145">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="ec8e8-146">Zie voor meer informatie over welke waarden die u kunt opgeven bij het maken van een AssetDeliveryPolicy de [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

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
    
            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="ec8e8-147">Azure Media Services kunt u Widevine codering toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-147">Azure Media Services also enables you to add Widevine encryption.</span></span> <span data-ttu-id="ec8e8-148">Het volgende voorbeeld bevat zowel PlayReady als Widevine wordt toegevoegd aan het leveringsbeleid voor Assets.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-148">The following example demonstrates both PlayReady and Widevine being added to the asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get the PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // to append /? KID =< keyId > to the end of the url when creating the manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

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


        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="ec8e8-149">Bij het versleutelen met Widevine, zou u alleen leveren met STREEPJES zijn.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-149">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="ec8e8-150">Zorg ervoor dat u DASH asset levering-protocol.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-150">Make sure to specify DASH in the asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="ec8e8-151">DynamicEnvelopeEncryption-leveringsbeleid voor Assets</span><span class="sxs-lookup"><span data-stu-id="ec8e8-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="ec8e8-152">De volgende **CreateAssetDeliveryPolicy** methode maakt u de **AssetDeliveryPolicy** dat is geconfigureerd voor het toepassen van dynamische versleuteling (**DynamicEnvelopeEncryption**) in Smooth Streaming, HLS en DASH-protocollen (als u sommige protocollen niet opgeeft besluit, zullen zij streaming).</span><span class="sxs-lookup"><span data-stu-id="ec8e8-152">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to Smooth Streaming, HLS, and DASH protocols (if you decide to not specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="ec8e8-153">De methode heeft twee parameters: **Asset** (de asset die u wilt het leveringsbeleid toepassen) en **IContentKey** (de inhoudssleutel van de **EnvelopeEncryption** type Zie voor meer informatie: [maken van een inhoudssleutel](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="ec8e8-153">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="ec8e8-154">Zie voor meer informatie over welke waarden die u kunt opgeven bij het maken van een AssetDeliveryPolicy de [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get the Key Delivery Base Url by removing the Query parameter.  The Dynamic Encryption service will
        //  automatically add the correct key identifier to the url when it generates the Envelope encrypted content
        //  manifest.  Omitting the IV will also cause the Dynamice Encryption service to generate a deterministic
        //  IV for the content automatically.  By using the EnvelopeBaseKeyAcquisitionUrl and omitting the IV, this
        //  allows the AssetDelivery policy to be reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // The following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended to the envelope and
        //   the Initialization Vector (IV) to use for the envelope encryption.
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

        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="ec8e8-155"><a id="types"></a>Typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="ec8e8-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="ec8e8-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="ec8e8-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="ec8e8-157">De volgende enum beschrijft waarden die u voor het protocol van de levering van activa instellen kunt.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-157">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <span data-ttu-id="ec8e8-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="ec8e8-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="ec8e8-159">De volgende enum beschrijft waarden die u voor het beleidstype van asset-levering instellen kunt.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-159">The following enum describes values you can set for the asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// The Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption to the asset.
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

### <span data-ttu-id="ec8e8-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="ec8e8-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="ec8e8-161">De volgende enum beschrijft waarden die u gebruiken kunt voor het configureren van de leveringsmethode van de inhoudssleutel aan de client.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-161">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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

### <span data-ttu-id="ec8e8-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="ec8e8-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="ec8e8-163">De volgende enum beschrijft waarden die u instellen kunt op de sleutels die worden gebruikt om op te halen van specifieke configuratie van een leveringsbeleid voor Assets configureren.</span><span class="sxs-lookup"><span data-stu-id="ec8e8-163">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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
        /// The initialization vector to use for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// The PlayReady License Acquisition Url to use for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// The PlayReady Custom Attributes to add to the PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// The initialization vector to use for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="ec8e8-164">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="ec8e8-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ec8e8-165">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="ec8e8-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

