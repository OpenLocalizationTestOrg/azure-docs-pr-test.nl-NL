---
title: aaaQuery voor B2B-berichten in de Operations Management Suite - Azure Logic Apps | Microsoft Docs
description: Maken van query's tootrack AS2, X 12 en EDIFACT berichten in Hallo Operations Management Suite
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a>Query voor AS2, X 12 en EDIFACT berichten in Hallo Microsoft Operations Management Suite (OMS)

toofind hello AS2, X 12 en EDIFACT berichten die u bijhoudt met [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in Hallo [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), kunt u query's die op basis van specifieke acties filteren maken criteria. U kunt bijvoorbeeld berichten op basis van een specifieke interchange besturingselement getal vinden.

## <a name="requirements"></a>Vereisten

* Een logische app die ingesteld met de logboekregistratie van diagnostische gegevens. Meer informatie over [hoe toocreate een logische app](../logic-apps/logic-apps-create-a-logic-app.md) en [hoe tooset logboekregistratie voor die app logica van](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Integratie-account ingesteld met de controle en logboekregistratie. Meer informatie over [hoe toocreate een account integratie](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) en [hoe tooset van controle en logboekregistratie voor dat account](../logic-apps/logic-apps-monitor-b2b-message.md).

* Als u dat nog niet gedaan hebt, [publiceren diagnostische gegevens tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) en [bericht bijhouden in OMS instellen](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

> [!NOTE]
> Nadat u Hallo vorige vereisten hebt voldaan, moet u een werkruimte in Hallo hebben [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). U moet gebruiken Hallo dezelfde OMS-werkruimte voor het bijhouden van uw B2B-communicatie in OMS. 
>  
> Als u een OMS-werkruimte niet hebt, ontdek [hoe toocreate een OMS-werkruimte](../log-analytics/log-analytics-get-started.md).

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a>Bericht-query's maken met filters in Hallo Operations Management Suite-portal

In dit voorbeeld ziet hoe u berichten op basis van hun DIF besturingselement aantal kunt vinden.

> [!TIP] 
> Als u de naam van uw OMS-werkruimte, gaat u tooyour werkruimte startpagina (`https://{your-workspace-name}.portal.mms.microsoft.com`), en beginnen bij stap 4. Anders kunt u beginnen bij stap 1.

1. In Hallo [Azure-portal](https://portal.azure.com), kies **meer Services**. Zoek naar 'log analytics' in en kies vervolgens **logboekanalyse** als volgt te werk:

   ![Log Analytics vinden](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. Onder **logboekanalyse**, zoeken en selecteert u de OMS-werkruimte.

   ![Selecteer de OMS-werkruimte](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. Onder **Management**, kies **OMS-Portal**.

   ![Kies de OMS-portal](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. Kies op de startpagina OMS **logboek zoeken**.

   ![Kies op uw startpagina OMS "Logboek zoeken"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -of-

   ![Kies 'Logboek zoeken' hello OMS menu](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. Voer in het zoekvak hello, een veld dat u wilt dat toofind, en druk op **Enter**. Wanneer u te typen begint, OMS laat zien u mogelijke overeenkomsten en de bewerkingen die u kunt gebruiken. Meer informatie over [hoe toofind gegevens in logboekanalyse](../log-analytics/log-analytics-log-searches.md).

   Dit voorbeeld wordt gezocht voor gebeurtenissen met de **Type = AzureDiagnostics**.

   ![Begin met het typen van queryreeks](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. Kies in de linkerbalk Hallo Hallo periode die u tooview wilt. Kies een filterquery tooyour tooadd **+ toevoegen**.

   ![Filter tooquery toevoegen](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. Onder **Filters toevoegen**, Voer Hallo filternaam in zodat u de gewenste Hallo-filter kunt vinden. Selecteer Hallo-filter en kies **+ toevoegen**.

   toofind hello interchange besturingselement nummer in dit voorbeeld Hallo-word 'interchange' zoekt en selecteert **event_record_messageProperties_interchangeControlNumber_s** als Hallo filter.

   ![Selecteer filter](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. Selecteer in de linkerbalk Hallo Hallo filterwaarde wilt toouse en kies **toepassen**.

   In het volgende voorbeeld wordt de Hallo interchange controle-aantal we willen Hallo-berichten.

   ![Selecteer filterwaarde](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. Nu terug toohello query die u maakt. De query is bijgewerkt met het geselecteerde filter gebeurtenis en de waarde. De resultaten van uw vorige worden nu te gefilterd.

    ![Tooyour query met gefilterde resultaten retourneren](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a>Sla de query voor toekomstig gebruik

1. Uit uw query op Hallo **logboek zoeken** pagina **opslaan**. De query een naam geven, selecteert u een categorie en kies **opslaan**.

   ![De query een naam en categorie geven](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. tooview uw query kiezen **Favorieten**.

   !['Favorieten' kiezen](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. Onder **opgeslagen zoekacties**, selecteert u uw query zodat u kunt Hallo resultaten weergeven. tooupdate hello query zodat u kunt verschillende resultaten vinden Hallo query bewerken.

   ![Uw query selecteren](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a>Zoeken en opgeslagen query's uitvoeren in Hallo Operations Management Suite-portal

1. Open de startpagina van de OMS-werkruimte (`https://{your-workspace-name}.portal.mms.microsoft.com`), en kies **logboek zoeken**.

   ![Kies op uw startpagina OMS "Logboek zoeken"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -of-

   ![Kies 'Logboek zoeken' hello OMS menu](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. Op Hallo **logboek zoeken** startpagina, kiest u **Favorieten**.

   !['Favorieten' kiezen](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. Onder **opgeslagen zoekacties**, selecteert u uw query zodat u kunt Hallo resultaten weergeven. tooupdate hello query zodat u kunt verschillende resultaten vinden Hallo query bewerken.

   ![Uw query selecteren](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a>Volgende stappen

* [Volgschema’s voor AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Volgschema’s voor X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Bijhouden van aangepaste schema 's](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)