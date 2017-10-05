---
title: Configureren van beleidsregels voor beveiliging van inhoud met behulp van de Azure-portal | Microsoft Docs
description: In dit artikel laat zien hoe de Azure portal gebruiken voor het configureren van beleid voor beveiliging van inhoud. Ook wordt uitgelegd hoe u dynamische versleuteling voor de activa in te schakelen.
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
ms.openlocfilehash: 67b3fa9936daebeafb7e87fe3a7b0c7e0105b3b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-content-protection-policies-using-the-azure-portal"></a><span data-ttu-id="495f1-104">Beleidsregels voor beveiliging van inhoud met behulp van de Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="495f1-104">Configuring content protection policies using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="495f1-105">U hebt een Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="495f1-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="495f1-106">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="495f1-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="495f1-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="495f1-107">Overview</span></span>
<span data-ttu-id="495f1-108">Microsoft Azure Media Services (AMS) kunt u voor het beveiligen van uw media vanaf het moment dat het verlaten van uw computer via de opslag, verwerking en levering.</span><span class="sxs-lookup"><span data-stu-id="495f1-108">Microsoft Azure Media Services (AMS) enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="495f1-109">Media Services kunt u leveren de inhoud versleuteld dynamisch met Advanced Encryption Standard (AES) (met behulp van coderingssleutels 128-bits), common encryption (CENC) met PlayReady en/of Widevine DRM en Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="495f1-109">Media Services allows you to deliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="495f1-110">AMS voorziet in een service voor het leveren van DRM-licenties en AES-sleutels geautoriseerde clients wissen.</span><span class="sxs-lookup"><span data-stu-id="495f1-110">AMS provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="495f1-111">De Azure-portal kunt u een maken **sleutel/licentie autorisatiebeleid** voor alle typen versleutelingen.</span><span class="sxs-lookup"><span data-stu-id="495f1-111">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="495f1-112">In dit artikel laat zien hoe beleid voor beveiliging van inhoud configureren met de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="495f1-112">This article demonstrates how to configure content protection policies with the Azure portal.</span></span> <span data-ttu-id="495f1-113">Ook wordt uitgelegd hoe u dynamische versleuteling toepassen op uw assets.</span><span class="sxs-lookup"><span data-stu-id="495f1-113">The article also shows how to apply dynamic encryption to your assets.</span></span>


