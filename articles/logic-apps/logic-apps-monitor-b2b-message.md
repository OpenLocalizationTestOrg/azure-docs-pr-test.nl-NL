---
title: aaaMonitor B2B-transacties en logboekregistratie - Azure Logic Apps instellen | Microsoft Docs
description: Monitor AS2, X 12 en EDIFACT berichten, start logboekregistratie van diagnostische gegevens voor uw account integratie
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
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="9c442-103">Bewaken en het instellen van logboekregistratie van diagnostische gegevens voor B2B-communicatie in integratieaccounts</span><span class="sxs-lookup"><span data-stu-id="9c442-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="9c442-104">Na het instellen van B2B-communicatie tussen twee bedrijfsprocessen of toepassingen via uw account integratie met deze entiteiten berichten met elkaar kunnen uitwisselen.</span><span class="sxs-lookup"><span data-stu-id="9c442-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="9c442-105">tooconfirm deze communicatie werkt zoals verwacht, kunt u instellen voor AS2, X12, bewaking en EDIFACT berichten, samen met de logboekregistratie van diagnostische gegevens voor uw account integratie via Hallo [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="9c442-105">tooconfirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="9c442-106">Deze service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) bewaakt uw cloud en on-premises omgevingen, zodat u kunt de beschikbaarheid en prestaties, onderhouden en verzamelt ook details van de runtime en gebeurtenissen voor uitgebreidere foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="9c442-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="9c442-107">U kunt ook [uw diagnostische gegevens met andere services gebruiken](#extend-diagnostic-data), zoals Azure Storage en Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="9c442-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="9c442-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9c442-108">Requirements</span></span>

