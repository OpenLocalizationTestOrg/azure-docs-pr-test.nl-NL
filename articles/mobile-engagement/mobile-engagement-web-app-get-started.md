---
title: aaaGet de slag met Azure Mobile Engagement voor Web-Apps | Microsoft Docs
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en pushmeldingen voor Web-Apps.
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
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="67eb3-103">Aan de slag met Azure Mobile Engagement voor web-apps</span><span class="sxs-lookup"><span data-stu-id="67eb3-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="67eb3-104">Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand gebruik van uw Web-App.</span><span class="sxs-lookup"><span data-stu-id="67eb3-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="67eb3-105">Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten.</span><span class="sxs-lookup"><span data-stu-id="67eb3-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="67eb3-106">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="67eb3-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="67eb3-107">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="67eb3-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="67eb3-108">Visual Studio 2015 of een andere editor van uw keuze</span><span class="sxs-lookup"><span data-stu-id="67eb3-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="67eb3-109">Web SDK</span><span class="sxs-lookup"><span data-stu-id="67eb3-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="67eb3-110">Deze Web-SDK is Preview-versie en alleen Analytics Hallo momenteel ondersteunt en biedt geen ondersteuning voor pushmeldingen verzenden browser of in-app nog.</span><span class="sxs-lookup"><span data-stu-id="67eb3-110">This Web SDK is in Preview and only supports Analytics at hello moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="67eb3-111">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="67eb3-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="67eb3-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="67eb3-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="67eb3-113">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="67eb3-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="67eb3-114">Mobile Engagement instellen voor uw web-app</span><span class="sxs-lookup"><span data-stu-id="67eb3-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="67eb3-115"><a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="67eb3-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="67eb3-116">Deze zelfstudie toont een 'basisintegratie,' Hallo minimale set die vereist toocollect gegevens.</span><span class="sxs-lookup"><span data-stu-id="67eb3-116">This tutorial presents a "basic integration," which is hello minimal set required toocollect data.</span></span>

<span data-ttu-id="67eb3-117">We gaan een eenvoudige web-app maken met Visual Studio-integratie voor toodemonstrate hello, maar u Hallo met een webtoepassing die ook buiten Visual Studio gemaakt stappen kunt.</span><span class="sxs-lookup"><span data-stu-id="67eb3-117">We will create a basic web app with Visual Studio toodemonstrate hello integration though you can follow hello steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="67eb3-118">Een nieuwe web-app maken</span><span class="sxs-lookup"><span data-stu-id="67eb3-118">Create a new Web App</span></span>
<span data-ttu-id="67eb3-119">Hallo volgende stappen wordt ervan uitgegaan Hallo gebruik van Visual Studio 2015 al Hallo stappen vergelijkbaar in eerdere versies van Visual Studio zijn.</span><span class="sxs-lookup"><span data-stu-id="67eb3-119">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="67eb3-120">Start Visual Studio en in Hallo **Start** Schakel in het scherm **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="67eb3-120">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="67eb3-121">Selecteer in het pop-upvenster Hallo **Web** -> **ASP.Net-webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="67eb3-121">In hello pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="67eb3-122">Vul Hallo app **naam**, **locatie** en **oplossingsnaam**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="67eb3-122">Fill in hello app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="67eb3-123">In Hallo **Selecteer een sjabloon** pop-up Selecteer **leeg** onder **ASP.Net 4.5 sjablonen** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="67eb3-123">In hello **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="67eb3-124">U hebt nu een nieuwe lege Web-App-project waarin hello Azure Mobile Engagement Web SDK is geïntegreerd gemaakt.</span><span class="sxs-lookup"><span data-stu-id="67eb3-124">You have now created a new blank Web App project into which we will integrate hello Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="67eb3-125">Verbinding maken met uw app tooMobile Engagement back-end</span><span class="sxs-lookup"><span data-stu-id="67eb3-125">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="67eb3-126">Maak een nieuwe map **javascript** in uw oplossing en Hallo Web SDK JS bestand toevoegen **azure engagement.js** in de App.</span><span class="sxs-lookup"><span data-stu-id="67eb3-126">Create a new folder called **javascript** in your solution and add hello Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="67eb3-127">Voeg een nieuw bestand genaamd **main.js** in deze map javascript Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="67eb3-127">Add a new file called **main.js** in this javascript folder with hello following code.</span></span> <span data-ttu-id="67eb3-128">Zorg ervoor dat tooupdate Hallo-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="67eb3-128">Make sure tooupdate hello connection string.</span></span> <span data-ttu-id="67eb3-129">Dit `azureEngagement` -object worden gebruikte tooaccess Web SDK-methoden.</span><span class="sxs-lookup"><span data-stu-id="67eb3-129">This `azureEngagement` object will be used tooaccess Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio met js-bestanden][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="67eb3-131">Realtime-bewaking inschakelen</span><span class="sxs-lookup"><span data-stu-id="67eb3-131">Enable real-time monitoring</span></span>
<span data-ttu-id="67eb3-132">U moet ten minste één activiteit toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn.</span><span class="sxs-lookup"><span data-stu-id="67eb3-132">In order toostart sending data and ensuring that hello users are active, you must send at least one Activity toohello Mobile Engagement backend.</span></span> <span data-ttu-id="67eb3-133">Een activiteit in de context Hallo van een web-app is een webpagina.</span><span class="sxs-lookup"><span data-stu-id="67eb3-133">An activity in hello context of a web app is a web page.</span></span> 

1. <span data-ttu-id="67eb3-134">Maak een nieuwe pagina aangeroepen **home.html** in uw oplossing en als Hallo vanaf pagina voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="67eb3-134">Create a new page called **home.html** in your solution and set it as hello starting page for your web app.</span></span> 
2. <span data-ttu-id="67eb3-135">Hallo twee JavaScript die we eerder in deze pagina hebt toegevoegd door toe te voegen Hallo volgende binnen Hallo hoofdtekst tag bevatten.</span><span class="sxs-lookup"><span data-stu-id="67eb3-135">Include hello two javascripts we added earlier in this page by adding hello following within hello body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="67eb3-136">Hallo hoofdtekst tag toocall EngagementAgent van bijwerken `startActivity` methode</span><span class="sxs-lookup"><span data-stu-id="67eb3-136">Update hello body tag toocall EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="67eb3-137">Zo ziet uw **home.html**-pagina eruit</span><span class="sxs-lookup"><span data-stu-id="67eb3-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="67eb3-138">App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="67eb3-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="67eb3-139">Analyse uitbreiden</span><span class="sxs-lookup"><span data-stu-id="67eb3-139">Extend analytics</span></span>
<span data-ttu-id="67eb3-140">Hier zijn alle Hallo methoden beschikbaar met Web-SDK die u voor analyses kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="67eb3-140">Here are all hello methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="67eb3-141">Activiteiten/webpagina's:</span><span class="sxs-lookup"><span data-stu-id="67eb3-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="67eb3-142">Gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="67eb3-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="67eb3-143">Fouten</span><span class="sxs-lookup"><span data-stu-id="67eb3-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="67eb3-144">Taken</span><span class="sxs-lookup"><span data-stu-id="67eb3-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

