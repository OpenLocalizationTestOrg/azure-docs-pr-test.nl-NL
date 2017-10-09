---
title: aaaOptimize Azure content delivery voor uw scenario
description: Hoe toooptimize levering van uw inhoud voor specifieke scenario's
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a>Azure content delivery voor uw scenario optimaliseren

Wanneer u inhoud tooa grote wereldwijde doelgroep leveren, is dit kritieke tooensure Hallo geoptimaliseerd levering van uw inhoud. Hello Azure inhoud Delivery Network kunt optimaliseren Hallo levering ervaring op basis van Hallo type inhoud dat u hebt. Inhoud is een website, een live stream, een video of een groot bestand downloaden. Als u een content delivery network (CDN)-eindpunt maakt, geeft u een scenario in Hallo **geoptimaliseerd voor** optie. Uw keuze bepaalt welke optimalisatie toegepaste toohello inhoud vanaf de CDN-eindpunt Hallo geleverd.

Optimalisatie die zijn ontworpen toouse best practice gedrag tooimprove contentlevering prestaties en betere oorsprong-offload. Uw keuzes scenario invloed hebben op prestaties door het wijzigen van configuraties voor gedeeltelijke caching, object verdeling in segmenten en Hallo oorsprong mislukt-beleid voor opnieuw proberen. 

Dit artikel bevat een overzicht van diverse functies voor optimalisatie en wanneer u deze moet gebruiken. Zie voor meer informatie over de functies en beperkingen Hallo respectieve artikelen op elk type afzonderlijke optimalisatie.

> [!NOTE]
> Uw **geoptimaliseerd voor** kunnen variëren op basis van het Hallo-provider die u selecteert. CDN-providers toepassen uitbreiding op verschillende manieren, afhankelijk van Hallo scenario. 

## <a name="provider-options"></a>Opties van de provider

Hello Azure Content Delivery Network van Akamai ondersteunt:

* Algemene webtoepassingen levering 

* Algemene mediastreaming

* Video-on-demand mediastreaming

* Grote bestanden downloaden

* Dynamische site-versnelling 

Hello Azure Content Delivery Network van Verizon ondersteunt alleen algemene webtoepassingen levering. Het kan worden gebruikt voor de video op aanvraag en grote bestanden te downloaden. U hebt geen tooselect een type optimalisatie.

Het is raadzaam variaties tussen verschillende providers tooselect Hallo optimale provider voor de levering van de prestaties te testen.

## <a name="select-and-configure-optimization-types"></a>Selecteer en optimalisatie typen configureren

een nieuw eindpunt toocreate een optimalisatie-type dat het meest geschikt Hallo scenario en type inhoud dat u wilt dat eindpunt toodeliver Hallo selecteren. **Algemene webtoepassingen levering** Hallo is standaard geselecteerd. U kunt Hallo optimalisatieoptie voor een bestaande Akamai-eindpunt op elk gewenst moment bijwerken. Deze wijziging onderbroken geen levering van CDN Hallo. 

1. Selecteer een eindpunt binnen een standaard Akamai-profiel.

    ![Selectie van het eindpunt ](./media/cdn-optimization-overview/01_Akamai.png)

