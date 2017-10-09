---
title: aaaHybrid ontwerp van DRM subsystem(s) met Azure Media Services | Microsoft Docs
description: Dit onderwerp wordt besproken hybride ontwerp van DRM subsystem(s) met Azure Media Services.
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="1924b-103">Hybride ontwerp van DRM subsystem(s)</span><span class="sxs-lookup"><span data-stu-id="1924b-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="1924b-104">Dit onderwerp wordt besproken hybride ontwerp van DRM subsystem(s) met Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="1924b-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="1924b-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1924b-105">Overview</span></span>

<span data-ttu-id="1924b-106">Azure Media Services biedt ondersteuning voor Hallo drie DRM-systeem te volgen:</span><span class="sxs-lookup"><span data-stu-id="1924b-106">Azure Media Services provides support for hello following three DRM system:</span></span>

* <span data-ttu-id="1924b-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="1924b-107">PlayReady</span></span>
* <span data-ttu-id="1924b-108">Widevine (modulaire)</span><span class="sxs-lookup"><span data-stu-id="1924b-108">Widevine (Modular)</span></span>
* <span data-ttu-id="1924b-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="1924b-109">FairPlay</span></span>

<span data-ttu-id="1924b-110">Hallo DRM ondersteuning omvat DRM-versleuteling (dynamische versleuteling) en licentie-levering met Azure Media Player alle 3 DRM's ondersteunen als een browser speler SDK.</span><span class="sxs-lookup"><span data-stu-id="1924b-110">hello DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="1924b-111">Zie voor een uitgebreide behandeling van DRM/CENC subsysteem ontwerpen en implementeren, Hallo-document met de titel [CENC met Multi-DRM en toegangsbeheer](media-services-cenc-with-multidrm-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="1924b-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see hello document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="1924b-112">Hoewel we volledige ondersteuning voor drie DRM-systemen bieden, hoeven soms klanten toouse verschillende onderdelen van hun eigen infrastructuur/subsystemen in toevoeging tooAzure Media Services toobuild een hybride DRM-subsysteem.</span><span class="sxs-lookup"><span data-stu-id="1924b-112">Although we offer complete support for three DRM systems, sometimes customers need toouse various parts of their own infrastructure/subsystems in addition tooAzure Media Services toobuild a hybrid DRM subsystem.</span></span>

<span data-ttu-id="1924b-113">Hieronder worden enkele veelgestelde vragen gesteld door klanten:</span><span class="sxs-lookup"><span data-stu-id="1924b-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="1924b-114">"Kan ik mijn eigen DRM-licentieservers gebruiken?"</span><span class="sxs-lookup"><span data-stu-id="1924b-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="1924b-115">(In dit geval klanten hebben geïnvesteerd in DRM licentie-serverfarm met ingesloten bedrijfslogica).</span><span class="sxs-lookup"><span data-stu-id="1924b-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="1924b-116">'Kan ik gebruiken alleen levering van uw licentie DRM in Azure Media Services zonder het hosten van inhoud in AMS?'</span><span class="sxs-lookup"><span data-stu-id="1924b-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-hello-ams-drm-platform"></a><span data-ttu-id="1924b-117">Modulariteit Hallo DRM AMS-platform</span><span class="sxs-lookup"><span data-stu-id="1924b-117">Modularity of hello AMS DRM platform</span></span>

<span data-ttu-id="1924b-118">Als onderdeel van een uitgebreide video cloudplatform heeft Azure Media Services DRM een ontwerp met flexibiliteit en modulariteit in gedachten.</span><span class="sxs-lookup"><span data-stu-id="1924b-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="1924b-119">U kunt Azure Media Services gebruiken met een van de Hallo verschillende combinaties die worden beschreven in Hallo onderstaande tabel (een uitleg van Hallo notatie gebruikt in de tabel Hallo volgt) te volgen.</span><span class="sxs-lookup"><span data-stu-id="1924b-119">You can use Azure Media Services with any of hello following different combinations described in hello table below (an explanation of hello notation used in hello table follows).</span></span> 

