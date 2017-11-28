---
title: aaaImprove prestaties door het comprimeren van bestanden in Azure CDN | Microsoft Docs
description: Meer informatie over hoe tooimprove bestandsoverdracht snelheid en toeneemt laadprestaties van de pagina door de bestanden in Azure CDN te comprimeren.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="a558e-103">De prestaties verbeteren door het comprimeren van bestanden in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a558e-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="a558e-104">Compressie is een eenvoudige en effectieve methode tooimprove bestand overdrachtssnelheid en de pagina load prestaties door het bestand voordat het verkleinen van Hallo-server wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="a558e-104">Compression is a simple and effective method tooimprove file transfer speed and increase page load performance by reducing file size before it is sent from hello server.</span></span> <span data-ttu-id="a558e-105">Het verlaagt de bandbreedtekosten en biedt een responsievere ervaring voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a558e-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="a558e-106">Er zijn twee manieren tooenable compressie:</span><span class="sxs-lookup"><span data-stu-id="a558e-106">There are two ways tooenable compression:</span></span>

* <span data-ttu-id="a558e-107">U kunt compressie inschakelen op uw server oorsprong in dat geval hello CDN passeren Hallo gecomprimeerde bestanden uit en levert tooclients gecomprimeerde bestanden die ze aanvragen.</span><span class="sxs-lookup"><span data-stu-id="a558e-107">You can enable compression on your origin server, in which case hello CDN passes through hello compressed files and deliver compressed files tooclients that request them.</span></span>
* <span data-ttu-id="a558e-108">U kunt compressie rechtstreeks op CDN randservers, waarin case Hallo CDN comprimeert Hallo van bestanden en dienen ze tooend gebruikers, zelfs als ze niet zijn gecomprimeerd door de bronserver Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a558e-108">You can enable compression directly on CDN edge servers, in which case hello CDN compresses hello files and serve them tooend users, even if they are not compressed by hello origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a558e-109">CDN-configuratiewijzigingen sommige toopropagate tijd via Hallo-netwerk.</span><span class="sxs-lookup"><span data-stu-id="a558e-109">CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="a558e-110">Voor <b>Azure CDN van Akamai</b> profielen, doorgeven voltooid gewoonlijk in onder één minuut.</span><span class="sxs-lookup"><span data-stu-id="a558e-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="a558e-111">Voor <b>Azure CDN van Verizon</b> profielen, meestal ziet u uw wijzigingen toepassen binnen 90 minuten.</span><span class="sxs-lookup"><span data-stu-id="a558e-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="a558e-112">Als dit Hallo eerst die u compressie voor uw CDN-eindpunt hebt ingesteld, moet u wachten op van 1 tot 2 uur toobe ervoor Hallo compressie-instellingen zijn doorgegeven toohello POP's voor het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="a558e-112">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="a558e-113">Compressie inschakelen</span><span class="sxs-lookup"><span data-stu-id="a558e-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="a558e-114">Hallo categorieën Standard en Premium-CDN bieden dezelfde functionaliteit voor compressie hello, maar hello gebruikersinterface verschilt.</span><span class="sxs-lookup"><span data-stu-id="a558e-114">hello Standard and Premium CDN tiers provide hello same compression functionality, but hello user interface differs.</span></span>  <span data-ttu-id="a558e-115">Zie voor meer informatie over de verschillen tussen de lagen Standard en Premium-CDN Hallo [overzicht van Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a558e-115">For more information about hello differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="a558e-116">Standaardlaag</span><span class="sxs-lookup"><span data-stu-id="a558e-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="a558e-117">Deze sectie geldt te**Azure CDN Standard van Verizon** en **Azure CDN Standard van Akamai** profielen.</span><span class="sxs-lookup"><span data-stu-id="a558e-117">This section applies too**Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="a558e-118">Klik op Hallo CDN-eindpunt gewenst toomanage Hallo CDN-profielpagina.</span><span class="sxs-lookup"><span data-stu-id="a558e-118">From hello CDN profile page, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![CDN-profiel pagina eindpunten](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="a558e-120">Hallo CDN-eindpunt pagina wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a558e-120">hello CDN endpoint page opens.</span></span>
2. <span data-ttu-id="a558e-121">Klik op Hallo **configureren** knop.</span><span class="sxs-lookup"><span data-stu-id="a558e-121">Click hello **Configure** button.</span></span>
   
    ![Knop pagina CDN-profiel beheren](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="a558e-123">Hallo CDN configuratiepagina wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a558e-123">hello CDN Configuration page opens.</span></span>
3. <span data-ttu-id="a558e-124">Schakel **compressie**.</span><span class="sxs-lookup"><span data-stu-id="a558e-124">Turn on **Compression**.</span></span>
   
    ![CDN-opties voor compressie](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="a558e-126">Gebruik de standaardtypen hello, of wijzig Hallo lijst door te verwijderen of toevoegen, bestandstypen.</span><span class="sxs-lookup"><span data-stu-id="a558e-126">Use hello default types, or modify hello list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="a558e-127">Tijdens mogelijk is, wordt het wordt niet aangeraden tooapply compressie toocompressed indelingen, zoals ZIP, MP3, MP4, JPG, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="a558e-127">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="a558e-128">Wanneer u klaar bent, klikt u op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a558e-128">After making your changes, click hello **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="a558e-129">Premiumlaag</span><span class="sxs-lookup"><span data-stu-id="a558e-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="a558e-130">Deze sectie geldt te**Azure CDN Premium van Verizon** profielen.</span><span class="sxs-lookup"><span data-stu-id="a558e-130">This section applies too**Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="a558e-131">Klik op Hallo Hallo CDN-profielpagina **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="a558e-131">From hello CDN profile page, click hello **Manage** button.</span></span>
   
    ![Knop pagina CDN-profiel beheren](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="a558e-133">Hallo CDN-beheerportal geopend.</span><span class="sxs-lookup"><span data-stu-id="a558e-133">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="a558e-134">Houd de muis boven Hallo **HTTP grote** tabblad en houd de muis boven Hallo **Cache-instellingen** doel.</span><span class="sxs-lookup"><span data-stu-id="a558e-134">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="a558e-135">Klik op **compressie**.</span><span class="sxs-lookup"><span data-stu-id="a558e-135">Click on **Compression**.</span></span>

    ![Compressie bestandsselectie](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="a558e-137">Opties voor compressie worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a558e-137">Compression options are displayed.</span></span>
   
    ![Bestandscompressie](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="a558e-139">Compressie inschakelen door te klikken op Hallo **compressie ingeschakeld** keuzerondje.</span><span class="sxs-lookup"><span data-stu-id="a558e-139">Enable compression by clicking hello **Compression Enabled** radio button.</span></span>  <span data-ttu-id="a558e-140">Voer Hallo MIME-typen gewenste toocompress als een door komma's gescheiden lijst met (zonder spaties) in Hallo **bestandstypen** textbox.</span><span class="sxs-lookup"><span data-stu-id="a558e-140">Enter hello MIME types you wish toocompress as a comma-delimited list (no spaces) in hello **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="a558e-141">Tijdens mogelijk is, wordt het wordt niet aangeraden tooapply compressie toocompressed indelingen, zoals ZIP, MP3, MP4, JPG, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="a558e-141">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="a558e-142">Wanneer u klaar bent, klikt u op Hallo **Update** knop.</span><span class="sxs-lookup"><span data-stu-id="a558e-142">After making your changes, click hello **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="a558e-143">Regels voor compressie</span><span class="sxs-lookup"><span data-stu-id="a558e-143">Compression rules</span></span>
<span data-ttu-id="a558e-144">Deze tabellen beschrijven Azure CDN compressie gedrag voor elk scenario.</span><span class="sxs-lookup"><span data-stu-id="a558e-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a558e-145">Voor **Azure CDN van Verizon** (standaard en Premium), alleen in aanmerking komende bestanden zijn gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="a558e-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="a558e-146">toobe in aanmerking komen voor compressie, een bestand moet:</span><span class="sxs-lookup"><span data-stu-id="a558e-146">toobe eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="a558e-147">Groter zijn dan 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="a558e-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="a558e-148">Kleiner dan 1 MB zijn.</span><span class="sxs-lookup"><span data-stu-id="a558e-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="a558e-149">Voor **Azure CDN van Akamai**, alle bestanden in aanmerking komen voor compressie.</span><span class="sxs-lookup"><span data-stu-id="a558e-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="a558e-150">Een bestand moet voor alle Azure CDN-producten, een MIME-type dat is [geconfigureerd voor compressie](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="a558e-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="a558e-151">**Azure CDN van Verizon** profielen (standaard en Premium) ondersteuning **gzip** (GNU zip), **deflate**, **bzip2**, of **br** codering (Brotli).</span><span class="sxs-lookup"><span data-stu-id="a558e-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="a558e-152">Hallo compressie wordt voor het coderen van Brotli alleen aan de rand van het Hallo gedaan.</span><span class="sxs-lookup"><span data-stu-id="a558e-152">For Brotli encoding, hello compression is done only at hello edge.</span></span> <span data-ttu-id="a558e-153">Hallo clientbrowser moet verzenden Hallo-aanvraag voor het coderen van Brotli en Hallo gecomprimeerde asset moet zijn gecomprimeerd Hallo oorsprong zijde eerst.</span><span class="sxs-lookup"><span data-stu-id="a558e-153">hello client/browser must send hello request for Brotli encoding and hello compressed asset must have been compressed on hello origin side first.</span></span> 
>
><span data-ttu-id="a558e-154">**Azure CDN van Akamai** profielen ondersteunen alleen **gzip** codering.</span><span class="sxs-lookup"><span data-stu-id="a558e-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="a558e-155">**Azure CDN van Akamai** eindpunten altijd aanvragen **gzip** gecodeerde bestanden vanuit de oorsprong hello, ongeacht het Hallo-clientaanvraag.</span><span class="sxs-lookup"><span data-stu-id="a558e-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from hello origin, regardless of hello client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="a558e-156">Compressie uitgeschakeld of het bestand is niet in aanmerking voor compressie</span><span class="sxs-lookup"><span data-stu-id="a558e-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="a558e-157">Aangevraagde indeling van de client (via de header Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="a558e-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="a558e-158">In de cache-bestandsindeling</span><span class="sxs-lookup"><span data-stu-id="a558e-158">Cached file format</span></span> | <span data-ttu-id="a558e-159">CDN-antwoord toohello client</span><span class="sxs-lookup"><span data-stu-id="a558e-159">CDN response toohello client</span></span> | <span data-ttu-id="a558e-160">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a558e-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a558e-161">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-161">Compressed</span></span> |<span data-ttu-id="a558e-162">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-162">Compressed</span></span> |<span data-ttu-id="a558e-163">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-163">Compressed</span></span> | |
| <span data-ttu-id="a558e-164">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-164">Compressed</span></span> |<span data-ttu-id="a558e-165">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-165">Uncompressed</span></span> |<span data-ttu-id="a558e-166">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-166">Uncompressed</span></span> | |
| <span data-ttu-id="a558e-167">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-167">Compressed</span></span> |<span data-ttu-id="a558e-168">Niet in cache</span><span class="sxs-lookup"><span data-stu-id="a558e-168">Not cached</span></span> |<span data-ttu-id="a558e-169">Wel of niet gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="a558e-170">Is afhankelijk van het antwoord van de oorsprong</span><span class="sxs-lookup"><span data-stu-id="a558e-170">Depends on origin response</span></span> |
| <span data-ttu-id="a558e-171">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-171">Uncompressed</span></span> |<span data-ttu-id="a558e-172">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-172">Compressed</span></span> |<span data-ttu-id="a558e-173">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-173">Uncompressed</span></span> | |
| <span data-ttu-id="a558e-174">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-174">Uncompressed</span></span> |<span data-ttu-id="a558e-175">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-175">Uncompressed</span></span> |<span data-ttu-id="a558e-176">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-176">Uncompressed</span></span> | |
| <span data-ttu-id="a558e-177">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-177">Uncompressed</span></span> |<span data-ttu-id="a558e-178">Niet in cache</span><span class="sxs-lookup"><span data-stu-id="a558e-178">Not cached</span></span> |<span data-ttu-id="a558e-179">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="a558e-180">Compressie is ingeschakeld en de bestandsnaam komt in aanmerking voor compressie</span><span class="sxs-lookup"><span data-stu-id="a558e-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="a558e-181">Aangevraagde indeling van de client (via de header Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="a558e-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="a558e-182">In de cache-bestandsindeling</span><span class="sxs-lookup"><span data-stu-id="a558e-182">Cached file format</span></span> | <span data-ttu-id="a558e-183">CDN-antwoord toohello client</span><span class="sxs-lookup"><span data-stu-id="a558e-183">CDN response toohello client</span></span> | <span data-ttu-id="a558e-184">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a558e-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a558e-185">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-185">Compressed</span></span> |<span data-ttu-id="a558e-186">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-186">Compressed</span></span> |<span data-ttu-id="a558e-187">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-187">Compressed</span></span> |<span data-ttu-id="a558e-188">CDN-transcodes tussen ondersteunde indelingen</span><span class="sxs-lookup"><span data-stu-id="a558e-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="a558e-189">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-189">Compressed</span></span> |<span data-ttu-id="a558e-190">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-190">Uncompressed</span></span> |<span data-ttu-id="a558e-191">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-191">Compressed</span></span> |<span data-ttu-id="a558e-192">CDN voert compressie</span><span class="sxs-lookup"><span data-stu-id="a558e-192">CDN performs compression</span></span> |
| <span data-ttu-id="a558e-193">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-193">Compressed</span></span> |<span data-ttu-id="a558e-194">Niet in cache</span><span class="sxs-lookup"><span data-stu-id="a558e-194">Not cached</span></span> |<span data-ttu-id="a558e-195">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-195">Compressed</span></span> |<span data-ttu-id="a558e-196">CDN uitvoert compressie als oorsprong niet-gecomprimeerde retourneert.</span><span class="sxs-lookup"><span data-stu-id="a558e-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="a558e-197">**Azure CDN van Verizon** geeft niet-gecomprimeerde bestand op de eerste aanvraag Hallo en vervolgens comprimeert Hallo en caches Hallo-bestand voor volgende aanvragen.</span><span class="sxs-lookup"><span data-stu-id="a558e-197">**Azure CDN from Verizon** passes hello uncompressed file on hello first request and then compresses and caches hello file for subsequent requests.</span></span>  <span data-ttu-id="a558e-198">Bestanden met `Cache-Control: no-cache` header nooit worden gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="a558e-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="a558e-199">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-199">Uncompressed</span></span> |<span data-ttu-id="a558e-200">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="a558e-200">Compressed</span></span> |<span data-ttu-id="a558e-201">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-201">Uncompressed</span></span> |<span data-ttu-id="a558e-202">CDN voert decompressie</span><span class="sxs-lookup"><span data-stu-id="a558e-202">CDN performs decompression</span></span> |
| <span data-ttu-id="a558e-203">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-203">Uncompressed</span></span> |<span data-ttu-id="a558e-204">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-204">Uncompressed</span></span> |<span data-ttu-id="a558e-205">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-205">Uncompressed</span></span> | |
| <span data-ttu-id="a558e-206">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-206">Uncompressed</span></span> |<span data-ttu-id="a558e-207">Niet in cache</span><span class="sxs-lookup"><span data-stu-id="a558e-207">Not cached</span></span> |<span data-ttu-id="a558e-208">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="a558e-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="a558e-209">Media Services-CDN-compressie</span><span class="sxs-lookup"><span data-stu-id="a558e-209">Media Services CDN Compression</span></span>
<span data-ttu-id="a558e-210">Voor Media Services CDN ingeschakeld streaming-eindpunten, compressie is standaard ingeschakeld voor Hallo typen inhoud te volgen: vnd.ms-toepassing-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, toepassing/f4m + xml.</span><span class="sxs-lookup"><span data-stu-id="a558e-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for hello following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="a558e-211">U kunt geen in-of uitschakelen compressie voor Hallo typen met behulp van hello Azure-portal vermeld.</span><span class="sxs-lookup"><span data-stu-id="a558e-211">You cannot enable/disable compression for hello mentioned types using hello Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="a558e-212">Zie ook</span><span class="sxs-lookup"><span data-stu-id="a558e-212">See also</span></span>
* [<span data-ttu-id="a558e-213">Problemen met CDN-bestandscompressie oplossen</span><span class="sxs-lookup"><span data-stu-id="a558e-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

