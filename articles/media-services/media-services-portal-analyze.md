---
title: aaaAnalyze uw media met Azure-portal Hallo | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe tooprocess uw media met Media Analytics-mediaprocessoren (Management Packs) met behulp van hello Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="2a660-103">Analyseer uw media met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2a660-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="2a660-104">toocomplete in deze zelfstudie, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="2a660-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="2a660-105">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2a660-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="2a660-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2a660-106">Overview</span></span>
<span data-ttu-id="2a660-107">Azure Media Services Analytics is een verzameling spraakonderdelen en visuele onderdelen (op enterprise schaal, naleving, beveiliging en globale bereiken) waarmee het eenvoudiger voor organisaties en bedrijven tooderive bruikbare inzichten aan hun video's.</span><span class="sxs-lookup"><span data-stu-id="2a660-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="2a660-108">Zie voor meer overzicht van Azure Media Services Analytics [dit](media-services-analytics-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="2a660-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="2a660-109">Dit onderwerp wordt beschreven hoe tooprocess uw media met Media Analytics-mediaprocessoren (Management Packs) met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2a660-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="2a660-110">Media Analytics Management Packs produceren MP4-bestanden of JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="2a660-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="2a660-111">Als een Mediaprocessor een MP4-bestand, kunt u Hallo bestand progressief downloaden.</span><span class="sxs-lookup"><span data-stu-id="2a660-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="2a660-112">Als een Mediaprocessor een JSON-bestand, kunt u Hallo-bestand downloaden van hello Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="2a660-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="2a660-113">Kies een asset die u tooanalyze wilt</span><span class="sxs-lookup"><span data-stu-id="2a660-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="2a660-114">In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="2a660-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="2a660-115">In Hallo **instellingen** Selecteer **activa**.</span><span class="sxs-lookup"><span data-stu-id="2a660-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="2a660-116">.</span><span class="sxs-lookup"><span data-stu-id="2a660-116">.</span></span>
    <span data-ttu-id="2a660-117">![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="2a660-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="2a660-118">Selecteer Hallo asset die u wilt dat tooanalyze en druk op Hallo **analyseren** knop.</span><span class="sxs-lookup"><span data-stu-id="2a660-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="2a660-120">In Hallo **proces media asset met Media Analytics** venster, selecteer Hallo-processor.</span><span class="sxs-lookup"><span data-stu-id="2a660-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="2a660-121">Hallo rest van Hallo artikel wordt uitgelegd waarom en hoe toouse elke processor.</span><span class="sxs-lookup"><span data-stu-id="2a660-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="2a660-122">Druk op **maken** toohello start een taak.</span><span class="sxs-lookup"><span data-stu-id="2a660-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="2a660-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="2a660-123">Azure Media Indexer</span></span>
<span data-ttu-id="2a660-124">Hallo **Azure Media Indexer** Mediaprocessor kunt u toomake media-bestanden en inhoud kan worden doorzocht, evenals gesloten closed captioning houdt genereren.</span><span class="sxs-lookup"><span data-stu-id="2a660-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="2a660-125">In deze sectie biedt een aantal details van de opties die u voor deze MP opgeven kunt.</span><span class="sxs-lookup"><span data-stu-id="2a660-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="2a660-127">Taal</span><span class="sxs-lookup"><span data-stu-id="2a660-127">Language</span></span>
<span data-ttu-id="2a660-128">Hallo natuurlijke taal toobe herkend in multimedia Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="2a660-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="2a660-129">Engels of Spaans.</span><span class="sxs-lookup"><span data-stu-id="2a660-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="2a660-130">Bijschriften</span><span class="sxs-lookup"><span data-stu-id="2a660-130">Captions</span></span>
<span data-ttu-id="2a660-131">U kunt een bijschrift-indeling die zal worden gegenereerd op basis van uw inhoud.</span><span class="sxs-lookup"><span data-stu-id="2a660-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="2a660-132">Een indexing-taak kan ondertitelingsbestanden bestanden in de volgende indelingen Hallo genereren:</span><span class="sxs-lookup"><span data-stu-id="2a660-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="2a660-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="2a660-133">**SAMI**</span></span>
* <span data-ttu-id="2a660-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="2a660-134">**TTML**</span></span>
* <span data-ttu-id="2a660-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="2a660-135">**WebVTT**</span></span>

<span data-ttu-id="2a660-136">Gesloten bijschrift (CC)-bestanden in de volgende indelingen kunnen worden gebruikt toomake audio en video bestanden toegankelijk toopeople met handicap horen.</span><span class="sxs-lookup"><span data-stu-id="2a660-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="2a660-137">AIB bestand</span><span class="sxs-lookup"><span data-stu-id="2a660-137">AIB file</span></span>
<span data-ttu-id="2a660-138">Selecteer deze optie als u zou zoals toogenerate Hallo Audio Index Blob-bestand voor gebruik met Hallo IFilter van aangepaste SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="2a660-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="2a660-139">Zie voor meer informatie [dit](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span><span class="sxs-lookup"><span data-stu-id="2a660-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="2a660-140">Trefwoorden</span><span class="sxs-lookup"><span data-stu-id="2a660-140">Keywords</span></span>
<span data-ttu-id="2a660-141">Selecteer deze optie als u toogenerate een trefwoorden XML-bestand wilt.</span><span class="sxs-lookup"><span data-stu-id="2a660-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="2a660-142">Dit bestand bevat trefwoorden geëxtraheerd uit Hallo spraak inhoud, met de frequentie en offset informatie.</span><span class="sxs-lookup"><span data-stu-id="2a660-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="2a660-143">Taaknaam</span><span class="sxs-lookup"><span data-stu-id="2a660-143">Job name</span></span>
<span data-ttu-id="2a660-144">Een beschrijvende naam waarmee u Hallo taak identificeren.</span><span class="sxs-lookup"><span data-stu-id="2a660-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="2a660-145">[Dit](media-services-portal-check-job-progress.md) artikel wordt beschreven hoe u de voortgang van een taak Hallo kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="2a660-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2a660-146">Bestand voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="2a660-146">Output file</span></span>
<span data-ttu-id="2a660-147">Een beschrijvende naam waarmee u Hallo uitvoer inhoud identificeren.</span><span class="sxs-lookup"><span data-stu-id="2a660-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="2a660-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="2a660-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="2a660-149">Azure Media Hyperlapse is een Management Pack dat smooth video's verstreken tijd van eerste persoon of actie camera inhoud maakt.</span><span class="sxs-lookup"><span data-stu-id="2a660-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="2a660-150">Raadpleeg [dit](media-services-hyperlapse-content.md) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2a660-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="2a660-151">In deze sectie biedt een aantal details van de opties die u voor deze MP opgeven kunt.</span><span class="sxs-lookup"><span data-stu-id="2a660-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="2a660-153">Snelheid</span><span class="sxs-lookup"><span data-stu-id="2a660-153">Speed</span></span>
<span data-ttu-id="2a660-154">Hallo snelheid met welke toospeed up Hallo invoervideo opgeven.</span><span class="sxs-lookup"><span data-stu-id="2a660-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="2a660-155">Hallo-uitvoer is een weergave gestabiliseerd en verstreken tijd van Hallo invoervideo.</span><span class="sxs-lookup"><span data-stu-id="2a660-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="2a660-156">Taaknaam</span><span class="sxs-lookup"><span data-stu-id="2a660-156">Job name</span></span>
<span data-ttu-id="2a660-157">Een beschrijvende naam waarmee u Hallo taak identificeren.</span><span class="sxs-lookup"><span data-stu-id="2a660-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="2a660-158">[Dit](media-services-portal-check-job-progress.md) artikel wordt beschreven hoe u de voortgang van een taak Hallo kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="2a660-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2a660-159">Bestand voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="2a660-159">Output file</span></span>
<span data-ttu-id="2a660-160">Een beschrijvende naam waarmee u Hallo uitvoer inhoud identificeren.</span><span class="sxs-lookup"><span data-stu-id="2a660-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="2a660-161">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="2a660-161">Azure Media Face Detector</span></span>
<span data-ttu-id="2a660-162">Hallo **Azure Media Face detectie** Mediaprocessor (MP) kunt u toocount, de bewegingen bijhouden, en zelfs meter doelgroep deelname en reactie via bedacht.</span><span class="sxs-lookup"><span data-stu-id="2a660-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="2a660-163">Deze service bevat twee functies:</span><span class="sxs-lookup"><span data-stu-id="2a660-163">This service contains two features:</span></span> 

* <span data-ttu-id="2a660-164">**Face-detectie**</span><span class="sxs-lookup"><span data-stu-id="2a660-164">**Face detection**</span></span>
  
    <span data-ttu-id="2a660-165">Face-detectie zoekt en houdt menselijke vlakken binnen een video.</span><span class="sxs-lookup"><span data-stu-id="2a660-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="2a660-166">Meerdere vlakken kunnen worden gedetecteerd en vervolgens worden bijgehouden als ze onderweg, met Hallo-metagegevens en de locatie geretourneerd in een JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="2a660-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="2a660-167">Tijdens de bijhouden, wordt geprobeerd toogive een consistente ID toohello dezelfde geconfronteerd terwijl Hallo persoon is navigeren op het scherm, zelfs als ze zijn ondervindt hinder van obstakels of kort Hallo frame laat.</span><span class="sxs-lookup"><span data-stu-id="2a660-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2a660-168">Deze services voert geen gezichtsherkenning.</span><span class="sxs-lookup"><span data-stu-id="2a660-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="2a660-169">Een persoon die Hallo frame verlaat of ondervindt voor wordt hinder van obstakels te lang krijgt een nieuwe ID wanneer ze terugkeren.</span><span class="sxs-lookup"><span data-stu-id="2a660-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="2a660-170">**Emotiedetectie**</span><span class="sxs-lookup"><span data-stu-id="2a660-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="2a660-171">Emotiedetectie is een optioneel onderdeel van Hallo Face Detection Media Processor op dat analyse op meerdere emotionele kenmerken van Hallo vlakken gedetecteerd retourneert, met inbegrip van gelukkig, sadness bang, volgt uitzien en meer.</span><span class="sxs-lookup"><span data-stu-id="2a660-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="2a660-173">Modus voor detectie</span><span class="sxs-lookup"><span data-stu-id="2a660-173">Detection mode</span></span>
<span data-ttu-id="2a660-174">Een van de volgende modi Hallo kan worden gebruikt door Hallo processor:</span><span class="sxs-lookup"><span data-stu-id="2a660-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="2a660-175">Face-detectie</span><span class="sxs-lookup"><span data-stu-id="2a660-175">face detection</span></span>
* <span data-ttu-id="2a660-176">per emotiedetectie face</span><span class="sxs-lookup"><span data-stu-id="2a660-176">per face emotion detection</span></span>
* <span data-ttu-id="2a660-177">cumulatieve emotiedetectie</span><span class="sxs-lookup"><span data-stu-id="2a660-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="2a660-178">Taaknaam</span><span class="sxs-lookup"><span data-stu-id="2a660-178">Job name</span></span>
<span data-ttu-id="2a660-179">Een beschrijvende naam waarmee u Hallo taak identificeren.</span><span class="sxs-lookup"><span data-stu-id="2a660-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="2a660-180">[Dit](media-services-portal-check-job-progress.md) artikel wordt beschreven hoe u de voortgang van een taak Hallo kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="2a660-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2a660-181">Bestand voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="2a660-181">Output file</span></span>
<span data-ttu-id="2a660-182">Een beschrijvende naam waarmee u Hallo uitvoer inhoud identificeren.</span><span class="sxs-lookup"><span data-stu-id="2a660-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="2a660-183">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="2a660-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="2a660-184">Hallo **Azure Media beweging detectie** media processor (MP) kunt u tooefficiently secties van belang zijn binnen een video anders lang en probleemloze identificeren.</span><span class="sxs-lookup"><span data-stu-id="2a660-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="2a660-185">Bewegingsdetectie kan worden gebruikt voor statische camera beeldmateriaal tooidentify secties van Hallo video waar beweging optreedt.</span><span class="sxs-lookup"><span data-stu-id="2a660-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="2a660-186">Er wordt een JSON-bestand met een metagegevens met tijdstempels en de regio waar Hallo gebeurtenis heeft plaatsgevonden voor begrenzingsvak Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="2a660-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="2a660-187">Gericht op beveiliging video feeds, is deze technologie kunnen toocategorize beweging in de relevante gebeurtenissen en fout-positieven zoals schaduwen en licht wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="2a660-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="2a660-188">Hiermee kunt u toogenerate beveiligingswaarschuwingen van de camera feeds zonder terwijl tooextract kunnen momenten van belang van zeer lange toezicht video's met oneindige irrelevante gebeurtenissen, spam.</span><span class="sxs-lookup"><span data-stu-id="2a660-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="2a660-190">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="2a660-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="2a660-191">Deze processor kunt u bij het maken van samenvattingen van lange video's door interessante codefragmenten automatisch selecteren van bronvideo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a660-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="2a660-192">Dit is handig als u wilt dat een snel overzicht van welke tooexpect in een lange video tooprovide.</span><span class="sxs-lookup"><span data-stu-id="2a660-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="2a660-193">Zie voor gedetailleerde informatie en voorbeelden [gebruik Azure Media Video Thumbnails tooCreate samenvatting van een Video](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="2a660-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="2a660-195">Taaknaam</span><span class="sxs-lookup"><span data-stu-id="2a660-195">Job name</span></span>
<span data-ttu-id="2a660-196">Een beschrijvende naam waarmee u Hallo taak identificeren.</span><span class="sxs-lookup"><span data-stu-id="2a660-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="2a660-197">[Dit](media-services-portal-check-job-progress.md) artikel wordt beschreven hoe u de voortgang van een taak Hallo kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="2a660-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2a660-198">Bestand voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="2a660-198">Output file</span></span>
<span data-ttu-id="2a660-199">Een beschrijvende naam waarmee u Hallo uitvoer inhoud identificeren.</span><span class="sxs-lookup"><span data-stu-id="2a660-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2a660-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a660-200">Next steps</span></span>
<span data-ttu-id="2a660-201">Weergave Media Services-leertrajecten.</span><span class="sxs-lookup"><span data-stu-id="2a660-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2a660-202">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="2a660-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

