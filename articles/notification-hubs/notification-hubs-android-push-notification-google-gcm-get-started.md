---
title: Pushmeldingen verzenden naar Android met Azure Notification Hubs | Microsoft Docs
description: In deze zelfstudie leert u hoe u met Azure Notification Hubs pushmeldingen verzendt naar Android-apparaten.
services: notification-hubs
documentationcenter: android
keywords: pushmeldingen,pushmelding,android-pushmelding
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 808fc10ef1ebb3288facbdf2e9e817b27d4fc6bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="76284-104">Pushmeldingen naar Android verzenden met Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="76284-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="76284-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="76284-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="76284-106">In dit onderwerp worden pushmeldingen met Google Cloud Messaging (GCM) getoond.</span><span class="sxs-lookup"><span data-stu-id="76284-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="76284-107">Als u gebruikmaakt van Google Firebase Cloud Messaging (FCM), verwijzen wij u naar [Sending push notifications to Android with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md) (Pushmeldingen verzenden naar Android met Azure Notification Hubs en FCM).</span><span class="sxs-lookup"><span data-stu-id="76284-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications to Android with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="76284-108">In deze zelfstudie wordt gedemonstreerd hoe u met Azure Notification Hubs pushmeldingen verzendt naar een Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="76284-108">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an Android application.</span></span>
<span data-ttu-id="76284-109">U maakt een lege Android-app die pushmeldingen ontvangt via Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="76284-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="76284-110">U kunt de voltooide code voor deze zelfstudie [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted) downloaden op GitHub.</span><span class="sxs-lookup"><span data-stu-id="76284-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76284-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="76284-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="76284-112">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="76284-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="76284-113">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="76284-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="76284-114">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="76284-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="76284-115">Naast een actief Azure-account, zoals hierboven vermeld, hebt u voor deze zelfstudie alleen nog de meest recente versie van [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797) nodig.</span><span class="sxs-lookup"><span data-stu-id="76284-115">In addition to an active Azure account mentioned above, this tutorial only requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="76284-116">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Android-apps.</span><span class="sxs-lookup"><span data-stu-id="76284-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="76284-117">Een project maken dat Google Cloud Messaging ondersteunt</span><span class="sxs-lookup"><span data-stu-id="76284-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="76284-118">Een nieuwe Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="76284-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="76284-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="76284-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="76284-120">Selecteer in de blade **Instellingen** **Notification Services** en vervolgens **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="76284-120">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="76284-121">Voer de API-sleutel in en klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="76284-121">Enter the API key and click **Save**.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="76284-123">De Notification Hub is nu geconfigureerd voor GCM en u hebt de verbindingsreeksen om uw app te registreren voor het ontvangen en verzenden van pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="76284-123">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="76284-124"><a id="connecting-app"></a>Uw app verbinden met de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="76284-124"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="76284-125">Een nieuw Android-project maken</span><span class="sxs-lookup"><span data-stu-id="76284-125">Create a new Android project</span></span>
1. <span data-ttu-id="76284-126">Start een nieuw Android Studio-project in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="76284-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio - nieuw project][13]
2. <span data-ttu-id="76284-128">Kies de vormfactor voor **Telefoon en tablet** en de **minimale SDK** die u wilt ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="76284-128">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="76284-129">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="76284-129">Then click **Next**.</span></span>
   
   ![Android Studio - werkstroom voor het maken van een project][14]
