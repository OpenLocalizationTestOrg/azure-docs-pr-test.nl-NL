---
title: aaaGet slag met Notification Hubs voor Xamarin.Android-apps | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Xamarin.android-toepassing.
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
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="72ae6-103">Aan de slag met Notification Hubs met Xamarin voor Android</span><span class="sxs-lookup"><span data-stu-id="72ae6-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="72ae6-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="72ae6-104">Overview</span></span>
<span data-ttu-id="72ae6-105">Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Xamarin.Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="72ae6-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Xamarin.Android application.</span></span>
<span data-ttu-id="72ae6-106">U maakt een lege Xamarin.Android-app die pushmeldingen ontvangt via Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="72ae6-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="72ae6-107">Wanneer u klaar bent, moet u kunnen toouse push uw notification hub toobroadcast meldingen tooall Hallo apparaten waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="72ae6-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="72ae6-108">Hallo voltooide code is beschikbaar in Hallo [NotificationHubs-app] [ GitHub] voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="72ae6-108">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="72ae6-109">Deze zelfstudie wordt Hallo eenvoudige scenario uitzenden met Notification hubs beschreven.</span><span class="sxs-lookup"><span data-stu-id="72ae6-109">This tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="72ae6-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="72ae6-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="72ae6-111">Hallo voltooid code voor deze zelfstudie kunt u vinden op GitHub [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="72ae6-111">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72ae6-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="72ae6-112">Prerequisites</span></span>
<span data-ttu-id="72ae6-113">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="72ae6-113">This tutorial requires hello following:</span></span>

* <span data-ttu-id="72ae6-114">Visual Studio met Xamarin in Windows of Xamarin Studio in Mac OS X. U vindt de volledige installatie-instructies in [Instellen en installeren voor Visual Studio en Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="72ae6-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="72ae6-115">Actief Google-account</span><span class="sxs-lookup"><span data-stu-id="72ae6-115">Active Google account</span></span>
* <span data-ttu-id="72ae6-116">[Azure Messaging-onderdeel]</span><span class="sxs-lookup"><span data-stu-id="72ae6-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="72ae6-117">[Google Cloud Messaging-clientonderdeel]</span><span class="sxs-lookup"><span data-stu-id="72ae6-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="72ae6-118">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Xamarin.Android-apps.</span><span class="sxs-lookup"><span data-stu-id="72ae6-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72ae6-119">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="72ae6-119">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="72ae6-120">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="72ae6-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="72ae6-121">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="72ae6-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="72ae6-122">Google Cloud Messaging inschakelen</span><span class="sxs-lookup"><span data-stu-id="72ae6-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="72ae6-123">Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="72ae6-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="72ae6-124">Klik op Hallo <b>configureren</b> tabblad Hallo bovenaan, Voer Hallo <b>API-sleutel</b> waarde als u hebt verkregen in de vorige sectie Hallo en klik vervolgens op <b>opslaan</b>.</span><span class="sxs-lookup"><span data-stu-id="72ae6-124">Click hello <b>Configure</b> tab at hello top, enter hello <b>API Key</b> value you obtained in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="72ae6-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="72ae6-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="72ae6-126">Uw notification hub is nu geconfigureerd toowork bij GCM en u Hallo verbinding tekenreeksen tooboth uw app tooreceive meldingen en toosend pushmeldingen registreren hebt.</span><span class="sxs-lookup"><span data-stu-id="72ae6-126">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive notifications and toosend push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="72ae6-127">Verbinding maken met uw app toohello notification hub</span><span class="sxs-lookup"><span data-stu-id="72ae6-127">Connect your app toohello notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="72ae6-128">Een nieuw project maken</span><span class="sxs-lookup"><span data-stu-id="72ae6-128">Create a new project</span></span>
1. <span data-ttu-id="72ae6-129">Klik in Xamarin Studio op **Nieuwe oplossing**, klik op **Android-app** en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="72ae6-130">Voer uw **appnaam** en **id** in.</span><span class="sxs-lookup"><span data-stu-id="72ae6-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="72ae6-131">Klik op Hallo **doelplatforms** u toosupport wilt en klik vervolgens op **volgende** en **maken**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-131">Click hello **Target Plaforms** you want toosupport and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="72ae6-132">Hierop wordt een nieuw Android-project gemaakt.</span><span class="sxs-lookup"><span data-stu-id="72ae6-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="72ae6-133">Hallo Projecteigenschappen openen met de rechtermuisknop op het nieuwe project in Hallo weergave oplossing kiezen **opties**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-133">Open hello project properties by right-clicking your new project in hello Solution view and choosing **Options**.</span></span> <span data-ttu-id="72ae6-134">Selecteer Hallo **Android-toepassing** item in Hallo **bouwen** sectie.</span><span class="sxs-lookup"><span data-stu-id="72ae6-134">Select hello **Android Application** item in hello **Build** section.</span></span>
   
    <span data-ttu-id="72ae6-135">Zorg ervoor dat Hallo eerste letter van uw **pakketnaam** in kleine letters.</span><span class="sxs-lookup"><span data-stu-id="72ae6-135">Ensure that hello first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="72ae6-136">de eerste letter Hallo van Hallo pakketnaam moet een kleine letter.</span><span class="sxs-lookup"><span data-stu-id="72ae6-136">hello first letter of hello package name must be lowercase.</span></span> <span data-ttu-id="72ae6-137">Als dit niet zo is, worden er toepassingsmanifestfouten weergegeven wanneer u hieronder uw **BroadcastReceiver** en **IntentFilter** voor pushmeldingen registreert.</span><span class="sxs-lookup"><span data-stu-id="72ae6-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="72ae6-138">Eventueel set Hallo **minimumversie van android** tooanother API-niveau.</span><span class="sxs-lookup"><span data-stu-id="72ae6-138">Optionally, set hello **Minimum Android version** tooanother API Level.</span></span>
3. <span data-ttu-id="72ae6-139">Eventueel set Hallo **doelversie van android** toohello een andere API-versie die u wilt dat tootarget (moet API-niveau 8 of hoger).</span><span class="sxs-lookup"><span data-stu-id="72ae6-139">Optionally, set hello **Target Android version** toohello another API version that you want tootarget (must be API level 8 or higher).</span></span>

<span data-ttu-id="72ae6-140">Klik op **OK** en sluiten Hallo Projectopties dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="72ae6-140">Click **OK** and close hello Project Options dialog.</span></span>

### <a name="add-hello-required-components-tooyour-project"></a><span data-ttu-id="72ae6-141">Hallo vereiste onderdelen tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="72ae6-141">Add hello required components tooyour project</span></span>
<span data-ttu-id="72ae6-142">Hallo Google Cloud Messaging-Client beschikbaar is op Hallo Xamarin Component Store vereenvoudigt Hallo ondersteunen van pushmeldingen in Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="72ae6-142">hello Google Cloud Messaging Client available on hello Xamarin Component Store simplifies hello process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="72ae6-143">Met de rechtermuisknop op de map voor Hallo-onderdelen in de Xamarin.Android-app en kies **meer onderdelen ophalen**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-143">Right-click hello Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="72ae6-144">Zoeken naar Hallo **Azure Messaging** onderdeel en toe te voegen toohello project.</span><span class="sxs-lookup"><span data-stu-id="72ae6-144">Search for hello **Azure Messaging** component and add it toohello project.</span></span>
3. <span data-ttu-id="72ae6-145">Zoeken naar Hallo **Google Cloud Messaging-Client** onderdeel en toe te voegen toohello project.</span><span class="sxs-lookup"><span data-stu-id="72ae6-145">Search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="72ae6-146">Notification Hubs in uw project instellen</span><span class="sxs-lookup"><span data-stu-id="72ae6-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="72ae6-147">Verzamel de volgende informatie voor uw Android-app en notification hub Hallo:</span><span class="sxs-lookup"><span data-stu-id="72ae6-147">Gather hello following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="72ae6-148">**GoogleProjectNumber**: dit Project Number-waarde niet ophalen uit Hallo overzicht van uw app op Hallo Google Developer-Portal.</span><span class="sxs-lookup"><span data-stu-id="72ae6-148">**GoogleProjectNumber**:  Get this Project Number value from hello overview of your app on hello Google Developer Portal.</span></span> <span data-ttu-id="72ae6-149">U hebt aangebracht een notitie van deze waarde genoteerd toen u Hallo-app op Hallo portal gemaakt.</span><span class="sxs-lookup"><span data-stu-id="72ae6-149">You made a note of this value earlier when you created hello app on hello portal.</span></span>
   * <span data-ttu-id="72ae6-150">**Verbindingsreeks voor luisteren**: op Hallo dashboard in Hallo [klassieke Azure-Portal], klikt u op **verbindingsreeksen weergeven**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-150">**Listen connection string**: On hello dashboard in hello [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="72ae6-151">Kopiëren Hallo *DefaultListenSharedAccessSignature* verbindingsreeks voor deze waarde.</span><span class="sxs-lookup"><span data-stu-id="72ae6-151">Copy hello *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="72ae6-152">**Hubnaam**: dit is de naam Hallo van uw hub uit Hallo [klassieke Azure-Portal].</span><span class="sxs-lookup"><span data-stu-id="72ae6-152">**Hub name**: This is hello name of your hub from hello [Azure Classic Portal].</span></span> <span data-ttu-id="72ae6-153">Bijvoorbeeld *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="72ae6-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="72ae6-154">Maak een **Constants.cs** klasse voor uw Xamarin-project en definieer Hallo constante waarden in de klasse hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="72ae6-154">Create a **Constants.cs** class for your Xamarin project and define hello following constant values in hello class.</span></span> <span data-ttu-id="72ae6-155">Vervang Hallo tijdelijke aanduidingen door uw waarden.</span><span class="sxs-lookup"><span data-stu-id="72ae6-155">Replace hello placeholders with your values.</span></span>
     
       <span data-ttu-id="72ae6-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="72ae6-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="72ae6-157">}</span><span class="sxs-lookup"><span data-stu-id="72ae6-157">}</span></span>
