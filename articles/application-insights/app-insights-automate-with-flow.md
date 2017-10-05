---
title: Azure Application Insights-processen met Microsoft-Flow automatiseren
description: Meer informatie over hoe u Microsoft Flow snel herhaalbare processen automatiseren met behulp van de Application Insights-connector kunt gebruiken.
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
ms.openlocfilehash: 510f4f284bbd0dbe4171896899f7ade7dee19e39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="automate-azure-application-insights-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="e2660-103">Azure Application Insights-processen met de connector voor Microsoft-Flow automatiseren</span><span class="sxs-lookup"><span data-stu-id="e2660-103">Automate Azure Application Insights processes with the connector for Microsoft Flow</span></span>

<span data-ttu-id="e2660-104">Vindt u uzelf herhaaldelijk de dezelfde query's uitvoeren op de telemetriegegevens om te controleren of uw service goed werkt?</span><span class="sxs-lookup"><span data-stu-id="e2660-104">Do you find yourself repeatedly running the same queries on your telemetry data to check that your service is functioning properly?</span></span> <span data-ttu-id="e2660-105">Zoekt u voor het automatiseren van deze query's voor het vinden van trends en afwijkingen en vervolgens uw eigen werkstromen omheen te bouwen?</span><span class="sxs-lookup"><span data-stu-id="e2660-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="e2660-106">De Azure Application Insights-connector (preview) voor Microsoft-Flow is de juiste hulpprogramma voor deze doeleinden.</span><span class="sxs-lookup"><span data-stu-id="e2660-106">The Azure Application Insights connector (preview) for Microsoft Flow is the right tool for these purposes.</span></span>

<span data-ttu-id="e2660-107">Met deze integratie kunt u nu meerdere processen automatiseren zonder een één regel code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="e2660-107">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="e2660-108">Nadat u een stroom met behulp van een actie Application Insights hebt gemaakt, wordt uw Application Insights Analytics query automatisch uitgevoerd door de stroom.</span><span class="sxs-lookup"><span data-stu-id="e2660-108">After you create a flow by using an Application Insights action, the flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="e2660-109">U kunt ook aanvullende acties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e2660-109">You can add additional actions as well.</span></span> <span data-ttu-id="e2660-110">Microsoft-Flow maakt honderden acties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="e2660-110">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="e2660-111">U kunt bijvoorbeeld Microsoft Flow automatisch een e-mailmelding verzenden of maken van een bug in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e2660-111">For example, you can use Microsoft Flow to automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="e2660-112">U kunt ook een van de vele gebruiken [sjablonen](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) die beschikbaar zijn voor de connector voor Microsoft-Flow.</span><span class="sxs-lookup"><span data-stu-id="e2660-112">You can also use one of the many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for the connector for Microsoft Flow.</span></span> <span data-ttu-id="e2660-113">Deze sjablonen wordt het proces van het maken van een stroom versnellen.</span><span class="sxs-lookup"><span data-stu-id="e2660-113">These templates speed up the process of creating a flow.</span></span> 

<!--The Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="e2660-114">Maken van een stroom voor Application Insights</span><span class="sxs-lookup"><span data-stu-id="e2660-114">Create a flow for Application Insights</span></span>