|<span data-ttu-id="1924b-120">**Inhoud die als host fungeert & oorsprong**</span><span class="sxs-lookup"><span data-stu-id="1924b-120">**Content hosting & origin**</span></span>|<span data-ttu-id="1924b-121">**Versleuteling van inhoud**</span><span class="sxs-lookup"><span data-stu-id="1924b-121">**Content encryption**</span></span>|<span data-ttu-id="1924b-122">**Levering van DRM-licentie**</span><span class="sxs-lookup"><span data-stu-id="1924b-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="1924b-123">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-123">AMS</span></span>|<span data-ttu-id="1924b-124">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-124">AMS</span></span>|<span data-ttu-id="1924b-125">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-125">AMS</span></span>|
|<span data-ttu-id="1924b-126">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-126">AMS</span></span>|<span data-ttu-id="1924b-127">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-127">AMS</span></span>|<span data-ttu-id="1924b-128">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-128">Third-party</span></span>|
|<span data-ttu-id="1924b-129">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-129">AMS</span></span>|<span data-ttu-id="1924b-130">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-130">Third-party</span></span>|<span data-ttu-id="1924b-131">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-131">AMS</span></span>|
|<span data-ttu-id="1924b-132">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-132">AMS</span></span>|<span data-ttu-id="1924b-133">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-133">Third-party</span></span>|<span data-ttu-id="1924b-134">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-134">Third-party</span></span>|
|<span data-ttu-id="1924b-135">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-135">Third-party</span></span>|<span data-ttu-id="1924b-136">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-136">Third-party</span></span>|<span data-ttu-id="1924b-137">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="1924b-138">Inhoud die als host fungeert & oorsprong</span><span class="sxs-lookup"><span data-stu-id="1924b-138">Content hosting & origin</span></span>

* <span data-ttu-id="1924b-139">AMS: video asset wordt gehost in AMS en streaming is via AMS streaming-eindpunten (maar niet noodzakelijkerwijs dynamische pakketten).</span><span class="sxs-lookup"><span data-stu-id="1924b-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="1924b-140">Derde: video is gehost en op een derde partij streaming platform buiten AMS geleverd.</span><span class="sxs-lookup"><span data-stu-id="1924b-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="1924b-141">Versleuteling van inhoud</span><span class="sxs-lookup"><span data-stu-id="1924b-141">Content encryption</span></span>

* <span data-ttu-id="1924b-142">AMS: versleuteling van inhoud is uitgevoerd dynamisch/op aanvraag door AMS dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="1924b-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="1924b-143">Derde partij: versleuteling van inhoud wordt uitgevoerd buiten de AMS met een vooraf verwerken van de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="1924b-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="1924b-144">Levering van DRM-licentie</span><span class="sxs-lookup"><span data-stu-id="1924b-144">DRM license delivery</span></span>

* <span data-ttu-id="1924b-145">AMS: DRM-licentie is geleverd door de AMS-licentieservice levering.</span><span class="sxs-lookup"><span data-stu-id="1924b-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="1924b-146">Derde: DRM-licentie wordt geleverd door een derde partij DRM-licentieserver buiten AMS.</span><span class="sxs-lookup"><span data-stu-id="1924b-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="1924b-147">Configureren op basis van uw hybride scenario</span><span class="sxs-lookup"><span data-stu-id="1924b-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="1924b-148">Inhoudssleutel</span><span class="sxs-lookup"><span data-stu-id="1924b-148">Content key</span></span>

<span data-ttu-id="1924b-149">Door de configuratie van een inhoudssleutel, kunt u bepalen Hallo kenmerken van zowel AMS dynamische versleuteling en AMS-licentieservice levering te volgen:</span><span class="sxs-lookup"><span data-stu-id="1924b-149">Through configuration of a content key, you can control hello following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="1924b-150">Hallo-inhoudssleutel voor dynamische DRM versleuteling gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1924b-150">hello content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="1924b-151">DRM licentie inhoud toobe geleverd door de services voor het leveren van licenties: rechten, inhoudssleutel en beperkingen.</span><span class="sxs-lookup"><span data-stu-id="1924b-151">DRM license content toobe delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="1924b-152">Type **inhoud autorisatiebeleid beleidsbeperking**: openen, IP- of tokenbeperking.</span><span class="sxs-lookup"><span data-stu-id="1924b-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="1924b-153">Als **token** type **autorisatiebeleid beleidsbeperking wordt gebruikt**, Hallo **inhoud autorisatiebeleid beleidsbeperking** moet worden voldaan voordat een licentie wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="1924b-153">If **token** type of **content key authorization policy restriction is used**, hello **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="1924b-154">Leveringsbeleid voor Assets</span><span class="sxs-lookup"><span data-stu-id="1924b-154">Asset delivery policy</span></span>

