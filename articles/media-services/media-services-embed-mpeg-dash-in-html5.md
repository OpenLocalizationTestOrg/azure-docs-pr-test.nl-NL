---
title: aaaEmbedding MPEG-DASH adaptieve Streaming Video in een toepassing HTML5 met DASH.js | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe een MPEG-DASH adaptieve Streaming Video in een toepassing HTML5 met DASH.js tooembed.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="64e5d-103">Een MPEG-DASH adaptieve Streaming Video insluiten in een toepassing HTML5 met DASH.js</span><span class="sxs-lookup"><span data-stu-id="64e5d-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="64e5d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="64e5d-104">Overview</span></span>
<span data-ttu-id="64e5d-105">MPEG-DASH is een ISO-norm voor adaptief streamen van video-inhoud, die biedt aanzienlijke voordelen voor gebruikers die toodeliver hoogwaardige, adaptief videostreaming uitvoer wilt Hallo.</span><span class="sxs-lookup"><span data-stu-id="64e5d-105">MPEG-DASH is an ISO standard for hello adaptive streaming of video content, which offers significant benefits for those who wish toodeliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="64e5d-106">Met MPEG-DASH wordt Hallo videostream automatisch tooa lagere definitie verwijderen als Hallo netwerk wordt overbelast.</span><span class="sxs-lookup"><span data-stu-id="64e5d-106">With MPEG-DASH, hello video stream will automatically drop tooa lower definition when hello network becomes congested.</span></span> <span data-ttu-id="64e5d-107">Dit vermindert de kans op Hallo van Hallo viewer 'onderbroken' video bekijken terwijl Hallo player gedownload Hallo naast enkele seconden tooplay (aka buffer).</span><span class="sxs-lookup"><span data-stu-id="64e5d-107">This reduces hello likelihood of hello viewer seeing a "paused" video while hello player downloads hello next few seconds tooplay (aka buffering).</span></span> <span data-ttu-id="64e5d-108">Zoals opstoppingen in het netwerk wordt beperkt, wordt Hallo-speler op zijn beurt tooa hogere quality-stroom geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="64e5d-108">As network congestion reduces, hello video player will in turn return tooa higher quality stream.</span></span> <span data-ttu-id="64e5d-109">Deze mogelijkheid tooadapt Hallo bandbreedte vereist resulteert ook in een snellere begintijd voor video.</span><span class="sxs-lookup"><span data-stu-id="64e5d-109">This ability tooadapt hello bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="64e5d-110">Betekent dat de eerste paar seconden Hallo kunnen worden afgespeeld in een lagere quality-segment van fast te downloaden en doeltreffendere tooa hogere kwaliteit zodra voldoende inhoud zijn gebufferd.</span><span class="sxs-lookup"><span data-stu-id="64e5d-110">That means that hello first few seconds can be played in a fast-to-download lower quality segment and then step up tooa higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="64e5d-111">Dash.js is een open-source MPEG-DASH-speler geschreven in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="64e5d-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="64e5d-112">Het doel is tooprovide een robuuste, platformoverschrijdende-speler vrijelijk in toepassingen waarvoor afspelen van video's kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="64e5d-112">Its goal is tooprovide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="64e5d-113">Het biedt MPEG-DASH afspelen in browsers die ondersteuning biedt voor Hallo W3C Media bron extensies (muis) vandaag zijn Chrome, Microsoft Edge en IE11 (andere browsers hebt aangegeven dat hun opzet toosupport muis).</span><span class="sxs-lookup"><span data-stu-id="64e5d-113">It provides MPEG-DASH playback in any browser that supports hello W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent toosupport MSE).</span></span> <span data-ttu-id="64e5d-114">Js Zie voor meer informatie over DASH.js hello GitHub dash.js-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="64e5d-114">For more information about DASH.js, js see hello GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="64e5d-115">Maken van een browser gebaseerde streaming video-speler</span><span class="sxs-lookup"><span data-stu-id="64e5d-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="64e5d-116">een eenvoudige pagina die wordt weergegeven een video-speler met Hallo verwacht toocreate besturingselementen dergelijke een play, onderbreken, terugspoelen enz., moet u:</span><span class="sxs-lookup"><span data-stu-id="64e5d-116">toocreate a simple web page that displays a video player with hello expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="64e5d-117">Maken van een HTML-pagina</span><span class="sxs-lookup"><span data-stu-id="64e5d-117">Create an HTML page</span></span>
2. <span data-ttu-id="64e5d-118">Hallo video-tag toevoegen</span><span class="sxs-lookup"><span data-stu-id="64e5d-118">Add hello video tag</span></span>
3. <span data-ttu-id="64e5d-119">Hallo dash.js player toevoegen</span><span class="sxs-lookup"><span data-stu-id="64e5d-119">Add hello dash.js player</span></span>
4. <span data-ttu-id="64e5d-120">Hallo player initialiseren</span><span class="sxs-lookup"><span data-stu-id="64e5d-120">Initialize hello player</span></span>
5. <span data-ttu-id="64e5d-121">Sommige CSS-stijl toevoegen</span><span class="sxs-lookup"><span data-stu-id="64e5d-121">Add some CSS style</span></span>
6. <span data-ttu-id="64e5d-122">Hallo-resultaten weergeven in een browser die u, muis implementeert</span><span class="sxs-lookup"><span data-stu-id="64e5d-122">View hello results in a browser that implements MSE</span></span>

