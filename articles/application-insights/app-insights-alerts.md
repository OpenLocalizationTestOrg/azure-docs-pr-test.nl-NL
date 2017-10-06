---
title: aaaSet waarschuwingen in Azure Application Insights | Microsoft Docs
description: Blijf op de hoogte over trage responstijden, uitzonderingen, en andere prestaties of gebruik wijzigingen in uw web-app.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a>Meldingen instellen in Application Insights
[Azure Application Insights] [ start] waarschuwt u toochanges in prestaties of gebruik metrische gegevens in uw web-app. 

Application Insights wordt uw live app bewaakt op een [groot aantal verschillende platformen] [ platforms] toohelp u prestatieproblemen en gebruikspatronen te begrijpen.

Er zijn drie soorten waarschuwingen:

* **Metrische waarschuwingen** laat u weten wanneer een metriek een drempelwaarde overschrijden gedurende een bepaalde - zoals reactietijden, aantal uitzonderingen is, CPU-gebruik of paginaweergaven. 
* [**Webtests** ] [ availability] laat u weten wanneer uw site is niet beschikbaar op Hallo internet of traag reageert. [Meer informatie][availability].
* [**Proactieve diagnoses** ](app-insights-proactive-diagnostics.md) worden automatisch geconfigureerd toonotify u over ongebruikelijke prestatiepatronen.

We zich richten op metrische waarschuwingen in dit artikel.

## <a name="set-a-metric-alert"></a>Een metriek waarschuwing instellen
Open Hallo waarschuwingsregels blade en gebruik Hallo toevoegen knop. 

![Hallo waarschuwingsregels blade kiezen waarschuwing toevoegen. Uw app niet instellen omdat de bron toomeasure hello, Geef een naam op voor Hallo waarschuwing en een waarde kiezen.](./media/app-insights-alerts/01-set-metric.png)

