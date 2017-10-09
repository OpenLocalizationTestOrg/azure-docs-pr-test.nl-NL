---
title: aaaAzure gebeurtenis raster levering en probeer het opnieuw
description: Beschrijft hoe Azure gebeurtenis raster gebeurtenissen biedt en de manier waarop niet-bezorgde berichten worden verwerkt.
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a>Gebeurtenis raster berichtbezorging en probeer het opnieuw 

Dit artikel wordt beschreven hoe Azure gebeurtenis raster omgaat met gebeurtenissen bij levering is niet bevestigd.

Gebeurtenis raster bevat duurzame levering. Elk bericht ten minste eenmaal voor elk abonnement levert. Gebeurtenissen worden geregistreerd toohello webhook van elk abonnement onmiddellijk worden verzonden. Als een webhook niet ontvangstbevestiging is van een gebeurtenis binnen 60 seconden na de eerste levering Hallo proberen, gebeurtenis raster levering van Hallo gebeurtenis opnieuw probeert.

## <a name="message-delivery-status"></a>Bericht bezorgingsstatus

Gebeurtenis raster maakt gebruik van HTTP-antwoord codes tooacknowledge ontvangst van gebeurtenissen. 

### <a name="success-codes"></a>Geslaagd-codes

Hallo volgende HTTP-antwoordcodes erop wijzen dat een gebeurtenis is geleverd met succes tooyour webhook. Gebeurtenis raster beschouwt levering voltooid.

- 200 OK
- 202 geaccepteerd

### <a name="failure-codes"></a>Fout-codes

Hallo volgende HTTP-antwoordcodes erop wijzen dat een gebeurtenis bezorging is mislukt. Gebeurtenis raster opnieuw geprobeerd toosend Hallo gebeurtenis. 

- 400 onjuiste aanvraag
- 401-niet toegestaan
- 404 – Niet gevonden
- Time-out voor 408 aanvragen
- 414 URI te lang
- Interne serverfout 500
- 503 Service niet beschikbaar
- 504 gateway Timeout

Andere antwoordcode of een gebrek aan een antwoord geeft een fout. Gebeurtenis raster pogingen levering. 

## <a name="retry-intervals"></a>Intervallen voor nieuwe pogingen

Een beleid voor opnieuw proberen van exponentieel uitstel gebruikt voor gebeurtenis raster voor de levering van de gebeurtenis. Als uw webhook niet reageert of een foutcode retourneert, opnieuw gebeurtenis raster levering op Hallo schema te volgen:

1. 10 seconden
2. 30 seconden
3. 1 minuut
4. 5 minuten
5. 10 minuten
6. 30 minuten
7. 1 uur

Gebeurtenis raster voegt een kleine willekeurige tooall opnieuw intervallen.

## <a name="retry-duration"></a>Probeer duur

Tijdens de preview hello verloopt Azure gebeurtenis raster alle gebeurtenissen die niet worden bezorgd binnen twee uur. Voordat algemeen beschikbaar is worden deze tijd toegenomen too24 uur. 

## <a name="next-steps"></a>Volgende stappen

* Zie voor een inleiding-tooEvent raster [over gebeurtenis raster](overview.md).
* tooquickly aan de slag met Event raster, Zie [maken en route aangepaste gebeurtenissen met Azure Event raster](custom-event-quickstart.md).
