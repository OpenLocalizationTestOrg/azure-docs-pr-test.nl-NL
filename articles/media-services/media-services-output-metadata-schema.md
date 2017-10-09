---
title: aaaAzure Media Services-uitvoerschema metagegevens | Microsoft Docs
description: Hallo onderwerp overzicht een van Azure Media Services-uitvoerschema metagegevens.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 7f07d6accbe0b171d0408b15d5e1e6b5afd6c367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="output-metadata"></a><span data-ttu-id="7f357-103">Metagegevens</span><span class="sxs-lookup"><span data-stu-id="7f357-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="7f357-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7f357-104">Overview</span></span>
<span data-ttu-id="7f357-105">Een codeertaak is gekoppeld aan een invoer asset (of activa) waarop tooperform sommige taken codering.</span><span class="sxs-lookup"><span data-stu-id="7f357-105">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span> <span data-ttu-id="7f357-106">Bijvoorbeeld coderen een MP4-bestand tooH.264 MP4 adaptive bitrate ingesteld; Maak een miniatuur; overlays maken.</span><span class="sxs-lookup"><span data-stu-id="7f357-106">For example, encode an MP4 file tooH.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="7f357-107">Na voltooiing van een taak wordt een uitvoerasset geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="7f357-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="7f357-108">Hallo uitvoerasset bevat video, audio, miniaturen, enz. Hallo uitvoerasset bevat ook een bestand met metagegevens over Hallo uitvoerasset.</span><span class="sxs-lookup"><span data-stu-id="7f357-108">hello output asset contains video, audio, thumbnails, etc. hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="7f357-109">Hallo naam van XML-bestand met metagegevens Hallo heeft Hallo volgende indeling: &lt;source_file_name&gt;_manifest.xml (bijvoorbeeld BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="7f357-109">hello name of hello metadata XML file has hello following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="7f357-110">Als u tooexamine Hallo metagegevensbestand wilt, kunt u een **SAS** locator en downloaden Hallo bestand tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="7f357-110">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span>  