> [!NOTE]
> <span data-ttu-id="495f1-114">Als u de klassieke Azure portal gebruikt voor het maken van beleid voor gegevensbeveiliging, het beleid mogelijk niet in de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="495f1-114">If you used the Azure classic portal to create protection policies, the policies may not appear in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="495f1-115">Echter alle beleidsregels van de oude, nog bestaan.</span><span class="sxs-lookup"><span data-stu-id="495f1-115">However, all the old polices still exist.</span></span> <span data-ttu-id="495f1-116">U kunt deze met Azure Media Services .NET SDK controleren of de [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) hulpprogramma (overzicht van het beleid met de rechtermuisknop op de asset -> weergave informatie (F4) -> Klik op het tabblad inhoud sleutels -> Klik op de sleutel).</span><span class="sxs-lookup"><span data-stu-id="495f1-116">You can examine them using the Azure Media Services .NET SDK or the [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (to see the policies, right-click on the asset -> Display information (F4)->click on Content keys tab-> click on the key).</span></span> 
> 
> <span data-ttu-id="495f1-117">Als u versleutelen van uw asset met behulp van nieuwe beleidsregels wilt, configureert u deze met de Azure-portal, klik op Opslaan en dynamische versleuteling toepassen.</span><span class="sxs-lookup"><span data-stu-id="495f1-117">If you want to encrypt your asset using new policies, configure them with the Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="495f1-118">Beginnen met de configuratie van de beveiliging van inhoud</span><span class="sxs-lookup"><span data-stu-id="495f1-118">Start configuring content protection</span></span>
<span data-ttu-id="495f1-119">Als u de portal wilt beginnen met de configuratie van de beveiliging van inhoud, globale op uw AMS-account, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="495f1-119">To use the portal to start configuring content protection, global to your AMS account, do the following:</span></span>

1. <span data-ttu-id="495f1-120">Selecteer uw Azure Media Services-account in [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="495f1-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="495f1-121">Selecteer **instellingen** > **Content protection**.</span><span class="sxs-lookup"><span data-stu-id="495f1-121">Select **Settings** > **Content protection**.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="495f1-123">Autorisatiebeleid voor de sleutel/licentie</span><span class="sxs-lookup"><span data-stu-id="495f1-123">Key/license authorization policy</span></span>
<span data-ttu-id="495f1-124">AMS ondersteunt meerdere manieren van gebruikers die sleutel of licentie-aanvragen te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="495f1-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="495f1-125">Het autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en voldaan door de client om de sleutel/licentie worden delived naar de client.</span><span class="sxs-lookup"><span data-stu-id="495f1-125">The content key authorization policy must be configured by you and met by your client in order for the key/license to be delived to the client.</span></span> <span data-ttu-id="495f1-126">Het autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: **openen** of **token** beperking.</span><span class="sxs-lookup"><span data-stu-id="495f1-126">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="495f1-127">De Azure-portal kunt u een maken **sleutel/licentie autorisatiebeleid** voor alle typen versleutelingen.</span><span class="sxs-lookup"><span data-stu-id="495f1-127">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="495f1-128">Open</span><span class="sxs-lookup"><span data-stu-id="495f1-128">Open</span></span>
<span data-ttu-id="495f1-129">Open beperking betekent dat het systeem de sleutel voor iedereen die een sleutel aanvraag indient levert.</span><span class="sxs-lookup"><span data-stu-id="495f1-129">Open restriction means that the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="495f1-130">Deze beperking kan handig zijn voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="495f1-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="495f1-131">Token</span><span class="sxs-lookup"><span data-stu-id="495f1-131">Token</span></span>
<span data-ttu-id="495f1-132">Het beleid met de tokenbeperking moet vergezeld gaan van een token dat is uitgegeven door Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="495f1-132">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="495f1-133">Media Services ondersteunt tokens in de indeling Simple Web Tokens (SWT) en JSON Web Token (JWT)-indeling.</span><span class="sxs-lookup"><span data-stu-id="495f1-133">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="495f1-134">Media Services biedt geen Token Services beveiligen.</span><span class="sxs-lookup"><span data-stu-id="495f1-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="495f1-135">U kunt een aangepaste STS maken of gebruikmaken van Microsoft Azure ACS voor het probleem van tokens.</span><span class="sxs-lookup"><span data-stu-id="495f1-135">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="495f1-136">De STS moeten worden geconfigureerd voor het maken van een token dat is ondertekend met de opgegeven sleutel- en claims die u hebt opgegeven in de configuratie van de tokenbeperking.</span><span class="sxs-lookup"><span data-stu-id="495f1-136">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="495f1-137">De Media Services sleutellevering-service wordt de aangevraagde sleutel (of licentie) naar de client als het token geldig is en de claims in het token overeenkomen met die zijn geconfigureerd voor de sleutel (of licentie) geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="495f1-137">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="495f1-138">Wanneer beleid voor het configureren van het token worden beperkt, moet u de verificatie van de primaire sleutel, uitgever en doelgroep parameters opgeven.</span><span class="sxs-lookup"><span data-stu-id="495f1-138">When configuring the token restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="495f1-139">De verificatie van de primaire sleutel bevat de sleutel die het token is ondertekend met, certificaatverlener is de secure token service die de token uitgeeft.</span><span class="sxs-lookup"><span data-stu-id="495f1-139">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="495f1-140">De doelgroep (ook wel bereik genoemd) beschrijft de intentie van het token of de resource het token gemachtigd voor toegang tot.</span><span class="sxs-lookup"><span data-stu-id="495f1-140">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="495f1-141">De Media Services-service sleutellevering valideert dat deze waarden in het token overeenkomen met de waarden in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="495f1-141">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="495f1-143">PlayReady-rechtensjabloon</span><span class="sxs-lookup"><span data-stu-id="495f1-143">PlayReady rights template</span></span>
<span data-ttu-id="495f1-144">Zie voor gedetailleerde informatie over de rechtensjabloon PlayReady [Media Services PlayReady licentie sjabloon overzicht](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="495f1-144">For detailed information about the PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="495f1-145">Niet-permanente</span><span class="sxs-lookup"><span data-stu-id="495f1-145">Non persistent</span></span>
<span data-ttu-id="495f1-146">Als u de licentie als niet-permanente configureert, wordt deze alleen bewaard in het geheugen terwijl de licentie wordt gebruikt door Windows media player.</span><span class="sxs-lookup"><span data-stu-id="495f1-146">If you configure license as non-persistent, it is only held in memory while the player is using the license.</span></span>  

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="495f1-148">Permanente</span><span class="sxs-lookup"><span data-stu-id="495f1-148">Persistent</span></span>
<span data-ttu-id="495f1-149">Als u de licentie als permanente configureert, wordt deze opgeslagen in de permanente opslag op de client.</span><span class="sxs-lookup"><span data-stu-id="495f1-149">If you configure the license  as persistent, it is saved in persistent storage on the client.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="495f1-151">Widevine-rechtensjabloon</span><span class="sxs-lookup"><span data-stu-id="495f1-151">Widevine rights template</span></span>
<span data-ttu-id="495f1-152">Zie voor gedetailleerde informatie over de rechtensjabloon Widevine [Widevine-licentie sjabloon overzicht](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="495f1-152">For detailed information about the Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="495f1-153">Basic</span><span class="sxs-lookup"><span data-stu-id="495f1-153">Basic</span></span>
<span data-ttu-id="495f1-154">Wanneer u selecteert **Basic**, de sjabloon wordt gemaakt met alle standaardwaarden waarden.</span><span class="sxs-lookup"><span data-stu-id="495f1-154">When you select **Basic**, the template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="495f1-155">Geavanceerd</span><span class="sxs-lookup"><span data-stu-id="495f1-155">Advanced</span></span>
<span data-ttu-id="495f1-156">Zie voor gedetailleerde uitleg over geavanceerde optie Widevine configuraties [dit](media-services-widevine-license-template-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="495f1-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="495f1-158">FairPlay-configuratie</span><span class="sxs-lookup"><span data-stu-id="495f1-158">FairPlay configuration</span></span>
<span data-ttu-id="495f1-159">FairPlay om versleuteling te schakelen, moet u het certificaat van de App en de toepassing geheime sleutel (vraag) bieden via de optie FairPlay-configuratie.</span><span class="sxs-lookup"><span data-stu-id="495f1-159">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option.</span></span> <span data-ttu-id="495f1-160">Zie voor gedetailleerde informatie over de vereisten en FairPlay configuratie [dit](media-services-protect-hls-with-fairplay.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="495f1-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-to-your-asset"></a><span data-ttu-id="495f1-162">Dynamische versleuteling toepassen op uw asset</span><span class="sxs-lookup"><span data-stu-id="495f1-162">Apply dynamic encryption to your asset</span></span>
<span data-ttu-id="495f1-163">Om te profiteren van dynamische versleuteling, moet u het bronbestand coderen in een set adaptive bitrate MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="495f1-163">To take advantage of dynamic encryption, you need to encode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-to-encrypt"></a><span data-ttu-id="495f1-164">Selecteer een asset die u wilt versleutelen</span><span class="sxs-lookup"><span data-stu-id="495f1-164">Select an asset that you want to encrypt</span></span>
<span data-ttu-id="495f1-165">Overzicht van alle uw assets selecteert **instellingen** > **activa**.</span><span class="sxs-lookup"><span data-stu-id="495f1-165">To see all your assets, select **Settings** > **Assets**.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="495f1-167">Versleutelen met AES of DRM</span><span class="sxs-lookup"><span data-stu-id="495f1-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="495f1-168">Indrukken **versleutelen** op een actief, krijgt u twee opties: **AES** of **DRM**.</span><span class="sxs-lookup"><span data-stu-id="495f1-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="495f1-169">AES</span><span class="sxs-lookup"><span data-stu-id="495f1-169">AES</span></span>
<span data-ttu-id="495f1-170">AES wissen sleutelcodering wordt ingeschakeld voor alle protocollen voor streaming: Smooth Streaming, HLS en MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="495f1-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="495f1-172">DRM</span><span class="sxs-lookup"><span data-stu-id="495f1-172">DRM</span></span>
<span data-ttu-id="495f1-173">Wanneer u het tabblad DRM selecteert, krijgt u verschillende mogelijkheden van het beleid van de beveiliging van inhoud (die u moet nu hebt geconfigureerd) + een reeks protocollen voor streaming.</span><span class="sxs-lookup"><span data-stu-id="495f1-173">When you select the DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="495f1-174">**PlayReady en Widevine met MPEG-DASH** -wordt uw MPEG-DASH-stream met PlayReady en Widevine DRM's dynamisch versleutelen.</span><span class="sxs-lookup"><span data-stu-id="495f1-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="495f1-175">**PlayReady en Widevine met MPEG-DASH + FairPlay met HLS** -wordt dynamisch versleutelen u MPEG-DASH-stroom met PlayReady en Widevine DRM's.</span><span class="sxs-lookup"><span data-stu-id="495f1-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="495f1-176">Uw HLS-streams met FairPlay zal ook worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="495f1-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="495f1-177">**PlayReady alleen met Smooth Streaming, HLS en MPEG-DASH** -wordt dynamisch versleutelen Smooth Streaming, HLS, MPEG-DASH-streams met PlayReady DRM.</span><span class="sxs-lookup"><span data-stu-id="495f1-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="495f1-178">**Widevine alleen met MPEG-DASH** -wordt dynamisch versleutelen u MPEG-DASH met Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="495f1-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="495f1-179">**FairPlay alleen met HLS** -wordt uw HLS-stream met FairPlay dynamisch versleutelen.</span><span class="sxs-lookup"><span data-stu-id="495f1-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="495f1-180">FairPlay om versleuteling te schakelen, moet u het certificaat van de App en de toepassing geheime sleutel (vraag) via de optie FairPlay configuratie van de beveiliging van inhoud-instellingenblade opgeven.</span><span class="sxs-lookup"><span data-stu-id="495f1-180">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option of the Content Protection settings blade.</span></span>

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="495f1-182">Wanneer u de versleutelingsselectie hebt gemaakt, drukt u op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="495f1-182">Once you make the encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="495f1-183">Als u van plan bent om af te spelen een AES HLS in Safari versleuteld, Zie [deze blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="495f1-183">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="495f1-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="495f1-184">Next steps</span></span>
<span data-ttu-id="495f1-185">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="495f1-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="495f1-186">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="495f1-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

