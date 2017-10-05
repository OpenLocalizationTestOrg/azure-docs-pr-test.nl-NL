---
title: Aan de slag met Azure Mobile Engagement voor Unity Android-implementatie
description: Informatie over het gebruik van Azure Mobile Engagement met analyses en pushmeldingen voor implementaties van Unity-apps op iOS-apparaten.
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
ms.openlocfilehash: bf0b758159d475b4ed7eadb84227e4824e11ba86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="ffbe9-103">Aan de slag met Azure Mobile Engagement voor Unity Android-implementatie</span><span class="sxs-lookup"><span data-stu-id="ffbe9-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="ffbe9-104">In dit onderwerp leest u hoe u Azure Mobile Engagement gebruikt om inzicht te krijgen in het gebruik van uw apps, en om pushmeldingen te verzenden aan gesegmenteerde gebruikers van een Unity-toepassing bij implementatie op een Android-apparaat.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an Android device.</span></span>
<span data-ttu-id="ffbe9-105">Deze zelfstudie maakt gebruik van de bekende Unity-zelfstudie 'Roll a Ball' als uitgangspunt.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="ffbe9-106">Volg de stappen in deze [zelfstudie](mobile-engagement-unity-roll-a-ball.md) voordat u doorgaat met de Mobile Engagement-integratie die we in de onderstaande zelfstudie presenteren.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="ffbe9-107">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="ffbe9-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="ffbe9-108">Unity Editor</span><span class="sxs-lookup"><span data-stu-id="ffbe9-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="ffbe9-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="ffbe9-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="ffbe9-110">Google Android SDK</span><span class="sxs-lookup"><span data-stu-id="ffbe9-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="ffbe9-111">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ffbe9-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ffbe9-113">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="ffbe9-114"><a id="setup-azme"></a>Mobile Engagement instellen voor uw Android-app</span><span class="sxs-lookup"><span data-stu-id="ffbe9-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="ffbe9-115"><a id="connecting-app"></a>Uw app verbinden met de back-end van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ffbe9-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="ffbe9-116">Het Unity-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="ffbe9-116">Import the Unity package</span></span>
1. <span data-ttu-id="ffbe9-117">Download het [Mobile Engagement Unity-pakket](https://aka.ms/azmeunitysdk) en sla het op uw lokale computer op.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="ffbe9-118">Ga naar **Assets -> Import Package -> Custom Package** en selecteer het pakket dat u in de vorige stap hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="ffbe9-119">Zorg dat alle bestanden zijn geselecteerd en klik op de knop **Import**.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="ffbe9-120">Wanneer het importeren is voltooid, ziet u de geïmporteerde SDK-bestanden in het project.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="ffbe9-121">EngagementConfiguration bijwerken</span><span class="sxs-lookup"><span data-stu-id="ffbe9-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="ffbe9-122">Open het scriptbestand **EngagementConfiguration** in de SDK-map en werk **ANDROID\_CONNECTION\_STRING** bij met de verbindingsreeks die u eerder hebt verkregen via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="ffbe9-123">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-123">Save the file</span></span> 
3. <span data-ttu-id="ffbe9-124">Voer **File -> Engagement -> Generate Android Manifest** uit.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="ffbe9-125">Dit is de invoegtoepassing die is toegevoegd door Mobile Engagement SDK. Klik erop om uw projectinstellingen automatisch bij te werken.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-125">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="ffbe9-126">Zorg ervoor dat u dit altijd doet wanneer u het bestand **EngagementConfiguration** bijwerkt, omdat uw wijzigingen anders niet worden doorgevoerd in de app.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-126">Make sure to execute this every time you update the **EngagementConfiguration** file otherwise your changes will not be reflected in the app.</span></span> 
> 
> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="ffbe9-127">De app voor eenvoudig bijhouden configureren</span><span class="sxs-lookup"><span data-stu-id="ffbe9-127">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="ffbe9-128">Open het script **PlayerController** dat is  gekoppeld aan het object Player om het te bewerken.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-128">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="ffbe9-129">Voeg het volgende toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="ffbe9-129">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="ffbe9-130">Het volgende toevoegen aan de methode `Start()`</span><span class="sxs-lookup"><span data-stu-id="ffbe9-130">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="ffbe9-131">De app implementeren en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ffbe9-131">Deploy and run the app</span></span>
<span data-ttu-id="ffbe9-132">Zorg voor dat Android SDK is geïnstalleerd op uw computer voordat u deze Unity-app op uw apparaat gaat implementeren.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-132">Make sure that you have Android SDK installed on your machine before attempting to deploy this Unity app to your device.</span></span> 

1. <span data-ttu-id="ffbe9-133">Sluit een Android-apparaat aan op de computer.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-133">Connect an Android device to your machine.</span></span> 
2. <span data-ttu-id="ffbe9-134">Open **File -> Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="ffbe9-135">Selecteer **Android** en klik vervolgens op **Switch Platform**.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="ffbe9-136">Klik op **Player settings** en geef een geldige bundel-id op.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="ffbe9-137">Klik tot slot op **Build And Run**.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="ffbe9-138">U wordt mogelijk gevraagd een mapnaam op te geven voor het opslaan van het Android-pakket.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-138">You may be asked to provide a folder name to store the Android package.</span></span> 
7. <span data-ttu-id="ffbe9-139">Als alles goed gaat, wordt het pakket geïmplementeerd op het aangesloten apparaat en ziet u de Unity-game op uw telefoon.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-139">If everything goes fine, then the package will be deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="ffbe9-140"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="ffbe9-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="ffbe9-141"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="ffbe9-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="ffbe9-142">EngagementConfiguration bijwerken</span><span class="sxs-lookup"><span data-stu-id="ffbe9-142">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="ffbe9-143">Open het scriptbestand **EngagementConfiguration** in de SDK-map en werk **ANDROID\_GOOGLE\_NUMBER** bij met het **Google Project Number** dat u eerder hebt verkregen via de Google Cloud Developer-portal.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-143">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_GOOGLE\_NUMBER** with the **Google Project Number** you obtained earlier from the Google Cloud Developer portal.</span></span> <span data-ttu-id="ffbe9-144">Dit is een tekenreeks die tussen dubbele aanhalingstekens moet worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-144">This is a string value so make sure to enclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="ffbe9-145">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-145">Save the file.</span></span> 
3. <span data-ttu-id="ffbe9-146">Voer **File -> Engagement -> Generate Android Manifest** uit.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="ffbe9-147">Dit is de invoegtoepassing die is toegevoegd door Mobile Engagement SDK. Klik erop om uw projectinstellingen automatisch bij te werken.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-147">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-the-app-to-receive-notifications"></a><span data-ttu-id="ffbe9-148">De app configureren voor het ontvangen van meldingen</span><span class="sxs-lookup"><span data-stu-id="ffbe9-148">Configure the app to receive notifications</span></span>
1. <span data-ttu-id="ffbe9-149">Open het script **PlayerController** dat is  gekoppeld aan het object Player om het te bewerken.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-149">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="ffbe9-150">Voeg het volgende toe aan de methode `Start()`.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-150">Add the following to the `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="ffbe9-151">Nu de app is bijgewerkt, kunt u die implementeren en uitvoeren op een apparaat aan de hand van de onderstaande instructies.</span><span class="sxs-lookup"><span data-stu-id="ffbe9-151">Now that the app is updated, deploy and run the app on a device per the instructions provided below.</span></span> 

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
