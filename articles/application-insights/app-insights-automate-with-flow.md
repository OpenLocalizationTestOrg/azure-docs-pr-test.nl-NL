---
title: aaaAutomate Azure Application Insights verwerkt met Microsoft-Flow
description: Meer informatie over hoe u kunt Microsoft Flow tooquickly herhaalbare processen automatiseren met behulp van Hallo Application Insights-connector.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="5810f-103">Azure Application Insights-processen met Hallo-connector voor Microsoft-Flow automatiseren</span><span class="sxs-lookup"><span data-stu-id="5810f-103">Automate Azure Application Insights processes with hello connector for Microsoft Flow</span></span>

<span data-ttu-id="5810f-104">Vindt u uzelf herhaaldelijk uitgevoerd Hallo dezelfde query's op uw telemetrie gegevens toocheck die uw service goed werkt?</span><span class="sxs-lookup"><span data-stu-id="5810f-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck that your service is functioning properly?</span></span> <span data-ttu-id="5810f-105">Zoek tooautomate zijn deze query's voor het vinden van trends en afwijkingen en vervolgens uw eigen werkstromen omheen te bouwen? Hello Azure Application Insights-connector (preview) voor Microsoft-Flow is de juiste hulpprogramma Hallo voor deze doeleinden.</span><span class="sxs-lookup"><span data-stu-id="5810f-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Microsoft Flow is hello right tool for these purposes.</span></span>

<span data-ttu-id="5810f-106">Met deze integratie kunt u nu meerdere processen automatiseren zonder een één regel code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="5810f-106">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="5810f-107">Nadat u een stroom met behulp van een actie Application Insights hebt gemaakt, wordt uw Application Insights Analytics query automatisch uitgevoerd door Hallo-stroom.</span><span class="sxs-lookup"><span data-stu-id="5810f-107">After you create a flow by using an Application Insights action, hello flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="5810f-108">U kunt ook aanvullende acties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5810f-108">You can add additional actions as well.</span></span> <span data-ttu-id="5810f-109">Microsoft-Flow maakt honderden acties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="5810f-109">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="5810f-110">U kunt bijvoorbeeld Microsoft Flow tooautomatically verzenden een e-mailmelding gebruiken of maken van een bug in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="5810f-110">For example, you can use Microsoft Flow tooautomatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="5810f-111">U kunt ook een gebruiken Hallo veel [sjablonen](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) die beschikbaar zijn voor het Hallo-connector voor Microsoft-Flow.</span><span class="sxs-lookup"><span data-stu-id="5810f-111">You can also use one of hello many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for hello connector for Microsoft Flow.</span></span> <span data-ttu-id="5810f-112">Deze sjablonen versnellen Hallo van het maken van een stroom.</span><span class="sxs-lookup"><span data-stu-id="5810f-112">These templates speed up hello process of creating a flow.</span></span> 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="5810f-113">Maken van een stroom voor Application Insights</span><span class="sxs-lookup"><span data-stu-id="5810f-113">Create a flow for Application Insights</span></span>

