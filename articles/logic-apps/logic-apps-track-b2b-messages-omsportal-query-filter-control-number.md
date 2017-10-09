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
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="b6203-103">Query voor AS2, X 12 en EDIFACT berichten in Hallo Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="b6203-103">Query for AS2, X12, and EDIFACT messages in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="b6203-104">toofind hello AS2, X 12 en EDIFACT berichten die u bijhoudt met [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in Hallo [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), kunt u query's die op basis van specifieke acties filteren maken criteria.</span><span class="sxs-lookup"><span data-stu-id="b6203-104">toofind hello AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="b6203-105">U kunt bijvoorbeeld berichten op basis van een specifieke interchange besturingselement getal vinden.</span><span class="sxs-lookup"><span data-stu-id="b6203-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="b6203-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b6203-106">Requirements</span></span>

* <span data-ttu-id="b6203-107">Een logische app die ingesteld met de logboekregistratie van diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="b6203-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="b6203-108">Meer informatie over [hoe toocreate een logische app](../logic-apps/logic-apps-create-a-logic-app.md) en [hoe tooset logboekregistratie voor die app logica van](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="b6203-108">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="b6203-109">Integratie-account ingesteld met de controle en logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="b6203-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="b6203-110">Meer informatie over [hoe toocreate een account integratie](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) en [hoe tooset van controle en logboekregistratie voor dat account](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="b6203-110">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="b6203-111">Als u dat nog niet gedaan hebt, [publiceren diagnostische gegevens tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) en [bericht bijhouden in OMS instellen](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="b6203-111">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b6203-112">Nadat u Hallo vorige vereisten hebt voldaan, moet u een werkruimte in Hallo hebben [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6203-112">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="b6203-113">U moet gebruiken Hallo dezelfde OMS-werkruimte voor het bijhouden van uw B2B-communicatie in OMS.</span><span class="sxs-lookup"><span data-stu-id="b6203-113">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="b6203-114">Als u een OMS-werkruimte niet hebt, ontdek [hoe toocreate een OMS-werkruimte](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6203-114">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a><span data-ttu-id="b6203-115">Bericht-query's maken met filters in Hallo Operations Management Suite-portal</span><span class="sxs-lookup"><span data-stu-id="b6203-115">Create message queries with filters in hello Operations Management Suite portal</span></span>

<span data-ttu-id="b6203-116">In dit voorbeeld ziet hoe u berichten op basis van hun DIF besturingselement aantal kunt vinden.</span><span class="sxs-lookup"><span data-stu-id="b6203-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="b6203-117">Als u de naam van uw OMS-werkruimte, gaat u tooyour werkruimte startpagina (`https://{your-workspace-name}.portal.mms.microsoft.com`), en beginnen bij stap 4.</span><span class="sxs-lookup"><span data-stu-id="b6203-117">If you know your OMS workspace name, go tooyour workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="b6203-118">Anders kunt u beginnen bij stap 1.</span><span class="sxs-lookup"><span data-stu-id="b6203-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="b6203-119">In Hallo [Azure-portal](https://portal.azure.com), kies **meer Services**.</span><span class="sxs-lookup"><span data-stu-id="b6203-119">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="b6203-120">Zoek naar 'log analytics' in en kies vervolgens **logboekanalyse** als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="b6203-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Log Analytics vinden](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="b6203-122">Onder **logboekanalyse**, zoeken en selecteert u de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="b6203-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Selecteer de OMS-werkruimte](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="b6203-124">Onder **Management**, kies **OMS-Portal**.</span><span class="sxs-lookup"><span data-stu-id="b6203-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Kies de OMS-portal](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="b6203-126">Kies op de startpagina OMS **logboek zoeken**.</span><span class="sxs-lookup"><span data-stu-id="b6203-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Kies op uw startpagina OMS "Logboek zoeken"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="b6203-128">-of-</span><span class="sxs-lookup"><span data-stu-id="b6203-128">-or-</span></span>

   ![Kies 'Logboek zoeken' hello OMS menu](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="b6203-130">Voer in het zoekvak hello, een veld dat u wilt dat toofind, en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b6203-130">In hello search box, enter a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="b6203-131">Wanneer u te typen begint, OMS laat zien u mogelijke overeenkomsten en de bewerkingen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b6203-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="b6203-132">Meer informatie over [hoe toofind gegevens in logboekanalyse](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="b6203-132">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="b6203-133">Dit voorbeeld wordt gezocht voor gebeurtenissen met de **Type = AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="b6203-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Begin met het typen van queryreeks](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="b6203-135">Kies in de linkerbalk Hallo Hallo periode die u tooview wilt.</span><span class="sxs-lookup"><span data-stu-id="b6203-135">In hello left bar, choose hello timeframe that you want tooview.</span></span> <span data-ttu-id="b6203-136">Kies een filterquery tooyour tooadd **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b6203-136">tooadd a filter tooyour query, choose **+Add**.</span></span>

   ![Filter tooquery toevoegen](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="b6203-138">Onder **Filters toevoegen**, Voer Hallo filternaam in zodat u de gewenste Hallo-filter kunt vinden.</span><span class="sxs-lookup"><span data-stu-id="b6203-138">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="b6203-139">Selecteer Hallo-filter en kies **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b6203-139">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="b6203-140">toofind hello interchange besturingselement nummer in dit voorbeeld Hallo-word 'interchange' zoekt en selecteert **event_record_messageProperties_interchangeControlNumber_s** als Hallo filter.</span><span class="sxs-lookup"><span data-stu-id="b6203-140">toofind hello interchange control number, this example searches for hello word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as hello filter.</span></span>

   ![Selecteer filter](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="b6203-142">Selecteer in de linkerbalk Hallo Hallo filterwaarde wilt toouse en kies **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="b6203-142">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   <span data-ttu-id="b6203-143">In het volgende voorbeeld wordt de Hallo interchange controle-aantal we willen Hallo-berichten.</span><span class="sxs-lookup"><span data-stu-id="b6203-143">This example selects hello interchange control number for hello messages we want.</span></span>

   ![Selecteer filterwaarde](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="b6203-145">Nu terug toohello query die u maakt.</span><span class="sxs-lookup"><span data-stu-id="b6203-145">Now return toohello query that you're building.</span></span> <span data-ttu-id="b6203-146">De query is bijgewerkt met het geselecteerde filter gebeurtenis en de waarde.</span><span class="sxs-lookup"><span data-stu-id="b6203-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="b6203-147">De resultaten van uw vorige worden nu te gefilterd.</span><span class="sxs-lookup"><span data-stu-id="b6203-147">Your previous results are now filtered too.</span></span>

    ![Tooyour query met gefilterde resultaten retourneren](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="b6203-149">Sla de query voor toekomstig gebruik</span><span class="sxs-lookup"><span data-stu-id="b6203-149">Save your query for future use</span></span>

1. <span data-ttu-id="b6203-150">Uit uw query op Hallo **logboek zoeken** pagina **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b6203-150">From your query on hello **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="b6203-151">De query een naam geven, selecteert u een categorie en kies **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b6203-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![De query een naam en categorie geven](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="b6203-153">tooview uw query kiezen **Favorieten**.</span><span class="sxs-lookup"><span data-stu-id="b6203-153">tooview your query, choose **Favorites**.</span></span>

   !['Favorieten' kiezen](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="b6203-155">Onder **opgeslagen zoekacties**, selecteert u uw query zodat u kunt Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="b6203-155">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="b6203-156">tooupdate hello query zodat u kunt verschillende resultaten vinden Hallo query bewerken.</span><span class="sxs-lookup"><span data-stu-id="b6203-156">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Uw query selecteren](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a><span data-ttu-id="b6203-158">Zoeken en opgeslagen query's uitvoeren in Hallo Operations Management Suite-portal</span><span class="sxs-lookup"><span data-stu-id="b6203-158">Find and run saved queries in hello Operations Management Suite portal</span></span>

1. <span data-ttu-id="b6203-159">Open de startpagina van de OMS-werkruimte (`https://{your-workspace-name}.portal.mms.microsoft.com`), en kies **logboek zoeken**.</span><span class="sxs-lookup"><span data-stu-id="b6203-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Kies op uw startpagina OMS "Logboek zoeken"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="b6203-161">-of-</span><span class="sxs-lookup"><span data-stu-id="b6203-161">-or-</span></span>

   ![Kies 'Logboek zoeken' hello OMS menu](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="b6203-163">Op Hallo **logboek zoeken** startpagina, kiest u **Favorieten**.</span><span class="sxs-lookup"><span data-stu-id="b6203-163">On hello **Log Search** home page, choose **Favorites**.</span></span>

   !['Favorieten' kiezen](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="b6203-165">Onder **opgeslagen zoekacties**, selecteert u uw query zodat u kunt Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="b6203-165">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="b6203-166">tooupdate hello query zodat u kunt verschillende resultaten vinden Hallo query bewerken.</span><span class="sxs-lookup"><span data-stu-id="b6203-166">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Uw query selecteren](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="b6203-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b6203-168">Next steps</span></span>

* [<span data-ttu-id="b6203-169">Volgschema’s voor AS2</span><span class="sxs-lookup"><span data-stu-id="b6203-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="b6203-170">Volgschema’s voor X12</span><span class="sxs-lookup"><span data-stu-id="b6203-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="b6203-171">Bijhouden van aangepaste schema 's</span><span class="sxs-lookup"><span data-stu-id="b6203-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)