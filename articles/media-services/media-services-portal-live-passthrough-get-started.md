---
title: Live streamen met on-premises coderingsprogramma's via Azure Portal | Microsoft Docs
description: In deze zelfstudie wordt u begeleid bij het maken van een kanaal dat is geconfigureerd voor een doorvoerlevering.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 6939e3b31c3c1b514df4c559c2d9408fce122a4e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-the-azure-portal"></a><span data-ttu-id="2cccc-103">Live streamen met on-premises coderingsprogramma's via Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2cccc-103">How to perform live streaming with on-premises encoders using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2cccc-104">Portal</span><span class="sxs-lookup"><span data-stu-id="2cccc-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="2cccc-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2cccc-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="2cccc-106">REST</span><span class="sxs-lookup"><span data-stu-id="2cccc-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="2cccc-107">Deze zelfstudie bevat de stappen voor het maken van een **kanaal** via Azure Portal dat is geconfigureerd voor een doorvoerlevering.</span><span class="sxs-lookup"><span data-stu-id="2cccc-107">This tutorial walks you through the steps of using the Azure portal to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2cccc-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2cccc-108">Prerequisites</span></span>
<span data-ttu-id="2cccc-109">Hieronder wordt aangegeven wat de vereisten zijn om de zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="2cccc-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="2cccc-110">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="2cccc-110">An Azure account.</span></span> <span data-ttu-id="2cccc-111">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2cccc-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="2cccc-112">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="2cccc-112">A Media Services account.</span></span> <span data-ttu-id="2cccc-113">Zie [Een Media Services-account maken](media-services-portal-create-account.md) voor meer informatie over het maken van een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="2cccc-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="2cccc-114">Een webcam.</span><span class="sxs-lookup"><span data-stu-id="2cccc-114">A webcam.</span></span> <span data-ttu-id="2cccc-115">Bijvoorbeeld [Telestream Wirecast-coderingsprogramma](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="2cccc-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="2cccc-116">Het wordt ten zeerste aanbevolen de volgende artikelen te lezen:</span><span class="sxs-lookup"><span data-stu-id="2cccc-116">It is highly recommended to review the following articles:</span></span>

* [<span data-ttu-id="2cccc-117">Azure Media Services RTMP-ondersteuning en live coderingsprogramma's</span><span class="sxs-lookup"><span data-stu-id="2cccc-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="2cccc-118">Overzicht van live streamen met Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="2cccc-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="2cccc-119">Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken</span><span class="sxs-lookup"><span data-stu-id="2cccc-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="2cccc-120"><a id="scenario"></a>Algemeen scenario voor live streamen</span><span class="sxs-lookup"><span data-stu-id="2cccc-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="2cccc-121">In de volgende stappen worden de taken beschreven voor het maken van algemene toepassingen voor live streamen die kanalen gebruiken die zijn geconfigureerd voor doorvoerlevering.</span><span class="sxs-lookup"><span data-stu-id="2cccc-121">The following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="2cccc-122">In deze zelfstudie wordt getoond hoe een doorvoerkanaal en live gebeurtenissen worden gemaakt en beheerd.</span><span class="sxs-lookup"><span data-stu-id="2cccc-122">This tutorial shows how to create and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="2cccc-123">Controleer of het streaming-eindpunt van waar u inhoud wilt streamen, de status **Wordt uitgevoerd** heeft.</span><span class="sxs-lookup"><span data-stu-id="2cccc-123">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
1. <span data-ttu-id="2cccc-124">Sluit een videocamera aan op een computer.</span><span class="sxs-lookup"><span data-stu-id="2cccc-124">Connect a video camera to a computer.</span></span> <span data-ttu-id="2cccc-125">Start en configureer een on-premises live coderingsprogramma waarmee een multi-bitrate RTMP- of Fragmented MP4-stream wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2cccc-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="2cccc-126">Zie [Azure Media Services RTMP-ondersteuning en live coderingsprogramma's](http://go.microsoft.com/fwlink/?LinkId=532824) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2cccc-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="2cccc-127">Deze stap kan ook worden uitgevoerd nadat u uw kanaal hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2cccc-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="2cccc-128">Maak en start een doorvoerkanaal.</span><span class="sxs-lookup"><span data-stu-id="2cccc-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="2cccc-129">Haal de URL voor opnemen voor het kanaal op.</span><span class="sxs-lookup"><span data-stu-id="2cccc-129">Retrieve the Channel ingest URL.</span></span> 
   
    <span data-ttu-id="2cccc-130">De URL voor opnemen wordt gebruikt door het live coderingsprogramma om de stream naar het kanaal te verzenden.</span><span class="sxs-lookup"><span data-stu-id="2cccc-130">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>
4. <span data-ttu-id="2cccc-131">Haal de voorbeeld-URL voor het kanaal op.</span><span class="sxs-lookup"><span data-stu-id="2cccc-131">Retrieve the Channel preview URL.</span></span> 
   
    <span data-ttu-id="2cccc-132">Gebruik deze URL om te controleren of de livestream goed door het kanaal wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="2cccc-132">Use this URL to verify that your channel is properly receiving the live stream.</span></span>
5. <span data-ttu-id="2cccc-133">Maak een live gebeurtenis/programma.</span><span class="sxs-lookup"><span data-stu-id="2cccc-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="2cccc-134">Wanneer u Azure Portal gebruikt, wordt bij het maken van een live gebeurtenis ook een asset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2cccc-134">When using the Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="2cccc-135">Start de gebeurtenis/het programma wanneer u klaar bent om te streamen en te archiveren.</span><span class="sxs-lookup"><span data-stu-id="2cccc-135">Start the event/program when you are ready to start streaming and archiving.</span></span>
7. <span data-ttu-id="2cccc-136">Het live coderingsprogramma kan desgewenst een signaal ontvangen dat een advertentie moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="2cccc-136">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="2cccc-137">De advertentie wordt ingevoegd in de uitvoerstream.</span><span class="sxs-lookup"><span data-stu-id="2cccc-137">The advertisement is inserted in the output stream.</span></span>
8. <span data-ttu-id="2cccc-138">Stop de gebeurtenis/het programma als u het streamen wilt stoppen en de gebeurtenis wilt archiveren.</span><span class="sxs-lookup"><span data-stu-id="2cccc-138">Stop the event/program whenever you want to stop streaming and archiving the event.</span></span>
9. <span data-ttu-id="2cccc-139">Verwijder de gebeurtenis/het programma (en verwijder desgewenst de asset).</span><span class="sxs-lookup"><span data-stu-id="2cccc-139">Delete the event/program (and optionally delete the asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="2cccc-140">Zie [Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md) voor meer informatie over de concepten en overwegingen ten aanzien van live streamen met on-premises coderingsprogramma's en doorvoerkanalen.</span><span class="sxs-lookup"><span data-stu-id="2cccc-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) to learn about concepts and considerations related to live streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="to-view-notifications-and-errors"></a><span data-ttu-id="2cccc-141">Meldingen en fouten weergeven</span><span class="sxs-lookup"><span data-stu-id="2cccc-141">To view notifications and errors</span></span>
<span data-ttu-id="2cccc-142">Als u de meldingen en fouten wilt weergeven die door Azure Portal zijn gegenereerd, klikt u op het pictogram Melding.</span><span class="sxs-lookup"><span data-stu-id="2cccc-142">If you want to view notifications and errors produced by the Azure portal, click on the Notification icon.</span></span>

![Meldingen](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="2cccc-144">Doorvoerkanalen en gebeurtenissen maken en starten</span><span class="sxs-lookup"><span data-stu-id="2cccc-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="2cccc-145">Een kanaal is gekoppeld aan gebeurtenissen/programma's waarmee u het publiceren en opslaan van segmenten in een live stream kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="2cccc-145">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="2cccc-146">Kanalen beheren gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="2cccc-146">Channels manage events.</span></span> 

<span data-ttu-id="2cccc-147">U kunt het aantal uren opgeven dat u de opgenomen inhoud voor het programma wilt behouden door de lengte voor **Archiefvenster** in te stellen.</span><span class="sxs-lookup"><span data-stu-id="2cccc-147">You can specify the number of hours you want to retain the recorded content for the program by setting the **Archive Window** length.</span></span> <span data-ttu-id="2cccc-148">Deze waarde kan worden ingesteld van minimaal 5 minuten tot maximaal 25 uur.</span><span class="sxs-lookup"><span data-stu-id="2cccc-148">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span></span> <span data-ttu-id="2cccc-149">De lengte van een archiefvenster bepaalt ook de maximale hoeveelheid tijd die clients terug in de tijd kunnen zoeken vanaf de huidige live positie.</span><span class="sxs-lookup"><span data-stu-id="2cccc-149">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span></span> <span data-ttu-id="2cccc-150">Gebeurtenissen kunnen in de opgegeven tijdsduur worden uitgevoerd, maar de inhoud die achter de lengte van het venster valt, wordt altijd verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2cccc-150">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span></span> <span data-ttu-id="2cccc-151">De waarde van deze eigenschap bepaalt ook hoe lang de clientmanifesten kunnen groeien.</span><span class="sxs-lookup"><span data-stu-id="2cccc-151">This value of this property also determines how long the client manifests can grow.</span></span>

<span data-ttu-id="2cccc-152">Elke gebeurtenis is gekoppeld aan een asset.</span><span class="sxs-lookup"><span data-stu-id="2cccc-152">Each event is associated with an asset.</span></span> <span data-ttu-id="2cccc-153">Als u de gebeurtenis wilt publiceren, moet u een OnDemand-locator voor de gekoppelde asset maken.</span><span class="sxs-lookup"><span data-stu-id="2cccc-153">To publish the event, you must create an OnDemand locator for the associated asset.</span></span> <span data-ttu-id="2cccc-154">Met deze locator kunt u een streaming-URL maken die u aan uw clients kunt leveren.</span><span class="sxs-lookup"><span data-stu-id="2cccc-154">Having this locator enables you to build a streaming URL that you can provide to your clients.</span></span>

<span data-ttu-id="2cccc-155">Een kanaal ondersteunt maximaal drie gelijktijdig actieve gebeurtenissen, zodat u meerdere archieven van dezelfde binnenkomende stream kunt maken.</span><span class="sxs-lookup"><span data-stu-id="2cccc-155">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span></span> <span data-ttu-id="2cccc-156">Hierdoor kunt u verschillende onderdelen van een gebeurtenis naar behoefte publiceren en archiveren.</span><span class="sxs-lookup"><span data-stu-id="2cccc-156">This allows you to publish and archive different parts of an event as needed.</span></span> <span data-ttu-id="2cccc-157">Zo kan het voor uw bedrijf nodig zijn zes uur van een programma te archiveren, maar alleen de laatste tien minuten uit te zenden.</span><span class="sxs-lookup"><span data-stu-id="2cccc-157">For example, your business requirement is to archive 6 hours of a program, but to broadcast only last 10 minutes.</span></span> <span data-ttu-id="2cccc-158">Hiervoor moet u twee gelijktijdig actieve programma's maken.</span><span class="sxs-lookup"><span data-stu-id="2cccc-158">To accomplish this, you need to create two concurrently running programs.</span></span> <span data-ttu-id="2cccc-159">Het ene programma wordt ingesteld om zes uur van de gebeurtenis te archiveren, maar het programma wordt niet gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="2cccc-159">One program is set to archive 6 hours of the event but the program is not published.</span></span> <span data-ttu-id="2cccc-160">Het andere programma wordt ingesteld om tien minuten te archiveren en dit programma wordt wel gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="2cccc-160">The other program is set to archive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="2cccc-161">Gebruik de bestaande live gebeurtenissen niet opnieuw.</span><span class="sxs-lookup"><span data-stu-id="2cccc-161">You should not reuse existing live events.</span></span> <span data-ttu-id="2cccc-162">In plaats daarvan maakt en start u een nieuwe gebeurtenis voor elke gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2cccc-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="2cccc-163">Start de gebeurtenis wanneer u klaar bent om te streamen en te archiveren.</span><span class="sxs-lookup"><span data-stu-id="2cccc-163">Start the event when you are ready to start streaming and archiving.</span></span> <span data-ttu-id="2cccc-164">Stop het programma als u het streamen wilt stoppen en de gebeurtenis wilt archiveren.</span><span class="sxs-lookup"><span data-stu-id="2cccc-164">Stop the program whenever you want to stop streaming and archiving the event.</span></span> 

<span data-ttu-id="2cccc-165">Als u de gearchiveerde inhoud wilt verwijderen, stopt en verwijdert u de gebeurtenis en verwijdert u vervolgens de gekoppelde asset.</span><span class="sxs-lookup"><span data-stu-id="2cccc-165">To delete archived content, stop and delete the event and then delete the associated asset.</span></span> <span data-ttu-id="2cccc-166">Een asset kan niet worden verwijderd als deze wordt gebruikt door een gebeurtenis. U moet eerst de gebeurtenis verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2cccc-166">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="2cccc-167">Zelfs na het stoppen en verwijderen van de gebeurtenis kunnen gebruikers de gearchiveerde inhoud als video op aanvraag streamen, mits u de asset niet hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2cccc-167">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span>

<span data-ttu-id="2cccc-168">Als u de gearchiveerde inhoud wilt behouden maar deze niet langer voor streaming beschikbaar mag zijn, verwijdert u de streaming-locator.</span><span class="sxs-lookup"><span data-stu-id="2cccc-168">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span></span>

### <a name="to-use-the-portal-to-create-a-channel"></a><span data-ttu-id="2cccc-169">De portal gebruiken om een kanaal te maken</span><span class="sxs-lookup"><span data-stu-id="2cccc-169">To use the portal to create a channel</span></span>
<span data-ttu-id="2cccc-170">In deze secties ziet u hoe u de optie **Snelle invoer** gebruikt om een doorvoerkanaal te maken.</span><span class="sxs-lookup"><span data-stu-id="2cccc-170">This section shows how to use the **Quick Create** option to create a pass-through channel.</span></span>

<span data-ttu-id="2cccc-171">Zie [Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md) voor meer informatie over doorvoerkanalen.</span><span class="sxs-lookup"><span data-stu-id="2cccc-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="2cccc-172">Selecteer uw Azure Media Services-account in [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2cccc-172">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="2cccc-173">Klik in het venster **Instellingen** op **Live streamen**.</span><span class="sxs-lookup"><span data-stu-id="2cccc-173">In the **Settings** window, click **Live streaming**.</span></span> 
   
    ![Aan de slag](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="2cccc-175">Het venster **Live streamen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2cccc-175">The **Live streaming** window appears.</span></span>
3. <span data-ttu-id="2cccc-176">Klik op **Snelle invoer** om een doorvoerkanaal te maken met het RTMP-opnameprotocol.</span><span class="sxs-lookup"><span data-stu-id="2cccc-176">Click **Quick Create** to create a pass-through channel with the RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="2cccc-177">Het venster **EEN NIEUW KANAAL MAKEN** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2cccc-177">The **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="2cccc-178">Geef het nieuwe kanaal een naam en klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="2cccc-178">Give the new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="2cccc-179">Hierop wordt een doorvoerkanaal gemaakt met het RTMP-opnameprotocol.</span><span class="sxs-lookup"><span data-stu-id="2cccc-179">This creates a pass-through channel with the RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="2cccc-180">Gebeurtenissen maken</span><span class="sxs-lookup"><span data-stu-id="2cccc-180">Create events</span></span>
1. <span data-ttu-id="2cccc-181">Selecteer een kanaal waaraan u een gebeurtenis wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2cccc-181">Select a channel to which you want to add an event.</span></span>
2. <span data-ttu-id="2cccc-182">Klik op de knop **Live gebeurtenis**.</span><span class="sxs-lookup"><span data-stu-id="2cccc-182">Press **Live Event** button.</span></span>

![Gebeurtenis](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="2cccc-184">URL’s voor opnemen ophalen</span><span class="sxs-lookup"><span data-stu-id="2cccc-184">Get ingest URLs</span></span>
<span data-ttu-id="2cccc-185">Wanneer het kanaal is gemaakt, kunt u URL’s voor opnemen ophalen die u aan het live coderingsprogramma levert.</span><span class="sxs-lookup"><span data-stu-id="2cccc-185">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span></span> <span data-ttu-id="2cccc-186">Het coderingsprogramma gebruikt deze URL's voor het invoeren van een live stream.</span><span class="sxs-lookup"><span data-stu-id="2cccc-186">The encoder uses these URLs to input a live stream.</span></span>

![Gemaakt](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-the-event"></a><span data-ttu-id="2cccc-188">De gebeurtenis bekijken</span><span class="sxs-lookup"><span data-stu-id="2cccc-188">Watch the event</span></span>
<span data-ttu-id="2cccc-189">Als u een gebeurtenis wilt bekijken, klikt u op **Bekijken** in Azure Portal of kopieert u de streaming-URL en gebruikt u een speler van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="2cccc-189">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span></span> 

![Gemaakt](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="2cccc-191">De live gebeurtenis wordt automatisch geconverteerd naar inhoud op aanvraag wanneer deze wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="2cccc-191">Live event automatically get converted to on-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="2cccc-192">Opruimen</span><span class="sxs-lookup"><span data-stu-id="2cccc-192">Clean up</span></span>
<span data-ttu-id="2cccc-193">Zie [Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md) voor meer informatie over doorvoerkanalen.</span><span class="sxs-lookup"><span data-stu-id="2cccc-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="2cccc-194">Een kanaal kan alleen worden gestopt, wanneer alle gebeurtenissen/programma's op het kanaal zijn gestopt.</span><span class="sxs-lookup"><span data-stu-id="2cccc-194">A channel can be stopped only when all events/programs on the channel have been stopped.</span></span>  <span data-ttu-id="2cccc-195">Nadat het kanaal is gestopt, worden hiervoor geen kosten meer in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="2cccc-195">Once the Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="2cccc-196">Als u het kanaal opnieuw wilt starten, wordt dezelfde URL voor opnemen gebruikt, zodat u het coderingsprogramma niet opnieuw hoeft te configureren.</span><span class="sxs-lookup"><span data-stu-id="2cccc-196">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span></span>
* <span data-ttu-id="2cccc-197">Een kanaal kan alleen worden verwijderd, wanneer alle live gebeurtenissen op het kanaal zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2cccc-197">A channel can be deleted only when all live events on the channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="2cccc-198">Gearchiveerde inhoud weergeven</span><span class="sxs-lookup"><span data-stu-id="2cccc-198">View archived content</span></span>
<span data-ttu-id="2cccc-199">Zelfs na het stoppen en verwijderen van de gebeurtenis kunnen gebruikers de gearchiveerde inhoud als video op aanvraag streamen, mits u de asset niet hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2cccc-199">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span> <span data-ttu-id="2cccc-200">Een asset kan niet worden verwijderd als deze wordt gebruikt door een gebeurtenis. U moet eerst de gebeurtenis verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2cccc-200">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="2cccc-201">Voor het beheren van uw assets selecteert u **Instelling** en klikt u vervolgens op **Assets**.</span><span class="sxs-lookup"><span data-stu-id="2cccc-201">To manage your assets, select **Setting** and click **Assets**.</span></span>

![Assets](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="2cccc-203">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="2cccc-203">Next step</span></span>
<span data-ttu-id="2cccc-204">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="2cccc-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2cccc-205">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="2cccc-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