* Hallo-bron voordat Hallo andere eigenschappen instellen. **Kies '(onderdelen)' hello resource** als u wilt dat tooset waarschuwingen op de prestaties of gebruik metrische gegevens.
* geeft u de waarschuwing toohello Hallo-naam moet uniek zijn binnen de resourcegroep hello (niet alleen uw toepassing).
* Worden zorgvuldige toonote Hallo eenheden waarin u wordt gevraagd tooenter Hallo drempelwaarde.
* Als u selectievakje Hallo '... e-eigenaars', worden waarschuwingen verzonden door de e-tooeveryone wie toegang tot toothis resourcegroep heeft. deze personen, ingesteld tooexpand toohello toe te voegen [resourcegroep of abonnement](app-insights-resources-roles-access-control.md) (geen resource Hallo).
* Als u 'Extra e-mailberichten' opgeeft, worden waarschuwingen verzonden toothose personen of groepen (of u dit selectievakje inschakelt Hallo e-eigenaars...' vak). 
* Stel een [webhook adres](../monitoring-and-diagnostics/insights-webhooks-alerts.md) als u een web-app die tooalerts reageert hebt ingesteld. Deze wordt aangeroepen wanneer Hallo waarschuwing is geactiveerd en wanneer het probleem is opgelost. (Maar houd er rekening mee dat op dit moment, query-parameters niet als webhookeigenschappen doorgegeven.)
* U kunt uitschakelen of inschakelen Hallo signaal: Hallo knoppen Hallo boven aan het Hallo-blade.

*Waarschuwing knop Hallo toevoegen wordt niet weergegeven.* 

* Gebruikt u een organisatie-account? Als u de eigenaar of bijdrager toegang toothis toepassingsresource hebt, kunt u waarschuwingen instellen. Bekijk Hallo Access Control-blade. [Meer informatie over toegangsbeheer][roles].

> [!NOTE]
> Hallo waarschuwingen blade u ziet dat er al een waarschuwing set up is: [proactieve diagnoses](app-insights-proactive-failure-diagnostics.md). Hallo automatische waarschuwing controleert een bepaalde meetwaarde, percentage mislukte. Tenzij u toodisable Hallo proactieve waarschuwing besluit, hoeft u geen tooset uw eigen een waarschuwing voor Faalpercentage van de aanvraag. 
> 
> 

## <a name="see-your-alerts"></a>Uw waarschuwingen weergegeven
Krijgt u een e-mailbericht wanneer de status van een waarschuwing wijzigt tussen inactieve en actief. 

Hallo huidige status van elke waarschuwing wordt weergegeven in Hallo waarschuwingsregels blade.

Er is een overzicht van recente activiteiten in Hallo waarschuwingen vervolgkeuzelijst:

![Waarschuwingen-omlaag](./media/app-insights-alerts/010-alert-drop.png)

Hallo-geschiedenis van statuswijzigingen heeft Hallo activiteitenlogboek:

![Klik op instellingen, controlelogboeken op de overzichtsblade Hallo](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a>Hoe waarschuwingen werken
* Een waarschuwing heeft drie statussen: 'Nooit geactiveerd', 'Geactiveerd' en "Opgelost." Geactiveerde betekent Hallo voorwaarde die u hebt opgegeven is waar, wanneer deze het laatst is geëvalueerd.
* Een melding wordt gegenereerd wanneer de status van een waarschuwing wordt gewijzigd. (Als Hallo meldingsvoorwaarde al true is wanneer u Hallo waarschuwing gemaakt, mogelijk niet krijgt u een melding totdat Hallo voorwaarde onwaar gaat.)
* Elke melding genereert een e-mailadres als u gecontroleerd Hallo e-mailberichten vak of e-mailadressen opgegeven. U kunt ook zoeken op Hallo meldingen vervolgkeuzelijst.
* Een waarschuwing wordt elke keer dat een metriek, maar niet anders binnenkomt geëvalueerd.
* Hallo evaluatie Hallo metriek aggregeert via Hallo voorgaande periode, en vergelijkt deze toohello drempelwaarde toodetermine Hallo nieuwe status.
* Hallo-periode die u kiest geeft Hallo-interval gedurende welke de metrische gegevens worden geaggregeerd. Heeft geen invloed op hoe vaak hello waarschuwing wordt geëvalueerd: dat is afhankelijk van Hallo frequentie van de aankomst van metrische gegevens.
* Als er worden geen gegevens is voor een bepaalde metriek voor even binnenkomt, heeft Hallo hiaat verschillende gevolgen voor de evaluatie van de waarschuwing en op Hallo grafieken in metrische explorer. Als er geen gegevens die u voor het langer dan steekproefinterval Hallo-grafiek toont Hallo-diagram in metrische explorer een waarde van 0. Maar een waarschuwing op basis van Hallo dezelfde metrische gegevens is niet opnieuw worden geëvalueerd en Hallo van waarschuwing status blijft ongewijzigd. 
  
    Wanneer gegevens uiteindelijk aankomen, gaat de grafiek Hallo tooa back andere waarde dan nul. Hallo-waarschuwing wordt geëvalueerd op basis van Hallo gegevens beschikbaar voor Hallo periode die u hebt opgegeven. Als nieuwe gegevenspunt Hallo Hallo slechts één beschikbaar in Hallo periode, Hallo cumulatieve gebaseerd alleen op punt van gegevens.
* Een waarschuwing kunt vaak knipperen tussen waarschuwingen en de goede status, zelfs als u een lange periode instelt. Dit kan gebeuren als de metrische waarde hello wordt bewogen rond Hallo drempelwaarde. Er is geen hysteresis Hallo drempelwaarde: Hallo overgang tooalert gebeurt op dezelfde als Hallo overgang toohealthy waarde Hallo.

## <a name="what-are-good-alerts-tooset"></a>Wat zijn goede waarschuwingen tooset?
Dit is afhankelijk van uw toepassing. toostart, is het handig niet tooset te veel metrische gegevens. Besteed voldoende tijd kijken naar uw metrische grafieken terwijl uw app wordt uitgevoerd, tooget een idee voor hoe het werkt normaal. Deze oefening kunt u de prestaties van tooimprove manieren vinden. Stel waarschuwingen tootell u wanneer Hallo metrische gegevens buiten de normale zone Hallo gaat. 

Populaire waarschuwingen zijn onder andere:

* [Browser metrische gegevens][client], met name Browser **pagina laadtijden**, geschikt zijn voor webtoepassingen. Als uw pagina veel scripts heeft, moet u controleren of **browseruitzonderingen**. In de volgorde tooget deze metrische gegevens en waarschuwingen, hebt u tooset up [webpagina bewaking][client].
* **Serverreactietijd** voor de serverzijde Hallo van webtoepassingen. En het instellen van waarschuwingen, Let op deze metrische toosee als deze niet goed met hoog tarieven varieert: variatie kan erop wijzen dat uw app wordt uitgevoerd onvoldoende resources. 
* **Serveruitzonderingen** -toosee ze, hebt u toodo sommige [aanvullende instellingen](app-insights-asp-net-exceptions.md).

Vergeet niet dat [proactieve fout snelheid diagnostics](app-insights-proactive-failure-diagnostics.md) automatisch monitor Hallo-snelheid waarmee uw app toorequests met fout codes reageert. 

## <a name="automation"></a>Automatisering
* [Gebruik PowerShell tooautomate instellen van waarschuwingen](app-insights-powershell-alerts.md)
* [Webhooks tooautomate reageert tooalerts gebruiken](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>Zie ook
* [Webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md)
* [Instellen van waarschuwingen automatiseren](app-insights-powershell-alerts.md)
* [Proactieve diagnostische gegevens](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

