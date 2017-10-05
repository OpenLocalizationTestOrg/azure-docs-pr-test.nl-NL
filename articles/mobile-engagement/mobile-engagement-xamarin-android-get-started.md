---
title: Aan de slag met Azure Mobile Engagement voor Xamarin.Android
description: Informatie over het gebruik van Azure Mobile Engagement met analyses en pushmeldingen voor Xamarin.Android-apps.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 7b3d01b32c2d5a40448fc22861cd45f612238f2f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="e3c07-103">Aan de slag met Azure Mobile Engagement voor Xamarin.Android-apps</span><span class="sxs-lookup"><span data-stu-id="e3c07-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e3c07-104">In dit onderwerp leest u hoe u Azure Mobile Engagement gebruikt om inzicht te krijgen in het gebruik van uw apps, en om pushmeldingen te verzenden aan gesegmenteerde gebruikers van een Xamarin.Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e3c07-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="e3c07-105">Deze zelfstudie laat een eenvoudig broadcast-scenario met Mobile Engagement zien.</span><span class="sxs-lookup"><span data-stu-id="e3c07-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="e3c07-106">U maakt een lege Xamarin.Android-app die basisgegevens verzamelt en pushmeldingen ontvangt via Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="e3c07-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="e3c07-107">De Azure Mobile Engagement-service wordt in maart 2018 beëindigd en is momenteel alleen beschikbaar voor bestaande klanten.</span><span class="sxs-lookup"><span data-stu-id="e3c07-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="e3c07-108">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e3c07-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="e3c07-109">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="e3c07-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="e3c07-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="e3c07-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="e3c07-111">U kunt ook Visual Studio gebruiken met Xamarin, maar deze zelfstudie gebruikt Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="e3c07-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="e3c07-112">Zie [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installatie voor Visual Studio en Xamarin) voor installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="e3c07-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="e3c07-113">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="e3c07-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="e3c07-114">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="e3c07-114">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e3c07-115">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="e3c07-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e3c07-116">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e3c07-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="e3c07-117"><a id="setup-azme"></a>Mobile Engagement instellen voor uw Android-app</span><span class="sxs-lookup"><span data-stu-id="e3c07-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e3c07-118"><a id="connecting-app"></a>Uw app verbinden met de back-end van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e3c07-118"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="e3c07-119">Deze zelfstudie toont een ‘basisintegratie’, de minimale set die vereist is voor het verzamelen van gegevens en verzenden van een pushmelding.</span><span class="sxs-lookup"><span data-stu-id="e3c07-119">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="e3c07-120">We gaan een eenvoudige app maken met Xamarin Studio ter illustratie van de integratie.</span><span class="sxs-lookup"><span data-stu-id="e3c07-120">We will create a basic app with Xamarin Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="e3c07-121">Een nieuw Xamarin.Android-project maken</span><span class="sxs-lookup"><span data-stu-id="e3c07-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="e3c07-122">Start **Xamarin Studio** en ga naar **File** -> **New** -> **Solution**.</span><span class="sxs-lookup"><span data-stu-id="e3c07-122">Launch **Xamarin Studio** Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="e3c07-123">Selecteer **Android App**, controleer of de geselecteerde taal **C#** is en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="e3c07-123">Select **Android App** then make sure the selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="e3c07-124">Vul de velden **App Name** en **Organization Identifier** in.</span><span class="sxs-lookup"><span data-stu-id="e3c07-124">Fill in the **App Name** and the **Organization Identifier**.</span></span> <span data-ttu-id="e3c07-125">Zorg dat er een vinkje staat bij **Google Play Services** en klik vervolgens op **Next**.</span><span class="sxs-lookup"><span data-stu-id="e3c07-125">Make sure to checkmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="e3c07-126">Werk de velden **Project Name**, **Solution Name** en **Location** bij indien nodig en klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e3c07-126">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="e3c07-127">Xamarin Studio maakt de app waarin we Mobile Engagement gaan integreren.</span><span class="sxs-lookup"><span data-stu-id="e3c07-127">Xamarin Studio will create the app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="e3c07-128">Uw app verbinden met de back-end van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e3c07-128">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="e3c07-129">Klik met de rechtermuisknop op de map **Packages** in het venster Solution en selecteer **Add Packages…**.</span><span class="sxs-lookup"><span data-stu-id="e3c07-129">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="e3c07-130">Zoeken de **Microsoft Azure Mobile Engagement Xamarin SDK** en voeg die toe aan uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="e3c07-130">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="e3c07-131">Open **MainActivity.cs** en voeg het volgende toe met instructies:</span><span class="sxs-lookup"><span data-stu-id="e3c07-131">Open **MainActivity.cs** and add the following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="e3c07-132">In de methode `OnCreate` voegt u het volgende toe om de verbinding met de back-end van Mobile Engagement te initialiseren.</span><span class="sxs-lookup"><span data-stu-id="e3c07-132">In the `OnCreate` method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="e3c07-133">Zorg ervoor dat u uw **verbindingsreeks** toevoegt.</span><span class="sxs-lookup"><span data-stu-id="e3c07-133">Make sure to add your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="e3c07-134">Machtigingen en een servicedeclaratie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e3c07-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="e3c07-135">Open het bestand **Manifest.xml** onder de map Properties.</span><span class="sxs-lookup"><span data-stu-id="e3c07-135">Open up the **Manifest.xml** file under the Properties folder.</span></span> <span data-ttu-id="e3c07-136">Selecteer het tabblad Source zodat u de XML-bron direct kunt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e3c07-136">Select Source tab so that you directly update the XML source.</span></span>
2. <span data-ttu-id="e3c07-137">Voeg de volgende machtigingen toe aan het bestand Manifest.xml (dat zich bevindt onder de map **Properties**) van uw project, direct vóór of na de tag `<application>`:</span><span class="sxs-lookup"><span data-stu-id="e3c07-137">Add these permissions to the Manifest.xml (which can be found under the **Properties** folder) of your project immediately before or after the `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="e3c07-138">Voeg het volgende toe tussen de tags `<application>` en `</application>` om de agent-service te declareren:</span><span class="sxs-lookup"><span data-stu-id="e3c07-138">Add the following between the `<application>` and `</application>` tags to declare the agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="e3c07-139">In de code die u zojuist hebt geplakt, vervangt u `"<Your application name>"` in het label.</span><span class="sxs-lookup"><span data-stu-id="e3c07-139">In the code you just pasted, replace `"<Your application name>"` in the label.</span></span> <span data-ttu-id="e3c07-140">Dit wordt weergegeven in het menu **Instellingen**, waar gebruikers de services kunnen zien die worden uitgevoerd op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="e3c07-140">This is displayed in the **Settings** menu where users can see services running on the device.</span></span> <span data-ttu-id="e3c07-141">U kunt bijvoorbeeld het woord 'Service' aan dat label toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e3c07-141">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="e3c07-142">Een scherm naar Mobile Engagement verzenden</span><span class="sxs-lookup"><span data-stu-id="e3c07-142">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="e3c07-143">Om te beginnen met het verzenden van gegevens en ervoor te zorgen dat de gebruikers actief zijn, moet u ten minste één scherm naar de back-end van Mobile Engagement sturen.</span><span class="sxs-lookup"><span data-stu-id="e3c07-143">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span> <span data-ttu-id="e3c07-144">Om dit te doen zorgt u ervoor dat de `MainActivity` overneemt van `EngagementActivity` in plaats van `Activity`.</span><span class="sxs-lookup"><span data-stu-id="e3c07-144">For doing this - ensure that the `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="e3c07-145">Als u niet kunt overnemen van `EngagementActivity`, moet u vervolgens de methode `.StartActivity` en `.EndActivity` toevoegen in respectievelijk `OnResume` en `OnPause`.</span><span class="sxs-lookup"><span data-stu-id="e3c07-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="e3c07-146"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="e3c07-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e3c07-147"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="e3c07-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="e3c07-148">Met Mobile Engagement kunt u communiceren met uw gebruikers en ze bereiken met pushmeldingen en in-app-berichten in de context van campagnes.</span><span class="sxs-lookup"><span data-stu-id="e3c07-148">Mobile Engagement allows you to interact with and REACH your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="e3c07-149">Deze module heet REACH in de Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="e3c07-149">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="e3c07-150">In de volgende secties stelt u de app in om die te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e3c07-150">The following sections sets up your app to receive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
