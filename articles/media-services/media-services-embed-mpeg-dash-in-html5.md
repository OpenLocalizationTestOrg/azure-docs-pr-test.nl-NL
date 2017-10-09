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
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>Een MPEG-DASH adaptieve Streaming Video insluiten in een toepassing HTML5 met DASH.js
## <a name="overview"></a>Overzicht
MPEG-DASH is een ISO-norm voor adaptief streamen van video-inhoud, die biedt aanzienlijke voordelen voor gebruikers die toodeliver hoogwaardige, adaptief videostreaming uitvoer wilt Hallo. Met MPEG-DASH wordt Hallo videostream automatisch tooa lagere definitie verwijderen als Hallo netwerk wordt overbelast. Dit vermindert de kans op Hallo van Hallo viewer 'onderbroken' video bekijken terwijl Hallo player gedownload Hallo naast enkele seconden tooplay (aka buffer). Zoals opstoppingen in het netwerk wordt beperkt, wordt Hallo-speler op zijn beurt tooa hogere quality-stroom geretourneerd. Deze mogelijkheid tooadapt Hallo bandbreedte vereist resulteert ook in een snellere begintijd voor video. Betekent dat de eerste paar seconden Hallo kunnen worden afgespeeld in een lagere quality-segment van fast te downloaden en doeltreffendere tooa hogere kwaliteit zodra voldoende inhoud zijn gebufferd.

Dash.js is een open-source MPEG-DASH-speler geschreven in JavaScript. Het doel is tooprovide een robuuste, platformoverschrijdende-speler vrijelijk in toepassingen waarvoor afspelen van video's kan worden gebruikt. Het biedt MPEG-DASH afspelen in browsers die ondersteuning biedt voor Hallo W3C Media bron extensies (muis) vandaag zijn Chrome, Microsoft Edge en IE11 (andere browsers hebt aangegeven dat hun opzet toosupport muis). Js Zie voor meer informatie over DASH.js hello GitHub dash.js-opslagplaats.

## <a name="creating-a-browser-based-streaming-video-player"></a>Maken van een browser gebaseerde streaming video-speler
een eenvoudige pagina die wordt weergegeven een video-speler met Hallo verwacht toocreate besturingselementen dergelijke een play, onderbreken, terugspoelen enz., moet u:

1. Maken van een HTML-pagina
2. Hallo video-tag toevoegen
3. Hallo dash.js player toevoegen
4. Hallo player initialiseren
5. Sommige CSS-stijl toevoegen
6. Hallo-resultaten weergeven in een browser die u, muis implementeert

Bij het initialiseren Hallo player kan worden voltooid in slechts een handvol regels van JavaScript-code. Met dash.js echt is het dat eenvoudige tooembed MPEG-DASH-video in uw browser gebaseerde toepassingen.

## <a name="creating-hello-html-page"></a>Hallo HTML-pagina maken
de eerste stap Hallo is toocreate een standaard-HTML-pagina met Hallo **video** element Sla dit bestand als basicPlayer.html als Hallo volgende voorbeeld laat zien:

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>Toe te voegen Hallo DASH.js Player
tooadd hello dash.js verwijzing implementatie toohello toepassing, moet u toograb hello dash.all.js bestand van Hallo 1.0 release van dash.js project. Dit moet worden opgeslagen in Hallo JavaScript-map van uw toepassing. Dit bestand is een gemak-bestand dat alle Hallo nodig dash.js code tot één bestand verzamelt. Hebt u een kijkje rond Hallo dash.js opslagplaats, wordt u Hallo afzonderlijke bestanden zoeken, testen van code en nog veel meer, maar als alle toodo gewenste is gebruik dash.js en Hallo dash.all.js bestand is wat u nodig hebt.

tooadd hello dash.js player tooyour toepassingen, toevoegen een script toohello head tagsectie van basicPlayer.html:

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


Maak vervolgens een functie tooinitialize Hallo speler wanneer Hallo pagina wordt geladen. Hallo script volgen na Hallo regel waarin u dash.all.js laden toevoegen:

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

Deze functie maakt eerst een DashContext. Dit is de gebruikte tooconfigure Hallo-toepassing voor een specifieke runtime-omgeving. Vanuit technisch oogpunt definieert het Hallo-klassen die Hallo afhankelijkheid injectie framework gebruiken moeten tijdens het construeren van de toepassing hello. In de meeste gevallen gebruikt u Dash.di.DashContext.

Vervolgens exemplaar te maken van de primaire klasse Hallo van Hallo dash.js framework, Media Player. Deze klasse bevat Hallo core methoden die nodig zijn, zoals afspelen en onderbreken, beheert Hallo relatie met video Hallo-element en ook beheert Hallo interpretatie van Hallo Media presentatie beschrijving (MPD)-bestand waarin wordt beschreven Hallo video toobe afgespeeld.

Hallo startup() functie Hallo Media Player-klasse wordt aangeroepen tooensure die player Hallo is gereed tooplay video. Onder andere deze functie zorgt ervoor dat alle benodigde Hallo-klassen (zoals gedefinieerd door de Hallo context) zijn geladen. Zodra Hallo player gereed is, kunt u Hallo video element tooit met Hallo attachView() functie koppelen. Dit kunt Hallo Media Player tooinject Hallo videostream in Hallo-element en ook het afspelen indien nodig.

Hallo-URL van Hallo MPD bestand toohello Media Player doorgeven zodat deze op de hoogte van Hallo video wordt verwacht tooplay.hello setupVideo() functie gemaakte moet toobe uitgevoerd nadat Hallo pagina volledig is geladen. Dit doen met behulp van de gebeurtenisonLoad Hallo van Hallo body-element. Wijzig uw <body> element op:

    <body onload="setupVideo()">

Tot slot stelt Hallo-grootte van video Hallo-element met CSS. In een omgeving met adaptieve streaming is dit vooral belangrijk omdat Hallo grootte van de video wordt afgespeeld Hallo veranderen kan als afspelen toochanging netwerkomstandigheden aanpast. In deze eenvoudige demo gewoon afdwingen Hallo video element toobe 80% van de beschikbare browservenster Hallo door toe te voegen Hallo CSS toohello head-sectie van de pagina hello te volgen:

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>Het afspelen van Video
tooplay video in uw browser naar Hallo basicPlayback.html bestand en klik op afspelen op Hallo-speler weergegeven.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zie ook
[Videospelertoepassingen ontwikkelen](media-services-develop-video-players.md)

[GitHub-opslagplaats voor dash.js](https://github.com/Dash-Industry-Forum/dash.js) 

