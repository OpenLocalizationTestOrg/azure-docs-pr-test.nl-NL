---
title: Een MPEG-DASH adaptieve Streaming Video insluiten in een toepassing HTML5 met DASH.js | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe u een MPEG-DASH adaptieve Streaming Video in een toepassing HTML5 met DASH.js insluiten.
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
ms.openlocfilehash: 27ce6325773ba1f9fd9cd9ab9e07ea9f5e2488ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="1d5be-103">Een MPEG-DASH adaptieve Streaming Video insluiten in een toepassing HTML5 met DASH.js</span><span class="sxs-lookup"><span data-stu-id="1d5be-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="1d5be-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1d5be-104">Overview</span></span>
<span data-ttu-id="1d5be-105">MPEG-DASH is een ISO-norm voor adaptief streamen van video-inhoud, die biedt aanzienlijke voordelen voor gebruikers die u wilt leveren van hoge kwaliteit, adaptief videostreaming-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="1d5be-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for those who wish to deliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="1d5be-106">Met MPEG-DASH wordt de video-stream automatisch verwijderen voor de definitie van een lagere wanneer het netwerk overbelast raakt.</span><span class="sxs-lookup"><span data-stu-id="1d5be-106">With MPEG-DASH, the video stream will automatically drop to a lower definition when the network becomes congested.</span></span> <span data-ttu-id="1d5be-107">Dit vermindert de kans van de viewer 'onderbroken' video zien terwijl de speler wordt gedownload de volgende enkele seconden om af te spelen (aka buffer).</span><span class="sxs-lookup"><span data-stu-id="1d5be-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span></span> <span data-ttu-id="1d5be-108">Zoals opstoppingen in het netwerk wordt beperkt, wordt op zijn beurt de video speler naar een hogere quality-stroom geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="1d5be-108">As network congestion reduces, the video player will in turn return to a higher quality stream.</span></span> <span data-ttu-id="1d5be-109">Deze mogelijkheid aan te passen aan de vereiste bandbreedte resulteert ook in een snellere begintijd voor video.</span><span class="sxs-lookup"><span data-stu-id="1d5be-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="1d5be-110">Dat betekent dat de eerste paar seconden kunnen worden afgespeeld in een lagere quality-segment van fast te downloaden en vervolgens de buffer van stap tot een hogere eenmaal voldoende kwaliteit-inhoud is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1d5be-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="1d5be-111">Dash.js is een open-source MPEG-DASH-speler geschreven in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1d5be-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="1d5be-112">Het doel is te bieden een robuuste, platformoverschrijdende-speler vrijelijk in toepassingen waarvoor afspelen van video's kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1d5be-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="1d5be-113">Het biedt MPEG-DASH afspelen in browsers die ondersteuning biedt voor W3C Media bron extensies (muis) vandaag Chrome, Microsoft Edge en IE11 (andere browsers hebt aangegeven dat hun bedoeld ter ondersteuning van de muis).</span><span class="sxs-lookup"><span data-stu-id="1d5be-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent to support MSE).</span></span> <span data-ttu-id="1d5be-114">Js Zie voor meer informatie over DASH.js de GitHub-opslagplaats dash.js.</span><span class="sxs-lookup"><span data-stu-id="1d5be-114">For more information about DASH.js, js see the GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="1d5be-115">Maken van een browser gebaseerde streaming video-speler</span><span class="sxs-lookup"><span data-stu-id="1d5be-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="1d5be-116">Besturingselementen voor het maken van een eenvoudige pagina die wordt weergegeven een video-speler met de verwachte dergelijke een play, onderbreken, terugspoelen enz., moet u:</span><span class="sxs-lookup"><span data-stu-id="1d5be-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="1d5be-117">Maken van een HTML-pagina</span><span class="sxs-lookup"><span data-stu-id="1d5be-117">Create an HTML page</span></span>
2. <span data-ttu-id="1d5be-118">De video-tag toevoegen</span><span class="sxs-lookup"><span data-stu-id="1d5be-118">Add the video tag</span></span>
3. <span data-ttu-id="1d5be-119">Windows media player dash.js toevoegen</span><span class="sxs-lookup"><span data-stu-id="1d5be-119">Add the dash.js player</span></span>
4. <span data-ttu-id="1d5be-120">Windows media player initialiseren</span><span class="sxs-lookup"><span data-stu-id="1d5be-120">Initialize the player</span></span>
5. <span data-ttu-id="1d5be-121">Sommige CSS-stijl toevoegen</span><span class="sxs-lookup"><span data-stu-id="1d5be-121">Add some CSS style</span></span>
6. <span data-ttu-id="1d5be-122">Bekijk de resultaten in een browser die u, muis implementeert</span><span class="sxs-lookup"><span data-stu-id="1d5be-122">View the results in a browser that implements MSE</span></span>

