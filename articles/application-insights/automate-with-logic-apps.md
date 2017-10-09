---
title: aaaAutomate Azure Application Insights verwerkt met behulp van Logic Apps.
description: Meer informatie over hoe u snel herhaalbare processen kunt automatiseren door Hallo Application Insights-connector tooyour logische app toe te voegen.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="1a7f1-103">Application Insights-processen automatiseren met behulp van Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1a7f1-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="1a7f1-104">Vindt u uzelf herhaaldelijk Hallo dezelfde query's uitvoeren op uw gegevens telemetrie toocheck of uw service goed werkt?</span><span class="sxs-lookup"><span data-stu-id="1a7f1-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="1a7f1-105">Zoek tooautomate zijn deze query's voor het vinden van trends en afwijkingen en vervolgens uw eigen werkstromen omheen te bouwen? Hello Azure Application Insights-connector (preview) voor Logic Apps is de juiste hulpprogramma Hallo voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="1a7f1-106">Met deze integratie kunt u meerdere processen automatiseren zonder een één regel code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="1a7f1-107">U kunt een logische app maken met Application Insights Hallo connector tooquickly een Application Insights-proces automatiseren.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="1a7f1-108">U kunt ook aanvullende acties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-108">You can add additional actions as well.</span></span> <span data-ttu-id="1a7f1-109">Hallo Logic Apps-functie van Azure App Service kunt u honderden acties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="1a7f1-110">Bijvoorbeeld, met behulp van een logische app, kunt u automatisch een e-mailmelding verzenden of maken van een bug in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="1a7f1-111">U kunt ook een gebruiken Hallo veel beschikbaar [sjablonen](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp versnellen Hallo-proces voor het maken van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="1a7f1-112">Een logische app maken voor Application Insights</span><span class="sxs-lookup"><span data-stu-id="1a7f1-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="1a7f1-113">In deze zelfstudie leert u hoe toocreate een logische app die gebruikmaakt van Hallo Analytics autocluster algoritme toogroup kenmerken in Hallo-gegevens voor een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="1a7f1-114">Hallo resultaten verzonden Hallo stroom automatisch via e-mail, slechts één voorbeeld van hoe u kunt Application Insights Analytics en Logic Apps samen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="1a7f1-115">Stap 1: Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="1a7f1-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="1a7f1-116">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1a7f1-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1a7f1-117">In Hallo **nieuw** deelvenster **Web en mobiel**, en selecteer vervolgens **logische App**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Nieuwe logische app venster](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="1a7f1-119">Stap 2: Een trigger voor uw logische app maken</span><span class="sxs-lookup"><span data-stu-id="1a7f1-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="1a7f1-120">In Hallo **Logic App-ontwerper** venster onder **beginnen met een algemene trigger**, selecteer **terugkeerpatroon**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Logic App Designer-venster](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="1a7f1-122">In Hallo **frequentie** de optie **dag** en klikt u op Hallo **Interval** in het vak **1**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    ![Logic App-ontwerper "Recurrence" venster](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="1a7f1-124">Stap 3: Een Application Insights-actie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a7f1-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="1a7f1-125">Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="1a7f1-126">In Hallo **kiest u een actie** zoekvak, type **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="1a7f1-127">Onder **acties**, klikt u op **Azure Application Insights – visualiseren Analytics query Preview**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Logic App-ontwerper 'Kies een actie' venster](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="1a7f1-129">Stap 4: Verbinding maken met tooan Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="1a7f1-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="1a7f1-130">toocomplete deze stap moet u een toepassings-ID en een API-sleutel voor uw resource.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="1a7f1-131">U kunt ze ophalen uit hello Azure-portal, zoals wordt weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="1a7f1-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Toepassings-ID in hello Azure-portal](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="1a7f1-133">Geef een naam voor uw verbinding, het Hallo toepassings-ID en het Hallo-API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![Venster Logic App-ontwerper stroom-verbinding](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="1a7f1-135">Stap 5: Hallo Analytics-query en grafiektype opgeven</span><span class="sxs-lookup"><span data-stu-id="1a7f1-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="1a7f1-136">In Hallo voorbeeld te volgen, Hallo query Hallo is mislukt-aanvragen in Hallo laatste dag selecteert en verbindt deze met uitzonderingen die zijn opgetreden tijdens het Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="1a7f1-137">Analytics correleert Hallo kan aanvragen, op basis van Hallo operation_Id id.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="1a7f1-138">Hallo resultaten segmenten Hallo query vervolgens met behulp van Hallo autocluster algoritme.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="1a7f1-139">Wanneer u uw eigen query's maakt, moet u controleren of ze correct in Analytics werken voordat u deze tooyour stroom toevoegt.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="1a7f1-140">In Hallo **Query** Voeg Hallo Analytics-query te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a7f1-140">In hello **Query** box, add hello following Analytics query:</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```

2. <span data-ttu-id="1a7f1-141">In Hallo **grafiektype** de optie **HTML-tabel**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![De configuratie queryvenster Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="1a7f1-143">Stap 6: Hallo logic app toosend e-mail configureren</span><span class="sxs-lookup"><span data-stu-id="1a7f1-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="1a7f1-144">Klik op **nieuwe stap**, en selecteer vervolgens **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="1a7f1-145">Typ in het zoekvak Hallo **Outlook van Office 365**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="1a7f1-146">Klik op **Outlook in Office 365 – stuurt u een e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Selectie van Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="1a7f1-148">In Hallo **e-mailbericht verzenden** venster Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a7f1-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="1a7f1-149">a.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-149">a.</span></span> <span data-ttu-id="1a7f1-150">Typ de e-mailadres Hallo van Hallo ontvanger.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="1a7f1-151">b.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-151">b.</span></span> <span data-ttu-id="1a7f1-152">Typ een onderwerp voor Hallo e-mail.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="1a7f1-153">c.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-153">c.</span></span> <span data-ttu-id="1a7f1-154">Klik ergens in Hallo **hoofdtekst** vak en selecteer vervolgens op Hallo dynamische inhoud menu dat op het juiste Hallo verschijnt **hoofdtekst**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="1a7f1-155">d.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-155">d.</span></span> <span data-ttu-id="1a7f1-156">Klik op **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-156">Click **Show advanced options**.</span></span>

      ![Outlook-configuratie voor Office 365](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="1a7f1-158">Hallo dynamische inhoud menu Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a7f1-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="1a7f1-159">a.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-159">a.</span></span> <span data-ttu-id="1a7f1-160">Selecteer **Bijlagenaam**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="1a7f1-161">b.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-161">b.</span></span> <span data-ttu-id="1a7f1-162">Selecteer **bijlage inhoud**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="1a7f1-163">c.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-163">c.</span></span> <span data-ttu-id="1a7f1-164">In Hallo **Is HTML** de optie **Ja**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Configuratiescherm voor Office 365-e-mailadres](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="1a7f1-166">Stap 7: Opslaan en uw logische app testen</span><span class="sxs-lookup"><span data-stu-id="1a7f1-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="1a7f1-167">Klik op **opslaan** toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="1a7f1-168">U kunt wachten op Hallo trigger toorun Hallo logische app, of u kunt Hallo logische app onmiddellijk uitvoeren door te selecteren **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="1a7f1-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![Scherm van logische app maken](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="1a7f1-170">Wanneer uw logische app wordt uitgevoerd, is het Hallo ontvangers die u hebt opgegeven in de lijst met e-mailbericht Hallo ontvangt een e-mail dat op Hallo volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="1a7f1-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![Logic app e-mailbericht](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="1a7f1-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a7f1-172">Next steps</span></span>

- <span data-ttu-id="1a7f1-173">Meer informatie over het maken van [analysequery's](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="1a7f1-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="1a7f1-174">Meer informatie over [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="1a7f1-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





