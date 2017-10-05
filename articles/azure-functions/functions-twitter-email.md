---
title: "Maken van een functie die kan worden geïntegreerd met Azure Logic Apps | Microsoft Docs"
description: "Maak een functie die kan worden geïntegreerd met Azure Logic Apps en cognitieve Azure-Services tweet gevoel categoriseren en meldingen verzenden wanneer gevoel slecht is."
services: functions, logic-apps, cognitive-services
keywords: werkstroom, cloud-apps, cloudservices, bedrijfsprocessen, systeemintegratie, enterprise application integration, EAI
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 4a5dc668e21c5328b308c8f5852aaa922232374d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="b9067-104">Maken van een functie die kan worden geïntegreerd met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b9067-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="b9067-105">Azure Functions integreert met Azure Logic Apps in de ontwerpfunctie voor Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="b9067-105">Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer.</span></span> <span data-ttu-id="b9067-106">Deze integratie kunt u de verwerkingskracht van functies in integraties met andere Azure en services van derden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9067-106">This integration lets you use the computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="b9067-107">Deze zelfstudie ziet u het gebruik van functies met Logic Apps en cognitieve Azure-Services voor het analyseren van gevoel uit Twitter-berichten.</span><span class="sxs-lookup"><span data-stu-id="b9067-107">This tutorial shows you how to use Functions with Logic Apps and Azure Cognitive Services to analyze sentiment from Twitter posts.</span></span> <span data-ttu-id="b9067-108">Een functie HTTP geactiveerd categoriseert tweets als groen, geel of rood op basis van de score gevoel.</span><span class="sxs-lookup"><span data-stu-id="b9067-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.</span></span> <span data-ttu-id="b9067-109">Een e-mailbericht wordt verzonden wanneer slechte gevoel wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="b9067-109">An email is sent when poor sentiment is detected.</span></span> 

![afbeelding van de eerste twee stappen van de app in App-ontwerper voor logica](media/functions-twitter-email/designer1.png)

<span data-ttu-id="b9067-111">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="b9067-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b9067-112">Maak een cognitieve Services-account.</span><span class="sxs-lookup"><span data-stu-id="b9067-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="b9067-113">Maak een functie die tweet gevoel ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="b9067-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="b9067-114">Maak een logische app die is verbonden met Twitter.</span><span class="sxs-lookup"><span data-stu-id="b9067-114">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="b9067-115">Detectie van gevoel toevoegen aan de logische app.</span><span class="sxs-lookup"><span data-stu-id="b9067-115">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="b9067-116">De logische app verbinden met de functie.</span><span class="sxs-lookup"><span data-stu-id="b9067-116">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="b9067-117">Stuur een e-mail op basis van het antwoord van de functie.</span><span class="sxs-lookup"><span data-stu-id="b9067-117">Send an email based on the response from the function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9067-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b9067-118">Prerequisites</span></span>

