---
title: aaaSmart diagnostische gegevens van web-app prestaties wijzigingen in Azure Application Insights | Microsoft Docs
description: Automatische diagnoses pieken of stappen in de prestatietelemetrie van uw web-app.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a>Onverwachte wijzigingen in uw app telemetrie onderzoeken

*Deze functie is in preview.*

Diagnose plotselinge veranderingen in uw web-app prestatie- of gebruik met een enkele klik! Hallo Smart Diagnostics functie is beschikbaar wanneer u een grafiek tijd in maakt [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md). Wanneer er ook een ongebruikelijke wijzigingen van de trend van uw resultaten, zoals een piek- of een dip Hallo identificeert Smart Diagnostics een patroon van dimensies en de bijbehorende waarden die Hallo wijzigen verklaren kunnen. Zo kunt u snel Hallo probleem opsporen. 

In dit voorbeeld Smart Diagnostics geconstateerd een patroon van eigenschapswaarden met Hallo wijziging en licht Hallo verschil tussen de resultaten met en zonder dit patroon:

![voorbeeld analytics diagnostics resultaat](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a>Gegevenswijzigingen onderzoeken

1.  Een query in analyses uitvoeren en deze worden weergegeven als een tijd-grafiek. 
2.  Klik op elk gewenst moment gemarkeerde piek indien aanwezig.
 
    ![piek-punt](./media/app-insights-analytics-diagnostics/peak.png)

    Diagnostische gegevens duurt een paar seconden toodiscover een patroon.

3. Hallo diagnostische resultaten tabblad ziet u een patroon dat de onderbreking van uw gegevens kan verklaren.

    ![Resultaat](./media/app-insights-analytics-diagnostics/result.png)
 
    Hallo tekst weergegeven hello dimensiewaarden die worden weergegeven toocorrelate met Hallo shift. In dit voorbeeld is deze gekoppeld aan een bepaalde aanvraag en een bepaalde browser-versie.

    U ziet ook Hallo twee onderdelen van de grafiek hello, met Hallo filter true en false. Hallo false onderdeel toont een trend ongewijzigd. Met andere woorden, is er geen wijziging in de resultaten van de telemetrie hello, als we uitsluiten Hallo problematisch combinatie van dimensies die Diagnostics is geïdentificeerd. Daarentegen, Hallo resultaten binnen deze combinatie een indrukwekkende wijziging binnen Hallo gemarkeerd gebied van onderzoek worden weergegeven. Dit betekent dat diagnostische gegevens van een combinatie van eigenschappen die Hallo wijziging wordt heeft gevonden.

4.  Als het Hallo-patroon complex is, moet u toohover via **Alles weergeven** toosee Hallo dimensies.

    ![alles weergeven](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  Als diagnostische gegevens er geen significante patroon toonotify over Hallo vindt ' geen ' resultatenpagina krijgt. Op dit moment kunt u uw query wijzigen. U kan bijvoorbeeld Hallo tijdsbereik en binning in Analytics-query voor een verdere analyse en mogelijk betere resultaten beperken.

. Met een bepaalde pagina van uw website is een probleem op een bepaalde browser Hallo-kennis, u kunt nu rechte toohello probleem pagina gaan en onderzoeken van recente wijzigingen.

## <a name="try-hello-demo"></a>Probeer het Hallo-demo

[Klik hier toosee een demonstratie](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) op voorbeeldgegevens.

## <a name="how-it-works"></a>Hoe werkt het?

Smart Diagnostics maakt gebruik van een geavanceerde zonder supervisie machine learning-algoritme op basis van Hallo [DiffPatterns](app-insights-analytics-reference.md) bewerking. Het lijkt erop voor candidate patronen die Hallo gegevens wijzigen verklaren kunnen. Het Hallo-impact van elke kandidaat op Hallo metrische gegevens analyseert en bevat Hallo-patroon dat beste met Hallo wijziging correleert.

## <a name="no-diagnostic-points"></a>Geen diagnostische punten?

Smart Diagnostics werkt alleen wanneer Hallo volgende criteria wordt voldaan:

 * Smart Diagnostics-instelling is ingeschakeld. Zoek in de Instellingenpictogram Hallo in Analytics.
 * Hallo Smart Diagnostics optie in de instellingen is geselecteerd. 
 * Tijdas: Hallo x-as van grafiekgebied Hallo moet van het type `datetime`.
 * Line- of gebied grafiek: Diagnostics werkt alleen deze typen van grafiek. Gebruik `| render timechart` of `| render areachart` aan Hallo einde van uw query; of Selecteer een regel of vlakdiagram Hallo vervolgkeuzelijst selector.
 * Onderbreking: Er moet een aanzienlijke onderbreking Hallo-gegevens.
 * Onvoldoende punten tooanalyze.
 * Niet meer dan een overzicht van de component in Hallo-query.
 * Geen project-component met de definitie van een naam voordat Hallo overzicht van de component.

 
 ## <a name="related-articles"></a>Verwante artikelen:

 * [Analytics-zelfstudie](app-insights-analytics-tour.md)
 * [Detectie van smartcard](app-insights-proactive-diagnostics.md) waarschuwt u automatisch tooperformance problemen.
