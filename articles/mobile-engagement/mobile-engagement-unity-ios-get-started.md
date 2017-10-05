---
title: Aan de slag met Azure Mobile Engagement voor Unity iOS-implementatie
description: Informatie over het gebruik van Azure Mobile Engagement met analyses en pushmeldingen voor implementaties van Unity-apps op iOS-apparaten.
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c8f50404771965ec636065346ac04e059d264c3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="008fb-103">Aan de slag met Azure Mobile Engagement voor Unity iOS-implementatie</span><span class="sxs-lookup"><span data-stu-id="008fb-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="008fb-104">In dit onderwerp leest u hoe u Azure Mobile Engagement gebruikt om inzicht te krijgen in het gebruik van uw apps, en om pushmeldingen te verzenden aan gesegmenteerde gebruikers van een Unity-toepassing bij implementatie op een iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="008fb-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an iOS device.</span></span>
<span data-ttu-id="008fb-105">Deze zelfstudie maakt gebruik van de bekende Unity-zelfstudie ‘Roll a Ball’ als uitgangspunt.</span><span class="sxs-lookup"><span data-stu-id="008fb-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="008fb-106">Volg de stappen in deze [zelfstudie](mobile-engagement-unity-roll-a-ball.md) voordat u doorgaat met de Mobile Engagement-integratie die we in de onderstaande zelfstudie presenteren.</span><span class="sxs-lookup"><span data-stu-id="008fb-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="008fb-107">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="008fb-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="008fb-108">Unity Editor</span><span class="sxs-lookup"><span data-stu-id="008fb-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="008fb-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="008fb-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="008fb-110">XCode Editor</span><span class="sxs-lookup"><span data-stu-id="008fb-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="008fb-111">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="008fb-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="008fb-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="008fb-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="008fb-113">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="008fb-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="008fb-114"><a id="setup-azme"></a>Mobile Engagement instellen voor uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="008fb-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="008fb-115"><a id="connecting-app"></a>Uw app verbinden met de back-end van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="008fb-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="008fb-116">Het Unity-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="008fb-116">Import the Unity package</span></span>
1. <span data-ttu-id="008fb-117">Download het [Mobile Engagement Unity-pakket](https://aka.ms/azmeunitysdk) en sla het op uw lokale computer op.</span><span class="sxs-lookup"><span data-stu-id="008fb-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="008fb-118">Ga naar **Assets -> Import Package -> Custom Package** en selecteer het pakket dat u in de vorige stap hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="008fb-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="008fb-119">Zorg dat alle bestanden zijn geselecteerd en klik op de knop **Import**.</span><span class="sxs-lookup"><span data-stu-id="008fb-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="008fb-120">Wanneer het importeren is voltooid, ziet u de geïmporteerde SDK-bestanden in het project.</span><span class="sxs-lookup"><span data-stu-id="008fb-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="008fb-121">De EngagementConfiguration bijwerken</span><span class="sxs-lookup"><span data-stu-id="008fb-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="008fb-122">Open het scriptbestand **EngagementConfiguration** in de SDK-map en werk **IOS\_CONNECTION\_STRING** bij met de verbindingsreeks die u eerder hebt verkregen van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="008fb-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **IOS\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="008fb-123">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="008fb-123">Save the file.</span></span> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="008fb-124">De app voor eenvoudig bijhouden configureren</span><span class="sxs-lookup"><span data-stu-id="008fb-124">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="008fb-125">Open het script **PlayerController** dat is  gekoppeld aan het object Player om het te bewerken.</span><span class="sxs-lookup"><span data-stu-id="008fb-125">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="008fb-126">Voeg het volgende toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="008fb-126">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="008fb-127">Het volgende toevoegen aan de methode `Start()`</span><span class="sxs-lookup"><span data-stu-id="008fb-127">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="008fb-128">De app implementeren en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="008fb-128">Deploy and run the app</span></span>
1. <span data-ttu-id="008fb-129">Sluit een iOS-apparaat aan op de computer.</span><span class="sxs-lookup"><span data-stu-id="008fb-129">Connect an iOS device to your machine.</span></span> 
2. <span data-ttu-id="008fb-130">Open **File -> Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="008fb-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="008fb-131">Selecteer **iOS** en klik vervolgens op **Switch Platform**.</span><span class="sxs-lookup"><span data-stu-id="008fb-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="008fb-132">Klik op **Player settings** en geef een geldige bundel-id op.</span><span class="sxs-lookup"><span data-stu-id="008fb-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="008fb-133">Klik tot slot op **Build And Run**.</span><span class="sxs-lookup"><span data-stu-id="008fb-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="008fb-134">U wordt mogelijk gevraagd een mapnaam op te geven voor het opslaan van het iOS-pakket.</span><span class="sxs-lookup"><span data-stu-id="008fb-134">You may be asked to provide a folder name to store the iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="008fb-135">Als alles goed gaat, wordt het project gecompileerd en moet u het kunnen openen in XCode.</span><span class="sxs-lookup"><span data-stu-id="008fb-135">If everything goes fine, then the project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="008fb-136">Zorg ervoor dat de **Bundel-id** juist is in het project.</span><span class="sxs-lookup"><span data-stu-id="008fb-136">Make sure that the **Bundle identifier** is correct in the project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="008fb-137">Voer nu de app uit in XCode, zodat het pakket wordt geïmplementeerd op het aangesloten apparaat. Nu moet u de Unity-game zien op uw telefoon.</span><span class="sxs-lookup"><span data-stu-id="008fb-137">Now run the app in XCode so that the package is deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="008fb-138"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="008fb-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="008fb-139"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="008fb-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="008fb-140">Met Mobile Engagement kunt u communiceren met uw gebruikers en ze bereiken met pushmeldingen en in-app-berichten in de context van campagnes.</span><span class="sxs-lookup"><span data-stu-id="008fb-140">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="008fb-141">Deze module heet REACH in de Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="008fb-141">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="008fb-142">U hoeft verder niets te configureren in uw app als deze is al ingesteld voor het ontvangen van meldingen.</span><span class="sxs-lookup"><span data-stu-id="008fb-142">You don't have to do any additional configuration in your app to receive notifications and it is already setup for it.</span></span>

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
