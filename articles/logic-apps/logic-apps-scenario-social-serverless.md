---
title: aaaScenario - Maak een klant insights dashboard met Azure zonder server | Microsoft Docs
description: Een voorbeeld van hoe u een dashboard toomanage klant feedback, sociale gegevens en meer met Azure Logic Apps en Azure Functions samenstellen kunt.
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
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="eb47c-103">Een realtime klant insights dashboard maken met Azure Logic Apps en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="eb47c-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="eb47c-104">Azure zonder Server-hulpprogramma's bieden krachtige mogelijkheden tooquickly build en host toepassingen in de cloud Hallo, zonder toothink over infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="eb47c-104">Azure Serverless tools provide powerful capabilities tooquickly build and host applications in hello cloud, without having toothink about infrastructure.</span></span>  <span data-ttu-id="eb47c-105">In dit scenario wordt er een tootrigger dashboard maken op feedback van klanten, feedback met machine learning analyseren en insights publiceren een bron, zoals Power BI of Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="eb47c-105">In this scenario, we will create a dashboard tootrigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-hello-scenario-and-tools-used"></a><span data-ttu-id="eb47c-106">Overzicht van scenario Hallo en hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="eb47c-106">Overview of hello scenario and tools used</span></span>

<span data-ttu-id="eb47c-107">In deze oplossing voor tooimplement order, we maken gebruik van Hallo twee belangrijke onderdelen van zonder server apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) en [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="eb47c-107">In order tooimplement this solution, we will leverage hello two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="eb47c-108">Logic Apps is een zonder server werkstroomengine in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="eb47c-108">Logic Apps is a serverless workflow engine in hello cloud.</span></span>  <span data-ttu-id="eb47c-109">Het biedt orchestration voor zonder Server-onderdelen en ook verbindt tooover 100 services en API's.</span><span class="sxs-lookup"><span data-stu-id="eb47c-109">It provides orchestration across serverless components, and also connects tooover 100 services and APIs.</span></span>  <span data-ttu-id="eb47c-110">We gaan een logic app tootrigger op feedback van klanten maken voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="eb47c-110">For this scenario, we will create a logic app tootrigger on feedback from customers.</span></span>  <span data-ttu-id="eb47c-111">Hallo-connectors die bij het kruisreagerende toocustomer feedback helpen kunnen onder andere Outlook.com, Office 365, enquête Monkey, Twitter en een HTTP-aanvraag [van een webformulier](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span><span class="sxs-lookup"><span data-stu-id="eb47c-111">Some of hello connectors that can assist in reacting toocustomer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="eb47c-112">Hallo-werkstroom hieronder, wordt er een hashtag op Twitter bewaken.</span><span class="sxs-lookup"><span data-stu-id="eb47c-112">For hello workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="eb47c-113">Functies bieden zonder server compute in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="eb47c-113">Functions provide serverless compute in hello cloud.</span></span>  <span data-ttu-id="eb47c-114">In dit scenario gebruiken we Azure Functions tooflag tweets van klanten op basis van een reeks vooraf gedefinieerde sleutel woorden.</span><span class="sxs-lookup"><span data-stu-id="eb47c-114">In this scenario, we will use Azure Functions tooflag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="eb47c-115">de volledige oplossing Hallo kan worden [bouwen in Visual Studio](logic-apps-deploy-from-vs.md) en [geïmplementeerd als onderdeel van een sjabloon resource](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="eb47c-115">hello entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="eb47c-116">Er is ook video-overzicht van scenario Hallo [op Channel 9](http://aka.ms/logicappsdemo).</span><span class="sxs-lookup"><span data-stu-id="eb47c-116">There is also video walkthrough of hello scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a><span data-ttu-id="eb47c-117">Hallo logic app tootrigger bouwen op klantgegevens</span><span class="sxs-lookup"><span data-stu-id="eb47c-117">Build hello logic app tootrigger on customer data</span></span>

<span data-ttu-id="eb47c-118">Na [maken van een logische app](logic-apps-create-a-logic-app.md) in Visual Studio of hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="eb47c-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or hello Azure portal:</span></span>

1. <span data-ttu-id="eb47c-119">Toevoegen van een trigger voor **op nieuwe Tweets** van Twitter</span><span class="sxs-lookup"><span data-stu-id="eb47c-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="eb47c-120">Hallo trigger toolisten tootweets configureren op een sleutelwoord of hashtag.</span><span class="sxs-lookup"><span data-stu-id="eb47c-120">Configure hello trigger toolisten tootweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="eb47c-121">Hallo terugkeerpatroon eigenschap op Hallo trigger wordt bepaald hoe vaak Hallo logische app controleert op nieuwe items op triggers op basis van polling</span><span class="sxs-lookup"><span data-stu-id="eb47c-121">hello recurrence property on hello trigger will determine how frequently hello logic app checks for new items on polling-based triggers</span></span>

   ![Voorbeeld van een trigger Twitter][1]

<span data-ttu-id="eb47c-123">Deze app wordt nu gestart op alle nieuwe tweets.</span><span class="sxs-lookup"><span data-stu-id="eb47c-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="eb47c-124">We kunnen vervolgens worden die gegevens tweet en meer Hallo gevoel uitgedrukt inzicht in.</span><span class="sxs-lookup"><span data-stu-id="eb47c-124">We can then take that tweet data and understand more of hello sentiment expressed.</span></span>  <span data-ttu-id="eb47c-125">Voor deze gebruiken we Hallo [Azure cognitieve Service](https://azure.microsoft.com/services/cognitive-services/) toodetect gevoel van tekst.</span><span class="sxs-lookup"><span data-stu-id="eb47c-125">For this we use hello [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) toodetect sentiment of text.</span></span>

1. <span data-ttu-id="eb47c-126">Klik op **nieuwe stap**</span><span class="sxs-lookup"><span data-stu-id="eb47c-126">Click **New Step**</span></span>
1. <span data-ttu-id="eb47c-127">Selecteer of zoek naar Hallo **Tekstanalyse** connector</span><span class="sxs-lookup"><span data-stu-id="eb47c-127">Select or search for hello **Text Analytics** connector</span></span>
1. <span data-ttu-id="eb47c-128">Selecteer Hallo **detecteren gevoel** bewerking</span><span class="sxs-lookup"><span data-stu-id="eb47c-128">Select hello **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="eb47c-129">Als u wordt gevraagd, geeft u een geldige sleutel cognitieve Services voor Hallo Text Analytics-service</span><span class="sxs-lookup"><span data-stu-id="eb47c-129">If prompted, provide a valid Cognitive Services key for hello Text Analytics service</span></span>
1. <span data-ttu-id="eb47c-130">Hallo toevoegen **Tweet tekst** als tekst tooanalyze Hallo.</span><span class="sxs-lookup"><span data-stu-id="eb47c-130">Add hello **Tweet Text** as hello text tooanalyze.</span></span>

<span data-ttu-id="eb47c-131">Nu dat we Hallo tweet gegevens en inzichten op Hallo tweet hebt, kan een aantal andere connectors relevant zijn:</span><span class="sxs-lookup"><span data-stu-id="eb47c-131">Now that we have hello tweet data, and insights on hello tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="eb47c-132">Power BI - rijen tooStreaming gegevensset toevoegen: weergave tweets realtime op een Power BI-dashboard.</span><span class="sxs-lookup"><span data-stu-id="eb47c-132">Power BI - Add Rows tooStreaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="eb47c-133">Azure Data Lake - bestand toevoegen: gegevensset tooinclude van klant gegevens tooan Azure Data Lake analytics-taken toevoegen.</span><span class="sxs-lookup"><span data-stu-id="eb47c-133">Azure Data Lake - Append file: Add customer data tooan Azure Data Lake dataset tooinclude in analytics jobs.</span></span>
* <span data-ttu-id="eb47c-134">SQL - rijen toevoegen: opslaan van gegevens in een database voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="eb47c-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="eb47c-135">Vertraging - bericht verzenden: waarschuwing van een ongebruikt kanaal op negatieve feedback die acties vereist.</span><span class="sxs-lookup"><span data-stu-id="eb47c-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="eb47c-136">Een Azure-functie kan ook worden gebruikt toodo meer aangepaste compute boven op het Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="eb47c-136">An Azure Function can also be used toodo more custom compute on top of hello data.</span></span>

## <a name="enriching-hello-data-with-an-azure-function"></a><span data-ttu-id="eb47c-137">Hallo-gegevens uit te breiden met een Azure-functie</span><span class="sxs-lookup"><span data-stu-id="eb47c-137">Enriching hello data with an Azure Function</span></span>

<span data-ttu-id="eb47c-138">Voordat we een functie maken kunt, moeten we toohave een functie-app in ons Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="eb47c-138">Before we can create a function, we need toohave a function app in our Azure subscription.</span></span>  <span data-ttu-id="eb47c-139">Meer informatie over het maken van een Azure-functie in de portal Hallo kunnen [hier vinden](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="eb47c-139">Details on creating an Azure Function in hello portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="eb47c-140">Voor een functie toobe aangeroepen rechtstreeks vanuit een logische app, het moet een HTTP toohave activeren binding.</span><span class="sxs-lookup"><span data-stu-id="eb47c-140">For a function toobe called directly from a logic app, it needs toohave an HTTP trigger binding.</span></span>  <span data-ttu-id="eb47c-141">Aangeraden wordt Hallo **HttpTrigger** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="eb47c-141">We recommend using hello **HttpTrigger** template.</span></span>

<span data-ttu-id="eb47c-142">In dit scenario zou aanvraagtekst Hallo Hallo Azure-functie Hallo tweet tekst zijn.</span><span class="sxs-lookup"><span data-stu-id="eb47c-142">In this scenario, hello request body of hello Azure Function would be hello tweet text.</span></span>  <span data-ttu-id="eb47c-143">In de functiecode hello, gewoon definiëren logica op als Hallo tweet tekst een sleutel woord of woordgroep bevat.</span><span class="sxs-lookup"><span data-stu-id="eb47c-143">In hello function code, simply define logic on if hello tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="eb47c-144">Hallo-functie zelf kan worden gehouden zo eenvoudig of complex zo nodig voor Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="eb47c-144">hello function itself could be kept as simple or complex as needed for hello scenario.</span></span>

<span data-ttu-id="eb47c-145">Aan het einde van de Hallo van Hallo-functie, moet u gewoon een antwoord toohello logische app met enkele gegevens retourneren.</span><span class="sxs-lookup"><span data-stu-id="eb47c-145">At hello end of hello function, simply return a response toohello logic app with some data.</span></span>  <span data-ttu-id="eb47c-146">Dit kan zijn van een eenvoudige Booleaanse waarde (bijvoorbeeld `containsKeyword`), of een complex object.</span><span class="sxs-lookup"><span data-stu-id="eb47c-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![Geconfigureerde Azure-functie stap][2]

> [!TIP]
> <span data-ttu-id="eb47c-148">Bij het openen van een complexe antwoord van een functie in een logische app, moet u Hallo parseren JSON actie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eb47c-148">When accessing a complex response from a function in a logic app, use hello Parse JSON action.</span></span>

<span data-ttu-id="eb47c-149">Wanneer de functie Hallo is opgeslagen, kan worden toegevoegd in Hallo logische app die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eb47c-149">Once hello function is saved, it can be added into hello logic app created above.</span></span>  <span data-ttu-id="eb47c-150">In Hallo logische app:</span><span class="sxs-lookup"><span data-stu-id="eb47c-150">In hello logic app:</span></span>

1. <span data-ttu-id="eb47c-151">Klik op tooadd een **nieuwe stap**</span><span class="sxs-lookup"><span data-stu-id="eb47c-151">Click tooadd a **New Step**</span></span>
1. <span data-ttu-id="eb47c-152">Selecteer Hallo **Azure Functions** connector</span><span class="sxs-lookup"><span data-stu-id="eb47c-152">Select hello **Azure Functions** connector</span></span>
1. <span data-ttu-id="eb47c-153">Selecteer een bestaande functie toochoose en blader toohello functie gemaakt</span><span class="sxs-lookup"><span data-stu-id="eb47c-153">Select toochoose an existing function, and browse toohello function created</span></span>
1. <span data-ttu-id="eb47c-154">Verzenden in Hallo **Tweet tekst** voor Hallo **aanvraagtekst**</span><span class="sxs-lookup"><span data-stu-id="eb47c-154">Send in hello **Tweet Text** for hello **Request Body**</span></span>

## <a name="running-and-monitoring-hello-solution"></a><span data-ttu-id="eb47c-155">Controleert Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="eb47c-155">Running and monitoring hello solution</span></span>

<span data-ttu-id="eb47c-156">Een van de voordelen van het ontwerpen van zonder Server integraties in Logic Apps Hallo is Hallo uitgebreide foutopsporing en bewakingsmogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="eb47c-156">One of hello benefits of authoring serverless orchestrations in Logic Apps is hello rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="eb47c-157">Alle uitvoeren (huidige of historische) kan worden weergegeven uit in Visual Studio hello Azure-portal of via SDK's en Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="eb47c-157">Any run (current or historic) can be viewed from within Visual Studio, hello Azure portal, or via hello REST API and SDKs.</span></span>

<span data-ttu-id="eb47c-158">Een van de Hallo eenvoudigste manieren tootest een logische app gebruikt Hallo **uitvoeren** knop in Hallo designer.</span><span class="sxs-lookup"><span data-stu-id="eb47c-158">One of hello easiest ways tootest a logic app is using hello **Run** button in hello designer.</span></span>  <span data-ttu-id="eb47c-159">Te klikken op **uitvoeren** gaan toopoll Hallo-trigger om de vijf seconden totdat een gebeurtenis wordt gedetecteerd en een actuele weergave geven tijdens de voortgang van de Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="eb47c-159">Clicking **Run** will continue toopoll hello trigger every 5 seconds until an event is detected, and give a live view as hello run progresses.</span></span>

<span data-ttu-id="eb47c-160">Geschiedenis van vorige uitvoering kunnen worden weergegeven op de overzichtsblade Hallo in hello Azure-portal of met behulp van Visual Studio Cloud Explorer Hallo.</span><span class="sxs-lookup"><span data-stu-id="eb47c-160">Previous run histories can be viewed on hello Overview blade in hello Azure portal, or using hello Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="eb47c-161">Maken van een implementatiesjabloon voor geautomatiseerde implementaties</span><span class="sxs-lookup"><span data-stu-id="eb47c-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="eb47c-162">Zodra een oplossing is ontwikkeld, kan deze worden vastgelegd en geïmplementeerd via een Azure-implementatie sjabloon tooany Azure-regio in Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="eb47c-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template tooany Azure region in hello world.</span></span>  <span data-ttu-id="eb47c-163">Dit is handig voor beide wijzigen parameters voor verschillende versies van deze werkstroom, maar ook voor het integreren van deze oplossing in een pijplijn build en release.</span><span class="sxs-lookup"><span data-stu-id="eb47c-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="eb47c-164">Informatie over het maken van een sjabloon voor de implementatie vindt [in dit artikel](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="eb47c-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="eb47c-165">Azure Functions kunnen ook worden opgenomen in de implementatiesjabloon Hallo - zodat de volledige oplossing Hallo met alle afhankelijkheden kan worden beheerd als één sjabloon.</span><span class="sxs-lookup"><span data-stu-id="eb47c-165">Azure Functions can also be incorporated in hello deployment template - so hello entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="eb47c-166">Een voorbeeld van een functie-implementatiesjabloon vindt u in Hallo [Azure quickstart sjabloon opslagplaats](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span><span class="sxs-lookup"><span data-stu-id="eb47c-166">An example of a function deployment template can be found in hello [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb47c-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eb47c-167">Next steps</span></span>

* [<span data-ttu-id="eb47c-168">Zie andere voorbeelden en scenario's voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="eb47c-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="eb47c-169">Bekijk een videowalkthrough over het maken van deze oplossing voor end-to-end</span><span class="sxs-lookup"><span data-stu-id="eb47c-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="eb47c-170">Meer informatie over hoe toohandle en catch uitzonderingen in een logische app</span><span class="sxs-lookup"><span data-stu-id="eb47c-170">Learn how toohandle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png