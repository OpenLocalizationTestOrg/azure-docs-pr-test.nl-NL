---
title: Met dynamische AES-128-versleuteling en sleutellevering service | Microsoft Docs
description: Microsoft Azure Media Services kunt u de inhoud die is versleuteld met AES-128-bits versleutelingssleutels bezorgen. Media Services biedt ook de service voor het leveren van de sleutel die zorgt voor versleutelingssleutels tot gemachtigde gebruikers. Dit onderwerp wordt beschreven hoe dynamisch versleutelen met AES-128 en de service sleutellevering te gebruiken.
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
ms.openlocfilehash: ae1b36c26e688e74eb8fcc1a4cdbd3be0c014c08
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="0c53c-105">Met behulp van dynamische AES-128-versleuteling en sleutellevering service</span><span class="sxs-lookup"><span data-stu-id="0c53c-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c53c-106">.NET</span><span class="sxs-lookup"><span data-stu-id="0c53c-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="0c53c-107">Java</span><span class="sxs-lookup"><span data-stu-id="0c53c-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="0c53c-108">PHP</span><span class="sxs-lookup"><span data-stu-id="0c53c-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="0c53c-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0c53c-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="0c53c-110">Zie [dit](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video voor een overzicht van het beveiligen van uw Media-inhoud met AES-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="0c53c-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how to protect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="0c53c-111">Microsoft Azure Media Services kunt u om Http-Live-Streaming (HLS) en Smooth Streams versleuteld met Advanced Encryption Standard (AES) (met behulp van coderingssleutels 128-bits) te leveren.</span><span class="sxs-lookup"><span data-stu-id="0c53c-111">Microsoft Azure Media Services enables you to deliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="0c53c-112">Media Services biedt ook de service voor het leveren van de sleutel die zorgt voor versleutelingssleutels tot gemachtigde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0c53c-112">Media Services also provides the Key Delivery service that delivers encryption keys to authorized users.</span></span> <span data-ttu-id="0c53c-113">Als u voor Media Services wilt voor het versleutelen van een asset, moet u een versleutelingssleutel koppelen aan de asset en ook autorisatiebeleid voor de sleutel te configureren.</span><span class="sxs-lookup"><span data-stu-id="0c53c-113">If you want for Media Services to encrypt an asset, you need to associate an encryption key with the asset and also configure authorization policies for the key.</span></span> <span data-ttu-id="0c53c-114">Wanneer een stream is aangevraagd door een speler, gebruikt Media Services de opgegeven sleutel voor het dynamisch versleutelen van uw inhoud met behulp van AES-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="0c53c-114">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="0c53c-115">Voor het ontsleutelen van de stroom, Windows media player vraagt om de sleutel van de service sleutellevering.</span><span class="sxs-lookup"><span data-stu-id="0c53c-115">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="0c53c-116">De service beoordeelt om te bepalen of de gebruiker is gemachtigd om op te halen van de sleutel, de autorisatie-beleidsregels die u hebt opgegeven voor de sleutel.</span><span class="sxs-lookup"><span data-stu-id="0c53c-116">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="0c53c-117">Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="0c53c-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="0c53c-118">Het autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: beperking voor openen of tokenbeperking.</span><span class="sxs-lookup"><span data-stu-id="0c53c-118">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="0c53c-119">Het beleid met de tokenbeperking moet vergezeld gaan van een token dat is uitgegeven door Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="0c53c-119">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="0c53c-120">Media Services ondersteunt tokens in de indelingen [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) en [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT).</span><span class="sxs-lookup"><span data-stu-id="0c53c-120">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="0c53c-121">Zie voor meer informatie [autorisatiebeleid voor de inhoudssleutel configureren](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="0c53c-121">For more information, see [Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="0c53c-122">Als u dynamische versleuteling wilt gebruiken, moet u een asset hebben die een set multi-bitrate MP4-bestanden of multi-bitrate Smooth Streaming-bronbestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="0c53c-122">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="0c53c-123">Ook moet u het leveringsbeleid voor de asset (Zie verderop in dit onderwerp) configureren.</span><span class="sxs-lookup"><span data-stu-id="0c53c-123">You also need to configure the delivery policy for the asset (described later in this topic).</span></span> <span data-ttu-id="0c53c-124">Vervolgens zorgt de server voor streaming on demand er op basis van de indeling die is opgegeven in de streaming-URL voor dat de stream wordt geleverd in het protocol dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="0c53c-124">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="0c53c-125">Hierdoor hoeft u voor slechts één opslagindeling de bestanden op te slaan en hiervoor te betalen. De Media Services-service bouwt en levert de juiste reactie op basis van aanvragen van een client.</span><span class="sxs-lookup"><span data-stu-id="0c53c-125">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="0c53c-126">In dit onderwerp is nuttig voor ontwikkelaars die werken aan toepassingen die beveiligde media leveren.</span><span class="sxs-lookup"><span data-stu-id="0c53c-126">This topic would be useful to developers that work on applications that deliver protected media.</span></span> <span data-ttu-id="0c53c-127">Het onderwerp leest u hoe de service sleutellevering met een autorisatiebeleid zodanig configureren dat alleen geautoriseerde clients de versleutelingssleutels kunnen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="0c53c-127">The topic shows you how to configure the key delivery service with authorization policies so that only authorized clients could receive the encryption keys.</span></span> <span data-ttu-id="0c53c-128">Ook ziet u hoe u dynamische versleuteling wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0c53c-128">It also shows how to use dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="0c53c-129">Sleutellevering servicewerkstroom en dynamische AES-128-versleuteling</span><span class="sxs-lookup"><span data-stu-id="0c53c-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="0c53c-130">Hieronder vindt u algemene stappen die u uitvoeren moet bij het versleutelen van uw assets met AES, met behulp van de Media Services-service sleutellevering en dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="0c53c-130">The following are general steps that you would need to perform when encrypting your assets with AES, using the Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="0c53c-131">[Maak een asset en upload bestanden in de asset](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="0c53c-131">[Create an asset and upload files into the asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="0c53c-132">[Codeer de asset met het bestand naar de adaptive bitrate MP4-set](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="0c53c-132">[Encode the asset containing the file to the adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="0c53c-133">[Maak een inhoudssleutel en deze koppelen aan de gecodeerde asset](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="0c53c-133">[Create a content key and associate it with the encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="0c53c-134">De inhoudssleutel bevat in Media Services de versleutelingssleutel van de asset.</span><span class="sxs-lookup"><span data-stu-id="0c53c-134">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="0c53c-135">[Autorisatiebeleid voor de inhoudssleutel configureren](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="0c53c-135">[Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="0c53c-136">U moet het autorisatiebeleid voor de inhoudssleutel hebben geconfigureerd en de client moet aan dit beleid voldoen om de inhoudssleutel aan de client te kunnen leveren.</span><span class="sxs-lookup"><span data-stu-id="0c53c-136">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>
5. <span data-ttu-id="0c53c-137">[Configureer het leveringsbeleid voor een asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="0c53c-137">[Configure the delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="0c53c-138">De configuratie van een leveringsbeleid omvat:-URL voor het verkrijgen en initialisatie-Vector (IV) (AES 128 vereist dat de dezelfde IV worden opgegeven bij het versleutelen en ontsleutelen), leveringsprotocol (bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), het type dynamische versleuteling (bijvoorbeeld envelop of er geen dynamische versleuteling).</span><span class="sxs-lookup"><span data-stu-id="0c53c-138">The delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires the same IV to be supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="0c53c-139">U kunt voor dezelfde asset een ander beleid voor elk protocol toepassen.</span><span class="sxs-lookup"><span data-stu-id="0c53c-139">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="0c53c-140">U kunt bijvoorbeeld PlayReady-versleuteling toepassen op Smooth/DASH en AES Envelope op HLS.</span><span class="sxs-lookup"><span data-stu-id="0c53c-140">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="0c53c-141">Alle protocollen die niet zijn gedefinieerd in een leveringsbeleid (u voegt bijvoorbeeld één beleid toe waarmee alleen HLS als protocol wordt opgegeven), worden voor streaming geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="0c53c-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="0c53c-142">De uitzondering hierop is als u helemaal geen leveringsbeleid voor assets hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="0c53c-142">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="0c53c-143">In dat geval is streaming voor alle protocollen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="0c53c-143">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="0c53c-144">[Maak een OnDemand-locator](media-services-protect-with-aes128.md#create_locator) om op te halen van een streaming-URL.</span><span class="sxs-lookup"><span data-stu-id="0c53c-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order to get a streaming URL.</span></span>

<span data-ttu-id="0c53c-145">Ook ziet u het onderwerp [hoe een clienttoepassing kan aanvragen voor een sleutel van de service sleutellevering](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="0c53c-145">The topic also shows [how a client application can request a key from the key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="0c53c-146">Vindt u een volledige .NET [voorbeeld](media-services-protect-with-aes128.md#example) aan het einde van het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="0c53c-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at the end of the topic.</span></span>

<span data-ttu-id="0c53c-147">De volgende afbeelding geeft een illustratie van de hierboven beschreven werkstroom.</span><span class="sxs-lookup"><span data-stu-id="0c53c-147">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="0c53c-148">Hier wordt het token gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="0c53c-148">Here the token is used for authentication.</span></span>

![Beschermen met AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="0c53c-150">De rest van dit onderwerp bevat gedetailleerde uitleg, codevoorbeelden en koppelingen naar onderwerpen waarin u ziet hoe u de hierboven beschreven taken kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0c53c-150">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="0c53c-151">Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="0c53c-151">Current limitations</span></span>
<span data-ttu-id="0c53c-152">Als u het leveringsbeleid voor uw asset toevoegt of bijwerkt, moet u een bestaande locator (indien aanwezig) verwijderen en een nieuwe locator maken.</span><span class="sxs-lookup"><span data-stu-id="0c53c-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="0c53c-153"><a id="create_asset"></a>Maak een asset en upload bestanden in de asset</span><span class="sxs-lookup"><span data-stu-id="0c53c-153"><a id="create_asset"></a>Create an asset and upload files into the asset</span></span>
<span data-ttu-id="0c53c-154">Als u uw video's wilt beheren, coderen en streamen, moet u eerst uw inhoud uploaden naar Microsoft Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="0c53c-154">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="0c53c-155">Uw inhoud wordt na het uploaden veilig opgeslagen in de cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="0c53c-155">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> 

<span data-ttu-id="0c53c-156">Zie [Upload Files into a Media Services account](media-services-dotnet-upload-files.md) (Bestanden uploaden naar een Media Services-account) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="0c53c-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="0c53c-157"><a id="encode_asset"></a>De asset met het bestand naar de adaptive bitrate die MP4-set coderen</span><span class="sxs-lookup"><span data-stu-id="0c53c-157"><a id="encode_asset"></a>Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="0c53c-158">Bij dynamische versleuteling hoeft u alleen maar een asset te maken die een set multi-bitrate MP4-bestanden of multi-bitrate Smooth Streaming-bronbestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="0c53c-158">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="0c53c-159">Klik, op basis van de opgegeven indeling de manifest- of fragmentdeel aanvraag, de On-Demand Streaming server zorgt ervoor dat u de stream ontvangt in het protocol dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="0c53c-159">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="0c53c-160">Hierdoor hoeft u voor slechts één opslagindeling de bestanden op te slaan en hiervoor te betalen. De Media Services-service bouwt en levert de juiste reactie op basis van aanvragen van een client.</span><span class="sxs-lookup"><span data-stu-id="0c53c-160">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="0c53c-161">Zie het onderwerp [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) (Overzicht van dynamische pakketten) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0c53c-161">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="0c53c-162">Wanneer uw AMS-account is gemaakt, wordt er een **standaardstreaming-eindpunt** met de status **Gestopt** toegevoegd aan uw account.</span><span class="sxs-lookup"><span data-stu-id="0c53c-162">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="0c53c-163">Als u inhoud wilt streamen en gebruik wilt maken van dynamische pakketten en dynamische versleuteling, moet het streaming-eindpunt van waar u inhoud wilt streamen, de status **Wordt uitgevoerd** hebben.</span><span class="sxs-lookup"><span data-stu-id="0c53c-163">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="0c53c-164">Uw asset moet ook om het gebruik van dynamische pakketten en dynamische versleuteling te kunnen bevatten een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden.</span><span class="sxs-lookup"><span data-stu-id="0c53c-164">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="0c53c-165">Zie [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) (Een asset coderen met Media Encoder Standard) voor instructies voor het coderen.</span><span class="sxs-lookup"><span data-stu-id="0c53c-165">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="0c53c-166"><a id="create_contentkey"></a>Een inhoudssleutel maken en deze koppelen aan de gecodeerde asset</span><span class="sxs-lookup"><span data-stu-id="0c53c-166"><a id="create_contentkey"></a>Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="0c53c-167">In Media Services bevat de inhoudssleutel de sleutel waarmee u een asset wilt coderen.</span><span class="sxs-lookup"><span data-stu-id="0c53c-167">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="0c53c-168">Zie [Create content key](media-services-dotnet-create-contentkey.md) (Inhoudssleutel maken) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="0c53c-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="0c53c-169"><a id="configure_key_auth_policy"></a>Het autorisatiebeleid voor de inhoudssleutel configureren</span><span class="sxs-lookup"><span data-stu-id="0c53c-169"><a id="configure_key_auth_policy"></a>Configure the content key’s authorization policy</span></span>
<span data-ttu-id="0c53c-170">Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="0c53c-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="0c53c-171">U moet het autorisatiebeleid voor inhoudssleutels hebben geconfigureerd en de client (speler) moet aan dit beleid voldoen om de sleutel aan de client te kunnen leveren.</span><span class="sxs-lookup"><span data-stu-id="0c53c-171">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="0c53c-172">Het autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: open, token beperking of IP-beperking.</span><span class="sxs-lookup"><span data-stu-id="0c53c-172">The content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="0c53c-173">Zie [Autorisatiebeleid voor inhoudssleutels configureren](media-services-dotnet-configure-content-key-auth-policy.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="0c53c-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="0c53c-174"><a id="configure_asset_delivery_policy"></a>Leveringsbeleid voor assets configureren</span><span class="sxs-lookup"><span data-stu-id="0c53c-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="0c53c-175">Configureer het leveringsbeleid voor uw asset.</span><span class="sxs-lookup"><span data-stu-id="0c53c-175">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="0c53c-176">De configuratie van het leveringsbeleid voor assets omvat onder andere het volgende:</span><span class="sxs-lookup"><span data-stu-id="0c53c-176">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="0c53c-177">De URL van de Key-overname.</span><span class="sxs-lookup"><span data-stu-id="0c53c-177">The Key acquisition URL.</span></span> 
* <span data-ttu-id="0c53c-178">De initialisatie van de Vector (IV) voor de envelop-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="0c53c-178">The Initialization Vector (IV) to use for the envelope encryption.</span></span> <span data-ttu-id="0c53c-179">AES-128 is vereist dat de dezelfde IV worden opgegeven bij het versleutelen en ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="0c53c-179">AES 128 requires the same IV to be supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="0c53c-180">Het protocol voor het leveren van assets (bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle).</span><span class="sxs-lookup"><span data-stu-id="0c53c-180">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="0c53c-181">Het type dynamische versleuteling (bijvoorbeeld AES envelope) of er geen dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="0c53c-181">The type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="0c53c-182">Zie [Leveringsbeleid voor assets configureren](media-services-rest-configure-asset-delivery-policy.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="0c53c-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="0c53c-183"><a id="create_locator"></a>Een OnDemand-streaminglocator maken om een streaming-URL op te halen</span><span class="sxs-lookup"><span data-stu-id="0c53c-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="0c53c-184">U moet de gebruiker voorzien van de streaming-URL voor Smooth, DASH of HLS.</span><span class="sxs-lookup"><span data-stu-id="0c53c-184">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="0c53c-185">Als u het leveringsbeleid voor uw asset toevoegt of bijwerkt, moet u een bestaande locator (indien aanwezig) verwijderen en een nieuwe locator maken.</span><span class="sxs-lookup"><span data-stu-id="0c53c-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="0c53c-186">Zie [Build a streaming URL](media-services-deliver-streaming-content.md) (Een streaming-URL bouwen) voor instructies over het publiceren van een asset en bouwen van een streaming-URL.</span><span class="sxs-lookup"><span data-stu-id="0c53c-186">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="0c53c-187">Een test-token ophalen</span><span class="sxs-lookup"><span data-stu-id="0c53c-187">Get a test token</span></span>
<span data-ttu-id="0c53c-188">Haal op basis van de tokenbeperking een test-token op die is gebruikt voor het sleutelautorisatiebeleid.</span><span class="sxs-lookup"><span data-stu-id="0c53c-188">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="0c53c-189">U kunt [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) gebruiken om uw stream te testen.</span><span class="sxs-lookup"><span data-stu-id="0c53c-189">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <span data-ttu-id="0c53c-190"><a id="client_request"></a>Hoe kan de client een sleutel van de service sleutellevering aanvragen?</span><span class="sxs-lookup"><span data-stu-id="0c53c-190"><a id="client_request"></a>How can your client request a key from the key delivery service?</span></span>
<span data-ttu-id="0c53c-191">In de vorige stap, moet u de URL die naar een manifestbestand verwijst samengesteld.</span><span class="sxs-lookup"><span data-stu-id="0c53c-191">In the previous step, you constructed the URL that points to a manifest file.</span></span> <span data-ttu-id="0c53c-192">De client moet de benodigde gegevens ophalen uit de streaming-manifestbestanden als doel het maken van een aanvraag naar de service sleutellevering.</span><span class="sxs-lookup"><span data-stu-id="0c53c-192">Your client needs to extract the necessary information from the streaming manifest files in order to make a request to the key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="0c53c-193">Manifestbestanden</span><span class="sxs-lookup"><span data-stu-id="0c53c-193">Manifest files</span></span>
<span data-ttu-id="0c53c-194">De client om op te halen van de URL (dat ook bevat inhoudssleutel Id (kid)) moet de waarde van het manifestbestand.</span><span class="sxs-lookup"><span data-stu-id="0c53c-194">The client needs to extract the URL (that also contains content key Id (kid)) value from the manifest file.</span></span> <span data-ttu-id="0c53c-195">De client probeert vervolgens te ontvangen van de versleutelingssleutel van de service sleutellevering.</span><span class="sxs-lookup"><span data-stu-id="0c53c-195">The client will then try to get the encryption key from the key delivery service.</span></span> <span data-ttu-id="0c53c-196">De client moet ook de IV waarde en het gebruik het ontsleutelen van de stroom extraheren. Het volgende codefragment bevat de <Protection> element van het manifest Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="0c53c-196">The client also needs to extract the IV value and use it do decrypt the stream.The following snippet shows the <Protection> element of the Smooth Streaming manifest.</span></span>

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

<span data-ttu-id="0c53c-197">In het geval van HLS, is het manifest hoofdmap onderverdeeld in segment bestanden.</span><span class="sxs-lookup"><span data-stu-id="0c53c-197">In the case of HLS, the root manifest is broken into segment files.</span></span> 

<span data-ttu-id="0c53c-198">Bijvoorbeeld: het manifest voor de hoofdmap is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) en het bevat een lijst met bestandsnamen segment.</span><span class="sxs-lookup"><span data-stu-id="0c53c-198">For example, the root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="0c53c-199">Als u een van de segment-bestanden in de teksteditor (bijvoorbeeld http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain openen #EXT-X-sleutel waarmee wordt aangegeven dat het bestand is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="0c53c-199">If you open one of the segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that the file is encrypted.</span></span>

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
><span data-ttu-id="0c53c-200">Als u van plan bent om af te spelen een AES HLS in Safari versleuteld, Zie [deze blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="0c53c-200">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-the-key-from-the-key-delivery-service"></a><span data-ttu-id="0c53c-201">De sleutel van de service sleutellevering aanvragen</span><span class="sxs-lookup"><span data-stu-id="0c53c-201">Request the key from the key delivery service</span></span>

<span data-ttu-id="0c53c-202">De volgende code laat zien hoe een aanvraag te verzenden naar de Media Services-sleutellevering-service via een sleutellevering Uri (dat is opgehaald uit het manifest) en een token (in dit onderwerp spreekt niet over het ophalen van Simple Web Tokens uit een Secure Token Service).</span><span class="sxs-lookup"><span data-stu-id="0c53c-202">The following code shows how to send a request to the Media Services key delivery service using a key delivery Uri (that was extracted from the manifest) and a token (this topic does not talk about how to get Simple Web Tokens from a Secure Token Service).</span></span>

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

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="0c53c-203">De inhoud beveiligen met AES-128 met .NET</span><span class="sxs-lookup"><span data-stu-id="0c53c-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0c53c-204">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="0c53c-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="0c53c-205">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0c53c-205">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="0c53c-206">Voeg de volgende elementen toe aan **appSettings** dat in het bestand app.config is gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="0c53c-206">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="0c53c-207"><a id="example"></a>Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="0c53c-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="0c53c-208">Overschrijf de code in uw Program.cs-bestand met de code die wordt weergegeven in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="0c53c-208">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="0c53c-209">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="0c53c-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="0c53c-210">U moet dezelfde beleids-id gebruiken als u altijd dezelfde dagen/toegangsmachtigingen gebruikt, bijvoorbeeld beleidsregels voor locators die zijn bedoeld om gedurende een lange periode gehandhaafd te blijven (niet-upload-beleidsregels).</span><span class="sxs-lookup"><span data-stu-id="0c53c-210">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="0c53c-211">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0c53c-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="0c53c-212">Zorg ervoor dat variabelen zo worden bijgewerkt dat ze verwijzen naar de mappen waar uw invoerbestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="0c53c-212">Make sure to update variables to point to folders where your input files are located.</span></span>

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
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing the issuer of the token.  
        // Must match the value in the token for the token to be considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // The Audience or Scope of the token.  
        // Must match the value in the token for the token to be considered valid.
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
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //The GenerateTestToken method returns the token without the word “Bearer” in front
            //so you have to add it in front of the token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use the bit.ly/aesplayer Flash player to test the URL 
            // (with open authorization policy). 
            // Paste the URL and click the Update button to play the video. 
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
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

            // Associate the key with the asset.
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

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
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

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose to associate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in the key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  the URL does not contains a key ID

            // The following policy configuration specifies: 
            // key url that will have KID=<Guid> appended to the envelope and
            // the Initialization Vector (IV) to use for the envelope encryption.

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

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin. 
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file. 
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


## <a name="media-services-learning-paths"></a><span data-ttu-id="0c53c-213">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="0c53c-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0c53c-214">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="0c53c-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