<span data-ttu-id="1d5be-123">Tijdens de initialisatie van de speler kan worden voltooid in slechts een handvol regels van JavaScript-code.</span><span class="sxs-lookup"><span data-stu-id="1d5be-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="1d5be-124">Met dash.js echt is het eenvoudig voor het insluiten van video MPEG-DASH in uw browser gebaseerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1d5be-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-the-html-page"></a><span data-ttu-id="1d5be-125">Maken van de HTML-pagina</span><span class="sxs-lookup"><span data-stu-id="1d5be-125">Creating the HTML Page</span></span>
<span data-ttu-id="1d5be-126">De eerste stap is het maken van een standaard HTML-pagina met de **video** element Sla dit bestand als basicPlayer.html, zoals het volgende voorbeeld laat zien:</span><span class="sxs-lookup"><span data-stu-id="1d5be-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-the-dashjs-player"></a><span data-ttu-id="1d5be-127">Windows Media Player DASH.js toevoegen</span><span class="sxs-lookup"><span data-stu-id="1d5be-127">Adding the DASH.js Player</span></span>
<span data-ttu-id="1d5be-128">Voor de implementatie van dash.js verwijzing toevoegen aan de toepassing, moet u het bestand dash.all.js van versie 1.0 van dash.js project halen.</span><span class="sxs-lookup"><span data-stu-id="1d5be-128">To add the dash.js reference implementation to the application, you’ll need to grab the dash.all.js file from the 1.0 release of dash.js project.</span></span> <span data-ttu-id="1d5be-129">Dit moet worden opgeslagen in de JavaScript-map van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="1d5be-129">This should be saved in the JavaScript folder of your application.</span></span> <span data-ttu-id="1d5be-130">Dit bestand is een gemak-bestand dat alle benodigde dash.js code tot één bestand verzamelt.</span><span class="sxs-lookup"><span data-stu-id="1d5be-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span></span> <span data-ttu-id="1d5be-131">Als u een kijkje rond de opslagplaats dash.js hebt, u de afzonderlijke bestanden niet vinden, testen code en nog veel meer, maar als u wilt doen gebruik dash.js, wordt het bestand dash.all.js is wat u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="1d5be-131">If you have a look around the dash.js repository, you will find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span></span>

<span data-ttu-id="1d5be-132">Toevoegen als u wilt de speler dash.js toevoegen aan uw toepassingen, scriptcode naar de sectie head van basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="1d5be-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="1d5be-133">Maak vervolgens een functie voor het initialiseren van de speler als de pagina wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="1d5be-133">Next, create a function to initialize the player when the page loads.</span></span> <span data-ttu-id="1d5be-134">Het volgende script toevoegen na de regel waar u dash.all.js laden:</span><span class="sxs-lookup"><span data-stu-id="1d5be-134">Add the following script after the line in which you load dash.all.js:</span></span>

    <script>
    // setup the video element and attach it to the Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="1d5be-135">Deze functie maakt eerst een DashContext.</span><span class="sxs-lookup"><span data-stu-id="1d5be-135">This function first creates a DashContext.</span></span> <span data-ttu-id="1d5be-136">Dit wordt gebruikt voor het configureren van de toepassing voor een specifieke runtime-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1d5be-136">This is used to configure the application for a specific runtime environment.</span></span> <span data-ttu-id="1d5be-137">Vanuit technisch oogpunt Hiermee definieert u de klassen die voor de afhankelijkheid injectie framework wordt gebruikt bij het maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1d5be-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span></span> <span data-ttu-id="1d5be-138">In de meeste gevallen gebruikt u Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="1d5be-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="1d5be-139">Vervolgens exemplaar maken van de primaire klasse van het framework dash.js, Media Player.</span><span class="sxs-lookup"><span data-stu-id="1d5be-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="1d5be-140">Deze klasse bevat de belangrijkste methoden die nodig zijn, zoals afspelen en onderbreken, beheert de relatie met de video-element en beheert ook de interpretatie van het bestand Media presentatie beschrijving (MPD) waarin de video wordt afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="1d5be-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file which describes the video to be played.</span></span>

