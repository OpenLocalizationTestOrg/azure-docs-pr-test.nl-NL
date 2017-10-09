---
title: aaaTroubleshooting bestandscompressie in Azure CDN | Microsoft Docs
description: Problemen oplossen met Azure CDN bestandscompressie.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="98f12-103">Problemen met CDN-bestandscompressie oplossen</span><span class="sxs-lookup"><span data-stu-id="98f12-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="98f12-104">Dit artikel helpt u problemen oplossen met [CDN bestandscompressie](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="98f12-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="98f12-105">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [hello Azure MSDN en forums Stack Overflow Hallo](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="98f12-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="98f12-106">U kunt ook kunt u ook een incident voor ondersteuning van Azure bestand.</span><span class="sxs-lookup"><span data-stu-id="98f12-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="98f12-107">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en klik op **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="98f12-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="98f12-108">Symptoom</span><span class="sxs-lookup"><span data-stu-id="98f12-108">Symptom</span></span>
<span data-ttu-id="98f12-109">Compressie voor uw eindpunt is ingeschakeld, maar de bestanden niet-gecomprimeerde worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="98f12-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="98f12-110">toocheck of de bestanden zijn gecomprimeerd wordt geretourneerd, moet u een hulpprogramma zoals toouse [Fiddler](http://www.telerik.com/fiddler) of uw browser [hulpprogramma's voor ontwikkelaars](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="98f12-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="98f12-111">Selectievakje Hallo HTTP-antwoordheaders geretourneerd met de CDN in de cache opgeslagen inhoud.</span><span class="sxs-lookup"><span data-stu-id="98f12-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="98f12-112">Als er een header met de naam is `Content-Encoding` met een waarde van **gzip**, **bzip2**, of **deflate**, uw inhoud wordt gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="98f12-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Inhoud-Encoding-header](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="98f12-114">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="98f12-114">Cause</span></span>
<span data-ttu-id="98f12-115">Er zijn verschillende mogelijke oorzaken, inclusief:</span><span class="sxs-lookup"><span data-stu-id="98f12-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="98f12-116">Hallo aangevraagde inhoud is niet in aanmerking komen voor compressie.</span><span class="sxs-lookup"><span data-stu-id="98f12-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="98f12-117">Compressie is niet ingeschakeld voor Hallo bestandstype aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="98f12-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="98f12-118">Hallo HTTP-aanvraag bevat geen aanvragen van een geldige compressietype header.</span><span class="sxs-lookup"><span data-stu-id="98f12-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="98f12-119">Stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="98f12-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="98f12-120">Net als bij het implementeren van nieuwe eindpunten configuratiewijzigingen CDN sommige toopropagate tijd via Hallo-netwerk.</span><span class="sxs-lookup"><span data-stu-id="98f12-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="98f12-121">Normaal gesproken worden wijzigingen toegepast binnen 90 minuten.</span><span class="sxs-lookup"><span data-stu-id="98f12-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="98f12-122">Als dit Hallo eerst die u compressie voor uw CDN-eindpunt hebt ingesteld, moet u wachten op van 1 tot 2 uur toobe ervoor Hallo compressie-instellingen toohello POP's zijn doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="98f12-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="98f12-123">Hallo aanvraag controleren</span><span class="sxs-lookup"><span data-stu-id="98f12-123">Verify hello request</span></span>
<span data-ttu-id="98f12-124">Eerst moet er een snelle controle op Hallo aanvraag doen.</span><span class="sxs-lookup"><span data-stu-id="98f12-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="98f12-125">U kunt uw browser [hulpprogramma's voor ontwikkelaars](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview Hallo-aanvragen worden gedaan.</span><span class="sxs-lookup"><span data-stu-id="98f12-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="98f12-126">Controleer of het Hallo-aanvraag wordt verzonden tooyour eindpunt-URL, `<endpointname>.azureedge.net`, en niet uw oorsprong.</span><span class="sxs-lookup"><span data-stu-id="98f12-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="98f12-127">Controleer of het Hallo-aanvraag bevat een **Accept-Encoding** header en het Hallo-waarde voor deze koptekst bevat **gzip**, **deflate**, of **bzip2** .</span><span class="sxs-lookup"><span data-stu-id="98f12-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="98f12-128">**Azure CDN van Akamai** profielen alleen ondersteuning voor **gzip** codering.</span><span class="sxs-lookup"><span data-stu-id="98f12-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![CDN-aanvraagheaders](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="98f12-130">Controleer of de compressie-instellingen (standaard CDN-profiel)</span><span class="sxs-lookup"><span data-stu-id="98f12-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="98f12-131">Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN Standard van Verizon** of **Azure CDN Standard van Akamai** profiel.</span><span class="sxs-lookup"><span data-stu-id="98f12-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="98f12-132">Navigeer tooyour eindpunt in Hallo [Azure-portal](https://portal.azure.com) en klik op Hallo **configureren** knop.</span><span class="sxs-lookup"><span data-stu-id="98f12-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="98f12-133">Controleer of compressie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="98f12-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="98f12-134">Controleer of Hallo MIME-type voor Hallo inhoud toobe gecomprimeerd is opgenomen in de lijst Hallo van gecomprimeerde indelingen.</span><span class="sxs-lookup"><span data-stu-id="98f12-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![CDN compressie-instellingen](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="98f12-136">Controleer of de compressie-instellingen (Premium-CDN-profiel)</span><span class="sxs-lookup"><span data-stu-id="98f12-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="98f12-137">Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN Premium van Verizon** profiel.</span><span class="sxs-lookup"><span data-stu-id="98f12-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="98f12-138">Navigeer tooyour eindpunt in Hallo [Azure-portal](https://portal.azure.com) en klik op Hallo **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="98f12-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="98f12-139">de aanvullende portal Hello wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="98f12-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="98f12-140">Houd de muis boven Hallo **HTTP grote** tabblad en houd de muis boven Hallo **Cache-instellingen** doel.</span><span class="sxs-lookup"><span data-stu-id="98f12-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="98f12-141">Klik op **compressie**.</span><span class="sxs-lookup"><span data-stu-id="98f12-141">Click **Compression**.</span></span> 

* <span data-ttu-id="98f12-142">Controleer of compressie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="98f12-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="98f12-143">Controleer of Hallo **bestandstypen** lijst bevat een lijst door komma's gescheiden (zonder spaties) met MIME-typen.</span><span class="sxs-lookup"><span data-stu-id="98f12-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="98f12-144">Controleer of Hallo MIME-type voor Hallo inhoud toobe gecomprimeerd is opgenomen in de lijst Hallo van gecomprimeerde indelingen.</span><span class="sxs-lookup"><span data-stu-id="98f12-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![CDN premium compressie-instellingen](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="98f12-146">Controleer of het Hallo-inhoud in cache wordt opgeslagen</span><span class="sxs-lookup"><span data-stu-id="98f12-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="98f12-147">Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN van Verizon** profiel (Standard of Premium).</span><span class="sxs-lookup"><span data-stu-id="98f12-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="98f12-148">Controleer met ontwikkelhulpprogramma's van uw browser Hallo headers tooensure Hallo responsbestand opgeslagen in de cache in Hallo regio waar deze wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="98f12-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="98f12-149">Controleer de Hallo **Server** antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="98f12-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="98f12-150">Hallo-header moet Hallo-indeling hebben **Platform (ID POP-Server)**, zoals in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="98f12-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="98f12-151">Controleer de Hallo **X-Cache** antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="98f12-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="98f12-152">Hallo-header moet worden gelezen **bereikt**.</span><span class="sxs-lookup"><span data-stu-id="98f12-152">hello header should read **HIT**.</span></span>  

![CDN-antwoordheaders](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="98f12-154">Controleer of het Hallo-bestand voldoet aan de vereiste grootte Hallo</span><span class="sxs-lookup"><span data-stu-id="98f12-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="98f12-155">Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN van Verizon** profiel (Standard of Premium).</span><span class="sxs-lookup"><span data-stu-id="98f12-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="98f12-156">toobe in aanmerking komen voor compressie, een bestand moet voldoen aan Hallo volgens de vereisten van de grootte:</span><span class="sxs-lookup"><span data-stu-id="98f12-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="98f12-157">Groter zijn dan 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="98f12-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="98f12-158">Kleiner dan 1 MB.</span><span class="sxs-lookup"><span data-stu-id="98f12-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="98f12-159">Controleer Hallo van de aanvraag op de bronserver Hallo voor een **Via** koptekst</span><span class="sxs-lookup"><span data-stu-id="98f12-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="98f12-160">Hallo **Via** HTTP-header aangeeft toohello-webserver die Hallo aanvraag wordt doorgegeven via een proxyserver.</span><span class="sxs-lookup"><span data-stu-id="98f12-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="98f12-161">Microsoft IIS-webservers standaard antwoorden niet comprimeren wanneer Hallo-aanvraag bevat een **Via** header.</span><span class="sxs-lookup"><span data-stu-id="98f12-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="98f12-162">toooverride dit gedrag Hallo volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="98f12-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="98f12-163">**IIS 6**: [ingesteld HcNoCompressionForProxies = 'FALSE' in de eigenschappen van de IIS-Metabase Hallo](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="98f12-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="98f12-164">**IIS 7 en hoger**: [zowel **noCompressionForHttp10** en **noCompressionForProxies** tooFalse in de serverconfiguratie Hallo](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="98f12-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

