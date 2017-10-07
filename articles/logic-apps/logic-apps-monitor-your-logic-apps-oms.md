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
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="97655-103">Controleren en verkrijgen van inzicht in logic app wordt uitgevoerd met Operations Management Suite (OMS) en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="97655-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="97655-104">Voor bewaking en uitgebreidere informatie over foutopsporing, kunt u Log Analytics inschakelen op Hallo dezelfde tijd bij het maken van een logische app.</span><span class="sxs-lookup"><span data-stu-id="97655-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="97655-105">Log Analytics biedt Diagnostische logboekregistratie en controle voor uw logische app wordt uitgevoerd via Hallo Operations Management Suite (OMS)-portal.</span><span class="sxs-lookup"><span data-stu-id="97655-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="97655-106">Wanneer u Hallo Logic Apps-Management-oplossing tooOMS toevoegt, krijgt u de cumulatieve status van uw logische app wordt uitgevoerd en de specifieke gegevens, zoals status, uitvoeringstijd, de status opnieuw indienen en correlatie-id's.</span><span class="sxs-lookup"><span data-stu-id="97655-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="97655-107">Dit onderwerp leest hoe tooturn op logboekanalyse of installeer Logic Apps-beheeroplossing in OMS Hallo zodat u kunt de runtime-gebeurtenissen weergeven of gegevens voor uw logische app uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="97655-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="97655-108">toomonitor uw bestaande logische apps als volgt te werk te [Diagnostische logboekregistratie inschakelen en het verzenden van logic app runtime gegevens tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="97655-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="97655-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="97655-109">Requirements</span></span>

