---
title: aaaSCOM integratie met Application Insights | Microsoft Docs
description: Als u een SCOM-gebruiker bent, prestaties bewaken en onderzoeken van problemen met Application Insights. Uitgebreide dashboards, slimme waarschuwingen, krachtige diagnostische hulpprogramma's en analyse query's.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>Toepassingsprestaties bewaken met Application Insights voor SCOM
Als u System Center Operations Manager (SCOM) toomanage uw servers, kunt u bewaking van prestaties en prestatieproblemen met behulp van Hallo [Azure Application Insights](app-insights-asp-net.md). Application Insights wordt uw webtoepassing inkomende aanvragen en uitgaande REST en SQL-aanroepen, uitzonderingen en logboektraceringen bewaakt. Het biedt dashboards metrische grafieken en slimme waarschuwingen, evenals krachtige diagnostische gegevens doorzoeken en analytische query's via deze telemetrie. 

U kunt overschakelen op de bewaking van Application Insights met behulp van een SCOM management pack.

## <a name="before-you-start"></a>Voordat u begint
We gaan ervan uit:

* U bekend bent met SCOM en dat u SCOM 2012 R2 of 2016 toomanage uw IIS-webservers.
* U hebt al geïnstalleerd op de servers die een webtoepassing die u toomonitor met Application Insights wilt.
* App-framework-versie is .NET 4.5 of hoger.
* Hebt u toegang tooa abonnement in [Microsoft Azure](https://azure.com) en toohello kunt aanmelden [Azure-portal](https://portal.azure.com). Uw organisatie kan een abonnement hebt en uw Microsoft-account tooit kunt toevoegen.

(ontwikkelteam Hallo Hallo mogelijk bouwen [Application Insights-SDK](app-insights-asp-net.md) in Hallo web-app. Deze instrumentation build-tijd biedt deze meer flexibiliteit bij het schrijven van aangepaste telemetrie. Echter, het maakt niet uit: u kunt stappen Hallo Hier wordt beschreven, met of zonder Hallo SDK ingebouwd.)

## <a name="one-time-install-application-insights-management-pack"></a>(Eenmaal) Application Insights management pack installeren
Op het Hallo-machine waarop u Operations Manager uitvoert:

1. Een oude versie van Hallo management pack verwijderen:
   1. Open in Operations Manager, beheer-, Management Packs. 
   2. Verwijder de oude versie Hallo.
2. Download en installeer Hallo management pack uit Hallo-catalogus.
3. Start Operations Manager opnieuw.

## <a name="create-a-management-pack"></a>Een management pack maken
1. Open in Operations Manager **ontwerpen**, **.NET... met Application Insights**, **Wizard bewaking toevoegen**, en kies opnieuw **.NET... met de toepassing Insights**.
   
    ![](./media/app-insights-scom/020.png)
2. Na uw app naam Hallo-configuratie. (U hebt tooinstrument één app tegelijk.)
   
    ![](./media/app-insights-scom/030.png)
3. Hallo op dezelfde pagina van de wizard, maak een nieuw management pack of Selecteer een pakket dat u eerder voor Application Insights hebt gemaakt.
   
     (Hallo Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is een sjabloon, waaruit u een exemplaar maken. U kunt opnieuw gebruiken hetzelfde exemplaar later Hallo.)

    ![Typ in Hallo tabblad algemene eigenschappen, Hallo-naam van Hallo-app. Klik op Nieuw en typ een naam voor een management pack. Klik op OK en klik op volgende.](./media/app-insights-scom/040.png)

1. Kies een app die u toomonitor wilt. Hallo zoekfunctie zoekt tussen apps die zijn geïnstalleerd op uw servers.
   
    ![Op welke tabblad tooMonitor klikt u op toevoegen, typt u deel van naam van de app hello, klik op zoeken, OK Hallo-app en klik vervolgens op toevoegen, kiest.](./media/app-insights-scom/050.png)
   
    Hallo optioneel bewaking bereik veld mag gebruikte toospecify een subset van uw servers, als u niet dat in alle servers toomonitor Hallo-app wilt.
2. Op de volgende wizardpagina hello, moet u eerst uw referenties toosign in tooMicrosoft Azure opgeven.
   
    Op deze pagina kunt kiezen u Hallo Application Insights-resource waar u Hallo telemetrie gegevens toobe geanalyseerd en weergegeven. 
   
   * Als de toepassing hello is geconfigureerd voor Application Insights tijdens de ontwikkeling, selecteert u de bestaande resource.
   * Anders maakt u een nieuwe resource met de naam van het Hallo-app. Als er andere apps die deel uitmaken van Hallo hetzelfde systeem, plaatst u deze in Hallo dezelfde resourcegroep bevinden, toomake toegang toohello telemetrie eenvoudiger toomanage.
     
     U kunt deze instellingen later wijzigen.
     
     ![Klik op 'aanmelden' op het tabblad voor Application Insights-instellingen en geef de referenties van uw Microsoft-account voor Azure. Kies een abonnement, de resourcegroep en de resource.](./media/app-insights-scom/060.png)
3. Hallo voltooid de wizard.
   
    ![Klik op Maken](./media/app-insights-scom/070.png)

Herhaal deze procedure voor elke app die u toomonitor wilt.

Als u toochange instellingen later nodig, opnieuw Hallo eigenschappen van de monitor Hallo vanuit Hallo ontwerpen-venster te openen.

![In het ontwerp, selecteer .NET Application Performance Monitoring met Application Insights, selecteer de monitor en klikt u op Eigenschappen.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>Controleer of de bewaking
Hallo-monitor is dat u zoekt naar uw app hebt geïnstalleerd op elke server. Waar het Hallo-app wordt gevonden configureert het Application Insights Status Monitor toomonitor Hallo app. Indien nodig, worden eerst Status Monitor op Hallo server installeert.

U kunt controleren welke exemplaren van Hallo app dat is aangetroffen:

![Open in de bewaking, Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>Weergave telemetrie in Application Insights
In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello bron voor uw app. U [grafieken weergegeven telemetrie](app-insights-dashboards.md) van uw app. (Als dit nog niet wordt weergegeven om op de hoofdpagina Hallo nog, klikt u op livestream metrische gegevens.)

## <a name="next-steps"></a>Volgende stappen
* [Instellen van een dashboard](app-insights-dashboards.md) toobring samen Hallo belangrijkste grafieken bewaking van deze en andere apps.
* [Meer informatie over metrische gegevens](app-insights-metrics-explorer.md)
* [Waarschuwingen instellen](app-insights-alerts.md)
* [Prestatieproblemen oplossen](app-insights-detect-triage-diagnose.md)
* [Krachtige Analytics-query 's](app-insights-analytics.md)
* [Webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md)

