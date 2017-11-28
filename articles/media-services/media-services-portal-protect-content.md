---
title: aaaConfiguring inhoudsbeveiliging beleidsregels met behulp van Azure-portal Hallo | Microsoft Docs
description: In dit artikel laat zien hoe toouse hello Azure portal tooconfigure content protection-beleid. Hallo artikel wordt ook toont hoe tooenable dynamische versleuteling voor de activa.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a><span data-ttu-id="cdc4e-104">Beleidsregels voor beveiliging van inhoud met behulp van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="cdc4e-104">Configuring content protection policies using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="cdc4e-105">toocomplete in deze zelfstudie, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="cdc4e-106">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="cdc4e-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="cdc4e-107">Overview</span></span>
<span data-ttu-id="cdc4e-108">Microsoft Azure Media Services (AMS) kunt u toosecure uw media Hallo tijd vanaf uw computer via de opslag, verwerking en levering.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-108">Microsoft Azure Media Services (AMS) enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="cdc4e-109">Media Services kunt u toodeliver uw inhoud versleuteld dynamisch met Advanced Encryption Standard (AES) (met behulp van coderingssleutels 128-bits), common encryption (CENC) met PlayReady en/of Widevine DRM en Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-109">Media Services allows you toodeliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="cdc4e-110">AMS voorziet in een service voor het leveren van DRM-licenties en AES wissen sleutels tooauthorized clients.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-110">AMS provides a service for delivering DRM licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="cdc4e-111">Hello Azure-portal kunt u toocreate een **sleutel/licentie autorisatiebeleid** voor alle typen versleutelingen.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-111">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="cdc4e-112">In dit artikel laat zien hoe tooconfigure inhoud beveiligingsbeleid Hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-112">This article demonstrates how tooconfigure content protection policies with hello Azure portal.</span></span> <span data-ttu-id="cdc4e-113">Hallo artikel wordt ook toont hoe tooapply dynamische versleuteling tooyour activa.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-113">hello article also shows how tooapply dynamic encryption tooyour assets.</span></span>


> [!NOTE]
> <span data-ttu-id="cdc4e-114">Als u hello Azure classic portal toocreate protection-beleid gebruikt, Hallo beleid mogelijk niet in Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cdc4e-114">If you used hello Azure classic portal toocreate protection policies, hello policies may not appear in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="cdc4e-115">Alle Hallo oude beleidsregels echter nog steeds aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-115">However, all hello old polices still exist.</span></span> <span data-ttu-id="cdc4e-116">U kunt ze controleren met behulp van Azure Media Services .NET SDK of Hallo Hallo [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) hulpprogramma (toosee Hallo beleidsregels, klik met de rechtermuisknop op Hallo asset -> weergave informatie (F4) -> Klik op inhoud sleutels tabblad -> Klik op het Hallo-sleutel).</span><span class="sxs-lookup"><span data-stu-id="cdc4e-116">You can examine them using hello Azure Media Services .NET SDK or hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (toosee hello policies, right-click on hello asset -> Display information (F4)->click on Content keys tab-> click on hello key).</span></span> 
> 
> <span data-ttu-id="cdc4e-117">Als u uw asset werken met beleid voor nieuwe tooencrypt wilt, configureert u deze met hello Azure-portal, klik op Opslaan en dynamische versleuteling toepassen.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-117">If you want tooencrypt your asset using new policies, configure them with hello Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="cdc4e-118">Beginnen met de configuratie van de beveiliging van inhoud</span><span class="sxs-lookup"><span data-stu-id="cdc4e-118">Start configuring content protection</span></span>
<span data-ttu-id="cdc4e-119">toouse hello portal toostart content protection globale tooyour AMS-account configureren Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="cdc4e-119">toouse hello portal toostart configuring content protection, global tooyour AMS account, do hello following:</span></span>

