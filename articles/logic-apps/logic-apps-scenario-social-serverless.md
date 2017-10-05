---
title: 'Scenario: een klant insights dashboard maken met Azure zonder server | Microsoft Docs'
description: Een voorbeeld van hoe u een dashboard voor het beheren van feedback van klanten, sociale gegevens en meer met Azure Logic Apps en Azure Functions kunt samenstellen.
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: 0b6e118cb13ab8185d8eeb42bec6147155967967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="18f84-103">Een realtime klant insights dashboard maken met Azure Logic Apps en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="18f84-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="18f84-104">Azure zonder Server-hulpprogramma's bieden krachtige mogelijkheden om snel te bouwen en toepassingen in de cloud, zonder dat bij het nadenken over de infrastructuur worden gehost.</span><span class="sxs-lookup"><span data-stu-id="18f84-104">Azure Serverless tools provide powerful capabilities to quickly build and host applications in the cloud, without having to think about infrastructure.</span></span>  <span data-ttu-id="18f84-105">In dit scenario zullen we een dashboard voor het activeren van feedback van klanten, feedback met machine learning analyseren en inzichten publiceren een bron, zoals Power BI of Azure Data Lake maken.</span><span class="sxs-lookup"><span data-stu-id="18f84-105">In this scenario, we will create a dashboard to trigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-the-scenario-and-tools-used"></a><span data-ttu-id="18f84-106">Overzicht van het scenario en de hulpprogramma's gebruikt</span><span class="sxs-lookup"><span data-stu-id="18f84-106">Overview of the scenario and tools used</span></span>