<span data-ttu-id="7f357-111">Dit onderwerp wordt besproken Hallo-elementen en typen van Hallo XML-schema op welke Hallo uitvoer metada (&lt;source_file_name&gt;_manifest.xml) is gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="7f357-111">This topic discusses hello elements and types of hello XML schema on which hello output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="7f357-112">Zie voor meer informatie over het Hallo-bestand met metagegevens over Hallo invoer asset [invoer metagegevens](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7f357-112">For information about hello file that contains metadata about hello input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="7f357-113">U vindt Hallo volledig schema code en XML-voorbeeld aan Hallo einde van dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7f357-113">You can find hello complete schema code and XML example at hello end of this topic.</span></span>  
>
>

## <span data-ttu-id="7f357-114"><a name="AssetFiles "></a>Het hoofdelement AssetFiles</span><span class="sxs-lookup"><span data-stu-id="7f357-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="7f357-115">Verzameling AssetFile vermeldingen voor Hallo coderingstaak.</span><span class="sxs-lookup"><span data-stu-id="7f357-115">Collection of AssetFile entries for hello encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="7f357-116">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="7f357-116">Child elements</span></span>
| <span data-ttu-id="7f357-117">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-117">Name</span></span> | <span data-ttu-id="7f357-118">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f357-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="7f357-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="7f357-120">minOccurs = "0" maxOccurs = '1'</span><span class="sxs-lookup"><span data-stu-id="7f357-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="7f357-121">Een [AssetFile element](media-services-output-metadata-schema.md) dat onderdeel is van Hallo AssetFiles verzameling.</span><span class="sxs-lookup"><span data-stu-id="7f357-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of hello AssetFiles collection.</span></span> |

## <span data-ttu-id="7f357-122"><a name="AssetFile "></a>AssetFile element</span><span class="sxs-lookup"><span data-stu-id="7f357-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="7f357-123">U vindt een XML-voorbeeld [XML-voorbeeld](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="7f357-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="7f357-124">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="7f357-124">Attributes</span></span>
| <span data-ttu-id="7f357-125">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-125">Name</span></span> | <span data-ttu-id="7f357-126">Type</span><span class="sxs-lookup"><span data-stu-id="7f357-126">Type</span></span> | <span data-ttu-id="7f357-127">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f357-128">**Naam**</span><span class="sxs-lookup"><span data-stu-id="7f357-128">**Name**</span></span><br/><br/> <span data-ttu-id="7f357-129">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-129">Required</span></span> |<span data-ttu-id="7f357-130">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="7f357-130">**xs:string**</span></span> |<span data-ttu-id="7f357-131">Hallo media asset-bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="7f357-131">hello media asset file name.</span></span> |
| <span data-ttu-id="7f357-132">**Grootte**</span><span class="sxs-lookup"><span data-stu-id="7f357-132">**Size**</span></span><br/><br/> <span data-ttu-id="7f357-133">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-134">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-134">Required</span></span> |<span data-ttu-id="7f357-135">**xs:Long**</span><span class="sxs-lookup"><span data-stu-id="7f357-135">**xs:long**</span></span> |<span data-ttu-id="7f357-136">Grootte van Hallo asset bestandsgrootte in bytes.</span><span class="sxs-lookup"><span data-stu-id="7f357-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="7f357-137">**Duur**</span><span class="sxs-lookup"><span data-stu-id="7f357-137">**Duration**</span></span><br/><br/> <span data-ttu-id="7f357-138">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-138">Required</span></span> |<span data-ttu-id="7f357-139">**xs: duration**</span><span class="sxs-lookup"><span data-stu-id="7f357-139">**xs:duration**</span></span> |<span data-ttu-id="7f357-140">Inhoud afspelen back duur.</span><span class="sxs-lookup"><span data-stu-id="7f357-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="7f357-141">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="7f357-141">Child elements</span></span>
| <span data-ttu-id="7f357-142">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-142">Name</span></span> | <span data-ttu-id="7f357-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f357-144">**Bronnen**</span><span class="sxs-lookup"><span data-stu-id="7f357-144">**Sources**</span></span> |<span data-ttu-id="7f357-145">Verzameling van de invoerbron/mediabestanden, die is verwerkt in volgorde tooproduce deze AssetFile.</span><span class="sxs-lookup"><span data-stu-id="7f357-145">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span> <span data-ttu-id="7f357-146">Zie voor meer informatie [bronelement](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7f357-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="7f357-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="7f357-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="7f357-148">minOccurs = "0" maxOccurs = '1'</span><span class="sxs-lookup"><span data-stu-id="7f357-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="7f357-149">Elke fysieke AssetFile kan nul of meer video houdt interleaved naar een indeling voor de juiste container in het bevatten.</span><span class="sxs-lookup"><span data-stu-id="7f357-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="7f357-150">Dit is de verzameling Hallo van deze video houdt.</span><span class="sxs-lookup"><span data-stu-id="7f357-150">This is hello collection of all those video tracks.</span></span> <span data-ttu-id="7f357-151">Zie voor meer informatie [VideoTracks element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7f357-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="7f357-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="7f357-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="7f357-153">minOccurs = "0" maxOccurs = '1'</span><span class="sxs-lookup"><span data-stu-id="7f357-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="7f357-154">Elke fysieke AssetFile kan nul of meer audio houdt interleaved naar een indeling voor de juiste container in het bevatten.</span><span class="sxs-lookup"><span data-stu-id="7f357-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="7f357-155">Dit is de audio houdt Hallo verzameling.</span><span class="sxs-lookup"><span data-stu-id="7f357-155">This is hello collection of all those audio tracks.</span></span> <span data-ttu-id="7f357-156">Zie voor meer informatie [AudioTracks element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7f357-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="7f357-157"><a name="Sources "></a>Bronnen-element</span><span class="sxs-lookup"><span data-stu-id="7f357-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="7f357-158">Verzameling van de invoerbron/mediabestanden, die is verwerkt in volgorde tooproduce deze AssetFile.</span><span class="sxs-lookup"><span data-stu-id="7f357-158">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span>  

<span data-ttu-id="7f357-159">U vindt een XML-voorbeeld [XML-voorbeeld](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="7f357-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="7f357-160">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="7f357-160">Child elements</span></span>
| <span data-ttu-id="7f357-161">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-161">Name</span></span> | <span data-ttu-id="7f357-162">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f357-163">**Bron**</span><span class="sxs-lookup"><span data-stu-id="7f357-163">**Source**</span></span><br/><br/> <span data-ttu-id="7f357-164">minOccurs = "1" maxOccurs = 'unbounded'</span><span class="sxs-lookup"><span data-stu-id="7f357-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="7f357-165">Een invoer/bronbestand dat wordt gebruikt bij het genereren van deze activa.</span><span class="sxs-lookup"><span data-stu-id="7f357-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="7f357-166">Zie voor meer informatie [bronelement](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7f357-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="7f357-167"><a name="Source "></a>Bronelement</span><span class="sxs-lookup"><span data-stu-id="7f357-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="7f357-168">Een invoer/bronbestand dat wordt gebruikt bij het genereren van deze activa.</span><span class="sxs-lookup"><span data-stu-id="7f357-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="7f357-169">U vindt een XML-voorbeeld [XML-voorbeeld](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="7f357-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="7f357-170">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="7f357-170">Attributes</span></span>
| <span data-ttu-id="7f357-171">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-171">Name</span></span> | <span data-ttu-id="7f357-172">Type</span><span class="sxs-lookup"><span data-stu-id="7f357-172">Type</span></span> | <span data-ttu-id="7f357-173">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f357-174">**Naam**</span><span class="sxs-lookup"><span data-stu-id="7f357-174">**Name**</span></span><br/><br/> <span data-ttu-id="7f357-175">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-175">Required</span></span> |<span data-ttu-id="7f357-176">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="7f357-176">**xs:string**</span></span> |<span data-ttu-id="7f357-177">Bestandsnaam van de invoerbron.</span><span class="sxs-lookup"><span data-stu-id="7f357-177">Input source file name.</span></span> |

## <span data-ttu-id="7f357-178"><a name="VideoTracks "></a>VideoTracks element</span><span class="sxs-lookup"><span data-stu-id="7f357-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="7f357-179">Elke fysieke AssetFile kan nul of meer video houdt interleaved naar een indeling voor de juiste container in het bevatten.</span><span class="sxs-lookup"><span data-stu-id="7f357-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="7f357-180">Dit is de verzameling Hallo van deze video houdt.</span><span class="sxs-lookup"><span data-stu-id="7f357-180">This is hello collection of all those video tracks.</span></span>  

<span data-ttu-id="7f357-181">U vindt een XML-voorbeeld [XML-voorbeeld](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="7f357-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="7f357-182">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="7f357-182">Child elements</span></span>
| <span data-ttu-id="7f357-183">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-183">Name</span></span> | <span data-ttu-id="7f357-184">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f357-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="7f357-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="7f357-186">minOccurs = "1" maxOccurs = 'unbounded'</span><span class="sxs-lookup"><span data-stu-id="7f357-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="7f357-187">Een specifieke video in Hallo bovenliggende AssetFile bijhouden.</span><span class="sxs-lookup"><span data-stu-id="7f357-187">A specific video track in hello parent AssetFile.</span></span> <span data-ttu-id="7f357-188">Zie voor meer informatie [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="7f357-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="7f357-189"><a name="VideoTrack"></a>VideoTrack element</span><span class="sxs-lookup"><span data-stu-id="7f357-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="7f357-190">Een specifieke video in Hallo bovenliggende AssetFile bijhouden.</span><span class="sxs-lookup"><span data-stu-id="7f357-190">A specific video track in hello parent AssetFile.</span></span>  

<span data-ttu-id="7f357-191">U vindt een XML-voorbeeld [XML-voorbeeld](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="7f357-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="7f357-192">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="7f357-192">Attributes</span></span>
| <span data-ttu-id="7f357-193">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-193">Name</span></span> | <span data-ttu-id="7f357-194">Type</span><span class="sxs-lookup"><span data-stu-id="7f357-194">Type</span></span> | <span data-ttu-id="7f357-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f357-196">**ID**</span><span class="sxs-lookup"><span data-stu-id="7f357-196">**Id**</span></span><br/><br/> <span data-ttu-id="7f357-197">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-198">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-198">Required</span></span> |<span data-ttu-id="7f357-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-199">**xs:int**</span></span> |<span data-ttu-id="7f357-200">Op nul gebaseerde index van deze video bijhouden. **Opmerking:** dit is niet noodzakelijkerwijs Hallo TrackID zoals gebruikt in een MP4-bestand.</span><span class="sxs-lookup"><span data-stu-id="7f357-200">Zero-based index of this video track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="7f357-201">**Code**</span><span class="sxs-lookup"><span data-stu-id="7f357-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="7f357-202">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-202">Required</span></span> |<span data-ttu-id="7f357-203">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="7f357-203">**xs:string**</span></span> |<span data-ttu-id="7f357-204">Video-codec code code.</span><span class="sxs-lookup"><span data-stu-id="7f357-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="7f357-205">**Profiel**</span><span class="sxs-lookup"><span data-stu-id="7f357-205">**Profile**</span></span> |<span data-ttu-id="7f357-206">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="7f357-206">**xs:string**</span></span> |<span data-ttu-id="7f357-207">Profiel van de geselecteerde instelling H264 (alleen van toepassing tooH264 codec).</span><span class="sxs-lookup"><span data-stu-id="7f357-207">H264 profile (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="7f357-208">**Niveau**</span><span class="sxs-lookup"><span data-stu-id="7f357-208">**Level**</span></span> |<span data-ttu-id="7f357-209">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="7f357-209">**xs:string**</span></span> |<span data-ttu-id="7f357-210">Geselecteerde instelling H264 niveau (alleen van toepassing tooH264 codec).</span><span class="sxs-lookup"><span data-stu-id="7f357-210">H264 level (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="7f357-211">**Breedte**</span><span class="sxs-lookup"><span data-stu-id="7f357-211">**Width**</span></span><br/><br/> <span data-ttu-id="7f357-212">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-213">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-213">Required</span></span> |<span data-ttu-id="7f357-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-214">**xs:int**</span></span> |<span data-ttu-id="7f357-215">Gecodeerde video breedte in pixels.</span><span class="sxs-lookup"><span data-stu-id="7f357-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="7f357-216">**Hoogte**</span><span class="sxs-lookup"><span data-stu-id="7f357-216">**Height**</span></span><br/><br/> <span data-ttu-id="7f357-217">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-218">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-218">Required</span></span> |<span data-ttu-id="7f357-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-219">**xs:int**</span></span> |<span data-ttu-id="7f357-220">Gecodeerde video hoogte in pixels.</span><span class="sxs-lookup"><span data-stu-id="7f357-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="7f357-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="7f357-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="7f357-222">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-223">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-223">Required</span></span> |<span data-ttu-id="7f357-224">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="7f357-224">**xs:double**</span></span> |<span data-ttu-id="7f357-225">Beeldscherm hoogte-breedteverhouding teller.</span><span class="sxs-lookup"><span data-stu-id="7f357-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="7f357-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="7f357-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="7f357-227">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-228">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-228">Required</span></span> |<span data-ttu-id="7f357-229">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="7f357-229">**xs:double**</span></span> |<span data-ttu-id="7f357-230">Noemer voor de hoogte-breedteverhouding beeld weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f357-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="7f357-231">**Framesnelheid**</span><span class="sxs-lookup"><span data-stu-id="7f357-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="7f357-232">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-233">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-233">Required</span></span> |<span data-ttu-id="7f357-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="7f357-234">**xs:decimal**</span></span> |<span data-ttu-id="7f357-235">Framesnelheid van video .3f indeling gemeten.</span><span class="sxs-lookup"><span data-stu-id="7f357-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="7f357-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="7f357-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="7f357-237">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-238">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-238">Required</span></span> |<span data-ttu-id="7f357-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="7f357-239">**xs:decimal**</span></span> |<span data-ttu-id="7f357-240">Vooraf ingestelde doel framesnelheid van video .3f-indeling.</span><span class="sxs-lookup"><span data-stu-id="7f357-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="7f357-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="7f357-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="7f357-242">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-243">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-243">Required</span></span> |<span data-ttu-id="7f357-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-244">**xs:int**</span></span> |<span data-ttu-id="7f357-245">Gemiddelde video bitsnelheid in kilobits per seconde berekend op basis van Hallo AssetFile.</span><span class="sxs-lookup"><span data-stu-id="7f357-245">Average video bit rate in kilobits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="7f357-246">Alleen Hallo elementaire stroom nettolading telt en bevat geen Hallo verpakking overhead.</span><span class="sxs-lookup"><span data-stu-id="7f357-246">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="7f357-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="7f357-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="7f357-248">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-249">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-249">Required</span></span> |<span data-ttu-id="7f357-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-250">**xs:int**</span></span> |<span data-ttu-id="7f357-251">Doel gemiddelde bitrate voor deze video bijhouden, zoals aangevraagd via de codering voorinstelling Hallo in kilobits per seconde.</span><span class="sxs-lookup"><span data-stu-id="7f357-251">Target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="7f357-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="7f357-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="7f357-253">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-253">minInclusive ="0"</span></span> |<span data-ttu-id="7f357-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-254">**xs:int**</span></span> |<span data-ttu-id="7f357-255">Gemiddelde bitrate Max GOP voor deze video spoor in kilobits per seconde.</span><span class="sxs-lookup"><span data-stu-id="7f357-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="7f357-256"><a name="AudioTracks "></a>AudioTracks element</span><span class="sxs-lookup"><span data-stu-id="7f357-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="7f357-257">Elke fysieke AssetFile kan nul of meer audio houdt interleaved naar een indeling voor de juiste container in het bevatten.</span><span class="sxs-lookup"><span data-stu-id="7f357-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="7f357-258">Dit is de audio houdt Hallo verzameling.</span><span class="sxs-lookup"><span data-stu-id="7f357-258">This is hello collection of all those audio tracks.</span></span>  

<span data-ttu-id="7f357-259">U vindt een XML-voorbeeld [XML-voorbeeld](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="7f357-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="7f357-260">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="7f357-260">Child elements</span></span>
| <span data-ttu-id="7f357-261">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-261">Name</span></span> | <span data-ttu-id="7f357-262">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f357-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="7f357-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="7f357-264">minOccurs = "1" maxOccurs = 'unbounded'</span><span class="sxs-lookup"><span data-stu-id="7f357-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="7f357-265">Een specifieke audio in Hallo bovenliggende AssetFile bijhouden.</span><span class="sxs-lookup"><span data-stu-id="7f357-265">A specific audio track in hello parent AssetFile.</span></span> <span data-ttu-id="7f357-266">Zie voor meer informatie [AudioTrack element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7f357-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="7f357-267"><a name="AudioTrack "></a>AudioTrack element</span><span class="sxs-lookup"><span data-stu-id="7f357-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="7f357-268">Een specifieke audio in Hallo bovenliggende AssetFile bijhouden.</span><span class="sxs-lookup"><span data-stu-id="7f357-268">A specific audio track in hello parent AssetFile.</span></span>  

<span data-ttu-id="7f357-269">U vindt een XML-voorbeeld [XML-voorbeeld](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="7f357-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="7f357-270">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="7f357-270">Attributes</span></span>
| <span data-ttu-id="7f357-271">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-271">Name</span></span> | <span data-ttu-id="7f357-272">Type</span><span class="sxs-lookup"><span data-stu-id="7f357-272">Type</span></span> | <span data-ttu-id="7f357-273">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f357-274">**ID**</span><span class="sxs-lookup"><span data-stu-id="7f357-274">**Id**</span></span><br/><br/> <span data-ttu-id="7f357-275">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-276">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-276">Required</span></span> |<span data-ttu-id="7f357-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-277">**xs:int**</span></span> |<span data-ttu-id="7f357-278">Op nul gebaseerde index van deze-nummer. **Opmerking:** dit is niet noodzakelijkerwijs Hallo TrackID zoals gebruikt in een MP4-bestand.</span><span class="sxs-lookup"><span data-stu-id="7f357-278">Zero-based index of this audio track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="7f357-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="7f357-279">**Codec**</span></span> |<span data-ttu-id="7f357-280">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="7f357-280">**xs:string**</span></span> |<span data-ttu-id="7f357-281">-Nummer codec tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="7f357-281">Audio track codec string.</span></span> |
| <span data-ttu-id="7f357-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="7f357-282">**EncoderVersion**</span></span> |<span data-ttu-id="7f357-283">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="7f357-283">**xs:string**</span></span> |<span data-ttu-id="7f357-284">Versietekenreeks van optionele codering vereist is voor EAC3.</span><span class="sxs-lookup"><span data-stu-id="7f357-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="7f357-285">**Kanalen**</span><span class="sxs-lookup"><span data-stu-id="7f357-285">**Channels**</span></span><br/><br/> <span data-ttu-id="7f357-286">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-287">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-287">Required</span></span> |<span data-ttu-id="7f357-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-288">**xs:int**</span></span> |<span data-ttu-id="7f357-289">Aantal audio kanalen.</span><span class="sxs-lookup"><span data-stu-id="7f357-289">Number of audio channels.</span></span> |
| <span data-ttu-id="7f357-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="7f357-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="7f357-291">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-292">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-292">Required</span></span> |<span data-ttu-id="7f357-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-293">**xs:int**</span></span> |<span data-ttu-id="7f357-294">Samplefrequentie van audio in steekproeven per seconde of Hz.</span><span class="sxs-lookup"><span data-stu-id="7f357-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="7f357-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="7f357-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="7f357-296">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-297">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-297">Required</span></span> |<span data-ttu-id="7f357-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-298">**xs:int**</span></span> |<span data-ttu-id="7f357-299">Gemiddelde audio bitsnelheid in bits per seconde berekend op basis van Hallo AssetFile.</span><span class="sxs-lookup"><span data-stu-id="7f357-299">Average audio bit rate in bits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="7f357-300">Alleen Hallo elementaire stroom nettolading telt en bevat geen Hallo verpakking overhead.</span><span class="sxs-lookup"><span data-stu-id="7f357-300">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="7f357-301">**Het BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="7f357-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="7f357-302">minInclusive = '0'</span><span class="sxs-lookup"><span data-stu-id="7f357-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="7f357-303">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-303">Required</span></span> |<span data-ttu-id="7f357-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-304">**xs:int**</span></span> |<span data-ttu-id="7f357-305">Bits per fragment voor Hallo wFormatTag indeling typt.</span><span class="sxs-lookup"><span data-stu-id="7f357-305">Bits per sample for hello wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="7f357-306">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="7f357-306">Child elements</span></span>
| <span data-ttu-id="7f357-307">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-307">Name</span></span> | <span data-ttu-id="7f357-308">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f357-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="7f357-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="7f357-310">minOccurs = "0" maxOccurs = '1'</span><span class="sxs-lookup"><span data-stu-id="7f357-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="7f357-311">Volume softwarelicentiecontrole resultaat parameters.</span><span class="sxs-lookup"><span data-stu-id="7f357-311">Loudness metering result parameters.</span></span> <span data-ttu-id="7f357-312">Zie voor meer informatie [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7f357-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="7f357-313"><a name="LoudnessMeteringResultParameters "></a>LoudnessMeteringResultParameters element</span><span class="sxs-lookup"><span data-stu-id="7f357-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="7f357-314">Volume softwarelicentiecontrole resultaat parameters.</span><span class="sxs-lookup"><span data-stu-id="7f357-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="7f357-315">U vindt een XML-voorbeeld [XML-voorbeeld](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="7f357-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="7f357-316">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="7f357-316">Attributes</span></span>
| <span data-ttu-id="7f357-317">Naam</span><span class="sxs-lookup"><span data-stu-id="7f357-317">Name</span></span> | <span data-ttu-id="7f357-318">Type</span><span class="sxs-lookup"><span data-stu-id="7f357-318">Type</span></span> | <span data-ttu-id="7f357-319">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f357-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f357-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="7f357-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="7f357-321">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="7f357-321">**xs:string**</span></span> |<span data-ttu-id="7f357-322">**Dolby** professional volume softwarelicentiecontrole development kitversie.</span><span class="sxs-lookup"><span data-stu-id="7f357-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="7f357-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="7f357-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="7f357-324">minInclusive = '-31' maxInclusive = '-' 1</span><span class="sxs-lookup"><span data-stu-id="7f357-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="7f357-325">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-325">Required</span></span> |<span data-ttu-id="7f357-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="7f357-326">**xs:int**</span></span> |<span data-ttu-id="7f357-327">DialogNormalization gegenereerd via DPLM, vereist wanneer LoudnessMetering is ingesteld</span><span class="sxs-lookup"><span data-stu-id="7f357-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="7f357-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="7f357-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="7f357-329">minInclusive = '-70' maxInclusive = "10"</span><span class="sxs-lookup"><span data-stu-id="7f357-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="7f357-330">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-330">Required</span></span> |<span data-ttu-id="7f357-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="7f357-331">**xs:float**</span></span> |<span data-ttu-id="7f357-332">Geïntegreerde volume</span><span class="sxs-lookup"><span data-stu-id="7f357-332">Integrated loudness</span></span> |
| <span data-ttu-id="7f357-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="7f357-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="7f357-334">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-334">Required</span></span> |<span data-ttu-id="7f357-335">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="7f357-335">**xs:string**</span></span> |<span data-ttu-id="7f357-336">Geïntegreerde volume eenheid.</span><span class="sxs-lookup"><span data-stu-id="7f357-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="7f357-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="7f357-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="7f357-338">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-338">Required</span></span> |<span data-ttu-id="7f357-339">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="7f357-339">**xs:string**</span></span> |<span data-ttu-id="7f357-340">Beperken van id</span><span class="sxs-lookup"><span data-stu-id="7f357-340">Gating identifier</span></span> |
| <span data-ttu-id="7f357-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="7f357-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="7f357-342">minInclusive = "0" maxInclusive = "100"</span><span class="sxs-lookup"><span data-stu-id="7f357-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="7f357-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="7f357-343">**xs:float**</span></span> |<span data-ttu-id="7f357-344">Spraak inhoud via Hallo programma, als een percentage.</span><span class="sxs-lookup"><span data-stu-id="7f357-344">Speech content over hello program, as a percentage.</span></span> |
| <span data-ttu-id="7f357-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="7f357-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="7f357-346">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-346">Required</span></span> |<span data-ttu-id="7f357-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="7f357-347">**xs:float**</span></span> |<span data-ttu-id="7f357-348">Piekwaarde absolute voorbeeld, sinds opnieuw instellen of nadat deze is uitgeschakeld, per kanaal.</span><span class="sxs-lookup"><span data-stu-id="7f357-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="7f357-349">Eenheden zijn dBFS.</span><span class="sxs-lookup"><span data-stu-id="7f357-349">Units are dBFS.</span></span> |
| <span data-ttu-id="7f357-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="7f357-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="7f357-351">vaste = "dBFS"</span><span class="sxs-lookup"><span data-stu-id="7f357-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="7f357-352">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-352">Required</span></span> |<span data-ttu-id="7f357-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="7f357-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="7f357-354">Voorbeeld piek-eenheid.</span><span class="sxs-lookup"><span data-stu-id="7f357-354">Sample peak unit.</span></span> |
| <span data-ttu-id="7f357-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="7f357-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="7f357-356">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-356">Required</span></span> |<span data-ttu-id="7f357-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="7f357-357">**xs:float**</span></span> |<span data-ttu-id="7f357-358">Maximale true piekwaarde, volgens de ITU-R BS.1770-2, sinds opnieuw instellen of nadat deze is uitgeschakeld, per kanaal.</span><span class="sxs-lookup"><span data-stu-id="7f357-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="7f357-359">Eenheden zijn dBTP.</span><span class="sxs-lookup"><span data-stu-id="7f357-359">Units are dBTP.</span></span> |
| <span data-ttu-id="7f357-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="7f357-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="7f357-361">vaste = "dBTP"</span><span class="sxs-lookup"><span data-stu-id="7f357-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="7f357-362">Vereist</span><span class="sxs-lookup"><span data-stu-id="7f357-362">Required</span></span> |<span data-ttu-id="7f357-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="7f357-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="7f357-364">De waarde True Piekeenheid.</span><span class="sxs-lookup"><span data-stu-id="7f357-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="7f357-365">Schema-Code</span><span class="sxs-lookup"><span data-stu-id="7f357-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
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
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order tooproduce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
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
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
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
                            <xs:attribute name="Framerate" use="required">  
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
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second</xs:documentation>  
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
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over hello program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
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
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
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
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <span data-ttu-id="7f357-366"><a name="xml"></a>XML-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="7f357-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="7f357-367">Hallo Hieronder volgt een voorbeeld van Hallo metagegevens uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="7f357-367">hello following is an example of hello Output metadata file.</span></span>  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="7f357-368">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f357-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7f357-369">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="7f357-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
