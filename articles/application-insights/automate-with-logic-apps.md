---
title: Azure Application Insights-processen automatiseren met behulp van Logic Apps.
description: Meer informatie over hoe u snel herhaalbare processen kunt automatiseren door de Application Insights-connector toe te voegen aan uw logische app.
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
ms.openlocfilehash: 36df5bc0a019f4197d40fd6fa5a2a9957820c8b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="a307f-103">Application Insights-processen automatiseren met behulp van Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a307f-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="a307f-104">Vindt u uzelf herhaaldelijk de dezelfde query's uitvoeren op de telemetriegegevens om te controleren of uw service goed werkt?</span><span class="sxs-lookup"><span data-stu-id="a307f-104">Do you find yourself repeatedly running the same queries on your telemetry data to check whether your service is functioning properly?</span></span> <span data-ttu-id="a307f-105">Zoekt u voor het automatiseren van deze query's voor het vinden van trends en afwijkingen en vervolgens uw eigen werkstromen omheen te bouwen?</span><span class="sxs-lookup"><span data-stu-id="a307f-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="a307f-106">De Azure Application Insights-connector (preview) voor Logic Apps is het juiste programma voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="a307f-106">The Azure Application Insights connector (preview) for Logic Apps is the right tool for this purpose.</span></span>

<span data-ttu-id="a307f-107">Met deze integratie kunt u meerdere processen automatiseren zonder een één regel code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="a307f-107">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="a307f-108">U kunt een logische app maken met de Application Insights-connector voor het snel een Application Insights-proces te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="a307f-108">You can create a logic app with the Application Insights connector to quickly automate any Application Insights process.</span></span> 

<span data-ttu-id="a307f-109">U kunt ook aanvullende acties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a307f-109">You can add additional actions as well.</span></span> <span data-ttu-id="a307f-110">De functie Logic Apps van Azure App Service maakt honderden acties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="a307f-110">The Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="a307f-111">Bijvoorbeeld, met behulp van een logische app, kunt u automatisch een e-mailmelding verzenden of maken van een bug in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a307f-111">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="a307f-112">U kunt ook een van de vele beschikbaar gebruiken [sjablonen](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) om u te helpen bij het maken van uw logische app versnellen.</span><span class="sxs-lookup"><span data-stu-id="a307f-112">You can also use one of the many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) to help speed up the process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="a307f-113">Een logische app maken voor Application Insights</span><span class="sxs-lookup"><span data-stu-id="a307f-113">Create a logic app for Application Insights</span></span>