<span data-ttu-id="1d5be-141">De functie startup() van de Media Player-klasse wordt aangeroepen om ervoor te zorgen dat Windows media player gereed is voor het afspelen van video.</span><span class="sxs-lookup"><span data-stu-id="1d5be-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span></span> <span data-ttu-id="1d5be-142">Onder andere deze functie zorgt ervoor dat alle benodigde klassen (zoals gedefinieerd door de context) zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="1d5be-142">Amongst other things this function ensures that all the necessary classes (as defined by the context) have been loaded.</span></span> <span data-ttu-id="1d5be-143">Zodra de speler gereed is, kunt u de video element aan met behulp van de functie attachView() koppelen.</span><span class="sxs-lookup"><span data-stu-id="1d5be-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span></span> <span data-ttu-id="1d5be-144">Hierdoor kunnen de Media Player naar de videostream invoeren in het element en ook het afspelen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="1d5be-144">This enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span></span>

<span data-ttu-id="1d5be-145">De URL van het bestand MPD doorgeven aan de Media Player, zodat deze op de hoogte van de video dat naar verwachting af te spelen. De zojuist gemaakte setupVideo()-functie moet worden uitgevoerd nadat de pagina volledig is geladen.</span><span class="sxs-lookup"><span data-stu-id="1d5be-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.The setupVideo() function just created will need to be executed once the page has fully loaded.</span></span> <span data-ttu-id="1d5be-146">Dit doen met behulp van de gebeurtenis onload van het body-element.</span><span class="sxs-lookup"><span data-stu-id="1d5be-146">Do this by using the onload event of the body element.</span></span> <span data-ttu-id="1d5be-147">Wijzig uw <body> element op:</span><span class="sxs-lookup"><span data-stu-id="1d5be-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="1d5be-148">Tot slot stelt u de grootte van de video-element met CSS.</span><span class="sxs-lookup"><span data-stu-id="1d5be-148">Finally, set the size of the video element using CSS.</span></span> <span data-ttu-id="1d5be-149">In een omgeving met adaptieve streaming is dit vooral belangrijk omdat de grootte van de video wordt afgespeeld veranderen kan als afspelen aanpast aan veranderende netwerkomstandigheden.</span><span class="sxs-lookup"><span data-stu-id="1d5be-149">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span></span> <span data-ttu-id="1d5be-150">In deze eenvoudige demo gewoon de video-element moet 80% van de beschikbare browservenster door de volgende CSS toe te voegen aan de head-sectie van de pagina afdwingen:</span><span class="sxs-lookup"><span data-stu-id="1d5be-150">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="1d5be-151">Het afspelen van Video</span><span class="sxs-lookup"><span data-stu-id="1d5be-151">Playing a Video</span></span>
<span data-ttu-id="1d5be-152">Als u wilt afspelen van video, wijst u in uw browser naar het bestand basicPlayback.html en op afspelen op de video player weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1d5be-152">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1d5be-153">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="1d5be-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1d5be-154">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="1d5be-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1d5be-155">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1d5be-155">See Also</span></span>
[<span data-ttu-id="1d5be-156">Videospelertoepassingen ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="1d5be-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="1d5be-157">GitHub-opslagplaats voor dash.js</span><span class="sxs-lookup"><span data-stu-id="1d5be-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

