---
title: Het oplossen van problemen bestandscompressie in Azure CDN | Microsoft Docs
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
ms.openlocfilehash: 5ef8a8262eb40aa827161764f03a63d031e43273
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="0d02b-103">Problemen met CDN-bestandscompressie oplossen</span><span class="sxs-lookup"><span data-stu-id="0d02b-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="0d02b-104">Dit artikel helpt u problemen oplossen met [CDN bestandscompressie](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="0d02b-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="0d02b-105">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u de Azure-experts raadplegen op [de Azure MSDN en de Stack Overflow-forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="0d02b-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="0d02b-106">U kunt ook kunt u ook een incident voor ondersteuning van Azure bestand.</span><span class="sxs-lookup"><span data-stu-id="0d02b-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="0d02b-107">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en klik op **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="0d02b-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="0d02b-108">Symptoom</span><span class="sxs-lookup"><span data-stu-id="0d02b-108">Symptom</span></span>
<span data-ttu-id="0d02b-109">Compressie voor uw eindpunt is ingeschakeld, maar de bestanden niet-gecomprimeerde worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="0d02b-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="0d02b-110">Om te controleren of de bestanden worden geretourneerd gecomprimeerde, die u wilt gebruiken, een hulpprogramma zoals [Fiddler](http://www.telerik.com/fiddler) of uw browser [hulpprogramma's voor ontwikkelaars](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="0d02b-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="0d02b-111">Controleer de HTTP-antwoordheaders geretourneerd met uw cache CDN-inhoud.</span><span class="sxs-lookup"><span data-stu-id="0d02b-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="0d02b-112">Als er een header met de naam is `Content-Encoding` met een waarde van **gzip**, **bzip2**, of **deflate**, uw inhoud wordt gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="0d02b-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Inhoud-Encoding-header](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="0d02b-114">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="0d02b-114">Cause</span></span>
<span data-ttu-id="0d02b-115">Er zijn verschillende mogelijke oorzaken, inclusief:</span><span class="sxs-lookup"><span data-stu-id="0d02b-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="0d02b-116">De aangevraagde inhoud is niet in aanmerking komen voor compressie.</span><span class="sxs-lookup"><span data-stu-id="0d02b-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="0d02b-117">Compressie is niet ingeschakeld voor het aangevraagde type.</span><span class="sxs-lookup"><span data-stu-id="0d02b-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="0d02b-118">De HTTP-aanvraag bevat geen aanvragen van een geldige compressietype header.</span><span class="sxs-lookup"><span data-stu-id="0d02b-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="0d02b-119">Stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="0d02b-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="0d02b-120">Net als bij het implementeren van nieuwe eindpunten configuratiewijzigingen CDN enige tijd worden doorgegeven via het netwerk.</span><span class="sxs-lookup"><span data-stu-id="0d02b-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="0d02b-121">Normaal gesproken worden wijzigingen toegepast binnen 90 minuten.</span><span class="sxs-lookup"><span data-stu-id="0d02b-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="0d02b-122">Als dit de eerste keer dat u compressie voor uw CDN-eindpunt hebt ingesteld, kunt u overwegen 1 tot 2 uur wachten om er zeker van te zijn dat de instellingen zijn doorgegeven aan de POP's compressie.</span><span class="sxs-lookup"><span data-stu-id="0d02b-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="0d02b-123">Controleer of de aanvraag</span><span class="sxs-lookup"><span data-stu-id="0d02b-123">Verify the request</span></span>
<span data-ttu-id="0d02b-124">Er moet eerst een snelle controle van de aanvraag doen.</span><span class="sxs-lookup"><span data-stu-id="0d02b-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="0d02b-125">U kunt uw browser [hulpprogramma's voor ontwikkelaars](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) om de aanvragen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="0d02b-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="0d02b-126">Controleer of de aanvraag wordt verzonden naar uw eindpunt-URL, `<endpointname>.azureedge.net`, en niet uw oorsprong.</span><span class="sxs-lookup"><span data-stu-id="0d02b-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="0d02b-127">Controleer of de aanvraag bevat een **Accept-Encoding** header en de waarde voor deze koptekst bevat **gzip**, **deflate**, of **bzip2**.</span><span class="sxs-lookup"><span data-stu-id="0d02b-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="0d02b-128">**Azure CDN van Akamai** profielen alleen ondersteuning voor **gzip** codering.</span><span class="sxs-lookup"><span data-stu-id="0d02b-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![CDN-aanvraagheaders](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="0d02b-130">Controleer of de compressie-instellingen (standaard CDN-profiel)</span><span class="sxs-lookup"><span data-stu-id="0d02b-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="0d02b-131">Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN Standard van Verizon** of **Azure CDN Standard van Akamai** profiel.</span><span class="sxs-lookup"><span data-stu-id="0d02b-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="0d02b-132">Navigeer naar uw eindpunt in de [Azure-portal](https://portal.azure.com) en klik op de **configureren** knop.</span><span class="sxs-lookup"><span data-stu-id="0d02b-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="0d02b-133">Controleer of compressie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0d02b-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="0d02b-134">Controleer of het MIME-type voor de inhoud wordt gecomprimeerd is opgenomen in de lijst met gecomprimeerde indelingen.</span><span class="sxs-lookup"><span data-stu-id="0d02b-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN compressie-instellingen](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="0d02b-136">Controleer of de compressie-instellingen (Premium-CDN-profiel)</span><span class="sxs-lookup"><span data-stu-id="0d02b-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="0d02b-137">Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN Premium van Verizon** profiel.</span><span class="sxs-lookup"><span data-stu-id="0d02b-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="0d02b-138">Navigeer naar uw eindpunt in de [Azure-portal](https://portal.azure.com) en klik op de **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="0d02b-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="0d02b-139">De aanvullende portal wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="0d02b-139">The supplemental portal will open.</span></span>  <span data-ttu-id="0d02b-140">Beweeg de muisaanwijzer over de **HTTP grote** tabblad en klik vervolgens Beweeg de muisaanwijzer over de **Cache-instellingen** doel.</span><span class="sxs-lookup"><span data-stu-id="0d02b-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="0d02b-141">Klik op **compressie**.</span><span class="sxs-lookup"><span data-stu-id="0d02b-141">Click **Compression**.</span></span> 

* <span data-ttu-id="0d02b-142">Controleer of compressie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0d02b-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="0d02b-143">Controleer of de **bestandstypen** lijst bevat een lijst door komma's gescheiden (zonder spaties) met MIME-typen.</span><span class="sxs-lookup"><span data-stu-id="0d02b-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="0d02b-144">Controleer of het MIME-type voor de inhoud wordt gecomprimeerd is opgenomen in de lijst met gecomprimeerde indelingen.</span><span class="sxs-lookup"><span data-stu-id="0d02b-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN premium compressie-instellingen](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a><span data-ttu-id="0d02b-146">Controleer of dat de inhoud in cache wordt opgeslagen</span><span class="sxs-lookup"><span data-stu-id="0d02b-146">Verify the content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="0d02b-147">Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN van Verizon** profiel (Standard of Premium).</span><span class="sxs-lookup"><span data-stu-id="0d02b-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="0d02b-148">Controleer met ontwikkelhulpprogramma's van uw browser de antwoordheaders om te controleren of dat het bestand in cache wordt opgeslagen in de regio waar deze wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="0d02b-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="0d02b-149">Controleer de **Server** antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="0d02b-149">Check the **Server** response header.</span></span>  <span data-ttu-id="0d02b-150">De header moet de indeling **Platform (ID POP-Server)**, zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0d02b-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="0d02b-151">Controleer de **X-Cache** antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="0d02b-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="0d02b-152">De header moet worden gelezen **bereikt**.</span><span class="sxs-lookup"><span data-stu-id="0d02b-152">The header should read **HIT**.</span></span>  

![CDN-antwoordheaders](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a><span data-ttu-id="0d02b-154">Controleer of het bestand voldoet aan de vereiste grootte</span><span class="sxs-lookup"><span data-stu-id="0d02b-154">Verify the file meets the size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="0d02b-155">Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN van Verizon** profiel (Standard of Premium).</span><span class="sxs-lookup"><span data-stu-id="0d02b-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="0d02b-156">Als u in aanmerking komen voor compressie, een bestand moet voldoen aan de volgende vereiste grootte:</span><span class="sxs-lookup"><span data-stu-id="0d02b-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="0d02b-157">Groter zijn dan 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="0d02b-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="0d02b-158">Kleiner dan 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0d02b-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="0d02b-159">Controleer de aanvraag op de bronserver voor een **Via** koptekst</span><span class="sxs-lookup"><span data-stu-id="0d02b-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="0d02b-160">De **Via** HTTP-header wordt aangegeven dat de webserver dat de aanvraag wordt doorgegeven via een proxyserver.</span><span class="sxs-lookup"><span data-stu-id="0d02b-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="0d02b-161">Microsoft IIS-webservers standaard antwoorden niet comprimeren wanneer de aanvraag bevat een **Via** header.</span><span class="sxs-lookup"><span data-stu-id="0d02b-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="0d02b-162">Als u wilt dit gedrag negeren door het volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="0d02b-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="0d02b-163">**IIS 6**: [ingesteld HcNoCompressionForProxies = 'FALSE' in de IIS-Metabase-eigenschappen](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="0d02b-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="0d02b-164">**IIS 7 en hoger**: [zowel **noCompressionForHttp10** en **noCompressionForProxies** op False in de serverconfiguratie](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="0d02b-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