<span data-ttu-id="18f84-107">Om deze oplossing te implementeren, zullen we gebruikmaken van de twee belangrijkste onderdelen van zonder server apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) en [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="18f84-107">In order to implement this solution, we will leverage the two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="18f84-108">Logic Apps is een zonder server werkstroomengine in de cloud.</span><span class="sxs-lookup"><span data-stu-id="18f84-108">Logic Apps is a serverless workflow engine in the cloud.</span></span>  <span data-ttu-id="18f84-109">Deze orchestration biedt verschillende zonder Server-onderdelen en ook verbinding maakt met meer dan 100 API's en services.</span><span class="sxs-lookup"><span data-stu-id="18f84-109">It provides orchestration across serverless components, and also connects to over 100 services and APIs.</span></span>  <span data-ttu-id="18f84-110">We gaan een logische app activeren op feedback van klanten te maken voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="18f84-110">For this scenario, we will create a logic app to trigger on feedback from customers.</span></span>  <span data-ttu-id="18f84-111">Enkele van de connectors die helpen kunnen bij het reageren op feedback van klanten Outlook.com, Office 365, enquête Monkey, Twitter en een HTTP-aanvraag zijn [van een webformulier](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span><span class="sxs-lookup"><span data-stu-id="18f84-111">Some of the connectors that can assist in reacting to customer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="18f84-112">Voor de werkstroom hieronder, wordt er een hashtag op Twitter bewaken.</span><span class="sxs-lookup"><span data-stu-id="18f84-112">For the workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="18f84-113">Functies bieden zonder server compute in de cloud.</span><span class="sxs-lookup"><span data-stu-id="18f84-113">Functions provide serverless compute in the cloud.</span></span>  <span data-ttu-id="18f84-114">In dit scenario gebruiken we Azure Functions tweets van klanten op basis van een reeks vooraf gedefinieerde trefwoorden markeren.</span><span class="sxs-lookup"><span data-stu-id="18f84-114">In this scenario, we will use Azure Functions to flag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="18f84-115">De volledige oplossing kan worden [bouwen in Visual Studio](logic-apps-deploy-from-vs.md) en [geïmplementeerd als onderdeel van een sjabloon resource](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="18f84-115">The entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="18f84-116">Er is ook video-overzicht van het scenario [op Channel 9](http://aka.ms/logicappsdemo).</span><span class="sxs-lookup"><span data-stu-id="18f84-116">There is also video walkthrough of the scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-the-logic-app-to-trigger-on-customer-data"></a><span data-ttu-id="18f84-117">De logische app activeren op gegevens van de klant opbouwen</span><span class="sxs-lookup"><span data-stu-id="18f84-117">Build the logic app to trigger on customer data</span></span>

<span data-ttu-id="18f84-118">Na [maken van een logische app](logic-apps-create-a-logic-app.md) in Visual Studio of de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="18f84-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or the Azure portal:</span></span>

1. <span data-ttu-id="18f84-119">Toevoegen van een trigger voor **op nieuwe Tweets** van Twitter</span><span class="sxs-lookup"><span data-stu-id="18f84-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="18f84-120">Configureer de trigger om te luisteren naar tweets op een sleutelwoord of hashtag.</span><span class="sxs-lookup"><span data-stu-id="18f84-120">Configure the trigger to listen to tweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="18f84-121">De eigenschap terugkeerpatroon in de trigger wordt bepaald hoe vaak de logische app controleert op nieuwe items op triggers op basis van polling</span><span class="sxs-lookup"><span data-stu-id="18f84-121">The recurrence property on the trigger will determine how frequently the logic app checks for new items on polling-based triggers</span></span>

   ![Voorbeeld van een trigger Twitter][1]

<span data-ttu-id="18f84-123">Deze app wordt nu gestart op alle nieuwe tweets.</span><span class="sxs-lookup"><span data-stu-id="18f84-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="18f84-124">We kunnen vervolgens worden die gegevens tweet en begrijpen meer van de gevoel uitgedrukt.</span><span class="sxs-lookup"><span data-stu-id="18f84-124">We can then take that tweet data and understand more of the sentiment expressed.</span></span>  <span data-ttu-id="18f84-125">We gebruiken hiervoor de [Azure cognitieve Service](https://azure.microsoft.com/services/cognitive-services/) voor het detecteren van gevoel van tekst.</span><span class="sxs-lookup"><span data-stu-id="18f84-125">For this we use the [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) to detect sentiment of text.</span></span>

1. <span data-ttu-id="18f84-126">Klik op **nieuwe stap**</span><span class="sxs-lookup"><span data-stu-id="18f84-126">Click **New Step**</span></span>
1. <span data-ttu-id="18f84-127">Selecteer of zoek naar de **Tekstanalyse** connector</span><span class="sxs-lookup"><span data-stu-id="18f84-127">Select or search for the **Text Analytics** connector</span></span>
1. <span data-ttu-id="18f84-128">Selecteer de **detecteren gevoel** bewerking</span><span class="sxs-lookup"><span data-stu-id="18f84-128">Select the **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="18f84-129">Als u wordt gevraagd, geeft u een geldige sleutel cognitieve Services voor de service Tekstanalyse</span><span class="sxs-lookup"><span data-stu-id="18f84-129">If prompted, provide a valid Cognitive Services key for the Text Analytics service</span></span>
1. <span data-ttu-id="18f84-130">Voeg de **Tweet tekst** als de tekst te analyseren.</span><span class="sxs-lookup"><span data-stu-id="18f84-130">Add the **Tweet Text** as the text to analyze.</span></span>

<span data-ttu-id="18f84-131">Nu dat we de tweet gegevens en inzichten op de tweet hebt, kan een aantal andere connectors relevant zijn:</span><span class="sxs-lookup"><span data-stu-id="18f84-131">Now that we have the tweet data, and insights on the tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="18f84-132">Power BI - rijen toevoegen aan de gegevensset Streaming: weergave tweets realtime op een Power BI-dashboard.</span><span class="sxs-lookup"><span data-stu-id="18f84-132">Power BI - Add Rows to Streaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="18f84-133">Azure Data Lake - bestand toevoegen: klantgegevens toevoegen aan een Azure Data Lake-gegevensset in analytics-taken op te nemen.</span><span class="sxs-lookup"><span data-stu-id="18f84-133">Azure Data Lake - Append file: Add customer data to an Azure Data Lake dataset to include in analytics jobs.</span></span>
* <span data-ttu-id="18f84-134">SQL - rijen toevoegen: opslaan van gegevens in een database voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="18f84-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="18f84-135">Vertraging - bericht verzenden: waarschuwing van een ongebruikt kanaal op negatieve feedback die acties vereist.</span><span class="sxs-lookup"><span data-stu-id="18f84-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="18f84-136">Een Azure-functie kan ook worden gebruikt om te doen meer aangepaste rekenservice boven op de gegevens.</span><span class="sxs-lookup"><span data-stu-id="18f84-136">An Azure Function can also be used to do more custom compute on top of the data.</span></span>

## <a name="enriching-the-data-with-an-azure-function"></a><span data-ttu-id="18f84-137">De gegevens met een Azure-functie uit te breiden</span><span class="sxs-lookup"><span data-stu-id="18f84-137">Enriching the data with an Azure Function</span></span>

<span data-ttu-id="18f84-138">Voordat we een functie maken kunt, moeten we hebben een functie-app in ons Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="18f84-138">Before we can create a function, we need to have a function app in our Azure subscription.</span></span>  <span data-ttu-id="18f84-139">Meer informatie over het maken van een Azure-functie in de portal kunnen [hier vinden](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="18f84-139">Details on creating an Azure Function in the portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="18f84-140">Voor een functie moet worden aangeroepen rechtstreeks vanuit een logische app, moet beschikken over een HTTP-binding activeren.</span><span class="sxs-lookup"><span data-stu-id="18f84-140">For a function to be called directly from a logic app, it needs to have an HTTP trigger binding.</span></span>  <span data-ttu-id="18f84-141">Wordt u aangeraden de **HttpTrigger** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="18f84-141">We recommend using the **HttpTrigger** template.</span></span>

<span data-ttu-id="18f84-142">In dit scenario zou de hoofdtekst van de aanvraag van de Azure-functie worden de tweet tekst.</span><span class="sxs-lookup"><span data-stu-id="18f84-142">In this scenario, the request body of the Azure Function would be the tweet text.</span></span>  <span data-ttu-id="18f84-143">In de functiecode gewoon definiëren logica op als de tekst tweet een sleutel woord of woordgroep bevat.</span><span class="sxs-lookup"><span data-stu-id="18f84-143">In the function code, simply define logic on if the tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="18f84-144">De functie zelf kan worden gehouden zo eenvoudig of complex zo nodig voor het scenario.</span><span class="sxs-lookup"><span data-stu-id="18f84-144">The function itself could be kept as simple or complex as needed for the scenario.</span></span>

<span data-ttu-id="18f84-145">Aan het einde van de functie moet u gewoon een antwoord naar de logische app met enkele gegevens retourneren.</span><span class="sxs-lookup"><span data-stu-id="18f84-145">At the end of the function, simply return a response to the logic app with some data.</span></span>  <span data-ttu-id="18f84-146">Dit kan zijn van een eenvoudige Booleaanse waarde (bijvoorbeeld `containsKeyword`), of een complex object.</span><span class="sxs-lookup"><span data-stu-id="18f84-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![Geconfigureerde Azure-functie stap][2]

> [!TIP]
> <span data-ttu-id="18f84-148">Bij het openen van een complexe antwoord van een functie in een logische app, moet u de actie parseren JSON gebruiken.</span><span class="sxs-lookup"><span data-stu-id="18f84-148">When accessing a complex response from a function in a logic app, use the Parse JSON action.</span></span>

<span data-ttu-id="18f84-149">Wanneer de functie is opgeslagen, kan worden toegevoegd in de logische app die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="18f84-149">Once the function is saved, it can be added into the logic app created above.</span></span>  <span data-ttu-id="18f84-150">In de logische app:</span><span class="sxs-lookup"><span data-stu-id="18f84-150">In the logic app:</span></span>

1. <span data-ttu-id="18f84-151">Klik hier om een **nieuwe stap**</span><span class="sxs-lookup"><span data-stu-id="18f84-151">Click to add a **New Step**</span></span>
1. <span data-ttu-id="18f84-152">Selecteer de **Azure Functions** connector</span><span class="sxs-lookup"><span data-stu-id="18f84-152">Select the **Azure Functions** connector</span></span>
1. <span data-ttu-id="18f84-153">Selecteer een bestaande functie kiezen en blader naar de functie gemaakt</span><span class="sxs-lookup"><span data-stu-id="18f84-153">Select to choose an existing function, and browse to the function created</span></span>
1. <span data-ttu-id="18f84-154">Verzenden in de **Tweet tekst** voor de **aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="18f84-154">Send in the **Tweet Text** for the **Request Body**</span></span>

## <a name="running-and-monitoring-the-solution"></a><span data-ttu-id="18f84-155">Controleert de oplossing</span><span class="sxs-lookup"><span data-stu-id="18f84-155">Running and monitoring the solution</span></span>

<span data-ttu-id="18f84-156">Een van de voordelen van het ontwerpen van zonder Server integraties in Logic Apps is de uitgebreide foutopsporing en mogelijkheden voor bewaking.</span><span class="sxs-lookup"><span data-stu-id="18f84-156">One of the benefits of authoring serverless orchestrations in Logic Apps is the rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="18f84-157">Alle uitvoeren (huidige of historische) kan worden weergegeven uit in Visual Studio de Azure-portal of via de REST-API en SDK's.</span><span class="sxs-lookup"><span data-stu-id="18f84-157">Any run (current or historic) can be viewed from within Visual Studio, the Azure portal, or via the REST API and SDKs.</span></span>

<span data-ttu-id="18f84-158">Een van de eenvoudigste manieren voor het testen van een logische app gebruikt de **uitvoeren** knop in de ontwerpfunctie.</span><span class="sxs-lookup"><span data-stu-id="18f84-158">One of the easiest ways to test a logic app is using the **Run** button in the designer.</span></span>  <span data-ttu-id="18f84-159">Te klikken op **uitvoeren** , blijven de trigger pollen om de vijf seconden totdat een gebeurtenis wordt gedetecteerd en de voortgang van de uitvoering van een actuele weergave zoveel.</span><span class="sxs-lookup"><span data-stu-id="18f84-159">Clicking **Run** will continue to poll the trigger every 5 seconds until an event is detected, and give a live view as the run progresses.</span></span>

<span data-ttu-id="18f84-160">Geschiedenis van vorige uitvoering kunnen worden weergegeven op de overzichtsblade in de Azure portal of met behulp van Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="18f84-160">Previous run histories can be viewed on the Overview blade in the Azure portal, or using the Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="18f84-161">Maken van een implementatiesjabloon voor geautomatiseerde implementaties</span><span class="sxs-lookup"><span data-stu-id="18f84-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="18f84-162">Zodra een oplossing is ontwikkeld, kan deze worden vastgelegd en geïmplementeerd via een Azure-implementatie-sjabloon naar een Azure-regio in de hele wereld.</span><span class="sxs-lookup"><span data-stu-id="18f84-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template to any Azure region in the world.</span></span>  <span data-ttu-id="18f84-163">Dit is handig voor beide wijzigen parameters voor verschillende versies van deze werkstroom, maar ook voor het integreren van deze oplossing in een pijplijn build en release.</span><span class="sxs-lookup"><span data-stu-id="18f84-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="18f84-164">Informatie over het maken van een sjabloon voor de implementatie vindt [in dit artikel](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="18f84-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="18f84-165">Azure Functions kunnen ook worden opgenomen in de sjabloon voor de implementatie - zodat de volledige oplossing met alle afhankelijkheden kan worden beheerd als één sjabloon.</span><span class="sxs-lookup"><span data-stu-id="18f84-165">Azure Functions can also be incorporated in the deployment template - so the entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="18f84-166">Een voorbeeld van een functie-implementatiesjabloon vindt u in de [Azure quickstart sjabloon opslagplaats](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span><span class="sxs-lookup"><span data-stu-id="18f84-166">An example of a function deployment template can be found in the [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18f84-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18f84-167">Next steps</span></span>

* [<span data-ttu-id="18f84-168">Zie andere voorbeelden en scenario's voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="18f84-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="18f84-169">Bekijk een videowalkthrough over het maken van deze oplossing voor end-to-end</span><span class="sxs-lookup"><span data-stu-id="18f84-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="18f84-170">Informatie over het verwerken en uitzonderingen in een logische app catch</span><span class="sxs-lookup"><span data-stu-id="18f84-170">Learn how to handle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png