2. <span data-ttu-id="72ae6-158">Voeg de volgende Hallo using-instructies te**MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="72ae6-158">Add hello following using statements too**MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="72ae6-159">Toevoegen van een variabele toohello exemplaar `MainActivity` klasse die gebruikt tooshow een waarschuwingsvenster worden wanneer Hallo-app wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="72ae6-159">Add an instance variable toohello `MainActivity` class that will be used tooshow an alert dialog when hello app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="72ae6-160">Maken van de volgende methode in Hallo Hallo **MainActivity** klasse:</span><span class="sxs-lookup"><span data-stu-id="72ae6-160">Create hello following method in hello **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="72ae6-161">In Hallo `OnCreate` methode van **MainActivity.cs**, initialiseren Hallo `instance` variabele en voeg een aanroep te`RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="72ae6-161">In hello `OnCreate` method of **MainActivity.cs**, initialize hello `instance` variable and add a call too`RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="72ae6-162">Maak een nieuwe klasse, **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="72ae6-163">U wordt hieronder begeleid bij het maken van een geheel nieuwe klasse **BroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="72ae6-164">Echter, het maken van een snelle alternatieve toomanually **MyBroadcastReceiver.cs** toorefer toohello is **GcmService.cs** bestand vinden in het Hallo Xamarin.Android-voorbeeldproject opgenomen Hello [NotificationHubs-voorbeelden][GitHub].</span><span class="sxs-lookup"><span data-stu-id="72ae6-164">However, a quick alternative toomanually creating **MyBroadcastReceiver.cs** is toorefer toohello **GcmService.cs** file found in hello sample Xamarin.Android project included with hello [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="72ae6-165">Het dupliceren van **GcmService.cs** en wijzigen van klassenamen kan ook een goede plaats-toostart.</span><span class="sxs-lookup"><span data-stu-id="72ae6-165">Duplicating **GcmService.cs** and changing class names can be a great place toostart as well.</span></span>
   > 
   > 
7. <span data-ttu-id="72ae6-166">Voeg de volgende Hallo using-instructies te**MyBroadcastReceiver.cs** (verwijst toohello onderdeel en de assembly die u eerder hebt toegevoegd):</span><span class="sxs-lookup"><span data-stu-id="72ae6-166">Add hello following using statements too**MyBroadcastReceiver.cs** (referring toohello component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="72ae6-167">In **MyBroadcastReceiver.cs**, toevoegen van de volgende machtigingsaanvragen tussen Hallo Hallo **met** -instructies en Hallo **naamruimte** declaratie:</span><span class="sxs-lookup"><span data-stu-id="72ae6-167">In **MyBroadcastReceiver.cs**, add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="72ae6-168">In **MyBroadcastReceiver.cs**, Hallo wijzigen **MyBroadcastReceiver** toomatch Hallo volgende klasse:</span><span class="sxs-lookup"><span data-stu-id="72ae6-168">In **MyBroadcastReceiver.cs**, change hello **MyBroadcastReceiver** class toomatch hello following:</span></span>
   
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
10. <span data-ttu-id="72ae6-169">Voeg een andere klasse in **MyBroadcastReceiver.cs** toe met de naam **PushHandlerService** die is afgeleid van **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="72ae6-170">Zorg ervoor dat tooapply hello **Service** toohello kenmerkklasse:</span><span class="sxs-lookup"><span data-stu-id="72ae6-170">Make sure tooapply hello **Service** attribute toohello class:</span></span>
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="72ae6-171">Met **GcmServiceBase** worden de volgende methoden geïmplementeerd: **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** en **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="72ae6-172">Onze **PushHandlerService** implementatieklasse moet deze methoden overschrijven en deze methoden antwoord toointeracting bij Hallo notification hub wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="72ae6-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response toointeracting with hello notification hub.</span></span>
12. <span data-ttu-id="72ae6-173">Hallo overschrijven **OnRegistered()** methode in **PushHandlerService** met behulp van de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="72ae6-173">Override hello **OnRegistered()** method in **PushHandlerService** by using hello following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
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
    > <span data-ttu-id="72ae6-174">In Hallo **OnRegistered()** code hierboven, let u Hallo mogelijkheid toospecify labels tooregister voor specifieke berichtenkanalen.</span><span class="sxs-lookup"><span data-stu-id="72ae6-174">In hello **OnRegistered()** code above, you should note hello ability toospecify tags tooregister for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="72ae6-175">Hallo overschrijven **OnMessage** methode in **PushHandlerService** met behulp van de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="72ae6-175">Override hello **OnMessage** method in **PushHandlerService** by using hello following code:</span></span>
    
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
14. <span data-ttu-id="72ae6-176">Voeg de volgende Hallo **createNotification** en **dialogNotify** methoden te**PushHandlerService** om gebruikers te informeren wanneer een melding wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="72ae6-176">Add hello following **createNotification** and **dialogNotify** methods too**PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="72ae6-177">Het meldingsontwerp in Android versie 5.0 en hoger wijkt aanzienlijk af van vorige versies.</span><span class="sxs-lookup"><span data-stu-id="72ae6-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="72ae6-178">Als u dit op Android 5.0 of hoger testen moet Hallo app toobe tooreceive Hallo melding uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="72ae6-178">If you test this on Android 5.0 or later, hello app will need toobe running tooreceive hello notification.</span></span> <span data-ttu-id="72ae6-179">Zie [Android-meldingen](http://go.microsoft.com/fwlink/?LinkId=615880) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="72ae6-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
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
15. <span data-ttu-id="72ae6-180">Overschrijf abstracte leden **OnUnRegistered()**, **OnRecoverableError()** en **OnError()** zodat uw code wordt gecompileerd:</span><span class="sxs-lookup"><span data-stu-id="72ae6-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
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

## <a name="run-your-app-in-hello-emulator"></a><span data-ttu-id="72ae6-181">Uitvoeren van uw app in Hallo-emulator</span><span class="sxs-lookup"><span data-stu-id="72ae6-181">Run your app in hello emulator</span></span>
<span data-ttu-id="72ae6-182">Als u deze app in Hallo-emulator uitvoert, zorg ervoor dat u een Android Virtual Device (AVD) die ondersteuning biedt voor Google APIs gebruikt.</span><span class="sxs-lookup"><span data-stu-id="72ae6-182">If you run this app in hello emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72ae6-183">In de volgorde tooreceive pushmeldingen, moet u een Google-account instellen op uw Android Virtual Device.</span><span class="sxs-lookup"><span data-stu-id="72ae6-183">In order tooreceive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="72ae6-184">(In Hallo-emulator te navigeren**instellingen** en klik op **Account toevoegen**.) Zorg ook dat Hallo-emulator is verbonden toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="72ae6-184">(In hello emulator, navigate too**Settings** and click **Add Account**.) Also, make sure that hello emulator is connected toohello Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="72ae6-185">Het meldingsontwerp in Android versie 5.0 en hoger wijkt aanzienlijk af van vorige versies.</span><span class="sxs-lookup"><span data-stu-id="72ae6-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="72ae6-186">Zie [Android-meldingen](http://go.microsoft.com/fwlink/?LinkId=615880) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="72ae6-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="72ae6-187">Klik in **Extra** op **Android Emulator Manager openen**, selecteer uw apparaat en klik vervolgens op **Bewerken**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="72ae6-188">Selecteer **Google API's** in **Doel** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="72ae6-189">Op de bovenste werkbalk Hallo **uitvoeren**, en selecteer vervolgens uw app.</span><span class="sxs-lookup"><span data-stu-id="72ae6-189">On hello top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="72ae6-190">Hiermee start Hallo-emulator en Hallo app uitvoert.</span><span class="sxs-lookup"><span data-stu-id="72ae6-190">This starts hello emulator and runs hello app.</span></span>
   
   <span data-ttu-id="72ae6-191">Hallo app haalt Hallo *registrationId* van GCM en wordt geregistreerd bij Hallo notification hub.</span><span class="sxs-lookup"><span data-stu-id="72ae6-191">hello app retrieves hello *registrationId* from GCM and registers with hello notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="72ae6-192">Meldingen verzenden vanuit uw back-end</span><span class="sxs-lookup"><span data-stu-id="72ae6-192">Send notifications from your backend</span></span>
<span data-ttu-id="72ae6-193">U kunt testen ontvangst van meldingen in uw app door meldingen te verzenden in Hallo [klassieke Azure-Portal] via Hallo debug tabblad op Hallo notification hub, zoals wordt weergegeven in onderstaande welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="72ae6-193">You can test receiving notifications in your app by sending notifications in hello [Azure Classic Portal] via hello debug tab on hello notification hub, as shown in hello screen below.</span></span>

![][30]

<span data-ttu-id="72ae6-194">Pushmeldingen worden gewoonlijk in een back-endservice zoals Mobile Services of ASP.NET verzonden met een compatibele bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="72ae6-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="72ae6-195">U kunt ook Hallo REST-API gebruiken direct toosend worden meldingsberichten als een bibliotheek niet beschikbaar voor uw back-end is.</span><span class="sxs-lookup"><span data-stu-id="72ae6-195">You can also use hello REST API directly toosend notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="72ae6-196">Hier volgt een lijst met andere zelfstudies mogelijk wilt u tooreview voor verzenden van meldingen:</span><span class="sxs-lookup"><span data-stu-id="72ae6-196">Here is a list of some other tutorials that you may want tooreview for sending notifications:</span></span>

* <span data-ttu-id="72ae6-197">ASP.NET: Zie [Notification Hubs gebruiken toopush meldingen toousers].</span><span class="sxs-lookup"><span data-stu-id="72ae6-197">ASP.NET: See [Use Notification Hubs toopush notifications toousers].</span></span>
* <span data-ttu-id="72ae6-198">Azure Notification Hubs Java SDK: Zie [hoe toouse Notification Hubs vanuit Java](notification-hubs-java-push-notification-tutorial.md) voor het verzenden van meldingen vanuit Java.</span><span class="sxs-lookup"><span data-stu-id="72ae6-198">Azure Notification Hubs Java SDK: See [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="72ae6-199">Dit is getest in Eclipse voor Android-ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="72ae6-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="72ae6-200">PHP: Zie [hoe toouse Notification Hubs vanuit PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="72ae6-200">PHP: See [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="72ae6-201">In de volgende subsecties Hallo Hallo zelfstudie verzendt u meldingen met behulp van een .NET-consoletoepassing en met behulp van een mobiele service via een knooppuntscript.</span><span class="sxs-lookup"><span data-stu-id="72ae6-201">In hello next subsections of hello tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="72ae6-202">(Optioneel) Meldingen verzenden met een .NET-app</span><span class="sxs-lookup"><span data-stu-id="72ae6-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="72ae6-203">In deze sectie worden meldingen verzonden met een .NET-console-app.</span><span class="sxs-lookup"><span data-stu-id="72ae6-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="72ae6-204">Maak een nieuwe Visual C#-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="72ae6-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="72ae6-205">Klik in Visual Studio achtereenvolgens op **Extra**, **NuGet Package Manager** en **Package Manager-console**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="72ae6-206">Hiermee geeft Hallo Package Manager-Console in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="72ae6-206">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="72ae6-207">In Hallo venster Package Manager-Console, stelt u Hallo **standaardproject** tooyour nieuwe console toepassingsproject en vervolgens in het consolevenster hello, Hallo volgende opdracht wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="72ae6-207">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="72ae6-208">Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="72ae6-208">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="72ae6-209">Open het bestand Program.cs hello en voeg de volgende Hallo `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="72ae6-209">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="72ae6-210">In uw `Program` klasse, Hallo volgende methode toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="72ae6-210">In your `Program` class, add hello following method.</span></span> <span data-ttu-id="72ae6-211">Bijwerken van Hallo tijdelijke aanduiding voor tekst met uw *DefaultFullSharedAccessSignature* verbindingsreeks en hubnaam verbindingsnaam van Hallo [klassieke Azure-Portal].</span><span class="sxs-lookup"><span data-stu-id="72ae6-211">Update hello placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from hello [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="72ae6-212">Toevoegen van de volgende regels in Hallo uw **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="72ae6-212">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="72ae6-213">Druk op Hallo F5 sleutel toorun Hallo app.</span><span class="sxs-lookup"><span data-stu-id="72ae6-213">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="72ae6-214">U ontvangt een melding in Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="72ae6-214">You should receive a notification in hello app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="72ae6-215">(Optioneel) Meldingen verzenden met een mobiele service</span><span class="sxs-lookup"><span data-stu-id="72ae6-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="72ae6-216">Volg [Aan de slag met Mobile Services].</span><span class="sxs-lookup"><span data-stu-id="72ae6-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="72ae6-217">Meld u aan toohello [klassieke Azure-Portal], en selecteer uw mobiele service.</span><span class="sxs-lookup"><span data-stu-id="72ae6-217">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="72ae6-218">Selecteer Hallo **Scheduler** tabblad Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="72ae6-218">Select hello **Scheduler** tab on hello top.</span></span>
   
      ![][22]
4. <span data-ttu-id="72ae6-219">Maak een nieuwe geplande taak, voeg een naam in en selecteer **Op aanvraag**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="72ae6-220">Wanneer het Hallo-taak is gemaakt, klikt u op Hallo taaknaam.</span><span class="sxs-lookup"><span data-stu-id="72ae6-220">When hello job is created, click hello job name.</span></span> <span data-ttu-id="72ae6-221">Klik vervolgens op Hallo **Script** tabblad op Hallo bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="72ae6-221">Then click hello **Script** tab on hello top bar.</span></span>
6. <span data-ttu-id="72ae6-222">Hallo volgende script in de plannerfunctie invoegen.</span><span class="sxs-lookup"><span data-stu-id="72ae6-222">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="72ae6-223">Zorg ervoor dat tooreplace Hallo tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultFullSharedAccessSignature* die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="72ae6-223">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="72ae6-224">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="72ae6-224">Click **Save**.</span></span>
   
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
7. <span data-ttu-id="72ae6-225">Klik op **eenmaal uitvoeren** op de balk onderaan Hallo.</span><span class="sxs-lookup"><span data-stu-id="72ae6-225">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="72ae6-226">U ontvangt een pop-upmelding.</span><span class="sxs-lookup"><span data-stu-id="72ae6-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72ae6-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72ae6-227">Next steps</span></span>
<span data-ttu-id="72ae6-228">In dit eenvoudige voorbeeld hebt u uitgezonden meldingen tooall uw Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="72ae6-228">In this simple example, you broadcasted notifications tooall your Android devices.</span></span> <span data-ttu-id="72ae6-229">In order tootarget specifieke gebruikers, raadpleegt u de zelfstudie toohello [Notification Hubs gebruiken toopush meldingen toousers].</span><span class="sxs-lookup"><span data-stu-id="72ae6-229">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="72ae6-230">Als u wilt dat toosegment gebruikers op belangengroepen, kunt u lezen [Notification Hubs gebruiken toosend belangrijk nieuws].</span><span class="sxs-lookup"><span data-stu-id="72ae6-230">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="72ae6-231">Meer informatie over het toouse Notification Hubs in [richtlijnen voor Notification Hubs] en in Hallo [Notification Hubs hoe toofor Android].</span><span class="sxs-lookup"><span data-stu-id="72ae6-231">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
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
[Aan de slag met Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[klassieke Azure-Portal]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs hoe toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[Notification Hubs gebruiken toopush meldingen toousers]: /manage/services/notification-hubs/notify-users-aspnet
[Notification Hubs gebruiken toosend belangrijk nieuws]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Google Cloud Messaging-clientonderdeel]: http://components.xamarin.com/view/GCMClient/
[Azure Messaging-onderdeel]: http://components.xamarin.com/view/azure-messaging