<span data-ttu-id="64e5d-123">Bij het initialiseren Hallo player kan worden voltooid in slechts een handvol regels van JavaScript-code.</span><span class="sxs-lookup"><span data-stu-id="64e5d-123">Initializing hello player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="64e5d-124">Met dash.js echt is het dat eenvoudige tooembed MPEG-DASH-video in uw browser gebaseerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="64e5d-124">Using dash.js, it really is that simple tooembed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-hello-html-page"></a><span data-ttu-id="64e5d-125">Hallo HTML-pagina maken</span><span class="sxs-lookup"><span data-stu-id="64e5d-125">Creating hello HTML Page</span></span>
<span data-ttu-id="64e5d-126">de eerste stap Hallo is toocreate een standaard-HTML-pagina met Hallo **video** element Sla dit bestand als basicPlayer.html als Hallo volgende voorbeeld laat zien:</span><span class="sxs-lookup"><span data-stu-id="64e5d-126">hello first step is toocreate a standard HTML page containing hello **video** element, save this file as basicPlayer.html, as hello following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a><span data-ttu-id="64e5d-127">Toe te voegen Hallo DASH.js Player</span><span class="sxs-lookup"><span data-stu-id="64e5d-127">Adding hello DASH.js Player</span></span>
<span data-ttu-id="64e5d-128">tooadd hello dash.js verwijzing implementatie toohello toepassing, moet u toograb hello dash.all.js bestand van Hallo 1.0 release van dash.js project.</span><span class="sxs-lookup"><span data-stu-id="64e5d-128">tooadd hello dash.js reference implementation toohello application, you’ll need toograb hello dash.all.js file from hello 1.0 release of dash.js project.</span></span> <span data-ttu-id="64e5d-129">Dit moet worden opgeslagen in Hallo JavaScript-map van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="64e5d-129">This should be saved in hello JavaScript folder of your application.</span></span> <span data-ttu-id="64e5d-130">Dit bestand is een gemak-bestand dat alle Hallo nodig dash.js code tot één bestand verzamelt.</span><span class="sxs-lookup"><span data-stu-id="64e5d-130">This file is a convenience file that pulls together all hello necessary dash.js code into a single file.</span></span> <span data-ttu-id="64e5d-131">Hebt u een kijkje rond Hallo dash.js opslagplaats, wordt u Hallo afzonderlijke bestanden zoeken, testen van code en nog veel meer, maar als alle toodo gewenste is gebruik dash.js en Hallo dash.all.js bestand is wat u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="64e5d-131">If you have a look around hello dash.js repository, you will find hello individual files, test code and much more, but if all you want toodo is use dash.js, then hello dash.all.js file is what you need.</span></span>

<span data-ttu-id="64e5d-132">tooadd hello dash.js player tooyour toepassingen, toevoegen een script toohello head tagsectie van basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="64e5d-132">tooadd hello dash.js player tooyour applications, add a script tag toohello head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="64e5d-133">Maak vervolgens een functie tooinitialize Hallo speler wanneer Hallo pagina wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="64e5d-133">Next, create a function tooinitialize hello player when hello page loads.</span></span> <span data-ttu-id="64e5d-134">Hallo script volgen na Hallo regel waarin u dash.all.js laden toevoegen:</span><span class="sxs-lookup"><span data-stu-id="64e5d-134">Add hello following script after hello line in which you load dash.all.js:</span></span>

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="64e5d-135">Deze functie maakt eerst een DashContext.</span><span class="sxs-lookup"><span data-stu-id="64e5d-135">This function first creates a DashContext.</span></span> <span data-ttu-id="64e5d-136">Dit is de gebruikte tooconfigure Hallo-toepassing voor een specifieke runtime-omgeving.</span><span class="sxs-lookup"><span data-stu-id="64e5d-136">This is used tooconfigure hello application for a specific runtime environment.</span></span> <span data-ttu-id="64e5d-137">Vanuit technisch oogpunt definieert het Hallo-klassen die Hallo afhankelijkheid injectie framework gebruiken moeten tijdens het construeren van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="64e5d-137">From a technical point of view, it defines hello classes that hello dependency injection framework should use when constructing hello application.</span></span> <span data-ttu-id="64e5d-138">In de meeste gevallen gebruikt u Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="64e5d-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="64e5d-139">Vervolgens exemplaar te maken van de primaire klasse Hallo van Hallo dash.js framework, Media Player.</span><span class="sxs-lookup"><span data-stu-id="64e5d-139">Next, instantiate hello primary class of hello dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="64e5d-140">Deze klasse bevat Hallo core methoden die nodig zijn, zoals afspelen en onderbreken, beheert Hallo relatie met video Hallo-element en ook beheert Hallo interpretatie van Hallo Media presentatie beschrijving (MPD)-bestand waarin wordt beschreven Hallo video toobe afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="64e5d-140">This class contains hello core methods needed such as play and pause, manages hello relationship with hello video element and also manages hello interpretation of hello Media Presentation Description (MPD) file which describes hello video toobe played.</span></span>

