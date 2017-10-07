---
title: aaaMonitor prestaties van Azure-web-app | Microsoft Docs
description: Prestaties controleren voor Azure-web-apps. Laad- en reactietijd voor grafieken, afhankelijkheidsinformatie en waarschuwingen instellen voor prestaties.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a>Prestaties van Azure-web-apps controleren
In Hallo [Azure Portal](https://portal.azure.com) kunt u een application performance monitoring instellen uw [Azure-web-apps](../app-service-web/app-service-web-overview.md). [Azure Application Insights](app-insights-overview.md) instrumenten van uw app toosend telemetrie over de activiteiten toohello Application Insights-service, waar ze worden opgeslagen en geanalyseerd. Daar metrische grafieken en zoekfuncties kunnen worden gebruikt toohelp vaststellen van problemen met de prestaties verbeteren en beoordelen van informatie over het gebruik.

## <a name="run-time-or-build-time"></a>Runtime of buildtime
U kunt configureren om bewaking in door te instrumenteren Hallo-app op twee manieren:

* **Runtime**: u kunt een uitbreiding van de prestatiecontrole selecteren wanneer uw web-app al gepubliceerd is. Het is niet nodig toorebuild of uw app opnieuw te installeren. U ontvangt een standaardset aan pakketten voor het controleren van reactietijden, succespercentages, uitzonderingen, afhankelijkheden, enzovoort. 
* **Buildtime**: u kunt een pakket installeren in uw app in ontwikkeling. Deze optie is veelzijdiger. In aanvulling toohello dezelfde standaard pakketten, kunt u code toocustomize Hallo telemetrie of toosend uw eigen telemetrie. U kunt specifieke activiteiten of record gebeurtenissen op basis van toohello semantiek van het domein van uw app registreren. 

## <a name="run-time-instrumentation-with-application-insights"></a>Runtime-instrumentatiesleutel met Application Insights
Als u al een web-app uitvoert in Azure, is er al sprake van enige controle: frequentie van aanvragen en fouten. Application Insights tooget meer, zoals reactietijden, bewaking aanroepen toodependencies Slimme detectie en krachtige logboekanalyse Hallo-querytaal toevoegen. 

1. **Selecteer Application Insights** in hello Azure Configuratiescherm voor uw web-app.
   
    ![Kies Application Insights onder Controleren.](./media/app-insights-azure-web-apps/05-extend.png)
   
   * Kies toocreate een nieuwe resource, tenzij u al ingesteld voor deze app een Application Insights-resource door andere route.
2. **Instrumenteer uw web-app** nadat Application Insights is geïnstalleerd. 
   
    ![Uw web-app instrumenteren](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   **Schakel bewaking aan clientzijde in** voor paginaweergave- en gebruikerstelemetrie.

   * Selecteer Instellingen > Toepassingsinstellingen
   * Voeg een nieuw sleutelwaardepaar toe bij App-instellingen: 
   
    Sleutel: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Waarde:`true`
   * **Sla** Hallo instellingen en **opnieuw** uw app.
3. **Controleer uw app**.  [Expore hello gegevens](#explore-the-data).

Als u wilt, kunt u later Hallo-app met Application Insights maken.

*Hoe ik Application Insights verwijderen, of schakel toosending tooanother resource?*

* Open in Azure, open Hallo blade web-app besturingselement en onder ontwikkelingsprogramma's **extensies**. Verwijder de extensie Application Insights Hallo. Klik onder controle, kies Application Insights en maak of selecteer Hallo-bron die u wilt.

## <a name="build-hello-app-with-application-insights"></a>Hallo-app met Application Insights bouwen
Application Insights kan gedetailleerdere telemetrie verstrekken door een SDK in uw app te installeren. U kunt met name traceerlogboeken verzamelen, [aangepaste telemetrie schrijven](app-insights-api-custom-events-metrics.md) en gedetailleerdere uitzonderingsrapporten ophalen.

1. Configureer **in Visual Studio** (2013-update 2 of hoger) Application Insights voor uw project.

    Met de rechtermuisknop op het Hallo-webproject en selecteer **toevoegen > Application Insights** of **Configure Application Insights**.
   
    ![Met de rechtermuisknop op het Hallo-webproject en het toevoegen of configureren van Application Insights kiezen](./media/app-insights-azure-web-apps/03-add.png)
   
    Als u wordt gevraagd toosign in, moet u Hallo referenties gebruikt voor uw Azure-account.
   
    Hallo-bewerking heeft twee gevolgen:
   
   1. Maakt een Application Insights-resource in Azure, waarbij telemetrie wordt opgeslagen, geanalyseerd en weergegeven.
   2. Voegt Hallo Application Insights NuGet-pakket tooyour code (indien deze nog niet er), en configureert deze toosend telemetrie toohello Azure-resource.
2. **Hallo telemetrie testen** door actieve Hallo-app in uw ontwikkelcomputer (F5).
3. **Hallo-app publiceren** tooAzure in Hallo gebruikelijke manier. 

*Hoe schakel ik toosending tooa verschillende Application Insights-resource*

* Kies in Visual Studio-project met de rechtermuisknop op Hallo **Configure Application Insights** en kies de gewenste Hallo-bron. U Hallo optie toocreate een nieuwe resource. Opnieuw maken en implementeren

## <a name="explore-hello-data"></a>Hallo-gegevens verkennen
1. Hallo Application Insights-blade van uw web-app in het Configuratiescherm, ziet u Live metrische gegevens, waarin aanvragen en fouten binnen een tweede of twee van deze optreden. Dit is bijzonder handige informatie wanneer u uw app opnieuw publiceert, omdat u problemen onmiddellijk te zien krijgt.
2. Klik in de volledige Application Insights-resource toohello.

    ![Doorklikken](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    U kunt er ook rechtstreeks naartoe gaan via Azure-resourcenavigatie.

1. Klik op via een grafiek tooget meer detail:
   
    ![Klik op de overzichtsblade van Hallo Application Insights in een grafiek](./media/app-insights-azure-web-apps/07-dependency.png)
   
    U kunt [metrische blades aanpassen](app-insights-metrics-explorer.md).
2. Klik in het verdere toosee afzonderlijke gebeurtenissen en hun eigenschappen:
   
    ![Klik op een gebeurtenis type tooopen een zoekopdracht op dat type gefilterd](./media/app-insights-azure-web-apps/08-requests.png)
   
    U ziet Hallo '...' koppeling tooopen alle eigenschappen.
   
    U kunt [zoekacties aanpassen](app-insights-diagnostic-search.md).

Gebruik voor krachtigere zoekopdrachten via uw telemetrie Hallo [querytaal van logboekanalyse](app-insights-analytics-tour.md).

## <a name="more-telemetry"></a>Meer telemetrie

* [Gegevens voor laden van webpagina](app-insights-javascript.md)
* [Aangepaste telemetrie](app-insights-api-custom-events-metrics.md)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Volgende stappen
* [Hallo profiler uitvoeren op uw live app](app-insights-profiler.md).
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample): Azure Functions bewaken met Application Insights
* [Inschakelen van Azure diagnostics](app-insights-azure-diagnostics.md) toobe verzonden tooApplication Insights.
* [Service health metrische gegevens controleren](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.
* [Ontvang waarschuwingsmeldingen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) wanneer er operationele gebeurtenissen plaatsvinden of metrische gegevens een drempelwaarde overschrijden.
* Gebruik [Application Insights voor JavaScript-apps en webpagina's](app-insights-javascript.md) tooget client telemetrie Hallo browsers die een webpagina bezoekt.
* [Webtests voor beschikbaarheid instellen](app-insights-monitor-web-app-availability.md) toobe gewaarschuwd als uw site is niet beschikbaar.

