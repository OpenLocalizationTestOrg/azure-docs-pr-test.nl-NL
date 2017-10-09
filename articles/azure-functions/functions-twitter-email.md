---
title: "een functie die kan worden geïntegreerd met Azure Logic Apps aaaCreate | Microsoft Docs"
description: "Maken van een functie die kan worden geïntegreerd met Azure Logic Apps en cognitieve Azure-Services toocategorize tweet gevoel en meldingen te verzenden wanneer gevoel slecht is."
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
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="bc443-104">Maken van een functie die kan worden geïntegreerd met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="bc443-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="bc443-105">Azure Functions integreert met Azure Logic Apps in Hallo Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="bc443-105">Azure Functions integrates with Azure Logic Apps in hello Logic Apps Designer.</span></span> <span data-ttu-id="bc443-106">Deze integratie kunt u Hallo rekenkracht van functies in integraties met andere Azure en services van derden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc443-106">This integration lets you use hello computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="bc443-107">Deze zelfstudie leert u hoe toouse functioneert met Logic Apps en cognitieve Azure-Services tooanalyze gevoel uit Twitter-berichten.</span><span class="sxs-lookup"><span data-stu-id="bc443-107">This tutorial shows you how toouse Functions with Logic Apps and Azure Cognitive Services tooanalyze sentiment from Twitter posts.</span></span> <span data-ttu-id="bc443-108">Een functie HTTP geactiveerd categoriseert tweets als groen, geel of rood op basis van Hallo gevoel score.</span><span class="sxs-lookup"><span data-stu-id="bc443-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on hello sentiment score.</span></span> <span data-ttu-id="bc443-109">Een e-mailbericht wordt verzonden wanneer slechte gevoel wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="bc443-109">An email is sent when poor sentiment is detected.</span></span> 

![afbeelding van de eerste twee stappen van de app in App-ontwerper voor logica](media/functions-twitter-email/designer1.png)

<span data-ttu-id="bc443-111">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="bc443-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bc443-112">Maak een cognitieve Services-account.</span><span class="sxs-lookup"><span data-stu-id="bc443-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="bc443-113">Maak een functie die tweet gevoel ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="bc443-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="bc443-114">Een logische app die is verbonden tooTwitter maken.</span><span class="sxs-lookup"><span data-stu-id="bc443-114">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="bc443-115">Gevoel detectie toohello logic app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bc443-115">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="bc443-116">Verbinding maken Hallo logic app toohello functie.</span><span class="sxs-lookup"><span data-stu-id="bc443-116">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="bc443-117">Een e-mailbericht op basis van het antwoord van de functie Hallo Hallo verzenden.</span><span class="sxs-lookup"><span data-stu-id="bc443-117">Send an email based on hello response from hello function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc443-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bc443-118">Prerequisites</span></span>