<span data-ttu-id="64e5d-141">Hallo startup() functie Hallo Media Player-klasse wordt aangeroepen tooensure die player Hallo is gereed tooplay video.</span><span class="sxs-lookup"><span data-stu-id="64e5d-141">hello startup() function of hello MediaPlayer class is called tooensure that hello player is ready tooplay video.</span></span> <span data-ttu-id="64e5d-142">Onder andere deze functie zorgt ervoor dat alle benodigde Hallo-klassen (zoals gedefinieerd door de Hallo context) zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="64e5d-142">Amongst other things this function ensures that all hello necessary classes (as defined by hello context) have been loaded.</span></span> <span data-ttu-id="64e5d-143">Zodra Hallo player gereed is, kunt u Hallo video element tooit met Hallo attachView() functie koppelen.</span><span class="sxs-lookup"><span data-stu-id="64e5d-143">Once hello player is ready, you can attach hello video element tooit using hello attachView() function.</span></span> <span data-ttu-id="64e5d-144">Dit kunt Hallo Media Player tooinject Hallo videostream in Hallo-element en ook het afspelen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="64e5d-144">This enables hello MediaPlayer tooinject hello video stream into hello element and also control playback as necessary.</span></span>

<span data-ttu-id="64e5d-145">Hallo-URL van Hallo MPD bestand toohello Media Player doorgeven zodat deze op de hoogte van Hallo video wordt verwacht tooplay.hello setupVideo() functie gemaakte moet toobe uitgevoerd nadat Hallo pagina volledig is geladen.</span><span class="sxs-lookup"><span data-stu-id="64e5d-145">Pass hello URL of hello MPD file toohello MediaPlayer so that it knows about hello video it is expected tooplay.hello setupVideo() function just created will need toobe executed once hello page has fully loaded.</span></span> <span data-ttu-id="64e5d-146">Dit doen met behulp van de gebeurtenisonLoad Hallo van Hallo body-element.</span><span class="sxs-lookup"><span data-stu-id="64e5d-146">Do this by using hello onload event of hello body element.</span></span> <span data-ttu-id="64e5d-147">Wijzig uw <body> element op:</span><span class="sxs-lookup"><span data-stu-id="64e5d-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="64e5d-148">Tot slot stelt Hallo-grootte van video Hallo-element met CSS.</span><span class="sxs-lookup"><span data-stu-id="64e5d-148">Finally, set hello size of hello video element using CSS.</span></span> <span data-ttu-id="64e5d-149">In een omgeving met adaptieve streaming is dit vooral belangrijk omdat Hallo grootte van de video wordt afgespeeld Hallo veranderen kan als afspelen toochanging netwerkomstandigheden aanpast.</span><span class="sxs-lookup"><span data-stu-id="64e5d-149">In an adaptive streaming environment, this is especially important because hello size of hello video being played may change as playback adapts toochanging network conditions.</span></span> <span data-ttu-id="64e5d-150">In deze eenvoudige demo gewoon afdwingen Hallo video element toobe 80% van de beschikbare browservenster Hallo door toe te voegen Hallo CSS toohello head-sectie van de pagina hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="64e5d-150">In this simple demo simply force hello video element toobe 80% of hello available browser window by adding hello following CSS toohello head section of hello page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="64e5d-151">Het afspelen van Video</span><span class="sxs-lookup"><span data-stu-id="64e5d-151">Playing a Video</span></span>
<span data-ttu-id="64e5d-152">tooplay video in uw browser naar Hallo basicPlayback.html bestand en klik op afspelen op Hallo-speler weergegeven.</span><span class="sxs-lookup"><span data-stu-id="64e5d-152">tooplay a video, point your browser at hello basicPlayback.html file and click play on hello video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="64e5d-153">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="64e5d-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="64e5d-154">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="64e5d-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="64e5d-155">Zie ook</span><span class="sxs-lookup"><span data-stu-id="64e5d-155">See Also</span></span>
[<span data-ttu-id="64e5d-156">Videospelertoepassingen ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="64e5d-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="64e5d-157">GitHub-opslagplaats voor dash.js</span><span class="sxs-lookup"><span data-stu-id="64e5d-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

