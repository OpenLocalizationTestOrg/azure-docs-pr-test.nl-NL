---
title: aaaAzure Media Services invoer metagegevensschema | Microsoft Docs
description: Hallo onderwerp overzicht een van de invoer metagegevensschema Azure Media Services.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a><span data-ttu-id="a1dbc-103">Invoer metagegevens</span><span class="sxs-lookup"><span data-stu-id="a1dbc-103">Input Metadata</span></span>
<span data-ttu-id="a1dbc-104">Een codeertaak is gekoppeld aan een invoer asset (of activa) waarop tooperform sommige taken codering.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-104">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span>  <span data-ttu-id="a1dbc-105">Na voltooiing van een taak wordt een uitvoerasset geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="a1dbc-106">Hallo uitvoerasset video, audio, miniatuurweergaven manifest bevat, enz. Hallo uitvoerasset bevat ook een bestand met metagegevens over Hallo invoer asset.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-106">hello output asset contains video, audio, thumbnails, manifest, etc. hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="a1dbc-107">Hallo naam van XML-bestand met metagegevens Hallo heeft Hallo volgende indeling: &lt;asset_id&gt;_metadata.xml (bijvoorbeeld 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), waarbij &lt;asset_id&gt; Hallo item-id hebt is de waarde van Hallo invoer actief.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-107">hello name of hello metadata XML file has hello following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is hello AssetId value of hello input asset.</span></span>  

