---
title: Controleer de status, logboekregistratie instellen en ontvang waarschuwingen - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 4795f5728d4ce6ff21b97bc3fefd6a53e0c6a11b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="77a02-103">Status controleren, instellen van logboekregistratie van diagnostische gegevens en waarschuwingen inschakelen voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="77a02-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="77a02-104">Nadat u [maken en uitvoeren van een logische app](../logic-apps/logic-apps-create-a-logic-app.md), u kunt de geschiedenis wordt uitgevoerd, trigger geschiedenis, status en prestaties controleren.</span><span class="sxs-lookup"><span data-stu-id="77a02-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="77a02-105">Instellen voor het bewaken van realtime-gebeurtenissen en uitgebreidere foutopsporing, [logboekregistratie van diagnostische gegevens](#azure-diagnostics) voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="77a02-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="77a02-106">Op die manier kunt u [zoeken en weergeven van gebeurtenissen](#find-events), zoals de trigger-gebeurtenissen, voer gebeurtenissen en in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="77a02-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="77a02-107">U kunt dit ook gebruiken [diagnostics-gegevens met andere services](#extend-diagnostic-data), zoals Azure Storage en Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="77a02-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="77a02-108">Als u meldingen over fouten of andere mogelijke problemen, instellen van [waarschuwingen](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="77a02-108">To get notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="77a02-109">Bijvoorbeeld, kunt u een waarschuwing die detecteert 'wanneer meer dan vijf wordt uitgevoerd niet in een uur."</span><span class="sxs-lookup"><span data-stu-id="77a02-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="77a02-110">U kunt ook instellen bewaking, bijhouden en logboekregistratie programmatisch met behulp van [Azure Diagnostics gebeurtenisinstellingen en eigenschappen](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="77a02-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="77a02-111">Weergave wordt uitgevoerd en geschiedenis van trigger voor uw logische app</span><span class="sxs-lookup"><span data-stu-id="77a02-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="77a02-112">Vinden van uw logische app in de [Azure-portal](https://portal.azure.com), kiest u in het Azure hoofdmenu **meer services**.</span><span class="sxs-lookup"><span data-stu-id="77a02-112">To find your logic app in the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **More services**.</span></span> <span data-ttu-id="77a02-113">In het zoekvak 'logische apps' vinden en kies **Logic apps**.</span><span class="sxs-lookup"><span data-stu-id="77a02-113">In the search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Uw logische app zoeken](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="77a02-115">De Azure-portal bevat alle logic-apps die gekoppeld aan uw Azure-abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="77a02-115">The Azure portal shows all the logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="77a02-116">Selecteer uw logische app, en kies vervolgens **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="77a02-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="77a02-117">De Azure-portal ziet u de geschiedenis wordt uitgevoerd en de geschiedenis van trigger voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="77a02-117">The Azure portal shows the runs history and trigger history for your logic app.</span></span> <span data-ttu-id="77a02-118">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="77a02-118">For example:</span></span>

   ![Logische app geschiedenis en trigger geschiedenis wordt uitgevoerd](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="77a02-120">**Wordt uitgevoerd geschiedenis** toont de uitvoert voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="77a02-120">**Runs history** shows all the runs for your logic app.</span></span> 
   * <span data-ttu-id="77a02-121">**Activeren van de geschiedenis** ziet u de triggeractiviteit voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="77a02-121">**Trigger History** shows all the trigger activity for your logic app.</span></span>

   <span data-ttu-id="77a02-122">Zie voor een beschrijving van status [problemen met uw logische app](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="77a02-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="77a02-123">Als u de gegevens die u, op de werkbalk verwacht niet kunt vinden kiezen **vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="77a02-123">If you don't find the data that you expect, on the toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="77a02-124">Om weer te geven van de stappen van een specifieke uitvoeren onder **wordt uitgevoerd geschiedenis**, selecteren die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="77a02-124">To view the steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="77a02-125">De weergave van de monitor geeft elke stap in die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="77a02-125">The monitor view shows each step in that run.</span></span> <span data-ttu-id="77a02-126">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="77a02-126">For example:</span></span>

   ![Acties voor een specifieke uitvoeren](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="77a02-128">Voor meer informatie over het uitvoeren, kiest u **Details uitvoering van**.</span><span class="sxs-lookup"><span data-stu-id="77a02-128">To get more details about the run, choose **Run Details**.</span></span> <span data-ttu-id="77a02-129">Deze informatie bevat een overzicht van de stappen, status, invoer en uitvoer voor de verwerking.</span><span class="sxs-lookup"><span data-stu-id="77a02-129">This information summarizes the steps, status, inputs, and outputs for the run.</span></span> 

   ![Kies 'Details uitvoeren'](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="77a02-131">Bijvoorbeeld, krijgt u de run **correlatie-ID**, die u mogelijk wanneer u de [REST-API voor Logic Apps](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="77a02-131">For example, you can get the run's **Correlation ID**, which you might need when you use the [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="77a02-132">Als u meer informatie over een specifieke stap, kiest u die stap.</span><span class="sxs-lookup"><span data-stu-id="77a02-132">To get details about a specific step, choose that step.</span></span> <span data-ttu-id="77a02-133">U kunt nu gegevens, zoals de invoer, uitvoer en eventuele fouten die hebben plaatsgevonden voor die stap bekijken.</span><span class="sxs-lookup"><span data-stu-id="77a02-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="77a02-134">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="77a02-134">For example:</span></span>

   ![Stap-details](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="77a02-136">Alle details van de runtime en gebeurtenissen worden in de service Logic Apps versleuteld.</span><span class="sxs-lookup"><span data-stu-id="77a02-136">All runtime details and events are encrypted within the Logic Apps service.</span></span> <span data-ttu-id="77a02-137">Ze worden alleen als een gebruiker vraagt om weer te geven dat de gegevens ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="77a02-137">They are decrypted only when a user requests to view that data.</span></span> <span data-ttu-id="77a02-138">U kunt ook toegang tot deze gebeurtenissen met [gebaseerd toegangsbeheer (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="77a02-138">You can also control access to these events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="77a02-139">Als u meer informatie over een specifieke triggergebeurtenis, gaat u terug naar de **overzicht** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="77a02-139">To get details about a specific trigger event, go back to the **Overview** pane.</span></span> <span data-ttu-id="77a02-140">Onder **activeren geschiedenis**, selecteert u de triggergebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="77a02-140">Under **Trigger history**, select the trigger event.</span></span> <span data-ttu-id="77a02-141">U kunt nu gegevens, zoals de invoer en uitvoer, bijvoorbeeld bekijken:</span><span class="sxs-lookup"><span data-stu-id="77a02-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Gebeurtenisdetails van trigger voor uitvoer](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="77a02-143">Diagnostische gegevens voor uw logische app logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="77a02-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="77a02-144">Voor uitgebreidere foutopsporing met details van de runtime en gebeurtenissen, kunt u zich aanmelden met diagnostische gegevens instellen [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77a02-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="77a02-145">Log Analytics is een service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) die wordt bewaakt uw cloud en on-premises omgevingen om te helpen uw behouden hun beschikbaarheid en prestaties.</span><span class="sxs-lookup"><span data-stu-id="77a02-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments to help you maintain their availability and performance.</span></span> 

<span data-ttu-id="77a02-146">Voordat u begint, moet u een OMS-werkruimte hebt.</span><span class="sxs-lookup"><span data-stu-id="77a02-146">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="77a02-147">Meer informatie over [het maken van een OMS-werkruimte](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="77a02-147">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="77a02-148">In de [Azure-portal](https://portal.azure.com), zoeken en selecteert u uw logische app.</span><span class="sxs-lookup"><span data-stu-id="77a02-148">In the [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="77a02-149">Klik in het menu logic app blade onder **bewaking**, kies **Diagnostics** > **diagnostische instellingen**.</span><span class="sxs-lookup"><span data-stu-id="77a02-149">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Ga naar de bewakings-, diagnose, diagnostische instellingen](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="77a02-151">Onder **diagnostische instellingen**, kies **op**.</span><span class="sxs-lookup"><span data-stu-id="77a02-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Logboeken met diagnostische gegevens inschakelen](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="77a02-153">Selecteer de OMS-werkruimte en gebeurtenis categorie voor logboekregistratie nu zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="77a02-153">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="77a02-154">Selecteer **verzenden met logboekanalyse**.</span><span class="sxs-lookup"><span data-stu-id="77a02-154">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="77a02-155">Onder **logboekanalyse**, kies **configureren**.</span><span class="sxs-lookup"><span data-stu-id="77a02-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="77a02-156">Onder **OMS werkruimten**, selecteer de OMS-werkruimte moet worden gebruikt voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="77a02-156">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="77a02-157">Onder **logboek**, selecteer de **WorkflowRuntime** categorie.</span><span class="sxs-lookup"><span data-stu-id="77a02-157">Under **Log**, select the **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="77a02-158">Kies een metrische interval.</span><span class="sxs-lookup"><span data-stu-id="77a02-158">Choose the metric interval.</span></span>
   6. <span data-ttu-id="77a02-159">Als u bent klaar, kiest u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="77a02-159">When you're done, choose **Save**.</span></span>

   ![Selecteer de OMS-werkruimte en de gegevens voor logboekregistratie](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="77a02-161">U kunt nu gebeurtenissen en andere gegevens zoeken voor trigger-gebeurtenissen, gebeurtenissen en actie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="77a02-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="77a02-162">Zoeken naar gebeurtenissen en gegevens voor uw logische app</span><span class="sxs-lookup"><span data-stu-id="77a02-162">Find events and data for your logic app</span></span>

<span data-ttu-id="77a02-163">Om te zoeken en weergeven van gebeurtenissen in uw logische app, zoals gebeurtenissen, gebeurtenissen, uitvoeren en actie activeren, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="77a02-163">To find and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="77a02-164">In de [Azure-portal](https://portal.azure.com), kies **meer Services**.</span><span class="sxs-lookup"><span data-stu-id="77a02-164">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="77a02-165">Zoek naar 'log analytics' en kies vervolgens **logboekanalyse** als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="77a02-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Kies 'Log Analytics'](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="77a02-167">Onder **logboekanalyse**, zoeken en selecteert u de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="77a02-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selecteer de OMS-werkruimte](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="77a02-169">Onder **Management**, kies **OMS-Portal**.</span><span class="sxs-lookup"><span data-stu-id="77a02-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Kies 'OMS-Portal'](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="77a02-171">Kies op de startpagina OMS **logboek zoeken**.</span><span class="sxs-lookup"><span data-stu-id="77a02-171">On your OMS home page, choose **Log Search**.</span></span>

   ![Kies op uw startpagina OMS "Logboek zoeken"](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="77a02-173">-of-</span><span class="sxs-lookup"><span data-stu-id="77a02-173">-or-</span></span>

   ![Kies in het menu OMS "Logboek zoeken"](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="77a02-175">Geef in het zoekvak, een veld dat u wilt zoeken en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77a02-175">In the search box, specify a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="77a02-176">Wanneer u te typen begint, OMS laat zien u mogelijke overeenkomsten en de bewerkingen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="77a02-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="77a02-177">Bijvoorbeeld als u zoekt de top 10-gebeurtenissen die hebben plaatsgevonden, invoeren en deze zoekopdracht selecteren: **categorie WorkflowRuntime = | top 10**</span><span class="sxs-lookup"><span data-stu-id="77a02-177">For example, to find the top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Geef zoektekenreeks](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="77a02-179">Meer informatie over [hoe u gegevens wilt zoeken in logboekanalyse](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="77a02-179">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="77a02-180">Kies de periode die u wilt weergeven in de linkerbalk op de resultatenpagina.</span><span class="sxs-lookup"><span data-stu-id="77a02-180">On the results page, in the left bar, choose the timeframe that you want to view.</span></span>
<span data-ttu-id="77a02-181">Als u wilt uw query te verfijnen door een filter toe te voegen, kies **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="77a02-181">To refine your query by adding a filter, choose **+Add**.</span></span>

   ![Kies tijdskader voor de queryresultaten](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="77a02-183">Onder **Filters toevoegen**, voer de naam van het filter zodat u kunt het filter dat u wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="77a02-183">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="77a02-184">Selecteer het filter en kies **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="77a02-184">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="77a02-185">In dit voorbeeld wordt het woord 'status' mislukt-gebeurtenissen onder vinden **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="77a02-185">This example uses the word "status" to find failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="77a02-186">Hier het filter voor **status_s** is al geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="77a02-186">Here the filter for **status_s** is already selected.</span></span>

   ![Selecteer filter](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="77a02-188">Selecteer de filterwaarde die u wilt gebruiken en kies in de linkerbalk **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="77a02-188">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   ![Filterwaarde selecteert, kiest u 'Toepassen'](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="77a02-190">Nu kunt u terugkeren naar de query die u maakt.</span><span class="sxs-lookup"><span data-stu-id="77a02-190">Now return to the query that you're building.</span></span> <span data-ttu-id="77a02-191">De query wordt bijgewerkt met het geselecteerde filter en de waarde.</span><span class="sxs-lookup"><span data-stu-id="77a02-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="77a02-192">De resultaten van uw vorige worden nu te gefilterd.</span><span class="sxs-lookup"><span data-stu-id="77a02-192">Your previous results are now filtered too.</span></span>

   ![Ga terug naar uw query met gefilterde resultaten](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="77a02-194">Sla de query voor toekomstig gebruik, kies **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="77a02-194">To save your query for future use, choose **Save**.</span></span> <span data-ttu-id="77a02-195">Meer informatie over [het opslaan van uw query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="77a02-195">Learn [how to save your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="77a02-196">Hoe en waar u diagnostische gegevens gebruikt met andere services uitbreiden</span><span class="sxs-lookup"><span data-stu-id="77a02-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="77a02-197">U kunt samen met Azure Log Analytics uitbreiden hoe u diagnostische gegevens van uw logische app gebruiken met andere Azure-services, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="77a02-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="77a02-198">Archief Azure Diagnostics wordt geregistreerd in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="77a02-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="77a02-199">Azure Diagnostics logboeken naar Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="77a02-199">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="77a02-200">U kunt vervolgens get real-time bewaking met Telemetrie en analyses van andere services, zoals [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) en [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="77a02-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="77a02-201">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="77a02-201">For example:</span></span>

* [<span data-ttu-id="77a02-202">Stroomgegevens uit Event Hubs met Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="77a02-202">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="77a02-203">Streaming gegevens analyseren met Stream Analytics en een realtime analytics-dashboard maken in Power BI</span><span class="sxs-lookup"><span data-stu-id="77a02-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="77a02-204">Op basis van de opties die u wilt instellen, zorg ervoor dat u eerste [maken van een Azure storage-account](../storage/common/storage-create-storage-account.md) of [maken van een Azure event hub](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="77a02-204">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="77a02-205">Selecteer de opties voor waar u diagnostische gegevens verzenden:</span><span class="sxs-lookup"><span data-stu-id="77a02-205">Then select the options for where you want to send diagnostic data:</span></span>

![Gegevens verzenden naar Azure storage-account of event hub](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="77a02-207">Bewaarperiode gelden alleen wanneer u kiest voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="77a02-207">Retention periods apply only when you choose to use a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="77a02-208">Waarschuwingen voor uw logische app instellen</span><span class="sxs-lookup"><span data-stu-id="77a02-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="77a02-209">Instellen voor het bewaken van specifieke metrische gegevens of overschreden drempelwaarden voor uw logische app [waarschuwingen in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="77a02-209">To monitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="77a02-210">Meer informatie over [metrische gegevens in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="77a02-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="77a02-211">Voor het instellen van waarschuwingen zonder [Azure Log Analytics](../log-analytics/log-analytics-overview.md), als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="77a02-211">To set up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="77a02-212">Voor meer geavanceerde criteria voor waarschuwingen en acties, [logboekanalyse instellen](#azure-diagnostics) te.</span><span class="sxs-lookup"><span data-stu-id="77a02-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="77a02-213">In het menu logic app blade onder **bewaking**, kies **Diagnostics** > **waarschuwing regels** > **waarschuwing toevoegen** als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="77a02-213">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Een waarschuwing voor uw logische app toevoegen](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="77a02-215">Op de **een waarschuwingsregel toevoegen** blade maken van de waarschuwing, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="77a02-215">On the **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="77a02-216">Onder **Resource**, selecteer uw logische app, als dat niet is gebeurd.</span><span class="sxs-lookup"><span data-stu-id="77a02-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="77a02-217">Geef een naam en beschrijving voor de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="77a02-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="77a02-218">Selecteer een **metriek** of gebeurtenis die u wilt traceren.</span><span class="sxs-lookup"><span data-stu-id="77a02-218">Select a **Metric** or event that you want to track.</span></span>
   4. <span data-ttu-id="77a02-219">Selecteer een **voorwaarde**, Geef een **drempelwaarde** voor de metriek, en selecteer de **periode** voor het bewaken van deze metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="77a02-219">Select a **Condition**, specify a **Threshold** for the metric, and select the **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="77a02-220">Geef aan of e-mail voor de waarschuwing te verzenden.</span><span class="sxs-lookup"><span data-stu-id="77a02-220">Select whether to send mail for the alert.</span></span> 
   6. <span data-ttu-id="77a02-221">Geef een andere e-mailadressen voor het verzenden van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="77a02-221">Specify any other email addresses for sending the alert.</span></span> 
   <span data-ttu-id="77a02-222">U kunt ook opgeven van een webhook-URL waarvoor de waarschuwing te verzenden.</span><span class="sxs-lookup"><span data-stu-id="77a02-222">You can also specify a webhook URL where you want to send the alert.</span></span>

   <span data-ttu-id="77a02-223">Bijvoorbeeld: met deze regel verzendt een waarschuwing wanneer vijf of meer wordt uitgevoerd in een uur mislukken:</span><span class="sxs-lookup"><span data-stu-id="77a02-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Metrische waarschuwingsregel maken](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="77a02-225">Voor een logische app uitvoeren vanaf een waarschuwing, u kunt opnemen de [aanvraag trigger](../connectors/connectors-native-reqres.md) in uw werkstroom waarmee u taken, zoals deze voorbeelden uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="77a02-225">To run a logic app from an alert, you can include the [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="77a02-226">Boeken naar ongebruikt</span><span class="sxs-lookup"><span data-stu-id="77a02-226">Post to Slack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="77a02-227">Een tekst verzenden</span><span class="sxs-lookup"><span data-stu-id="77a02-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="77a02-228">Een bericht toevoegen aan een wachtrij</span><span class="sxs-lookup"><span data-stu-id="77a02-228">Add a message to a queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="77a02-229">Instellingen van Azure Diagnostics-gebeurtenis en details</span><span class="sxs-lookup"><span data-stu-id="77a02-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="77a02-230">Elke diagnostische gebeurtenissen voor meer informatie over uw logische app en dat de gebeurtenis, bijvoorbeeld de status heeft, begintijd, eindtijd en enzovoort.</span><span class="sxs-lookup"><span data-stu-id="77a02-230">Each diagnostic event has details about your logic app and that event, for example, the status, start time, end time, and so on.</span></span> <span data-ttu-id="77a02-231">Als u bewaking, bijhouden en logboekregistratie programmatisch instelt, kunt organisatie-eenheid deze details met de [REST-API voor Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) en de [REST-API voor Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="77a02-231">To programmatically set up monitoring, tracking, and logging, ou can use these details with the [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and the [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="77a02-232">Bijvoorbeeld, de `ActionCompleted` gebeurtenis heeft de `clientTrackingId` en `trackedProperties` eigenschappen die u gebruiken kunt voor bewaking en bij te houden:</span><span class="sxs-lookup"><span data-stu-id="77a02-232">For example, the `ActionCompleted` event has the `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

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

* <span data-ttu-id="77a02-233">`clientTrackingId`: Als dat niet het opgegeven Azure automatisch deze ID wordt gegenereerd en gebeurtenissen via een logische app uitgevoerd verbindt, inclusief alle geneste werkstromen die worden aangeroepen vanuit de logische app.</span><span class="sxs-lookup"><span data-stu-id="77a02-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from the logic app.</span></span> <span data-ttu-id="77a02-234">U kunt deze ID van een trigger handmatig opgeven door een `x-ms-client-tracking-id` header met uw aangepaste id-waarde in de aanvraag van de trigger.</span><span class="sxs-lookup"><span data-stu-id="77a02-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in the trigger request.</span></span> <span data-ttu-id="77a02-235">U kunt een aanvraag trigger, HTTP-trigger of webhook trigger.</span><span class="sxs-lookup"><span data-stu-id="77a02-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="77a02-236">`trackedProperties`: Als u wilt in- of uitgangen in diagnostische gegevens bijhouden, kunt u bijgehouden eigenschappen toevoegen aan de acties in uw logische app JSON-definitie.</span><span class="sxs-lookup"><span data-stu-id="77a02-236">`trackedProperties`: To track inputs or outputs in diagnostics data, you can add tracked properties to actions in your logic app's JSON definition.</span></span> <span data-ttu-id="77a02-237">Bijgehouden eigenschappen kunnen volgen slechts één actie in- en uitgangen, maar u kunt de `correlation` eigenschappen van gebeurtenissen die correleren over acties in een uitvoering.</span><span class="sxs-lookup"><span data-stu-id="77a02-237">Tracked properties can track only a single action's inputs and outputs, but you can use the `correlation` properties of events to correlate across actions in a run.</span></span>

  <span data-ttu-id="77a02-238">Om bij te houden op een of meer eigenschappen, voeg de `trackedProperties` sectie en de eigenschappen die u de definitie van de actie wilt.</span><span class="sxs-lookup"><span data-stu-id="77a02-238">To track one or more properties, add the `trackedProperties` section and the properties you want to the action definition.</span></span> <span data-ttu-id="77a02-239">Stel bijvoorbeeld dat u wilt bijhouden van gegevens, zoals een 'volgorde-ID' in uw telemetrie:</span><span class="sxs-lookup"><span data-stu-id="77a02-239">For example, suppose you want to track data like an "order ID" in your telemetry:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="77a02-240">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="77a02-240">Next steps</span></span>

* [<span data-ttu-id="77a02-241">Sjablonen maken voor logic app-implementatie en releasebeheer</span><span class="sxs-lookup"><span data-stu-id="77a02-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="77a02-242">B2B-scenario's met Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="77a02-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="77a02-243">B2B-berichten bewaken</span><span class="sxs-lookup"><span data-stu-id="77a02-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)