---
title: aaaGet gestart met Azure Mobile Engagement voor Unity iOS-implementatie
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en Pushmeldingen voor Unity-apps tooiOS apparaten implementeren.
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
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="d1d40-103">Aan de slag met Azure Mobile Engagement voor Unity iOS-implementatie</span><span class="sxs-lookup"><span data-stu-id="d1d40-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d1d40-104">Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand gebruik van uw Apps en hoe toosend push-meldingen toosegmented gebruikers van een Unity-toepassing bij het implementeren van tooan iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="d1d40-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan iOS device.</span></span>
<span data-ttu-id="d1d40-105">Deze zelfstudie maakt gebruik van Hallo klassieke Unity draaien een zelfstudie bDe volledige als Hallo beginpunt.</span><span class="sxs-lookup"><span data-stu-id="d1d40-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="d1d40-106">U moet Hallo stappen in deze [zelfstudie](mobile-engagement-unity-roll-a-ball.md) voordat u doorgaat met de Hallo Mobile Engagement-integratie die we in Hallo onderstaande zelfstudie presenteren.</span><span class="sxs-lookup"><span data-stu-id="d1d40-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="d1d40-107">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d1d40-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="d1d40-108">Unity Editor</span><span class="sxs-lookup"><span data-stu-id="d1d40-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="d1d40-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="d1d40-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="d1d40-110">XCode Editor</span><span class="sxs-lookup"><span data-stu-id="d1d40-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="d1d40-111">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="d1d40-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d1d40-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="d1d40-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d1d40-113">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d1d40-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="d1d40-114"><a id="setup-azme"></a>Mobile Engagement instellen voor uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="d1d40-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d1d40-115"><a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="d1d40-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="d1d40-116">Hallo Unity-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="d1d40-116">Import hello Unity package</span></span>
1. <span data-ttu-id="d1d40-117">Hallo downloaden [Mobile Engagement Unity-pakket](https://aka.ms/azmeunitysdk) en sla het tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="d1d40-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="d1d40-118">Ga te**Assets -> Import Package -> Custom Package** en u hebt gedownload in Hallo hierboven stap Selecteer Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="d1d40-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="d1d40-119">Zorg dat alle bestanden zijn geselecteerd en klik op de knop **Import**.</span><span class="sxs-lookup"><span data-stu-id="d1d40-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="d1d40-120">Nadat het importeren is voltooid, ziet u Hallo geïmporteerd SDK-bestanden in uw project.</span><span class="sxs-lookup"><span data-stu-id="d1d40-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="d1d40-121">Hallo EngagementConfiguration bijwerken</span><span class="sxs-lookup"><span data-stu-id="d1d40-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="d1d40-122">Open Hallo **EngagementConfiguration** scriptbestand uit het SDK-map en werk Hallo Hallo **IOS\_verbinding\_tekenreeks** met Hallo-verbindingsreeks die u eerder hebt verkregen. van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d1d40-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **IOS\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="d1d40-123">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="d1d40-123">Save hello file.</span></span> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="d1d40-124">Hallo-app voor eenvoudig bijhouden configureren</span><span class="sxs-lookup"><span data-stu-id="d1d40-124">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="d1d40-125">Open Hallo **PlayerController** script gekoppeld toohello Player object bewerken.</span><span class="sxs-lookup"><span data-stu-id="d1d40-125">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="d1d40-126">Voeg de volgende Hallo met de instructie:</span><span class="sxs-lookup"><span data-stu-id="d1d40-126">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="d1d40-127">Hallo na toohello toevoegen `Start()` methode</span><span class="sxs-lookup"><span data-stu-id="d1d40-127">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="d1d40-128">Implementeren en het Hallo-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d1d40-128">Deploy and run hello app</span></span>
1. <span data-ttu-id="d1d40-129">Verbinding maken met een iOS-apparaat tooyour machine.</span><span class="sxs-lookup"><span data-stu-id="d1d40-129">Connect an iOS device tooyour machine.</span></span> 
2. <span data-ttu-id="d1d40-130">Open **File -> Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="d1d40-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="d1d40-131">Selecteer **iOS** en klik vervolgens op **Switch Platform**.</span><span class="sxs-lookup"><span data-stu-id="d1d40-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="d1d40-132">Klik op **Player settings** en geef een geldige bundel-id op.</span><span class="sxs-lookup"><span data-stu-id="d1d40-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="d1d40-133">Klik tot slot op **Build And Run**.</span><span class="sxs-lookup"><span data-stu-id="d1d40-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="d1d40-134">Hebt u mogelijk gevraagd tooprovide een map naam toostore Hallo iOS-pakket.</span><span class="sxs-lookup"><span data-stu-id="d1d40-134">You may be asked tooprovide a folder name toostore hello iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="d1d40-135">Als alles goed gaat, Hallo project gecompileerd en u moet openen in uw XCode-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1d40-135">If everything goes fine, then hello project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="d1d40-136">Zorg ervoor dat Hallo **bundel-id** in Hallo project juist is.</span><span class="sxs-lookup"><span data-stu-id="d1d40-136">Make sure that hello **Bundle identifier** is correct in hello project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="d1d40-137">Nu Hallo app uitvoeren in XCode, zodat het Hallo-pakket geïmplementeerde tooyour aangesloten apparaat en ziet u de Unity-game op uw telefoon!</span><span class="sxs-lookup"><span data-stu-id="d1d40-137">Now run hello app in XCode so that hello package is deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="d1d40-138"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="d1d40-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d1d40-139"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="d1d40-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="d1d40-140">Mobile Engagement kunt u toointeract met uw gebruikers- en bereiken met pushmeldingen en in-app-berichten in Hallo context van campagnes.</span><span class="sxs-lookup"><span data-stu-id="d1d40-140">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="d1d40-141">Deze module heet REACH in Hallo Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="d1d40-141">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="d1d40-142">U hoeft toodo extra configuratie in uw app-meldingen tooreceive en is al ingesteld voor het.</span><span class="sxs-lookup"><span data-stu-id="d1d40-142">You don't have toodo any additional configuration in your app tooreceive notifications and it is already setup for it.</span></span>

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
