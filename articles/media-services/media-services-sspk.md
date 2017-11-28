---
title: "Microsoft® Smooth Streaming Client overdragen Kit aaaLicensing"
description: "Meer informatie over hoe toolicensing Hallo Microsoft® Smooth Streaming Client overdragen Kit."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="77d3a-103">Licentieverlening Microsoft® Smooth Streaming Client Kit overdragen</span><span class="sxs-lookup"><span data-stu-id="77d3a-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="77d3a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="77d3a-104">Overview</span></span>
<span data-ttu-id="77d3a-105">Microsoft Smooth Streaming Client overdragen Kit (**SSPK** voor korte) is een Smooth Streaming clientimplementatie die is geoptimaliseerd toohelp ingesloten fabrikanten, kabel en mobiele operators, inhoud serviceproviders, telefoon fabrikanten, onafhankelijke softwareleveranciers (ISV's) en solution providers toocreate producten en services voor streaming adaptieve streaming inhoud in Smooth Streaming-indeling.</span><span class="sxs-lookup"><span data-stu-id="77d3a-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized toohelp embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers toocreate products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="77d3a-106">SSPK is een onafhankelijke implementatie voor apparaten en platforms van Smooth Streaming-client die kan worden geïmplementeerd door Hallo licentiehouder tooany apparaten en platforms.</span><span class="sxs-lookup"><span data-stu-id="77d3a-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by hello licensee tooany device and platform.</span></span> 

<span data-ttu-id="77d3a-107">Hieronder vindt u een hoog niveau architectuur is en IIS Smooth Streaming overdragen Kit in is Hallo Smooth Streaming Client implementatie geleverd door Microsoft en bevat alle Hallo corelogica voor het afspelen van inhoud Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="77d3a-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is hello Smooth Streaming Client implementation provided by Microsoft and includes all hello core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="77d3a-108">Dit wordt vervolgens door partners voor een specifiek apparaat of platform overgezet door het juiste interfaces implementeren.</span><span class="sxs-lookup"><span data-stu-id="77d3a-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="77d3a-110">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="77d3a-110">Description</span></span>
<span data-ttu-id="77d3a-111">SSPK is in licentie gegeven op voorwaarden die worden geboden door uitstekende bedrijfswaarde.</span><span class="sxs-lookup"><span data-stu-id="77d3a-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="77d3a-112">SSPK licentie biedt Hallo industrie met:</span><span class="sxs-lookup"><span data-stu-id="77d3a-112">SSPK license provides hello industry with:</span></span>

* <span data-ttu-id="77d3a-113">Smooth Streaming overdragen Kit-bron in C++</span><span class="sxs-lookup"><span data-stu-id="77d3a-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="77d3a-114">functionaliteit Smooth Streaming Client implementeert</span><span class="sxs-lookup"><span data-stu-id="77d3a-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="77d3a-115">voegt indeling parseren, methodiek, buffer logica, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="77d3a-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="77d3a-116">Spelertoepassing API 's</span><span class="sxs-lookup"><span data-stu-id="77d3a-116">Player application APIs</span></span> 
  * <span data-ttu-id="77d3a-117">API's voor interactie met een media player-toepassing</span><span class="sxs-lookup"><span data-stu-id="77d3a-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="77d3a-118">Platform Abstraction Layer (PAL)-Interface</span><span class="sxs-lookup"><span data-stu-id="77d3a-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="77d3a-119">API's voor interactie met Hallo besturingssysteem (threads, sockets)</span><span class="sxs-lookup"><span data-stu-id="77d3a-119">programming interfaces for interaction with hello operating system (threads, sockets)</span></span>
* <span data-ttu-id="77d3a-120">Hardware Abstraction Layer (HAL)-Interface</span><span class="sxs-lookup"><span data-stu-id="77d3a-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="77d3a-121">programming interfaces voor interactie met hardware A / V decoders (decoderen, rendering)</span><span class="sxs-lookup"><span data-stu-id="77d3a-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="77d3a-122">Beheerinterface van digitale rechten (DRM)</span><span class="sxs-lookup"><span data-stu-id="77d3a-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="77d3a-123">API's voor het verwerken van DRM via Hallo DRM Abstraction Layer (DAL)</span><span class="sxs-lookup"><span data-stu-id="77d3a-123">programming interfaces for handling DRM through hello DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="77d3a-124">Microsoft PlayReady overdragen Kit wordt afzonderlijk worden geleverd, maar kan worden geïntegreerd via deze interface.</span><span class="sxs-lookup"><span data-stu-id="77d3a-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="77d3a-125">Klik voor meer informatie over licenties voor Microsoft PlayReady Device [hier](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="77d3a-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="77d3a-126">Implementatie-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="77d3a-126">Implementation samples</span></span> 
  * <span data-ttu-id="77d3a-127">Voorbeeldimplementatie PAL voor Linux</span><span class="sxs-lookup"><span data-stu-id="77d3a-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="77d3a-128">Voorbeeldimplementatie HAL voor GStreamer</span><span class="sxs-lookup"><span data-stu-id="77d3a-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="77d3a-129">Licentieopties</span><span class="sxs-lookup"><span data-stu-id="77d3a-129">Licensing Options</span></span>
<span data-ttu-id="77d3a-130">Microsoft Smooth Streaming Client overdragen Kit toolicensees beschikbaar wordt gemaakt onder twee afzonderlijke licentieovereenkomsten: één voor het ontwikkelen van Smooth Streaming Client Interim-producten en andere voor het distribueren van Smooth Streaming Client eindproducten tooend gebruikers.</span><span class="sxs-lookup"><span data-stu-id="77d3a-130">Microsoft Smooth Streaming Client Porting Kit is made available toolicensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products tooend users.</span></span>

* <span data-ttu-id="77d3a-131">Voor chipsetfabrikanten, systeemintegrators of independent software vendors (ISV's) die behoefte hebben aan een bron code overdragen toodevelop Interim-producten, een Microsoft Smooth Streaming Client overdragen Kit kit **Interim productlicentie** moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit toodevelop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="77d3a-132">Voor fabrikanten of ISV's die behoefte hebben aan distributierechten voor Smooth Streaming Client eindproducten tooend gebruikers, Hallo Microsoft Smooth Streaming Client overdragen Kit **laatste productlicentie** moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products tooend users, hello Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="77d3a-133">Microsoft Smooth Streaming Client Kit Interim productlicentie overdragen</span><span class="sxs-lookup"><span data-stu-id="77d3a-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="77d3a-134">Onder deze licentie Microsoft biedt een Smooth Streaming Client overdragen Kit en Hallo nodig intellectueel eigendom rechten toodevelop en distribueren Smooth Streaming Client Interim producten tooother Smooth Streaming Client overdragen Kit apparaat licentiehouders die Smooth Streaming Client eindproducten distribueren.</span><span class="sxs-lookup"><span data-stu-id="77d3a-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and hello necessary intellectual property rights toodevelop and distribute Smooth Streaming Client Interim Products tooother Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="77d3a-135">Kostenstructuur</span><span class="sxs-lookup"><span data-stu-id="77d3a-135">Fee structure</span></span>
<span data-ttu-id="77d3a-136">Een VS 50.000 eenmalige licentiekosten biedt toegang tot toohello Smooth Streaming Client overdragen Kit.</span><span class="sxs-lookup"><span data-stu-id="77d3a-136">A U.S. $50,000 one-time license fee provides access toohello Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="77d3a-137">Microsoft Smooth Streaming Client Kit Final productlicentie overdragen</span><span class="sxs-lookup"><span data-stu-id="77d3a-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="77d3a-138">Microsoft biedt onder deze licentie alle nodige intellectueel eigendom rechten tooreceive Smooth Streaming Client Interim producten van andere Smooth Streaming Client overdragen Kit licentiehouders en de huisstijl van het bedrijf Smooth Streaming Client laatste toodistribute Producten tooend gebruikers.</span><span class="sxs-lookup"><span data-stu-id="77d3a-138">Under this license, Microsoft offers all necessary intellectual property rights tooreceive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and toodistribute company-branded Smooth Streaming Client Final Products tooend users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="77d3a-139">Kostenstructuur</span><span class="sxs-lookup"><span data-stu-id="77d3a-139">Fee structure</span></span>
<span data-ttu-id="77d3a-140">Hallo Smooth Streaming Client uiteindelijke Product wordt aangeboden onder een model royalty als onder:</span><span class="sxs-lookup"><span data-stu-id="77d3a-140">hello Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="77d3a-141">$0.10 per apparaat uitvoering is verzonden</span><span class="sxs-lookup"><span data-stu-id="77d3a-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="77d3a-142">Hallo royalty is beperkt tot 50.000 jaarlijks</span><span class="sxs-lookup"><span data-stu-id="77d3a-142">hello royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="77d3a-143">Er is geen royalty voor eerste 10.000 apparaat implementaties jaarlijks</span><span class="sxs-lookup"><span data-stu-id="77d3a-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="77d3a-144">Licentieverlening Procedure en SSPK toegang</span><span class="sxs-lookup"><span data-stu-id="77d3a-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="77d3a-145">Stuur een e-mail [ sspkinfo@microsoft.com ](mailto:sspkinfo@microsoft.com) licentieverlening voor alle query's.</span><span class="sxs-lookup"><span data-stu-id="77d3a-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="77d3a-146">Hallo [SSPK distributie portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) toegankelijk tooregistered Interim licentiehouders is.</span><span class="sxs-lookup"><span data-stu-id="77d3a-146">hello [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible tooregistered Interim licensees.</span></span>

<span data-ttu-id="77d3a-147">Tussentijdse en definitieve SSPK licentiehouders technische vragen te kunnen indienen[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="77d3a-147">Interim and Final SSPK licensees can submit technical questions too[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="77d3a-148">Microsoft Smooth Streaming Client tussentijdse Product overeenkomst licentiehouders</span><span class="sxs-lookup"><span data-stu-id="77d3a-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="77d3a-149">Adroit Business oplossingen, Inc</span><span class="sxs-lookup"><span data-stu-id="77d3a-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="77d3a-150">Geavanceerde digitale uitzending SA</span><span class="sxs-lookup"><span data-stu-id="77d3a-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="77d3a-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret W.S.</span><span class="sxs-lookup"><span data-stu-id="77d3a-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="77d3a-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="77d3a-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-153">Alticast Corporation</span></span>
* <span data-ttu-id="77d3a-154">Amazon digitale Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="77d3a-155">Arion-technologie, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="77d3a-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="77d3a-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-157">Cavium, Inc.</span></span>
* <span data-ttu-id="77d3a-158">EchoStar aanschaffen Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="77d3a-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-159">Enseo, Inc.</span></span>
* <span data-ttu-id="77d3a-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="77d3a-160">Fluendo S.A.</span></span>
* <span data-ttu-id="77d3a-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="77d3a-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="77d3a-162">Infomir GMBH</span></span>
* <span data-ttu-id="77d3a-163">Irdeto Verenigde Staten Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="77d3a-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="77d3a-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="77d3a-165">Liberty globale Services BW</span><span class="sxs-lookup"><span data-stu-id="77d3a-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="77d3a-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-166">MediaTek Inc.</span></span>
* <span data-ttu-id="77d3a-167">MStar Co Ltd</span><span class="sxs-lookup"><span data-stu-id="77d3a-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="77d3a-168">NINTENDO Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="77d3a-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="77d3a-170">Saffraan digitale beperkt</span><span class="sxs-lookup"><span data-stu-id="77d3a-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="77d3a-171">Sichuan Changhong elektrische Co. Ltd</span><span class="sxs-lookup"><span data-stu-id="77d3a-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="77d3a-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="77d3a-172">SoftAtHome</span></span>
* <span data-ttu-id="77d3a-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-173">Sony Corporation</span></span>
* <span data-ttu-id="77d3a-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="77d3a-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="77d3a-176">Top overwinning investeringen, Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="77d3a-177">Vestel Elektronik Sanayi ve Ticaret W.S.</span><span class="sxs-lookup"><span data-stu-id="77d3a-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="77d3a-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="77d3a-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="77d3a-180">Microsoft Smooth Streaming Client uiteindelijke Product overeenkomst licentiehouders</span><span class="sxs-lookup"><span data-stu-id="77d3a-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="77d3a-181">Geavanceerde digitale uitzending SA</span><span class="sxs-lookup"><span data-stu-id="77d3a-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="77d3a-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret W.S.</span><span class="sxs-lookup"><span data-stu-id="77d3a-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="77d3a-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="77d3a-184">Amazon digitale Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="77d3a-185">AmTRAN technologie Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="77d3a-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="77d3a-187">Arion-technologie, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="77d3a-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="77d3a-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="77d3a-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="77d3a-189">VE TİC.</span></span> <span data-ttu-id="77d3a-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="77d3a-190">A.Ş</span></span>
* <span data-ttu-id="77d3a-191">Brits Sky Broadcasting beperkt</span><span class="sxs-lookup"><span data-stu-id="77d3a-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="77d3a-192">CastPal Technology Inc. Shenzhen</span><span class="sxs-lookup"><span data-stu-id="77d3a-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="77d3a-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="77d3a-194">Dongguan digitale AV-technologie Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="77d3a-195">EchoStar aanschaffen Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="77d3a-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-196">Enseo, Inc.</span></span>
* <span data-ttu-id="77d3a-197">Filmflex films beperkt</span><span class="sxs-lookup"><span data-stu-id="77d3a-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="77d3a-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="77d3a-198">Fluendo S.A.</span></span>
* <span data-ttu-id="77d3a-199">Gibson innovaties beperkt</span><span class="sxs-lookup"><span data-stu-id="77d3a-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="77d3a-200">Haier informatie Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="77d3a-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="77d3a-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="77d3a-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="77d3a-203">Homecast Co. Ltd</span><span class="sxs-lookup"><span data-stu-id="77d3a-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="77d3a-204">Hon Hai precisie bedrijfstak Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="77d3a-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="77d3a-205">Infomir GMBH</span></span>
* <span data-ttu-id="77d3a-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="77d3a-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-207">KDDI Corporation</span></span>
* <span data-ttu-id="77d3a-208">NINTENDO Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="77d3a-209">Oranje SA</span><span class="sxs-lookup"><span data-stu-id="77d3a-209">Orange SA</span></span>
* <span data-ttu-id="77d3a-210">Saffraan digitale beperkt</span><span class="sxs-lookup"><span data-stu-id="77d3a-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="77d3a-211">Sagemcom breedband SAS</span><span class="sxs-lookup"><span data-stu-id="77d3a-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="77d3a-212">Shenzhen Coship Electronics CO. LTD</span><span class="sxs-lookup"><span data-stu-id="77d3a-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="77d3a-213">Shenzhen Jiuzhou elektrische Co. Ltd</span><span class="sxs-lookup"><span data-stu-id="77d3a-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="77d3a-214">Shenzhen Skyworth digitale technologie Co. Ltd</span><span class="sxs-lookup"><span data-stu-id="77d3a-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="77d3a-215">Sichuan Changhong elektrische Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="77d3a-216">Skardin industriële Corp.</span><span class="sxs-lookup"><span data-stu-id="77d3a-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="77d3a-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="77d3a-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="77d3a-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="77d3a-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="77d3a-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="77d3a-219">SoftAtHome</span></span>
* <span data-ttu-id="77d3a-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-220">Sony Corporation</span></span>
* <span data-ttu-id="77d3a-221">Beperkte TCL overzeese Marketing (Offshore Macau commerciële)</span><span class="sxs-lookup"><span data-stu-id="77d3a-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="77d3a-222">Technicolor levering technologieën, SAS</span><span class="sxs-lookup"><span data-stu-id="77d3a-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="77d3a-223">Tongfang globale Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="77d3a-224">Top overwinning investeringen, Ltd.</span><span class="sxs-lookup"><span data-stu-id="77d3a-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="77d3a-225">Toshiba Lifestyle-producten en Services Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="77d3a-226">Universele Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="77d3a-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="77d3a-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="77d3a-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="77d3a-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-228">Wistron Corporation</span></span>
* <span data-ttu-id="77d3a-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="77d3a-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="77d3a-230">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="77d3a-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="77d3a-231">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="77d3a-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