+ <span data-ttu-id="bc443-119">Een actieve [Twitter](https://twitter.com/) account.</span><span class="sxs-lookup"><span data-stu-id="bc443-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="bc443-120">Een [Outlook.com](https://outlook.com/) account (voor het verzenden van meldingen).</span><span class="sxs-lookup"><span data-stu-id="bc443-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="bc443-121">In dit onderwerp wordt gebruikt als het eerste punt Hallo resources gemaakt in [uw eerste functie maken vanuit Azure-portal Hallo](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="bc443-121">This topic uses as its starting point hello resources created in [Create your first function from hello Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="bc443-122">Als u dit nog niet hebt gedaan, voert u deze stappen nu toocreate functie-app.</span><span class="sxs-lookup"><span data-stu-id="bc443-122">If you haven't already done so, complete these steps now toocreate your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="bc443-123">Een cognitieve Services-account maken</span><span class="sxs-lookup"><span data-stu-id="bc443-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="bc443-124">Een cognitieve Services-account is vereist toodetect Hallo gevoel tweets wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="bc443-124">A Cognitive Services account is required toodetect hello sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="bc443-125">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bc443-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="bc443-126">Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bc443-126">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

3. <span data-ttu-id="bc443-127">Klik op **gegevens en analyse** > **cognitieve Services**.</span><span class="sxs-lookup"><span data-stu-id="bc443-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="bc443-128">Vervolgens Hallo-instellingen gebruiken als opgegeven in de tabel hello, Hallo voorwaarden accepteren en Controleer **pincode toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="bc443-128">Then, use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Blade cognitieve account maken](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="bc443-130">Instelling</span><span class="sxs-lookup"><span data-stu-id="bc443-130">Setting</span></span>      |  <span data-ttu-id="bc443-131">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="bc443-131">Suggested value</span></span>   | <span data-ttu-id="bc443-132">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bc443-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="bc443-133">**Naam**</span><span class="sxs-lookup"><span data-stu-id="bc443-133">**Name**</span></span> | <span data-ttu-id="bc443-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="bc443-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="bc443-135">Kies een unieke naam.</span><span class="sxs-lookup"><span data-stu-id="bc443-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="bc443-136">**API-type**</span><span class="sxs-lookup"><span data-stu-id="bc443-136">**API type**</span></span> | <span data-ttu-id="bc443-137">Tekstanalyse-API</span><span class="sxs-lookup"><span data-stu-id="bc443-137">Text Analytics API</span></span> | <span data-ttu-id="bc443-138">API gebruikt tooanalyze tekst.</span><span class="sxs-lookup"><span data-stu-id="bc443-138">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="bc443-139">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="bc443-139">**Location**</span></span> | <span data-ttu-id="bc443-140">VS - west</span><span class="sxs-lookup"><span data-stu-id="bc443-140">West US</span></span> | <span data-ttu-id="bc443-141">Op dit moment alleen **VS-West** is beschikbaar voor tekstanalyse.</span><span class="sxs-lookup"><span data-stu-id="bc443-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="bc443-142">**Prijscategorie**</span><span class="sxs-lookup"><span data-stu-id="bc443-142">**Pricing tier**</span></span> | <span data-ttu-id="bc443-143">F0</span><span class="sxs-lookup"><span data-stu-id="bc443-143">F0</span></span> | <span data-ttu-id="bc443-144">Beginnen met de laagste categorie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc443-144">Start with hello lowest tier.</span></span> <span data-ttu-id="bc443-145">Als u weinig aanroepen, schalen tooa hogere lagen.</span><span class="sxs-lookup"><span data-stu-id="bc443-145">If you run out of calls, scale tooa higher tier.</span></span>|
    | <span data-ttu-id="bc443-146">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="bc443-146">**Resource group**</span></span> | <span data-ttu-id="bc443-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bc443-147">myResourceGroup</span></span> | <span data-ttu-id="bc443-148">Gebruik Hallo dezelfde resourcegroep voor alle services in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="bc443-148">Use hello same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="bc443-149">Klik op **maken** toocreate uw account.</span><span class="sxs-lookup"><span data-stu-id="bc443-149">Click **Create** toocreate your account.</span></span> <span data-ttu-id="bc443-150">Nadat het Hallo-account is gemaakt, klikt u op uw nieuwe cognitieve Services-account vastgemaakt toohello dashboard.</span><span class="sxs-lookup"><span data-stu-id="bc443-150">After hello account is created, click your new Cognitive Services account pinned toohello dashboard.</span></span> 

5. <span data-ttu-id="bc443-151">Hallo-account, klikt u op **sleutels**, en kopieer vervolgens Hallo-waarde van **Key 1** en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="bc443-151">In hello account, click **Keys**, and then copy hello value of **Key 1** and save it.</span></span> <span data-ttu-id="bc443-152">U gebruikt deze sleutel tooconnect Hallo logic app tooyour cognitieve Services-account.</span><span class="sxs-lookup"><span data-stu-id="bc443-152">You use this key tooconnect hello logic app tooyour Cognitive Services account.</span></span> 
 
    ![Sleutels](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a><span data-ttu-id="bc443-154">Hallo-functie maken</span><span class="sxs-lookup"><span data-stu-id="bc443-154">Create hello function</span></span>

<span data-ttu-id="bc443-155">Functies biedt een goede manier toooffload verwerkingstaken in een werkstroom van logic apps.</span><span class="sxs-lookup"><span data-stu-id="bc443-155">Functions provides a great way toooffload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="bc443-156">Deze zelfstudie maakt gebruik van een HTTP-geactiveerde functie tooprocess tweet gevoel scores van cognitieve Services en retourneren een categoriewaarde.</span><span class="sxs-lookup"><span data-stu-id="bc443-156">This tutorial uses an HTTP triggered function tooprocess tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="bc443-157">Vouw de functie-app, klikt u op Hallo  **+**  knop naast te**functies**, klikt u op Hallo **HTTPTrigger** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="bc443-157">Expand your function app, click hello **+** button next too**Functions**, click hello **HTTPTrigger** template.</span></span> <span data-ttu-id="bc443-158">Type `CategorizeSentiment` voor Hallo functie **naam** en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="bc443-158">Type `CategorizeSentiment` for hello function **Name** and click **Create**.</span></span>

    ![Functie Apps blade functies +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="bc443-160">Hallo-inhoud van Hallo run.csx bestand vervangen door Hallo code te volgen en klik vervolgens op **opslaan**:</span><span class="sxs-lookup"><span data-stu-id="bc443-160">Replace hello contents of hello run.csx file with hello following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
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
    <span data-ttu-id="bc443-161">Deze functiecode retourneert een kleurcategorie is gebaseerd op Hallo gevoel score Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bc443-161">This function code returns a color category based on hello sentiment score received in hello request.</span></span> 

3. <span data-ttu-id="bc443-162">tootest Hallo-functie, klikt u op **Test** Hallo rechterkant tooexpand Hallo Test tabblad. Typ een waarde van `0.2` voor Hallo **aanvraagtekst**, en klik vervolgens op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="bc443-162">tootest hello function, click **Test** at hello far right tooexpand hello Test tab. Type a value of `0.2` for hello **Request body**, and then click **Run**.</span></span> <span data-ttu-id="bc443-163">Een waarde van **rood** Hallo hoofdtekst van antwoord Hallo wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="bc443-163">A value of **RED** is returned in hello body of hello response.</span></span> 

    ![Hallo functie testen in hello Azure-portal](./media/functions-twitter-email/test.png)

<span data-ttu-id="bc443-165">U hebt nu een functie die gevoel scores ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="bc443-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="bc443-166">Vervolgens kunt u een logische app, die de functie kan worden geïntegreerd met uw accounts Twitter en cognitieve Services maken.</span><span class="sxs-lookup"><span data-stu-id="bc443-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="bc443-167">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="bc443-167">Create a logic app</span></span>   

1. <span data-ttu-id="bc443-168">In Azure-portal hello, klikt u op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bc443-168">In hello Azure portal, click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="bc443-169">Klik op **Enterprise Integration** > **logische App**.</span><span class="sxs-lookup"><span data-stu-id="bc443-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="bc443-170">Hallo-instellingen gebruiken als opgegeven in de tabel hello, Controleer **pincode toodashboard**, en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="bc443-170">Then, use hello settings as specified in hello table, check **Pin toodashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="bc443-171">Typ een **naam** zoals `TweetSentiment`, Hallo-instellingen gebruiken die zijn opgegeven in de tabel Hallo Hallo voorwaarden accepteren en Controleer **pincode toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="bc443-171">Then, type a **Name** like `TweetSentiment`,  use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Logische app maken in hello Azure-portal](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="bc443-173">Instelling</span><span class="sxs-lookup"><span data-stu-id="bc443-173">Setting</span></span>      |  <span data-ttu-id="bc443-174">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="bc443-174">Suggested value</span></span>   | <span data-ttu-id="bc443-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bc443-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="bc443-176">**Naam**</span><span class="sxs-lookup"><span data-stu-id="bc443-176">**Name**</span></span> | <span data-ttu-id="bc443-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="bc443-177">TweetSentiment</span></span> | <span data-ttu-id="bc443-178">Kies een passende naam voor uw app.</span><span class="sxs-lookup"><span data-stu-id="bc443-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="bc443-179">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="bc443-179">**Resource group**</span></span> | <span data-ttu-id="bc443-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bc443-180">myResourceGroup</span></span> | <span data-ttu-id="bc443-181">API gebruikt tooanalyze tekst.</span><span class="sxs-lookup"><span data-stu-id="bc443-181">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="bc443-182">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="bc443-182">**Location**</span></span> | <span data-ttu-id="bc443-183">VS - oost</span><span class="sxs-lookup"><span data-stu-id="bc443-183">East US</span></span> | <span data-ttu-id="bc443-184">Kies een locatie sluiten tooyou.</span><span class="sxs-lookup"><span data-stu-id="bc443-184">Choose a location close tooyou.</span></span> |
    | <span data-ttu-id="bc443-185">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="bc443-185">**Resource group**</span></span> | <span data-ttu-id="bc443-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bc443-186">myResourceGroup</span></span> | <span data-ttu-id="bc443-187">Kies Hallo dezelfde bestaande resourcegroep als voorheen.</span><span class="sxs-lookup"><span data-stu-id="bc443-187">Choose hello same existing resource group as before.</span></span>|

4. <span data-ttu-id="bc443-188">Klik op **maken** toocreate uw logische app.</span><span class="sxs-lookup"><span data-stu-id="bc443-188">Click **Create** toocreate your logic app.</span></span> <span data-ttu-id="bc443-189">Nadat het Hallo-app is gemaakt, klikt u op uw nieuwe logische app vastgemaakt toohello dashboard.</span><span class="sxs-lookup"><span data-stu-id="bc443-189">After hello app is created, click your new logic app pinned toohello dashboard.</span></span> <span data-ttu-id="bc443-190">Klik in Logic Apps Designer Hallo, schuif naar beneden en klikt u op Hallo **lege logische App** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="bc443-190">Then in hello Logic Apps Designer, scroll down and click hello **Blank Logic App** template.</span></span> 

    ![Lege Logic Apps-sjabloon](media/functions-twitter-email/blank.png)

<span data-ttu-id="bc443-192">U kunt nu Hallo Logic Apps Designer tooadd services en triggers tooyour-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc443-192">You can now use hello Logic Apps Designer tooadd services and triggers tooyour app.</span></span>

## <a name="connect-tootwitter"></a><span data-ttu-id="bc443-193">Verbinding maken met tooTwitter</span><span class="sxs-lookup"><span data-stu-id="bc443-193">Connect tooTwitter</span></span>

<span data-ttu-id="bc443-194">Maak eerst een verbinding tooyour Twitter-account.</span><span class="sxs-lookup"><span data-stu-id="bc443-194">First, create a connection tooyour Twitter account.</span></span> <span data-ttu-id="bc443-195">Hallo logische app worden opgevraagd op tweets Hallo app toorun wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="bc443-195">hello logic app polls for tweets, which trigger hello app toorun.</span></span>

1. <span data-ttu-id="bc443-196">In de ontwerpfunctie hello, klikt u op Hallo **Twitter** service en klikt u op Hallo **wanneer een nieuwe tweet wordt gepost** trigger.</span><span class="sxs-lookup"><span data-stu-id="bc443-196">In hello designer, click hello **Twitter** service, and click hello **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="bc443-197">Meld u aan tooyour Twitter-account en autoriseren van Logic Apps toouse uw account.</span><span class="sxs-lookup"><span data-stu-id="bc443-197">Sign in tooyour Twitter account and authorize Logic Apps toouse your account.</span></span>

2. <span data-ttu-id="bc443-198">Hallo Twitter triggerinstellingen zoals opgegeven in de tabel hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc443-198">Use hello Twitter trigger settings as specified in hello table.</span></span> 

    ![Instellingen voor Twitter-connector](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="bc443-200">Instelling</span><span class="sxs-lookup"><span data-stu-id="bc443-200">Setting</span></span>      |  <span data-ttu-id="bc443-201">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="bc443-201">Suggested value</span></span>   | <span data-ttu-id="bc443-202">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bc443-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="bc443-203">**Zoektekst**</span><span class="sxs-lookup"><span data-stu-id="bc443-203">**Search text**</span></span> | <span data-ttu-id="bc443-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="bc443-204">#Azure</span></span> | <span data-ttu-id="bc443-205">Gebruik een hashtag die populaire voor nieuwe tweets toogenerate in hello gekozen-interval.</span><span class="sxs-lookup"><span data-stu-id="bc443-205">Use a hashtag that is popular enough for toogenerate new tweets in hello chosen interval.</span></span> <span data-ttu-id="bc443-206">Wanneer met behulp van de gratis laag Hallo en uw hashtag te populair is, kunt u snel omhoog Hallo transacties gebruiken in uw cognitieve Services-account.</span><span class="sxs-lookup"><span data-stu-id="bc443-206">When using hello Free tier and your hashtag is too popular, you can quickly use up hello transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="bc443-207">**Frequentie**</span><span class="sxs-lookup"><span data-stu-id="bc443-207">**Frequency**</span></span> | <span data-ttu-id="bc443-208">Minuut</span><span class="sxs-lookup"><span data-stu-id="bc443-208">Minute</span></span> | <span data-ttu-id="bc443-209">Hallo frequentie eenheid gebruikt voor het polling-Twitter.</span><span class="sxs-lookup"><span data-stu-id="bc443-209">hello frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="bc443-210">**Interval**</span><span class="sxs-lookup"><span data-stu-id="bc443-210">**Interval**</span></span> | <span data-ttu-id="bc443-211">15</span><span class="sxs-lookup"><span data-stu-id="bc443-211">15</span></span> | <span data-ttu-id="bc443-212">Hallo-tijd is verstreken tussen Twitter-aanvragen in de frequentie eenheden.</span><span class="sxs-lookup"><span data-stu-id="bc443-212">hello time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="bc443-213">Klik op **opslaan** tooconnect tooyour Twitter-account.</span><span class="sxs-lookup"><span data-stu-id="bc443-213">Click **Save** tooconnect tooyour Twitter account.</span></span> 

<span data-ttu-id="bc443-214">Uw app is nu verbonden tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="bc443-214">Now your app is connected tooTwitter.</span></span> <span data-ttu-id="bc443-215">Vervolgens maakt u verbinding maken met tootext analytics toodetect Hallo gevoel verzamelde tweets.</span><span class="sxs-lookup"><span data-stu-id="bc443-215">Next, you connect tootext analytics toodetect hello sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="bc443-216">Detectie van gevoel toevoegen</span><span class="sxs-lookup"><span data-stu-id="bc443-216">Add sentiment detection</span></span>

1. <span data-ttu-id="bc443-217">Klik op **nieuwe stap**, en vervolgens **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bc443-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Nieuwe stap, waarna een actie toevoegen](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="bc443-219">In **kiest u een actie**, klikt u op **Tekstanalyse**, en klik vervolgens op Hallo **detecteren gevoel** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="bc443-219">In **Choose an action**, click **Text Analytics**, and then click hello **Detect sentiment** action.</span></span>

    ![Gevoel detecteren](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="bc443-221">Typ de naam van een verbinding zoals `MyCognitiveServicesConnection`, plak Hallo-sleutel voor uw cognitieve Services-dat u hebt opgeslagen account en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="bc443-221">Type a connection name such as `MyCognitiveServicesConnection`, paste hello key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="bc443-222">Klik op **tekst tooanalyze** > **Tweet tekst**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bc443-222">Click **Text tooanalyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Gevoel detecteren](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="bc443-224">Nu dat gevoel detectie is geconfigureerd, kunt u een verbinding tooyour-functie die Hallo gevoel score uitvoer verbruikt kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bc443-224">Now that sentiment detection is configured, you can add a connection tooyour function that consumes hello sentiment score output.</span></span>

## <a name="connect-sentiment-output-tooyour-function"></a><span data-ttu-id="bc443-225">Verbinding maken met gevoel uitvoer tooyour functie</span><span class="sxs-lookup"><span data-stu-id="bc443-225">Connect sentiment output tooyour function</span></span>

1. <span data-ttu-id="bc443-226">In Hallo Logic Apps Designer, klikt u op **nieuwe stap** > **een actie toevoegen**, en klik vervolgens op **Azure Functions**.</span><span class="sxs-lookup"><span data-stu-id="bc443-226">In hello Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="bc443-227">Klik op **kiest u een Azure-functie**, selecteer Hallo **CategorizeSentiment** functie die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bc443-227">Click **Choose an Azure function**, select hello **CategorizeSentiment** function you created earlier.</span></span>  

    ![Azure vak voor de functie kiezen met een Azure-functie](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="bc443-229">In **aanvraagtekst**, klikt u op **Score** en vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bc443-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Score](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="bc443-231">De functie wordt nu worden geactiveerd wanneer een score gevoel wordt verzonden vanuit Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="bc443-231">Now, your function is triggered when a sentiment score is sent from hello logic app.</span></span> <span data-ttu-id="bc443-232">Een kleurcode categorie geretourneerd door Hallo functie toohello logische app.</span><span class="sxs-lookup"><span data-stu-id="bc443-232">A color-coded category is returned toohello logic app by hello function.</span></span> <span data-ttu-id="bc443-233">Vervolgens voegt u een e-mailbericht dat wordt verzonden als een waarde gevoel van **rood** wordt geretourneerd vanaf Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="bc443-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from hello function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="bc443-234">E-mailmeldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="bc443-234">Add email notifications</span></span>

<span data-ttu-id="bc443-235">Hallo laatste deel van de werkstroom Hallo is tootrigger een e-mailbericht wanneer Hallo gevoel wordt berekend als _rood_.</span><span class="sxs-lookup"><span data-stu-id="bc443-235">hello last part of hello workflow is tootrigger an email when hello sentiment is scored as _RED_.</span></span> <span data-ttu-id="bc443-236">In dit onderwerp gebruikt een Outlook.com-connector.</span><span class="sxs-lookup"><span data-stu-id="bc443-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="bc443-237">U kunt vergelijkbare stappen toouse Gmail of Outlook van Office 365-connector kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bc443-237">You can perform similar steps toouse a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="bc443-238">In Hallo Logic Apps Designer, klikt u op **nieuwe stap** > **een voorwaarde toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bc443-238">In hello Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="bc443-239">Klik op **kiest u een waarde**, klikt u vervolgens op **hoofdtekst**.</span><span class="sxs-lookup"><span data-stu-id="bc443-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="bc443-240">Selecteer **gelijk is aan**, klikt u op **kiest u een waarde** en het type `RED`, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bc443-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Een voorwaarde toohello logische app toevoegen.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="bc443-242">In **zo ja, niets doen**, klikt u op **een actie toevoegen**, zoeken naar `outlook.com`, klikt u op **e-mailbericht verzenden**, en meld u aan tooyour Outlook.com-account.</span><span class="sxs-lookup"><span data-stu-id="bc443-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in tooyour Outlook.com account.</span></span>
    
    ![Kies een actie voor Hallo voorwaarde.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="bc443-244">Als u geen een Outlook.com-account hebt, kunt u een andere connector, zoals Gmail of Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="bc443-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="bc443-245">In Hallo **e-mailbericht verzenden** actie, gebruik Hallo e-mailinstellingen als opgegeven in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc443-245">In hello **Send an email** action, use hello email settings as specified in hello table.</span></span> 

    ![Configureer Hallo e voor Hallo verzend een e-actie.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="bc443-247">Instelling</span><span class="sxs-lookup"><span data-stu-id="bc443-247">Setting</span></span>      |  <span data-ttu-id="bc443-248">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="bc443-248">Suggested value</span></span>   | <span data-ttu-id="bc443-249">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bc443-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="bc443-250">**Aan**</span><span class="sxs-lookup"><span data-stu-id="bc443-250">**To**</span></span> | <span data-ttu-id="bc443-251">Typ uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="bc443-251">Type your email address</span></span> | <span data-ttu-id="bc443-252">Hallo e-mailadres dat Hallo melding ontvangt.</span><span class="sxs-lookup"><span data-stu-id="bc443-252">hello email address that receives hello notification.</span></span> |
    | <span data-ttu-id="bc443-253">**Onderwerp**</span><span class="sxs-lookup"><span data-stu-id="bc443-253">**Subject**</span></span> | <span data-ttu-id="bc443-254">Negatieve tweet gevoel gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="bc443-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="bc443-255">Hallo onderwerpregel van het e-mailmelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc443-255">hello subject line of hello email notification.</span></span>  |
    | <span data-ttu-id="bc443-256">**Hoofdtekst**</span><span class="sxs-lookup"><span data-stu-id="bc443-256">**Body**</span></span> | <span data-ttu-id="bc443-257">Tweet tekst, locatie</span><span class="sxs-lookup"><span data-stu-id="bc443-257">Tweet text, Location</span></span> | <span data-ttu-id="bc443-258">Klik op Hallo **Tweet tekst** en **locatie** parameters.</span><span class="sxs-lookup"><span data-stu-id="bc443-258">Click hello **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="bc443-259">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bc443-259">Click **Save**.</span></span>

<span data-ttu-id="bc443-260">Nu dat Hallo werkstroom voltooid is, kunt u Hallo logische app- en Zie Hallo-functie op het werk.</span><span class="sxs-lookup"><span data-stu-id="bc443-260">Now that hello workflow is complete, you can enable hello logic app and see hello function at work.</span></span>

## <a name="test-hello-workflow"></a><span data-ttu-id="bc443-261">Test Hallo werkstroom</span><span class="sxs-lookup"><span data-stu-id="bc443-261">Test hello workflow</span></span>

1. <span data-ttu-id="bc443-262">In Hallo Logic App-ontwerper, klikt u op **uitvoeren** toostart Hallo app.</span><span class="sxs-lookup"><span data-stu-id="bc443-262">In hello Logic App Designer, click **Run** toostart hello app.</span></span>

2. <span data-ttu-id="bc443-263">Klik in de linkerkolom hello, **overzicht** toosee Hallo status van Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="bc443-263">In hello left column, click **Overview** toosee hello status of hello logic app.</span></span> 
 
    ![Uitvoeringsstatus van Logic app](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="bc443-265">(Optioneel) Klik op een hello wordt uitgevoerd toosee details van Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bc443-265">(Optional) Click one of hello runs toosee details of hello execution.</span></span>

4. <span data-ttu-id="bc443-266">Tooyour functie gaat, Hallo logboeken bekijken en controleren of gevoel waarden zijn ontvangen en verwerkt.</span><span class="sxs-lookup"><span data-stu-id="bc443-266">Go tooyour function, view hello logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Logboeken van de functie weergeven](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="bc443-268">Wanneer een potentieel negatieve gevoel wordt gedetecteerd, krijgt u een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="bc443-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="bc443-269">Als u een e-mailbericht hebt ontvangen, kunt u elke keer Hallo functie code tooreturn rood wijzigen:</span><span class="sxs-lookup"><span data-stu-id="bc443-269">If you haven't received an email, you can change hello function code tooreturn RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="bc443-270">Nadat u e-mailmeldingen hebt gecontroleerd, kunt u back toohello oorspronkelijke code wijzigen:</span><span class="sxs-lookup"><span data-stu-id="bc443-270">After you have verified email notifications, change back toohello original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="bc443-271">Nadat u deze zelfstudie hebt voltooid, moet u Hallo logische app uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="bc443-271">After you have completed this tutorial, you should disable hello logic app.</span></span> <span data-ttu-id="bc443-272">Door het uitschakelen van Hallo app u voorkomen dat u in rekening gebracht voor uitvoeringen en met behulp van Hallo transacties in uw cognitieve Services-account.</span><span class="sxs-lookup"><span data-stu-id="bc443-272">By disabling hello app, you avoid being charged for executions and using up hello transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="bc443-273">Nu hebt u gezien hoe eenvoudig het is toointegrate functies in een werkstroom Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="bc443-273">Now you have seen how easy it is toointegrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-hello-logic-app"></a><span data-ttu-id="bc443-274">Hallo logische app uitschakelen</span><span class="sxs-lookup"><span data-stu-id="bc443-274">Disable hello logic app</span></span>

<span data-ttu-id="bc443-275">toodisable hello logische app, klikt u op **overzicht** en klik vervolgens op **uitschakelen** Hallo boven aan het welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="bc443-275">toodisable hello logic app, click **Overview** and then click **Disable** at hello top of hello screen.</span></span> <span data-ttu-id="bc443-276">Hierdoor wordt voorkomen dat Hallo logische app uitgevoerd en steeds kosten zonder Hallo-app te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="bc443-276">This stops hello logic app from running and incurring charges without deleting hello app.</span></span> 

![De functie Logboeken](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="bc443-278">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc443-278">Next steps</span></span>

<span data-ttu-id="bc443-279">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="bc443-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bc443-280">Maak een cognitieve Services-account.</span><span class="sxs-lookup"><span data-stu-id="bc443-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="bc443-281">Maak een functie die tweet gevoel ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="bc443-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="bc443-282">Een logische app die is verbonden tooTwitter maken.</span><span class="sxs-lookup"><span data-stu-id="bc443-282">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="bc443-283">Gevoel detectie toohello logic app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bc443-283">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="bc443-284">Verbinding maken Hallo logic app toohello functie.</span><span class="sxs-lookup"><span data-stu-id="bc443-284">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="bc443-285">Een e-mailbericht op basis van het antwoord van de functie Hallo Hallo verzenden.</span><span class="sxs-lookup"><span data-stu-id="bc443-285">Send an email based on hello response from hello function.</span></span>

<span data-ttu-id="bc443-286">Hoe gaan van de volgende zelfstudie toolearn toohello toocreate een zonder Server API voor de functie.</span><span class="sxs-lookup"><span data-stu-id="bc443-286">Advance toohello next tutorial toolearn how toocreate a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="bc443-287">Een serverloze API maken met behulp van Azure Functions</span><span class="sxs-lookup"><span data-stu-id="bc443-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="bc443-288">toolearn meer informatie over Logic Apps, Zie [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="bc443-288">toolearn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