<span data-ttu-id="97655-110">Voordat u begint, moet u toohave een OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="97655-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="97655-111">Meer informatie over [hoe toocreate een OMS-werkruimte](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="97655-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="97655-112">Logboekregistratie van diagnostische gegevens inschakelen bij het maken van logische apps</span><span class="sxs-lookup"><span data-stu-id="97655-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="97655-113">In [Azure-portal](https://portal.azure.com), een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="97655-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="97655-114">Kies **nieuwe** > **Enterprise Integration** > **logische App** > **maken**.</span><span class="sxs-lookup"><span data-stu-id="97655-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Een logische app maken](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="97655-116">In Hallo **maken logische app** pagina, deze taken uitvoeren zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="97655-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="97655-117">Geef een naam voor uw logische app en selecteer uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="97655-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="97655-118">Maak of Selecteer een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="97655-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="97655-119">Stel **logboekanalyse** te**op**.</span><span class="sxs-lookup"><span data-stu-id="97655-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="97655-120">Selecteer Hallo OMS-werkruimte waar u te verzenden van gegevens voor uw logische app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="97655-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="97655-121">Als u klaar bent, kiest u **pincode toodashboard** > **maken**.</span><span class="sxs-lookup"><span data-stu-id="97655-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![Logische app maken](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="97655-123">Nadat u deze stap, Azure uw logische app, nu is maakt die zijn gekoppeld aan de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="97655-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="97655-124">Deze stap installeert Hallo Logic Apps-beheeroplossing bovendien ook automatisch in de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="97655-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="97655-125">uw logische app wordt uitgevoerd in OMS, tooview [doorgaan met deze stappen](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="97655-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="97655-126">Hallo Logic Apps-beheeroplossing in OMS installeren</span><span class="sxs-lookup"><span data-stu-id="97655-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="97655-127">Als u al ingeschakeld logboekanalyse tijdens het maken van uw logische app, moet u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="97655-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="97655-128">U hebt al Hallo Logic Apps beheeroplossing geïnstalleerd in OMS.</span><span class="sxs-lookup"><span data-stu-id="97655-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="97655-129">In Hallo [Azure-portal](https://portal.azure.com), kies **meer Services**.</span><span class="sxs-lookup"><span data-stu-id="97655-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="97655-130">Zoek naar 'log analytics' als filter, en kies **logboekanalyse** zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="97655-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Kies 'Log Analytics'](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="97655-132">Onder **logboekanalyse**, zoeken en selecteert u de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="97655-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selecteer de OMS-werkruimte](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="97655-134">Onder **Management**, kies **OMS-Portal**.</span><span class="sxs-lookup"><span data-stu-id="97655-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Kies 'OMS-Portal'](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="97655-136">Op uw startpagina OMS als Hallo upgrade banner wordt weergegeven, kies Hallo banner zodat u eerst de OMS-werkruimte upgraden.</span><span class="sxs-lookup"><span data-stu-id="97655-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="97655-137">Kies vervolgens **galerie met oplossingen**.</span><span class="sxs-lookup"><span data-stu-id="97655-137">Then choose **Solutions Gallery**.</span></span>

   ![Kies 'Galerie met oplossingen'](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="97655-139">Onder **alle oplossingen**, zoeken en kiest u de tegel Hallo voor Hallo **Logic Apps Management** oplossing.</span><span class="sxs-lookup"><span data-stu-id="97655-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   ![Kies 'Logic Apps Management'](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="97655-141">Kies tooinstall Hallo oplossing in de OMS-werkruimte **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97655-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   ![Kies "Toevoegen" voor 'Logic Apps Management'](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="97655-143">Uw logische app wordt uitgevoerd in de OMS-werkruimte weergeven</span><span class="sxs-lookup"><span data-stu-id="97655-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="97655-144">tooview hello aantal en de status van uw logische app wordt uitgevoerd, gaat u toohello overzichtspagina voor de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="97655-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="97655-145">Bekijk de details op Hallo Hallo **Logic Apps Management** tegel.</span><span class="sxs-lookup"><span data-stu-id="97655-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![Overzichttegel waarbij logic app uitvoeren en status](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="97655-147">Als deze upgrade banner wordt weergegeven in plaats van Hallo Logic Apps Management tegel, kiest u Hallo banner zodat u uw OMS-werkruimte eerst upgraden.</span><span class="sxs-lookup"><span data-stu-id="97655-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Upgrade 'OMS-werkruimte'](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="97655-149">tooview een samenvatting met meer informatie over uw logische app wordt uitgevoerd, kies Hallo **Logic Apps Management** tegel.</span><span class="sxs-lookup"><span data-stu-id="97655-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="97655-150">Uw logische app wordt uitgevoerd worden hier, gegroepeerd op naam of uitvoeringsstatus.</span><span class="sxs-lookup"><span data-stu-id="97655-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Samenvatting van status voor uw logische app wordt uitgevoerd](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="97655-152">alle Hallo tooview wordt uitgevoerd voor een specifieke logische app of de status, selecteer Hallo rij voor een logische app of met de status.</span><span class="sxs-lookup"><span data-stu-id="97655-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="97655-153">Hier volgt een voorbeeld waarin alle hello wordt uitgevoerd voor een specifieke logische app:</span><span class="sxs-lookup"><span data-stu-id="97655-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![Weergave voor een logische app of met de status wordt uitgevoerd](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="97655-155">Hallo **opnieuw indienen** kolom ziet u 'Ja' voor worden uitgevoerd die het resultaat zijn van een opnieuw ingediende uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="97655-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="97655-156">toofilter deze resultaten, kunt u uitvoeren zowel client- en serverzijde filteren.</span><span class="sxs-lookup"><span data-stu-id="97655-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="97655-157">Client-side '-filter: Kies Hallo filters die u wilt dat voor elke kolom.</span><span class="sxs-lookup"><span data-stu-id="97655-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="97655-158">Hier volgen enkele voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="97655-158">Here are some examples:</span></span>

     ![Voorbeeld kolomfilters](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="97655-160">Filter serverzijde: toochoose een specifiek tijdstip venster of toolimit Hallo aantal wordt uitgevoerd die worden weergegeven, gebruik Hallo bereik besturingselement bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="97655-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="97655-161">Standaard worden alleen 1000 records tegelijk weergegeven.</span><span class="sxs-lookup"><span data-stu-id="97655-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Wijziging Hallo tijdvenster](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="97655-163">alle tooview Hallo acties en de bijbehorende gegevens voor een specifieke uitvoeren, selecteer een rij die Hallo logboek zoekpagina wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="97655-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="97655-164">Deze informatie in een tabel, kiest u tooview **tabel**.</span><span class="sxs-lookup"><span data-stu-id="97655-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="97655-165">toochange hello query, kunt u Hallo queryreeks in de zoekbalk Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="97655-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="97655-166">Kies voor een betere ervaring **Advanced Analytics**.</span><span class="sxs-lookup"><span data-stu-id="97655-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Acties en details voor een logische app uitgevoerd weergeven](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="97655-168">Hier op Hallo Azure Log Analytics pagina kunt u query's en bijwerken weergeven Hallo resultaat is van een Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="97655-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="97655-169">Deze query gebruikt [Kusto querytaal](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), die u als u wilt dat andere resultaten tooview kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="97655-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Azure Log Analytics - queryweergave](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="97655-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97655-171">Next steps</span></span>

* [<span data-ttu-id="97655-172">B2B-berichten bewaken</span><span class="sxs-lookup"><span data-stu-id="97655-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
