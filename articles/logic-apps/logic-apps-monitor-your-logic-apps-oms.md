---
title: aaaMonitor en get inzicht in uw logische app wordt uitgevoerd met OMS - Azure Logic Apps | Microsoft Docs
description: Uw logische app wordt uitgevoerd met logboekanalyse en Operations Management Suite (OMS) tooget insights en uitgebreidere foutopsporing details voor probleemoplossing en diagnostische gegevens controleren
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>Controleren en verkrijgen van inzicht in logic app wordt uitgevoerd met Operations Management Suite (OMS) en Log Analytics

Voor bewaking en uitgebreidere informatie over foutopsporing, kunt u Log Analytics inschakelen op Hallo dezelfde tijd bij het maken van een logische app. Log Analytics biedt Diagnostische logboekregistratie en controle voor uw logische app wordt uitgevoerd via Hallo Operations Management Suite (OMS)-portal. Wanneer u Hallo Logic Apps-Management-oplossing tooOMS toevoegt, krijgt u de cumulatieve status van uw logische app wordt uitgevoerd en de specifieke gegevens, zoals status, uitvoeringstijd, de status opnieuw indienen en correlatie-id's.

Dit onderwerp leest hoe tooturn op logboekanalyse of installeer Logic Apps-beheeroplossing in OMS Hallo zodat u kunt de runtime-gebeurtenissen weergeven of gegevens voor uw logische app uitgevoerd.

 > [!TIP]
 > toomonitor uw bestaande logische apps als volgt te werk te [Diagnostische logboekregistratie inschakelen en het verzenden van logic app runtime gegevens tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

## <a name="requirements"></a>Vereisten

Voordat u begint, moet u toohave een OMS-werkruimte. Meer informatie over [hoe toocreate een OMS-werkruimte](../log-analytics/log-analytics-get-started.md). 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>Logboekregistratie van diagnostische gegevens inschakelen bij het maken van logische apps

1. In [Azure-portal](https://portal.azure.com), een logische app maken. Kies **nieuwe** > **Enterprise Integration** > **logische App** > **maken**.

   ![Een logische app maken](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. In Hallo **maken logische app** pagina, deze taken uitvoeren zoals wordt weergegeven:

   1. Geef een naam voor uw logische app en selecteer uw Azure-abonnement. 
   2. Maak of Selecteer een Azure-resourcegroep.
   3. Stel **logboekanalyse** te**op**. 
   Selecteer Hallo OMS-werkruimte waar u te verzenden van gegevens voor uw logische app wordt uitgevoerd. 
   4. Als u klaar bent, kiest u **pincode toodashboard** > **maken**.

      ![Logische app maken](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      Nadat u deze stap, Azure uw logische app, nu is maakt die zijn gekoppeld aan de OMS-werkruimte. 
      Deze stap installeert Hallo Logic Apps-beheeroplossing bovendien ook automatisch in de OMS-werkruimte.

3. uw logische app wordt uitgevoerd in OMS, tooview [doorgaan met deze stappen](#view-logic-app-runs-oms).

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>Hallo Logic Apps-beheeroplossing in OMS installeren

Als u al ingeschakeld logboekanalyse tijdens het maken van uw logische app, moet u deze stap overslaan. U hebt al Hallo Logic Apps beheeroplossing geïnstalleerd in OMS.

1. In Hallo [Azure-portal](https://portal.azure.com), kies **meer Services**. Zoek naar 'log analytics' als filter, en kies **logboekanalyse** zoals wordt weergegeven:

   ![Kies 'Log Analytics'](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. Onder **logboekanalyse**, zoeken en selecteert u de OMS-werkruimte. 

   ![Selecteer de OMS-werkruimte](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. Onder **Management**, kies **OMS-Portal**.

   ![Kies 'OMS-Portal'](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. Op uw startpagina OMS als Hallo upgrade banner wordt weergegeven, kies Hallo banner zodat u eerst de OMS-werkruimte upgraden. Kies vervolgens **galerie met oplossingen**.

   ![Kies 'Galerie met oplossingen'](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. Onder **alle oplossingen**, zoeken en kiest u de tegel Hallo voor Hallo **Logic Apps Management** oplossing.

   ![Kies 'Logic Apps Management'](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. Kies tooinstall Hallo oplossing in de OMS-werkruimte **toevoegen**.

   ![Kies "Toevoegen" voor 'Logic Apps Management'](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>Uw logische app wordt uitgevoerd in de OMS-werkruimte weergeven

1. tooview hello aantal en de status van uw logische app wordt uitgevoerd, gaat u toohello overzichtspagina voor de OMS-werkruimte. Bekijk de details op Hallo Hallo **Logic Apps Management** tegel.

   ![Overzichttegel waarbij logic app uitvoeren en status](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > Als deze upgrade banner wordt weergegeven in plaats van Hallo Logic Apps Management tegel, kiest u Hallo banner zodat u uw OMS-werkruimte eerst upgraden.
  
   > ![Upgrade 'OMS-werkruimte'](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. tooview een samenvatting met meer informatie over uw logische app wordt uitgevoerd, kies Hallo **Logic Apps Management** tegel.

   Uw logische app wordt uitgevoerd worden hier, gegroepeerd op naam of uitvoeringsstatus.

   ![Samenvatting van status voor uw logische app wordt uitgevoerd](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. alle Hallo tooview wordt uitgevoerd voor een specifieke logische app of de status, selecteer Hallo rij voor een logische app of met de status.

   Hier volgt een voorbeeld waarin alle hello wordt uitgevoerd voor een specifieke logische app:

   ![Weergave voor een logische app of met de status wordt uitgevoerd](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > Hallo **opnieuw indienen** kolom ziet u 'Ja' voor worden uitgevoerd die het resultaat zijn van een opnieuw ingediende uitvoeren.

4. toofilter deze resultaten, kunt u uitvoeren zowel client- en serverzijde filteren.

   * Client-side '-filter: Kies Hallo filters die u wilt dat voor elke kolom. 
   Hier volgen enkele voorbeelden:

     ![Voorbeeld kolomfilters](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * Filter serverzijde: toochoose een specifiek tijdstip venster of toolimit Hallo aantal wordt uitgevoerd die worden weergegeven, gebruik Hallo bereik besturingselement bovenaan Hallo Hallo pagina. 
   Standaard worden alleen 1000 records tegelijk weergegeven. 
   
     ![Wijziging Hallo tijdvenster](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. alle tooview Hallo acties en de bijbehorende gegevens voor een specifieke uitvoeren, selecteer een rij die Hallo logboek zoekpagina wordt geopend. 

   * Deze informatie in een tabel, kiest u tooview **tabel**.
   * toochange hello query, kunt u Hallo queryreeks in de zoekbalk Hallo bewerken. 
   Kies voor een betere ervaring **Advanced Analytics**.

     ![Acties en details voor een logische app uitgevoerd weergeven](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     Hier op Hallo Azure Log Analytics pagina kunt u query's en bijwerken weergeven Hallo resultaat is van een Hallo tabel. 
     Deze query gebruikt [Kusto querytaal](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), die u als u wilt dat andere resultaten tooview kunt bewerken. 

     ![Azure Log Analytics - queryweergave](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>Volgende stappen

* [B2B-berichten bewaken](../logic-apps/logic-apps-monitor-b2b-message.md)
