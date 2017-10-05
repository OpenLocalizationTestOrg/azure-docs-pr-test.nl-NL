---
title: De prestaties verbeteren door het comprimeren van bestanden in Azure CDN | Microsoft Docs
description: Informatie over het verbeteren van bestand overdrachtssnelheid en verhoogt de laadprestaties van de pagina door de bestanden in Azure CDN te comprimeren.
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
ms.openlocfilehash: 7546650e6096a880f4fb4d0c94dd4ecc00b70160
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="1fc6d-103">De prestaties verbeteren door het comprimeren van bestanden in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="1fc6d-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="1fc6d-104">Compressie is een eenvoudige en effectieve methode voor het verbeteren van bestand overdrachtssnelheid en laadprestaties van de pagina vergroten door bestandscompressie voordat deze wordt verzonden van de server.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span></span> <span data-ttu-id="1fc6d-105">Het verlaagt de bandbreedtekosten en biedt een responsievere ervaring voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="1fc6d-106">Er zijn twee manieren compressie inschakelen:</span><span class="sxs-lookup"><span data-stu-id="1fc6d-106">There are two ways to enable compression:</span></span>

* <span data-ttu-id="1fc6d-107">Als u compressie inschakelen op uw bronserver waarin geval de CDN naar de gecomprimeerde bestanden passeert en gecomprimeerde bestanden leveren aan clients die deze aanvragen.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-107">You can enable compression on your origin server, in which case the CDN passes through the compressed files and deliver compressed files to clients that request them.</span></span>
* <span data-ttu-id="1fc6d-108">Als u compressie inschakelen rechtstreeks op de CDN-randservers in dat geval de CDN de bestanden comprimeren en leveren aan eindgebruikers, zelfs als ze niet zijn gecomprimeerd door de bronserver.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-108">You can enable compression directly on CDN edge servers, in which case the CDN compresses the files and serve them to end users, even if they are not compressed by the origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1fc6d-109">CDN-configuratiewijzigingen enige tijd worden doorgegeven via het netwerk.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-109">CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="1fc6d-110">Voor <b>Azure CDN van Akamai</b> profielen, doorgeven voltooid gewoonlijk in onder één minuut.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="1fc6d-111">Voor <b>Azure CDN van Verizon</b> profielen, meestal ziet u uw wijzigingen toepassen binnen 90 minuten.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="1fc6d-112">Als dit de eerste keer dat u compressie voor uw CDN-eindpunt hebt ingesteld, kunt u overwegen 1 tot 2 uur wachten om er zeker van te zijn dat de instellingen zijn doorgegeven aan de POP's voor het oplossen van problemen compressie</span><span class="sxs-lookup"><span data-stu-id="1fc6d-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="1fc6d-113">Compressie inschakelen</span><span class="sxs-lookup"><span data-stu-id="1fc6d-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="1fc6d-114">De categorieën Standard en Premium-CDN bieden dezelfde functionaliteit compressie, maar de gebruikersinterface verschilt.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span></span>  <span data-ttu-id="1fc6d-115">Zie voor meer informatie over de verschillen tussen de categorieën Standard en Premium-CDN [overzicht van Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1fc6d-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="1fc6d-116">Standaardlaag</span><span class="sxs-lookup"><span data-stu-id="1fc6d-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="1fc6d-117">Deze sectie geldt voor **Azure CDN Standard van Verizon** en **Azure CDN Standard van Akamai** profielen.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="1fc6d-118">Klik op het CDN-eindpunt dat u wilt beheren via de pagina CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-118">From the CDN profile page, click the CDN endpoint you wish to manage.</span></span>
   
    ![CDN-profiel pagina eindpunten](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="1fc6d-120">De pagina CDN-eindpunt wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-120">The CDN endpoint page opens.</span></span>
2. <span data-ttu-id="1fc6d-121">Klik op de **configureren** knop.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-121">Click the **Configure** button.</span></span>
   
    ![Knop pagina CDN-profiel beheren](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="1fc6d-123">De pagina configuratie van CDN wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-123">The CDN Configuration page opens.</span></span>
3. <span data-ttu-id="1fc6d-124">Schakel **compressie**.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-124">Turn on **Compression**.</span></span>
   
    ![CDN-opties voor compressie](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="1fc6d-126">Gebruik de standaardtypen of wijzigt u de lijst door te verwijderen of toevoegen, bestandstypen.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-126">Use the default types, or modify the list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1fc6d-127">Tijdens mogelijk niet verdient compressie toepassen op gecomprimeerde indelingen, zoals ZIP, MP3, MP4, JPG, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="1fc6d-128">Wanneer u klaar bent, klikt u op de **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-128">After making your changes, click the **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="1fc6d-129">Premiumlaag</span><span class="sxs-lookup"><span data-stu-id="1fc6d-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="1fc6d-130">Deze sectie geldt voor **Azure CDN Premium van Verizon** profielen.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="1fc6d-131">Klik op de pagina CDN-profiel de **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-131">From the CDN profile page, click the **Manage** button.</span></span>
   
    ![Knop pagina CDN-profiel beheren](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="1fc6d-133">Hiermee opent u de CDN-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-133">The CDN management portal opens.</span></span>
2. <span data-ttu-id="1fc6d-134">Beweeg de muisaanwijzer over de **HTTP grote** tabblad en klik vervolgens Beweeg de muisaanwijzer over de **Cache-instellingen** doel.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="1fc6d-135">Klik op **compressie**.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-135">Click on **Compression**.</span></span>

    ![Compressie bestandsselectie](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="1fc6d-137">Opties voor compressie worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-137">Compression options are displayed.</span></span>
   
    ![Bestandscompressie](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="1fc6d-139">Compressie inschakelen door te klikken op de **compressie ingeschakeld** keuzerondje.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-139">Enable compression by clicking the **Compression Enabled** radio button.</span></span>  <span data-ttu-id="1fc6d-140">Voer de MIME-typen die u wilt comprimeren als een door komma's gescheiden lijst (zonder spaties) in de **bestandstypen** textbox.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-140">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1fc6d-141">Tijdens mogelijk niet verdient compressie toepassen op gecomprimeerde indelingen, zoals ZIP, MP3, MP4, JPG, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-141">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="1fc6d-142">Wanneer u klaar bent, klikt u op de **Update** knop.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-142">After making your changes, click the **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="1fc6d-143">Regels voor compressie</span><span class="sxs-lookup"><span data-stu-id="1fc6d-143">Compression rules</span></span>
<span data-ttu-id="1fc6d-144">Deze tabellen beschrijven Azure CDN compressie gedrag voor elk scenario.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1fc6d-145">Voor **Azure CDN van Verizon** (standaard en Premium), alleen in aanmerking komende bestanden zijn gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="1fc6d-146">Als u in aanmerking komen voor compressie, moet een bestand:</span><span class="sxs-lookup"><span data-stu-id="1fc6d-146">To be eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="1fc6d-147">Groter zijn dan 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="1fc6d-148">Kleiner dan 1 MB zijn.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="1fc6d-149">Voor **Azure CDN van Akamai**, alle bestanden in aanmerking komen voor compressie.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="1fc6d-150">Een bestand moet voor alle Azure CDN-producten, een MIME-type dat is [geconfigureerd voor compressie](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="1fc6d-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="1fc6d-151">**Azure CDN van Verizon** profielen (standaard en Premium) ondersteuning **gzip** (GNU zip), **deflate**, **bzip2**, of **br** codering (Brotli).</span><span class="sxs-lookup"><span data-stu-id="1fc6d-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="1fc6d-152">De compressie is gedaan voor het coderen van Brotli alleen aan de rand.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-152">For Brotli encoding, the compression is done only at the edge.</span></span> <span data-ttu-id="1fc6d-153">De aanvraag voor het coderen van Brotli door de clientbrowser moet verzenden en het gecomprimeerde actief moet zijn gecomprimeerd aan de kant van de oorsprong eerst.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-153">The client/browser must send the request for Brotli encoding and the compressed asset must have been compressed on the origin side first.</span></span> 
>
><span data-ttu-id="1fc6d-154">**Azure CDN van Akamai** profielen ondersteunen alleen **gzip** codering.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="1fc6d-155">**Azure CDN van Akamai** eindpunten altijd aanvragen **gzip** gecodeerde bestanden vanuit de oorsprong, ongeacht de clientaanvraag.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="1fc6d-156">Compressie uitgeschakeld of het bestand is niet in aanmerking voor compressie</span><span class="sxs-lookup"><span data-stu-id="1fc6d-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="1fc6d-157">Aangevraagde indeling van de client (via de header Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="1fc6d-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="1fc6d-158">In de cache-bestandsindeling</span><span class="sxs-lookup"><span data-stu-id="1fc6d-158">Cached file format</span></span> | <span data-ttu-id="1fc6d-159">CDN-antwoord naar de client</span><span class="sxs-lookup"><span data-stu-id="1fc6d-159">CDN response to the client</span></span> | <span data-ttu-id="1fc6d-160">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1fc6d-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1fc6d-161">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-161">Compressed</span></span> |<span data-ttu-id="1fc6d-162">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-162">Compressed</span></span> |<span data-ttu-id="1fc6d-163">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-163">Compressed</span></span> | |
| <span data-ttu-id="1fc6d-164">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-164">Compressed</span></span> |<span data-ttu-id="1fc6d-165">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-165">Uncompressed</span></span> |<span data-ttu-id="1fc6d-166">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-166">Uncompressed</span></span> | |
| <span data-ttu-id="1fc6d-167">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-167">Compressed</span></span> |<span data-ttu-id="1fc6d-168">Niet in cache</span><span class="sxs-lookup"><span data-stu-id="1fc6d-168">Not cached</span></span> |<span data-ttu-id="1fc6d-169">Wel of niet gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="1fc6d-170">Is afhankelijk van het antwoord van de oorsprong</span><span class="sxs-lookup"><span data-stu-id="1fc6d-170">Depends on origin response</span></span> |
| <span data-ttu-id="1fc6d-171">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-171">Uncompressed</span></span> |<span data-ttu-id="1fc6d-172">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-172">Compressed</span></span> |<span data-ttu-id="1fc6d-173">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-173">Uncompressed</span></span> | |
| <span data-ttu-id="1fc6d-174">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-174">Uncompressed</span></span> |<span data-ttu-id="1fc6d-175">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-175">Uncompressed</span></span> |<span data-ttu-id="1fc6d-176">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-176">Uncompressed</span></span> | |
| <span data-ttu-id="1fc6d-177">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-177">Uncompressed</span></span> |<span data-ttu-id="1fc6d-178">Niet in cache</span><span class="sxs-lookup"><span data-stu-id="1fc6d-178">Not cached</span></span> |<span data-ttu-id="1fc6d-179">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="1fc6d-180">Compressie is ingeschakeld en de bestandsnaam komt in aanmerking voor compressie</span><span class="sxs-lookup"><span data-stu-id="1fc6d-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="1fc6d-181">Aangevraagde indeling van de client (via de header Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="1fc6d-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="1fc6d-182">In de cache-bestandsindeling</span><span class="sxs-lookup"><span data-stu-id="1fc6d-182">Cached file format</span></span> | <span data-ttu-id="1fc6d-183">CDN-antwoord naar de client</span><span class="sxs-lookup"><span data-stu-id="1fc6d-183">CDN response to the client</span></span> | <span data-ttu-id="1fc6d-184">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1fc6d-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1fc6d-185">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-185">Compressed</span></span> |<span data-ttu-id="1fc6d-186">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-186">Compressed</span></span> |<span data-ttu-id="1fc6d-187">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-187">Compressed</span></span> |<span data-ttu-id="1fc6d-188">CDN-transcodes tussen ondersteunde indelingen</span><span class="sxs-lookup"><span data-stu-id="1fc6d-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="1fc6d-189">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-189">Compressed</span></span> |<span data-ttu-id="1fc6d-190">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-190">Uncompressed</span></span> |<span data-ttu-id="1fc6d-191">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-191">Compressed</span></span> |<span data-ttu-id="1fc6d-192">CDN voert compressie</span><span class="sxs-lookup"><span data-stu-id="1fc6d-192">CDN performs compression</span></span> |
| <span data-ttu-id="1fc6d-193">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-193">Compressed</span></span> |<span data-ttu-id="1fc6d-194">Niet in cache</span><span class="sxs-lookup"><span data-stu-id="1fc6d-194">Not cached</span></span> |<span data-ttu-id="1fc6d-195">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-195">Compressed</span></span> |<span data-ttu-id="1fc6d-196">CDN uitvoert compressie als oorsprong niet-gecomprimeerde retourneert.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="1fc6d-197">**Azure CDN van Verizon** niet-gecomprimeerde bestand op de eerste aanvraag wordt doorgegeven en vervolgens worden gecomprimeerd en slaat het bestand voor volgende aanvragen.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-197">**Azure CDN from Verizon** passes the uncompressed file on the first request and then compresses and caches the file for subsequent requests.</span></span>  <span data-ttu-id="1fc6d-198">Bestanden met `Cache-Control: no-cache` header nooit worden gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="1fc6d-199">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-199">Uncompressed</span></span> |<span data-ttu-id="1fc6d-200">Gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="1fc6d-200">Compressed</span></span> |<span data-ttu-id="1fc6d-201">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-201">Uncompressed</span></span> |<span data-ttu-id="1fc6d-202">CDN voert decompressie</span><span class="sxs-lookup"><span data-stu-id="1fc6d-202">CDN performs decompression</span></span> |
| <span data-ttu-id="1fc6d-203">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-203">Uncompressed</span></span> |<span data-ttu-id="1fc6d-204">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-204">Uncompressed</span></span> |<span data-ttu-id="1fc6d-205">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-205">Uncompressed</span></span> | |
| <span data-ttu-id="1fc6d-206">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-206">Uncompressed</span></span> |<span data-ttu-id="1fc6d-207">Niet in cache</span><span class="sxs-lookup"><span data-stu-id="1fc6d-207">Not cached</span></span> |<span data-ttu-id="1fc6d-208">Niet-gecomprimeerde</span><span class="sxs-lookup"><span data-stu-id="1fc6d-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="1fc6d-209">Media Services-CDN-compressie</span><span class="sxs-lookup"><span data-stu-id="1fc6d-209">Media Services CDN Compression</span></span>
<span data-ttu-id="1fc6d-210">Voor Media Services CDN ingeschakeld streaming-eindpunten, compressie is standaard ingeschakeld voor de volgende inhoudstypen: vnd.ms-toepassing-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, toepassing/f4m + xml.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="1fc6d-211">U kunt geen in-of uitschakelen compressie voor de genoemde typen met de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1fc6d-211">You cannot enable/disable compression for the mentioned types using the Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="1fc6d-212">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1fc6d-212">See also</span></span>
* [<span data-ttu-id="1fc6d-213">Problemen met CDN-bestandscompressie oplossen</span><span class="sxs-lookup"><span data-stu-id="1fc6d-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