* <span data-ttu-id="9c442-109">Een logische app die ingesteld met de logboekregistratie van diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="9c442-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="9c442-110">Meer informatie over [hoe tooset logboekregistratie voor die app logica van](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="9c442-110">Learn [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="9c442-111">Nadat u hebt deze vereiste voldaan, moet u een werkruimte in Hallo hebben [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c442-111">After you've met this requirement, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="9c442-112">Moet u dezelfde OMS-werkruimte Hallo bij het instellen van logboekregistratie voor uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="9c442-112">You should use hello same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="9c442-113">Als u een OMS-werkruimte niet hebt, ontdek [hoe toocreate een OMS-werkruimte](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9c442-113">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="9c442-114">Een integratie-account dat is gekoppeld tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="9c442-114">An integration account that's linked tooyour logic app.</span></span> <span data-ttu-id="9c442-115">Meer informatie over [hoe toocreate een integratie met een koppeling tooyour logische app account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="9c442-115">Learn [how toocreate an integration account with a link tooyour logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="9c442-116">Diagnostische gegevens voor uw account integratie logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="9c442-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="9c442-117">U kunt rechtstreeks vanaf uw account integratie logboekregistratie inschakelen of [via hello Azure-controleservice](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="9c442-117">You can turn on logging either directly from your integration account or [through hello Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="9c442-118">Azure biedt een eenvoudige bewaking met niveau van de infrastructuur-gegevens.</span><span class="sxs-lookup"><span data-stu-id="9c442-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="9c442-119">Meer informatie over [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="9c442-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="9c442-120">Diagnostische gegevens rechtstreeks vanuit uw account integratie logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="9c442-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="9c442-121">In Hallo [Azure-portal](https://portal.azure.com), zoeken en selecteert u uw integratie-account.</span><span class="sxs-lookup"><span data-stu-id="9c442-121">In hello [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="9c442-122">Onder **bewaking**, kies **diagnostische logboeken** als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="9c442-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Zoeken en selecteert u uw account integratie, kiest u 'Diagnostische logboeken'](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="9c442-124">Nadat u uw integratie-account hebt geselecteerd, worden volgende waarden Hallo automatisch geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9c442-124">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="9c442-125">Als deze waarden correct zijn, kiest u **diagnostische gegevens inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="9c442-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="9c442-126">Selecteer anders Hallo-waarden die u wilt:</span><span class="sxs-lookup"><span data-stu-id="9c442-126">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="9c442-127">Onder **abonnement**, selecteer hello Azure-abonnement dat u met uw integratie-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9c442-127">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="9c442-128">Onder **resourcegroep**, selecteer Hallo resourcegroep die u met uw account integratie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9c442-128">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="9c442-129">Onder **brontype**, selecteer **integratieaccounts**.</span><span class="sxs-lookup"><span data-stu-id="9c442-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="9c442-130">Onder **Resource**, selecteert u uw integratie-account.</span><span class="sxs-lookup"><span data-stu-id="9c442-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="9c442-131">Kies **diagnostische gegevens inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="9c442-131">Choose **Turn on diagnostics**.</span></span>

   ![Diagnostische gegevens voor uw account integratie instellen](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="9c442-133">Onder **diagnostische instellingen**, en vervolgens **Status**, kies **op**.</span><span class="sxs-lookup"><span data-stu-id="9c442-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Azure diagnostische gegevens inschakelen](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="9c442-135">Nu selecteren Hallo OMS-werkruimte en gegevens toouse voor logboekregistratie, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9c442-135">Now select hello OMS workspace and data toouse for logging as shown:</span></span>

   1. <span data-ttu-id="9c442-136">Selecteer **tooLog Analytics verzenden**.</span><span class="sxs-lookup"><span data-stu-id="9c442-136">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="9c442-137">Onder **logboekanalyse**, kies **configureren**.</span><span class="sxs-lookup"><span data-stu-id="9c442-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="9c442-138">Onder **OMS werkruimten**, selecteer Hallo OMS-werkruimte toouse voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="9c442-138">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="9c442-139">Onder **logboek**, selecteer Hallo **IntegrationAccountTrackingEvents** categorie.</span><span class="sxs-lookup"><span data-stu-id="9c442-139">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="9c442-140">Kies **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9c442-140">Choose **Save**.</span></span>

   ![Log Analytics instellen zodat u kunt diagnostische gegevens tooa logboek verzenden](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="9c442-142">Nu [bijhouden voor uw B2B-berichten in OMS instellen](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="9c442-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="9c442-143">Inschakelen van logboekregistratie van diagnostische gegevens via de Azure-Monitor</span><span class="sxs-lookup"><span data-stu-id="9c442-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="9c442-144">In Hallo [Azure-portal](https://portal.azure.com), op Hallo van Azure hoofdmenu, kies **Monitor**, **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="9c442-144">In hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="9c442-145">Selecteer vervolgens uw account integratie als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="9c442-145">Then select your integration account as shown here:</span></span>

   ![Kies 'Bewaken', 'Diagnostische logboeken', selecteert u uw integratie-account](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="9c442-147">Nadat u uw integratie-account hebt geselecteerd, worden volgende waarden Hallo automatisch geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9c442-147">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="9c442-148">Als deze waarden correct zijn, kiest u **diagnostische gegevens inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="9c442-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="9c442-149">Selecteer anders Hallo-waarden die u wilt:</span><span class="sxs-lookup"><span data-stu-id="9c442-149">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="9c442-150">Onder **abonnement**, selecteer hello Azure-abonnement dat u met uw integratie-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9c442-150">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="9c442-151">Onder **resourcegroep**, selecteer Hallo resourcegroep die u met uw account integratie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9c442-151">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="9c442-152">Onder **brontype**, selecteer **integratieaccounts**.</span><span class="sxs-lookup"><span data-stu-id="9c442-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="9c442-153">Onder **Resource**, selecteert u uw integratie-account.</span><span class="sxs-lookup"><span data-stu-id="9c442-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="9c442-154">Kies **diagnostische gegevens inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="9c442-154">Choose **Turn on diagnostics**.</span></span>

   ![Diagnostische gegevens voor uw account integratie instellen](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="9c442-156">Onder **diagnostische instellingen**, kies **op**.</span><span class="sxs-lookup"><span data-stu-id="9c442-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Azure diagnostische gegevens inschakelen](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="9c442-158">Nu selecteren Hallo OMS werkruimte en gebeurtenis categorie voor logboekregistratie, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9c442-158">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="9c442-159">Selecteer **tooLog Analytics verzenden**.</span><span class="sxs-lookup"><span data-stu-id="9c442-159">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="9c442-160">Onder **logboekanalyse**, kies **configureren**.</span><span class="sxs-lookup"><span data-stu-id="9c442-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="9c442-161">Onder **OMS werkruimten**, selecteer Hallo OMS-werkruimte toouse voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="9c442-161">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="9c442-162">Onder **logboek**, selecteer Hallo **IntegrationAccountTrackingEvents** categorie.</span><span class="sxs-lookup"><span data-stu-id="9c442-162">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="9c442-163">Als u bent klaar, kiest u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9c442-163">When you're done, choose **Save**.</span></span>

   ![Log Analytics instellen zodat u kunt diagnostische gegevens tooa logboek verzenden](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="9c442-165">Nu [bijhouden voor uw B2B-berichten in OMS instellen](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="9c442-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="9c442-166">Hoe en waar u diagnostische gegevens gebruikt met andere services uitbreiden</span><span class="sxs-lookup"><span data-stu-id="9c442-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="9c442-167">U kunt samen met Azure Log Analytics uitbreiden hoe u diagnostische gegevens van uw logische app gebruiken met andere Azure-services, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9c442-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="9c442-168">Archief Azure Diagnostics wordt geregistreerd in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9c442-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="9c442-169">Stroom Azure Diagnostics logboeken tooAzure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="9c442-169">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="9c442-170">U kunt vervolgens get real-time bewaking met Telemetrie en analyses van andere services, zoals [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) en [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="9c442-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="9c442-171">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9c442-171">For example:</span></span>

* [<span data-ttu-id="9c442-172">Stroomgegevens van Event Hubs tooStream Analytics</span><span class="sxs-lookup"><span data-stu-id="9c442-172">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="9c442-173">Streaming gegevens analyseren met Stream Analytics en een realtime analytics-dashboard maken in Power BI</span><span class="sxs-lookup"><span data-stu-id="9c442-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="9c442-174">Op basis van het Hallo-opties die u wilt instellen, zorg ervoor dat u eerste [maken van een Azure storage-account](../storage/common/storage-create-storage-account.md) of [maken van een Azure event hub](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="9c442-174">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="9c442-175">Selecteer Hallo opties voor het gewenste toosend diagnostische gegevens:</span><span class="sxs-lookup"><span data-stu-id="9c442-175">Then select hello options for where you want toosend diagnostic data:</span></span>

![Verzenden van gegevens tooAzure storage-account of event hub](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="9c442-177">Bewaarperiode alleen van toepassing wanneer u een opslagaccount toouse kiezen.</span><span class="sxs-lookup"><span data-stu-id="9c442-177">Retention periods apply only when you choose toouse a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="9c442-178">Bijhouden van de ondersteunde schema 's</span><span class="sxs-lookup"><span data-stu-id="9c442-178">Supported tracking schemas</span></span>

<span data-ttu-id="9c442-179">Azure ondersteunt deze bijhouden schematypen waarin alle schema's, met uitzondering van type aangepast Hallo hebt opgelost.</span><span class="sxs-lookup"><span data-stu-id="9c442-179">Azure supports these tracking schema types, which all have fixed schemas except hello Custom type.</span></span>

* [<span data-ttu-id="9c442-180">Volgschema voor AS2</span><span class="sxs-lookup"><span data-stu-id="9c442-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="9c442-181">Volgschema voor X12</span><span class="sxs-lookup"><span data-stu-id="9c442-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="9c442-182">Aangepaste volgschema's</span><span class="sxs-lookup"><span data-stu-id="9c442-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="9c442-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9c442-183">Next steps</span></span>

* [<span data-ttu-id="9c442-184">B2B-berichten in OMS bijhouden</span><span class="sxs-lookup"><span data-stu-id="9c442-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "bijhouden B2B-berichten in OMS")
* [<span data-ttu-id="9c442-185">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="9c442-185">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")

