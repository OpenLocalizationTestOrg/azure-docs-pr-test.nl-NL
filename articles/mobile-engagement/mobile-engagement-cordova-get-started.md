---
title: Aan de slag met Azure Mobile Engagement voor Cordova/Phonegap
description: Informatie over het gebruik van Azure Mobile Engagement met analyses en pushmeldingen voor Cordova-/Phonegap-apps.
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d7a761310782faab1dda023785f93cf90742e2ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="e3da1-103">Aan de slag met Azure Mobile Engagement voor Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="e3da1-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e3da1-104">In dit onderwerp leest u hoe u Azure Mobile Engagement gebruikt om inzicht te krijgen in het gebruik van uw apps en het verzenden van pushmeldingen aan gesegmenteerde gebruikers van een mobiele toepassing die is ontwikkeld met Cordova.</span><span class="sxs-lookup"><span data-stu-id="e3da1-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="e3da1-105">In deze zelfstudie maken we een lege Cordova-app met een Mac en integreren we vervolgens de Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="e3da1-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="e3da1-106">Deze app verzamelt analytische basisgegevens en ontvangt pushmeldingen via Apple Push Notification System (APNS) voor iOS en Google Cloud Messaging (GCM) voor Android.</span><span class="sxs-lookup"><span data-stu-id="e3da1-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="e3da1-107">We implementeren de app op een iOS- of Android-apparaat voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="e3da1-107">We will deploy this to an iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="e3da1-108">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="e3da1-108">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e3da1-109">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="e3da1-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e3da1-110">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e3da1-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="e3da1-111">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="e3da1-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="e3da1-112">XCode, dat u vanuit de Mac App Store kunt installeren (voor de iOS-implementatie)</span><span class="sxs-lookup"><span data-stu-id="e3da1-112">XCode, which you can install from Mac App Store (for deploying to iOS)</span></span>
* <span data-ttu-id="e3da1-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (voor de Android-implementatie)</span><span class="sxs-lookup"><span data-stu-id="e3da1-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying to Android)</span></span>
* <span data-ttu-id="e3da1-114">Pushmeldingscertificaat (.p12), dat u kunt verkrijgen via Apple Dev Center voor APNS</span><span class="sxs-lookup"><span data-stu-id="e3da1-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="e3da1-115">GCM-projectnummer, dat u kunt vinden in uw Google Developer-Console voor GCM</span><span class="sxs-lookup"><span data-stu-id="e3da1-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="e3da1-116">Cordova-invoegtoepassing voor Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e3da1-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="e3da1-117">U vindt de broncode en het Leesmij-bestand voor de Cordova-invoegtoepassing in [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="e3da1-117">You can find the source code and the ReadMe for the Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="e3da1-118"><a id="setup-azme"></a>Mobile Engagement instellen voor uw Cordova-app</span><span class="sxs-lookup"><span data-stu-id="e3da1-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e3da1-119"><a id="connecting-app"></a>Uw app verbinden met de back-end van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e3da1-119"><a id="connecting-app"></a>Connecting your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="e3da1-120">Deze zelfstudie toont een ‘basisintegratie’, de minimale set die vereist is voor het verzamelen van gegevens en verzenden van een pushmelding.</span><span class="sxs-lookup"><span data-stu-id="e3da1-120">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="e3da1-121">We gaan een eenvoudige app maken met Cordova ter illustratie van de integratie.</span><span class="sxs-lookup"><span data-stu-id="e3da1-121">We will create a basic app with Cordova to demonstrate the integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="e3da1-122">Nieuw Cordova-project maken</span><span class="sxs-lookup"><span data-stu-id="e3da1-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="e3da1-123">Start het *Terminal*-venster op uw Mac-computer en typ het volgende, waarmee een nieuw Cordova-project wordt gemaakt op basis van de standaardsjabloon.</span><span class="sxs-lookup"><span data-stu-id="e3da1-123">Launch *Terminal* window on your Mac machine and type the following which will create a new Cordova project from the default template.</span></span> <span data-ttu-id="e3da1-124">Zorg ervoor dat het publicatieprofiel waarmee u de iOS-app uiteindelijk zult implementeren 'com.mycompany.myapp' gebruikt als de App ID.</span><span class="sxs-lookup"><span data-stu-id="e3da1-124">Make sure that the publishing profile you eventually use to deploy your iOS app is using 'com.mycompany.myapp' as the App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="e3da1-125">Voer het volgende uit om uw project te configureren voor **iOS** en voer het uit in de iOS-simulator:</span><span class="sxs-lookup"><span data-stu-id="e3da1-125">Execute the following to configure your project for **iOS** and run it in the iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="e3da1-126">Voer het volgende uit om uw project te configureren voor **Android** en voer het uit in de Android-emulator:</span><span class="sxs-lookup"><span data-stu-id="e3da1-126">Execute the following to configure your project for **Android** and run it in the Android emulator.</span></span> <span data-ttu-id="e3da1-127">Zorg ervoor dat in de instellingen van uw Android SDK Emulator Google API's (Google Inc.) wordt gebruikt als Target, met de CPU/ABI als Google API's ARM.</span><span class="sxs-lookup"><span data-stu-id="e3da1-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with the CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="e3da1-128">Voeg de invoegtoepassing Cordova Console toe.</span><span class="sxs-lookup"><span data-stu-id="e3da1-128">Add the Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="e3da1-129">Uw app verbinden met de back-end van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e3da1-129">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="e3da1-130">Installeer de Cordova-invoegtoepassing voor Azure Mobile Engagement en geef de volgende waarden van variabelen op voor het configureren van de invoegtoepassing:</span><span class="sxs-lookup"><span data-stu-id="e3da1-130">Install the Azure Mobile Engagement Cordova plugin while providing the variable values to configure the plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers the app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="e3da1-131">*Android Reach Icon*: dit moet de naam van de resource zijn zonder een extensie of drawable voorvoegsel (voorbeeld: mynotificationicon), en het pictogrambestand moet worden gekopieerd naar uw Android-project (platforms/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="e3da1-131">*Android Reach Icon* : must be the name of the resource without any extension, nor drawable prefix (ex: mynotificationicon), and the icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="e3da1-132">*iOS Reach Icon*: dit moet de naam van de resource zijn met de extensie (bijvoorbeeld: mynotificationicon.png), en het pictogrambestand moet worden toegevoegd aan uw iOS-project met XCode (via het menu Add Files)</span><span class="sxs-lookup"><span data-stu-id="e3da1-132">*iOS Reach Icon*  : must be the name of the resource with its extension (ex:  mynotificationicon.png), and the icon file must be added into your iOS project with XCode (using the Add Files Menu)</span></span>

## <span data-ttu-id="e3da1-133"><a id="monitor"></a>Realtime-bewaking inschakelen</span><span class="sxs-lookup"><span data-stu-id="e3da1-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="e3da1-134">Ga naar het Cordova-project, bewerk **www/js/index.js** en voeg de aanroep van Mobile Engagement toe om een nieuwe activiteit te declareren zodra de gebeurtenis *deviceReady* is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e3da1-134">In the Cordova project - edit **www/js/index.js** to add the call to Mobile Engagement to declare a new activity once the *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="e3da1-135">Voer de toepassing uit:</span><span class="sxs-lookup"><span data-stu-id="e3da1-135">Run the application:</span></span>
   
   * <span data-ttu-id="e3da1-136">**Voor iOS**</span><span class="sxs-lookup"><span data-stu-id="e3da1-136">**For iOS**</span></span>
     
       <span data-ttu-id="e3da1-137">In het venster `Terminal` start u uw app in een nieuw exemplaar van de simulator door het volgende uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="e3da1-137">In `Terminal` window launch your app in a new Simulator instance by executing the following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="e3da1-138">**Voor Android**</span><span class="sxs-lookup"><span data-stu-id="e3da1-138">**For Android**</span></span>
     
       <span data-ttu-id="e3da1-139">In het venster `Terminal` start u uw app in een nieuw exemplaar van de emulator door het volgende uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="e3da1-139">In `Terminal` window launch your app in a new emulator instance by executing the following:</span></span>
     
           cordova run android
3. <span data-ttu-id="e3da1-140">U ziet het volgende in de logboeken van de console:</span><span class="sxs-lookup"><span data-stu-id="e3da1-140">You can see the following in the console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="e3da1-141"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="e3da1-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e3da1-142"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="e3da1-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="e3da1-143">Met Mobile Engagement kunt u communiceren met uw gebruikers via pushmeldingen en in-app-berichten in de context van campagnes.</span><span class="sxs-lookup"><span data-stu-id="e3da1-143">Mobile Engagement allows you to interact with your users using Push Notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="e3da1-144">Deze module heet REACH in de Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="e3da1-144">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="e3da1-145">In de volgende secties stelt u de app in om die te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e3da1-145">The following sections will setup your app to receive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="e3da1-146">Pushreferenties configureren voor Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e3da1-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="e3da1-147">Om Mobile Engagement pushmeldingen te laten verzenden namens u, moet u het toegang geven tot uw certificaat voor Apple iOS of de API-sleutel van GCM Server.</span><span class="sxs-lookup"><span data-stu-id="e3da1-147">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="e3da1-148">Navigeer naar uw Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="e3da1-148">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="e3da1-149">Zorg ervoor dat u zich bevindt in de app die we gebruiken voor dit project en klik vervolgens op de knop **Engage** onderaan:</span><span class="sxs-lookup"><span data-stu-id="e3da1-149">Ensure you're in the app we're using for this project and then click on the **Engage** button at the bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="e3da1-150">U gaat naar de instellingenpagina van de Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="e3da1-150">You will land in the settings page in your Engagement Portal.</span></span> <span data-ttu-id="e3da1-151">Klik op de sectie **Native pushbericht**:</span><span class="sxs-lookup"><span data-stu-id="e3da1-151">From there click on the **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="e3da1-152">iOS-certificaat/API-sleutel GCM Server configureren</span><span class="sxs-lookup"><span data-stu-id="e3da1-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="e3da1-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="e3da1-153">**[iOS]**</span></span>
   
    <span data-ttu-id="e3da1-154">a.</span><span class="sxs-lookup"><span data-stu-id="e3da1-154">a.</span></span> <span data-ttu-id="e3da1-155">Selecteer uw .p12, upload het en typ uw wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="e3da1-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="e3da1-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="e3da1-156">**[Android]**</span></span>
   
    <span data-ttu-id="e3da1-157">a.</span><span class="sxs-lookup"><span data-stu-id="e3da1-157">a.</span></span> <span data-ttu-id="e3da1-158">Klik op het bewerkingspictogram vóór **API-sleutel** in de sectie GCM-instellingen. In het pop-upvenster dat wordt weergegeven, plakt u de GCM Server-sleutel. Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3da1-158">Click the edit icon in front of **API Key** in the GCM Settings section and in the popup which shows up, paste the GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-the-cordova-app"></a><span data-ttu-id="e3da1-159">Pushmeldingen inschakelen in de Cordova-app</span><span class="sxs-lookup"><span data-stu-id="e3da1-159">Enable push notifications in the Cordova app</span></span>
<span data-ttu-id="e3da1-160">Bewerk **www/js/index.js** om de aanroep van Mobile Engagement voor het aanvragen van pushmeldingen toe te voegen en een handler te declareren:</span><span class="sxs-lookup"><span data-stu-id="e3da1-160">Edit **www/js/index.js** to add the call to Mobile Engagement to request push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-the-app"></a><span data-ttu-id="e3da1-161">De app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e3da1-161">Run the app</span></span>
<span data-ttu-id="e3da1-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="e3da1-162">**[iOS]**</span></span>

1. <span data-ttu-id="e3da1-163">We gebruiken XCode voor het bouwen en implementeren van de app op het apparaat om pushmeldingen te testen, omdat iOS alleen pushmeldingen naar een daadwerkelijk apparaat toestaat.</span><span class="sxs-lookup"><span data-stu-id="e3da1-163">We will use XCode to build and deploy the app on the device to test push notifications since iOS only allows push notifications to an actual device.</span></span> <span data-ttu-id="e3da1-164">Ga naar de locatie waar uw Cordova-project is gemaakt en navigeer naar de locatie **...\platforms\ios**.</span><span class="sxs-lookup"><span data-stu-id="e3da1-164">Go to the location where your Cordova project is created and navigate to **...\platforms\ios** location.</span></span> <span data-ttu-id="e3da1-165">Open het systeemeigen .xcodeproj-bestand in XCode.</span><span class="sxs-lookup"><span data-stu-id="e3da1-165">Open up the native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="e3da1-166">Bouw en implementeer de Cordova-app op het iOS-apparaat met het account dat beschikt over het inrichtingsprofiel met het certificaat dat u zojuist hebt geüpload en de app-id die overeenkomt met de id die u hebt opgegeven bij het maken van de Cordova-app.</span><span class="sxs-lookup"><span data-stu-id="e3da1-166">Build and deploy the Cordova app to the iOS device using the account which has the provisioning profile containing the certificate you just uploaded to the Mobile Engagement portal and the App Id which matches the one you provided while creating the Cordova app.</span></span> <span data-ttu-id="e3da1-167">Raadpleeg de *Bundle identifier* in het bestand **Resources\*-info.plist** in XCode om te zorgen dat ze overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="e3da1-167">You can check out the *Bundle identifier* in your **Resources\*-info.plist** file in XCode to match it up.</span></span> 
3. <span data-ttu-id="e3da1-168">U krijgt de standaard iOS-pop-up te zien op uw apparaat, waarin wordt gemeld dat de app verzoekt om machtigingen voor het verzenden van meldingen</span><span class="sxs-lookup"><span data-stu-id="e3da1-168">You will see the standard iOS popup on your device saying that the app requests permission to send notifications.</span></span> <span data-ttu-id="e3da1-169">Geef toestemming.</span><span class="sxs-lookup"><span data-stu-id="e3da1-169">Grant the permission.</span></span> 

<span data-ttu-id="e3da1-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="e3da1-170">**[Android]**</span></span>

<span data-ttu-id="e3da1-171">U kunt eenvoudigweg de emulator gebruiken om de Android-app uit te voeren, omdat GCM-meldingen door de Android-emulator worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e3da1-171">You can simply use the emulator to run the Android app as GCM notifications are supported on the Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="e3da1-172"><a id="send"></a>Een melding verzenden naar uw app</span><span class="sxs-lookup"><span data-stu-id="e3da1-172"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="e3da1-173">We gaan nu een eenvoudige pushmeldingcampagne maken waarbij een pushmelding wordt verzonden naar uw app op het apparaat:</span><span class="sxs-lookup"><span data-stu-id="e3da1-173">We will now create a simple Push Notification campaign that will send a push to your app running on the device:</span></span>

1. <span data-ttu-id="e3da1-174">Navigeer naar het tabblad **Reach** in uw Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="e3da1-174">Navigate to the **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="e3da1-175">Klik op **Nieuwe aankondiging** om uw pushcampagne te maken.</span><span class="sxs-lookup"><span data-stu-id="e3da1-175">Click **New Announcement** to create your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="e3da1-176">Informatie invoeren voor het maken van uw campagne **[Android]**</span><span class="sxs-lookup"><span data-stu-id="e3da1-176">Provide inputs to create your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="e3da1-177">Geef uw campagne een **naam**.</span><span class="sxs-lookup"><span data-stu-id="e3da1-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="e3da1-178">Selecteer als **Bezorgingstype**  *Systeemmelding* *Eenvoudig*.</span><span class="sxs-lookup"><span data-stu-id="e3da1-178">Select the **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="e3da1-179">Selecteer als **Leveringstijd** *Elk tijdstip*.</span><span class="sxs-lookup"><span data-stu-id="e3da1-179">Select the **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="e3da1-180">Geef een **titel** op voor de melding die als eerste zal worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="e3da1-180">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="e3da1-181">Geef een **bericht** op als de berichttekst van de melding.</span><span class="sxs-lookup"><span data-stu-id="e3da1-181">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="e3da1-182">Informatie invoeren voor het maken van uw campagne **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="e3da1-182">Provide inputs to create your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="e3da1-183">Geef uw campagne een **naam**.</span><span class="sxs-lookup"><span data-stu-id="e3da1-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="e3da1-184">Selecteer als **Leveringstijd** *Alleen buiten app*.</span><span class="sxs-lookup"><span data-stu-id="e3da1-184">Select the **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="e3da1-185">Geef een **titel** op voor de melding die als eerste zal worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="e3da1-185">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="e3da1-186">Geef een **bericht** op als de berichttekst van de melding.</span><span class="sxs-lookup"><span data-stu-id="e3da1-186">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="e3da1-187">Blader naar beneden en selecteer in het gedeelte inhoud **Alleen melding**.</span><span class="sxs-lookup"><span data-stu-id="e3da1-187">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="e3da1-188">[Optioneel] U kunt ook een actie-URL opgeven.</span><span class="sxs-lookup"><span data-stu-id="e3da1-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="e3da1-189">Zorg ervoor dat die gebruikmaakt van een URL-schema dat wordt opgegeven bij het configureren van de variabele **AZME\_REDIRECT\_URL** van de invoegtoepassing, bijvoorbeeld *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="e3da1-189">Make sure that it uses a URL scheme provided while configuring the plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="e3da1-190">U hebt nu een campagne gemaakt die zo eenvoudig mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="e3da1-190">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="e3da1-191">Blader nogmaals naar beneden en klik op de knop **Maken** om uw campagne op te slaan.</span><span class="sxs-lookup"><span data-stu-id="e3da1-191">Now scroll down again and click the **Create** button to save your campaign.</span></span>
8. <span data-ttu-id="e3da1-192">Ten slotte moet u uw campagne **activeren**.</span><span class="sxs-lookup"><span data-stu-id="e3da1-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="e3da1-193">U ziet nu een pushmelding op het apparaat of de emulator als onderdeel van deze campagne.</span><span class="sxs-lookup"><span data-stu-id="e3da1-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="e3da1-194"><a id="next-steps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3da1-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="e3da1-195">Overzicht van alle methoden beschikbaar met Cordova Mobile Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="e3da1-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

