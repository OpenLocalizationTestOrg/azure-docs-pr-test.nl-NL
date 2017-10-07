---
title: aaaAnalyze gebruiker navigatiepatronen met een gebruiker in Azure Application Insights loopt | Microsoft docs
description: Analyseren hoe gebruikers navigeren tussen Hallo's en functies van uw web-app.
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a>Gebruiker navigatiepatronen met een gebruiker in Application Insights loopt analyseren

![Hulpprogramma voor Application Insights gebruiker stroomt](./media/app-insights-usage-flows/flows.png)

Hallo gebruiker loopt hulpprogramma visualiseren hoe gebruikers navigeren tussen Hallo's en functies van uw site. Het is ideaal voor het beantwoorden van vragen als:
* Hoe gebruikers navigeren vanuit een pagina op uw site?
* Wat gebruikers klikken op een pagina op uw site?
* Hallo waar zijn geplaatst dat gebruikers verloop in de meeste van uw site?
* Zijn er plaatsen waar gebruikers herhaaldelijk dezelfde actie steeds Hallo?

Hallo gebruiker loopt hulpprogramma wordt gestart van een weergave van de eerste pagina of de gebeurtenis die u opgeeft. Deze pagina of aangepaste gebeurtenis, loopt van de gebruiker opgegeven Hallo toont van paginaweergaven en aangepaste gebeurtenissen die gebruikers verzonden onmiddellijk daarna twee tijdens een sessie daarna, enzovoort stappen. Regels verschillende dikte van het aantal keren dat elk pad werd gevolgd door gebruikers worden weergegeven. Speciale knooppunten 'Sessie beëindigd' weergegeven hoeveel gebruikers geen paginaweergaven of aangepaste gebeurtenissen na verzonden hello voorafgaand aan knooppunt markeren waar gebruikers waarschijnlijk was uw site.



> [!NOTE]
> Uw Application Insights-resource moet paginaweergaven of aangepaste gebeurtenissen toouse Hallo gebruiker loopt hulpprogramma bevatten. [Meer informatie over hoe tooset van uw app toocollect pagina automatisch bekijkt Hello Application Insights JavaScript SDK](app-insights-javascript.md).
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a>Gestart door een weergave van de eerste pagina of aangepaste gebeurtenis te kiezen

![Kies een eerste gebeurtenis voor gebruiker stroomt](./media/app-insights-usage-flows/flows-initial-event.png)

tooget gestart beantwoorden van vragen met Hallo gebruiker loopt hulpprogramma, kies een weergave van de eerste pagina of aangepaste gebeurtenis tooserve als startpunt voor Hallo visualisatie Hallo:
1. Klik op de koppeling Hallo in Hallo ' wat gebruikers doen na...? ' titel of klik op de knop bewerken Hallo. 
2. Selecteer een paginaweergave of aangepaste gebeurtenis uit Hallo 'Eerste gebeurtenis' vervolgkeuzelijst.
3. Klik op 'Grafiek maken'.

Hallo 'Stap 1' kolom Hallo visualisatie wordt weergegeven wat gebruikers gedaan meest direct na de initiële gebeurtenis hello, geordend van boven naar beneden van de meeste tooleast frequent. Hallo 'Stap 2' en het weergeven van de volgende kolommen wat gebruikers voldoet daarna maken van een afbeelding van alle gebruikers van Hallo manieren bent gegaan door de site.

Standaard voorbeelden Hallo gebruiker loopt hulpprogramma willekeurig alleen Hallo afgelopen 24 uur van paginaweergaven en aangepaste gebeurtenis van uw site. U kunt verhogen Hallo tijdsbereik en Hallo balans van prestaties en nauwkeurigheid voor steekproeven in het menu van Hallo bewerken wijzigen.

Als het aantal paginaweergaven Hallo en aangepaste gebeurtenissen niet relevant tooyou, klikt u op 'X' Hallo op Hallo knooppunten die u wilt toohide. Wanneer u de gewenste toohide Hallo-knooppunten hebt geselecteerd, klikt u Hallo 'Grafiek maken' hieronder Hallo visualisatie. toosee alle Hallo knooppunten hebt verborgen, klik op de knop bewerken Hallo en bekijkt hello 'Uitgesloten gebeurtenissen' sectie.

Als paginaweergaven of aangepaste gebeurtenissen die ontbreken verwacht u toosee op Hallo visualisatie:
* Controleer 'Uitgesloten gebeurtenissen' Hallo-sectie in het menu van Hallo bewerken.
* Hallo 'Detailniveau' besturingselement in Hallo bewerken menu tooinclude minder frequent gebeurtenissen in Hallo-visualisatie gebruiken.
* Probeer toenemende Hallo tijdsbereik Hallo visualisatie in het menu van Hallo bewerken als Hallo paginaweergave of aangepaste gebeurtenis die u verwacht zelden wordt verzonden door gebruikers.
* Zorg ervoor dat Hallo paginaweergave of aangepaste gebeurtenis die u verwacht toobe verzameld door Hallo Application Insights-SDK in de broncode Hallo van uw site is ingesteld. [Meer informatie over het verzamelen van aangepaste gebeurtenissen.](app-insights-api-custom-events-metrics.md)

Als u wilt meer stappen voor het Hallo-visualisatie, gebruik Hallo 'Het aantal stappen' schuifregelaar in Hallo toosee menu Bewerken.

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a>Nadat u hebt een pagina of het onderdeel bezocht, waarbij gebruikers gaan en wat ze op?

