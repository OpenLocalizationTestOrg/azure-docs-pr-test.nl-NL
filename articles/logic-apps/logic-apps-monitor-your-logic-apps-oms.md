---
title: Monitor en get inzicht in uw logische app wordt uitgevoerd met OMS - Azure Logic Apps | Microsoft Docs
description: Bewaken van uw logische app wordt uitgevoerd met logboekanalyse en Operations Management Suite (OMS) om inzicht te krijgen en uitgebreidere foutopsporing informatie voor probleemoplossing en diagnostische gegevens opvragen
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
ms.openlocfilehash: 0e9f0ef3c87b5c0da1cc4ad16d37178c8f5c9625
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="30e37-103">Controleren en verkrijgen van inzicht in logic app wordt uitgevoerd met Operations Management Suite (OMS) en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="30e37-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="30e37-104">Voor bewaking en uitgebreidere informatie over foutopsporing, kunt u Log Analytics inschakelen op hetzelfde moment als u een logische app maakt.</span><span class="sxs-lookup"><span data-stu-id="30e37-104">For monitoring and richer debugging information, you can turn on Log Analytics at the same time when you create a logic app.</span></span> <span data-ttu-id="30e37-105">Log Analytics biedt Diagnostische logboekregistratie en controle voor uw logische app wordt uitgevoerd via de portal Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="30e37-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through the Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="30e37-106">Wanneer u de oplossing Logic Apps aan OMS toevoegt, krijgt u de cumulatieve status van uw logische app wordt uitgevoerd en de specifieke gegevens, zoals status, uitvoeringstijd, de status opnieuw indienen en correlatie-id's.</span><span class="sxs-lookup"><span data-stu-id="30e37-106">When you add the Logic Apps Management solution to OMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="30e37-107">Dit onderwerp wordt beschreven hoe logboekanalyse inschakelen of installeren van de oplossing Logic Apps Management in OMS zodat u de runtime-gebeurtenissen en de gegevens voor uw logische app uitgevoerd bekijken kunt.</span><span class="sxs-lookup"><span data-stu-id="30e37-107">This topic shows how to turn on Log Analytics or install the Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="30e37-108">Volg deze stappen voor voor het bewaken van uw bestaande logische apps [Diagnostische logboekregistratie inschakelen en logic app runtimegegevens verzenden naar OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="30e37-108">To monitor your existing logic apps, follow these steps to [turn on diagnostic logging and send logic app runtime data to OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="30e37-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="30e37-109">Requirements</span></span>

