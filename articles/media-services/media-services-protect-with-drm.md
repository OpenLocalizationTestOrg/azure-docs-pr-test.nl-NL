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
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="d2c40-105">PlayReady en/of Widevine Dynamic Common Encryption gebruiken</span><span class="sxs-lookup"><span data-stu-id="d2c40-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2c40-106">.NET</span><span class="sxs-lookup"><span data-stu-id="d2c40-106">.NET</span></span>](media-services-protect-with-drm.md)
> * [<span data-ttu-id="d2c40-107">Java</span><span class="sxs-lookup"><span data-stu-id="d2c40-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="d2c40-108">PHP</span><span class="sxs-lookup"><span data-stu-id="d2c40-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="d2c40-109">Microsoft Azure Media Services kunt u toodeliver MPEG DASH, Smooth Streaming en beveiligd met HTTP-Live-Streaming (HLS)-streams [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="d2c40-109">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="d2c40-110">Ook kunt u DASH-streams toodeliver versleuteld met Widevine DRM-licenties.</span><span class="sxs-lookup"><span data-stu-id="d2c40-110">It also enables you toodeliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="d2c40-111">Zowel PlayReady als Widevine zijn versleuteld volgens de specificatie Common Encryption (ISO/IEC 23001-7 CENC) Hallo.</span><span class="sxs-lookup"><span data-stu-id="d2c40-111">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="d2c40-112">U kunt [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (te beginnen met Hallo versie 3.5.1) of REST-API tooconfigure uw AssetDeliveryConfiguration toouse Widevine.</span><span class="sxs-lookup"><span data-stu-id="d2c40-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with hello version 3.5.1) or REST API tooconfigure your AssetDeliveryConfiguration toouse Widevine.</span></span>

<span data-ttu-id="d2c40-113">Media Services voorziet in een service voor het leveren van PlayReady- en Widevine DRM-licenties.</span><span class="sxs-lookup"><span data-stu-id="d2c40-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="d2c40-114">Media Services biedt ook API's waarmee u Hallo rechten configureren en beperkingen voor Hallo PlayReady of Widevine DRM runtime tooenforce wanneer een gebruiker gewenste afspeelt beveiligde inhoud.</span><span class="sxs-lookup"><span data-stu-id="d2c40-114">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello PlayReady or Widevine DRM runtime tooenforce when a user plays back protected content.</span></span> <span data-ttu-id="d2c40-115">Wanneer een gebruiker DRM beveiligde inhoud aanvraagt, wordt de Hallo spelertoepassing een licentie aangevraagd bij Hallo AMS-licentieservice.</span><span class="sxs-lookup"><span data-stu-id="d2c40-115">When a user requests a DRM protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="d2c40-116">Hallo AMS-licentieservice verstrekt een licentie toohello player als dit is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d2c40-116">hello AMS license service will issue a license toohello player if it is authorized.</span></span> <span data-ttu-id="d2c40-117">Een PlayReady of Widevine-licentie bevat Hallo ontsleutelingssleutel die kan worden gebruikt door Hallo client player toodecrypt en stream Hallo-inhoud.</span><span class="sxs-lookup"><span data-stu-id="d2c40-117">A PlayReady or Widevine license contains hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="d2c40-118">U kunt ook Hallo AMS-partners toohelp u leveren met Widevine-licenties te volgen: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="d2c40-118">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="d2c40-119">Zie integratie met [Axinom](media-services-axinom-integration.md) en [castLabs](media-services-castlabs-integration.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d2c40-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="d2c40-120">Media Services ondersteunt meerdere manieren om gebruikers te autoriseren die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="d2c40-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="d2c40-121">Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: openen of tokenbeperking beperking.</span><span class="sxs-lookup"><span data-stu-id="d2c40-121">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="d2c40-122">Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="d2c40-122">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="d2c40-123">Media Services ondersteunt tokens in Hallo [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) -indeling (SWT) en [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT)-indeling.</span><span class="sxs-lookup"><span data-stu-id="d2c40-123">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="d2c40-124">Zie voor meer informatie verificatiebeleid configureren Hallo de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="d2c40-124">For more information, see Configure hello content key’s authorization policy.</span></span>

<span data-ttu-id="d2c40-125">tootake profiteren van dynamische versleuteling hoeft u toohave een asset die een set multi-bitrate MP4-bestanden of multi-bitrate Smooth Streaming-bronbestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="d2c40-125">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="d2c40-126">U moet ook tooconfigure Hallo leveringsbeleid voor Hallo asset (Zie verderop in dit onderwerp).</span><span class="sxs-lookup"><span data-stu-id="d2c40-126">You also need tooconfigure hello delivery policies for hello asset (described later in this topic).</span></span> <span data-ttu-id="d2c40-127">Vervolgens, op basis van opgegeven in de streaming-URL Hallo Hallo-indeling, Hallo On-Demand Streaming server zorgt ervoor dat Hallo-stream wordt geleverd in Hallo protocol dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="d2c40-127">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="d2c40-128">Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in een één opslagindeling en Media Services bouwt en levert de juiste HTTP-antwoord Hallo op basis van elke aanvraag van een client.</span><span class="sxs-lookup"><span data-stu-id="d2c40-128">As a result, you only need toostore and pay for hello files in a single storage format and Media Services will build and serve hello appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="d2c40-129">In dit onderwerp is nuttig toodevelopers die werken aan toepassingen die media die zijn beveiligd met meerdere DRM's, zoals PlayReady en Widevine leveren.</span><span class="sxs-lookup"><span data-stu-id="d2c40-129">This topic would be useful toodevelopers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="d2c40-130">Hallo onderwerp leest u hoe tooconfigure PlayReady-licentieservice levering met een autorisatiebeleid Hallo zodat alleen geautoriseerde clients PlayReady of Widevine-licenties kunnen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d2c40-130">hello topic shows you how tooconfigure hello PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="d2c40-131">U ziet ook hoe toouse dynamische versleuteling met PlayReady of Widevine DRM via DASH.</span><span class="sxs-lookup"><span data-stu-id="d2c40-131">It also shows how toouse dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
><span data-ttu-id="d2c40-132">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="d2c40-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d2c40-133">uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="d2c40-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

## <a name="download-sample"></a><span data-ttu-id="d2c40-134">Voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="d2c40-134">Download sample</span></span>
<span data-ttu-id="d2c40-135">U kunt downloaden Hallo voorbeeld beschreven in dit artikel [hier](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="d2c40-135">You can download hello sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="d2c40-136">Dynamic Common Encryption en DRM-services voor het leveren van licenties configureren</span><span class="sxs-lookup"><span data-stu-id="d2c40-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="d2c40-137">Hallo hieronder vindt u algemene stappen zou u tooperform moet bij het beveiligen van uw assets met PlayReady met Hallo Media Services-licentieservice levering en dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="d2c40-137">hello following are general steps that you would need tooperform when protecting your assets with PlayReady, using hello Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="d2c40-138">Maak een asset en upload bestanden in Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="d2c40-138">Create an asset and upload files into hello asset.</span></span>
2. <span data-ttu-id="d2c40-139">Hallo asset met Hallo bestand toohello adaptive bitrate die MP4-set coderen.</span><span class="sxs-lookup"><span data-stu-id="d2c40-139">Encode hello asset containing hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="d2c40-140">Maak een inhoudssleutel en deze koppelen aan Hallo gecodeerde asset.</span><span class="sxs-lookup"><span data-stu-id="d2c40-140">Create a content key and associate it with hello encoded asset.</span></span> <span data-ttu-id="d2c40-141">Hallo inhoudssleutel bevat in Media Services de versleutelingssleutel van Hallo actief.</span><span class="sxs-lookup"><span data-stu-id="d2c40-141">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="d2c40-142">Hallo de inhoudssleutel verificatiebeleid configureren.</span><span class="sxs-lookup"><span data-stu-id="d2c40-142">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="d2c40-143">Hallo autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en door de client Hallo Hallo inhoud sleutel toobe geleverde toohello client zodat wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="d2c40-143">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>

    <span data-ttu-id="d2c40-144">Wanneer u Hallo autorisatiebeleid voor inhoudssleutels maakt, hebt u toospecify Hallo volgende nodig: leveringsmethode (PlayReady of Widevine), beperkingen (openen of token) en informatie specifieke toohello type sleutellevering waarmee wordt gedefinieerd hoe Hallo-sleutel wordt geleverd toohello client ([PlayReady](media-services-playready-license-template-overview.md) of [Widevine](media-services-widevine-license-template-overview.md) licentiesjabloon).</span><span class="sxs-lookup"><span data-stu-id="d2c40-144">When creating hello content key authorization policy, you need toospecify hello following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific toohello key delivery type that defines how hello key is delivered toohello client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="d2c40-145">Configureer het leveringsbeleid Hallo voor een asset.</span><span class="sxs-lookup"><span data-stu-id="d2c40-145">Configure hello delivery policy for an asset.</span></span> <span data-ttu-id="d2c40-146">Hallo levering-beleidsconfiguratie omvat: leveringsprotocol (bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), Hallo type dynamische versleuteling (bijvoorbeeld Common Encryption), PlayReady of Widevine-URL voor het verkrijgen van licentie.</span><span class="sxs-lookup"><span data-stu-id="d2c40-146">hello delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="d2c40-147">U kunt verschillende beleid tooeach protocol toepassen op Hallo dezelfde asset.</span><span class="sxs-lookup"><span data-stu-id="d2c40-147">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="d2c40-148">U kunt bijvoorbeeld PlayReady-versleuteling tooSmooth/DASH en AES Envelope tooHLS toepassen.</span><span class="sxs-lookup"><span data-stu-id="d2c40-148">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="d2c40-149">Alle protocollen die niet zijn gedefinieerd in een leveringsbeleid (bijvoorbeeld, u toevoegen één beleid waarmee alleen HLS als protocol Hallo) van streaming wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="d2c40-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="d2c40-150">Hallo uitzondering toothis is als u geen leveringsbeleid voor Assets helemaal gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="d2c40-150">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="d2c40-151">Vervolgens zijn alle protocollen toegestaan in Hallo wissen.</span><span class="sxs-lookup"><span data-stu-id="d2c40-151">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="d2c40-152">Maak een OnDemand-locator in volgorde tooget een streaming-URL.</span><span class="sxs-lookup"><span data-stu-id="d2c40-152">Create an OnDemand locator in order tooget a streaming URL.</span></span>

<span data-ttu-id="d2c40-153">U ziet een voorbeeld van een volledige .NET achter Hallo Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="d2c40-153">You will find a complete .NET example at hello end of hello topic.</span></span>

<span data-ttu-id="d2c40-154">Hallo volgende afbeelding ziet u Hallo werkstroom die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="d2c40-154">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="d2c40-155">Hallo-token wordt hier gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="d2c40-155">Here hello token is used for authentication.</span></span>

![Beveiligen met PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="d2c40-157">Hallo rest van dit onderwerp bevat gedetailleerde uitleg, codevoorbeelden en koppelingen tootopics waarin u kunt hoe tooachieve Hallo zien hierboven beschreven taken.</span><span class="sxs-lookup"><span data-stu-id="d2c40-157">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="d2c40-158">Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="d2c40-158">Current limitations</span></span>
<span data-ttu-id="d2c40-159">Als u toevoegen of bijwerken van een leveringsbeleid voor Assets, moet u verwijderen die zijn gekoppeld Hallo locator (indien aanwezig) en een nieuwe locator maken.</span><span class="sxs-lookup"><span data-stu-id="d2c40-159">If you add or update an asset delivery policy, you must delete hello associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="d2c40-160">Momenteel kunnen bij het versleutelen met Widevine via Azure Media Services niet meerdere inhoudssleutels worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d2c40-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a><span data-ttu-id="d2c40-161">Maak een asset en upload bestanden in Hallo asset</span><span class="sxs-lookup"><span data-stu-id="d2c40-161">Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="d2c40-162">In de volgorde toomanage, coderen en streamen video's, moet u eerst uw inhoud uploaden naar Microsoft Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="d2c40-162">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="d2c40-163">Na het uploaden, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="d2c40-163">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="d2c40-164">Zie [Upload Files into a Media Services account](media-services-dotnet-upload-files.md) (Bestanden uploaden naar een Media Services-account) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="d2c40-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a><span data-ttu-id="d2c40-165">Hallo asset met Hallo bestand toohello adaptive bitrate die MP4-set coderen</span><span class="sxs-lookup"><span data-stu-id="d2c40-165">Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="d2c40-166">Bij dynamische versleuteling hoeft u toocreate een asset die een set multi-bitrate MP4-bestanden of multi-bitrate Smooth Streaming-bronbestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="d2c40-166">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="d2c40-167">Vervolgens, op basis van de opgegeven indeling in het manifest Hallo Hallo en fragment aanvraag, Hallo On-Demand Streaming server zorgt ervoor dat u Hallo stream ontvangt in Hallo protocol dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="d2c40-167">Then, based on hello specified format in hello manifest and fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="d2c40-168">Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services-service bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client.</span><span class="sxs-lookup"><span data-stu-id="d2c40-168">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="d2c40-169">Zie voor meer informatie, Hallo [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="d2c40-169">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="d2c40-170">Voor instructies over het tooencode, Zie [hoe tooencode een asset met Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="d2c40-170">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="d2c40-171"><a id="create_contentkey"></a>Maak een inhoudssleutel en deze koppelen aan Hallo gecodeerde asset</span><span class="sxs-lookup"><span data-stu-id="d2c40-171"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="d2c40-172">In Media Services bevat inhoudssleutel Hallo Hallo-sleutel die u een asset tooencrypt wilt met.</span><span class="sxs-lookup"><span data-stu-id="d2c40-172">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="d2c40-173">Zie [Create content key](media-services-dotnet-create-contentkey.md) (Inhoudssleutel maken) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="d2c40-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="d2c40-174"><a id="configure_key_auth_policy"></a>Autorisatiebeleid Hallo de inhoudssleutel configureren</span><span class="sxs-lookup"><span data-stu-id="d2c40-174"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="d2c40-175">Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="d2c40-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="d2c40-176">Hallo autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en voldaan door Hallo-client (speler) om Hallo sleutel toobe toohello client geleverd.</span><span class="sxs-lookup"><span data-stu-id="d2c40-176">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="d2c40-177">Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: openen of tokenbeperking beperking.</span><span class="sxs-lookup"><span data-stu-id="d2c40-177">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="d2c40-178">Zie [Autorisatiebeleid voor inhoudssleutels configureren](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="d2c40-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <span data-ttu-id="d2c40-179"><a id="configure_asset_delivery_policy"></a>Leveringsbeleid voor assets configureren</span><span class="sxs-lookup"><span data-stu-id="d2c40-179"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="d2c40-180">Configureer Hallo leveringsbeleid voor uw asset.</span><span class="sxs-lookup"><span data-stu-id="d2c40-180">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="d2c40-181">Een aantal zaken die Hallo asset configuratie van een leveringsbeleid omvat:</span><span class="sxs-lookup"><span data-stu-id="d2c40-181">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="d2c40-182">Hallo DRM URL voor het verkrijgen van licentie.</span><span class="sxs-lookup"><span data-stu-id="d2c40-182">hello DRM license acquisition URL.</span></span>
* <span data-ttu-id="d2c40-183">Hallo asset leveringsprotocol (bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle).</span><span class="sxs-lookup"><span data-stu-id="d2c40-183">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="d2c40-184">Hallo type dynamische versleuteling (in dit geval Common Encryption).</span><span class="sxs-lookup"><span data-stu-id="d2c40-184">hello type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="d2c40-185">Zie [Leveringsbeleid voor assets configureren](media-services-rest-configure-asset-delivery-policy.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="d2c40-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="d2c40-186"><a id="create_locator"></a>Maak een OnDemand-streaminglocator in volgorde tooget een streaming-URL</span><span class="sxs-lookup"><span data-stu-id="d2c40-186"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="d2c40-187">U moet tooprovide uw gebruiker Hello streaming-URL voor Smooth, DASH of HLS.</span><span class="sxs-lookup"><span data-stu-id="d2c40-187">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="d2c40-188">Als u het leveringsbeleid voor uw asset toevoegt of bijwerkt, moet u een bestaande locator (indien aanwezig) verwijderen en een nieuwe locator maken.</span><span class="sxs-lookup"><span data-stu-id="d2c40-188">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
>
>

<span data-ttu-id="d2c40-189">Voor instructies over hoe toopublish een asset en bouwen van een streaming-URL, Zie [bouwen van een streaming-URL](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="d2c40-189">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="d2c40-190">Een test-token ophalen</span><span class="sxs-lookup"><span data-stu-id="d2c40-190">Get a test token</span></span>
<span data-ttu-id="d2c40-191">Een test-token ophalen op basis van de tokenbeperking Hallo die werd gebruikt voor het sleutelautorisatiebeleid Hallo.</span><span class="sxs-lookup"><span data-stu-id="d2c40-191">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="d2c40-192">U kunt Hallo [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest uw stream.</span><span class="sxs-lookup"><span data-stu-id="d2c40-192">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d2c40-193">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="d2c40-193">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="d2c40-194">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d2c40-194">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="d2c40-195">Hallo elementen te volgen toevoegen**appSettings** gedefinieerd in het bestand app.config:</span><span class="sxs-lookup"><span data-stu-id="d2c40-195">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="d2c40-196">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d2c40-196">Example</span></span>

<span data-ttu-id="d2c40-197">Hallo volgende voorbeeld demonstreert de functionaliteit die is geïntroduceerd in Azure Media Services SDK voor .net-versie 3.5.2 (met name Hallo mogelijkheid toodefine een Widevine licentiëren sjabloon en een Widevine-licentie aangevraagd bij Azure Media Services).</span><span class="sxs-lookup"><span data-stu-id="d2c40-197">hello following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, hello ability toodefine a Widevine license template and request a Widevine license from Azure Media Services).</span></span>

<span data-ttu-id="d2c40-198">Hallo-code in uw Program.cs-bestand met de Hallo-code die wordt weergegeven in deze sectie worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="d2c40-198">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="d2c40-199">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="d2c40-199">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d2c40-200">Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn).</span><span class="sxs-lookup"><span data-stu-id="d2c40-200">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d2c40-201">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d2c40-201">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="d2c40-202">Zorg ervoor dat tooupdate variabelen toopoint toofolders waar uw invoerbestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="d2c40-202">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

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


## <a name="next-step"></a><span data-ttu-id="d2c40-203">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="d2c40-203">Next step</span></span>
<span data-ttu-id="d2c40-204">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="d2c40-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d2c40-205">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="d2c40-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d2c40-206">Zie ook</span><span class="sxs-lookup"><span data-stu-id="d2c40-206">See also</span></span>
[<span data-ttu-id="d2c40-207">CENC met Multi-DRM en Toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="d2c40-207">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="d2c40-208">Widevine-verpakking met AMS configureren</span><span class="sxs-lookup"><span data-stu-id="d2c40-208">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="d2c40-209">Google Widevine-services voor het leveren van licenties in Azure Media Services aankondigen</span><span class="sxs-lookup"><span data-stu-id="d2c40-209">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