![Gebruiker loopt toounderstand gebruiken waarop gebruikers klikken op](./media/app-insights-usage-flows/flows-one-step.png)

Als uw eerste gebeurtenis een paginaweergave is, is Hallo eerste kolom ('stap 1) van Hallo visualisatie een snelle manier toounderstand wat gebruikers is onmiddellijk na het Hallo-pagina te bezoeken. Probeer uw site openen in een venster volgende toohello visualisatie loopt van de gebruiker. Vergelijk de verwachtingen van hoe gebruikers met Hallo Paginalijst toohello van gebeurtenissen in de kolom voor Hallo 'Stap 1 interacteren'. Vaak mag een UI-element op Hallo-pagina met een gering tooyour team tussen de meest gebruikte op de pagina Hallo Hallo. Het kan een goed startpunt voor ontwerp verbeteringen tooyour site zijn.

Als uw eerste gebeurtenis een aangepaste gebeurtenis is, toont de eerste kolom Hallo gebruikers heeft na het uitvoeren van deze actie. Net als bij paginaweergaven Overweeg als Hallo waargenomen gedrag van uw gebruikers komt overeen met de doelstellingen en de verwachtingen van uw team. Als de geselecteerde eerste gebeurtenis 'Toegevoegde Item tooShopping winkelwagen', bijvoorbeeld, er toosee als 'Ga tooCheckout' en 'Voltooid aankoop' worden weergegeven in het kort nadien Hallo visualisatie. Als gebruikersgedrag veel van uw verwachtingen verschilt, gebruikt u Hallo visualisatie toounderstand hoe gebruikers ophalen '' door de huidige ontwerp van uw site afgevangen worden.

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a>Hallo waar zijn geplaatst dat gebruikers verloop in de meeste van uw site?

Bekijk voor 'Sessie beëindigd' knooppunten die hoge-up worden weergegeven in een kolom in Hallo visualisatie, met name vroeg in een stroom. Dit betekent dat veel gebruikers waarschijnlijk churned van uw site nadat de volgende Hallo voorgaande pad van pagina's en interacties van de gebruikersinterface. Soms verloop - na het voltooien van bijvoorbeeld een aankoop op een e-commerce-site - wordt verwacht maar verloop is meestal een teken van problemen met het ontwerp, slechte prestaties of andere problemen met de site die kan worden verbeterd.

Houd er rekening mee dat 'sessie beëindigd' knooppunten alleen worden gebaseerd op telemetrie die is verzameld door deze Application Insights-resource. Als Application Insights heeft ontvangen telemetrie voor bepaalde gebruikersinteracties, kunnen gebruikers nog steeds hebt uitgevoerd in uw site op deze manieren nadat Hallo gebruiker loopt hulpprogramma zegt Hallo sessie beëindigd.

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a>Zijn er plaatsen waar gebruikers herhaaldelijk dezelfde actie steeds Hallo?

Zoek naar een paginaweergave of aangepaste gebeurtenis die door veel gebruikers via de volgende stappen in Hallo visualisatie wordt herhaald. Dit betekent meestal dat gebruikers herhalende taken op uw site uitvoeren wilt. Als u herhaling vinden, kunt u zien over het ontwerp van uw site Hallo wijzigen of toevoegen van nieuwe functionaliteit tooreduce herhaling. Bijvoorbeeld, toe te voegen bulksgewijs bewerkingsfunctionaliteit als u gebruikers, herhalende taken uitvoeren voor elke rij van een table-element vinden.

## <a name="common-questions"></a>Veelgestelde vragen

### <a name="why-do-steps-appear-disconnected"></a>Waarom worden stappen verbroken weergegeven?

![Gebruiker-stromen met niet-verbonden stappen](./media/app-insights-usage-flows/flows-disconnected.png)

Als u stappen (kolommen) in een visualisatie loopt van de gebruiker verbinding wordt verbroken, betekent dit geen enkel Hallo paden die door gebruikers tussen Hallo stappen is zodanig toobe weergegeven. tooshow minder frequente gebeurtenissen op Hallo visualisatie aanpassen Hallo 'Detailniveau' schuifregelaar in de menu Bewerken Hallo zodat Hallo stappen worden verbonden, weergegeven.

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a>Hallo eerste gebeurtenis vertegenwoordigen Hallo eerste tijd Hallo gebeurtenis zich in een sessie of elk gewenst moment wordt deze weergegeven in een sessie?

de eerste gebeurtenis Hallo op Hallo visualisatie vertegenwoordigt alleen Hallo eerst die een gebruiker die in de weergave of aangepaste gebeurtenis tijdens een sessie verzonden. Als gebruikers de eerste gebeurtenis Hallo meerdere keren in een sessie verzenden kunnen en vervolgens Hallo 'Stap 1' kolom alleen ziet u hoe gebruikers zich gedragen na Hallo *eerste* exemplaar van de eerste gebeurtenis, niet alle exemplaren.

## <a name="next-steps"></a>Volgende stappen

* [Overzicht gebruik](app-insights-usage-overview.md)
* [Gebruikers, sessies en gebeurtenissen](app-insights-usage-segmentation.md)
* [Retentie](app-insights-usage-retention.md)
* [Aangepaste gebeurtenissen tooyour app toevoegen](app-insights-api-custom-events-metrics.md)
