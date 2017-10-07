---
title: aaaRedact vlakken met Azure Media Analytics stapsgewijze Kennismaking | Microsoft Docs
description: Dit onderwerp bevat stapsgewijze instructies over het toorun een volledige redactie werkstroom met behulp van Azure Media Services Explorer (AMSE) en Azure Media Redactor Visualizer (open-source hulpprogramma).
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="02bbd-103">Redigeren vlakken met Azure Media Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="02bbd-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="02bbd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="02bbd-104">Overview</span></span>

<span data-ttu-id="02bbd-105">**Azure Media Redactor** is een [Azure Media Analytics](media-services-analytics-overview.md) Mediaprocessor (MP) die schaalbare face redactie in Hallo cloud biedt.</span><span class="sxs-lookup"><span data-stu-id="02bbd-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="02bbd-106">Face redactie kunt u toomodify uw video in volgorde tooblur vlakken van geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="02bbd-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="02bbd-107">U kunt toouse Hallo face redactie service in openbare veiligheid en nieuws media scenario's.</span><span class="sxs-lookup"><span data-stu-id="02bbd-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="02bbd-108">Een paar minuten beeldmateriaal waarin meerdere vlakken handmatig tooredact uur kunnen duren, maar met deze service Hallo face redactie proces een paar eenvoudige stappen is vereist.</span><span class="sxs-lookup"><span data-stu-id="02bbd-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="02bbd-109">Zie voor meer informatie [dit](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span><span class="sxs-lookup"><span data-stu-id="02bbd-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="02bbd-110">Voor meer informatie over **Azure Media Redactor**, Zie Hallo [Face redactie overzicht](media-services-face-redaction.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="02bbd-110">For details about  **Azure Media Redactor**, see hello [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="02bbd-111">Dit onderwerp bevat stapsgewijze instructies over het toorun een volledige redactie werkstroom met behulp van Azure Media Services Explorer (AMSE) en Azure Media Redactor Visualizer (open-source hulpprogramma).</span><span class="sxs-lookup"><span data-stu-id="02bbd-111">This topic shows step by step instructions on how toorun a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="02bbd-112">Hallo **Azure Media Redactor** MP is momenteel in Preview.</span><span class="sxs-lookup"><span data-stu-id="02bbd-112">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="02bbd-113">Is beschikbaar in alle openbare Azure-regio's, evenals US Government en China datacenters.</span><span class="sxs-lookup"><span data-stu-id="02bbd-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="02bbd-114">Dit voorbeeld is momenteel gratis.</span><span class="sxs-lookup"><span data-stu-id="02bbd-114">This preview is currently free of charge.</span></span> <span data-ttu-id="02bbd-115">In de huidige release hello, moet u er een limiet van 10 minuten is op verwerkte video lengte.</span><span class="sxs-lookup"><span data-stu-id="02bbd-115">In hello current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="02bbd-116">Zie voor meer informatie [dit](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span><span class="sxs-lookup"><span data-stu-id="02bbd-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="02bbd-117">Azure Media Services Explorer-werkstroom</span><span class="sxs-lookup"><span data-stu-id="02bbd-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="02bbd-118">Hallo gemakkelijkste manier tooget gestart met Redactor is toouse Hallo open-source AMSE-hulpprogramma op github.</span><span class="sxs-lookup"><span data-stu-id="02bbd-118">hello easiest way tooget started with Redactor is toouse hello open source AMSE tool on github.</span></span> <span data-ttu-id="02bbd-119">U kunt een vereenvoudigde werkstroom via uitvoeren **gecombineerd** modus als u niet toegang toohello aantekening json of Hallo face jpg-afbeeldingen tot moet.</span><span class="sxs-lookup"><span data-stu-id="02bbd-119">You can run a simplified workflow via **combined** mode if you don’t need access toohello annotation json or hello face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="02bbd-120">Downloaden en installeren</span><span class="sxs-lookup"><span data-stu-id="02bbd-120">Download and setup</span></span>