+ <span data-ttu-id="b9067-119">Een actieve [Twitter](https://twitter.com/) account.</span><span class="sxs-lookup"><span data-stu-id="b9067-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="b9067-120">Een [Outlook.com](https://outlook.com/) account (voor het verzenden van meldingen).</span><span class="sxs-lookup"><span data-stu-id="b9067-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="b9067-121">Als startpunt van dit onderwerp dienen de resources die zijn gemaakt in [Create your first function from the Azure portal](functions-create-first-azure-function.md) (Uw eerste functie maken vanuit Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="b9067-121">This topic uses as its starting point the resources created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="b9067-122">Als u dit nog niet hebt gedaan, moet u deze stappen nu voltooien om uw functie-app te maken.</span><span class="sxs-lookup"><span data-stu-id="b9067-122">If you haven't already done so, complete these steps now to create your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="b9067-123">Een cognitieve Services-account maken</span><span class="sxs-lookup"><span data-stu-id="b9067-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="b9067-124">Een cognitieve Services-account is vereist voor het detecteren van de gevoel tweets wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="b9067-124">A Cognitive Services account is required to detect the sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="b9067-125">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b9067-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="b9067-126">Klik op de knop **Nieuw** in de linkerbovenhoek van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b9067-126">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="b9067-127">Klik op **gegevens en analyse** > **cognitieve Services**.</span><span class="sxs-lookup"><span data-stu-id="b9067-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="b9067-128">Vervolgens gebruikt u de instellingen die zijn opgegeven in de tabel en controleer de voorwaarden accepteren **vastmaken aan dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b9067-128">Then, use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Blade cognitieve account maken](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="b9067-130">Instelling</span><span class="sxs-lookup"><span data-stu-id="b9067-130">Setting</span></span>      |  <span data-ttu-id="b9067-131">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="b9067-131">Suggested value</span></span>   | <span data-ttu-id="b9067-132">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9067-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="b9067-133">**Naam**</span><span class="sxs-lookup"><span data-stu-id="b9067-133">**Name**</span></span> | <span data-ttu-id="b9067-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="b9067-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="b9067-135">Kies een unieke naam.</span><span class="sxs-lookup"><span data-stu-id="b9067-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="b9067-136">**API-type**</span><span class="sxs-lookup"><span data-stu-id="b9067-136">**API type**</span></span> | <span data-ttu-id="b9067-137">Tekstanalyse-API</span><span class="sxs-lookup"><span data-stu-id="b9067-137">Text Analytics API</span></span> | <span data-ttu-id="b9067-138">API gebruikt voor het analyseren van tekst.</span><span class="sxs-lookup"><span data-stu-id="b9067-138">API used to analyze text.</span></span>  |
    | <span data-ttu-id="b9067-139">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="b9067-139">**Location**</span></span> | <span data-ttu-id="b9067-140">VS - west</span><span class="sxs-lookup"><span data-stu-id="b9067-140">West US</span></span> | <span data-ttu-id="b9067-141">Op dit moment alleen **VS-West** is beschikbaar voor tekstanalyse.</span><span class="sxs-lookup"><span data-stu-id="b9067-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="b9067-142">**Prijscategorie**</span><span class="sxs-lookup"><span data-stu-id="b9067-142">**Pricing tier**</span></span> | <span data-ttu-id="b9067-143">F0</span><span class="sxs-lookup"><span data-stu-id="b9067-143">F0</span></span> | <span data-ttu-id="b9067-144">Beginnen met de laagste categorie.</span><span class="sxs-lookup"><span data-stu-id="b9067-144">Start with the lowest tier.</span></span> <span data-ttu-id="b9067-145">Als u buiten aanroepen uitvoert, kan worden uitgebreid naar een hogere laag.</span><span class="sxs-lookup"><span data-stu-id="b9067-145">If you run out of calls, scale to a higher tier.</span></span>|
    | <span data-ttu-id="b9067-146">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="b9067-146">**Resource group**</span></span> | <span data-ttu-id="b9067-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b9067-147">myResourceGroup</span></span> | <span data-ttu-id="b9067-148">Gebruik dezelfde resourcegroep voor alle services in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b9067-148">Use the same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="b9067-149">Klik op **maken** om uw account te maken.</span><span class="sxs-lookup"><span data-stu-id="b9067-149">Click **Create** to create your account.</span></span> <span data-ttu-id="b9067-150">Nadat het account is gemaakt, klikt u op uw nieuwe cognitieve Services-account hebt vastgemaakt aan het dashboard.</span><span class="sxs-lookup"><span data-stu-id="b9067-150">After the account is created, click your new Cognitive Services account pinned to the dashboard.</span></span> 

5. <span data-ttu-id="b9067-151">Klik in het account op **sleutels**, en kopieert u de waarde van **Key 1** en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="b9067-151">In the account, click **Keys**, and then copy the value of **Key 1** and save it.</span></span> <span data-ttu-id="b9067-152">U gebruikt deze sleutel voor de logische app verbinding met uw cognitieve Services-account.</span><span class="sxs-lookup"><span data-stu-id="b9067-152">You use this key to connect the logic app to your Cognitive Services account.</span></span> 
 
    ![Sleutels](media/functions-twitter-email/keys.png)

## <a name="create-the-function"></a><span data-ttu-id="b9067-154">De functie maken</span><span class="sxs-lookup"><span data-stu-id="b9067-154">Create the function</span></span>

<span data-ttu-id="b9067-155">Functies biedt een uitstekende manier om de offload van taken in een werkstroom van logic apps.</span><span class="sxs-lookup"><span data-stu-id="b9067-155">Functions provides a great way to offload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="b9067-156">Deze zelfstudie gebruikt een functie HTTP is geactiveerd voor het verwerken van tweet gevoel scores van cognitieve Services en een categoriewaarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="b9067-156">This tutorial uses an HTTP triggered function to process tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="b9067-157">Vouw de functie-app, klikt u op de  **+**  naast **functies**, klikt u op de **HTTPTrigger** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b9067-157">Expand your function app, click the **+** button next to **Functions**, click the **HTTPTrigger** template.</span></span> <span data-ttu-id="b9067-158">Type `CategorizeSentiment` voor de functie **naam** en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="b9067-158">Type `CategorizeSentiment` for the function **Name** and click **Create**.</span></span>

    ![Functie Apps blade functies +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="b9067-160">De inhoud van het bestand run.csx vervangen door de volgende code en klik vervolgens op **opslaan**:</span><span class="sxs-lookup"><span data-stu-id="b9067-160">Replace the contents of the run.csx file with the following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="b9067-161">Deze functiecode retourneert een kleurcategorie op basis van de gevoel score ontvangen in de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b9067-161">This function code returns a color category based on the sentiment score received in the request.</span></span> 

3. <span data-ttu-id="b9067-162">U kunt de functie testen, klikt u op **testen** helemaal rechts op het tabblad testresultaten uitbreiden. Typ een waarde van `0.2` voor de **aanvraagtekst**, en klik vervolgens op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="b9067-162">To test the function, click **Test** at the far right to expand the Test tab. Type a value of `0.2` for the **Request body**, and then click **Run**.</span></span> <span data-ttu-id="b9067-163">Een waarde van **rood** in de hoofdtekst van het antwoord wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b9067-163">A value of **RED** is returned in the body of the response.</span></span> 

    ![De functie testen in de Azure portal](./media/functions-twitter-email/test.png)

<span data-ttu-id="b9067-165">U hebt nu een functie die gevoel scores ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="b9067-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="b9067-166">Vervolgens kunt u een logische app, die de functie kan worden geïntegreerd met uw accounts Twitter en cognitieve Services maken.</span><span class="sxs-lookup"><span data-stu-id="b9067-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="b9067-167">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="b9067-167">Create a logic app</span></span>   

1. <span data-ttu-id="b9067-168">Klik in de Azure-portal op de **nieuw** knop gevonden in de linkerbovenhoek van de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b9067-168">In the Azure portal, click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="b9067-169">Klik op **Enterprise Integration** > **logische App**.</span><span class="sxs-lookup"><span data-stu-id="b9067-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="b9067-170">Vervolgens gebruikt u de instellingen die zijn opgegeven in de tabel, selectievakje **vastmaken aan dashboard**, en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="b9067-170">Then, use the settings as specified in the table, check **Pin to dashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="b9067-171">Typ een **naam** zoals `TweetSentiment`, gebruik van de instellingen die zijn opgegeven in de tabel, accepteer de voorwaarden en Controleer **vastmaken aan dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b9067-171">Then, type a **Name** like `TweetSentiment`,  use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Logische app maken in de Azure portal](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="b9067-173">Instelling</span><span class="sxs-lookup"><span data-stu-id="b9067-173">Setting</span></span>      |  <span data-ttu-id="b9067-174">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="b9067-174">Suggested value</span></span>   | <span data-ttu-id="b9067-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9067-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="b9067-176">**Naam**</span><span class="sxs-lookup"><span data-stu-id="b9067-176">**Name**</span></span> | <span data-ttu-id="b9067-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="b9067-177">TweetSentiment</span></span> | <span data-ttu-id="b9067-178">Kies een passende naam voor uw app.</span><span class="sxs-lookup"><span data-stu-id="b9067-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="b9067-179">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="b9067-179">**Resource group**</span></span> | <span data-ttu-id="b9067-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b9067-180">myResourceGroup</span></span> | <span data-ttu-id="b9067-181">API gebruikt voor het analyseren van tekst.</span><span class="sxs-lookup"><span data-stu-id="b9067-181">API used to analyze text.</span></span>  |
    | <span data-ttu-id="b9067-182">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="b9067-182">**Location**</span></span> | <span data-ttu-id="b9067-183">VS - oost</span><span class="sxs-lookup"><span data-stu-id="b9067-183">East US</span></span> | <span data-ttu-id="b9067-184">Kies een locatie dicht bij u.</span><span class="sxs-lookup"><span data-stu-id="b9067-184">Choose a location close to you.</span></span> |
    | <span data-ttu-id="b9067-185">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="b9067-185">**Resource group**</span></span> | <span data-ttu-id="b9067-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b9067-186">myResourceGroup</span></span> | <span data-ttu-id="b9067-187">Kies dezelfde bestaande resourcegroep als voor.</span><span class="sxs-lookup"><span data-stu-id="b9067-187">Choose the same existing resource group as before.</span></span>|

4. <span data-ttu-id="b9067-188">Klik op **maken** uw logische app maken.</span><span class="sxs-lookup"><span data-stu-id="b9067-188">Click **Create** to create your logic app.</span></span> <span data-ttu-id="b9067-189">Nadat de app is gemaakt, klikt u op de nieuwe logische app vastgemaakt aan het dashboard.</span><span class="sxs-lookup"><span data-stu-id="b9067-189">After the app is created, click your new logic app pinned to the dashboard.</span></span> <span data-ttu-id="b9067-190">Klik in de ontwerpfunctie voor Logic Apps, schuif naar beneden en klikt u op de **lege logische App** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b9067-190">Then in the Logic Apps Designer, scroll down and click the **Blank Logic App** template.</span></span> 

    ![Lege Logic Apps-sjabloon](media/functions-twitter-email/blank.png)

<span data-ttu-id="b9067-192">U kunt nu de ontwerpfunctie van Logic Apps services en triggers toevoegt aan uw app.</span><span class="sxs-lookup"><span data-stu-id="b9067-192">You can now use the Logic Apps Designer to add services and triggers to your app.</span></span>

## <a name="connect-to-twitter"></a><span data-ttu-id="b9067-193">Verbinding maken met Twitter</span><span class="sxs-lookup"><span data-stu-id="b9067-193">Connect to Twitter</span></span>

<span data-ttu-id="b9067-194">Maak eerst een verbinding met uw Twitter-account.</span><span class="sxs-lookup"><span data-stu-id="b9067-194">First, create a connection to your Twitter account.</span></span> <span data-ttu-id="b9067-195">De logische app worden opgevraagd op tweets die worden uitgevoerd met de app te activeren.</span><span class="sxs-lookup"><span data-stu-id="b9067-195">The logic app polls for tweets, which trigger the app to run.</span></span>

1. <span data-ttu-id="b9067-196">Klik in de ontwerpfunctie voor de **Twitter** service en klik op de **wanneer een nieuwe tweet wordt gepost** trigger.</span><span class="sxs-lookup"><span data-stu-id="b9067-196">In the designer, click the **Twitter** service, and click the **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="b9067-197">Aanmelden bij uw Twitter-account en autoriseren van Logic Apps om uw account te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9067-197">Sign in to your Twitter account and authorize Logic Apps to use your account.</span></span>

2. <span data-ttu-id="b9067-198">Gebruik de instellingen van de trigger Twitter zoals opgegeven in de tabel.</span><span class="sxs-lookup"><span data-stu-id="b9067-198">Use the Twitter trigger settings as specified in the table.</span></span> 

    ![Instellingen voor Twitter-connector](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="b9067-200">Instelling</span><span class="sxs-lookup"><span data-stu-id="b9067-200">Setting</span></span>      |  <span data-ttu-id="b9067-201">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="b9067-201">Suggested value</span></span>   | <span data-ttu-id="b9067-202">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9067-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="b9067-203">**Zoektekst**</span><span class="sxs-lookup"><span data-stu-id="b9067-203">**Search text**</span></span> | <span data-ttu-id="b9067-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="b9067-204">#Azure</span></span> | <span data-ttu-id="b9067-205">Gebruik een hashtag die populaire voor nieuwe tweets genereren in het gekozen interval.</span><span class="sxs-lookup"><span data-stu-id="b9067-205">Use a hashtag that is popular enough for to generate new tweets in the chosen interval.</span></span> <span data-ttu-id="b9067-206">Wanneer met behulp van de laag gratis en uw hashtag te populair is, kunt u snel van de transacties gebruiken in uw cognitieve Services-account.</span><span class="sxs-lookup"><span data-stu-id="b9067-206">When using the Free tier and your hashtag is too popular, you can quickly use up the transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="b9067-207">**Frequentie**</span><span class="sxs-lookup"><span data-stu-id="b9067-207">**Frequency**</span></span> | <span data-ttu-id="b9067-208">Minuut</span><span class="sxs-lookup"><span data-stu-id="b9067-208">Minute</span></span> | <span data-ttu-id="b9067-209">De frequentie eenheid wordt gebruikt voor het polling-Twitter.</span><span class="sxs-lookup"><span data-stu-id="b9067-209">The frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="b9067-210">**Interval**</span><span class="sxs-lookup"><span data-stu-id="b9067-210">**Interval**</span></span> | <span data-ttu-id="b9067-211">15</span><span class="sxs-lookup"><span data-stu-id="b9067-211">15</span></span> | <span data-ttu-id="b9067-212">De verstreken tijd tussen Twitter-aanvragen in de frequentie eenheden.</span><span class="sxs-lookup"><span data-stu-id="b9067-212">The time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="b9067-213">Klik op **opslaan** verbinding maken met uw Twitter-account.</span><span class="sxs-lookup"><span data-stu-id="b9067-213">Click **Save** to connect to your Twitter account.</span></span> 

<span data-ttu-id="b9067-214">Uw app is nu verbonden met Twitter.</span><span class="sxs-lookup"><span data-stu-id="b9067-214">Now your app is connected to Twitter.</span></span> <span data-ttu-id="b9067-215">Vervolgens maakt verbinding u met tekstanalyse voor het detecteren van de gevoel verzamelde tweets.</span><span class="sxs-lookup"><span data-stu-id="b9067-215">Next, you connect to text analytics to detect the sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="b9067-216">Detectie van gevoel toevoegen</span><span class="sxs-lookup"><span data-stu-id="b9067-216">Add sentiment detection</span></span>

1. <span data-ttu-id="b9067-217">Klik op **nieuwe stap**, en vervolgens **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b9067-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Nieuwe stap, waarna een actie toevoegen](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="b9067-219">In **kiest u een actie**, klikt u op **Tekstanalyse**, en klik vervolgens op de **detecteren gevoel** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="b9067-219">In **Choose an action**, click **Text Analytics**, and then click the **Detect sentiment** action.</span></span>

    ![Gevoel detecteren](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="b9067-221">Typ de naam van een verbinding zoals `MyCognitiveServicesConnection`, plak de sleutel voor uw cognitieve Services-dat u hebt opgeslagen account en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="b9067-221">Type a connection name such as `MyCognitiveServicesConnection`, paste the key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="b9067-222">Klik op **tekst voor het analyseren van** > **Tweet tekst**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b9067-222">Click **Text to analyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Gevoel detecteren](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="b9067-224">Nu gevoel detectie is geconfigureerd, kunt u een verbinding toevoegen aan de functie die de uitvoer van de score gevoel verbruikt.</span><span class="sxs-lookup"><span data-stu-id="b9067-224">Now that sentiment detection is configured, you can add a connection to your function that consumes the sentiment score output.</span></span>

## <a name="connect-sentiment-output-to-your-function"></a><span data-ttu-id="b9067-225">Verbinding maken met gevoel uitvoer van de functie</span><span class="sxs-lookup"><span data-stu-id="b9067-225">Connect sentiment output to your function</span></span>

1. <span data-ttu-id="b9067-226">Klik in de ontwerpfunctie voor Logic Apps **nieuwe stap** > **een actie toevoegen**, en klik vervolgens op **Azure Functions**.</span><span class="sxs-lookup"><span data-stu-id="b9067-226">In the Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="b9067-227">Klik op **kiest u een Azure-functie**, selecteer de **CategorizeSentiment** functie die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b9067-227">Click **Choose an Azure function**, select the **CategorizeSentiment** function you created earlier.</span></span>  

    ![Azure vak voor de functie kiezen met een Azure-functie](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="b9067-229">In **aanvraagtekst**, klikt u op **Score** en vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b9067-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Score](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="b9067-231">De functie wordt nu geactiveerd wanneer een score gevoel wordt verzonden door de logische app.</span><span class="sxs-lookup"><span data-stu-id="b9067-231">Now, your function is triggered when a sentiment score is sent from the logic app.</span></span> <span data-ttu-id="b9067-232">Een kleurcode categorie wordt geretourneerd naar de logische app door de functie.</span><span class="sxs-lookup"><span data-stu-id="b9067-232">A color-coded category is returned to the logic app by the function.</span></span> <span data-ttu-id="b9067-233">Vervolgens voegt u een e-mailbericht dat wordt verzonden als een waarde gevoel van **rood** wordt geretourneerd vanaf de functie.</span><span class="sxs-lookup"><span data-stu-id="b9067-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from the function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="b9067-234">E-mailmeldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="b9067-234">Add email notifications</span></span>

<span data-ttu-id="b9067-235">Het laatste deel van de werkstroom is voor het activeren van een e-mailbericht wanneer de gevoel wordt berekend als _rood_.</span><span class="sxs-lookup"><span data-stu-id="b9067-235">The last part of the workflow is to trigger an email when the sentiment is scored as _RED_.</span></span> <span data-ttu-id="b9067-236">In dit onderwerp gebruikt een Outlook.com-connector.</span><span class="sxs-lookup"><span data-stu-id="b9067-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="b9067-237">U kunt vergelijkbare stappen voor het gebruik van een connector Gmail of Office 365 Outlook uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b9067-237">You can perform similar steps to use a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="b9067-238">Klik in de ontwerpfunctie voor Logic Apps **nieuwe stap** > **een voorwaarde toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b9067-238">In the Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="b9067-239">Klik op **kiest u een waarde**, klikt u vervolgens op **hoofdtekst**.</span><span class="sxs-lookup"><span data-stu-id="b9067-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="b9067-240">Selecteer **gelijk is aan**, klikt u op **kiest u een waarde** en het type `RED`, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b9067-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Een voorwaarde toevoegen aan de logische app.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="b9067-242">In **zo ja, niets doen**, klikt u op **een actie toevoegen**, zoeken naar `outlook.com`, klikt u op **e-mailbericht verzenden**, en meld u aan bij uw account Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="b9067-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in to your Outlook.com account.</span></span>
    
    ![Kies een actie voor de voorwaarde.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="b9067-244">Als u geen een Outlook.com-account hebt, kunt u een andere connector, zoals Gmail of Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="b9067-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="b9067-245">In de **e-mailbericht verzenden** actie, gebruik de e-mailinstellingen als in de tabel opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b9067-245">In the **Send an email** action, use the email settings as specified in the table.</span></span> 

    ![Configureer het e-mailbericht voor het verzenden van een e-actie.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="b9067-247">Instelling</span><span class="sxs-lookup"><span data-stu-id="b9067-247">Setting</span></span>      |  <span data-ttu-id="b9067-248">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="b9067-248">Suggested value</span></span>   | <span data-ttu-id="b9067-249">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9067-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="b9067-250">**Aan**</span><span class="sxs-lookup"><span data-stu-id="b9067-250">**To**</span></span> | <span data-ttu-id="b9067-251">Typ uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="b9067-251">Type your email address</span></span> | <span data-ttu-id="b9067-252">Het e-mailadres dat de melding ontvangt.</span><span class="sxs-lookup"><span data-stu-id="b9067-252">The email address that receives the notification.</span></span> |
    | <span data-ttu-id="b9067-253">**Onderwerp**</span><span class="sxs-lookup"><span data-stu-id="b9067-253">**Subject**</span></span> | <span data-ttu-id="b9067-254">Negatieve tweet gevoel gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="b9067-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="b9067-255">De onderwerpregel van het e-mailmeldingen.</span><span class="sxs-lookup"><span data-stu-id="b9067-255">The subject line of the email notification.</span></span>  |
    | <span data-ttu-id="b9067-256">**Hoofdtekst**</span><span class="sxs-lookup"><span data-stu-id="b9067-256">**Body**</span></span> | <span data-ttu-id="b9067-257">Tweet tekst, locatie</span><span class="sxs-lookup"><span data-stu-id="b9067-257">Tweet text, Location</span></span> | <span data-ttu-id="b9067-258">Klik op de **Tweet tekst** en **locatie** parameters.</span><span class="sxs-lookup"><span data-stu-id="b9067-258">Click the **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="b9067-259">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b9067-259">Click **Save**.</span></span>

<span data-ttu-id="b9067-260">Nu dat de werkstroom voltooid is, kunt u de logische app inschakelen en de functie op het werk ziet.</span><span class="sxs-lookup"><span data-stu-id="b9067-260">Now that the workflow is complete, you can enable the logic app and see the function at work.</span></span>

## <a name="test-the-workflow"></a><span data-ttu-id="b9067-261">De werkstroom testen</span><span class="sxs-lookup"><span data-stu-id="b9067-261">Test the workflow</span></span>

1. <span data-ttu-id="b9067-262">Klik in de ontwerpfunctie voor Logic App **uitvoeren** om de app te starten.</span><span class="sxs-lookup"><span data-stu-id="b9067-262">In the Logic App Designer, click **Run** to start the app.</span></span>

2. <span data-ttu-id="b9067-263">Klik in de linkerkolom **overzicht** voor de status van de logische app.</span><span class="sxs-lookup"><span data-stu-id="b9067-263">In the left column, click **Overview** to see the status of the logic app.</span></span> 
 
    ![Uitvoeringsstatus van Logic app](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="b9067-265">(Optioneel) Klik op een van de wordt uitgevoerd om de details van de uitvoering te bekijken.</span><span class="sxs-lookup"><span data-stu-id="b9067-265">(Optional) Click one of the runs to see details of the execution.</span></span>

4. <span data-ttu-id="b9067-266">Ga naar de functie, bekijk de logboeken en controleert u of gevoel waarden zijn ontvangen en verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b9067-266">Go to your function, view the logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Logboeken van de functie weergeven](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="b9067-268">Wanneer een potentieel negatieve gevoel wordt gedetecteerd, krijgt u een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="b9067-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="b9067-269">Als u een e-mailbericht hebt ontvangen, kunt u de functiecode om terug te keren rood telkens wanneer:</span><span class="sxs-lookup"><span data-stu-id="b9067-269">If you haven't received an email, you can change the function code to return RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="b9067-270">Nadat u hebt gecontroleerd dat e-mailmeldingen, wijzigt u terug naar de oorspronkelijke code:</span><span class="sxs-lookup"><span data-stu-id="b9067-270">After you have verified email notifications, change back to the original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="b9067-271">Nadat u deze zelfstudie hebt voltooid, moet u de logische app uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="b9067-271">After you have completed this tutorial, you should disable the logic app.</span></span> <span data-ttu-id="b9067-272">Door het uitschakelen van de app u voorkomen dat u in rekening gebracht voor uitvoeringen en met behulp van de transacties in uw cognitieve Services-account.</span><span class="sxs-lookup"><span data-stu-id="b9067-272">By disabling the app, you avoid being charged for executions and using up the transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="b9067-273">Nu hebt u gezien hoe eenvoudig het is het integreren van functies in een werkstroom Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="b9067-273">Now you have seen how easy it is to integrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-the-logic-app"></a><span data-ttu-id="b9067-274">De logische app uitschakelen</span><span class="sxs-lookup"><span data-stu-id="b9067-274">Disable the logic app</span></span>

<span data-ttu-id="b9067-275">Als u wilt uitschakelen op de logische app, **overzicht** en klik vervolgens op **uitschakelen** aan de bovenkant van het scherm.</span><span class="sxs-lookup"><span data-stu-id="b9067-275">To disable the logic app, click **Overview** and then click **Disable** at the top of the screen.</span></span> <span data-ttu-id="b9067-276">Hierdoor wordt voorkomen dat de logische app uitgevoerd en steeds kosten zonder te verwijderen van de app.</span><span class="sxs-lookup"><span data-stu-id="b9067-276">This stops the logic app from running and incurring charges without deleting the app.</span></span> 

![De functie Logboeken](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="b9067-278">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9067-278">Next steps</span></span>

<span data-ttu-id="b9067-279">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="b9067-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b9067-280">Maak een cognitieve Services-account.</span><span class="sxs-lookup"><span data-stu-id="b9067-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="b9067-281">Maak een functie die tweet gevoel ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="b9067-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="b9067-282">Maak een logische app die is verbonden met Twitter.</span><span class="sxs-lookup"><span data-stu-id="b9067-282">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="b9067-283">Detectie van gevoel toevoegen aan de logische app.</span><span class="sxs-lookup"><span data-stu-id="b9067-283">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="b9067-284">De logische app verbinden met de functie.</span><span class="sxs-lookup"><span data-stu-id="b9067-284">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="b9067-285">Stuur een e-mail op basis van het antwoord van de functie.</span><span class="sxs-lookup"><span data-stu-id="b9067-285">Send an email based on the response from the function.</span></span>

<span data-ttu-id="b9067-286">Ga naar de volgende zelfstudie voor meer informatie over het maken van een zonder Server API voor de functie.</span><span class="sxs-lookup"><span data-stu-id="b9067-286">Advance to the next tutorial to learn how to create a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="b9067-287">Een serverloze API maken met behulp van Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b9067-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="b9067-288">Zie voor meer informatie over Logic Apps, [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b9067-288">To learn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

