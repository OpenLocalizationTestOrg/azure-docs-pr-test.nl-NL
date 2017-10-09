---
title: aaaGet gestart met Azure Mobile Engagement voor Unity Android-implementatie
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en Pushmeldingen voor Unity-apps tooiOS apparaten implementeren.
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="e6d2c-103">Aan de slag met Azure Mobile Engagement voor Unity Android-implementatie</span><span class="sxs-lookup"><span data-stu-id="e6d2c-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e6d2c-104">Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand gebruik van uw Apps en hoe toosend push-meldingen toosegmented gebruikers van een Unity-toepassing bij het implementeren van tooan Android-apparaat.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan Android device.</span></span>
<span data-ttu-id="e6d2c-105">Deze zelfstudie maakt gebruik van Hallo klassieke Unity draaien een zelfstudie bDe volledige als Hallo beginpunt.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="e6d2c-106">U moet Hallo stappen in deze [zelfstudie](mobile-engagement-unity-roll-a-ball.md) voordat u doorgaat met de Hallo Mobile Engagement-integratie die we in Hallo onderstaande zelfstudie presenteren.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="e6d2c-107">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="e6d2c-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="e6d2c-108">Unity Editor</span><span class="sxs-lookup"><span data-stu-id="e6d2c-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="e6d2c-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="e6d2c-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="e6d2c-110">Google Android SDK</span><span class="sxs-lookup"><span data-stu-id="e6d2c-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="e6d2c-111">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e6d2c-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e6d2c-113">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="e6d2c-114"><a id="setup-azme"></a>Mobile Engagement instellen voor uw Android-app</span><span class="sxs-lookup"><span data-stu-id="e6d2c-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e6d2c-115"><a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="e6d2c-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="e6d2c-116">Hallo Unity-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="e6d2c-116">Import hello Unity package</span></span>
1. <span data-ttu-id="e6d2c-117">Hallo downloaden [Mobile Engagement Unity-pakket](https://aka.ms/azmeunitysdk) en sla het tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="e6d2c-118">Ga te**Assets -> Import Package -> Custom Package** en u hebt gedownload in Hallo hierboven stap Selecteer Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="e6d2c-119">Zorg dat alle bestanden zijn geselecteerd en klik op de knop **Import**.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="e6d2c-120">Nadat het importeren is voltooid, ziet u Hallo geïmporteerd SDK-bestanden in uw project.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="e6d2c-121">Hallo EngagementConfiguration bijwerken</span><span class="sxs-lookup"><span data-stu-id="e6d2c-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="e6d2c-122">Open Hallo **EngagementConfiguration** scriptbestand uit het SDK-map en werk Hallo Hallo **ANDROID\_verbinding\_tekenreeks** met Hallo-verbindingsreeks die u hebt verkregen oudere versies van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="e6d2c-123">Hallo-bestand opslaan</span><span class="sxs-lookup"><span data-stu-id="e6d2c-123">Save hello file</span></span> 
3. <span data-ttu-id="e6d2c-124">Voer **File -> Engagement -> Generate Android Manifest** uit.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="e6d2c-125">Dit is toegevoegd door Mobile Engagement SDK Hallo Hallo-invoegtoepassing en erop te klikken, wordt uw projectinstellingen automatisch bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-125">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="e6d2c-126">Hiervan ervoor tooexecute telkens wanneer u Hallo bijwerken **EngagementConfiguration** bestand anders uw wijzigingen niet worden doorgevoerd in Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-126">Make sure tooexecute this every time you update hello **EngagementConfiguration** file otherwise your changes will not be reflected in hello app.</span></span> 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="e6d2c-127">Hallo-app voor eenvoudig bijhouden configureren</span><span class="sxs-lookup"><span data-stu-id="e6d2c-127">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="e6d2c-128">Open Hallo **PlayerController** script gekoppeld toohello Player object bewerken.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-128">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="e6d2c-129">Voeg de volgende Hallo met de instructie:</span><span class="sxs-lookup"><span data-stu-id="e6d2c-129">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="e6d2c-130">Hallo na toohello toevoegen `Start()` methode</span><span class="sxs-lookup"><span data-stu-id="e6d2c-130">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="e6d2c-131">Implementeren en het Hallo-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e6d2c-131">Deploy and run hello app</span></span>
<span data-ttu-id="e6d2c-132">Zorg ervoor dat er Android SDK is geïnstalleerd op uw computer voordat u dit apparaat Unity-app tooyour probeert toodeploy.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-132">Make sure that you have Android SDK installed on your machine before attempting toodeploy this Unity app tooyour device.</span></span> 

1. <span data-ttu-id="e6d2c-133">Verbinding maken met een Android-apparaat tooyour-machine.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-133">Connect an Android device tooyour machine.</span></span> 
2. <span data-ttu-id="e6d2c-134">Open **File -> Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="e6d2c-135">Selecteer **Android** en klik vervolgens op **Switch Platform**.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="e6d2c-136">Klik op **Player settings** en geef een geldige bundel-id op.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="e6d2c-137">Klik tot slot op **Build And Run**.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="e6d2c-138">Hebt u mogelijk gevraagd tooprovide een map naam toostore hello Android-pakket.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-138">You may be asked tooprovide a folder name toostore hello Android package.</span></span> 
7. <span data-ttu-id="e6d2c-139">Als alles goed, gaat wordt Hallo pakket geïmplementeerde tooyour verbonden ziet apparaat en u de Unity-game op uw telefoon!</span><span class="sxs-lookup"><span data-stu-id="e6d2c-139">If everything goes fine, then hello package will be deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="e6d2c-140"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="e6d2c-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e6d2c-141"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="e6d2c-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="e6d2c-142">Hallo EngagementConfiguration bijwerken</span><span class="sxs-lookup"><span data-stu-id="e6d2c-142">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="e6d2c-143">Open Hallo **EngagementConfiguration** scriptbestand uit het SDK-map en werk Hallo Hallo **ANDROID\_GOOGLE\_getal** Hello **Google Project Aantal** u eerder hebt verkregen via Hallo Google Cloud Developer portal.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-143">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_GOOGLE\_NUMBER** with hello **Google Project Number** you obtained earlier from hello Google Cloud Developer portal.</span></span> <span data-ttu-id="e6d2c-144">Dit is een tekenreeks waarde dus zorg ervoor dat tooenclose deze tussen dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-144">This is a string value so make sure tooenclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="e6d2c-145">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-145">Save hello file.</span></span> 
3. <span data-ttu-id="e6d2c-146">Voer **File -> Engagement -> Generate Android Manifest** uit.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="e6d2c-147">Dit is toegevoegd door Mobile Engagement SDK Hallo Hallo-invoegtoepassing en erop te klikken, wordt uw projectinstellingen automatisch bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-147">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a><span data-ttu-id="e6d2c-148">Hallo app tooreceive meldingen configureren</span><span class="sxs-lookup"><span data-stu-id="e6d2c-148">Configure hello app tooreceive notifications</span></span>
1. <span data-ttu-id="e6d2c-149">Open Hallo **PlayerController** script gekoppeld toohello Player object bewerken.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-149">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="e6d2c-150">Hallo na toohello toevoegen `Start()` methode</span><span class="sxs-lookup"><span data-stu-id="e6d2c-150">Add hello following toohello `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="e6d2c-151">Nu dat hello app is bijgewerkt, implementeren en uitvoeren van Hallo-app op een apparaat per Hallo onderstaande instructies.</span><span class="sxs-lookup"><span data-stu-id="e6d2c-151">Now that hello app is updated, deploy and run hello app on a device per hello instructions provided below.</span></span> 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
