---
title: Aan de slag met Azure Mobile Engagement voor web-apps | Microsoft Docs
description: Ontdek hoe u Azure Mobile Engagement gebruikt met analyses en pushmeldingen voor web-apps.
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: abcb04e4e0a3ae4fdba3a4ded20b3846ac3b21e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="8ae12-103">Aan de slag met Azure Mobile Engagement voor web-apps</span><span class="sxs-lookup"><span data-stu-id="8ae12-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="8ae12-104">In dit onderwerp wordt beschreven hoe u met Azure Mobile Engagement uw gebruik van web-apps leert te begrijpen.</span><span class="sxs-lookup"><span data-stu-id="8ae12-104">This topic shows you how to use Azure Mobile Engagement to understand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="8ae12-105">De Azure Mobile Engagement-service wordt in maart 2018 beëindigd en is momenteel alleen beschikbaar voor bestaande klanten.</span><span class="sxs-lookup"><span data-stu-id="8ae12-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="8ae12-106">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8ae12-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="8ae12-107">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="8ae12-107">This tutorial requires the following:</span></span>

* <span data-ttu-id="8ae12-108">Visual Studio 2015 of een andere editor van uw keuze</span><span class="sxs-lookup"><span data-stu-id="8ae12-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="8ae12-109">Web SDK</span><span class="sxs-lookup"><span data-stu-id="8ae12-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="8ae12-110">Deze Web SDK bevindt zich nog in de previewfase en ondersteunt momenteel alleen Analytics en biedt geen ondersteuning voor het verzenden van pushmeldingen in browsers of apps.</span><span class="sxs-lookup"><span data-stu-id="8ae12-110">This Web SDK is in Preview and only supports Analytics at the moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="8ae12-111">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="8ae12-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="8ae12-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="8ae12-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8ae12-113">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8ae12-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="8ae12-114">Mobile Engagement instellen voor uw web-app</span><span class="sxs-lookup"><span data-stu-id="8ae12-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="8ae12-115"><a id="connecting-app"></a>Uw app verbinden met de back-end van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8ae12-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="8ae12-116">Deze zelfstudie toont een 'basisintegratie'. Dit is de minimale set die vereist is voor het verzamelen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="8ae12-116">This tutorial presents a "basic integration," which is the minimal set required to collect data.</span></span>

<span data-ttu-id="8ae12-117">We gaan een elementaire web-app maken met Visual Studio ter illustratie van de integratie, maar u kunt de stappen ook volgen met elke webtoepassing die buiten Visual Studio is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ae12-117">We will create a basic web app with Visual Studio to demonstrate the integration though you can follow the steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="8ae12-118">Een nieuwe web-app maken</span><span class="sxs-lookup"><span data-stu-id="8ae12-118">Create a new Web App</span></span>
<span data-ttu-id="8ae12-119">In de volgende stappen wordt ervan uitgegaan dat u Visual Studio 2015 gebruikt, hoewel de stappen hetzelfde zijn in eerdere versies van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8ae12-119">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="8ae12-120">Start Visual Studio en selecteer **New Project** in het scherm **Home**.</span><span class="sxs-lookup"><span data-stu-id="8ae12-120">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="8ae12-121">Selecteer **Web** -> **ASP.Net Web Application** (ASP.Net-webtoepassing) in de pop-up.</span><span class="sxs-lookup"><span data-stu-id="8ae12-121">In the pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="8ae12-122">Vul de **app-naam**, **locatie** en **oplossingsnaam** in en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ae12-122">Fill in the app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="8ae12-123">Selecteer in de pop-up **Select a template** (Selecteer een sjabloon) de optie **Empty** (Leeg) onder **ASP.Net 4.5 Templates** (ASP.Net 4.5-sjablonen) en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ae12-123">In the **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="8ae12-124">U hebt nu een nieuw, leeg web-app-project gemaakt waarin wij de Web SDK van Azure Mobile Engagement gaan integreren.</span><span class="sxs-lookup"><span data-stu-id="8ae12-124">You have now created a new blank Web App project into which we will integrate the Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="8ae12-125">Uw app verbinden met de back-end van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8ae12-125">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="8ae12-126">Maak een nieuwe map genaamd **javascript** in uw oplossing en voeg het Web SDK JS-bestand **azure-engagement.js** eraan toe.</span><span class="sxs-lookup"><span data-stu-id="8ae12-126">Create a new folder called **javascript** in your solution and add the Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="8ae12-127">Voeg met de volgende code een nieuw bestand met de naam **main.js** toe aan deze javascript-map.</span><span class="sxs-lookup"><span data-stu-id="8ae12-127">Add a new file called **main.js** in this javascript folder with the following code.</span></span> <span data-ttu-id="8ae12-128">Zorg ervoor dat u de verbindingstekenreeks bijwerkt.</span><span class="sxs-lookup"><span data-stu-id="8ae12-128">Make sure to update the connection string.</span></span> <span data-ttu-id="8ae12-129">Dit `azureEngagement`-object wordt gebruikt voor toegang tot Web SDK-methoden.</span><span class="sxs-lookup"><span data-stu-id="8ae12-129">This `azureEngagement` object will be used to access Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio met js-bestanden][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="8ae12-131">Realtime-bewaking inschakelen</span><span class="sxs-lookup"><span data-stu-id="8ae12-131">Enable real-time monitoring</span></span>
<span data-ttu-id="8ae12-132">U dient ten minste één activiteit naar de back-end van Mobile Engagement te sturen om te beginnen met het verzenden van gegevens en ervoor te zorgen dat de gebruikers actief zijn.</span><span class="sxs-lookup"><span data-stu-id="8ae12-132">In order to start sending data and ensuring that the users are active, you must send at least one Activity to the Mobile Engagement backend.</span></span> <span data-ttu-id="8ae12-133">Een activiteit in de context van een web-app is een webpagina.</span><span class="sxs-lookup"><span data-stu-id="8ae12-133">An activity in the context of a web app is a web page.</span></span> 

1. <span data-ttu-id="8ae12-134">Maak een nieuwe pagina met de naam **home.html** in uw oplossing en stel deze in als de startpagina van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="8ae12-134">Create a new page called **home.html** in your solution and set it as the starting page for your web app.</span></span> 
2. <span data-ttu-id="8ae12-135">Neem er de twee javascripts in op die we eerder aan deze pagina hebben toegevoegd door het volgende in de <body>-tag toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="8ae12-135">Include the two javascripts we added earlier in this page by adding the following within the body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="8ae12-136">Werk de <body>-tag bij zodat de `startActivity`-methode van EngagementAgent wordt aangeroepen</span><span class="sxs-lookup"><span data-stu-id="8ae12-136">Update the body tag to call EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="8ae12-137">Zo ziet uw **home.html**-pagina eruit</span><span class="sxs-lookup"><span data-stu-id="8ae12-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="8ae12-138">App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="8ae12-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="8ae12-139">Analyse uitbreiden</span><span class="sxs-lookup"><span data-stu-id="8ae12-139">Extend analytics</span></span>
<span data-ttu-id="8ae12-140">Dit zijn alle methoden die momenteel bij Web SDK beschikbaar zijn die u voor analyses kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8ae12-140">Here are all the methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="8ae12-141">Activiteiten/webpagina's:</span><span class="sxs-lookup"><span data-stu-id="8ae12-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="8ae12-142">Gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="8ae12-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="8ae12-143">Fouten</span><span class="sxs-lookup"><span data-stu-id="8ae12-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="8ae12-144">Taken</span><span class="sxs-lookup"><span data-stu-id="8ae12-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