3. <span data-ttu-id="76284-131">Kies **Lege activiteit** als belangrijkste activiteit, klik op **Volgende** en klik vervolgens op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="76284-131">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="76284-132">Google Play-services aan het project toevoegen</span><span class="sxs-lookup"><span data-stu-id="76284-132">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="76284-133">Azure Notification Hubs-bibliotheken toevoegen</span><span class="sxs-lookup"><span data-stu-id="76284-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="76284-134">Voeg in het bestand `Build.Gradle` voor de **app** de volgende regels toe in het gedeelte **afhankelijkheden**.</span><span class="sxs-lookup"><span data-stu-id="76284-134">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="76284-135">Voeg de volgende opslagplaats toe na het gedeelte **afhankelijkheden**.</span><span class="sxs-lookup"><span data-stu-id="76284-135">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="76284-136">De AndroidManifest.xml bijwerken</span><span class="sxs-lookup"><span data-stu-id="76284-136">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="76284-137">Als u GCM wilt ondersteunen, moet u een exemplaar-id listenerservice in de code implementeren die wordt gebruikt voor het [verkrijgen van registratietokens](https://developers.google.com/cloud-messaging/android/client#sample-register) met de [API-exemplaar-id van Google](https://developers.google.com/instance-id/).</span><span class="sxs-lookup"><span data-stu-id="76284-137">To support GCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="76284-138">In deze zelfstudie noemen we deze klasse `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="76284-138">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="76284-139">Voeg de volgende servicedefinitie toe aan het bestand AndroidManifest.xml in de `<application>`-tag.</span><span class="sxs-lookup"><span data-stu-id="76284-139">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="76284-140">Vervang de tijdelijke aanduiding `<your package>` door de werkelijke pakketnaam die boven in het bestand `AndroidManifest.xml` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="76284-140">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="76284-141">Nadat we het GCM-registratietoken van de API voor exemplaar-id’s hebben ontvangen, gebruiken we dit voor [registratie bij de Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="76284-141">Once we have received our GCM registration token from the Instance ID API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="76284-142">Deze registratie op de achtergrond wordt ondersteund met een `IntentService` met de naam `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="76284-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="76284-143">Deze service ook is verantwoordelijk voor [het vernieuwen van ons GCM-registratietoken](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="76284-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="76284-144">Voeg de volgende servicedefinitie toe aan het bestand AndroidManifest.xml in de `<application>`-tag.</span><span class="sxs-lookup"><span data-stu-id="76284-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="76284-145">Vervang de tijdelijke aanduiding `<your package>` door de werkelijke pakketnaam die boven in het bestand `AndroidManifest.xml` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="76284-145">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="76284-146">Er wordt ook een ontvanger voor het ontvangen van meldingen gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="76284-146">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="76284-147">Voeg de volgende ontvangerdefinitie toe aan het bestand AndroidManifest.xml in de `<application>`-tag.</span><span class="sxs-lookup"><span data-stu-id="76284-147">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="76284-148">Vervang de tijdelijke aanduiding `<your package>` door de werkelijke pakketnaam die boven in het bestand `AndroidManifest.xml` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="76284-148">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="76284-149">Voeg de volgende vereiste GCM gerelateerde machtigingen toe onder de `</application>`-tag.</span><span class="sxs-lookup"><span data-stu-id="76284-149">Add the following necessary GCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="76284-150">Vervang `<your package>` door de pakketnaam die boven in het bestand `AndroidManifest.xml` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="76284-150">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="76284-151">Zie [Een GCM Client-app instellen voor Android](https://developers.google.com/cloud-messaging/android/client#manifest) voor meer informatie over deze machtigingen.</span><span class="sxs-lookup"><span data-stu-id="76284-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="76284-152">Code toevoegen</span><span class="sxs-lookup"><span data-stu-id="76284-152">Adding code</span></span>
1. <span data-ttu-id="76284-153">Vouw in de Project-weergave **app** > **src** > **main** > **java** uit.</span><span class="sxs-lookup"><span data-stu-id="76284-153">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="76284-154">Klik met de rechtermuisknop op de pakketmap onder **java**, klik op **Nieuw** en klik vervolgens op **Java-klasse**.</span><span class="sxs-lookup"><span data-stu-id="76284-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="76284-155">Voeg een nieuwe klasse met de naam `NotificationSettings` toe.</span><span class="sxs-lookup"><span data-stu-id="76284-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - nieuwe Java-klasse][6]
   
    <span data-ttu-id="76284-157">Zorg ervoor dat u de volgende drie tijdelijke aanduidingen in de volgende code bijwerkt voor de klasse `NotificationSettings`:</span><span class="sxs-lookup"><span data-stu-id="76284-157">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="76284-158">**Verzender-id**: het projectnummer dat u eerder in de [Google Cloud Console](http://cloud.google.com/console) hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="76284-158">**SenderId**: The project number you obtained earlier in the [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="76284-159">**HubListenConnectionString**: de verbindingsreeks **DefaultListenAccessSignature** voor de hub.</span><span class="sxs-lookup"><span data-stu-id="76284-159">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="76284-160">Kopieer deze verbindingsreeks door te klikken op **Toegangsbeleid** in de hubblade **Instellingen** in [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="76284-160">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="76284-161">**HubName**: gebruik de naam van uw Notification Hub die wordt weergegeven in de hubblade in [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="76284-161">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="76284-162">`NotificationSettings`-code:</span><span class="sxs-lookup"><span data-stu-id="76284-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="76284-163">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="76284-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="76284-164">}</span><span class="sxs-lookup"><span data-stu-id="76284-164">}</span></span>
2. <span data-ttu-id="76284-165">Voeg aan de hand van de bovenstaande stappen nog een klasse toe met de naam `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="76284-165">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="76284-166">Dit is de implementatie van onze exemplaar-id listenerservice.</span><span class="sxs-lookup"><span data-stu-id="76284-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="76284-167">De code voor deze klasse roept de `IntentService` aan voor het op de achtergrond [vernieuwen van het GCM-token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="76284-167">The code for this class will call our `IntentService` to [refresh the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="76284-168">Voeg een andere nieuwe klasse toe aan uw project met de naam `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="76284-168">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="76284-169">Dit is de implementatie voor onze `IntentService` die zorgt voor [het vernieuwen van het GCM-token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) en [registratie bij de Notification Hub](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="76284-169">This will be the implementation for our `IntentService` that will handle [refreshing the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="76284-170">Gebruik de volgende code voor deze klasse.</span><span class="sxs-lookup"><span data-stu-id="76284-170">Use the following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
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
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting to register with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete token refresh", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="76284-171">Voeg in uw klasse `MainActivity` de volgende instructies voor `import` toe boven de klassendeclaratie.</span><span class="sxs-lookup"><span data-stu-id="76284-171">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="76284-172">Voeg de volgende privé-leden toe aan de bovenkant van de klasse.</span><span class="sxs-lookup"><span data-stu-id="76284-172">Add the following private members at the top of the class.</span></span> <span data-ttu-id="76284-173">We gebruiken deze [om de beschikbaarheid van Google Play Services te controleren, zoals aanbevolen door Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="76284-173">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="76284-174">Voeg in uw klasse `MainActivity` de volgende methode toe om de beschikbaarheid van Google Play Services te controleren.</span><span class="sxs-lookup"><span data-stu-id="76284-174">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
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
5. <span data-ttu-id="76284-175">Voeg in uw klasse `MainActivity` de volgende code toe waarmee Google Play Services wordt gecontroleerd voordat u uw `IntentService` aanroept om uw GCM-registratietoken op te halen en te registreren met de Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="76284-175">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService to register this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="76284-176">In de methode `OnCreate` van de klasse `MainActivity` voegt u de volgende code toe om het registratieproces te starten wanneer de activiteit wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="76284-176">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="76284-177">Voeg deze extra methoden toe aan de `MainActivity` om de status van de app te controleren en een rapport van de status in uw app op te nemen.</span><span class="sxs-lookup"><span data-stu-id="76284-177">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="76284-178">Voor de methode `ToastNotify` wordt het besturingselement *Hello World* gebruikt `TextView` om de status en kennisgevingen permanent in de app te melden.</span><span class="sxs-lookup"><span data-stu-id="76284-178">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="76284-179">In de indeling activity_main.xml voegt u de volgende id toe voor het besturingselement.</span><span class="sxs-lookup"><span data-stu-id="76284-179">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="76284-180">Nu voegt u een subklasse toe voor de ontvanger die is gedefinieerd in AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="76284-180">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="76284-181">Voeg een andere nieuwe klasse toe aan uw project met de naam `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="76284-181">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="76284-182">Voeg boven in `MyHandler.java` de volgende importinstructie toe:</span><span class="sxs-lookup"><span data-stu-id="76284-182">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="76284-183">Voeg de volgende code toe voor de klasse `MyHandler`, zodat dit een subklasse van `com.microsoft.windowsazure.notifications.NotificationsHandler` wordt.</span><span class="sxs-lookup"><span data-stu-id="76284-183">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="76284-184">Deze code overschrijft de methode `OnReceive`, zodat de handler de ontvangen meldingen rapporteert.</span><span class="sxs-lookup"><span data-stu-id="76284-184">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="76284-185">De handler verzendt ook de pushmelding naar Android Notification Manager met de methode `sendNotification()`.</span><span class="sxs-lookup"><span data-stu-id="76284-185">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="76284-186">De methode `sendNotification()` moet worden uitgevoerd wanneer de app niet actief is en een melding is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="76284-186">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="76284-187">Klik in Android Studio in de menubalk op **Bouwen** > **Project opnieuw opbouwen** om ervoor te zorgen dat uw code geen fouten bevat.</span><span class="sxs-lookup"><span data-stu-id="76284-187">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="76284-188">Pushmeldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="76284-188">Sending push notifications</span></span>
<span data-ttu-id="76284-189">U kunt testen of u pushmeldingen in uw app ontvangt door deze meldingen via [Azure Portal] te verzenden. Ga naar het gedeelte **Probleemoplossing** in de hubblade, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="76284-189">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Azure Notification Hubs - Verzenden testen](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="76284-191">(Optioneel) Pushmeldingen rechtstreeks vanuit de app verzenden</span><span class="sxs-lookup"><span data-stu-id="76284-191">(Optional) Send push notifications directly from the app</span></span>
<span data-ttu-id="76284-192">Normaal gesproken verzendt u meldingen via een back-endserver.</span><span class="sxs-lookup"><span data-stu-id="76284-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="76284-193">Mogelijk wilt u pushmeldingen direct vanuit de clienttoepassing kunnen verzenden.</span><span class="sxs-lookup"><span data-stu-id="76284-193">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="76284-194">In dit gedeelte wordt uitgelegd hoe u meldingen vanuit de client verzendt met de [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="76284-194">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="76284-195">Vouw in de Project-weergave van Android Studio-Project **App** > **src** > **main** > **res** > **layout** uit.</span><span class="sxs-lookup"><span data-stu-id="76284-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="76284-196">Open het indelingsbestand `activity_main.xml` en klik op het tabblad **Tekst** om de tekst van het bestand bij te werken.</span><span class="sxs-lookup"><span data-stu-id="76284-196">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="76284-197">Werk de tekst bij met de onderstaande code, waarmee u nieuwe besturingselementen `Button` en `EditText` voor het verzenden van pushmeldingen toevoegt aan de Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="76284-197">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="76284-198">Voeg deze code onderin toe, net voor `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="76284-198">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="76284-199">Vouw in de Project-weergave van Android Studio-Project **App** > **src** > **main** > **res** > **values** uit.</span><span class="sxs-lookup"><span data-stu-id="76284-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="76284-200">Open het bestand `strings.xml` en voeg de tekenreekswaarden toe waarnaar wordt verwezen door de nieuwe besturingselementen `Button` en `EditText`.</span><span class="sxs-lookup"><span data-stu-id="76284-200">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="76284-201">Voeg deze onder in het bestand toe, net voor `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="76284-201">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="76284-202">Voeg in het bestand `NotificationSetting.java` de volgende instelling toe voor de klasse `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="76284-202">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="76284-203">Werk `HubFullAccess` bij met de verbindingsreeks **DefaultFullSharedAccessSignature** voor uw hub.</span><span class="sxs-lookup"><span data-stu-id="76284-203">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="76284-204">U kunt deze verbindingsreeks kopiëren vanuit [Azure Portal] door te klikken op **Toegangsbeleid** op de blade **Instellingen** voor uw Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="76284-204">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="76284-205">Voeg in uw bestand `MainActivity.java` de volgende instructies voor `import` toe boven de klasse `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="76284-205">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="76284-206">Voeg in uw bestand `MainActivity.java` de volgende leden toe boven de klasse `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="76284-206">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="76284-207">U moet een Software Access Signature (SaS)-token maken om een POST-aanvraag te verifiëren om berichten naar uw Notification Hub te kunnen verzenden.</span><span class="sxs-lookup"><span data-stu-id="76284-207">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="76284-208">U doet dit door de belangrijkste gegevens uit de verbindingsreeks te parseren en vervolgens het SaS-token te maken, zoals vermeld in [Algemene concepten](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="76284-208">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="76284-209">De volgende code is een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="76284-209">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="76284-210">Voeg in `MainActivity.java` de volgende methode toe aan de klasse `MainActivity` om uw verbindingsreeks te parseren.</span><span class="sxs-lookup"><span data-stu-id="76284-210">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
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
7. <span data-ttu-id="76284-211">Voeg in `MainActivity.java` de volgende methode toe aan de klasse `MainActivity` om een SAS-verificatietoken te maken.</span><span class="sxs-lookup"><span data-stu-id="76284-211">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
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
8. <span data-ttu-id="76284-212">Voeg in `MainActivity.java` de volgende methode toe aan de klasse `MainActivity` om het klikken op de knop **Melding verzenden** te activeren en de pushmelding naar de hub te verzenden met de ingebouwde REST-API.</span><span class="sxs-lookup"><span data-stu-id="76284-212">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
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

## <a name="testing-your-app"></a><span data-ttu-id="76284-213">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="76284-213">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="76284-214">Pushmeldingen in de emulator</span><span class="sxs-lookup"><span data-stu-id="76284-214">Push notifications in the emulator</span></span>
<span data-ttu-id="76284-215">Als u pushmeldingen binnen een emulator wilt testen, moet u ervoor zorgen dat de installatiekopie van de emulator het Google API-niveau ondersteunt dat u voor uw app hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="76284-215">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="76284-216">Als uw installatiekopie geen ondersteuning biedt voor native Google API’s, verschijnt de uitzondering **SERVICE\_NIET\_BESCHIKBAAR**.</span><span class="sxs-lookup"><span data-stu-id="76284-216">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="76284-217">Bovendien moet u ervoor zorgen dat u uw Google-account hebt toegevoegd aan uw actieve emulator onder **Instellingen** > **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="76284-217">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="76284-218">Anders kunnen pogingen om opnieuw te registreren bij GCM leiden tot de uitzondering **VERIFICATIE\_MISLUKT**.</span><span class="sxs-lookup"><span data-stu-id="76284-218">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="76284-219">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="76284-219">Running the application</span></span>
1. <span data-ttu-id="76284-220">Start de app. U zult zien dat de registratie-id meldt dat de registratie is gelukt.</span><span class="sxs-lookup"><span data-stu-id="76284-220">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
      ![Testen op Android - Kanaalregistratie][18]
2. <span data-ttu-id="76284-222">Voer een melding in die moet worden verzonden naar alle Android-apparaten die zijn geregistreerd bij de hub.</span><span class="sxs-lookup"><span data-stu-id="76284-222">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
      ![Testen op Android - een bericht verzenden][19]

3. <span data-ttu-id="76284-224">Druk op **Melding verzenden**.</span><span class="sxs-lookup"><span data-stu-id="76284-224">Press **Send Notification**.</span></span> <span data-ttu-id="76284-225">Alle apparaten waarop de app actief is, ontvangen een `AlertDialog`-exemplaar met de pushmelding.</span><span class="sxs-lookup"><span data-stu-id="76284-225">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="76284-226">Apparaten waarop de app niet actief is, maar die eerder zijn geregistreerd voor pushmeldingen, ontvangen een melding in Android Notification Manager.</span><span class="sxs-lookup"><span data-stu-id="76284-226">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="76284-227">Deze meldingen kunnen worden bekeken door omlaag te vegen vanuit de linkerbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="76284-227">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
      ![Testen op Android - meldingen][21]

## <a name="next-steps"></a><span data-ttu-id="76284-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76284-229">Next steps</span></span>
<span data-ttu-id="76284-230">U kunt het beste de zelfstudie [Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden] doornemen.</span><span class="sxs-lookup"><span data-stu-id="76284-230">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="76284-231">Hierin ziet u hoe u meldingen van een ASP.NET-back-end verzendt met tags voor specifieke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="76284-231">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="76284-232">Zie [Notification Hubs gebruiken om belangrijk nieuws te verzenden] als u gebruikers wilt indelen op belangengroep.</span><span class="sxs-lookup"><span data-stu-id="76284-232">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="76284-233">Zie [Richtlijnen voor Notification Hubs] voor meer algemene informatie over Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="76284-233">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="76284-234">[Richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="76284-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="76284-235">[Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="76284-235">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="76284-236">[Notification Hubs gebruiken om belangrijk nieuws te verzenden]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="76284-236">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="76284-237">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="76284-237">[Azure Portal]: https://portal.azure.com</span></span>
