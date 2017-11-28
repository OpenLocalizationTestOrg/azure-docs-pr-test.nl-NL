---
title: Pushmeldingen verzenden naar Android met Azure Notification Hubs en Firebase Cloud Messaging | Microsoft Docs
description: In deze zelfstudie leert u hoe u met Azure Notification Hubs en Firebase Cloud Messaging pushmeldingen verzendt naar Android-apparaten.
services: notification-hubs
documentationcenter: android
keywords: pushmeldingen,pushmelding,android-pushmelding, firebase cloud messaging
author: ysxu
manager: erikre
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: 45a3fa5c7190e039fd637c78a41eeb3f6ede9bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="cba59-104">Pushmeldingen naar Android verzenden met Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="cba59-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="cba59-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="cba59-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cba59-106">In dit onderwerp worden pushmeldingen met Google Firebase Cloud Messaging (FCM) getoond.</span><span class="sxs-lookup"><span data-stu-id="cba59-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="cba59-107">Als u gebruikmaakt van Google Cloud Messaging (GCM), verwijzen wij u naar [Sending push notifications to Android with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md) (Pushmeldingen verzenden naar Android met Azure Notification Hubs en GCM).</span><span class="sxs-lookup"><span data-stu-id="cba59-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications to Android with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="cba59-108">In deze zelfstudie wordt gedemonstreerd hoe u met Azure Notification Hubs Firebase Cloud Messaging en pushmeldingen verzendt naar een Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cba59-108">This tutorial shows you how to use Azure Notification Hubs and Firebase Cloud Messaging to send push notifications to an Android application.</span></span>
<span data-ttu-id="cba59-109">U maakt een lege Android-app die pushmeldingen ontvangt via Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="cba59-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="cba59-110">U kunt de voltooide code voor deze zelfstudie [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase) downloaden op GitHub.</span><span class="sxs-lookup"><span data-stu-id="cba59-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cba59-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cba59-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cba59-112">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="cba59-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="cba59-113">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="cba59-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cba59-114">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cba59-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="cba59-115">Naast een actief Azure-account, zoals hierboven vermeld, hebt u voor deze zelfstudie nog de meest recente versie van [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797) nodig.</span><span class="sxs-lookup"><span data-stu-id="cba59-115">In addition to an active Azure account mentioned above, this tutorial requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="cba59-116">Android 2.3 of hoger voor Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="cba59-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="cba59-117">Google Repository revisie 27 of hoger is vereist voor Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="cba59-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="cba59-118">Google Play-Services 9.0.2 of hoger voor Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="cba59-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="cba59-119">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Android-apps.</span><span class="sxs-lookup"><span data-stu-id="cba59-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="cba59-120">Een nieuw Android Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="cba59-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="cba59-121">Start een nieuw Android Studio-project in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="cba59-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="cba59-122">Kies de vormfactor voor **Telefoon en tablet** en de **minimale SDK** die u wilt ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="cba59-122">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="cba59-123">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cba59-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="cba59-124">Kies **Lege activiteit** als belangrijkste activiteit, klik op **Volgende** en klik vervolgens op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="cba59-124">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="cba59-125">Een project maken dat Firebase Cloud Messaging ondersteunt</span><span class="sxs-lookup"><span data-stu-id="cba59-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="cba59-126">Een nieuwe Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="cba59-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="cba59-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="cba59-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="cba59-128">Selecteer in de blade **Instellingen** van uw Notification Hub **Notification Services** en vervolgens **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="cba59-128">In the **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="cba59-129">Voer de FCM-serversleutel die u eerder hebt gekopieerd uit de [Firebase console](https://firebase.google.com/console/) in en klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cba59-129">Enter the FCM server key you copied earlier from the [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="cba59-131">De Notification Hub is nu geconfigureerd voor Firebase Cloud Messaging en u hebt de verbindingsreeksen om uw app te registreren voor het ontvangen en verzenden van pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="cba59-131">Your notification hub is now configured to work with Firebase Cloud Messagin, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="cba59-132"><a id="connecting-app"></a>Uw app verbinden met de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="cba59-132"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="cba59-133">Google Play-services aan het project toevoegen</span><span class="sxs-lookup"><span data-stu-id="cba59-133">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="cba59-134">Azure Notification Hubs-bibliotheken toevoegen</span><span class="sxs-lookup"><span data-stu-id="cba59-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="cba59-135">Voeg in het bestand `Build.Gradle` voor de **app** de volgende regels toe in het gedeelte **afhankelijkheden**.</span><span class="sxs-lookup"><span data-stu-id="cba59-135">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="cba59-136">Voeg de volgende opslagplaats toe na het gedeelte **afhankelijkheden**.</span><span class="sxs-lookup"><span data-stu-id="cba59-136">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="cba59-137">De AndroidManifest.xml bijwerken</span><span class="sxs-lookup"><span data-stu-id="cba59-137">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="cba59-138">Als u FCM wilt ondersteunen, moet u een exemplaar-id listenerservice in de code implementeren die wordt gebruikt voor het [verkrijgen van registratietokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) met de [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span><span class="sxs-lookup"><span data-stu-id="cba59-138">To support FCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="cba59-139">In deze zelfstudie noemen we deze klasse `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="cba59-139">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="cba59-140">Voeg de volgende servicedefinitie toe aan het bestand AndroidManifest.xml in de `<application>`-tag.</span><span class="sxs-lookup"><span data-stu-id="cba59-140">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="cba59-141">Nadat we het FCM-registratietoken van de FirebaseInstanceId API hebben ontvangen, gebruiken we dit voor [registratie bij de Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="cba59-141">Once we have received our FCM registration token from the FirebaseInstanceId API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="cba59-142">Deze registratie op de achtergrond wordt ondersteund met een `IntentService` met de naam `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="cba59-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="cba59-143">Deze service ook is verantwoordelijk voor het vernieuwen van ons FCM-registratietoken.</span><span class="sxs-lookup"><span data-stu-id="cba59-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="cba59-144">Voeg de volgende servicedefinitie toe aan het bestand AndroidManifest.xml in de `<application>`-tag.</span><span class="sxs-lookup"><span data-stu-id="cba59-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="cba59-145">Er wordt ook een ontvanger voor het ontvangen van meldingen gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="cba59-145">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="cba59-146">Voeg de volgende ontvangerdefinitie toe aan het bestand AndroidManifest.xml in de `<application>`-tag.</span><span class="sxs-lookup"><span data-stu-id="cba59-146">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="cba59-147">Vervang de tijdelijke aanduiding `<your package>` door de werkelijke pakketnaam die boven in het bestand `AndroidManifest.xml` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cba59-147">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="cba59-148">Voeg de volgende vereiste FCM gerelateerde machtigingen toe onder de `</application>`-tag.</span><span class="sxs-lookup"><span data-stu-id="cba59-148">Add the following necessary FCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="cba59-149">Vervang `<your package>` door de pakketnaam die boven in het bestand `AndroidManifest.xml` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cba59-149">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="cba59-150">Zie voor meer informatie over deze machtigingen [Een GCM Client App instellen voor Android](https://developers.google.com/cloud-messaging/android/client#manifest) en [Een GCM Client App voor Android migreren naar Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span><span class="sxs-lookup"><span data-stu-id="cba59-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android to Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="cba59-151">Code toevoegen</span><span class="sxs-lookup"><span data-stu-id="cba59-151">Adding code</span></span>
1. <span data-ttu-id="cba59-152">Vouw in de Project-weergave **app** > **src** > **main** > **java** uit.</span><span class="sxs-lookup"><span data-stu-id="cba59-152">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="cba59-153">Klik met de rechtermuisknop op de pakketmap onder **java**, klik op **Nieuw** en klik vervolgens op **Java-klasse**.</span><span class="sxs-lookup"><span data-stu-id="cba59-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="cba59-154">Voeg een nieuwe klasse met de naam `NotificationSettings` toe.</span><span class="sxs-lookup"><span data-stu-id="cba59-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - nieuwe Java-klasse](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="cba59-156">Zorg ervoor dat u de volgende drie tijdelijke aanduidingen in de volgende code bijwerkt voor de klasse `NotificationSettings`:</span><span class="sxs-lookup"><span data-stu-id="cba59-156">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="cba59-157">**SenderId**: De Verzenders-ID die u eerder hebt verkregen in het tabblad **Cloud Messaging** tab van uw projectinstellingen in de [Firebase console](https://firebase.google.com/console/).</span><span class="sxs-lookup"><span data-stu-id="cba59-157">**SenderId**: The Sender Id you obtained earlier in the **Cloud Messaging** tab of your project settings in the [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="cba59-158">**HubListenConnectionString**: de verbindingsreeks **DefaultListenAccessSignature** voor de hub.</span><span class="sxs-lookup"><span data-stu-id="cba59-158">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="cba59-159">Kopieer deze verbindingsreeks door te klikken op **Toegangsbeleid** in de hubblade **Instellingen** in [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="cba59-159">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="cba59-160">**HubName**: gebruik de naam van uw Notification Hub die wordt weergegeven in de hubblade in [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="cba59-160">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="cba59-161">`NotificationSettings`-code:</span><span class="sxs-lookup"><span data-stu-id="cba59-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="cba59-162">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="cba59-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="cba59-163">}</span><span class="sxs-lookup"><span data-stu-id="cba59-163">}</span></span>
2. <span data-ttu-id="cba59-164">Voeg aan de hand van de bovenstaande stappen nog een klasse toe met de naam `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="cba59-164">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="cba59-165">Dit is de implementatie van onze exemplaar-id listenerservice.</span><span class="sxs-lookup"><span data-stu-id="cba59-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="cba59-166">De code voor deze klasse roept de `IntentService` aan voor het op de achtergrond [vernieuwen van het FCM-token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="cba59-166">The code for this class will call our `IntentService` to [refresh the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="cba59-167">Voeg een andere nieuwe klasse toe aan uw project met de naam `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="cba59-167">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="cba59-168">Dit is de implementatie voor onze `IntentService` die zorgt voor [het vernieuwen van het FCM-token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) en [registratie bij de Notification Hub](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="cba59-168">This will be the implementation for our `IntentService` that will handle [refreshing the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="cba59-169">Gebruik de volgende code voor deze klasse.</span><span class="sxs-lookup"><span data-stu-id="cba59-169">Use the following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {
   
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if the token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete registration", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="cba59-170">Voeg in uw klasse `MainActivity` de volgende instructies voor `import` toe boven de klassendeclaratie.</span><span class="sxs-lookup"><span data-stu-id="cba59-170">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="cba59-171">Voeg de volgende privé-leden toe aan de bovenkant van de klasse.</span><span class="sxs-lookup"><span data-stu-id="cba59-171">Add the following private members at the top of the class.</span></span> <span data-ttu-id="cba59-172">We gebruiken deze [om de beschikbaarheid van Google Play Services te controleren, zoals aanbevolen door Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="cba59-172">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="cba59-173">Voeg in uw klasse `MainActivity` de volgende methode toe om de beschikbaarheid van Google Play Services te controleren.</span><span class="sxs-lookup"><span data-stu-id="cba59-173">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
        /**
         * Check the device to make sure it has the Google Play Services APK. If
         * it doesn't, display a dialog that allows users to download the APK from
         * the Google Play Store or enable it in the device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. <span data-ttu-id="cba59-174">Voeg in uw klasse `MainActivity` de volgende code toe waarmee Google Play Services wordt gecontroleerd voordat u uw `IntentService` aanroept om uw FCM-registratietoken op te halen en te registreren met de Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="cba59-174">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService to register this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="cba59-175">In de methode `OnCreate` van de klasse `MainActivity` voegt u de volgende code toe om het registratieproces te starten wanneer de activiteit wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cba59-175">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="cba59-176">Voeg deze extra methoden toe aan de `MainActivity` om de status van de app te controleren en een rapport van de status in uw app op te nemen.</span><span class="sxs-lookup"><span data-stu-id="cba59-176">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. <span data-ttu-id="cba59-177">Voor de methode `ToastNotify` wordt het besturingselement *Hello World* gebruikt `TextView` om de status en kennisgevingen permanent in de app te melden.</span><span class="sxs-lookup"><span data-stu-id="cba59-177">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="cba59-178">In de indeling activity_main.xml voegt u de volgende id toe voor het besturingselement.</span><span class="sxs-lookup"><span data-stu-id="cba59-178">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="cba59-179">Nu voegt u een subklasse toe voor de ontvanger die is gedefinieerd in AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="cba59-179">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="cba59-180">Voeg een andere nieuwe klasse toe aan uw project met de naam `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="cba59-180">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="cba59-181">Voeg boven in `MyHandler.java` de volgende importinstructie toe:</span><span class="sxs-lookup"><span data-stu-id="cba59-181">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="cba59-182">Voeg de volgende code toe voor de klasse `MyHandler`, zodat dit een subklasse van `com.microsoft.windowsazure.notifications.NotificationsHandler` wordt.</span><span class="sxs-lookup"><span data-stu-id="cba59-182">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="cba59-183">Deze code overschrijft de methode `OnReceive`, zodat de handler de ontvangen meldingen rapporteert.</span><span class="sxs-lookup"><span data-stu-id="cba59-183">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="cba59-184">De handler verzendt ook de pushmelding naar Android Notification Manager met de methode `sendNotification()`.</span><span class="sxs-lookup"><span data-stu-id="cba59-184">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="cba59-185">De methode `sendNotification()` moet worden uitgevoerd wanneer de app niet actief is en een melding is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="cba59-185">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. <span data-ttu-id="cba59-186">Klik in Android Studio in de menubalk op **Bouwen** > **Project opnieuw opbouwen** om ervoor te zorgen dat uw code geen fouten bevat.</span><span class="sxs-lookup"><span data-stu-id="cba59-186">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="cba59-187">Voer de app op uw apparaat en controleer of dat deze correct is geregistreerd in de notification hub.</span><span class="sxs-lookup"><span data-stu-id="cba59-187">Run the app on your device and verify it registers successfully with the notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="cba59-188">Registratie kan mislukken bij de eerste introductie tot de `onTokenRefresh()` methode van exemplaar-id-service wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cba59-188">Registration may fail on the initial launch until the `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="cba59-189">De vernieuwing moet een succesvolle registratie met de notification hub tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="cba59-189">The refresh should intiate a successful registration with the notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="cba59-190">Pushmeldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="cba59-190">Sending push notifications</span></span>
<span data-ttu-id="cba59-191">U kunt testen of u pushmeldingen in uw app ontvangt door deze meldingen via [Azure Portal] te verzenden. Ga naar het gedeelte **Probleemoplossing** in de hubblade, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cba59-191">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Azure Notification Hubs - Verzenden testen](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="cba59-193">(Optioneel) Pushmeldingen rechtstreeks vanuit de app verzenden</span><span class="sxs-lookup"><span data-stu-id="cba59-193">(Optional) Send push notifications directly from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cba59-194">Dit voorbeeld van het verzenden van meldingen vanuit de client-app wordt uitsluitend voor educatieve doeleinden aangeboden.</span><span class="sxs-lookup"><span data-stu-id="cba59-194">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="cba59-195">Aangezien het hiervoor noodzakelijk is dat de `DefaultFullSharedAccessSignature` aanwezig is op de client-app, loopt uw Notification Hub het risico dat een gebruiker toegang kan krijgen en onbevoegd meldingen naar uw clients kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="cba59-195">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="cba59-196">Normaal gesproken verzendt u meldingen via een back-endserver.</span><span class="sxs-lookup"><span data-stu-id="cba59-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="cba59-197">Mogelijk wilt u pushmeldingen direct vanuit de clienttoepassing kunnen verzenden.</span><span class="sxs-lookup"><span data-stu-id="cba59-197">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="cba59-198">In dit gedeelte wordt uitgelegd hoe u meldingen vanuit de client verzendt met de [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="cba59-198">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="cba59-199">Vouw in de Project-weergave van Android Studio-Project **App** > **src** > **main** > **res** > **layout** uit.</span><span class="sxs-lookup"><span data-stu-id="cba59-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="cba59-200">Open het indelingsbestand `activity_main.xml` en klik op het tabblad **Tekst** om de tekst van het bestand bij te werken.</span><span class="sxs-lookup"><span data-stu-id="cba59-200">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="cba59-201">Werk de tekst bij met de onderstaande code, waarmee u nieuwe besturingselementen `Button` en `EditText` voor het verzenden van pushmeldingen toevoegt aan de Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="cba59-201">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="cba59-202">Voeg deze code onderin toe, net voor `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="cba59-202">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. <span data-ttu-id="cba59-203">Vouw in de Project-weergave van Android Studio-Project **App** > **src** > **main** > **res** > **values** uit.</span><span class="sxs-lookup"><span data-stu-id="cba59-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="cba59-204">Open het bestand `strings.xml` en voeg de tekenreekswaarden toe waarnaar wordt verwezen door de nieuwe besturingselementen `Button` en `EditText`.</span><span class="sxs-lookup"><span data-stu-id="cba59-204">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="cba59-205">Voeg deze onder in het bestand toe, net voor `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="cba59-205">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="cba59-206">Voeg in het bestand `NotificationSetting.java` de volgende instelling toe voor de klasse `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="cba59-206">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="cba59-207">Werk `HubFullAccess` bij met de verbindingsreeks **DefaultFullSharedAccessSignature** voor uw hub.</span><span class="sxs-lookup"><span data-stu-id="cba59-207">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="cba59-208">U kunt deze verbindingsreeks kopiëren vanuit [Azure Portal] door te klikken op **Toegangsbeleid** op de blade **Instellingen** voor uw Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="cba59-208">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="cba59-209">Voeg in uw bestand `MainActivity.java` de volgende instructies voor `import` toe boven de klasse `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="cba59-209">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. <span data-ttu-id="cba59-210">Voeg in uw bestand `MainActivity.java` de volgende leden toe boven de klasse `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="cba59-210">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="cba59-211">U moet een Software Access Signature (SaS)-token maken om een POST-aanvraag te verifiëren om berichten naar uw Notification Hub te kunnen verzenden.</span><span class="sxs-lookup"><span data-stu-id="cba59-211">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="cba59-212">U doet dit door de belangrijkste gegevens uit de verbindingsreeks te parseren en vervolgens het SaS-token te maken, zoals vermeld in [Algemene concepten](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="cba59-212">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="cba59-213">De volgende code is een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="cba59-213">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="cba59-214">Voeg in `MainActivity.java` de volgende methode toe aan de klasse `MainActivity` om uw verbindingsreeks te parseren.</span><span class="sxs-lookup"><span data-stu-id="cba59-214">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. <span data-ttu-id="cba59-215">Voeg in `MainActivity.java` de volgende methode toe aan de klasse `MainActivity` om een SAS-verificatietoken te maken.</span><span class="sxs-lookup"><span data-stu-id="cba59-215">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. <span data-ttu-id="cba59-216">Voeg in `MainActivity.java` de volgende methode toe aan de klasse `MainActivity` om het klikken op de knop **Melding verzenden** te activeren en de pushmelding naar de hub te verzenden met de ingebouwde REST-API.</span><span class="sxs-lookup"><span data-stu-id="cba59-216">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a><span data-ttu-id="cba59-217">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="cba59-217">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="cba59-218">Pushmeldingen in de emulator</span><span class="sxs-lookup"><span data-stu-id="cba59-218">Push notifications in the emulator</span></span>
<span data-ttu-id="cba59-219">Als u pushmeldingen binnen een emulator wilt testen, moet u ervoor zorgen dat de installatiekopie van de emulator het Google API-niveau ondersteunt dat u voor uw app hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="cba59-219">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="cba59-220">Als uw installatiekopie geen ondersteuning biedt voor native Google API’s, verschijnt de uitzondering **SERVICE\_NIET\_BESCHIKBAAR**.</span><span class="sxs-lookup"><span data-stu-id="cba59-220">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="cba59-221">Bovendien moet u ervoor zorgen dat u uw Google-account hebt toegevoegd aan uw actieve emulator onder **Instellingen** > **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="cba59-221">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="cba59-222">Anders kunnen pogingen om opnieuw te registreren bij GCM leiden tot de uitzondering **VERIFICATIE\_MISLUKT**.</span><span class="sxs-lookup"><span data-stu-id="cba59-222">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="cba59-223">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cba59-223">Running the application</span></span>
1. <span data-ttu-id="cba59-224">Start de app. U zult zien dat de registratie-id meldt dat de registratie is gelukt.</span><span class="sxs-lookup"><span data-stu-id="cba59-224">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="cba59-225">Voer een melding in die moet worden verzonden naar alle Android-apparaten die zijn geregistreerd bij de hub.</span><span class="sxs-lookup"><span data-stu-id="cba59-225">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="cba59-226">Druk op **Melding verzenden**.</span><span class="sxs-lookup"><span data-stu-id="cba59-226">Press **Send Notification**.</span></span> <span data-ttu-id="cba59-227">Alle apparaten waarop de app actief is, ontvangen een `AlertDialog`-exemplaar met de pushmelding.</span><span class="sxs-lookup"><span data-stu-id="cba59-227">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="cba59-228">Apparaten waarop de app niet actief is, maar die eerder zijn geregistreerd voor pushmeldingen, ontvangen een melding in Android Notification Manager.</span><span class="sxs-lookup"><span data-stu-id="cba59-228">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="cba59-229">Deze meldingen kunnen worden bekeken door omlaag te vegen vanuit de linkerbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="cba59-229">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="cba59-230">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cba59-230">Next steps</span></span>
<span data-ttu-id="cba59-231">U kunt het beste de zelfstudie [Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden] doornemen.</span><span class="sxs-lookup"><span data-stu-id="cba59-231">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="cba59-232">Hierin ziet u hoe u meldingen van een ASP.NET-back-end verzendt met tags voor specifieke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="cba59-232">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="cba59-233">Zie [Notification Hubs gebruiken om belangrijk nieuws te verzenden] als u gebruikers wilt indelen op belangengroep.</span><span class="sxs-lookup"><span data-stu-id="cba59-233">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="cba59-234">Zie [Richtlijnen voor Notification Hubs] voor meer algemene informatie over Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="cba59-234">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="cba59-235">[Richtlijnen voor Notification Hubs]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="cba59-235">[Notification Hubs Guidance]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="cba59-236">[Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="cba59-236">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="cba59-237">[Notification Hubs gebruiken om belangrijk nieuws te verzenden]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="cba59-237">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="cba59-238">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cba59-238">[Azure Portal]: https://portal.azure.com</span></span>