<span data-ttu-id="1924b-155">Door de configuratie van een leveringsbeleid voor Assets, kunt u bepalen Hallo kenmerken die worden gebruikt door dynamische packager AMS en dynamische versleuteling van een streaming-eindpunt AMS te volgen:</span><span class="sxs-lookup"><span data-stu-id="1924b-155">Through configuration of an asset delivery policy, you can control hello following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="1924b-156">Streaming-protocol en DRM versleuteling combinatie, zoals DASH onder CENC (PlayReady en Widevine), vloeiend streaming onder PlayReady, HLS met PlayReady- of Widevine.</span><span class="sxs-lookup"><span data-stu-id="1924b-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="1924b-157">Hallo standaard/ingesloten licentie levering van URL's voor elk Hallo betrokken DRM's.</span><span class="sxs-lookup"><span data-stu-id="1924b-157">hello default/embedded license delivery URLs for each of hello involved DRMs.</span></span>
* <span data-ttu-id="1924b-158">Licentie-of overname URL's (LA_URLs) in MPD DASH of HLS afspeellijst queryreeks van sleutel-ID (KID) bevatten voor Widevine en FairPlay, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="1924b-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="1924b-159">Scenario's en voorbeelden</span><span class="sxs-lookup"><span data-stu-id="1924b-159">Scenarios and samples</span></span>

<span data-ttu-id="1924b-160">Op basis van Hallo uitleg in de vorige sectie hello, Hallo na vijf hybride scenario's gebruiken respectieve **inhoudssleutel**-**leveringsbeleid voor Assets** configuratiecombinaties (Hallo voorbeelden die worden vermeld in de laatste kolom Hallo Volg Hallo tabel):</span><span class="sxs-lookup"><span data-stu-id="1924b-160">Based on hello explanations in hello previous section, hello following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (hello samples mentioned in hello last column follow hello table):</span></span>

|<span data-ttu-id="1924b-161">**Inhoud die als host fungeert & oorsprong**</span><span class="sxs-lookup"><span data-stu-id="1924b-161">**Content hosting & origin**</span></span>|<span data-ttu-id="1924b-162">**DRM-versleuteling**</span><span class="sxs-lookup"><span data-stu-id="1924b-162">**DRM encryption**</span></span>|<span data-ttu-id="1924b-163">**Levering van DRM-licentie**</span><span class="sxs-lookup"><span data-stu-id="1924b-163">**DRM license delivery**</span></span>|<span data-ttu-id="1924b-164">**Inhoudssleutel configureren**</span><span class="sxs-lookup"><span data-stu-id="1924b-164">**Configure content key**</span></span>|<span data-ttu-id="1924b-165">**Leveringsbeleid voor Assets configureren**</span><span class="sxs-lookup"><span data-stu-id="1924b-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="1924b-166">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="1924b-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="1924b-167">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-167">AMS</span></span>|<span data-ttu-id="1924b-168">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-168">AMS</span></span>|<span data-ttu-id="1924b-169">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-169">AMS</span></span>|<span data-ttu-id="1924b-170">Ja</span><span class="sxs-lookup"><span data-stu-id="1924b-170">Yes</span></span>|<span data-ttu-id="1924b-171">Ja</span><span class="sxs-lookup"><span data-stu-id="1924b-171">Yes</span></span>|<span data-ttu-id="1924b-172">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="1924b-172">Sample 1</span></span>|
|<span data-ttu-id="1924b-173">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-173">AMS</span></span>|<span data-ttu-id="1924b-174">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-174">AMS</span></span>|<span data-ttu-id="1924b-175">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-175">Third-party</span></span>|<span data-ttu-id="1924b-176">Ja</span><span class="sxs-lookup"><span data-stu-id="1924b-176">Yes</span></span>|<span data-ttu-id="1924b-177">Ja</span><span class="sxs-lookup"><span data-stu-id="1924b-177">Yes</span></span>|<span data-ttu-id="1924b-178">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="1924b-178">Sample 2</span></span>|
|<span data-ttu-id="1924b-179">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-179">AMS</span></span>|<span data-ttu-id="1924b-180">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-180">Third-party</span></span>|<span data-ttu-id="1924b-181">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-181">AMS</span></span>|<span data-ttu-id="1924b-182">Ja</span><span class="sxs-lookup"><span data-stu-id="1924b-182">Yes</span></span>|<span data-ttu-id="1924b-183">Nee</span><span class="sxs-lookup"><span data-stu-id="1924b-183">No</span></span>|<span data-ttu-id="1924b-184">Voorbeeld 3</span><span class="sxs-lookup"><span data-stu-id="1924b-184">Sample 3</span></span>|
|<span data-ttu-id="1924b-185">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-185">AMS</span></span>|<span data-ttu-id="1924b-186">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-186">Third-party</span></span>|<span data-ttu-id="1924b-187">Buiten</span><span class="sxs-lookup"><span data-stu-id="1924b-187">Outside</span></span>|<span data-ttu-id="1924b-188">Nee</span><span class="sxs-lookup"><span data-stu-id="1924b-188">No</span></span>|<span data-ttu-id="1924b-189">Nee</span><span class="sxs-lookup"><span data-stu-id="1924b-189">No</span></span>|<span data-ttu-id="1924b-190">Voorbeeld 4</span><span class="sxs-lookup"><span data-stu-id="1924b-190">Sample 4</span></span>|
|<span data-ttu-id="1924b-191">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-191">Third-party</span></span>|<span data-ttu-id="1924b-192">Van derden</span><span class="sxs-lookup"><span data-stu-id="1924b-192">Third-party</span></span>|<span data-ttu-id="1924b-193">AMS</span><span class="sxs-lookup"><span data-stu-id="1924b-193">AMS</span></span>|<span data-ttu-id="1924b-194">Ja</span><span class="sxs-lookup"><span data-stu-id="1924b-194">Yes</span></span>|<span data-ttu-id="1924b-195">Nee</span><span class="sxs-lookup"><span data-stu-id="1924b-195">No</span></span>|    

