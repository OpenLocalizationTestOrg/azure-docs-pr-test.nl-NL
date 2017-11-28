---
title: Aan de slag met Notification Hubs voor Xamarin.Android-apps | Microsoft Docs
description: In deze zelfstudie leert u hoe u met Azure Notification Hubs pushmeldingen verzendt naar een Xamarin.Android-toepassing.
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e0ef1b006a2b202c08a71caaff4ef4d763d50d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="ae2c9-103">Aan de slag met Notification Hubs met Xamarin voor Android</span><span class="sxs-lookup"><span data-stu-id="ae2c9-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ae2c9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ae2c9-104">Overview</span></span>
<span data-ttu-id="ae2c9-105">In deze zelfstudie wordt gedemonstreerd hoe u met Azure Notification Hubs pushmeldingen verzendt naar een Xamarin.Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Xamarin.Android application.</span></span>
<span data-ttu-id="ae2c9-106">U maakt een lege Xamarin.Android-app die pushmeldingen ontvangt via Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="ae2c9-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="ae2c9-107">Als u klaar bent, kunt u de Notification Hub gebruiken om pushmeldingen uit te zenden naar alle apparaten waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="ae2c9-108">De voltooide code is beschikbaar in het [NotificationHubs-app][GitHub]-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-108">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="ae2c9-109">In deze zelfstudie wordt een eenvoudig scenario voor het uitzenden met Notification Hubs beschreven.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-109">This tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ae2c9-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="ae2c9-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="ae2c9-111">De volledige code voor deze zelfstudie vindt u [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-111">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae2c9-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ae2c9-112">Prerequisites</span></span>
<span data-ttu-id="ae2c9-113">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-113">This tutorial requires the following:</span></span>

* <span data-ttu-id="ae2c9-114">Visual Studio met Xamarin in Windows of Xamarin Studio in Mac OS X. U vindt de volledige installatie-instructies in [Instellen en installeren voor Visual Studio en Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="ae2c9-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="ae2c9-115">Actief Google-account</span><span class="sxs-lookup"><span data-stu-id="ae2c9-115">Active Google account</span></span>
* <span data-ttu-id="ae2c9-116">[Azure Messaging-onderdeel]</span><span class="sxs-lookup"><span data-stu-id="ae2c9-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="ae2c9-117">[Google Cloud Messaging-clientonderdeel]</span><span class="sxs-lookup"><span data-stu-id="ae2c9-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="ae2c9-118">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Xamarin.Android-apps.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae2c9-119">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-119">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ae2c9-120">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ae2c9-121">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="ae2c9-122">Google Cloud Messaging inschakelen</span><span class="sxs-lookup"><span data-stu-id="ae2c9-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="ae2c9-123">Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="ae2c9-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="ae2c9-124">Klik op het tabblad <b>Configureren</b> bovenaan, voer de waarde voor <b>API-sleutel</b> in die u in de vorige sectie hebt verkregen en klik vervolgens op <b>Opslaan</b>.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-124">Click the <b>Configure</b> tab at the top, enter the <b>API Key</b> value you obtained in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="ae2c9-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="ae2c9-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="ae2c9-126">De Notification Hub is nu geconfigureerd om te werken met GCM en u hebt de verbindingsreeksen om uw app te registreren voor het ontvangen van meldingen en voor het verzenden van pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-126">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive notifications and to send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="ae2c9-127">Uw app verbinden met de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="ae2c9-127">Connect your app to the notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="ae2c9-128">Een nieuw project maken</span><span class="sxs-lookup"><span data-stu-id="ae2c9-128">Create a new project</span></span>
1. <span data-ttu-id="ae2c9-129">Klik in Xamarin Studio op **Nieuwe oplossing**, klik op **Android-app** en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="ae2c9-130">Voer uw **appnaam** en **id** in.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="ae2c9-131">Klik op de **doelplatforms** die u wilt ondersteunen en klik vervolgens op **Volgende** en **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-131">Click the **Target Plaforms** you want to support and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="ae2c9-132">Hierop wordt een nieuw Android-project gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="ae2c9-133">Open de projecteigenschappen door met de rechtermuisknop op het nieuwe project in de weergave Oplossing te klikken en **Opties** te kiezen.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-133">Open the project properties by right-clicking your new project in the Solution view and choosing **Options**.</span></span> <span data-ttu-id="ae2c9-134">Selecteer **Android-toepassing** in de sectie **Opbouwen**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-134">Select the **Android Application** item in the **Build** section.</span></span>
   
    <span data-ttu-id="ae2c9-135">Zorg ervoor dat de eerste letter van de **pakketnaam** een kleine letter is.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-135">Ensure that the first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ae2c9-136">De eerste letter van de pakketnaam moet een kleine letter zijn.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-136">The first letter of the package name must be lowercase.</span></span> <span data-ttu-id="ae2c9-137">Als dit niet zo is, worden er toepassingsmanifestfouten weergegeven wanneer u hieronder uw **BroadcastReceiver** en **IntentFilter** voor pushmeldingen registreert.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="ae2c9-138">U kunt **Minimumversie van Android** desgewenst instellen op een ander API-niveau.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-138">Optionally, set the **Minimum Android version** to another API Level.</span></span>
3. <span data-ttu-id="ae2c9-139">Ook kunt u **Doelversie van Android** instellen op een andere API-versie waarvoor u wilt ontwikkelen (dit moet een API-niveau 8 of hoger zijn).</span><span class="sxs-lookup"><span data-stu-id="ae2c9-139">Optionally, set the **Target Android version** to the another API version that you want to target (must be API level 8 or higher).</span></span>

<span data-ttu-id="ae2c9-140">Klik op **OK** en sluit het dialoogvenster Projectopties.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-140">Click **OK** and close the Project Options dialog.</span></span>

### <a name="add-the-required-components-to-your-project"></a><span data-ttu-id="ae2c9-141">De vereiste onderdelen toevoegen aan uw project</span><span class="sxs-lookup"><span data-stu-id="ae2c9-141">Add the required components to your project</span></span>
<span data-ttu-id="ae2c9-142">De Google Cloud Messaging-client die beschikbaar is in Xamarin Component Store vereenvoudigt het ondersteunen van pushmeldingen in Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-142">The Google Cloud Messaging Client available on the Xamarin Component Store simplifies the process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="ae2c9-143">Klik met de rechtermuisknop op de map Onderdelen in de Xamarin.Android-app en kies **Meer onderdelen ophalen**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-143">Right-click the Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="ae2c9-144">Zoek het onderdeel **Azure Messaging** en voeg dit toe aan het project.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-144">Search for the **Azure Messaging** component and add it to the project.</span></span>
3. <span data-ttu-id="ae2c9-145">Zoek het onderdeel **Google Cloud Messaging-client** en voeg dit toe aan het project.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-145">Search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="ae2c9-146">Notification Hubs in uw project instellen</span><span class="sxs-lookup"><span data-stu-id="ae2c9-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="ae2c9-147">Verzamel de volgende informatie voor uw Android-app en Notification Hub:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-147">Gather the following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="ae2c9-148">**GoogleProjectNumber**: haal deze projectnummerwaarde op uit het overzicht van uw app in de Google-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-148">**GoogleProjectNumber**:  Get this Project Number value from the overview of your app on the Google Developer Portal.</span></span> <span data-ttu-id="ae2c9-149">U hebt deze waarde genoteerd toen u de app in de portal maakte.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-149">You made a note of this value earlier when you created the app on the portal.</span></span>
   * <span data-ttu-id="ae2c9-150">**Verbindingsreeks voor luisteren**: klik op het dashboard in de [klassieke Azure Portal] op **Verbindingsreeksen weergeven**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-150">**Listen connection string**: On the dashboard in the [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="ae2c9-151">Kopieer de *DefaultListenSharedAccessSignature*-verbindingsreeks voor deze waarde.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-151">Copy the *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="ae2c9-152">**Hubnaam**: dit is de naam van uw hub uit de [klassieke Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="ae2c9-152">**Hub name**: This is the name of your hub from the [Azure Classic Portal].</span></span> <span data-ttu-id="ae2c9-153">Bijvoorbeeld *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="ae2c9-154">Maak een klasse **Constants.cs** voor uw Xamarin-project en definieer de volgende constantewaarden in de klasse.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-154">Create a **Constants.cs** class for your Xamarin project and define the following constant values in the class.</span></span> <span data-ttu-id="ae2c9-155">Vervang de tijdelijke aanduidingen door de waarden.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-155">Replace the placeholders with your values.</span></span>
     
       <span data-ttu-id="ae2c9-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="ae2c9-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="ae2c9-157">}</span><span class="sxs-lookup"><span data-stu-id="ae2c9-157">}</span></span>
2. <span data-ttu-id="ae2c9-158">Voeg de volgende using-instructies toe aan **MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-158">Add the following using statements to **MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="ae2c9-159">Voeg een exemplaarvariabele toe aan de klasse `MainActivity` die wordt gebruikt voor het weergeven van een waarschuwingsvenster wanneer de app wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-159">Add an instance variable to the `MainActivity` class that will be used to show an alert dialog when the app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="ae2c9-160">Maak de volgende methode in de klasse **MainActivity**:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-160">Create the following method in the **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="ae2c9-161">Initialiseer in de `OnCreate`-methode van **MainActivity.cs**de `instance`-variabele en voeg een aanroep naar `RegisterWithGCM` toe:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-161">In the `OnCreate` method of **MainActivity.cs**, initialize the `instance` variable and add a call to `RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from the "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="ae2c9-162">Maak een nieuwe klasse, **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ae2c9-163">U wordt hieronder begeleid bij het maken van een geheel nieuwe klasse **BroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="ae2c9-164">Voor een snel alternatief voor het handmatig maken van **MyBroadcastReceiver.cs** wordt u verwezen naar het bestand **GcmService.cs** in het Xamarin.Android-voorbeeldproject bij de [NotificationHubs-voorbeelden][GitHub].</span><span class="sxs-lookup"><span data-stu-id="ae2c9-164">However, a quick alternative to manually creating **MyBroadcastReceiver.cs** is to refer to the **GcmService.cs** file found in the sample Xamarin.Android project included with the [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="ae2c9-165">Het dupliceren van **GcmService.cs** en wijzigen van klassenamen kan ook een uitstekend uitgangspunt zijn.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-165">Duplicating **GcmService.cs** and changing class names can be a great place to start as well.</span></span>
   > 
   > 
7. <span data-ttu-id="ae2c9-166">Voeg de volgende using-instructies toe aan **MyBroadcastReceiver.cs** (waarbij u verwijst naar het onderdeel en de assembly die u eerder hebt toegevoegd):</span><span class="sxs-lookup"><span data-stu-id="ae2c9-166">Add the following using statements to **MyBroadcastReceiver.cs** (referring to the component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="ae2c9-167">Voeg in **MyBroadcastReceiver.cs** de volgende machtigingsaanvragen toe tussen de **using**-instructies en de **namespace**-declaratie:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-167">In **MyBroadcastReceiver.cs**, add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="ae2c9-168">Wijzig in **MyBroadcastReceiver.cs** de klasse **MyBroadcastReceiver** zodat deze overeenkomt met het volgende:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-168">In **MyBroadcastReceiver.cs**, change the **MyBroadcastReceiver** class to match the following:</span></span>
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. <span data-ttu-id="ae2c9-169">Voeg een andere klasse in **MyBroadcastReceiver.cs** toe met de naam **PushHandlerService** die is afgeleid van **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="ae2c9-170">Zorg ervoor dat het kenmerk **Service** op de klasse wordt toegepast:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-170">Make sure to apply the **Service** attribute to the class:</span></span>
    
         [Service] // Must use the service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="ae2c9-171">Met **GcmServiceBase** worden de volgende methoden geïmplementeerd: **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** en **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="ae2c9-172">De gebruikte **PushHandlerService**-implementatieklasse moet deze methoden overschrijven en deze methoden worden als reactie op de interactie met de Notification Hub geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response to interacting with the notification hub.</span></span>
12. <span data-ttu-id="ae2c9-173">Overschrijf de **OnRegistered()**-methode in **PushHandlerService** met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-173">Override the **OnRegistered()** method in **PushHandlerService** by using the following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "The device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > <span data-ttu-id="ae2c9-174">Zoals u ziet, kunnen met de bovenstaande **OnRegistered()**-code tags worden opgegeven om te registreren voor specifieke berichtenkanalen.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-174">In the **OnRegistered()** code above, you should note the ability to specify tags to register for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="ae2c9-175">Overschrijf de **OnMessage**-methode in **PushHandlerService** met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-175">Override the **OnMessage** method in **PushHandlerService** by using the following code:</span></span>
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. <span data-ttu-id="ae2c9-176">Voeg de volgende **createNotification**- en **dialogNotify**-methoden toe aan **PushHandlerService** om gebruikers te informeren als een melding wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-176">Add the following **createNotification** and **dialogNotify** methods to **PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ae2c9-177">Het meldingsontwerp in Android versie 5.0 en hoger wijkt aanzienlijk af van vorige versies.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="ae2c9-178">Als u dit met Android 5.0 of hoger test, moet de app actief zijn om de melding te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-178">If you test this on Android 5.0 or later, the app will need to be running to receive the notification.</span></span> <span data-ttu-id="ae2c9-179">Zie [Android-meldingen](http://go.microsoft.com/fwlink/?LinkId=615880) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent to show UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create the notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove the notification once the user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set the notification info
            //we use the pending intent, passing our ui intent over, which will get called
            //when the notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show the notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. <span data-ttu-id="ae2c9-180">Overschrijf abstracte leden **OnUnRegistered()**, **OnRecoverableError()** en **OnError()** zodat uw code wordt gecompileerd:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "The device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-the-emulator"></a><span data-ttu-id="ae2c9-181">Uw app uitvoeren in de emulator</span><span class="sxs-lookup"><span data-stu-id="ae2c9-181">Run your app in the emulator</span></span>
<span data-ttu-id="ae2c9-182">Als u deze app in de emulator uitvoert, gebruikt u een Android Virtual Device (AVD) dat ondersteuning biedt voor Google API's.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-182">If you run this app in the emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae2c9-183">Als u pushmeldingen wilt ontvangen, moet u een Google-account instellen op uw Android Virtual Device.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-183">In order to receive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="ae2c9-184">(Ga in de emulator naar **Instellingen** en klik op **Account toevoegen**.) Zorg er ook voor dat de emulator is verbonden met internet.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-184">(In the emulator, navigate to **Settings** and click **Add Account**.) Also, make sure that the emulator is connected to the Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="ae2c9-185">Het meldingsontwerp in Android versie 5.0 en hoger wijkt aanzienlijk af van vorige versies.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="ae2c9-186">Zie [Android-meldingen](http://go.microsoft.com/fwlink/?LinkId=615880) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="ae2c9-187">Klik in **Extra** op **Android Emulator Manager openen**, selecteer uw apparaat en klik vervolgens op **Bewerken**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="ae2c9-188">Selecteer **Google API's** in **Doel** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="ae2c9-189">Klik op de werkbalk aan de bovenkant op **Uitvoeren** en selecteer vervolgens uw app.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-189">On the top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="ae2c9-190">Hiermee start u de emulator en voert u de app uit.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-190">This starts the emulator and runs the app.</span></span>
   
   <span data-ttu-id="ae2c9-191">De app haalt de *registrationId* op uit GCM en wordt geregistreerd bij de Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-191">The app retrieves the *registrationId* from GCM and registers with the notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="ae2c9-192">Meldingen verzenden vanuit uw back-end</span><span class="sxs-lookup"><span data-stu-id="ae2c9-192">Send notifications from your backend</span></span>
<span data-ttu-id="ae2c9-193">U kunt de ontvangst van meldingen in uw app testen door meldingen in de [klassieke Azure Portal] te verzenden via het foutopsporingstabblad op de Notification Hub (zie onderstaande scherm).</span><span class="sxs-lookup"><span data-stu-id="ae2c9-193">You can test receiving notifications in your app by sending notifications in the [Azure Classic Portal] via the debug tab on the notification hub, as shown in the screen below.</span></span>

![][30]

<span data-ttu-id="ae2c9-194">Pushmeldingen worden gewoonlijk in een back-endservice zoals Mobile Services of ASP.NET verzonden met een compatibele bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="ae2c9-195">U kunt de REST API ook direct gebruiken om meldingsberichten te verzenden als er geen bibliotheek beschikbaar is voor uw back-end.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-195">You can also use the REST API directly to send notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="ae2c9-196">Hier volgt een lijst met andere zelfstudies die u kunt bekijken voor het verzenden van meldingen:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-196">Here is a list of some other tutorials that you may want to review for sending notifications:</span></span>

* <span data-ttu-id="ae2c9-197">ASP.NET: zie [Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden].</span><span class="sxs-lookup"><span data-stu-id="ae2c9-197">ASP.NET: See [Use Notification Hubs to push notifications to users].</span></span>
* <span data-ttu-id="ae2c9-198">Azure Notification Hubs Java SDK: zie [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) (Notification Hubs gebruiken vanuit Java) voor het verzenden van meldingen vanuit Java.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-198">Azure Notification Hubs Java SDK: See [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="ae2c9-199">Dit is getest in Eclipse voor Android-ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="ae2c9-200">PHP: zie [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md) (Notification Hubs gebruiken vanuit PHP).</span><span class="sxs-lookup"><span data-stu-id="ae2c9-200">PHP: See [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="ae2c9-201">In de volgende subsecties van de zelfstudie verzendt u meldingen met een .NET-console-app en met een mobiele service via een knooppuntscript.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-201">In the next subsections of the tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="ae2c9-202">(Optioneel) Meldingen verzenden met een .NET-app</span><span class="sxs-lookup"><span data-stu-id="ae2c9-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="ae2c9-203">In deze sectie worden meldingen verzonden met een .NET-console-app.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="ae2c9-204">Maak een nieuwe Visual C#-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="ae2c9-205">Klik in Visual Studio achtereenvolgens op **Extra**, **NuGet Package Manager** en **Package Manager-console**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="ae2c9-206">Hiermee wordt de Package Manager-console in Visual Studio weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-206">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="ae2c9-207">Stel in het venster Package Manager-console het **standaardproject** in op uw nieuwe consoletoepassingsproject en voer vervolgens in het consolevenster de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-207">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="ae2c9-208">Hiermee wordt een verwijzing toegevoegd aan de Azure Notification Hubs SDK met het <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-208">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="ae2c9-209">Open het bestand Program.cs en voeg de volgende `using`-instructie toe:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-209">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="ae2c9-210">Voeg in de klasse `Program` de volgende methode toe.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-210">In your `Program` class, add the following method.</span></span> <span data-ttu-id="ae2c9-211">Werk de tekst van de tijdelijke aanduidingen bij met uw *DefaultFullSharedAccessSignature*-verbindingsreeks en hubnaam uit de [klassieke Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="ae2c9-211">Update the placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from the [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="ae2c9-212">Voeg de volgende regels in de **Main**-methode toe:</span><span class="sxs-lookup"><span data-stu-id="ae2c9-212">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="ae2c9-213">Druk op de toets F5 om de app uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-213">Press the F5 key to run the app.</span></span> <span data-ttu-id="ae2c9-214">U ontvangt een melding in de app.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-214">You should receive a notification in the app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="ae2c9-215">(Optioneel) Meldingen verzenden met een mobiele service</span><span class="sxs-lookup"><span data-stu-id="ae2c9-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="ae2c9-216">Volg [Aan de slag met Mobile Services].</span><span class="sxs-lookup"><span data-stu-id="ae2c9-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="ae2c9-217">Meld u aan bij de [klassieke Azure Portal] en selecteer uw mobiele service.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-217">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="ae2c9-218">Selecteer het tabblad **Scheduler** aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-218">Select the **Scheduler** tab on the top.</span></span>
   
      ![][22]
4. <span data-ttu-id="ae2c9-219">Maak een nieuwe geplande taak, voeg een naam in en selecteer **Op aanvraag**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="ae2c9-220">Wanneer de taak is gemaakt, klikt u op de taaknaam.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-220">When the job is created, click the job name.</span></span> <span data-ttu-id="ae2c9-221">Klik vervolgens op het tabblad **Script** op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-221">Then click the **Script** tab on the top bar.</span></span>
6. <span data-ttu-id="ae2c9-222">Voeg het volgende script in de plannerfunctie in.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-222">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="ae2c9-223">Zorg ervoor dat de tijdelijke aanduidingen worden vervangen door de Notification Hub-naam en de verbindingsreeks voor *DefaultFullSharedAccessSignature* die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-223">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="ae2c9-224">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-224">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. <span data-ttu-id="ae2c9-225">Klik op **Eenmaal uitvoeren** op de balk onderaan.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-225">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="ae2c9-226">U ontvangt een pop-upmelding.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae2c9-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ae2c9-227">Next steps</span></span>
<span data-ttu-id="ae2c9-228">In dit eenvoudige voorbeeld hebt u meldingen uitgezonden naar al uw Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="ae2c9-228">In this simple example, you broadcasted notifications to all your Android devices.</span></span> <span data-ttu-id="ae2c9-229">Als u zich op specifieke gebruikers wilt richten, raadpleegt u de zelfstudie [Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden].</span><span class="sxs-lookup"><span data-stu-id="ae2c9-229">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="ae2c9-230">Als u gebruikers wilt indelen op belangengroepen, raadpleegt u [Notification Hubs gebruiken om belangrijk nieuws te verzenden].</span><span class="sxs-lookup"><span data-stu-id="ae2c9-230">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="ae2c9-231">Lees meer over het gebruik van Notification Hubs in [Richtlijnen voor Notification Hubs] en in [Notification Hubs-procedure voor Android].</span><span class="sxs-lookup"><span data-stu-id="ae2c9-231">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app to the Notification Hub]: #connecting-app
[Run your app with the emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="ae2c9-232">[Aan de slag met Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span><span class="sxs-lookup"><span data-stu-id="ae2c9-232">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span></span>
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

<span data-ttu-id="ae2c9-233">[klassieke Azure Portal]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="ae2c9-233">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
<span data-ttu-id="ae2c9-234">[Richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="ae2c9-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="ae2c9-235">[Notification Hubs-procedure voor Android]: http://msdn.microsoft.com/library/dn282661.aspx</span><span class="sxs-lookup"><span data-stu-id="ae2c9-235">[Notification Hubs How-To for Android]: http://msdn.microsoft.com/library/dn282661.aspx</span></span>

<span data-ttu-id="ae2c9-236">[Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="ae2c9-236">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="ae2c9-237">[Notification Hubs gebruiken om belangrijk nieuws te verzenden]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="ae2c9-237">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="ae2c9-238">[Google Cloud Messaging-clientonderdeel]: http://components.xamarin.com/view/GCMClient/</span><span class="sxs-lookup"><span data-stu-id="ae2c9-238">[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/</span></span>
<span data-ttu-id="ae2c9-239">[Azure Messaging-onderdeel]: http://components.xamarin.com/view/azure-messaging</span><span class="sxs-lookup"><span data-stu-id="ae2c9-239">[Azure Messaging Component]: http://components.xamarin.com/view/azure-messaging</span></span>
