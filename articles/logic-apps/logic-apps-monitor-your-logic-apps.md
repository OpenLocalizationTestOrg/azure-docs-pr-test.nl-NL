---
title: status van de aaaCheck logboekregistratie instellen en ontvang waarschuwingen - Azure Logic Apps | Microsoft Docs
description: Status en prestaties voor logische apps bewaken, meld u diagnostische gegevens en waarschuwingen instellen
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="c9f34-103">Status controleren, instellen van logboekregistratie van diagnostische gegevens en waarschuwingen inschakelen voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c9f34-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="c9f34-104">Nadat u [maken en uitvoeren van een logische app](../logic-apps/logic-apps-create-a-logic-app.md), u kunt de geschiedenis wordt uitgevoerd, trigger geschiedenis, status en prestaties controleren.</span><span class="sxs-lookup"><span data-stu-id="c9f34-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="c9f34-105">Instellen voor het bewaken van realtime-gebeurtenissen en uitgebreidere foutopsporing, [logboekregistratie van diagnostische gegevens](#azure-diagnostics) voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="c9f34-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="c9f34-106">Op die manier kunt u [zoeken en weergeven van gebeurtenissen](#find-events), zoals de trigger-gebeurtenissen, voer gebeurtenissen en in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="c9f34-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="c9f34-107">U kunt dit ook gebruiken [diagnostics-gegevens met andere services](#extend-diagnostic-data), zoals Azure Storage en Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="c9f34-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="c9f34-108">meldingen over fouten of andere mogelijke problemen tooget instellen [waarschuwingen](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="c9f34-108">tooget notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="c9f34-109">Bijvoorbeeld, kunt u een waarschuwing die detecteert 'wanneer meer dan vijf wordt uitgevoerd niet in een uur."</span><span class="sxs-lookup"><span data-stu-id="c9f34-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="c9f34-110">U kunt ook instellen bewaking, bijhouden en logboekregistratie programmatisch met behulp van [Azure Diagnostics gebeurtenisinstellingen en eigenschappen](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="c9f34-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="c9f34-111">Weergave wordt uitgevoerd en geschiedenis van trigger voor uw logische app</span><span class="sxs-lookup"><span data-stu-id="c9f34-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="c9f34-112">toofind uw logische app in Hallo [Azure-portal](https://portal.azure.com), op Hallo van Azure hoofdmenu, kies **meer services**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-112">toofind your logic app in hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **More services**.</span></span> <span data-ttu-id="c9f34-113">In het zoekvak hello, vinden 'logische apps' en kies **Logic apps**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-113">In hello search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Uw logische app zoeken](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="c9f34-115">Hello Azure-portal bevat alle Hallo logic apps die gekoppeld aan uw Azure-abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="c9f34-115">hello Azure portal shows all hello logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="c9f34-116">Selecteer uw logische app, en kies vervolgens **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="c9f34-117">Hello Azure-portal toont de geschiedenis van Hallo wordt uitgevoerd en geschiedenis van trigger voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="c9f34-117">hello Azure portal shows hello runs history and trigger history for your logic app.</span></span> <span data-ttu-id="c9f34-118">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c9f34-118">For example:</span></span>

   ![Logische app geschiedenis en trigger geschiedenis wordt uitgevoerd](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="c9f34-120">**Wordt uitgevoerd geschiedenis** toont alle Hallo uitvoeringen voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="c9f34-120">**Runs history** shows all hello runs for your logic app.</span></span> 
   * <span data-ttu-id="c9f34-121">**Activeren van de geschiedenis** toont alle Hallo triggeractiviteit voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="c9f34-121">**Trigger History** shows all hello trigger activity for your logic app.</span></span>

   <span data-ttu-id="c9f34-122">Zie voor een beschrijving van status [problemen met uw logische app](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="c9f34-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="c9f34-123">Als u niet kunt Hallo-gegevens die u verwacht vinden, op de werkbalk hello, kiest u **vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-123">If you don't find hello data that you expect, on hello toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="c9f34-124">tooview hello stappen van een specifieke uitvoeren onder **wordt uitgevoerd geschiedenis**, selecteren die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9f34-124">tooview hello steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="c9f34-125">Hallo monitor weergave toont elke stap in die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9f34-125">hello monitor view shows each step in that run.</span></span> <span data-ttu-id="c9f34-126">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c9f34-126">For example:</span></span>

   ![Acties voor een specifieke uitvoeren](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="c9f34-128">meer informatie over Hallo uitvoeren, kiest u tooget **Details uitvoering van**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-128">tooget more details about hello run, choose **Run Details**.</span></span> <span data-ttu-id="c9f34-129">Deze informatie bevat een overzicht van stappen hello, status, invoer en uitvoer voor Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9f34-129">This information summarizes hello steps, status, inputs, and outputs for hello run.</span></span> 

   ![Kies 'Details uitvoeren'](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="c9f34-131">Bijvoorbeeld, u krijgt Hallo uitvoeren van **correlatie-ID**, die u mogelijk wanneer u Hallo [REST-API voor Logic Apps](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="c9f34-131">For example, you can get hello run's **Correlation ID**, which you might need when you use hello [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="c9f34-132">details over een specifieke stap tooget kiezen die stap.</span><span class="sxs-lookup"><span data-stu-id="c9f34-132">tooget details about a specific step, choose that step.</span></span> <span data-ttu-id="c9f34-133">U kunt nu gegevens, zoals de invoer, uitvoer en eventuele fouten die hebben plaatsgevonden voor die stap bekijken.</span><span class="sxs-lookup"><span data-stu-id="c9f34-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="c9f34-134">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c9f34-134">For example:</span></span>

   ![Stap-details](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="c9f34-136">Alle details van de runtime en gebeurtenissen zijn gecodeerd binnen Hallo Logic Apps-service.</span><span class="sxs-lookup"><span data-stu-id="c9f34-136">All runtime details and events are encrypted within hello Logic Apps service.</span></span> <span data-ttu-id="c9f34-137">Ze worden alleen wanneer een gebruiker tooview die gegevens aanvraagt ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="c9f34-137">They are decrypted only when a user requests tooview that data.</span></span> <span data-ttu-id="c9f34-138">U kunt ook bepalen toothese toegangsgebeurtenissen met [gebaseerd toegangsbeheer (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="c9f34-138">You can also control access toothese events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="c9f34-139">details over een specifieke triggergebeurtenis tooget terug toohello **overzicht** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="c9f34-139">tooget details about a specific trigger event, go back toohello **Overview** pane.</span></span> <span data-ttu-id="c9f34-140">Onder **activeren geschiedenis**, selecteer Hallo triggergebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="c9f34-140">Under **Trigger history**, select hello trigger event.</span></span> <span data-ttu-id="c9f34-141">U kunt nu gegevens, zoals de invoer en uitvoer, bijvoorbeeld bekijken:</span><span class="sxs-lookup"><span data-stu-id="c9f34-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Gebeurtenisdetails van trigger voor uitvoer](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="c9f34-143">Diagnostische gegevens voor uw logische app logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="c9f34-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="c9f34-144">Voor uitgebreidere foutopsporing met details van de runtime en gebeurtenissen, kunt u zich aanmelden met diagnostische gegevens instellen [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9f34-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="c9f34-145">Log Analytics is een service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) die wordt bewaakt uw cloud en on-premises omgevingen toohelp hun beschikbaarheid en prestaties te behouden.</span><span class="sxs-lookup"><span data-stu-id="c9f34-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments toohelp you maintain their availability and performance.</span></span> 

<span data-ttu-id="c9f34-146">Voordat u begint, moet u toohave een OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="c9f34-146">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="c9f34-147">Meer informatie over [hoe toocreate een OMS-werkruimte](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c9f34-147">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="c9f34-148">In Hallo [Azure-portal](https://portal.azure.com), zoeken en selecteert u uw logische app.</span><span class="sxs-lookup"><span data-stu-id="c9f34-148">In hello [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="c9f34-149">Hallo logic app blade menu onder **bewaking**, kies **Diagnostics** > **diagnostische instellingen**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-149">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Diagnostische instellingen voor tooMonitoring, Diagnostics, gaan](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="c9f34-151">Onder **diagnostische instellingen**, kies **op**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Logboeken met diagnostische gegevens inschakelen](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="c9f34-153">Nu selecteren Hallo OMS werkruimte en gebeurtenis categorie voor logboekregistratie, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="c9f34-153">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="c9f34-154">Selecteer **tooLog Analytics verzenden**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-154">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="c9f34-155">Onder **logboekanalyse**, kies **configureren**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="c9f34-156">Onder **OMS werkruimten**, selecteer Hallo OMS-werkruimte toouse voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="c9f34-156">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="c9f34-157">Onder **logboek**, selecteer Hallo **WorkflowRuntime** categorie.</span><span class="sxs-lookup"><span data-stu-id="c9f34-157">Under **Log**, select hello **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="c9f34-158">Kies metrische hello-interval.</span><span class="sxs-lookup"><span data-stu-id="c9f34-158">Choose hello metric interval.</span></span>
   6. <span data-ttu-id="c9f34-159">Als u bent klaar, kiest u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-159">When you're done, choose **Save**.</span></span>

   ![Selecteer de OMS-werkruimte en de gegevens voor logboekregistratie](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="c9f34-161">U kunt nu gebeurtenissen en andere gegevens zoeken voor trigger-gebeurtenissen, gebeurtenissen en actie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9f34-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="c9f34-162">Zoeken naar gebeurtenissen en gegevens voor uw logische app</span><span class="sxs-lookup"><span data-stu-id="c9f34-162">Find events and data for your logic app</span></span>

<span data-ttu-id="c9f34-163">gebeurtenissen van toofind en weergeven in uw logische app, zoals trigger gebeurtenissen, uitvoeren en gebeurtenissen van de actie, als te werk volgt.</span><span class="sxs-lookup"><span data-stu-id="c9f34-163">toofind and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="c9f34-164">In Hallo [Azure-portal](https://portal.azure.com), kies **meer Services**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-164">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="c9f34-165">Zoek naar 'log analytics' en kies vervolgens **logboekanalyse** als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="c9f34-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Kies 'Log Analytics'](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="c9f34-167">Onder **logboekanalyse**, zoeken en selecteert u de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="c9f34-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selecteer de OMS-werkruimte](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="c9f34-169">Onder **Management**, kies **OMS-Portal**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Kies 'OMS-Portal'](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="c9f34-171">Kies op de startpagina OMS **logboek zoeken**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-171">On your OMS home page, choose **Log Search**.</span></span>

   ![Kies op uw startpagina OMS "Logboek zoeken"](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="c9f34-173">-of-</span><span class="sxs-lookup"><span data-stu-id="c9f34-173">-or-</span></span>

   ![Kies 'Logboek zoeken' hello OMS menu](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="c9f34-175">Geef in het zoekvak hello, een veld dat u wilt dat toofind, en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-175">In hello search box, specify a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="c9f34-176">Wanneer u te typen begint, OMS laat zien u mogelijke overeenkomsten en de bewerkingen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9f34-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="c9f34-177">Bijvoorbeeld toofind Hallo top 10 gebeurtenissen die hebben plaatsgevonden, invoeren en deze zoekopdracht selecteren: **categorie WorkflowRuntime = | top 10**</span><span class="sxs-lookup"><span data-stu-id="c9f34-177">For example, toofind hello top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Geef zoektekenreeks](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="c9f34-179">Meer informatie over [hoe toofind gegevens in logboekanalyse](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="c9f34-179">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="c9f34-180">Kies op Hallo resultatenpagina in de linkerbalk hello, Hallo periode die u tooview wilt.</span><span class="sxs-lookup"><span data-stu-id="c9f34-180">On hello results page, in hello left bar, choose hello timeframe that you want tooview.</span></span>
<span data-ttu-id="c9f34-181">kiest u uw query door een filter toe te voegen toorefine **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-181">toorefine your query by adding a filter, choose **+Add**.</span></span>

   ![Kies tijdskader voor de queryresultaten](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="c9f34-183">Onder **Filters toevoegen**, Voer Hallo filternaam in zodat u de gewenste Hallo-filter kunt vinden.</span><span class="sxs-lookup"><span data-stu-id="c9f34-183">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="c9f34-184">Selecteer Hallo-filter en kies **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-184">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="c9f34-185">In dit voorbeeld gebruikt Hallo word "status" toofind is mislukt-gebeurtenissen onder **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-185">This example uses hello word "status" toofind failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="c9f34-186">Hier Hallo filter voor **status_s** is al geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c9f34-186">Here hello filter for **status_s** is already selected.</span></span>

   ![Selecteer filter](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="c9f34-188">Selecteer in de linkerbalk Hallo Hallo filterwaarde wilt toouse en kies **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-188">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   ![Filterwaarde selecteert, kiest u 'Toepassen'](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="c9f34-190">Nu terug toohello query die u maakt.</span><span class="sxs-lookup"><span data-stu-id="c9f34-190">Now return toohello query that you're building.</span></span> <span data-ttu-id="c9f34-191">De query wordt bijgewerkt met het geselecteerde filter en de waarde.</span><span class="sxs-lookup"><span data-stu-id="c9f34-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="c9f34-192">De resultaten van uw vorige worden nu te gefilterd.</span><span class="sxs-lookup"><span data-stu-id="c9f34-192">Your previous results are now filtered too.</span></span>

   ![Tooyour query met gefilterde resultaten retourneren](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="c9f34-194">uw query voor toekomstig gebruik, kiest u toosave **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9f34-194">toosave your query for future use, choose **Save**.</span></span> <span data-ttu-id="c9f34-195">Meer informatie over [hoe toosave uw query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="c9f34-195">Learn [how toosave your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="c9f34-196">Hoe en waar u diagnostische gegevens gebruikt met andere services uitbreiden</span><span class="sxs-lookup"><span data-stu-id="c9f34-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="c9f34-197">U kunt samen met Azure Log Analytics uitbreiden hoe u diagnostische gegevens van uw logische app gebruiken met andere Azure-services, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c9f34-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="c9f34-198">Archief Azure Diagnostics wordt geregistreerd in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c9f34-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="c9f34-199">Stroom Azure Diagnostics logboeken tooAzure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c9f34-199">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="c9f34-200">U kunt vervolgens get real-time bewaking met Telemetrie en analyses van andere services, zoals [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) en [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="c9f34-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="c9f34-201">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c9f34-201">For example:</span></span>

* [<span data-ttu-id="c9f34-202">Stroomgegevens van Event Hubs tooStream Analytics</span><span class="sxs-lookup"><span data-stu-id="c9f34-202">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="c9f34-203">Streaming gegevens analyseren met Stream Analytics en een realtime analytics-dashboard maken in Power BI</span><span class="sxs-lookup"><span data-stu-id="c9f34-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="c9f34-204">Op basis van het Hallo-opties die u wilt instellen, zorg ervoor dat u eerste [maken van een Azure storage-account](../storage/common/storage-create-storage-account.md) of [maken van een Azure event hub](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="c9f34-204">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="c9f34-205">Selecteer Hallo opties voor het gewenste toosend diagnostische gegevens:</span><span class="sxs-lookup"><span data-stu-id="c9f34-205">Then select hello options for where you want toosend diagnostic data:</span></span>

![Verzenden van gegevens tooAzure storage-account of event hub](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="c9f34-207">Bewaarperiode alleen van toepassing wanneer u een opslagaccount toouse kiezen.</span><span class="sxs-lookup"><span data-stu-id="c9f34-207">Retention periods apply only when you choose toouse a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="c9f34-208">Waarschuwingen voor uw logische app instellen</span><span class="sxs-lookup"><span data-stu-id="c9f34-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="c9f34-209">specifieke metrische gegevens toomonitor of overschreden drempelwaarden voor uw logische app ingesteld [waarschuwingen in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="c9f34-209">toomonitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="c9f34-210">Meer informatie over [metrische gegevens in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c9f34-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="c9f34-211">tooset van waarschuwingen zonder [Azure Log Analytics](../log-analytics/log-analytics-overview.md), als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="c9f34-211">tooset up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="c9f34-212">Voor meer geavanceerde criteria voor waarschuwingen en acties, [logboekanalyse instellen](#azure-diagnostics) te.</span><span class="sxs-lookup"><span data-stu-id="c9f34-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="c9f34-213">Hallo logic app blade menu onder **bewaking**, kies **Diagnostics** > **waarschuwing regels** > **waarschuwing toevoegen**als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="c9f34-213">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Een waarschuwing voor uw logische app toevoegen](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="c9f34-215">Op Hallo **een waarschuwingsregel toevoegen** blade maken van de waarschuwing, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="c9f34-215">On hello **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="c9f34-216">Onder **Resource**, selecteer uw logische app, als dat niet is gebeurd.</span><span class="sxs-lookup"><span data-stu-id="c9f34-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="c9f34-217">Geef een naam en beschrijving voor de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="c9f34-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="c9f34-218">Selecteer een **metriek** of gebeurtenis die u tootrack wilt.</span><span class="sxs-lookup"><span data-stu-id="c9f34-218">Select a **Metric** or event that you want tootrack.</span></span>
   4. <span data-ttu-id="c9f34-219">Selecteer een **voorwaarde**, Geef een **drempelwaarde** voor Hallo metriek, en selecteer Hallo **periode** voor het bewaken van deze metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="c9f34-219">Select a **Condition**, specify a **Threshold** for hello metric, and select hello **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="c9f34-220">Selecteer of e-toosend voor Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="c9f34-220">Select whether toosend mail for hello alert.</span></span> 
   6. <span data-ttu-id="c9f34-221">Geef een andere e-mailadressen voor het verzenden van Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="c9f34-221">Specify any other email addresses for sending hello alert.</span></span> 
   <span data-ttu-id="c9f34-222">U kunt ook een waar u toosend Hallo waarschuwing webhook-URL opgeven.</span><span class="sxs-lookup"><span data-stu-id="c9f34-222">You can also specify a webhook URL where you want toosend hello alert.</span></span>

   <span data-ttu-id="c9f34-223">Bijvoorbeeld: met deze regel verzendt een waarschuwing wanneer vijf of meer wordt uitgevoerd in een uur mislukken:</span><span class="sxs-lookup"><span data-stu-id="c9f34-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Metrische waarschuwingsregel maken](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="c9f34-225">een logische app toorun vanuit een waarschuwing, kunt u Hallo opnemen [aanvraag trigger](../connectors/connectors-native-reqres.md) in uw werkstroom waarmee u taken, zoals deze voorbeelden uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c9f34-225">toorun a logic app from an alert, you can include hello [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="c9f34-226">Post tooSlack</span><span class="sxs-lookup"><span data-stu-id="c9f34-226">Post tooSlack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="c9f34-227">Een tekst verzenden</span><span class="sxs-lookup"><span data-stu-id="c9f34-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="c9f34-228">Een berichtenwachtrij tooa toevoegen</span><span class="sxs-lookup"><span data-stu-id="c9f34-228">Add a message tooa queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="c9f34-229">Instellingen van Azure Diagnostics-gebeurtenis en details</span><span class="sxs-lookup"><span data-stu-id="c9f34-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="c9f34-230">Elke diagnostische gebeurtenissen voor details over uw logische app en dat de gebeurtenis, bijvoorbeeld Hallo status heeft, begintijd, eindtijd en enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c9f34-230">Each diagnostic event has details about your logic app and that event, for example, hello status, start time, end time, and so on.</span></span> <span data-ttu-id="c9f34-231">tooprogrammatically bewaking, bijhouden en logboekregistratie instellen, organisatie-eenheid kunt gebruiken deze gegevens met Hallo [REST-API voor Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) en Hallo [REST-API voor Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="c9f34-231">tooprogrammatically set up monitoring, tracking, and logging, ou can use these details with hello [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and hello [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="c9f34-232">Bijvoorbeeld, Hallo `ActionCompleted` gebeurtenis heeft Hallo `clientTrackingId` en `trackedProperties` eigenschappen die u gebruiken kunt voor bewaking en bij te houden:</span><span class="sxs-lookup"><span data-stu-id="c9f34-232">For example, hello `ActionCompleted` event has hello `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="c9f34-233">`clientTrackingId`: Als dat niet het opgegeven Azure automatisch deze ID wordt gegenereerd en gebeurtenissen via een logische app uitgevoerd verbindt, inclusief alle geneste werkstromen die worden aangeroepen vanuit Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="c9f34-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from hello logic app.</span></span> <span data-ttu-id="c9f34-234">U kunt deze ID van een trigger handmatig opgeven door een `x-ms-client-tracking-id` header met uw aangepaste id-waarde in de aanvraag van de trigger Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9f34-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in hello trigger request.</span></span> <span data-ttu-id="c9f34-235">U kunt een aanvraag trigger, HTTP-trigger of webhook trigger.</span><span class="sxs-lookup"><span data-stu-id="c9f34-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="c9f34-236">`trackedProperties`: tootrack in- of uitgangen in diagnostics-gegevens, kunt u tooactions bijgehouden eigenschappen in uw logische app JSON-definitie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c9f34-236">`trackedProperties`: tootrack inputs or outputs in diagnostics data, you can add tracked properties tooactions in your logic app's JSON definition.</span></span> <span data-ttu-id="c9f34-237">Bijgehouden eigenschappen kunnen volgen slechts één actie in- en uitgangen, maar u kunt Hallo `correlation` eigenschappen van gebeurtenissen toocorrelate over acties in een uitvoering.</span><span class="sxs-lookup"><span data-stu-id="c9f34-237">Tracked properties can track only a single action's inputs and outputs, but you can use hello `correlation` properties of events toocorrelate across actions in a run.</span></span>

  <span data-ttu-id="c9f34-238">tootrack een of meer eigenschappen toevoegen Hallo `trackedProperties` sectie en Hallo gewenste toohello actie definitie eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c9f34-238">tootrack one or more properties, add hello `trackedProperties` section and hello properties you want toohello action definition.</span></span> <span data-ttu-id="c9f34-239">Stel bijvoorbeeld dat u wilt tootrack gegevens, zoals een 'volgorde-ID' in uw telemetrie:</span><span class="sxs-lookup"><span data-stu-id="c9f34-239">For example, suppose you want tootrack data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="c9f34-240">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9f34-240">Next steps</span></span>

* [<span data-ttu-id="c9f34-241">Sjablonen maken voor logic app-implementatie en releasebeheer</span><span class="sxs-lookup"><span data-stu-id="c9f34-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="c9f34-242">B2B-scenario's met Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="c9f34-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="c9f34-243">B2B-berichten bewaken</span><span class="sxs-lookup"><span data-stu-id="c9f34-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)