2. Onder **instellingen**, selecteer **optimalisatie**. Selecteer vervolgens een type in Hallo **geoptimaliseerd voor** vervolgkeuzelijst.

    ![Optimalisatie en type selectie](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a>Optimalisatie voor specifieke scenario 's

U kunt Hallo CDN-eindpunt voor een van de volgende scenario's Hallo optimaliseren. 

### <a name="general-web-delivery"></a>Algemene webtoepassingen levering

Algemene webtoepassingen levering is het meest voorkomende optimalisatieoptie Hallo. Het ontworpen voor algemene web content optimalisatie, zoals webpagina's en webtoepassingen. Deze optimalisatie kan ook worden gebruikt voor het bestand en video downloadt.

Een typische website bevat statische en dynamische inhoud. Statische inhoud bevat afbeeldingen, JavaScript-bibliotheken en StyleSheets die kunnen worden opgeslagen in de cache en toodifferent gebruikers geleverd. Dynamische inhoud is aangepast voor een afzonderlijke gebruiker, zoals nieuwsitems die zijn afgestemd tooa gebruikersprofiel. Dynamische inhoud is niet in cache opgeslagen omdat het unieke tooeach gebruiker, zoals een winkelwagen inhoud winkelen. Algemene webtoepassingen levering kunt optimaliseren van uw gehele website. 

> [!NOTE]
> Als u hello Azure Content Delivery Network van Akamai gebruikt, kunt u toouse deze optimalisatie als de gemiddelde bestandsgrootte kleiner dan 10 MB is. Als de gemiddelde grootte groter dan 10 MB is, selecteert u **grote bestanden downloaden** van Hallo **geoptimaliseerd voor** vervolgkeuzelijst.

### <a name="general-media-streaming"></a>Algemene mediastreaming

Als u toouse Hallo eindpunt voor live streamen en video-on-demand streaming nodig hebt, raden wij algemene mediastreaming optimalisatie.

Het is tijd gevoelige, streaming media, omdat pakketten die laat op Hallo-client binnenkomen leiden een ervaring verslechterde weer te geven tot kunnen, zoals frequente buffer van video-inhoud. Optimalisatie van mediastreaming minder Hallo latentie van media leveren van inhoud en biedt een smooth streaming ervaring voor gebruikers. 

Dit scenario is gebruikelijk voor Azure media service-klanten. Als u Azure mediaservices gebruikt, krijgt u een streaming-eindpunt dat kan worden gebruikt voor live en on-demand streaming. Met dit scenario nodig niet klanten tooswitch tooanother eindpunt wanneer ze van live tooon-demand streaming wijzigt. Algemene media streaming optimalisatie ondersteunt dit type scenario.

Hello Azure inhoud Delivery Network van Verizon Hallo algemene webtoepassingen levering optimalisatie type toodeliver streaming media-inhoud gebruikt.

toolearn meer informatie over mediastreaming optimalisatie, Zie [mediastreaming optimalisatie](cdn-media-streaming-optimization.md).

### <a name="video-on-demand-media-streaming"></a>Video-on-demand mediastreaming

Streaming media-optimalisatie video-on-demand verbetert video-on-demand streaming inhoud. Als u een eindpunt voor streaming video-on-demand gebruikt, kunt u toouse deze optie.

Hello Azure inhoud Delivery Network van Verizon Hallo algemene webtoepassingen levering optimalisatie type toodeliver streaming media-inhoud gebruikt.

toolearn meer informatie over mediastreaming optimalisatie, Zie [mediastreaming optimalisatie](cdn-media-streaming-optimization.md).

> [!NOTE]
> Als Hallo endpoint voornamelijk video-on-demand inhoud fungeert, gebruikt u dit type optimalisatie. het belangrijkste verschil tussen deze optimalisatie en Hallo algemene media streaming optimalisatie Hallo is Hallo verbindingstime-out probeer het opnieuw. Hallo-time-outwaarde is veel kortere toowork met live streaming-scenario's.

### <a name="large-file-download"></a>Grote bestanden downloaden

Als u hello Azure Content Delivery Network van Akamai gebruikt, moet u een groot bestand downloaden toodeliver bestanden groter dan 1,8 GB gebruiken. Hello Azure Content Delivery Network van Verizon beschikt niet over een beperking in het bestand downloaden van de grootte in de algemene webtoepassingen leveringsoptimalisatie.

Als u hello Azure inhoud Delivery Network van Akamai gebruikt, worden downloads van grote bestanden zijn geoptimaliseerd voor inhoud groter is dan 10 MB. Als de gemiddelde grootte kleiner dan 10 MB is, kunt u toouse algemene webtoepassingen levering. Als de gemiddelde bestandsgrootte consistent groter dan 10 MB zijn, is dit mogelijk efficiënter toocreate een afzonderlijke eindpunt voor grote bestanden. Firmware of software-updates zijn bijvoorbeeld meestal grote bestanden.

Hello Azure inhoud Delivery Network van Verizon Hallo algemene webtoepassingen levering optimalisatie type toodeliver streaming media-inhoud gebruikt.

toolearn meer informatie over de optimalisatie van grote bestanden, Zie [groot bestand optimalisatie](cdn-large-file-optimization.md).

### <a name="dynamic-site-acceleration"></a>Dynamische site-versnelling

 Dynamische site-versnelling is beschikbaar via zowel Akamai en Verizon Content Delivery Network-profielen. Deze optimalisatie omvat een toouse extra kosten. Zie voor meer informatie Hallo pagina met prijzen.

Dynamische site-versnelling bevat verschillende technieken die Hallo latentie en prestaties van dynamische inhoud profiteren. Technieken zijn onder andere route- en optimalisatie en optimalisatie van TCP. 

U kunt deze optimalisatie tooaccelerate een web-app met talrijke reacties die voor caching geschikte zijn niet gebruiken. Voorbeelden zijn zoekresultaten, afhandeling transacties of realtime-gegevens. U kunt toouse belangrijkste CDN cachebewerkingen mogelijkheden voor statische gegevens blijven. 