<span data-ttu-id="a307f-114">In deze zelfstudie leert u hoe u een logische app die gebruikmaakt van het algoritme Analytics autocluster kenmerken in de gegevens voor een webtoepassing maken.</span><span class="sxs-lookup"><span data-stu-id="a307f-114">In this tutorial, you learn how to create a logic app that uses the Analytics autocluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="a307f-115">De stroom verzendt de resultaten automatisch via e-mail, slechts één voorbeeld van hoe u kunt Application Insights Analytics en Logic Apps samen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a307f-115">The flow automatically sends the results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="a307f-116">Stap 1: Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="a307f-116">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="a307f-117">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a307f-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a307f-118">In de **nieuw** deelvenster **Web en mobiel**, en selecteer vervolgens **logische App**.</span><span class="sxs-lookup"><span data-stu-id="a307f-118">In the **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Nieuwe logische app venster](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="a307f-120">Stap 2: Een trigger voor uw logische app maken</span><span class="sxs-lookup"><span data-stu-id="a307f-120">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="a307f-121">In de **Logic App-ontwerper** venster onder **beginnen met een algemene trigger**, selecteer **terugkeerpatroon**.</span><span class="sxs-lookup"><span data-stu-id="a307f-121">In the **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Logic App Designer-venster](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="a307f-123">In de **frequentie** de optie **dag** en klikt u op de **Interval** in het vak **1**.</span><span class="sxs-lookup"><span data-stu-id="a307f-123">In the **Frequency** box, select **Day** and then, in the **Interval** box, type **1**.</span></span>

    ![Logic App-ontwerper "Recurrence" venster](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="a307f-125">Stap 3: Een Application Insights-actie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a307f-125">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="a307f-126">Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a307f-126">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="a307f-127">In de **kiest u een actie** zoekvak, type **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="a307f-127">In the **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="a307f-128">Onder **acties**, klikt u op **Azure Application Insights – visualiseren Analytics query Preview**.</span><span class="sxs-lookup"><span data-stu-id="a307f-128">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Logic App-ontwerper 'Kies een actie' venster](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="a307f-130">Stap 4: Verbinding maken met een Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="a307f-130">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="a307f-131">Deze stap voltooien, moet u een toepassings-ID en een API-sleutel voor uw resource.</span><span class="sxs-lookup"><span data-stu-id="a307f-131">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="a307f-132">U kunt ze ophalen uit de Azure-portal, zoals wordt weergegeven in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="a307f-132">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Toepassings-ID in de Azure portal](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="a307f-134">Geef een naam voor de verbinding, de toepassings-ID en de API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="a307f-134">Provide a name for your connection, the application ID, and the API key.</span></span>

![Venster Logic App-ontwerper stroom-verbinding](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="a307f-136">Stap 5: Geef het Analytics-query en grafiek type</span><span class="sxs-lookup"><span data-stu-id="a307f-136">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="a307f-137">In het volgende voorbeeld wordt de query selecteert de mislukte aanvragen binnen de laatste dag en verbindt deze met uitzonderingen die als onderdeel van de bewerking opgetreden.</span><span class="sxs-lookup"><span data-stu-id="a307f-137">In the following example, the query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="a307f-138">Analytics correleert de mislukte aanvragen, op basis van de operation_Id-id.</span><span class="sxs-lookup"><span data-stu-id="a307f-138">Analytics correlates the failed requests, based on the operation_Id identifier.</span></span> <span data-ttu-id="a307f-139">De query vervolgens de resultaten met behulp van de algoritme autocluster segmenten.</span><span class="sxs-lookup"><span data-stu-id="a307f-139">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="a307f-140">Wanneer u uw eigen query's maakt, moet u controleren of ze correct in Analytics werken voordat u deze aan uw stroom toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a307f-140">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

1. <span data-ttu-id="a307f-141">In de **Query** Voeg de volgende Analytics-query:</span><span class="sxs-lookup"><span data-stu-id="a307f-141">In the **Query** box, add the following Analytics query:</span></span> 

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

2. <span data-ttu-id="a307f-142">In de **grafiektype** de optie **HTML-tabel**.</span><span class="sxs-lookup"><span data-stu-id="a307f-142">In the **Chart Type** box, select **Html Table**.</span></span>

    ![De configuratie queryvenster Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-the-logic-app-to-send-email"></a><span data-ttu-id="a307f-144">Stap 6: Configureer de logische app voor het verzenden van e-mail</span><span class="sxs-lookup"><span data-stu-id="a307f-144">Step 6: Configure the logic app to send email</span></span>

1. <span data-ttu-id="a307f-145">Klik op **nieuwe stap**, en selecteer vervolgens **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a307f-145">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="a307f-146">Typ in het zoekvak **Outlook van Office 365**.</span><span class="sxs-lookup"><span data-stu-id="a307f-146">In the search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="a307f-147">Klik op **Outlook in Office 365 – stuurt u een e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="a307f-147">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Selectie van Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="a307f-149">In de **e-mailbericht verzenden** venster de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="a307f-149">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="a307f-150">a.</span><span class="sxs-lookup"><span data-stu-id="a307f-150">a.</span></span> <span data-ttu-id="a307f-151">Typ het e-mailadres van de ontvanger.</span><span class="sxs-lookup"><span data-stu-id="a307f-151">Type the email address of the recipient.</span></span>

   <span data-ttu-id="a307f-152">b.</span><span class="sxs-lookup"><span data-stu-id="a307f-152">b.</span></span> <span data-ttu-id="a307f-153">Typ een onderwerp in voor het e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="a307f-153">Type a subject for the email.</span></span>

   <span data-ttu-id="a307f-154">c.</span><span class="sxs-lookup"><span data-stu-id="a307f-154">c.</span></span> <span data-ttu-id="a307f-155">Klik ergens in de **hoofdtekst** vak en selecteer vervolgens in het dynamische inhoud menu dat op het recht verschijnt **hoofdtekst**.</span><span class="sxs-lookup"><span data-stu-id="a307f-155">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="a307f-156">d.</span><span class="sxs-lookup"><span data-stu-id="a307f-156">d.</span></span> <span data-ttu-id="a307f-157">Klik op **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="a307f-157">Click **Show advanced options**.</span></span>

      ![Outlook-configuratie voor Office 365](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="a307f-159">In het menu van dynamische inhoud het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a307f-159">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="a307f-160">a.</span><span class="sxs-lookup"><span data-stu-id="a307f-160">a.</span></span> <span data-ttu-id="a307f-161">Selecteer **Bijlagenaam**.</span><span class="sxs-lookup"><span data-stu-id="a307f-161">Select **Attachment Name**.</span></span>

    <span data-ttu-id="a307f-162">b.</span><span class="sxs-lookup"><span data-stu-id="a307f-162">b.</span></span> <span data-ttu-id="a307f-163">Selecteer **bijlage inhoud**.</span><span class="sxs-lookup"><span data-stu-id="a307f-163">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="a307f-164">c.</span><span class="sxs-lookup"><span data-stu-id="a307f-164">c.</span></span> <span data-ttu-id="a307f-165">In de **Is HTML** de optie **Ja**.</span><span class="sxs-lookup"><span data-stu-id="a307f-165">In the **Is HTML** box, select **Yes**.</span></span>

      ![Configuratiescherm voor Office 365-e-mailadres](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="a307f-167">Stap 7: Opslaan en uw logische app testen</span><span class="sxs-lookup"><span data-stu-id="a307f-167">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="a307f-168">Klik op **opslaan** uw wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="a307f-168">Click **Save** to save your changes.</span></span>

<span data-ttu-id="a307f-169">U kunt wachten op de trigger uit te voeren van de logische app, of u kunt de logische app onmiddellijk uitvoeren door te selecteren **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="a307f-169">You can wait for the trigger to run the logic app, or you can run the logic app immediately by selecting **Run**.</span></span>

![Scherm van logische app maken](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="a307f-171">Wanneer uw logische app wordt uitgevoerd, is de ontvangers die u hebt opgegeven in de lijst met e-mailbericht ontvangt een e-mailbericht dat op het volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="a307f-171">When your logic app runs, the recipients you specified in the email list will receive an email that looks like the following:</span></span>

![Logic app e-mailbericht](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="a307f-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a307f-173">Next steps</span></span>

- <span data-ttu-id="a307f-174">Meer informatie over het maken van [analysequery's](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="a307f-174">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="a307f-175">Meer informatie over [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="a307f-175">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