<span data-ttu-id="5810f-114">In deze zelfstudie leert u hoe toocreate een stroom die gebruikmaakt van Hallo Analytics automatisch cluster algoritme toogroup kenmerken in Hallo-gegevens voor een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="5810f-114">In this tutorial, you will learn how toocreate a flow that uses hello Analytics auto-cluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="5810f-115">Hallo resultaten verzonden Hallo stroom automatisch via e-mail, slechts één voorbeeld van hoe u kunt Microsoft Flow en Application Insights Analytics samen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5810f-115">hello flow automatically sends hello results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="5810f-116">Stap 1: Een stroom maken</span><span class="sxs-lookup"><span data-stu-id="5810f-116">Step 1: Create a flow</span></span>
1. <span data-ttu-id="5810f-117">Aanmelden te[Microsoft Flow](http://flow.microsoft.com), en selecteer vervolgens **mijn loopt**.</span><span class="sxs-lookup"><span data-stu-id="5810f-117">Sign in too[Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="5810f-118">Klik op **maken van een stroom van leeg**.</span><span class="sxs-lookup"><span data-stu-id="5810f-118">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="5810f-119">Stap 2: Maak een trigger voor uw flow</span><span class="sxs-lookup"><span data-stu-id="5810f-119">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="5810f-120">Selecteer **planning**, en selecteer vervolgens **schema - terugkeerpatroon**.</span><span class="sxs-lookup"><span data-stu-id="5810f-120">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="5810f-121">In Hallo **frequentie** de optie **dag**, en in Hallo **Interval** Voer **1**.</span><span class="sxs-lookup"><span data-stu-id="5810f-121">In hello **Frequency** box, select **Day**, and in hello **Interval** box, enter **1**.</span></span>

    ![Dialoogvenster voor Microsoft-Flow-trigger](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="5810f-123">Stap 3: Een Application Insights-actie toevoegen</span><span class="sxs-lookup"><span data-stu-id="5810f-123">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="5810f-124">Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5810f-124">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="5810f-125">Zoeken naar **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="5810f-125">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="5810f-126">Klik op **Azure Application Insights – visualiseren Analytics query Preview**.</span><span class="sxs-lookup"><span data-stu-id="5810f-126">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Analytics query-venster uitvoeren](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="5810f-128">Stap 4: Verbinding maken met tooan Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="5810f-128">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="5810f-129">toocomplete deze stap moet u een toepassings-ID en een API-sleutel voor uw resource.</span><span class="sxs-lookup"><span data-stu-id="5810f-129">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="5810f-130">U kunt ze ophalen uit hello Azure-portal, zoals wordt weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="5810f-130">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Toepassings-ID in hello Azure-portal](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="5810f-132">Geef een naam voor de verbinding, samen met de Hallo-toepassing-ID en API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="5810f-132">Provide a name for your connection, along with hello application ID and API key.</span></span>

    ![Venster van de verbinding met Microsoft-Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="5810f-134">Stap 5: Hallo Analytics-query en grafiektype opgeven</span><span class="sxs-lookup"><span data-stu-id="5810f-134">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="5810f-135">Deze voorbeeldquery Hallo is mislukt-aanvragen in Hallo laatste dag selecteert en verbindt deze met uitzonderingen die zijn opgetreden tijdens het Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="5810f-135">This example query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="5810f-136">Analytics correleert toe op basis van Hallo operation_Id id.</span><span class="sxs-lookup"><span data-stu-id="5810f-136">Analytics correlates them based on hello operation_Id identifier.</span></span> <span data-ttu-id="5810f-137">Hallo resultaten segmenten Hallo query vervolgens met behulp van Hallo autocluster algoritme.</span><span class="sxs-lookup"><span data-stu-id="5810f-137">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="5810f-138">Wanneer u uw eigen query's maakt, moet u controleren of ze correct in Analytics werken voordat u deze tooyour stroom toevoegt.</span><span class="sxs-lookup"><span data-stu-id="5810f-138">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

- <span data-ttu-id="5810f-139">Hallo na Analytics query toevoegen en selecteer vervolgens Hallo HTML tabeltype grafiek.</span><span class="sxs-lookup"><span data-stu-id="5810f-139">Add hello following Analytics query, and then select hello HTML table chart type.</span></span> 

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
    
    ![De configuratie queryvenster Analytics](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a><span data-ttu-id="5810f-141">Stap 6: Hallo stroom toosend e-mail configureren</span><span class="sxs-lookup"><span data-stu-id="5810f-141">Step 6: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="5810f-142">Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5810f-142">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="5810f-143">Zoeken naar **OfficeOutlook 365**.</span><span class="sxs-lookup"><span data-stu-id="5810f-143">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="5810f-144">Klik op **Outlook in Office 365 – stuurt u een e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="5810f-144">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Selectievenster voor Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="5810f-146">In Hallo **e-mailbericht verzenden** venster Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5810f-146">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="5810f-147">a.</span><span class="sxs-lookup"><span data-stu-id="5810f-147">a.</span></span> <span data-ttu-id="5810f-148">Typ de e-mailadres Hallo van Hallo ontvanger.</span><span class="sxs-lookup"><span data-stu-id="5810f-148">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="5810f-149">b.</span><span class="sxs-lookup"><span data-stu-id="5810f-149">b.</span></span> <span data-ttu-id="5810f-150">Typ een onderwerp voor Hallo e-mail.</span><span class="sxs-lookup"><span data-stu-id="5810f-150">Type a subject for hello email.</span></span>

   <span data-ttu-id="5810f-151">c.</span><span class="sxs-lookup"><span data-stu-id="5810f-151">c.</span></span> <span data-ttu-id="5810f-152">Klik ergens in Hallo **hoofdtekst** vak en selecteer vervolgens op Hallo dynamische inhoud menu dat op het juiste Hallo verschijnt **hoofdtekst**.</span><span class="sxs-lookup"><span data-stu-id="5810f-152">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="5810f-153">d.</span><span class="sxs-lookup"><span data-stu-id="5810f-153">d.</span></span> <span data-ttu-id="5810f-154">Klik op **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="5810f-154">Click **Show advanced options**.</span></span>

    ![Outlook-configuratie voor Office 365](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="5810f-156">Hallo dynamische inhoud menu Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5810f-156">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="5810f-157">a.</span><span class="sxs-lookup"><span data-stu-id="5810f-157">a.</span></span> <span data-ttu-id="5810f-158">Selecteer **Bijlagenaam**.</span><span class="sxs-lookup"><span data-stu-id="5810f-158">Select **Attachment Name**.</span></span>

    <span data-ttu-id="5810f-159">b.</span><span class="sxs-lookup"><span data-stu-id="5810f-159">b.</span></span> <span data-ttu-id="5810f-160">Selecteer **bijlage inhoud**.</span><span class="sxs-lookup"><span data-stu-id="5810f-160">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="5810f-161">c.</span><span class="sxs-lookup"><span data-stu-id="5810f-161">c.</span></span> <span data-ttu-id="5810f-162">In Hallo **Is HTML** de optie **Ja**.</span><span class="sxs-lookup"><span data-stu-id="5810f-162">In hello **Is HTML** box, select **Yes**.</span></span>

    ![Venster van Office 365 e-configuratie](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="5810f-164">Stap 7: Opslaan en testen van uw flow</span><span class="sxs-lookup"><span data-stu-id="5810f-164">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="5810f-165">In Hallo **stroom naam** vak en klik vervolgens op toevoegen van een naam voor uw flow **stroom maken**.</span><span class="sxs-lookup"><span data-stu-id="5810f-165">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Venster van de stroom maken](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="5810f-167">U kunt wachten om deze actie op Hallo trigger toorun of kunt u meteen via Hallo stroom uitvoeren [actieve Hallo-trigger op aanvraag](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="5810f-167">You can wait for hello trigger toorun this action, or you can run hello flow immediately by [running hello trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="5810f-168">Wanneer Hallo stroom wordt uitgevoerd, wordt Hallo ontvangers die u hebt opgegeven in de lijst met e-mailbericht Hallo een e-mailbericht dat op Hallo volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="5810f-168">When hello flow runs, hello recipients you have specified in hello email list receive an email message that looks like hello following:</span></span>

![Voorbeeldbericht](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="5810f-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5810f-170">Next steps</span></span>

- <span data-ttu-id="5810f-171">Meer informatie over het maken van [analysequery's](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="5810f-171">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="5810f-172">Meer informatie over [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5810f-172">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





