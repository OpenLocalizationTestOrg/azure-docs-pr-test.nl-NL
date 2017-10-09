---
title: aaaAzure Mobile Engagement Troubleshooting Guide - analyses
description: Het oplossen van problemen Analytics, bewaking, segmentering en Dashboard in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a>Gids voor probleemoplossing voor problemen die Analytics, bewaking, segmentering en Dashboard
Hallo volgen mogelijke problemen optreden bij hoe Azure Mobile Engagement wordt informatie verzameld over uw toepassingen, apparaten en gebruikers.

## <a name="missingdelayed-information"></a>Ontbrekende/uitgestelde informatie
### <a name="issue"></a>Probleem
* Informatie is in die voorkomen in Analytics, segmentering of Dashboard vertraagd.
* Er ontbreekt informatie in de bewaking.
* Er ontbreekt informatie in Analytics, segmentering of Dashboard.
* Roept segmentering beperkt.

### <a name="causes"></a>Oorzaken
* Kunt u Hallo Analytics API, Monitor-API en segmenten API toosee als gegevens u ontbreekt in Hallo UI zichtbaar via Hallo API's.
* Als hello Azure Mobile Engagement SDK is niet correct worden geïntegreerd in uw app niet u de informatie kunnen toosee in Hallo Analytics, segmentering, bewaking of Dashboards.
* Segmenten kunnen niet worden gewijzigd als ze zijn gemaakt, segmenten kunnen alleen worden 'gekloonde' (overgenomen) of 'vernietigd' (verwijderd). Segmenten kunnen alleen 10 criteria bevatten.
* Hallo aanbevolen manier tootest ontbreken gegevens van bewaking is toosetup een testapparaat, verwijderen en/of Hallo-app installeren op Hallo testapparaat.
* Informatie wordt elke 24 uur vernieuwd voor analyses, segmentering of Dashboards.
* Informatie in de nieuwe segmenten mogelijk niet weergegeven tot 24 uur nadat ze zijn gemaakt, zelfs als het Hallo-segment is gebaseerd op eerdere informatie.
* Uw analytics gegevens filteren in Hallo UI vindt u voorbeelden alle van dit type ongeacht Hallo-versie van uw app (bijvoorbeeld) "Loopt vast" gefilterd met de naam ziet van versie 1 en versie 2 van uw app).
* Hallo is periode voor analyses gebaseerd op Hallo datum in de apparaatinstellingen Hallo gebruikers, zodat een gebruiker waarvan telefoon heeft Hallo datum onjuist ingestelde in Hallo verkeerde periode weergegeven kan.
* Er zijn geen gegevens worden geregistreerd wanneer u de knop Hallo serverzijde te 'test' pushes, gegevens alleen worden geregistreerd voor echte pushcampagnes.

## <a name="cant-locate-items-in-ui"></a>Kan items niet vinden in de gebruikersinterface
### <a name="issue"></a>Probleem
* Kan niet op basis van bepaalde ingebouwd in segmenten maken of aangepaste app-gegevens labelen criteria.
* Kan niet vinden op bepaalde ingebouwde of aangepaste app-gegevens labelen criteria in Analytics, bewaking of Dashboards.
* Hallo-gegevens in Analytics, bewaking, segmentering of Dashboards kunnen niet worden geïnterpreteerd.

### <a name="causes"></a>Oorzaken
* Sommige items ingebouwde en app-info-codes zijn alleen beschikbaar als push criteria, maar mogelijk niet tooa segment toegevoegd of zichtbaar vanuit Analytics, bewaking of Dashboard. 
* Voor ingebouwde items en -labels die niet kunnen worden toegevoegd tooa segment app-gegevens, moet u toosetup lijst met doelen criteria in elke campagne tooperform Hallo dezelfde functie uitgevoerd als die gericht is op basis van een segment.
* Zie Hallo contextmenu's in Hallo Analytics, bewaking, segmentering en Dashboards secties van hello Azure Mobile Engagement UI voor meer informatie en hoe tooinformation.

## <a name="crash-troubleshooting"></a>Crash het oplossen van problemen
### <a name="issue"></a>Probleem
* Toepassing is vastgelopen verschijnen in Analytics, bewaking of Dashboard.

### <a name="causes"></a>Oorzaken
* tootroubleshoot toepassing is vastgelopen in Analytics, bewaking of Dashboard weergegeven. Zorg ervoor dat toocheck Hallo release-opmerkingen voor bekende problemen met eerdere versies van Hallo SDK.
* toofurther oplossen toepassing crashes uitvoeren van een gebeurtenis van een testapparaat waarop de toepassing is geïnstalleerd en uw apparaat-ID in de sectie Hallo 'Monitor – gebeurtenissen' Hallo Azure Mobile Engagement-gebruikersinterface worden opgezocht. Vervolgens Hallo-gebeurtenis die wordt veroorzaakt door uw toepassing toocrash uitvoeren en aanvullende gegevens in de sectie 'Monitor – Crash' hello Azure Mobile Engagement UI Hallo opzoeken. 

