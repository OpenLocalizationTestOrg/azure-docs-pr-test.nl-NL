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
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="3cd85-105">Met behulp van dynamische AES-128-versleuteling en sleutellevering service</span><span class="sxs-lookup"><span data-stu-id="3cd85-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3cd85-106">.NET</span><span class="sxs-lookup"><span data-stu-id="3cd85-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="3cd85-107">Java</span><span class="sxs-lookup"><span data-stu-id="3cd85-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="3cd85-108">PHP</span><span class="sxs-lookup"><span data-stu-id="3cd85-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="3cd85-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3cd85-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="3cd85-110">Zie [dit](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video voor een overzicht van hoe tooprotect uw Media Content met AES-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="3cd85-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how tooprotect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="3cd85-111">Microsoft Azure Media Services kunt u toodeliver Http-Live-Streaming (HLS) en Smooth Streams versleuteld met Advanced Encryption Standard (AES) (met behulp van coderingssleutels 128-bits).</span><span class="sxs-lookup"><span data-stu-id="3cd85-111">Microsoft Azure Media Services enables you toodeliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="3cd85-112">Media Services biedt ook een service voor het leveren van de sleutel Hallo die zorgt voor versleuteling sleutels tooauthorized gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3cd85-112">Media Services also provides hello Key Delivery service that delivers encryption keys tooauthorized users.</span></span> <span data-ttu-id="3cd85-113">Als u voor Media Services tooencrypt een asset wilt, u moet een versleutelingssleutel met Hallo asset tooassociate en autorisatiebeleid voor Hallo sleutel ook configureren.</span><span class="sxs-lookup"><span data-stu-id="3cd85-113">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key with hello asset and also configure authorization policies for hello key.</span></span> <span data-ttu-id="3cd85-114">Wanneer een stream is aangevraagd door een speler, Media Services gebruikt Hallo opgegeven sleutel toodynamically versleutelen van uw inhoud met behulp van AES-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="3cd85-114">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="3cd85-115">toodecrypt hello stream, Hallo player vraagt de Hallo sleutel van Hallo sleutellevering-service.</span><span class="sxs-lookup"><span data-stu-id="3cd85-115">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="3cd85-116">toodecide of Hallo gebruiker is gemachtigd tooget Hallo sleutel, Hallo service beoordeelt Hallo autorisatiebeleid die u hebt opgegeven voor Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="3cd85-116">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="3cd85-117">Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3cd85-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="3cd85-118">Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: openen of tokenbeperking beperking.</span><span class="sxs-lookup"><span data-stu-id="3cd85-118">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="3cd85-119">Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="3cd85-119">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="3cd85-120">Media Services ondersteunt tokens in Hallo [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) -indeling (SWT) en [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT)-indeling.</span><span class="sxs-lookup"><span data-stu-id="3cd85-120">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="3cd85-121">Zie voor meer informatie [autorisatiebeleid Hallo de inhoudssleutel configureren](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="3cd85-121">For more information, see [Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="3cd85-122">tootake profiteren van dynamische versleuteling hoeft u toohave een asset die een set multi-bitrate MP4-bestanden of multi-bitrate Smooth Streaming-bronbestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="3cd85-122">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="3cd85-123">U moet ook tooconfigure Hallo leveringsbeleid voor Hallo asset (Zie verderop in dit onderwerp).</span><span class="sxs-lookup"><span data-stu-id="3cd85-123">You also need tooconfigure hello delivery policy for hello asset (described later in this topic).</span></span> <span data-ttu-id="3cd85-124">Vervolgens, op basis van opgegeven in de streaming-URL Hallo Hallo-indeling, Hallo On-Demand Streaming server zorgt ervoor dat Hallo-stream wordt geleverd in Hallo protocol dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="3cd85-124">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="3cd85-125">Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services-service bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client.</span><span class="sxs-lookup"><span data-stu-id="3cd85-125">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="3cd85-126">In dit onderwerp is nuttig toodevelopers die werken aan toepassingen die beveiligde media leveren.</span><span class="sxs-lookup"><span data-stu-id="3cd85-126">This topic would be useful toodevelopers that work on applications that deliver protected media.</span></span> <span data-ttu-id="3cd85-127">Hallo onderwerp leest u hoe tooconfigure sleutellevering service met een autorisatiebeleid Hallo zodat alleen geautoriseerde clients Hallo versleutelingssleutels kunnen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3cd85-127">hello topic shows you how tooconfigure hello key delivery service with authorization policies so that only authorized clients could receive hello encryption keys.</span></span> <span data-ttu-id="3cd85-128">U ziet ook hoe toouse dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="3cd85-128">It also shows how toouse dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="3cd85-129">Sleutellevering servicewerkstroom en dynamische AES-128-versleuteling</span><span class="sxs-lookup"><span data-stu-id="3cd85-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="3cd85-130">Hallo hieronder vindt u algemene stappen zou u tooperform moet bij het versleutelen van uw assets met AES, met behulp van Hallo Media Services sleutellevering service en dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="3cd85-130">hello following are general steps that you would need tooperform when encrypting your assets with AES, using hello Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="3cd85-131">[Maak een asset en upload bestanden in Hallo asset](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="3cd85-131">[Create an asset and upload files into hello asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="3cd85-132">[Hallo asset met Hallo bestand toohello adaptive bitrate MP4-set coderen](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="3cd85-132">[Encode hello asset containing hello file toohello adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="3cd85-133">[Maak een inhoudssleutel en deze koppelen aan Hallo gecodeerde asset](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="3cd85-133">[Create a content key and associate it with hello encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="3cd85-134">Hallo inhoudssleutel bevat in Media Services de versleutelingssleutel van Hallo actief.</span><span class="sxs-lookup"><span data-stu-id="3cd85-134">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="3cd85-135">[Hallo de inhoudssleutel verificatiebeleid configureren](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="3cd85-135">[Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="3cd85-136">Hallo autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en door de client Hallo Hallo inhoud sleutel toobe geleverde toohello client zodat wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="3cd85-136">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>
5. <span data-ttu-id="3cd85-137">[Configureer het leveringsbeleid Hallo voor een asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="3cd85-137">[Configure hello delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="3cd85-138">Hallo levering-beleidsconfiguratie omvat:-URL voor het verkrijgen en initialisatie-Vector (IV) (AES 128 vereist Hallo dezelfde IV toobe opgegeven bij het versleutelen en ontsleutelen), leveringsprotocol (bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), Hallo type dynamische versleuteling (bijvoorbeeld envelop of er geen dynamische versleuteling).</span><span class="sxs-lookup"><span data-stu-id="3cd85-138">hello delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires hello same IV toobe supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="3cd85-139">U kunt verschillende beleid tooeach protocol toepassen op Hallo dezelfde asset.</span><span class="sxs-lookup"><span data-stu-id="3cd85-139">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="3cd85-140">U kunt bijvoorbeeld PlayReady-versleuteling tooSmooth/DASH en AES Envelope tooHLS toepassen.</span><span class="sxs-lookup"><span data-stu-id="3cd85-140">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="3cd85-141">Alle protocollen die niet zijn gedefinieerd in een leveringsbeleid (bijvoorbeeld, u toevoegen één beleid waarmee alleen HLS als protocol Hallo) van streaming wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="3cd85-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="3cd85-142">Hallo uitzondering toothis is als u geen leveringsbeleid voor Assets helemaal gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="3cd85-142">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="3cd85-143">Vervolgens zijn alle protocollen toegestaan in Hallo wissen.</span><span class="sxs-lookup"><span data-stu-id="3cd85-143">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="3cd85-144">[Maak een OnDemand-locator](media-services-protect-with-aes128.md#create_locator) in volgorde tooget een streaming-URL.</span><span class="sxs-lookup"><span data-stu-id="3cd85-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order tooget a streaming URL.</span></span>

<span data-ttu-id="3cd85-145">Hallo-onderwerp bevat ook [hoe een clienttoepassing kan aanvragen voor een sleutel van Hallo sleutellevering service](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="3cd85-145">hello topic also shows [how a client application can request a key from hello key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="3cd85-146">Vindt u een volledige .NET [voorbeeld](media-services-protect-with-aes128.md#example) achter Hallo Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="3cd85-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at hello end of hello topic.</span></span>

<span data-ttu-id="3cd85-147">Hallo volgende afbeelding ziet u Hallo werkstroom die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="3cd85-147">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="3cd85-148">Hallo-token wordt hier gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="3cd85-148">Here hello token is used for authentication.</span></span>

![Beschermen met AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="3cd85-150">Hallo rest van dit onderwerp bevat gedetailleerde uitleg, codevoorbeelden en koppelingen tootopics waarin u kunt hoe tooachieve Hallo zien hierboven beschreven taken.</span><span class="sxs-lookup"><span data-stu-id="3cd85-150">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="3cd85-151">Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="3cd85-151">Current limitations</span></span>
<span data-ttu-id="3cd85-152">Als u het leveringsbeleid voor uw asset toevoegt of bijwerkt, moet u een bestaande locator (indien aanwezig) verwijderen en een nieuwe locator maken.</span><span class="sxs-lookup"><span data-stu-id="3cd85-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="3cd85-153"><a id="create_asset"></a>Maak een asset en upload bestanden in Hallo asset</span><span class="sxs-lookup"><span data-stu-id="3cd85-153"><a id="create_asset"></a>Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="3cd85-154">In de volgorde toomanage, coderen en streamen video's, moet u eerst uw inhoud uploaden naar Microsoft Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="3cd85-154">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="3cd85-155">Na het uploaden, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="3cd85-155">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

<span data-ttu-id="3cd85-156">Zie [Upload Files into a Media Services account](media-services-dotnet-upload-files.md) (Bestanden uploaden naar een Media Services-account) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="3cd85-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="3cd85-157"><a id="encode_asset"></a>Hallo asset met Hallo bestand toohello adaptive bitrate die MP4-set coderen</span><span class="sxs-lookup"><span data-stu-id="3cd85-157"><a id="encode_asset"></a>Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="3cd85-158">Bij dynamische versleuteling hoeft u toocreate een asset die een set multi-bitrate MP4-bestanden of multi-bitrate Smooth Streaming-bronbestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="3cd85-158">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="3cd85-159">Vervolgens, op basis van de opgegeven indeling in het manifest Hallo Hallo of fragment aanvraag, Hallo On-Demand Streaming server zorgt ervoor dat u Hallo stream ontvangt in Hallo protocol dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="3cd85-159">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="3cd85-160">Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services-service bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client.</span><span class="sxs-lookup"><span data-stu-id="3cd85-160">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="3cd85-161">Zie voor meer informatie, Hallo [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="3cd85-161">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="3cd85-162">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="3cd85-162">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="3cd85-163">uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="3cd85-163">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="3cd85-164">Bovendien toobe kunnen toouse dynamische pakketten en dynamische versleuteling uw asset moet bevatten een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden.</span><span class="sxs-lookup"><span data-stu-id="3cd85-164">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="3cd85-165">Voor instructies over het tooencode, Zie [hoe tooencode een asset met Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="3cd85-165">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="3cd85-166"><a id="create_contentkey"></a>Maak een inhoudssleutel en deze koppelen aan Hallo gecodeerde asset</span><span class="sxs-lookup"><span data-stu-id="3cd85-166"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="3cd85-167">In Media Services bevat inhoudssleutel Hallo Hallo-sleutel die u een asset tooencrypt wilt met.</span><span class="sxs-lookup"><span data-stu-id="3cd85-167">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="3cd85-168">Zie [Create content key](media-services-dotnet-create-contentkey.md) (Inhoudssleutel maken) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="3cd85-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="3cd85-169"><a id="configure_key_auth_policy"></a>Autorisatiebeleid Hallo de inhoudssleutel configureren</span><span class="sxs-lookup"><span data-stu-id="3cd85-169"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="3cd85-170">Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3cd85-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="3cd85-171">Hallo autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en voldaan door Hallo-client (speler) om Hallo sleutel toobe toohello client geleverd.</span><span class="sxs-lookup"><span data-stu-id="3cd85-171">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="3cd85-172">Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: open, token beperking of IP-beperking.</span><span class="sxs-lookup"><span data-stu-id="3cd85-172">hello content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="3cd85-173">Zie [Autorisatiebeleid voor inhoudssleutels configureren](media-services-dotnet-configure-content-key-auth-policy.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="3cd85-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="3cd85-174"><a id="configure_asset_delivery_policy"></a>Leveringsbeleid voor assets configureren</span><span class="sxs-lookup"><span data-stu-id="3cd85-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="3cd85-175">Configureer Hallo leveringsbeleid voor uw asset.</span><span class="sxs-lookup"><span data-stu-id="3cd85-175">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="3cd85-176">Een aantal zaken die Hallo asset configuratie van een leveringsbeleid omvat:</span><span class="sxs-lookup"><span data-stu-id="3cd85-176">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="3cd85-177">Hallo-URL voor het verkrijgen van sleutel.</span><span class="sxs-lookup"><span data-stu-id="3cd85-177">hello Key acquisition URL.</span></span> 
* <span data-ttu-id="3cd85-178">Hallo initialisatie Vector (IV) toouse voor Hallo envelop versleuteling.</span><span class="sxs-lookup"><span data-stu-id="3cd85-178">hello Initialization Vector (IV) toouse for hello envelope encryption.</span></span> <span data-ttu-id="3cd85-179">AES-128 vereist Hallo dezelfde IV toobe opgegeven bij het versleutelen en ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="3cd85-179">AES 128 requires hello same IV toobe supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="3cd85-180">Hallo asset leveringsprotocol (bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle).</span><span class="sxs-lookup"><span data-stu-id="3cd85-180">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="3cd85-181">Hallo type dynamische versleuteling (bijvoorbeeld AES envelope) of er geen dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="3cd85-181">hello type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="3cd85-182">Zie [Leveringsbeleid voor assets configureren](media-services-rest-configure-asset-delivery-policy.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="3cd85-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="3cd85-183"><a id="create_locator"></a>Maak een OnDemand-streaminglocator in volgorde tooget een streaming-URL</span><span class="sxs-lookup"><span data-stu-id="3cd85-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="3cd85-184">U moet tooprovide uw gebruiker Hello streaming-URL voor Smooth, DASH of HLS.</span><span class="sxs-lookup"><span data-stu-id="3cd85-184">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="3cd85-185">Als u het leveringsbeleid voor uw asset toevoegt of bijwerkt, moet u een bestaande locator (indien aanwezig) verwijderen en een nieuwe locator maken.</span><span class="sxs-lookup"><span data-stu-id="3cd85-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="3cd85-186">Voor instructies over hoe toopublish een asset en bouwen van een streaming-URL, Zie [bouwen van een streaming-URL](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="3cd85-186">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="3cd85-187">Een test-token ophalen</span><span class="sxs-lookup"><span data-stu-id="3cd85-187">Get a test token</span></span>
<span data-ttu-id="3cd85-188">Een test-token ophalen op basis van de tokenbeperking Hallo die werd gebruikt voor het sleutelautorisatiebeleid Hallo.</span><span class="sxs-lookup"><span data-stu-id="3cd85-188">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="3cd85-189">U kunt Hallo [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest uw stream.</span><span class="sxs-lookup"><span data-stu-id="3cd85-189">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <span data-ttu-id="3cd85-190"><a id="client_request"></a>Hoe kan de client een sleutel van Hallo sleutellevering service aanvragen?</span><span class="sxs-lookup"><span data-stu-id="3cd85-190"><a id="client_request"></a>How can your client request a key from hello key delivery service?</span></span>
<span data-ttu-id="3cd85-191">In de vorige stap hello, moet u Hallo-URL die tooa manifestbestand verwijst samengesteld.</span><span class="sxs-lookup"><span data-stu-id="3cd85-191">In hello previous step, you constructed hello URL that points tooa manifest file.</span></span> <span data-ttu-id="3cd85-192">De client moet tooextract Hallo benodigde gegevens van de manifest-bestanden in de volgorde toomake een aanvraag toohello sleutellevering service streaming Hallo.</span><span class="sxs-lookup"><span data-stu-id="3cd85-192">Your client needs tooextract hello necessary information from hello streaming manifest files in order toomake a request toohello key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="3cd85-193">Manifestbestanden</span><span class="sxs-lookup"><span data-stu-id="3cd85-193">Manifest files</span></span>
<span data-ttu-id="3cd85-194">Hallo client tooextract Hallo URL (dat ook bevat inhoudssleutel Id (kid)) moet de waarde van het manifestbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="3cd85-194">hello client needs tooextract hello URL (that also contains content key Id (kid)) value from hello manifest file.</span></span> <span data-ttu-id="3cd85-195">Hallo-client wordt en probeer het tooget Hallo versleutelingssleutel van Hallo sleutellevering-service.</span><span class="sxs-lookup"><span data-stu-id="3cd85-195">hello client will then try tooget hello encryption key from hello key delivery service.</span></span> <span data-ttu-id="3cd85-196">Hallo client moet ook tooextract Hallo IV waarde en gebruik het Hallo stream.hello volgende codefragment ontsleutelen toont Hallo <Protection> element van Hallo Smooth Streaming manifest.</span><span class="sxs-lookup"><span data-stu-id="3cd85-196">hello client also needs tooextract hello IV value and use it do decrypt hello stream.hello following snippet shows hello <Protection> element of hello Smooth Streaming manifest.</span></span>

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

<span data-ttu-id="3cd85-197">In geval van HLS Hallo is Hallo hoofdmap manifest onderverdeeld in segment bestanden.</span><span class="sxs-lookup"><span data-stu-id="3cd85-197">In hello case of HLS, hello root manifest is broken into segment files.</span></span> 

<span data-ttu-id="3cd85-198">Hallo hoofdmap manifest is bijvoorbeeld: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) en het bevat een lijst met bestandsnamen segment.</span><span class="sxs-lookup"><span data-stu-id="3cd85-198">For example, hello root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="3cd85-199">Als u een van Hallo segment bestanden in de teksteditor (bijvoorbeeld http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should openen bevatten #EXT-X-sleutel, waarmee wordt aangegeven dat Hallo-bestand is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="3cd85-199">If you open one of hello segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that hello file is encrypted.</span></span>

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
><span data-ttu-id="3cd85-200">Als u van plan bent tooplay een AES HLS in Safari versleuteld, Zie [deze blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="3cd85-200">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-hello-key-from-hello-key-delivery-service"></a><span data-ttu-id="3cd85-201">Hallo-sleutel van Hallo sleutellevering service aanvragen</span><span class="sxs-lookup"><span data-stu-id="3cd85-201">Request hello key from hello key delivery service</span></span>

<span data-ttu-id="3cd85-202">Hallo volgende code toont hoe toosend een aanvraag toohello Media Services sleutel service voor het leveren met behulp van een sleutel levering Uri (dat is opgehaald uit Hallo manifest) en een token (in dit onderwerp spreekt niet over hoe tooget Simple Web Tokens uit een Secure Token Service).</span><span class="sxs-lookup"><span data-stu-id="3cd85-202">hello following code shows how toosend a request toohello Media Services key delivery service using a key delivery Uri (that was extracted from hello manifest) and a token (this topic does not talk about how tooget Simple Web Tokens from a Secure Token Service).</span></span>

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

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="3cd85-203">De inhoud beveiligen met AES-128 met .NET</span><span class="sxs-lookup"><span data-stu-id="3cd85-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3cd85-204">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="3cd85-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="3cd85-205">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3cd85-205">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="3cd85-206">Hallo elementen te volgen toevoegen**appSettings** gedefinieerd in het bestand app.config:</span><span class="sxs-lookup"><span data-stu-id="3cd85-206">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="3cd85-207"><a id="example"></a>Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3cd85-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="3cd85-208">Hallo-code in uw Program.cs-bestand met de Hallo-code die wordt weergegeven in deze sectie worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="3cd85-208">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="3cd85-209">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="3cd85-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="3cd85-210">Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn).</span><span class="sxs-lookup"><span data-stu-id="3cd85-210">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="3cd85-211">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3cd85-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="3cd85-212">Zorg ervoor dat tooupdate variabelen toopoint toofolders waar uw invoerbestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="3cd85-212">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="3cd85-213">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="3cd85-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3cd85-214">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="3cd85-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

