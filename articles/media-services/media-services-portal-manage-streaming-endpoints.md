---
title: streaming-eindpunten Hello Azure-portal aaaManage | Microsoft Docs
description: Dit onderwerp leest hoe toomanage streaming-eindpunten met hello Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="653ca-103">Streaming-eindpunten Hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="653ca-103">Manage streaming endpoints with hello Azure portal</span></span>

<span data-ttu-id="653ca-104">Dit onderwerp leest hoe toouse hello Azure portal toomanage streaming-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="653ca-104">This topic shows  how toouse hello Azure portal toomanage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="653ca-105">Zorg ervoor dat tooreview hello [overzicht](media-services-streaming-endpoints-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="653ca-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="653ca-106">Zie voor meer informatie over hoe tooscale streaming-eindpunt Hallo [dit](media-services-portal-scale-streaming-endpoints.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="653ca-106">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="653ca-107">Beginnen met het streaming-eindpunten beheren</span><span class="sxs-lookup"><span data-stu-id="653ca-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="653ca-108">streaming-eindpunten voor uw account beheren toostart Hallo te volgen.</span><span class="sxs-lookup"><span data-stu-id="653ca-108">toostart managing streaming endpoints for your account, do hello following.</span></span>

1. <span data-ttu-id="653ca-109">In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="653ca-109">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="653ca-110">In Hallo **instellingen** blade Selecteer **Streaming-eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="653ca-110">In hello **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![Streaming-eindpunt](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="653ca-112">U wordt alleen gefactureerd als uw Streaming-eindpunt wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="653ca-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="653ca-113">Een streaming-eindpunt toevoegen/verwijderen</span><span class="sxs-lookup"><span data-stu-id="653ca-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="653ca-114">Hallo standaardstreaming-eindpunt kan niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="653ca-114">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="653ca-115">streaming-eindpunt met behulp van tooadd/delete Hallo Azure-portal, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="653ca-115">tooadd/delete streaming endpoint using hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="653ca-116">tooadd een streaming-eindpunt, klikt u op Hallo **+ eindpunt** bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="653ca-116">tooadd a streaming endpoint, click hello **+ Endpoint** at hello top of hello page.</span></span> 

    <span data-ttu-id="653ca-117">U kunt meerdere Streaming-eindpunten op als u van plan toohave bent verschillende CDN of een CDN en directe toegang.</span><span class="sxs-lookup"><span data-stu-id="653ca-117">You might want multiple Streaming Endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="653ca-118">een streaming-eindpunt toodelete druk op **verwijderen** knop.</span><span class="sxs-lookup"><span data-stu-id="653ca-118">toodelete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="653ca-119">Klik op Hallo **Start** knop toostart Hallo streaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="653ca-119">Click hello **Start** button toostart hello streaming endpoint.</span></span>
   
    ![Streaming-eindpunt](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="653ca-121"><a id="configure_streaming_endpoints"></a>Hallo Streaming-eindpunt configureren</span><span class="sxs-lookup"><span data-stu-id="653ca-121"><a id="configure_streaming_endpoints"></a>Configuring hello Streaming Endpoint</span></span>
<span data-ttu-id="653ca-122">Streaming-eindpunt kunt u tooconfigure Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="653ca-122">Streaming Endpoint enables you tooconfigure hello following properties:</span></span>

* <span data-ttu-id="653ca-123">Toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="653ca-123">Access control</span></span>
* <span data-ttu-id="653ca-124">Cache-control</span><span class="sxs-lookup"><span data-stu-id="653ca-124">Cache control</span></span>
* <span data-ttu-id="653ca-125">Cross-site-beleid</span><span class="sxs-lookup"><span data-stu-id="653ca-125">Cross site access policies</span></span>

<span data-ttu-id="653ca-126">Zie voor gedetailleerde informatie over deze eigenschappen [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="653ca-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="653ca-127">U kunt de streaming-eindpunt configureren door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="653ca-127">You can configure streaming endpoint by doing hello following:</span></span>

1. <span data-ttu-id="653ca-128">Selecteer Hallo streaming-eindpunt dat u wilt dat tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="653ca-128">Select hello streaming endpoint you want tooconfigure.</span></span>
2. <span data-ttu-id="653ca-129">Klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="653ca-129">Click **Settings**.</span></span>

<span data-ttu-id="653ca-130">Hier volgt een korte beschrijving van Hallo velden.</span><span class="sxs-lookup"><span data-stu-id="653ca-130">A brief description of hello fields follows.</span></span>

![Streaming-eindpunt](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="653ca-132">Maximale cachegrootte beleid: de cachebewaartijd gebruikte tooconfigure voor activa geleverd door middel van deze streaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="653ca-132">Maximum cache policy: used tooconfigure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="653ca-133">Als geen waarde is ingesteld, wordt Hallo standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="653ca-133">If no value is set, hello default is used.</span></span> <span data-ttu-id="653ca-134">Hallo standaardwaarden kunnen ook rechtstreeks in Azure-opslag worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="653ca-134">hello default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="653ca-135">Als Azure CDN voor Hallo streaming-eindpunt is ingeschakeld, moet u Hallo cache beleid waarde tooless dan 600 seconden niet instellen.</span><span class="sxs-lookup"><span data-stu-id="653ca-135">If Azure CDN is enabled for hello streaming endpoint, you should not set hello cache policy value tooless than 600 seconds.</span></span>  
2. <span data-ttu-id="653ca-136">Toegestane IP-adressen: toospecify IP-adressen die mogen tooconnect toohello gepubliceerd streaming-eindpunt wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="653ca-136">Allowed IP addresses: used toospecify IP addresses that would be allowed tooconnect toohello published streaming endpoint.</span></span> <span data-ttu-id="653ca-137">Als er geen IP-adressen is opgegeven, wordt elk IP-adres kunnen tooconnect.</span><span class="sxs-lookup"><span data-stu-id="653ca-137">If no IP addresses specified, any IP address would be able tooconnect.</span></span> <span data-ttu-id="653ca-138">IP-adressen kunnen worden opgegeven als een enkel IP-adres (bijvoorbeeld: (10.0.0.1), een IP-adresbereik met een IP-adres en een CIDR-subnetmasker (bijvoorbeeld (10.0.0.1/22) of een IP-adresbereik IP-adres en een decimaal subnetmasker met punten (bijvoorbeeld: 10.0.0.1 ' () 255.255.255.0)').</span><span class="sxs-lookup"><span data-stu-id="653ca-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="653ca-139">Configuratie voor Akamai signature header-verificatie: gebruikt toospecify hoe handtekening header-verificatieaanvraag van Akamai servers is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="653ca-139">Configuration for Akamai signature header authentication: used toospecify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="653ca-140">Verlooptijd is ingesteld op UTC.</span><span class="sxs-lookup"><span data-stu-id="653ca-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="653ca-141">Schalen van uw Premium streaming-eindpunt</span><span class="sxs-lookup"><span data-stu-id="653ca-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="653ca-142">Raadpleeg [dit](media-services-portal-scale-streaming-endpoints.md) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="653ca-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="653ca-143"><a id="enable_cdn"></a>Integratie van Azure CDN inschakelen</span><span class="sxs-lookup"><span data-stu-id="653ca-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="653ca-144">Wanneer u een nieuw account maakt, wordt standaard Streaming-eindpunt Azure CDN-integratie is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="653ca-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="653ca-145">Desgewenst kunt u later toodisable/enable Hallo CDN streaming-eindpunt moet Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="653ca-145">If you later want toodisable/enable hello CDN, your streaming endpoint must be in hello **stopped** state.</span></span> <span data-ttu-id="653ca-146">Het kan too2 uur voor hello Azure CDN integratie tooget ingeschakeld en voor Hallo wijzigingen toobe active over alle Hallo CDN POP's duren.</span><span class="sxs-lookup"><span data-stu-id="653ca-146">It could take up too2 hours for hello Azure CDN integration tooget enabled and for hello changes toobe active across all hello CDN POPs.</span></span> <span data-ttu-id="653ca-147">Echter, u kunt uw streaming-eindpunt en stream zonder onderbrekingen start vanaf Hallo streaming-eindpunt en zodra Hallo-integratie voltooid is, Hallo stroom van Hallo CDN worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="653ca-147">However, your can start your streaming endpoint and stream without interruptions from hello streaming endpoint and once hello integration is complete, hello stream will be delivered from hello CDN.</span></span> <span data-ttu-id="653ca-148">Streaming-eindpunt is niet tijdens Hallo inrichting periode **vanaf** status en u merkt wellicht degredad prestaties.</span><span class="sxs-lookup"><span data-stu-id="653ca-148">During hello provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="653ca-149">CDN-integratie is ingeschakeld in alle hello Azure datacenters execpt China en Federal Goverment regio's.</span><span class="sxs-lookup"><span data-stu-id="653ca-149">CDN integration is enabled in all hello Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="653ca-150">Zodra deze is ingeschakeld, Hallo **toegangsbeheer**, **aangepaste hostnaam** en **Akamai Signature-verificatie** configuratie opgehaald uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="653ca-150">Once it is enabled, hello **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="653ca-151">Azure Media Services-integratie met Azure CDN is geïmplementeerd op **Azure CDN van Verizon** voor standaard streaming-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="653ca-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="653ca-152">Premium-streaming-eindpunten kan worden geconfigureerd met alle **Azure CDN prijzen lagen en providers**.</span><span class="sxs-lookup"><span data-stu-id="653ca-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="653ca-153">Zie voor meer informatie over de functies van Azure CDN Hallo [overzicht van CDN](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="653ca-153">For more information about Azure CDN features, see hello [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="653ca-154">Aanvullende overwegingen</span><span class="sxs-lookup"><span data-stu-id="653ca-154">Additional considerations</span></span>

* <span data-ttu-id="653ca-155">Wanneer CDN is ingeschakeld voor een streaming-eindpunt, kunnen geen clients inhoud rechtstreeks vanuit de oorsprong Hallo vragen.</span><span class="sxs-lookup"><span data-stu-id="653ca-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from hello origin.</span></span> <span data-ttu-id="653ca-156">Als u uw inhoud met of zonder CDN Hallo mogelijkheid tootest moet, kunt u een ander streaming-eindpunt dat niet ingeschakeld CDN is kunt maken.</span><span class="sxs-lookup"><span data-stu-id="653ca-156">If you need hello ability tootest your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="653ca-157">Uw streaming endpoint hostnaam blijft Hallo dezelfde nadat de CDN is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="653ca-157">Your streaming endpoint hostname remains hello same after enabling CDN.</span></span> <span data-ttu-id="653ca-158">U hoeft niet toomake eventuele wijzigingen tooyour media services-werkstroom nadat CDN is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="653ca-158">You don’t need toomake any changes tooyour media services workflow after CDN is enabled.</span></span> <span data-ttu-id="653ca-159">Als uw streaming endpoint-hostnaam strasbourg.streaming.mediaservices.windows.net, nadat de CDN is ingeschakeld, wordt bijvoorbeeld Hallo exact dezelfde hostnaam gebruikt.</span><span class="sxs-lookup"><span data-stu-id="653ca-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, hello exact same hostname is used.</span></span>
* <span data-ttu-id="653ca-160">Voor nieuwe streaming-eindpunten, kunt u CDN inschakelen door te maken van een nieuw eindpunt; voor bestaande streaming-eindpunten moet u toofirst stoppen Hallo eindpunt en klik vervolgens in-of uitschakelen Hallo CDN.</span><span class="sxs-lookup"><span data-stu-id="653ca-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need toofirst stop hello endpoint and then enable/disable hello CDN.</span></span>
* <span data-ttu-id="653ca-161">Standaard streaming-eindpunt kan alleen worden geconfigureerd met behulp van **Verizon standaard CDN-provider** met behulp van Azure-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="653ca-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="653ca-162">U kunt echter andere Azure CDN-providers met REST API's inschakelen.</span><span class="sxs-lookup"><span data-stu-id="653ca-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="653ca-163">CDN-profiel configureren</span><span class="sxs-lookup"><span data-stu-id="653ca-163">Configure CDN profile</span></span>

<span data-ttu-id="653ca-164">U kunt Hallo CDN-profiel configureren met behulp van Hallo **beheren CDN** knop van Hallo boven.</span><span class="sxs-lookup"><span data-stu-id="653ca-164">You can configure hello CDN profile by selecting hello **Manage CDN** button from hello top.</span></span>

![Streaming-eindpunt](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="653ca-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="653ca-166">Next steps</span></span>
<span data-ttu-id="653ca-167">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="653ca-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="653ca-168">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="653ca-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