1. <span data-ttu-id="02bbd-121">Download Hallo AMSE-hulpprogramma op [hier](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="02bbd-121">Download hello AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="02bbd-122">Meld u bij tooyour Media Services-account met behulp van de servicesleutel van uw.</span><span class="sxs-lookup"><span data-stu-id="02bbd-122">Log in tooyour Media Services account using your service key.</span></span>

    <span data-ttu-id="02bbd-123">tooobtain Hallo accountnaam en sleutelgegevens, Ga toohello [Azure-portal](https://portal.azure.com/) en selecteert u uw AMS-account.</span><span class="sxs-lookup"><span data-stu-id="02bbd-123">tooobtain hello account name and key information, go toohello [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="02bbd-124">Selecteer deze instellingen > sleutels.</span><span class="sxs-lookup"><span data-stu-id="02bbd-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="02bbd-125">Hallo beheren sleutels windows hello accountnaam ziet en Hallo primaire en secundaire sleutels worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02bbd-125">hello Manage keys windows shows hello account name and hello primary and secondary keys is displayed.</span></span> <span data-ttu-id="02bbd-126">Kopieer de waarden van het Hallo-accountnaam en het Hallo primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="02bbd-126">Copy values of hello account name and hello primary key.</span></span>

![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="02bbd-128">Eerst doorgeven: modus analyseren</span><span class="sxs-lookup"><span data-stu-id="02bbd-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="02bbd-129">Upload uw mediabestand via Asset –> uploaden, of via slepen en neerzetten.</span><span class="sxs-lookup"><span data-stu-id="02bbd-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="02bbd-130">Klik met de rechtermuisknop en verwerken van uw mediabestand Media Analytics met Azure Media Redactor –> –> analyseren modus.</span><span class="sxs-lookup"><span data-stu-id="02bbd-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="02bbd-133">Hallo uitvoer bevat een json-bestand van aantekeningen met face locatiegegevens, evenals een jpg van elke gedetecteerde gezicht.</span><span class="sxs-lookup"><span data-stu-id="02bbd-133">hello output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="02bbd-135">Tweede doorgeven – Redigeren modus</span><span class="sxs-lookup"><span data-stu-id="02bbd-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="02bbd-136">Upload uw oorspronkelijke video asset toohello de uitvoer van de eerste stap Hallo en instellen als primaire activa.</span><span class="sxs-lookup"><span data-stu-id="02bbd-136">Upload your original video asset toohello output from hello first pass and set as a primary asset.</span></span> 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="02bbd-138">(Optioneel) Bestand 'Dance_idlist.txt, waaronder een lijst met locatienamen gescheiden id's die u wenst dat tooredact Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="02bbd-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of hello IDs you wish tooredact.</span></span> 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="02bbd-140">(Optioneel) Elk bewerkingen toohello annotations.json bestand, zoals verhogen Hallo omsluitende vak grenzen maken.</span><span class="sxs-lookup"><span data-stu-id="02bbd-140">(Optional) Make any edits toohello annotations.json file such as increasing hello bounding box boundaries.</span></span> 
4. <span data-ttu-id="02bbd-141">Hallo uitvoerasset van de eerste stap Hallo Klik met de rechtermuisknop, selecteer Hallo Redactor en uitgevoerd met Hallo **Redact** modus.</span><span class="sxs-lookup"><span data-stu-id="02bbd-141">Right click hello output asset from hello first pass, select hello Redactor, and run with hello **Redact** mode.</span></span> 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="02bbd-143">Download of Hallo uiteindelijke geredigeerde uitvoerasset delen.</span><span class="sxs-lookup"><span data-stu-id="02bbd-143">Download or share hello final redacted output asset.</span></span> 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="02bbd-145">Azure Media Redactor Visualizer open-source hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="02bbd-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="02bbd-146">Een open-source [visualizer hulpprogramma](https://github.com/Microsoft/azure-media-redactor-visualizer) ontworpen toohelp ontwikkelaars net begint met de Hallo aantekeningen indeling met parseren en Hallo uitvoer is.</span><span class="sxs-lookup"><span data-stu-id="02bbd-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed toohelp developers just starting with hello annotations format with parsing and using hello output.</span></span>

<span data-ttu-id="02bbd-147">Nadat u Hallo-opslagplaats in volgorde toorun Hallo-project klonen, moet u toodownload FFMPEG van hun [officiële site](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="02bbd-147">After you clone hello repo, in order toorun hello project, you will need toodownload FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="02bbd-148">Als u een ontwikkelaar tooparse Hallo JSON aantekening gegevens probeert, zoekt u in Models.MetaData voorbeeld codevoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="02bbd-148">If you are a developer trying tooparse hello JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-hello-tool"></a><span data-ttu-id="02bbd-149">Hallo hulpprogramma instellen</span><span class="sxs-lookup"><span data-stu-id="02bbd-149">Set up hello tool</span></span>

1.  <span data-ttu-id="02bbd-150">Download en bouw de volledige oplossing Hallo.</span><span class="sxs-lookup"><span data-stu-id="02bbd-150">Download and build hello entire solution.</span></span> 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="02bbd-152">Download FFMPEG van [hier](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="02bbd-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="02bbd-153">Dit project is oorspronkelijk ontwikkeld met versie be1d324 (2016-10-04) met het statisch koppelen.</span><span class="sxs-lookup"><span data-stu-id="02bbd-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="02bbd-154">Kopieer ffmpeg.exe en ffprobe.exe toohello dezelfde uitvoermap als AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="02bbd-154">Copy ffmpeg.exe and ffprobe.exe toohello same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="02bbd-156">AzureMediaRedactor.exe worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="02bbd-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-hello-tool"></a><span data-ttu-id="02bbd-157">Hallo-hulpprogramma gebruiken</span><span class="sxs-lookup"><span data-stu-id="02bbd-157">Use hello tool</span></span>

1. <span data-ttu-id="02bbd-158">Verwerken van uw video in uw Azure Media Services-account met Hallo Redactor MP op analyseren modus.</span><span class="sxs-lookup"><span data-stu-id="02bbd-158">Process your video in your Azure Media Services account with hello Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="02bbd-159">Zowel de oorspronkelijke videobestand Hallo en uitvoer Hallo Hallo redactie downloaden - taak analyseren.</span><span class="sxs-lookup"><span data-stu-id="02bbd-159">Download both hello original video file and hello output of hello Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="02bbd-160">Voer toepassing hello uit visualizer en kies Hallo bestanden hierboven.</span><span class="sxs-lookup"><span data-stu-id="02bbd-160">Run hello visualizer application and choose hello files above.</span></span> 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="02bbd-162">Bekijk het bestand.</span><span class="sxs-lookup"><span data-stu-id="02bbd-162">Preview your file.</span></span> <span data-ttu-id="02bbd-163">Selecteer welke u bespreekt graag tooblur via Hallo zijbalk op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="02bbd-163">Select which faces you'd like tooblur via hello sidebar on hello right.</span></span> 
    
    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="02bbd-165">Hallo onder tekstveld wordt bijgewerkt met de Hallo face id's.</span><span class="sxs-lookup"><span data-stu-id="02bbd-165">hello bottom text field will update with hello face IDs.</span></span> <span data-ttu-id="02bbd-166">Maak een bestand met de naam 'idlist.txt' met deze id als een lijst met locatienamen gescheiden.</span><span class="sxs-lookup"><span data-stu-id="02bbd-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="02bbd-167">Hallo idlist.txt moet worden opgeslagen in ANSI.</span><span class="sxs-lookup"><span data-stu-id="02bbd-167">hello idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="02bbd-168">U kunt Kladblok toosave in ANSI.</span><span class="sxs-lookup"><span data-stu-id="02bbd-168">You can use notepad toosave in ANSI.</span></span>
    
6.  <span data-ttu-id="02bbd-169">Het uploaden van dit bestand toohello uitvoerasset uit stap 1.</span><span class="sxs-lookup"><span data-stu-id="02bbd-169">Upload this file toohello output asset from step 1.</span></span> <span data-ttu-id="02bbd-170">Hallo oorspronkelijke video toothis asset en upload en instellen als primaire asset.</span><span class="sxs-lookup"><span data-stu-id="02bbd-170">Upload hello original video toothis asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="02bbd-171">Redactie taak uitvoeren op dit activum met 'Redact' modus tooget Hallo laatste geredigeerde video.</span><span class="sxs-lookup"><span data-stu-id="02bbd-171">Run Redaction job on this asset with "Redact" mode tooget hello final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="02bbd-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02bbd-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="02bbd-173">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="02bbd-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="02bbd-174">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="02bbd-174">Related links</span></span>
[<span data-ttu-id="02bbd-175">Azure Media Services Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="02bbd-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="02bbd-176">Azure Media Analytics-demo 's</span><span class="sxs-lookup"><span data-stu-id="02bbd-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="02bbd-177">Face-redactie aangekondigd voor Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="02bbd-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