1. <span data-ttu-id="cdc4e-120">In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="cdc4e-121">Selecteer **instellingen** > **Content protection**.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-121">Select **Settings** > **Content protection**.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="cdc4e-123">Autorisatiebeleid voor de sleutel/licentie</span><span class="sxs-lookup"><span data-stu-id="cdc4e-123">Key/license authorization policy</span></span>
<span data-ttu-id="cdc4e-124">AMS ondersteunt meerdere manieren van gebruikers die sleutel of licentie-aanvragen te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="cdc4e-125">Hallo autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en voldaan door de client om Hallo sleutel/licentie toobe delived toohello client.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-125">hello content key authorization policy must be configured by you and met by your client in order for hello key/license toobe delived toohello client.</span></span> <span data-ttu-id="cdc4e-126">Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: **openen** of **token** beperking.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-126">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="cdc4e-127">Hello Azure-portal kunt u toocreate een **sleutel/licentie autorisatiebeleid** voor alle typen versleutelingen.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-127">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="cdc4e-128">Open</span><span class="sxs-lookup"><span data-stu-id="cdc4e-128">Open</span></span>
<span data-ttu-id="cdc4e-129">Open beperking houdt in dat systeem Hallo Hallo sleutel tooanyone die sleutels aanvragen levert.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-129">Open restriction means that hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="cdc4e-130">Deze beperking kan handig zijn voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="cdc4e-131">Token</span><span class="sxs-lookup"><span data-stu-id="cdc4e-131">Token</span></span>
<span data-ttu-id="cdc4e-132">Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="cdc4e-132">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="cdc4e-133">Media Services ondersteunt tokens in Hallo Simple Web Tokens (SWT) en JSON Web Token (JWT)-indeling.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-133">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="cdc4e-134">Media Services biedt geen Token Services beveiligen.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="cdc4e-135">U kunt een aangepaste STS maken of gebruikmaken van Microsoft Azure ACS tooissue tokens.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-135">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="cdc4e-136">Hallo STS moet geconfigureerde toocreate token van een ondertekend met Hallo opgegeven sleutel- en claims die u hebt opgegeven in de configuratie van Hallo tokenbeperking.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-136">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="cdc4e-137">Hallo Media Services sleutellevering service Hallo aangevraagd toohello (of licentiegegevens)-client retourneert als Hallo token geldig is en Hallo claims in Hallo token overeenkomen met die zijn geconfigureerd voor hello (of licentiegegevens).</span><span class="sxs-lookup"><span data-stu-id="cdc4e-137">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="cdc4e-138">U moet bij het configureren van token beperkte beleid Hallo Hallo verificatie van de primaire sleutel, uitgever en doelgroep parameters opgeven.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-138">When configuring hello token restricted policy, you must specify hello primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="cdc4e-139">Hallo verificatie van de primaire sleutel bevat Hallo key of Hallo-token is ondertekend met, de uitgever Hallo secure token-service die het Hallo-token uitgeeft.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-139">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="cdc4e-140">Hallo doelgroep (ook wel bereik genoemd) wordt beschreven Hallo bedoeling van Hallo token of Hallo resource Hallo token gemachtigd voor toegang tot.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-140">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="cdc4e-141">Hallo Media Services-service voor sleutellevering valideert dat deze waarden in Hallo token Hallo-waarden in de sjabloon Hallo overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-141">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="cdc4e-143">PlayReady-rechtensjabloon</span><span class="sxs-lookup"><span data-stu-id="cdc4e-143">PlayReady rights template</span></span>
<span data-ttu-id="cdc4e-144">Zie voor gedetailleerde informatie over Hallo PlayReady rechtensjabloon [Media Services PlayReady licentie sjabloon overzicht](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cdc4e-144">For detailed information about hello PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="cdc4e-145">Niet-permanente</span><span class="sxs-lookup"><span data-stu-id="cdc4e-145">Non persistent</span></span>
<span data-ttu-id="cdc4e-146">Als u de licentie als niet-permanente configureert, wordt deze alleen bewaard in het geheugen tijdens het Hallo-speler Hallo-licentie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-146">If you configure license as non-persistent, it is only held in memory while hello player is using hello license.</span></span>  

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="cdc4e-148">Permanente</span><span class="sxs-lookup"><span data-stu-id="cdc4e-148">Persistent</span></span>
<span data-ttu-id="cdc4e-149">Als u Hallo licentie als permanente configureert, wordt deze opgeslagen in de permanente opslag op Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-149">If you configure hello license  as persistent, it is saved in persistent storage on hello client.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="cdc4e-151">Widevine-rechtensjabloon</span><span class="sxs-lookup"><span data-stu-id="cdc4e-151">Widevine rights template</span></span>
<span data-ttu-id="cdc4e-152">Zie voor gedetailleerde informatie over Hallo Widevine rechtensjabloon [Widevine-licentie sjabloon overzicht](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cdc4e-152">For detailed information about hello Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="cdc4e-153">Basic</span><span class="sxs-lookup"><span data-stu-id="cdc4e-153">Basic</span></span>
<span data-ttu-id="cdc4e-154">Wanneer u selecteert **Basic**, Hallo sjabloon wordt gemaakt met alle standaardwaarden waarden.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-154">When you select **Basic**, hello template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="cdc4e-155">Geavanceerd</span><span class="sxs-lookup"><span data-stu-id="cdc4e-155">Advanced</span></span>
<span data-ttu-id="cdc4e-156">Zie voor gedetailleerde uitleg over geavanceerde optie Widevine configuraties [dit](media-services-widevine-license-template-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="cdc4e-158">FairPlay-configuratie</span><span class="sxs-lookup"><span data-stu-id="cdc4e-158">FairPlay configuration</span></span>
<span data-ttu-id="cdc4e-159">tooenable FairPlay versleuteling, moet u tooprovide Hallo certificaat-App en toepassing geheime sleutel (vraag) via Hallo FairPlay configuratieoptie.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-159">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option.</span></span> <span data-ttu-id="cdc4e-160">Zie voor gedetailleerde informatie over de vereisten en FairPlay configuratie [dit](media-services-protect-hls-with-fairplay.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a><span data-ttu-id="cdc4e-162">Dynamische versleuteling tooyour asset toepassen</span><span class="sxs-lookup"><span data-stu-id="cdc4e-162">Apply dynamic encryption tooyour asset</span></span>
<span data-ttu-id="cdc4e-163">tootake profiteren van dynamische versleuteling hoeft u tooencode uw bronbestand in een set adaptive bitrate MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-163">tootake advantage of dynamic encryption, you need tooencode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-tooencrypt"></a><span data-ttu-id="cdc4e-164">Selecteer een asset die u tooencrypt wilt</span><span class="sxs-lookup"><span data-stu-id="cdc4e-164">Select an asset that you want tooencrypt</span></span>
<span data-ttu-id="cdc4e-165">uw assets selecteert u toosee **instellingen** > **activa**.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-165">toosee all your assets, select **Settings** > **Assets**.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="cdc4e-167">Versleutelen met AES of DRM</span><span class="sxs-lookup"><span data-stu-id="cdc4e-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="cdc4e-168">Indrukken **versleutelen** op een actief, krijgt u twee opties: **AES** of **DRM**.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="cdc4e-169">AES</span><span class="sxs-lookup"><span data-stu-id="cdc4e-169">AES</span></span>
<span data-ttu-id="cdc4e-170">AES wissen sleutelcodering wordt ingeschakeld voor alle protocollen voor streaming: Smooth Streaming, HLS en MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="cdc4e-172">DRM</span><span class="sxs-lookup"><span data-stu-id="cdc4e-172">DRM</span></span>
<span data-ttu-id="cdc4e-173">Wanneer u Hallo DRM tabblad selecteert, krijgt u verschillende mogelijkheden van het beleid van de beveiliging van inhoud (die u moet nu hebt geconfigureerd) + een reeks protocollen voor streaming.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-173">When you select hello DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="cdc4e-174">**PlayReady en Widevine met MPEG-DASH** -wordt uw MPEG-DASH-stream met PlayReady en Widevine DRM's dynamisch versleutelen.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="cdc4e-175">**PlayReady en Widevine met MPEG-DASH + FairPlay met HLS** -wordt dynamisch versleutelen u MPEG-DASH-stroom met PlayReady en Widevine DRM's.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="cdc4e-176">Uw HLS-streams met FairPlay zal ook worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="cdc4e-177">**PlayReady alleen met Smooth Streaming, HLS en MPEG-DASH** -wordt dynamisch versleutelen Smooth Streaming, HLS, MPEG-DASH-streams met PlayReady DRM.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="cdc4e-178">**Widevine alleen met MPEG-DASH** -wordt dynamisch versleutelen u MPEG-DASH met Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="cdc4e-179">**FairPlay alleen met HLS** -wordt uw HLS-stream met FairPlay dynamisch versleutelen.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="cdc4e-180">tooenable FairPlay versleuteling, moet u tooprovide Hallo certificaat-App en toepassing geheime sleutel (vraag) via Hallo FairPlay configuratieoptie van blade Hallo Content Protection-instellingen.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-180">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option of hello Content Protection settings blade.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="cdc4e-182">Wanneer u Hallo versleutelingsselectie hebt gemaakt, drukt u op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-182">Once you make hello encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="cdc4e-183">Als u van plan bent tooplay een AES HLS in Safari versleuteld, Zie [deze blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="cdc4e-183">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdc4e-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cdc4e-184">Next steps</span></span>
<span data-ttu-id="cdc4e-185">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="cdc4e-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cdc4e-186">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="cdc4e-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