<span data-ttu-id="30e37-110">Voordat u begint, moet u een OMS-werkruimte hebt.</span><span class="sxs-lookup"><span data-stu-id="30e37-110">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="30e37-111">Meer informatie over [het maken van een OMS-werkruimte](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="30e37-111">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="30e37-112">Logboekregistratie van diagnostische gegevens inschakelen bij het maken van logische apps</span><span class="sxs-lookup"><span data-stu-id="30e37-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="30e37-113">In [Azure-portal](https://portal.azure.com), een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="30e37-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="30e37-114">Kies **nieuwe** > **Enterprise Integration** > **logische App** > **maken**.</span><span class="sxs-lookup"><span data-stu-id="30e37-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Een logische app maken](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="30e37-116">In de **maken logische app** pagina, deze taken uitvoeren zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="30e37-116">In the **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="30e37-117">Geef een naam voor uw logische app en selecteer uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="30e37-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="30e37-118">Maak of Selecteer een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="30e37-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="30e37-119">Stel **Meld Analytics** naar **op**.</span><span class="sxs-lookup"><span data-stu-id="30e37-119">Set **Log Analytics** to **On**.</span></span> 
   <span data-ttu-id="30e37-120">Selecteer de OMS-werkruimte waar u wilt verzenden van gegevens voor uw logische app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="30e37-120">Select the OMS workspace where you want to send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="30e37-121">Als u klaar bent, kiest u **vastmaken aan dashboard** > **maken**.</span><span class="sxs-lookup"><span data-stu-id="30e37-121">When you're ready, choose **Pin to dashboard** > **Create**.</span></span>

      ![Logische app maken](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="30e37-123">Nadat u deze stap, Azure uw logische app, nu is maakt die zijn gekoppeld aan de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="30e37-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="30e37-124">Deze stap installeert ook ook automatisch het beheersysteem voor Logic Apps in de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="30e37-124">Also, this step also automatically installs the Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="30e37-125">Om weer te geven van de logische app wordt uitgevoerd in OMS, [doorgaan met deze stappen](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="30e37-125">To view your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-the-logic-apps-management-solution-in-oms"></a><span data-ttu-id="30e37-126">De oplossing Logic Apps Management in OMS installeren</span><span class="sxs-lookup"><span data-stu-id="30e37-126">Install the Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="30e37-127">Als u al ingeschakeld logboekanalyse tijdens het maken van uw logische app, moet u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="30e37-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="30e37-128">U hebt al het beheersysteem voor Logic Apps geïnstalleerd in OMS.</span><span class="sxs-lookup"><span data-stu-id="30e37-128">You already have the Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="30e37-129">In de [Azure-portal](https://portal.azure.com), kies **meer Services**.</span><span class="sxs-lookup"><span data-stu-id="30e37-129">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="30e37-130">Zoek naar 'log analytics' als filter, en kies **logboekanalyse** zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="30e37-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Kies 'Log Analytics'](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="30e37-132">Onder **logboekanalyse**, zoeken en selecteert u de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="30e37-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selecteer de OMS-werkruimte](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="30e37-134">Onder **Management**, kies **OMS-Portal**.</span><span class="sxs-lookup"><span data-stu-id="30e37-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Kies 'OMS-Portal'](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="30e37-136">Op uw startpagina OMS als de upgrade banner wordt weergegeven, kies de banner zodat u uw OMS-werkruimte eerst upgraden.</span><span class="sxs-lookup"><span data-stu-id="30e37-136">On your OMS homepage, if the upgrade banner appears, choose the banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="30e37-137">Kies vervolgens **galerie met oplossingen**.</span><span class="sxs-lookup"><span data-stu-id="30e37-137">Then choose **Solutions Gallery**.</span></span>

   ![Kies 'Galerie met oplossingen'](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="30e37-139">Onder **alle oplossingen**, zoeken en kiest u de tegel voor de **Logic Apps Management** oplossing.</span><span class="sxs-lookup"><span data-stu-id="30e37-139">Under **All solutions**, find and choose the tile for the **Logic Apps Management** solution.</span></span>

   ![Kies 'Logic Apps Management'](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="30e37-141">Voor het installeren van de oplossing in de OMS-werkruimte, kiest u **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="30e37-141">To install the solution in your OMS workspace, choose **Add**.</span></span>

   ![Kies "Toevoegen" voor 'Logic Apps Management'](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="30e37-143">Uw logische app wordt uitgevoerd in de OMS-werkruimte weergeven</span><span class="sxs-lookup"><span data-stu-id="30e37-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="30e37-144">Het aantal en de status van uw logische app wordt uitgevoerd, Ga naar de overzichtspagina voor de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="30e37-144">To view the count and status for your logic app runs, go to the overview page for your OMS workspace.</span></span> <span data-ttu-id="30e37-145">Lees de informatie op de **Logic Apps Management** tegel.</span><span class="sxs-lookup"><span data-stu-id="30e37-145">Review the details on the **Logic Apps Management** tile.</span></span>

   ![Overzichttegel waarbij logic app uitvoeren en status](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="30e37-147">Als deze upgrade banner wordt weergegeven in plaats van de tegel Logic Apps Management, kiest u de banner zodat u uw OMS-werkruimte eerst upgraden.</span><span class="sxs-lookup"><span data-stu-id="30e37-147">If this upgrade banner appears instead of the Logic Apps Management tile, choose the banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Upgrade 'OMS-werkruimte'](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="30e37-149">Kies een overzicht met meer informatie over uw logische app wordt uitgevoerd, de **Logic Apps Management** tegel.</span><span class="sxs-lookup"><span data-stu-id="30e37-149">To view a summary with more details about your logic app runs, choose the **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="30e37-150">Uw logische app wordt uitgevoerd worden hier, gegroepeerd op naam of uitvoeringsstatus.</span><span class="sxs-lookup"><span data-stu-id="30e37-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Samenvatting van status voor uw logische app wordt uitgevoerd](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="30e37-152">Als u wilt weergeven van de uitvoert voor een specifieke logische app of de status, selecteer de rij voor een logische app of met de status.</span><span class="sxs-lookup"><span data-stu-id="30e37-152">To view all the runs for a specific logic app or status, select the row for a logic app or a status.</span></span>

   <span data-ttu-id="30e37-153">Hier volgt een voorbeeld waarin de uitvoert voor een specifieke logische app:</span><span class="sxs-lookup"><span data-stu-id="30e37-153">Here is an example that shows all the runs for a specific logic app:</span></span>

   ![Weergave voor een logische app of met de status wordt uitgevoerd](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="30e37-155">De **opnieuw indienen** kolom ziet u 'Ja' voor worden uitgevoerd die het resultaat zijn van een opnieuw ingediende uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="30e37-155">The **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="30e37-156">Als u wilt filteren op deze resultaten, kunt u zowel client- en serverzijde filteren uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="30e37-156">To filter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="30e37-157">Client-side '-filter: Kies de filters die u wilt dat voor elke kolom.</span><span class="sxs-lookup"><span data-stu-id="30e37-157">Client-side filter: For each column, choose the filters that you want.</span></span> 
   <span data-ttu-id="30e37-158">Hier volgen enkele voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="30e37-158">Here are some examples:</span></span>

     ![Voorbeeld kolomfilters](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="30e37-160">Filter serverzijde: kiezen van een specifiek tijdvenster of beperken het aantal uitgevoerd die worden weergegeven, gebruikt u het bereik-besturingselement aan de bovenkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="30e37-160">Server-side filter: To choose a specific time window or to limit the number of runs that appear, use the scope control at the top of the page.</span></span> 
   <span data-ttu-id="30e37-161">Standaard worden alleen 1000 records tegelijk weergegeven.</span><span class="sxs-lookup"><span data-stu-id="30e37-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Wijzigen van het tijdvenster](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="30e37-163">Als u wilt weergeven van alle acties en de bijbehorende gegevens voor een specifiek run, selecteer een rij die de zoekpagina logboek wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="30e37-163">To view all the actions and their details for a specific run, select a row, which opens the Log Search page.</span></span> 

   * <span data-ttu-id="30e37-164">U kunt deze informatie bekijken in een tabel **tabel**.</span><span class="sxs-lookup"><span data-stu-id="30e37-164">To view this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="30e37-165">Als u wilt de query wijzigt, kunt u de query-tekenreeks in de zoekbalk kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="30e37-165">To change the query, you can edit the query string in the search bar.</span></span> 
   <span data-ttu-id="30e37-166">Kies voor een betere ervaring **Advanced Analytics**.</span><span class="sxs-lookup"><span data-stu-id="30e37-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Acties en details voor een logische app uitgevoerd weergeven](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="30e37-168">Op de pagina Azure Log Analytics kunt u hier query's bijwerken en bekijk de resultaten van de tabel.</span><span class="sxs-lookup"><span data-stu-id="30e37-168">Here on the Azure Log Analytics page, you can update queries and view the results from the table.</span></span> 
     <span data-ttu-id="30e37-169">Deze query gebruikt [Kusto querytaal](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), die u als u wilt weergeven van verschillende resultaten kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="30e37-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want to view different results.</span></span> 

     ![Azure Log Analytics - queryweergave](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="30e37-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="30e37-171">Next steps</span></span>

* [<span data-ttu-id="30e37-172">B2B-berichten bewaken</span><span class="sxs-lookup"><span data-stu-id="30e37-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