<span data-ttu-id="a1dbc-108">Als u tooexamine Hallo metagegevensbestand wilt, kunt u een **SAS** locator en downloaden Hallo bestand tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-108">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="a1dbc-109">U kunt een voorbeeld vinden over het toocreate een SAS-locator en downloaden van een bestand [Hallo Media Services .NET SDK Extensions met](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-109">You can find an example on how toocreate a SAS locator and download a file  [Using hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="a1dbc-110">Dit onderwerp wordt besproken Hallo-elementen en typen van Hallo XML-schema op welke invoer metada hello (&lt;asset_id&gt;_metadata.xml) is gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-110">This topic discusses hello elements and types of hello XML schema on which hello input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="a1dbc-111">Zie voor meer informatie over het Hallo-bestand met metagegevens over Hallo uitvoerasset [uitvoer metagegevens](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-111">For information about hello file that contains metadata about hello output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="a1dbc-112">U vindt Hallo [Schema Code](media-services-input-metadata-schema.md#code) een [XML-voorbeeld](media-services-input-metadata-schema.md#xml) aan Hallo einde van dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-112">You can find hello [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at hello end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="a1dbc-113"><a name="AssetFiles"></a>AssetFiles-element (element root)</span><span class="sxs-lookup"><span data-stu-id="a1dbc-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="a1dbc-114">Bevat een verzameling [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s voor Hallo coderingstaak.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for hello encoding job.</span></span>  

<span data-ttu-id="a1dbc-115">Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-115">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="a1dbc-116">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-116">Name</span></span> | <span data-ttu-id="a1dbc-117">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a1dbc-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="a1dbc-119">minOccurs = "1" maxOccurs = 'unbounded'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="a1dbc-120">Een één onderliggend element.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-120">A single child element.</span></span> <span data-ttu-id="a1dbc-121">Zie voor meer informatie [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="a1dbc-122"><a name="AssetFile"></a>AssetFile element</span><span class="sxs-lookup"><span data-stu-id="a1dbc-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="a1dbc-123">Kenmerken en elementen die beschrijving van een assetbestand bevat.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="a1dbc-124">Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-124">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a1dbc-125">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="a1dbc-125">Attributes</span></span>
| <span data-ttu-id="a1dbc-126">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-126">Name</span></span> | <span data-ttu-id="a1dbc-127">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-127">Type</span></span> | <span data-ttu-id="a1dbc-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-129">**Naam**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-129">**Name**</span></span><br /><br /> <span data-ttu-id="a1dbc-130">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-130">Required</span></span> |<span data-ttu-id="a1dbc-131">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-131">**xs:string**</span></span> |<span data-ttu-id="a1dbc-132">Asset-bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-132">Asset file name.</span></span> |
| <span data-ttu-id="a1dbc-133">**Grootte**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-133">**Size**</span></span><br /><br /> <span data-ttu-id="a1dbc-134">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-134">Required</span></span> |<span data-ttu-id="a1dbc-135">**xs:Long**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-135">**xs:long**</span></span> |<span data-ttu-id="a1dbc-136">Grootte van Hallo asset bestandsgrootte in bytes.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="a1dbc-137">**Duur**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-137">**Duration**</span></span><br /><br /> <span data-ttu-id="a1dbc-138">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-138">Required</span></span> |<span data-ttu-id="a1dbc-139">**xs: duration**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-139">**xs:duration**</span></span> |<span data-ttu-id="a1dbc-140">Inhoud afspelen back duur.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-140">Content play back duration.</span></span> <span data-ttu-id="a1dbc-141">Voorbeeld: Duur = 'PT25M37.757S'.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="a1dbc-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="a1dbc-143">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-143">Required</span></span> |<span data-ttu-id="a1dbc-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-144">**xs:int**</span></span> |<span data-ttu-id="a1dbc-145">Aantal gegevensstromen in Hallo assetbestand.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-145">Number of streams in hello asset file.</span></span> |
| <span data-ttu-id="a1dbc-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="a1dbc-147">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-147">Required</span></span> |<span data-ttu-id="a1dbc-148">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-148">**xs:string**</span></span> |<span data-ttu-id="a1dbc-149">Indelingsnamen.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-149">Format names.</span></span> |
| <span data-ttu-id="a1dbc-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="a1dbc-151">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-151">Required</span></span> |<span data-ttu-id="a1dbc-152">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-152">**xs:string**</span></span> |<span data-ttu-id="a1dbc-153">Uitgebreide indelingsnamen.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-153">Format verbose names.</span></span> |
| <span data-ttu-id="a1dbc-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-154">**StartTime**</span></span> |<span data-ttu-id="a1dbc-155">**xs: duration**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-155">**xs:duration**</span></span> |<span data-ttu-id="a1dbc-156">Begintijd van inhoud.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-156">Content start time.</span></span> <span data-ttu-id="a1dbc-157">Voorbeeld: StartTime = 'PT2.669S'.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="a1dbc-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-158">**OverallBitRate**</span></span> |<span data-ttu-id="a1dbc-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-159">**xs:int**</span></span> |<span data-ttu-id="a1dbc-160">Gemiddelde bitrate van Hallo asset-bestand in kbps.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-160">Average bitrate of hello asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="a1dbc-161">Hallo na 4 onderliggende elementen moet worden weergegeven in een reeks.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-161">hello following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="a1dbc-162">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="a1dbc-162">Child elements</span></span>
| <span data-ttu-id="a1dbc-163">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-163">Name</span></span> | <span data-ttu-id="a1dbc-164">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-164">Type</span></span> | <span data-ttu-id="a1dbc-165">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-166">**Programma 's**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-166">**Programs**</span></span><br /><br /> <span data-ttu-id="a1dbc-167">minOccurs = '0'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-167">minOccurs="0"</span></span> | |<span data-ttu-id="a1dbc-168">Verzameling van alle [programma's element](media-services-input-metadata-schema.md#Programs) wanneer Hallo assetbestand heeft MPEG-TS-indeling.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when hello asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="a1dbc-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="a1dbc-170">minOccurs = '0'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-170">minOccurs="0"</span></span> | |<span data-ttu-id="a1dbc-171">Elk bestand fysiek activum kan nul of meer video houdt interleaved naar een indeling voor de juiste container bevatten.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="a1dbc-172">Dit element bevat een verzameling van alle [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) die deel uitmaken van Hallo assetbestand.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="a1dbc-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="a1dbc-174">minOccurs = '0'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-174">minOccurs="0"</span></span> | |<span data-ttu-id="a1dbc-175">Elk bestand fysiek activum kan nul of meer audio houdt interleaved naar een indeling voor de juiste container bevatten.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="a1dbc-176">Dit element bevat een verzameling van alle [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) die deel uitmaken van Hallo assetbestand.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="a1dbc-177">**Metagegevens**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="a1dbc-178">minOccurs = "0" maxOccurs = 'unbounded'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="a1dbc-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="a1dbc-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="a1dbc-180">De metagegevens van assetbestand weergegeven als key\value tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="a1dbc-181">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a1dbc-181">For example:</span></span><br /><br /> <span data-ttu-id="a1dbc-182">**&lt;Metagegevenssleutel = waarde 'taal' = 'eng' /&gt;**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="a1dbc-183"><a name="TrackType"></a>TrackType</span><span class="sxs-lookup"><span data-stu-id="a1dbc-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="a1dbc-184">Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-184">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a1dbc-185">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="a1dbc-185">Attributes</span></span>
| <span data-ttu-id="a1dbc-186">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-186">Name</span></span> | <span data-ttu-id="a1dbc-187">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-187">Type</span></span> | <span data-ttu-id="a1dbc-188">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-189">**ID**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-189">**Id**</span></span><br /><br /> <span data-ttu-id="a1dbc-190">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-190">Required</span></span> |<span data-ttu-id="a1dbc-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-191">**xs:int**</span></span> |<span data-ttu-id="a1dbc-192">Op nul gebaseerde index van dit audio- of -nummer.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="a1dbc-193">Dit is niet noodzakelijkerwijs dat Hallo TrackID zoals gebruikt in een MP4-bestand.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-193">This is not necessarily that hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="a1dbc-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-194">**Codec**</span></span> |<span data-ttu-id="a1dbc-195">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-195">**xs:string**</span></span> |<span data-ttu-id="a1dbc-196">Video bijhouden codec tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-196">Video track codec string.</span></span> |
| <span data-ttu-id="a1dbc-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-197">**CodecLongName**</span></span> |<span data-ttu-id="a1dbc-198">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-198">**xs:string**</span></span> |<span data-ttu-id="a1dbc-199">Audio- of bijhouden codec lange naam.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="a1dbc-200">**Tijdsbasis**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="a1dbc-201">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-201">Required</span></span> |<span data-ttu-id="a1dbc-202">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-202">**xs:string**</span></span> |<span data-ttu-id="a1dbc-203">Basis.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-203">Time base.</span></span> <span data-ttu-id="a1dbc-204">Voorbeeld: Tijdsbasis = ' 1/48000'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="a1dbc-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-205">**NumberOfFrames**</span></span> |<span data-ttu-id="a1dbc-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-206">**xs:int**</span></span> |<span data-ttu-id="a1dbc-207">Aantal frames (aanwezig voor video houdt).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="a1dbc-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-208">**StartTime**</span></span> |<span data-ttu-id="a1dbc-209">**xs: duration**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-209">**xs:duration**</span></span> |<span data-ttu-id="a1dbc-210">Begintijd bijhouden.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-210">Track start time.</span></span> <span data-ttu-id="a1dbc-211">Voorbeeld: StartTime = "PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="a1dbc-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="a1dbc-212">**Duur**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-212">**Duration**</span></span> |<span data-ttu-id="a1dbc-213">**xs: duration**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-213">**xs:duration**</span></span> |<span data-ttu-id="a1dbc-214">Duur bijhouden.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-214">Track duration.</span></span> <span data-ttu-id="a1dbc-215">Voorbeeld: Duur = 'PTSampleFormat M37.757S'.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="a1dbc-216">Hallo na 2 onderliggende elementen moet worden weergegeven in een reeks.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-216">hello following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="a1dbc-217">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="a1dbc-217">Child elements</span></span>
| <span data-ttu-id="a1dbc-218">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-218">Name</span></span> | <span data-ttu-id="a1dbc-219">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-219">Type</span></span> | <span data-ttu-id="a1dbc-220">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-221">**Toestand**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="a1dbc-222">minOccurs = "0" maxOccurs = '1'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="a1dbc-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="a1dbc-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="a1dbc-224">Bevat presentatie-informatie (bijvoorbeeld, of een bepaalde-nummer is voor een visuele handicap viewers).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="a1dbc-225">**Metagegevens**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="a1dbc-226">minOccurs = "0" maxOccurs = 'unbounded'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="a1dbc-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="a1dbc-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="a1dbc-228">Algemene sleutel/waarde-tekenreeksen die gebruikt toohold tal van informatie worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-228">Generic key/value strings that can be used toohold a variety of information.</span></span> <span data-ttu-id="a1dbc-229">Bijvoorbeeld, sleutel = 'taal' en waarde = 'eng'.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="a1dbc-230"><a name="AudioTrackType"></a>AudioTrackType (neemt over van TrackType)</span><span class="sxs-lookup"><span data-stu-id="a1dbc-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="a1dbc-231">**AudioTrackType** is globale complex type die eigenschappen van overneemt [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="a1dbc-232">Hallo type vertegenwoordigt een specifieke-nummer in Hallo assetbestand.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-232">hello type represents a specific audio track in hello asset file.</span></span>  

 <span data-ttu-id="a1dbc-233">Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-233">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a1dbc-234">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="a1dbc-234">Attributes</span></span>
| <span data-ttu-id="a1dbc-235">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-235">Name</span></span> | <span data-ttu-id="a1dbc-236">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-236">Type</span></span> | <span data-ttu-id="a1dbc-237">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-238">**SampleFormat**</span></span> |<span data-ttu-id="a1dbc-239">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-239">**xs:string**</span></span> |<span data-ttu-id="a1dbc-240">Voorbeeld-indeling.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-240">Sample format.</span></span> |
| <span data-ttu-id="a1dbc-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-241">**ChannelLayout**</span></span> |<span data-ttu-id="a1dbc-242">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-242">**xs:string**</span></span> |<span data-ttu-id="a1dbc-243">Lay-out van kanaal.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-243">Channel layout.</span></span> |
| <span data-ttu-id="a1dbc-244">**Kanalen**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-244">**Channels**</span></span><br /><br /> <span data-ttu-id="a1dbc-245">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-245">Required</span></span> |<span data-ttu-id="a1dbc-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-246">**xs:int**</span></span> |<span data-ttu-id="a1dbc-247">Aantal (0 of meer) audio kanalen.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="a1dbc-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="a1dbc-249">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-249">Required</span></span> |<span data-ttu-id="a1dbc-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-250">**xs:int**</span></span> |<span data-ttu-id="a1dbc-251">Samplefrequentie van audio in steekproeven per seconde of Hz.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="a1dbc-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-252">**Bitrate**</span></span> |<span data-ttu-id="a1dbc-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-253">**xs:int**</span></span> |<span data-ttu-id="a1dbc-254">Gemiddelde audio bitsnelheid in bits per seconde berekend op basis van Hallo assetbestand.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-254">Average audio bit rate in bits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="a1dbc-255">Alleen Hallo elementaire stroom nettolading wordt beschouwd en Hallo verpakking overhead is niet opgenomen in deze telling.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-255">Only hello elementary stream payload is counted, and hello packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="a1dbc-256">**Het BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-256">**BitsPerSample**</span></span> |<span data-ttu-id="a1dbc-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-257">**xs:int**</span></span> |<span data-ttu-id="a1dbc-258">Bits per fragment voor Hallo wFormatTag indeling typt.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-258">Bits per sample for hello wFormatTag format type.</span></span> |

## <span data-ttu-id="a1dbc-259"><a name="VideoTrackType"></a>VideoTrackType (neemt over van TrackType)</span><span class="sxs-lookup"><span data-stu-id="a1dbc-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="a1dbc-260">**VideoTrackType** is globale complex type die eigenschappen van overneemt [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="a1dbc-261">Hallo type vertegenwoordigt een specifieke video bijhouden in Hallo assetbestand.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-261">hello type represents a specific video track in hello asset file.</span></span>  

<span data-ttu-id="a1dbc-262">Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-262">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a1dbc-263">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="a1dbc-263">Attributes</span></span>
| <span data-ttu-id="a1dbc-264">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-264">Name</span></span> | <span data-ttu-id="a1dbc-265">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-265">Type</span></span> | <span data-ttu-id="a1dbc-266">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-267">**Code**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="a1dbc-268">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-268">Required</span></span> |<span data-ttu-id="a1dbc-269">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-269">**xs:string**</span></span> |<span data-ttu-id="a1dbc-270">Video-codec code code.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="a1dbc-271">**Profiel**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-271">**Profile**</span></span> |<span data-ttu-id="a1dbc-272">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-272">**xs:string**</span></span> |<span data-ttu-id="a1dbc-273">Profiel van de video bijhouden.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-273">Video track's profile.</span></span> |
| <span data-ttu-id="a1dbc-274">**Niveau**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-274">**Level**</span></span> |<span data-ttu-id="a1dbc-275">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-275">**xs:string**</span></span> |<span data-ttu-id="a1dbc-276">Niveau van de video bijhouden.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-276">Video track's level.</span></span> |
| <span data-ttu-id="a1dbc-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-277">**PixelFormat**</span></span> |<span data-ttu-id="a1dbc-278">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-278">**xs:string**</span></span> |<span data-ttu-id="a1dbc-279">Video bijhouden pixelindeling.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="a1dbc-280">**Breedte**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-280">**Width**</span></span><br /><br /> <span data-ttu-id="a1dbc-281">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-281">Required</span></span> |<span data-ttu-id="a1dbc-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-282">**xs:int**</span></span> |<span data-ttu-id="a1dbc-283">Gecodeerde video breedte in pixels.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="a1dbc-284">**Hoogte**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-284">**Height**</span></span><br /><br /> <span data-ttu-id="a1dbc-285">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-285">Required</span></span> |<span data-ttu-id="a1dbc-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-286">**xs:int**</span></span> |<span data-ttu-id="a1dbc-287">Gecodeerde video hoogte in pixels.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="a1dbc-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="a1dbc-289">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-289">Required</span></span> |<span data-ttu-id="a1dbc-290">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-290">**xs:double**</span></span> |<span data-ttu-id="a1dbc-291">Beeldscherm hoogte-breedteverhouding teller.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="a1dbc-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="a1dbc-293">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-293">Required</span></span> |<span data-ttu-id="a1dbc-294">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-294">**xs:double**</span></span> |<span data-ttu-id="a1dbc-295">Noemer voor de hoogte-breedteverhouding beeld weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="a1dbc-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="a1dbc-297">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-297">Required</span></span> |<span data-ttu-id="a1dbc-298">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-298">**xs:double**</span></span> |<span data-ttu-id="a1dbc-299">Video voorbeeld hoogte-breedteverhouding teller.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="a1dbc-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="a1dbc-301">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-301">**xs:double**</span></span> |<span data-ttu-id="a1dbc-302">Video voorbeeld hoogte-breedteverhouding teller.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="a1dbc-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="a1dbc-304">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-304">**xs:double**</span></span> |<span data-ttu-id="a1dbc-305">Noemer voor de hoogte-breedteverhouding video voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="a1dbc-306">**Framesnelheid**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="a1dbc-307">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-307">Required</span></span> |<span data-ttu-id="a1dbc-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-308">**xs:decimal**</span></span> |<span data-ttu-id="a1dbc-309">Framesnelheid van video .3f indeling gemeten.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="a1dbc-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-310">**Bitrate**</span></span> |<span data-ttu-id="a1dbc-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-311">**xs:int**</span></span> |<span data-ttu-id="a1dbc-312">Gemiddelde video bitsnelheid in kilobits per seconde berekend op basis van Hallo assetbestand.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-312">Average video bit rate in kilobits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="a1dbc-313">Alleen Hallo elementaire stroom nettolading wordt beschouwd en Hallo verpakking overhead is niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-313">Only hello elementary stream payload is counted, and hello packaging overhead is not included.</span></span> |
| <span data-ttu-id="a1dbc-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="a1dbc-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-315">**xs:int**</span></span> |<span data-ttu-id="a1dbc-316">Gemiddelde bitrate Max GOP voor deze video spoor in kilobits per seconde.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="a1dbc-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-317">**HasBFrames**</span></span> |<span data-ttu-id="a1dbc-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-318">**xs:int**</span></span> |<span data-ttu-id="a1dbc-319">Video bijhouden aantal B-frames.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="a1dbc-320"><a name="MetadataType"></a>MetadataType</span><span class="sxs-lookup"><span data-stu-id="a1dbc-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="a1dbc-321">**MetadataType** is globale complex type die worden beschreven van metagegevens van een assetbestand als sleutel/waarde-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="a1dbc-322">Bijvoorbeeld, sleutel = 'taal' en waarde = 'eng'.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="a1dbc-323">Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-323">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a1dbc-324">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="a1dbc-324">Attributes</span></span>
| <span data-ttu-id="a1dbc-325">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-325">Name</span></span> | <span data-ttu-id="a1dbc-326">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-326">Type</span></span> | <span data-ttu-id="a1dbc-327">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-328">**sleutel**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-328">**key**</span></span><br /><br /> <span data-ttu-id="a1dbc-329">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-329">Required</span></span> |<span data-ttu-id="a1dbc-330">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-330">**xs:string**</span></span> |<span data-ttu-id="a1dbc-331">Hallo-sleutel in het sleutel-waardepaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-331">hello key in hello key/value pair.</span></span> |
| <span data-ttu-id="a1dbc-332">**waarde**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-332">**value**</span></span><br /><br /> <span data-ttu-id="a1dbc-333">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-333">Required</span></span> |<span data-ttu-id="a1dbc-334">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-334">**xs:string**</span></span> |<span data-ttu-id="a1dbc-335">Hallo-waarde in het sleutel-waardepaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-335">hello value in hello key/value pair.</span></span> |

## <span data-ttu-id="a1dbc-336"><a name="ProgramType"></a>ProgramType</span><span class="sxs-lookup"><span data-stu-id="a1dbc-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="a1dbc-337">**ProgramType** is globale complex type die worden beschreven van een programma.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="a1dbc-338">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="a1dbc-338">Attributes</span></span>
| <span data-ttu-id="a1dbc-339">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-339">Name</span></span> | <span data-ttu-id="a1dbc-340">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-340">Type</span></span> | <span data-ttu-id="a1dbc-341">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="a1dbc-343">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-343">Required</span></span> |<span data-ttu-id="a1dbc-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-344">**xs:int**</span></span> |<span data-ttu-id="a1dbc-345">Programma-Id</span><span class="sxs-lookup"><span data-stu-id="a1dbc-345">Program Id</span></span> |
| <span data-ttu-id="a1dbc-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="a1dbc-347">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-347">Required</span></span> |<span data-ttu-id="a1dbc-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-348">**xs:int**</span></span> |<span data-ttu-id="a1dbc-349">Het aantal programma's.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-349">Number of programs.</span></span> |
| <span data-ttu-id="a1dbc-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="a1dbc-351">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-351">Required</span></span> |<span data-ttu-id="a1dbc-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-352">**xs:int**</span></span> |<span data-ttu-id="a1dbc-353">Programma kaart tabellen (PMTs) bevatten informatie over programma's.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="a1dbc-354">Zie voor meer informatie [BET](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="a1dbc-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="a1dbc-356">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-356">Required</span></span> |<span data-ttu-id="a1dbc-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-357">**xs:int**</span></span> |<span data-ttu-id="a1dbc-358">Door de decoder gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-358">Used by decoder.</span></span> <span data-ttu-id="a1dbc-359">Zie voor meer informatie [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span><span class="sxs-lookup"><span data-stu-id="a1dbc-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="a1dbc-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-360">**StartPTS**</span></span> |<span data-ttu-id="a1dbc-361">**xs: lang**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-361">**xs: long**</span></span> |<span data-ttu-id="a1dbc-362">Presentatie tijdstempel wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="a1dbc-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-363">**EndPTS**</span></span> |<span data-ttu-id="a1dbc-364">**xs: lang**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-364">**xs: long**</span></span> |<span data-ttu-id="a1dbc-365">Beëindigen presentatie tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="a1dbc-366"><a name="StreamDispositionType"></a>StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="a1dbc-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="a1dbc-367">**StreamDispositionType** is globale complex type die Hallo-stroom beschrijft.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-367">**StreamDispositionType** is a global complex type that describes hello stream.</span></span>  

<span data-ttu-id="a1dbc-368">Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-368">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a1dbc-369">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="a1dbc-369">Attributes</span></span>
| <span data-ttu-id="a1dbc-370">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-370">Name</span></span> | <span data-ttu-id="a1dbc-371">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-371">Type</span></span> | <span data-ttu-id="a1dbc-372">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-373">**Standaard**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-373">**Default**</span></span><br /><br /> <span data-ttu-id="a1dbc-374">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-374">Required</span></span> |<span data-ttu-id="a1dbc-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-375">**xs:int**</span></span> |<span data-ttu-id="a1dbc-376">Dit kenmerk too1 tooindicate die dit is de standaardpresentatie Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-376">Set this attribute too1 tooindicate this is hello default presentation.</span></span> |
| <span data-ttu-id="a1dbc-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-377">**Dub**</span></span><br /><br /> <span data-ttu-id="a1dbc-378">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-378">Required</span></span> |<span data-ttu-id="a1dbc-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-379">**xs:int**</span></span> |<span data-ttu-id="a1dbc-380">Stel dit kenmerk too1 tooindicate deze optie is Hallo nagesynchroniseerd presentatie.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-380">Set this attribute too1 tooindicate this is hello dubbed presentation.</span></span> |
| <span data-ttu-id="a1dbc-381">**Origineel**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-381">**Original**</span></span><br /><br /> <span data-ttu-id="a1dbc-382">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-382">Required</span></span> |<span data-ttu-id="a1dbc-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-383">**xs:int**</span></span> |<span data-ttu-id="a1dbc-384">Dit kenmerk too1 tooindicate die dit is de oorspronkelijke presentatie Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-384">Set this attribute too1 tooindicate this is hello original presentation.</span></span> |
| <span data-ttu-id="a1dbc-385">**Opmerking**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-385">**Comment**</span></span><br /><br /> <span data-ttu-id="a1dbc-386">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-386">Required</span></span> |<span data-ttu-id="a1dbc-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-387">**xs:int**</span></span> |<span data-ttu-id="a1dbc-388">Stel dit kenmerk too1 tooindicate deze bijhouden commentaar bevat.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-388">Set this attribute too1 tooindicate this track contains commentary.</span></span> |
| <span data-ttu-id="a1dbc-389">**Tekst**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="a1dbc-390">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-390">Required</span></span> |<span data-ttu-id="a1dbc-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-391">**xs:int**</span></span> |<span data-ttu-id="a1dbc-392">Stel dit kenmerk too1 tooindicate deze bijhouden tekst bevat.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-392">Set this attribute too1 tooindicate this track contains lyrics.</span></span> |
| <span data-ttu-id="a1dbc-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="a1dbc-394">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-394">Required</span></span> |<span data-ttu-id="a1dbc-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-395">**xs:int**</span></span> |<span data-ttu-id="a1dbc-396">Stel dit kenmerk too1 tooindicate dit vertegenwoordigt Hallo karaoke bijhouden (achtergrondmuziek, geen zang).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-396">Set this attribute too1 tooindicate this represents hello karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="a1dbc-397">**Gedwongen**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-397">**Forced**</span></span><br /><br /> <span data-ttu-id="a1dbc-398">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-398">Required</span></span> |<span data-ttu-id="a1dbc-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-399">**xs:int**</span></span> |<span data-ttu-id="a1dbc-400">Hallo gedwongen presentatie voor dit kenmerk too1 tooindicate die dit is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-400">Set this attribute too1 tooindicate this is hello forced presentation.</span></span> |
| <span data-ttu-id="a1dbc-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="a1dbc-402">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-402">Required</span></span> |<span data-ttu-id="a1dbc-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-403">**xs:int**</span></span> |<span data-ttu-id="a1dbc-404">Dit kenmerk too1 tooindicate die dit nummer voor Hallo slechthorenden is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-404">Set this attribute too1 tooindicate this track is for hello hearing impaired.</span></span> |
| <span data-ttu-id="a1dbc-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="a1dbc-406">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-406">Required</span></span> |<span data-ttu-id="a1dbc-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-407">**xs:int**</span></span> |<span data-ttu-id="a1dbc-408">Dit kenmerk too1 tooindicate die dit nummer voor Hallo visueel functioneel is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-408">Set this attribute too1 tooindicate this track is for hello visually impaired.</span></span> |
| <span data-ttu-id="a1dbc-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="a1dbc-410">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-410">Required</span></span> |<span data-ttu-id="a1dbc-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-411">**xs:int**</span></span> |<span data-ttu-id="a1dbc-412">Schone gevolgen voor dit kenmerk too1 tooindicate die dit nummer is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-412">Set this attribute too1 tooindicate this track has clean effects.</span></span> |
| <span data-ttu-id="a1dbc-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="a1dbc-414">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1dbc-414">Required</span></span> |<span data-ttu-id="a1dbc-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-415">**xs:int**</span></span> |<span data-ttu-id="a1dbc-416">Afbeeldingen voor dit kenmerk too1 tooindicate die dit nummer is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-416">Set this attribute too1 tooindicate this track has pictures.</span></span> |

## <span data-ttu-id="a1dbc-417"><a name="Programs"></a>Programma's-element</span><span class="sxs-lookup"><span data-stu-id="a1dbc-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="a1dbc-418">Wrapper-element dat bevat meerdere **programma** elementen.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="a1dbc-419">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="a1dbc-419">Child elements</span></span>
| <span data-ttu-id="a1dbc-420">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-420">Name</span></span> | <span data-ttu-id="a1dbc-421">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-421">Type</span></span> | <span data-ttu-id="a1dbc-422">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-423">**Programma**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-423">**Program**</span></span><br /><br /> <span data-ttu-id="a1dbc-424">minOccurs = "0" maxOccurs = 'unbounded'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="a1dbc-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="a1dbc-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="a1dbc-426">Bevat informatie over software in het assetbestand Hallo voor assetbestanden MPEG-TS-indeling.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-426">For asset files that are in MPEG-TS format, contains information about programs in hello asset file.</span></span> |

## <span data-ttu-id="a1dbc-427"><a name="VideoTracks"></a>VideoTracks element</span><span class="sxs-lookup"><span data-stu-id="a1dbc-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="a1dbc-428">Wrapper-element dat bevat meerdere **VideoTrack** elementen.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="a1dbc-429">Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-429">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="a1dbc-430">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="a1dbc-430">Child elements</span></span>
| <span data-ttu-id="a1dbc-431">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-431">Name</span></span> | <span data-ttu-id="a1dbc-432">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-432">Type</span></span> | <span data-ttu-id="a1dbc-433">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="a1dbc-435">minOccurs = "0" maxOccurs = 'unbounded'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="a1dbc-436">VideoTrackType (neemt over van TrackType)</span><span class="sxs-lookup"><span data-stu-id="a1dbc-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="a1dbc-437">Bevat informatie over video houdt in Hallo assetbestand.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-437">Contains information about video tracks in hello asset file.</span></span> |

## <span data-ttu-id="a1dbc-438"><a name="AudioTracks"></a>AudioTracks element</span><span class="sxs-lookup"><span data-stu-id="a1dbc-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="a1dbc-439">Wrapper-element dat bevat meerdere **AudioTrack** elementen.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="a1dbc-440">Een XML-voorbeeld aan Hallo einde van dit onderwerp: [XML-voorbeeld](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a1dbc-440">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="a1dbc-441">Elementen</span><span class="sxs-lookup"><span data-stu-id="a1dbc-441">elements</span></span>
| <span data-ttu-id="a1dbc-442">Naam</span><span class="sxs-lookup"><span data-stu-id="a1dbc-442">Name</span></span> | <span data-ttu-id="a1dbc-443">Type</span><span class="sxs-lookup"><span data-stu-id="a1dbc-443">Type</span></span> | <span data-ttu-id="a1dbc-444">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1dbc-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1dbc-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="a1dbc-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="a1dbc-446">minOccurs = "0" maxOccurs = 'unbounded'</span><span class="sxs-lookup"><span data-stu-id="a1dbc-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="a1dbc-447">AudioTrackType (neemt over van TrackType)</span><span class="sxs-lookup"><span data-stu-id="a1dbc-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="a1dbc-448">Bevat informatie over audio houdt in Hallo assetbestand.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-448">Contains information about audio tracks in hello asset file.</span></span> |

## <span data-ttu-id="a1dbc-449"><a name="code"></a>Schema-Code</span><span class="sxs-lookup"><span data-stu-id="a1dbc-449"><a name="code"></a> Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <span data-ttu-id="a1dbc-450"><a name="xml"></a>XML-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="a1dbc-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="a1dbc-451">Hallo Hier volgt een voorbeeld van een metagegevensbestand Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="a1dbc-451">hello following is an example of hello Input metadata file.</span></span>  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="a1dbc-452">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a1dbc-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a1dbc-453">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="a1dbc-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

