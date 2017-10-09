---
title: aaaReal tijd Twitter-gevoel analyse met Azure Stream Analytics | Microsoft Docs
description: Meer informatie over hoe toouse Stream Analytics voor analyse van realtime Twitter-gevoel. Stapsgewijze richtlijnen van gebeurtenis generatie toodata in een live dashboard.
keywords: het trendanalyse realtime twitter, gevoel analyse, analyse van sociale media, trend analysis-voorbeeld
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="8ba3b-105">Real-time Twitter-gevoel analyse in Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ba3b-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="8ba3b-106">Meer informatie over hoe een gevoel analysis-oplossing voor sociale media analytics doordat realtime toobuild gebeurtenissen Twitter in Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-106">Learn how toobuild a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="8ba3b-107">Vervolgens kunt u een Azure Stream Analytics query tooanalyze Hallo gegevens en de archieven Hallo resultaten voor later gebruik of gebruik een dashboard en [Power BI](https://powerbi.com/) tooprovide inzichten in realtime.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-107">You can then write an Azure Stream Analytics query tooanalyze hello data and either store hello results for later use or use a dashboard and [Power BI](https://powerbi.com/) tooprovide insights in real time.</span></span>

<span data-ttu-id="8ba3b-108">Sociale media analytics-hulpprogramma's waarmee organisaties kunnen begrijpen trends onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="8ba3b-109">Trends onderwerpen zijn onderwerpen en houding die een groot aantal berichten in sociale media hebt.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="8ba3b-110">Gevoel analyse, ook wel genoemd *advies analysemodel*, maakt gebruik van sociale media analytics extra toodetermine houding ten opzichte van een product, idee, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools toodetermine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="8ba3b-111">Trendgrafiek van realtime Twitter is een goed voorbeeld van een hulpprogramma voor analyse, omdat Hallo hashtag abonnementsmodel kunt u toolisten toospecific trefwoorden (hashtags) en gevoel analyse van de feed Hallo ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-111">Real-time Twitter trend analysis is a great example of an analytics tool, because hello hashtag subscription model enables you toolisten toospecific keywords (hashtags) and develop sentiment analysis of hello feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="8ba3b-112">Scenario: Sociale media gevoel analyse in realtime</span><span class="sxs-lookup"><span data-stu-id="8ba3b-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="8ba3b-113">Een bedrijf met een website nieuws media is geïnteresseerd in een voordeel ten opzichte van de concurrenten krijgen door de inhoud van de site die onmiddellijk relevante tooits lezers.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant tooits readers.</span></span> <span data-ttu-id="8ba3b-114">analyse van sociale media Hallo bedrijf gebruikt op onderwerpen die relevant tooreaders zijn als volgt realtime gevoel analyse van gegevens van Twitter.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-114">hello company uses social media analysis on topics that are relevant tooreaders by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="8ba3b-115">onderwerpen over trends in realtime op Twitter, tooidentify Hallo bedrijf behoeften realtime analyses over Hallo tweet volume en gevoel voor belangrijke onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-115">tooidentify trending topics in real time on Twitter, hello company needs real-time analytics about hello tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="8ba3b-116">Hallo nodig is met andere woorden, een gevoel analysis analytics-engine die gebaseerd op deze sociale media feed.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-116">In other words, hello need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ba3b-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8ba3b-117">Prerequisites</span></span>
<span data-ttu-id="8ba3b-118">In deze zelfstudie gebruikt u een clienttoepassing die is verbonden tooTwitter en zoekt tweets waarvoor bepaalde hashtags (die u kunt instellen).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-118">In this tutorial, you use a client application that connects tooTwitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="8ba3b-119">In volgorde toorun toepassing hello en analyseren van Hallo tweets met Azure Streaming Analytics, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-119">In order toorun hello application and analyze hello tweets using Azure Streaming Analytics, you must have hello following:</span></span>

* <span data-ttu-id="8ba3b-120">Een Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="8ba3b-120">An Azure subscription</span></span>
* <span data-ttu-id="8ba3b-121">Een Twitter-account</span><span class="sxs-lookup"><span data-stu-id="8ba3b-121">A Twitter account</span></span> 
* <span data-ttu-id="8ba3b-122">Een Twitter-toepassing en Hallo [OAuth-toegangstoken](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) voor die toepassing.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-122">A Twitter application, and hello [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="8ba3b-123">We bieden op hoog niveau instructies voor het toocreate later een Twitter-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-123">We provide high-level instructions for how toocreate a Twitter application later.</span></span>
* <span data-ttu-id="8ba3b-124">Hallo TwitterWPFClient toepassing, wat Hallo Twitter leest-feed.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-124">hello TwitterWPFClient application, which reads hello Twitter feed.</span></span> <span data-ttu-id="8ba3b-125">tooget deze toepassing, download Hallo [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) bestand van GitHub en pak vervolgens Hallo-pakket naar een map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-125">tooget this application, download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip hello package into a folder on your computer.</span></span> <span data-ttu-id="8ba3b-126">Als u wilt dat toosee Hallo broncode en Hallo toepassing uitvoert in een foutopsporingsprogramma, u de broncode Hallo van krijgt [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-126">If you want toosee hello source code and run hello application in a debugger, you can get hello source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="8ba3b-127">Maken van een event hub voor Streaming Analytics invoer</span><span class="sxs-lookup"><span data-stu-id="8ba3b-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="8ba3b-128">Hallo-voorbeeldtoepassing gebeurtenissen gegenereerd en stuurt ze tooan Azure event hub.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-128">hello sample application generates events and pushes them tooan Azure event hub.</span></span> <span data-ttu-id="8ba3b-129">Azure event hubs zijn Hallo voorkeurs-methode van gebeurtenis opname voor Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-129">Azure event hubs are hello preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="8ba3b-130">Zie voor meer informatie, Hallo [documentatie van Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-130">For more information, see hello [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="8ba3b-131">Een event hub-naamruimte en event hub maken</span><span class="sxs-lookup"><span data-stu-id="8ba3b-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="8ba3b-132">In deze procedure maakt u eerst een event hub-naamruimte maken en vervolgens voegt u toe een event hub toothat naamruimte.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-132">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namespace.</span></span> <span data-ttu-id="8ba3b-133">Event hub-naamruimten worden gebruikt toologically groep gerelateerde gebeurtenis bus exemplaren.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-133">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="8ba3b-134">Meld u bij toohello Azure-portal en klikt u op **nieuw** > **Internet der dingen** > **Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-134">Log  in toohello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="8ba3b-135">In Hallo **naamruimte maken** blade, voer de naam van een naamruimte zoals `<yourname>-socialtwitter-eh-ns`.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-135">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="8ba3b-136">Kunt u een naam voor de naamruimte hello, maar Hallo-naam moet geldig zijn voor een URL en deze uniek zijn binnen Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-136">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="8ba3b-137">Selecteer een abonnement maken of een resourcegroep kiezen, en klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![Een event hub-naamruimte maken](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="8ba3b-139">Wanneer het Hallo-naamruimte is voltooid implementeren, vinden Hallo event hub naamruimte in uw lijst met Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-139">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="8ba3b-140">Klik op de nieuwe naamruimte Hallo en op Hallo naamruimte Blade  **+ &nbsp;Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-140">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="8ba3b-141">Hallo toevoegen Event Hub knop voor het maken van nieuwe event hub</span><span class="sxs-lookup"><span data-stu-id="8ba3b-141">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="8ba3b-142">Naam Hallo nieuwe event hub `socialtwitter-eh`.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-142">Name hello new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="8ba3b-143">U kunt een andere naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-143">You can use a different name.</span></span> <span data-ttu-id="8ba3b-144">Als u dit doet, noteer, omdat u de naam van de hello later nodig.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-144">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="8ba3b-145">U hoeft niet tooset andere opties voor Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-145">You don't need tooset any other options for hello event hub.</span></span>

    ![Blade voor het maken van nieuwe event hub](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="8ba3b-147">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-147">Click **Create**.</span></span>


### <a name="grant-access-toohello-event-hub"></a><span data-ttu-id="8ba3b-148">Verleen toegang toohello event hub</span><span class="sxs-lookup"><span data-stu-id="8ba3b-148">Grant access toohello event hub</span></span>

<span data-ttu-id="8ba3b-149">Voordat een proces gegevens tooan event hub verzendt kan, moet Hallo event hub een beleid waarmee u de juiste toegang hebben.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-149">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="8ba3b-150">Hallo toegangsbeleid produceert een verbindingsreeks die autorisatie-informatie bevat.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-150">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="8ba3b-151">Klik op Hallo gebeurtenis naamruimte blade **Event Hubs** en klik vervolgens op Hallo-naam van uw nieuwe event hub.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-151">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="8ba3b-152">Klik op Hallo event hubblade **gedeeld toegangsbeleid** en klik vervolgens op  **+ &nbsp;toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-152">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8ba3b-153">Zorg ervoor dat u werkt met Hallo event hub niet Hallo event hub naamruimte.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-153">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="8ba3b-154">Een beleid met de naam toevoegen `socialtwitter-access` en voor **Claim**, selecteer **beheren**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![Blade voor een nieuwe event hub-beleid maken](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="8ba3b-156">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-156">Click **Create**.</span></span>

5.  <span data-ttu-id="8ba3b-157">Nadat Hallo beleid is geïmplementeerd, klikt u op het Hallo-lijst met beleidsregels voor gedeelde toegang.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-157">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="8ba3b-158">Hallo-zoekvak met het label **CONNECTION STRING-primaire sleutel** en klik op Hallo kopie knop volgende toohello-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-158">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![Kopiëren van primaire verbindingssleutel tekenreeks Hallo van Hallo-beleid](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="8ba3b-160">Hallo-verbindingsreeks in een teksteditor plakken.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-160">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="8ba3b-161">U moet deze verbindingsreeks voor de volgende sectie hello, nadat u een aantal kleine wijzigingen tooit.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-161">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="8ba3b-162">Hallo-verbindingsreeks ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-162">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="8ba3b-163">U ziet dat Hallo-verbindingsreeks meerdere sleutel / waarde-paren bevat, gescheiden door puntkomma's: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, en `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-163">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="8ba3b-164">Voor beveiliging zijn onderdelen van de verbindingsreeks Hallo in Hallo voorbeeld verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-164">For security, parts of hello connection string in hello example have been removed.</span></span>

8.  <span data-ttu-id="8ba3b-165">Verwijder in de teksteditor Hallo Hallo `EntityPath` paar uit de verbindingsreeks hello (Vergeet niet tooremove Hallo puntkomma voorafgaande).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-165">In hello text editor, remove hello `EntityPath` pair from hello connection string (don't forget tooremove hello semicolon that precedes it).</span></span> <span data-ttu-id="8ba3b-166">Wanneer u bent klaar, uitziet de verbindingsreeks Hallo:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-166">When you're done, hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a><span data-ttu-id="8ba3b-167">Configureren en starten van de toepassing hello Twitter-client</span><span class="sxs-lookup"><span data-stu-id="8ba3b-167">Configure and start hello Twitter client application</span></span>
<span data-ttu-id="8ba3b-168">Hallo-clienttoepassing opgehaald tweet gebeurtenissen rechtstreeks vanuit Twitter.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-168">hello client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="8ba3b-169">In volgorde toodo doet, moet machtigingen toocall Hallo Twitter Streaming-API's.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-169">In order toodo so, it needs permission toocall hello Twitter Streaming APIs.</span></span> <span data-ttu-id="8ba3b-170">tooconfigure dat toestemming hebben, u een toepassing maakt in Twitter, dat wordt gegenereerd unieke referenties (zoals een OAuth-token).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-170">tooconfigure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="8ba3b-171">Vervolgens kunt u Hallo client toepassing toouse deze referenties wanneer het API-aanroepen maakt.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-171">You can then configure hello client application toouse these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="8ba3b-172">Een Twitter-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="8ba3b-172">Create a Twitter application</span></span>
<span data-ttu-id="8ba3b-173">Als u nog geen een Twitter-toepassing die u voor deze zelfstudie gebruiken kunt, kunt u een maken.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="8ba3b-174">U moet al een Twitter-account hebben.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="8ba3b-175">de exacte stappen Hallo in Twitter voor het maken van een toepassing en het Hallo-sleutels, geheimen en -token ophalen kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-175">hello exact process in Twitter for creating an application and getting hello keys, secrets, and token might change.</span></span> <span data-ttu-id="8ba3b-176">Als u deze instructies niet overeenkomen met wat u ziet op Hallo Twitter-site, raadpleegt u toohello Twitter-documentatie voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-176">If these instructions don't match what you see on hello Twitter site, refer toohello Twitter developer documentation.</span></span>

1. <span data-ttu-id="8ba3b-177">Ga toohello [Twitter application management-pagina](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-177">Go toohello [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="8ba3b-178">Maak een nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-178">Create a new application.</span></span> 

    * <span data-ttu-id="8ba3b-179">Geef een geldige URL voor Hallo-website-URL.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-179">For hello website URL, specify a valid URL.</span></span> <span data-ttu-id="8ba3b-180">Er geen toobe een live site.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-180">It does not have toobe a live site.</span></span> <span data-ttu-id="8ba3b-181">(U kunt niet alleen opgeven `localhost`.)</span><span class="sxs-lookup"><span data-stu-id="8ba3b-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="8ba3b-182">Hallo callback veld leeg laten.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-182">Leave hello callback field blank.</span></span> <span data-ttu-id="8ba3b-183">Hallo-clienttoepassing die u voor deze zelfstudie gebruiken vereist geen retouraanroepen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-183">hello client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Maken van een toepassing in Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="8ba3b-185">Wijzig eventueel Hallo Toepassingsmachtigingen tooread alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-185">Optionally, change hello application's permissions tooread-only.</span></span>

4. <span data-ttu-id="8ba3b-186">Wanneer de toepassing hello wordt gemaakt, gaat u toohello **sleutels en toegangstokens** pagina.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-186">When hello application is created, go toohello **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="8ba3b-187">Klik op Hallo knop toogenerate een toegangstoken en toegang token geheim.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-187">Click hello button toogenerate an access token and access token secret.</span></span>

<span data-ttu-id="8ba3b-188">Bewaar deze informatie bij de hand hebt, hebt u deze in de volgende procedure Hallo.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-188">Keep this information handy, because you will need it in hello next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="8ba3b-189">Hallo-sleutels en geheimen voor Hallo Twitter-toepassing biedt toegang tooyour Twitter-account.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-189">hello keys and secrets for hello Twitter application provide access tooyour Twitter account.</span></span> <span data-ttu-id="8ba3b-190">Deze informatie als vertrouwelijk te behandelen, dezelfde Hallo als u uw wachtwoord Twitter.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-190">Treat this information as sensitive, hello same as you do your Twitter password.</span></span> <span data-ttu-id="8ba3b-191">Bijvoorbeeld: deze informatie in een toepassing dat u tooothers geeft niet insluiten.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-191">For example, don't embed this information in an application that you give tooothers.</span></span> 


### <a name="configure-hello-client-application"></a><span data-ttu-id="8ba3b-192">Hallo-clienttoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="8ba3b-192">Configure hello client application</span></span>
<span data-ttu-id="8ba3b-193">Er is een clienttoepassing die verbinding via de tooTwitter gegevens maakt gemaakt [Twitter van Streaming-API's](https://dev.twitter.com/streaming/overview) toocollect tweet gebeurtenissen over een specifieke set van onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-193">We've created a client application that connects tooTwitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) toocollect tweet events about a specific set of topics.</span></span> <span data-ttu-id="8ba3b-194">Hallo-toepassing hello gebruikt [Sentiment140](http://help.sentiment140.com/) open-source hulpprogramma waarmee toegewezen Hallo gevoel waarde tooeach tweet te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-194">hello application uses hello [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns hello following sentiment value tooeach tweet:</span></span>

* <span data-ttu-id="8ba3b-195">0 = negatief</span><span class="sxs-lookup"><span data-stu-id="8ba3b-195">0 = negative</span></span>
* <span data-ttu-id="8ba3b-196">2 = neutral</span><span class="sxs-lookup"><span data-stu-id="8ba3b-196">2 = neutral</span></span>
* <span data-ttu-id="8ba3b-197">4 = positief</span><span class="sxs-lookup"><span data-stu-id="8ba3b-197">4 = positive</span></span>

<span data-ttu-id="8ba3b-198">Nadat het Hallo tweet gebeurtenissen een gevoel-waarde is toegewezen, zijn ze geduwd toohello event hub die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-198">After hello tweet events have been assigned a sentiment value, they are pushed toohello event hub that you created earlier.</span></span>

<span data-ttu-id="8ba3b-199">Voordat de toepassing hello wordt uitgevoerd, is er bepaalde gegevens van u, zoals Hallo Twitter-sleutels en Hallo event hub-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-199">Before hello application runs, it requires certain information from you, like hello Twitter keys and hello event hub connection string.</span></span> <span data-ttu-id="8ba3b-200">U kunt opgeven dat Hallo configuratie-informatie op de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-200">You can provide hello configuration information in these ways:</span></span>

* <span data-ttu-id="8ba3b-201">Voer de toepassing hello en gebruik vervolgens van de toepassing hello UI tooenter Hallo sleutels, geheimen en verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-201">Run hello application, and then use hello application's UI tooenter hello keys, secrets, and connection string.</span></span> <span data-ttu-id="8ba3b-202">Als u dit doet, Hallo configuratie-informatie wordt gebruikt voor de huidige sessie, maar het is niet opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-202">If you do this, hello configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="8ba3b-203">Bewerken van de toepassing hello .config-bestand en er set Hallo-waarden.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-203">Edit hello application's .config file and set hello values there.</span></span> <span data-ttu-id="8ba3b-204">Deze aanpak Hallo configuratie-informatie blijft bestaan, maar het betekent ook dat deze potentieel gevoelige informatie wordt opgeslagen als tekst zonder opmaak op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-204">This approach persists hello configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="8ba3b-205">Hallo volgende procedure worden beide benaderingen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-205">hello following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="8ba3b-206">Zorg ervoor dat u hebt gedownload en uitgepakt Hallo [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) toepassing, zoals vermeld in het Hallo-vereisten.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-206">Make sure you've downloaded and unzipped hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in hello prerequisites.</span></span>

2. <span data-ttu-id="8ba3b-207">tooset hello waarden tijdens runtime (en alleen voor de huidige sessie Hallo) uitvoeren Hallo `TwitterWPFClient.exe` toepassing.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-207">tooset hello values at run time (and only for hello current session), run hello `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="8ba3b-208">Wanneer de toepassing hello wordt gevraagd, voert u Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-208">When hello application prompts you, enter hello following values:</span></span>

    * <span data-ttu-id="8ba3b-209">Hallo Twitter consumentsleutel (API-sleutel).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-209">hello Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="8ba3b-210">Hallo Twitter consumentgeheim (geheim API).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-210">hello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="8ba3b-211">Hallo Access Token Twitter.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-211">hello Twitter Access Token.</span></span>
    * <span data-ttu-id="8ba3b-212">Hallo Access Token geheim Twitter.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-212">hello Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="8ba3b-213">Hallo verbindingsreeksgegevens die u eerder hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-213">hello connection string information that you saved earlier.</span></span> <span data-ttu-id="8ba3b-214">Zorg ervoor dat u het Hallo-verbindingsreeks dat u Hallo verwijderd `EntityPath` sleutel-waardepaar uit.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-214">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="8ba3b-215">Hallo Twitter sleutelwoorden die u wilt dat toodetermine gevoel voor.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-215">hello Twitter keywords that you want toodetermine sentiment for.</span></span>

   ![TwitterWpfClient toepassing uitgevoerd, worden weergegeven met verborgen instellingen](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="8ba3b-217">tooset hello waarden permanent, een editor tooopen hello TwitterWpfClient.exe.config tekstbestand gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-217">tooset hello values persistently, use a text editor tooopen hello TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="8ba3b-218">Klik dan in Hallo `<appSettings>` element dit doen:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-218">Then in hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="8ba3b-219">Stel `oauth_consumer_key` toohello Twitter consumentsleutel (API-sleutel).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-219">Set `oauth_consumer_key` toohello Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="8ba3b-220">Stel `oauth_consumer_secret` toohello Twitter consumentgeheim (geheim API).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-220">Set `oauth_consumer_secret` toohello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="8ba3b-221">Stel `oauth_token` toohello Access Token Twitter.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-221">Set `oauth_token` toohello Twitter Access Token.</span></span>
    * <span data-ttu-id="8ba3b-222">Stel `oauth_token_secret` toohello Access Token geheim Twitter.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-222">Set `oauth_token_secret` toohello Twitter Access Token Secret.</span></span>

    <span data-ttu-id="8ba3b-223">Verderop in Hallo `<appSettings>` element, deze wijzigingen aanbrengen:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-223">Later in hello `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="8ba3b-224">Stel `EventHubName` naam toohello event hub (dat wil zeggen toohello waarde van Hallo entiteit pad).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-224">Set `EventHubName` toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="8ba3b-225">Stel `EventHubNameConnectionString` toohello-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-225">Set `EventHubNameConnectionString` toohello connection string.</span></span> <span data-ttu-id="8ba3b-226">Zorg ervoor dat u het Hallo-verbindingsreeks dat u Hallo verwijderd `EntityPath` sleutel-waardepaar uit.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-226">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="8ba3b-227">Hallo `<appSettings>` sectie eruit Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-227">hello `<appSettings>` section looks like hello following example.</span></span> <span data-ttu-id="8ba3b-228">(Voor duidelijkheid en beveiliging we sommige regels ingepakt en bepaalde tekens verwijderd.)</span><span class="sxs-lookup"><span data-stu-id="8ba3b-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![TwitterWpfClient toepassingsconfiguratiebestand in een teksteditor Hallo Twitter-sleutels en geheimen en Hallo event hub verbindingsinformatie weergeven](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="8ba3b-230">Als u al Hallo toepassing niet starten, nu TwitterWpfClient.exe uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-230">If you didn't already start hello application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="8ba3b-231">Klik op Hallo groene knop toocollect sociale gevoel.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-231">Click hello green start button toocollect social sentiment.</span></span> <span data-ttu-id="8ba3b-232">U ziet Tweet gebeurtenissen met de Hallo **CreatedAt**, **onderwerp**, en **SentimentScore** waarden tooyour event hub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-232">You see Tweet events with hello **CreatedAt**, **Topic**, and **SentimentScore** values being sent tooyour event hub.</span></span>

    ![TwitterWpfClient-toepassing wordt uitgevoerd, met een overzicht van tweets](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="8ba3b-234">Als u fouten ziet en u een stream met tweets weergegeven in de onderste deel Hallo van Hallo-venster niet ziet, Controleer Hallo sleutels en geheimen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-234">If you see errors, and you don't see a stream of tweets displayed in hello lower part of hello window, double-check hello keys and secrets.</span></span> <span data-ttu-id="8ba3b-235">Controleer ook de verbindingsreeks hello (Zorg ervoor dat deze geen Hallo bevat `EntityPath` sleutel en waarde.)</span><span class="sxs-lookup"><span data-stu-id="8ba3b-235">Also check hello connection string (make sure that it does not include hello `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="8ba3b-236">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="8ba3b-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="8ba3b-237">Nu dat tweet gebeurtenissen streaming in realtime van Twitter, kunt u instellen een Stream Analytics-taak tooanalyze deze gebeurtenissen in realtime.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job tooanalyze these events in real time.</span></span>

1. <span data-ttu-id="8ba3b-238">Klik in hello Azure-portal, op **nieuw** > **Internet der dingen** > **Stream Analytics-taak**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-238">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="8ba3b-239">Naam Hallo taak `socialtwitter-sa-job` en een abonnement, resourcegroep en locatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-239">Name hello job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="8ba3b-240">Het is een goed idee tooplace Hallo taak en Hallo event hub in Hallo dezelfde regio voor optimale prestaties en doet dat niet u tootransfer gegevens tussen regio's betaalt.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-240">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![Er wordt een nieuwe Stream Analytics-taak](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="8ba3b-242">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-242">Click **Create**.</span></span>

    <span data-ttu-id="8ba3b-243">Hallo-taak is gemaakt en Hallo portal geeft taakdetails weer.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-243">hello job is created and hello portal displays job details.</span></span>


## <a name="specify-hello-job-input"></a><span data-ttu-id="8ba3b-244">Geef Hallo taak voor invoer</span><span class="sxs-lookup"><span data-stu-id="8ba3b-244">Specify hello job input</span></span>

1. <span data-ttu-id="8ba3b-245">In de Stream Analytics-taak onder **taak topologie** in Hallo midden van de blade taak hello, klikt u op **invoer**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-245">In your Stream Analytics job, under **Job Topology** in hello middle of hello job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="8ba3b-246">In Hallo **invoer** blade, klikt u op  **+ &nbsp;toevoegen** en vult Hallo-blade met deze waarden:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-246">In hello **Inputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="8ba3b-247">**Invoeralias**: Gebruik de naam van Hallo `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-247">**Input alias**: Use hello name `TwitterStream`.</span></span> <span data-ttu-id="8ba3b-248">Als u een andere naam gebruikt, noteer het omdat u deze later nodig.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="8ba3b-249">**Gegevensbrontype**: Selecteer **gegevensstroom**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="8ba3b-250">**Bron**: Selecteer **Event hub**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="8ba3b-251">**Optie importeren**: Selecteer **gebruik event hub uit het huidige abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="8ba3b-252">**Service bus-naamruimte**: Selecteer Hallo event hub naamruimte die u eerder hebt gemaakt (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-252">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="8ba3b-253">**Event hub**: Selecteer Hallo event hub die u eerder hebt gemaakt (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-253">**Event hub**: Select hello event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="8ba3b-254">**Naam Event hub beleid**: Selecteer Hallo-beleid dat u eerder hebt gemaakt (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-254">**Event hub policy name**: Select hello access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Nieuwe invoer voor Streaming Analytics-taak maken](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="8ba3b-256">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-256">Click **Create**.</span></span>


## <a name="specify-hello-job-query"></a><span data-ttu-id="8ba3b-257">Hallo taak query opgeven</span><span class="sxs-lookup"><span data-stu-id="8ba3b-257">Specify hello job query</span></span>

<span data-ttu-id="8ba3b-258">Stream Analytics ondersteunt een eenvoudig, declaratief querymodel die transformaties beschrijft.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="8ba3b-259">toolearn meer informatie over het Hallo-taal, Zie Hallo [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-259">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="8ba3b-260">Deze zelfstudie helpt u bij het ontwerpen en testen van meerdere query's via Twitter-gegevens.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="8ba3b-261">toocompare hello aantal vermeldingen tussen onderwerpen, kunt u een [tumblingvenster](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget Hallo aantal vermeldingen onderwerp elke vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-261">toocompare hello number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="8ba3b-262">Sluit Hallo **invoer** blade als u dat nog niet gedaan hebt.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-262">Close hello **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="8ba3b-263">Klik op Hallo taakblade Hallo **Query** vak.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-263">In hello job blade, click hello **Query** box.</span></span> <span data-ttu-id="8ba3b-264">Azure bevat Hallo invoer en uitvoer die zijn geconfigureerd voor Hallo taak en kunnen u een query maken die u kunt de invoerstroom Hallo transformeren toohello uitvoer worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-264">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>

3. <span data-ttu-id="8ba3b-265">Zorg ervoor dat Hallo TwitterWpfClient toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-265">Make sure that hello TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="8ba3b-266">In Hallo **Query** blade, klikt u op Hallo punten volgende toohello `TwitterStream` invoer- en selecteer vervolgens **voorbeeldgegevens uit de invoer**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-266">In hello **Query** blade, click hello dots next toohello `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Menu Opties toouse voorbeeldgegevens voor Hallo Streaming Analytics-job vermelding met 'Voorbeeldgegevens uit invoer' geselecteerd](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="8ba3b-268">Hiermee opent u een blade die u opgeven hoeveel sample data tooget kunt, gedefinieerd in termen van hoe lang tooread Hallo stream invoeren.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-268">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

4. <span data-ttu-id="8ba3b-269">Stel **minuten** too3 en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-269">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    ![Opties voor de invoerstroom hello, een steekproef met '3 minuten' geselecteerd.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="8ba3b-271">Azure 3 minuten aan gegevens uit de invoerstroom Hallo voorbeelden en waarschuwt u als voorbeeldgegevens Hallo gereed is.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-271">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="8ba3b-272">(Dit duurt even.)</span><span class="sxs-lookup"><span data-stu-id="8ba3b-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="8ba3b-273">Hallo voorbeeldgegevens worden tijdelijk opgeslagen en is beschikbaar tijdens het Hallo-query-venster geopend.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-273">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="8ba3b-274">Als u Hallo query-venster sluit, Hallo voorbeeldgegevens wordt verwijderd en u een nieuwe set met voorbeeldgegevens toocreate hebt.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-274">If you close hello query window, hello sample data is discarded, and you have toocreate a new set of sample data.</span></span> 

5. <span data-ttu-id="8ba3b-275">Hallo-query in Hallo code-editor toohello volgende wijzigen:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-275">Change hello query in hello code editor toohello following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="8ba3b-276">Als niet `TwitterStream` als Hallo alias voor Hallo invoer vervangen door uw alias voor `TwitterStream` in Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-276">If didn't use `TwitterStream` as hello alias for hello input, substitute your alias for `TwitterStream` in hello query.</span></span>  

    <span data-ttu-id="8ba3b-277">Deze query gebruikt Hallo **TIMESTAMP BY** sleutelwoord toospecify een tijdstempelveld in Hallo nettolading toobe gebruikt in Hallo tijdelijke berekeningen.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-277">This query uses hello **TIMESTAMP BY** keyword toospecify a timestamp field in hello payload toobe used in hello temporal computation.</span></span> <span data-ttu-id="8ba3b-278">Als dit veld niet wordt opgegeven, wordt Hallo windowing bewerking uitgevoerd met behulp van Hallo hoelang elke gebeurtenis is ontvangen op Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-278">If this field isn't specified, hello windowing operation is performed by using hello time that each event arrived at hello event hub.</span></span> <span data-ttu-id="8ba3b-279">Meer informatie in de sectie Hallo 'aankomsttijd tegenover tijd Application' van [Stream Analytics Query verwijzing](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-279">Learn more in hello "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="8ba3b-280">Deze query ook toegang tot krijgt een tijdstempel voor Hallo einde van elke venster met Hallo **System.Timestamp** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-280">This query also accesses a timestamp for hello end of each window by using hello **System.Timestamp** property.</span></span>

5. <span data-ttu-id="8ba3b-281">Klik op **Test**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-281">Click **Test**.</span></span> <span data-ttu-id="8ba3b-282">Hallo-query wordt uitgevoerd tegen Hallo-gegevens die u door actieve.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-282">hello query runs against hello data that you sampled.</span></span>
    
6. <span data-ttu-id="8ba3b-283">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-283">Click **Save**.</span></span> <span data-ttu-id="8ba3b-284">Dit bespaart Hallo query als onderdeel van Hallo Streaming Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-284">This saves hello query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="8ba3b-285">(Deze kunt Hallo voorbeeldgegevens niet opslaan.)</span><span class="sxs-lookup"><span data-stu-id="8ba3b-285">(It doesn't save hello sample data.)</span></span>


## <a name="experiment-using-different-fields-from-hello-stream"></a><span data-ttu-id="8ba3b-286">Experimenteren met verschillende velden van Hallo stream</span><span class="sxs-lookup"><span data-stu-id="8ba3b-286">Experiment using different fields from hello stream</span></span> 

<span data-ttu-id="8ba3b-287">Hallo bevat volgende tabel Hallo velden die deel van Hallo streaming JSON-gegevens uitmaken.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-287">hello following table lists hello fields that are part of hello JSON streaming data.</span></span> <span data-ttu-id="8ba3b-288">U kunt gratis tooexperiment in Hallo query-editor.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-288">Feel free tooexperiment in hello query editor.</span></span>

|<span data-ttu-id="8ba3b-289">JSON-eigenschap</span><span class="sxs-lookup"><span data-stu-id="8ba3b-289">JSON property</span></span> | <span data-ttu-id="8ba3b-290">Definitie</span><span class="sxs-lookup"><span data-stu-id="8ba3b-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="8ba3b-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="8ba3b-291">CreatedAt</span></span> | <span data-ttu-id="8ba3b-292">Hallo-tijd die tweet Hallo is gemaakt</span><span class="sxs-lookup"><span data-stu-id="8ba3b-292">hello time that hello tweet was created</span></span>|
|<span data-ttu-id="8ba3b-293">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="8ba3b-293">Topic</span></span> | <span data-ttu-id="8ba3b-294">Hallo-onderwerp dat overeenkomt met de Hallo opgegeven trefwoord</span><span class="sxs-lookup"><span data-stu-id="8ba3b-294">hello topic that matches hello specified keyword</span></span>|
|<span data-ttu-id="8ba3b-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="8ba3b-295">SentimentScore</span></span> | <span data-ttu-id="8ba3b-296">Hallo gevoel score uit Sentiment140</span><span class="sxs-lookup"><span data-stu-id="8ba3b-296">hello sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="8ba3b-297">Auteur</span><span class="sxs-lookup"><span data-stu-id="8ba3b-297">Author</span></span> | <span data-ttu-id="8ba3b-298">Hallo Twitter-ingang die Hallo tweet wordt verzonden</span><span class="sxs-lookup"><span data-stu-id="8ba3b-298">hello Twitter handle that sent hello tweet</span></span>|
|<span data-ttu-id="8ba3b-299">Tekst</span><span class="sxs-lookup"><span data-stu-id="8ba3b-299">Text</span></span> | <span data-ttu-id="8ba3b-300">Hallo volledige hoofdtekst van Hallo tweet</span><span class="sxs-lookup"><span data-stu-id="8ba3b-300">hello full body of hello tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="8ba3b-301">Uitvoerlocatie maken</span><span class="sxs-lookup"><span data-stu-id="8ba3b-301">Create an output sink</span></span>

<span data-ttu-id="8ba3b-302">U hebt nu een stroom gebeurtenissen, een event hub invoer tooingest gebeurtenissen en een query tooperform een transformatie gedefinieerd via Hallo-stroom.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-302">You have now defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="8ba3b-303">de laatste stap Hallo is toodefine uitvoerlocatie voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-303">hello last step is toodefine an output sink for hello job.</span></span>  

<span data-ttu-id="8ba3b-304">In deze zelfstudie maakt schrijven u Hallo geaggregeerd tweet gebeurtenissen van Hallo taak query tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-304">In this tutorial, you write hello aggregated tweet events from hello job query tooAzure Blob storage.</span></span>  <span data-ttu-id="8ba3b-305">U kunt ook uw resultaten tooAzure SQL-Database, Azure Table storage, Event Hubs push of, afhankelijk van uw toepassing moet Power BI.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-305">You can also push your results tooAzure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-hello-job-output"></a><span data-ttu-id="8ba3b-306">Hallo taakuitvoer opgeven</span><span class="sxs-lookup"><span data-stu-id="8ba3b-306">Specify hello job output</span></span>

1. <span data-ttu-id="8ba3b-307">In Hallo **taak topologie** sectie, klikt u op Hallo **uitvoer** vak.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-307">In hello **Job Topology** section, click hello **Output** box.</span></span> 

2. <span data-ttu-id="8ba3b-308">In Hallo **uitvoer** blade, klikt u op  **+ &nbsp;toevoegen** en vult Hallo-blade met deze waarden:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-308">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="8ba3b-309">**Uitvoeraliassen**: Gebruik de naam van Hallo `TwitterStream-Output`.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-309">**Output alias**: Use hello name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="8ba3b-310">**Sink**: Selecteer **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="8ba3b-311">**Opties voor het importeren**: Selecteer **gebruik blob storage uit het huidige abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="8ba3b-312">**Storage-account**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-312">**Storage account**.</span></span> <span data-ttu-id="8ba3b-313">Selecteer **een nieuw opslagaccount maken.**</span><span class="sxs-lookup"><span data-stu-id="8ba3b-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="8ba3b-314">**Storage-account** (tweede vak).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-314">**Storage account** (second box).</span></span> <span data-ttu-id="8ba3b-315">Voer `YOURNAMEsa`, waarbij `YOURNAME` uw naam of een andere unieke tekenreeks is.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="8ba3b-316">Hallo-naam kan gebruiken die alleen kleine letters en cijfers en deze uniek zijn binnen Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-316">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="8ba3b-317">**Container**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-317">**Container**.</span></span> <span data-ttu-id="8ba3b-318">Voer `socialtwitter`.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="8ba3b-319">Hallo opslagaccountnaam- en containernaam zijn gebruikte samen tooprovide een URI voor Hallo blob storage als volgt:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-319">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    !['Nieuw uitvoer' blade voor Stream Analytics-taak](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="8ba3b-321">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-321">Click **Create**.</span></span> 

    <span data-ttu-id="8ba3b-322">Azure storage-account Hallo maakt en genereert een sleutel automatisch.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-322">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="8ba3b-323">Sluit Hallo **uitvoer** blade.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-323">Close hello **Outputs** blade.</span></span> 


## <a name="start-hello-job"></a><span data-ttu-id="8ba3b-324">Hallo taak starten</span><span class="sxs-lookup"><span data-stu-id="8ba3b-324">Start hello job</span></span>

<span data-ttu-id="8ba3b-325">Een taak invoer-, query- en uitvoer zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="8ba3b-326">U bent klaar toostart Hallo Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-326">You are ready toostart hello Stream Analytics job.</span></span>

1. <span data-ttu-id="8ba3b-327">Zorg ervoor dat Hallo TwitterWpfClient toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-327">Make sure that hello TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="8ba3b-328">Klik op Hallo taakblade **Start**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-328">In hello job blade, click **Start**.</span></span>

    ![Hallo Stream Analytics-taak starten](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="8ba3b-330">In Hallo **starttaak** blade voor **taakuitvoer begintijd**, selecteer **nu** en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-330">In hello **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Blade 'Start de taak' voor Hallo Stream Analytics-taak](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="8ba3b-332">Azure waarschuwt u als Hallo-taak is gestart en Hallo taak blade Hallo status wordt weergegeven als **met**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-332">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![Actieve taak](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="8ba3b-334">Uitvoer weergeven voor gevoel analyse</span><span class="sxs-lookup"><span data-stu-id="8ba3b-334">View output for sentiment analysis</span></span>

<span data-ttu-id="8ba3b-335">Nadat uw taak eenmaal is gestart en Hallo realtime Twitter-stroom wordt verwerkt, kunt u de uitvoer voor analyse gevoel Hallo kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-335">After your job has started running and is processing hello real-time Twitter stream, you can view hello output for sentiment analysis.</span></span>

<span data-ttu-id="8ba3b-336">U kunt een hulpprogramma zoals [Azure Opslagverkenner](https://http://storageexplorer.com/) of [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview uw taakuitvoerbestand in realtime.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview your job output in real time.</span></span> <span data-ttu-id="8ba3b-337">Hier kunt u [Power BI](https://powerbi.com/) tooextend uw toepassing tooinclude een aangepaste dashboard, zoals een weergegeven in de volgende schermafbeelding Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-337">From here, you can use [Power BI](https://powerbi.com/) tooextend your application tooinclude a customized dashboard like hello one shown in hello following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a><span data-ttu-id="8ba3b-339">Maken van een andere query tooidentify trends onderwerpen</span><span class="sxs-lookup"><span data-stu-id="8ba3b-339">Create another query tooidentify trending topics</span></span>

<span data-ttu-id="8ba3b-340">Een andere query kunt u toounderstand Twitter-gevoel is gebaseerd op een [Verschuivend venster](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-340">Another query you can use toounderstand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="8ba3b-341">tooidentify trends onderwerpen, die u zoeken naar onderwerpen die via een drempelwaarde voor vermeldingen in een opgegeven tijdsduur.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-341">tooidentify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="8ba3b-342">Oog op Hallo van deze zelfstudie wordt zoeken u naar onderwerpen die worden vermeld meer dan 20 keer in Hallo laatste 5 seconden.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-342">For hello purposes of this tutorial, you check for topics that are mentioned more than 20 times in hello last 5 seconds.</span></span>

1. <span data-ttu-id="8ba3b-343">Klik op Hallo taakblade **stoppen** toostop Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-343">In hello job blade, click **Stop** toostop hello job.</span></span> 

2. <span data-ttu-id="8ba3b-344">In Hallo **taak topologie** sectie, klikt u op Hallo **Query** vak.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-344">In hello **Job Topology** section, click hello **Query** box.</span></span> 

3. <span data-ttu-id="8ba3b-345">Hallo query toohello volgende wijzigen:</span><span class="sxs-lookup"><span data-stu-id="8ba3b-345">Change hello query toohello following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="8ba3b-346">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-346">Click **Save**.</span></span>

5. <span data-ttu-id="8ba3b-347">Zorg ervoor dat Hallo TwitterWpfClient toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-347">Make sure that hello TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="8ba3b-348">Klik op **Start** toorestart Hallo taak met de nieuwe query Hallo.</span><span class="sxs-lookup"><span data-stu-id="8ba3b-348">Click **Start** toorestart hello job using hello new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="8ba3b-349">Ondersteuning krijgen</span><span class="sxs-lookup"><span data-stu-id="8ba3b-349">Get support</span></span>
<span data-ttu-id="8ba3b-350">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="8ba3b-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ba3b-351">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8ba3b-351">Next steps</span></span>
* [<span data-ttu-id="8ba3b-352">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ba3b-352">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8ba3b-353">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ba3b-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8ba3b-354">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="8ba3b-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8ba3b-355">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="8ba3b-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8ba3b-356">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="8ba3b-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