<span data-ttu-id="e2660-115">In deze zelfstudie leert u hoe u een stroom die gebruikmaakt van het algoritme Analytics auto-cluster een Groepkenmerken in de gegevens voor een webtoepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="e2660-115">In this tutorial, you will learn how to create a flow that uses the Analytics auto-cluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="e2660-116">De stroom verzendt de resultaten automatisch via e-mail, slechts één voorbeeld van hoe u kunt Microsoft Flow en Application Insights Analytics samen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e2660-116">The flow automatically sends the results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="e2660-117">Stap 1: Een stroom maken</span><span class="sxs-lookup"><span data-stu-id="e2660-117">Step 1: Create a flow</span></span>
1. <span data-ttu-id="e2660-118">Aanmelden bij [Microsoft Flow](http://flow.microsoft.com), en selecteer vervolgens **mijn loopt**.</span><span class="sxs-lookup"><span data-stu-id="e2660-118">Sign in to [Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="e2660-119">Klik op **maken van een stroom van leeg**.</span><span class="sxs-lookup"><span data-stu-id="e2660-119">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="e2660-120">Stap 2: Maak een trigger voor uw flow</span><span class="sxs-lookup"><span data-stu-id="e2660-120">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="e2660-121">Selecteer **planning**, en selecteer vervolgens **schema - terugkeerpatroon**.</span><span class="sxs-lookup"><span data-stu-id="e2660-121">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="e2660-122">In de **frequentie** de optie **dag**, en in de **Interval** Voer **1**.</span><span class="sxs-lookup"><span data-stu-id="e2660-122">In the **Frequency** box, select **Day**, and in the **Interval** box, enter **1**.</span></span>

    ![Dialoogvenster voor Microsoft-Flow-trigger](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="e2660-124">Stap 3: Een Application Insights-actie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e2660-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="e2660-125">Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e2660-125">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="e2660-126">Zoeken naar **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="e2660-126">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="e2660-127">Klik op **Azure Application Insights – visualiseren Analytics query Preview**.</span><span class="sxs-lookup"><span data-stu-id="e2660-127">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Analytics query-venster uitvoeren](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="e2660-129">Stap 4: Verbinding maken met een Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="e2660-129">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="e2660-130">Deze stap voltooien, moet u een toepassings-ID en een API-sleutel voor uw resource.</span><span class="sxs-lookup"><span data-stu-id="e2660-130">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="e2660-131">U kunt ze ophalen uit de Azure-portal, zoals wordt weergegeven in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="e2660-131">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Toepassings-ID in de Azure portal](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="e2660-133">Geef een naam voor de verbinding, samen met de toepassing-ID en API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="e2660-133">Provide a name for your connection, along with the application ID and API key.</span></span>

    ![Venster van de verbinding met Microsoft-Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="e2660-135">Stap 5: Geef het Analytics-query en grafiek type</span><span class="sxs-lookup"><span data-stu-id="e2660-135">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="e2660-136">Deze voorbeeldquery selecteert de mislukte aanvragen binnen de laatste dag en ze correleert met uitzonderingen die als onderdeel van de bewerking opgetreden.</span><span class="sxs-lookup"><span data-stu-id="e2660-136">This example query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="e2660-137">Analytics correleert toe op basis van de operation_Id-id.</span><span class="sxs-lookup"><span data-stu-id="e2660-137">Analytics correlates them based on the operation_Id identifier.</span></span> <span data-ttu-id="e2660-138">De query vervolgens de resultaten met behulp van de algoritme autocluster segmenten.</span><span class="sxs-lookup"><span data-stu-id="e2660-138">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="e2660-139">Wanneer u uw eigen query's maakt, moet u controleren of ze correct in Analytics werken voordat u deze aan uw stroom toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e2660-139">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

- <span data-ttu-id="e2660-140">De volgende Analytics query toevoegen en selecteer vervolgens het grafiektype voor HTML-tabel.</span><span class="sxs-lookup"><span data-stu-id="e2660-140">Add the following Analytics query, and then select the HTML table chart type.</span></span> 

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

### <a name="step-6-configure-the-flow-to-send-email"></a><span data-ttu-id="e2660-142">Stap 6: De stroom voor het verzenden van e-mail configureren</span><span class="sxs-lookup"><span data-stu-id="e2660-142">Step 6: Configure the flow to send email</span></span>

1. <span data-ttu-id="e2660-143">Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e2660-143">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="e2660-144">Zoeken naar **OfficeOutlook 365**.</span><span class="sxs-lookup"><span data-stu-id="e2660-144">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="e2660-145">Klik op **Outlook in Office 365 – stuurt u een e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="e2660-145">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Selectievenster voor Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="e2660-147">In de **e-mailbericht verzenden** venster de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="e2660-147">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="e2660-148">a.</span><span class="sxs-lookup"><span data-stu-id="e2660-148">a.</span></span> <span data-ttu-id="e2660-149">Typ het e-mailadres van de ontvanger.</span><span class="sxs-lookup"><span data-stu-id="e2660-149">Type the email address of the recipient.</span></span>

   <span data-ttu-id="e2660-150">b.</span><span class="sxs-lookup"><span data-stu-id="e2660-150">b.</span></span> <span data-ttu-id="e2660-151">Typ een onderwerp in voor het e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="e2660-151">Type a subject for the email.</span></span>

   <span data-ttu-id="e2660-152">c.</span><span class="sxs-lookup"><span data-stu-id="e2660-152">c.</span></span> <span data-ttu-id="e2660-153">Klik ergens in de **hoofdtekst** vak en selecteer vervolgens in het dynamische inhoud menu dat op het recht verschijnt **hoofdtekst**.</span><span class="sxs-lookup"><span data-stu-id="e2660-153">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="e2660-154">d.</span><span class="sxs-lookup"><span data-stu-id="e2660-154">d.</span></span> <span data-ttu-id="e2660-155">Klik op **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="e2660-155">Click **Show advanced options**.</span></span>

    ![Outlook-configuratie voor Office 365](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="e2660-157">In het menu van dynamische inhoud het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e2660-157">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="e2660-158">a.</span><span class="sxs-lookup"><span data-stu-id="e2660-158">a.</span></span> <span data-ttu-id="e2660-159">Selecteer **Bijlagenaam**.</span><span class="sxs-lookup"><span data-stu-id="e2660-159">Select **Attachment Name**.</span></span>

    <span data-ttu-id="e2660-160">b.</span><span class="sxs-lookup"><span data-stu-id="e2660-160">b.</span></span> <span data-ttu-id="e2660-161">Selecteer **bijlage inhoud**.</span><span class="sxs-lookup"><span data-stu-id="e2660-161">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="e2660-162">c.</span><span class="sxs-lookup"><span data-stu-id="e2660-162">c.</span></span> <span data-ttu-id="e2660-163">In de **Is HTML** de optie **Ja**.</span><span class="sxs-lookup"><span data-stu-id="e2660-163">In the **Is HTML** box, select **Yes**.</span></span>

    ![Venster van Office 365 e-configuratie](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="e2660-165">Stap 7: Opslaan en testen van uw flow</span><span class="sxs-lookup"><span data-stu-id="e2660-165">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="e2660-166">In de **stroom naam** vak en klik vervolgens op toevoegen van een naam voor uw flow **stroom maken**.</span><span class="sxs-lookup"><span data-stu-id="e2660-166">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Venster van de stroom maken](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="e2660-168">U kunt wachten op de trigger wordt met deze actie worden uitgevoerd, of u kunt de stroom onmiddellijk via uitvoeren [de trigger op verzoek uitgevoerd](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="e2660-168">You can wait for the trigger to run this action, or you can run the flow immediately by [running the trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="e2660-169">Wanneer de stroom wordt uitgevoerd, wordt de ontvangers die u hebt opgegeven in de lijst met e-mailadres een e-mailbericht dat op het volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="e2660-169">When the flow runs, the recipients you have specified in the email list receive an email message that looks like the following:</span></span>

![Voorbeeldbericht](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="e2660-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2660-171">Next steps</span></span>

- <span data-ttu-id="e2660-172">Meer informatie over het maken van [analysequery's](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="e2660-172">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="e2660-173">Meer informatie over [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e2660-173">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