<span data-ttu-id="1924b-196">In de voorbeelden van Hallo werkt PlayReady-beveiliging voor DASH en smooth streaming.</span><span class="sxs-lookup"><span data-stu-id="1924b-196">In hello samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="1924b-197">Hallo video-URL's hieronder zijn smooth streaming-URL's.</span><span class="sxs-lookup"><span data-stu-id="1924b-197">hello video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="1924b-198">tooget Hallo bijbehorende DASH-URL's, net toevoegen ' (format = mpd-time-csf) '.</span><span class="sxs-lookup"><span data-stu-id="1924b-198">tooget hello corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="1924b-199">U kunt Hallo [azure media player testen](http://aka.ms/amtest) tootest in een browser.</span><span class="sxs-lookup"><span data-stu-id="1924b-199">You could use hello [azure media test player](http://aka.ms/amtest) tootest in a browser.</span></span> <span data-ttu-id="1924b-200">Hiermee kunt u tooconfigure die protocol toouse, onder welke tech streaming.</span><span class="sxs-lookup"><span data-stu-id="1924b-200">It allows you tooconfigure which streaming protocol toouse, under which tech.</span></span> <span data-ttu-id="1924b-201">Ondersteuning voor PlayReady via EME IE11 en MS-Edge van Windows 10.</span><span class="sxs-lookup"><span data-stu-id="1924b-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="1924b-202">Zie voor meer informatie [details over Hallo testen hulpprogramma](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span><span class="sxs-lookup"><span data-stu-id="1924b-202">For more information, see [details about hello test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="1924b-203">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="1924b-203">Sample 1</span></span>

* <span data-ttu-id="1924b-204">Bron-URL (basis): https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="1924b-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="1924b-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="1924b-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="1924b-206">Widevine-LA_URL (KOPPELTEKEN): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="1924b-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="1924b-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="1924b-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="1924b-208">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="1924b-208">Sample 2</span></span>

* <span data-ttu-id="1924b-209">Bron-URL (basis): http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="1924b-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="1924b-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="1924b-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="1924b-211">Voorbeeld 3</span><span class="sxs-lookup"><span data-stu-id="1924b-211">Sample 3</span></span>

* <span data-ttu-id="1924b-212">Bron-URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="1924b-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="1924b-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="1924b-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="1924b-214">Voorbeeld 4</span><span class="sxs-lookup"><span data-stu-id="1924b-214">Sample 4</span></span>

* <span data-ttu-id="1924b-215">Bron-URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="1924b-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="1924b-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="1924b-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="1924b-217">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="1924b-217">Summary</span></span>

<span data-ttu-id="1924b-218">Kortom, Azure Media Services DRM-componenten flexibel zijn, kunt u ze in een hybride scenario door te configureren inhoudssleutel en leveringsbeleid voor Assets, zoals beschreven in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="1924b-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1924b-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1924b-219">Next steps</span></span>
<span data-ttu-id="1924b-220">Weergave Media Services-leertrajecten.</span><span class="sxs-lookup"><span data-stu-id="1924b-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1924b-221">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="1924b-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

