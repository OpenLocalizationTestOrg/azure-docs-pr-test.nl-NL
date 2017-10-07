---
title: aaaSending push notifications tooAndroid met Azure Notification Hubs | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toopush meldingen tooAndroid apparaten.
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
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="f75b4-104">Push notifications tooAndroid met Azure Notification Hubs verzenden</span><span class="sxs-lookup"><span data-stu-id="f75b4-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="f75b4-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f75b4-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f75b4-106">In dit onderwerp worden pushmeldingen met Google Cloud Messaging (GCM) getoond.</span><span class="sxs-lookup"><span data-stu-id="f75b4-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="f75b4-107">Als u gebruikmaakt van Google Firebase Cloud Messaging (FCM), raadpleegt u [verzenden push notifications tooAndroid met Azure Notification Hubs en FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f75b4-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="f75b4-108">Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooan Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f75b4-108">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="f75b4-109">U maakt een lege Android-app die pushmeldingen ontvangt via Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="f75b4-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="f75b4-110">code voor deze zelfstudie Hallo voltooid kan worden gedownload van GitHub [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="f75b4-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f75b4-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f75b4-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f75b4-112">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="f75b4-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="f75b4-113">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="f75b4-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f75b4-114">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f75b4-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="f75b4-115">Bovendien tooan actief Azure-account hierboven vermeld in deze zelfstudie vereist alleen de meest recente versie van Hallo [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="f75b4-115">In addition tooan active Azure account mentioned above, this tutorial only requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="f75b4-116">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Android-apps.</span><span class="sxs-lookup"><span data-stu-id="f75b4-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="f75b4-117">Een project maken dat Google Cloud Messaging ondersteunt</span><span class="sxs-lookup"><span data-stu-id="f75b4-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="f75b4-118">Een nieuwe Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="f75b4-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="f75b4-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="f75b4-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="f75b4-120">In Hallo **instellingen** blade Selecteer **Notification Services** en vervolgens **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="f75b4-120">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="f75b4-121">Voer Hallo API-sleutel in en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f75b4-121">Enter hello API key and click **Save**.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="f75b4-123">Uw notification hub is nu geconfigureerd toowork bij GCM en u hebt Hallo verbinding tekenreeksen tooboth de tooreceive van uw app registreren en pushmeldingen te verzenden.</span><span class="sxs-lookup"><span data-stu-id="f75b4-123">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="f75b4-124"><a id="connecting-app"></a>Verbinding maken met uw app toohello notification hub</span><span class="sxs-lookup"><span data-stu-id="f75b4-124"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="f75b4-125">Een nieuw Android-project maken</span><span class="sxs-lookup"><span data-stu-id="f75b4-125">Create a new Android project</span></span>
1. <span data-ttu-id="f75b4-126">Start een nieuw Android Studio-project in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="f75b4-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio - nieuw project][13]
2. <span data-ttu-id="f75b4-128">Kies Hallo **telefoon en Tablet** factor en Hallo **minimale SDK** dat u wilt dat toosupport.</span><span class="sxs-lookup"><span data-stu-id="f75b4-128">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="f75b4-129">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f75b4-129">Then click **Next**.</span></span>
   
   ![Android Studio - werkstroom voor het maken van een project][14]
3. <span data-ttu-id="f75b4-131">Kies **lege activiteit** Hallo belangrijkste activiteit, klikt u op **volgende**, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f75b4-131">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="f75b4-132">Google Play services toohello project toevoegen</span><span class="sxs-lookup"><span data-stu-id="f75b4-132">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="f75b4-133">Azure Notification Hubs-bibliotheken toevoegen</span><span class="sxs-lookup"><span data-stu-id="f75b4-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="f75b4-134">In Hallo `Build.Gradle` -bestand voor Hallo **app**, toevoegen van de volgende regels in Hallo Hallo **afhankelijkheden** sectie.</span><span class="sxs-lookup"><span data-stu-id="f75b4-134">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="f75b4-135">Toevoegen van de volgende opslagplaats na Hallo Hallo **afhankelijkheden** sectie.</span><span class="sxs-lookup"><span data-stu-id="f75b4-135">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="f75b4-136">Hallo AndroidManifest.xml bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f75b4-136">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="f75b4-137">toosupport GCM, moet er een exemplaar-ID listenerservice implementeren in de code die wordt gebruikt te[verkrijgen van registratietokens](https://developers.google.com/cloud-messaging/android/client#sample-register) met [van Google API voor exemplaar-ID](https://developers.google.com/instance-id/).</span><span class="sxs-lookup"><span data-stu-id="f75b4-137">toosupport GCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="f75b4-138">In deze zelfstudie noemen we Hallo klasse `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="f75b4-138">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="f75b4-139">Hallo na toohello AndroidManifest.xml servicedefinitiebestand binnen Hallo toevoegen `<application>` label.</span><span class="sxs-lookup"><span data-stu-id="f75b4-139">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="f75b4-140">Vervang Hallo `<your package>` aanduiding voor items met de werkelijke pakketnaam die wordt weergegeven boven Hallo HALLO hallo `AndroidManifest.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="f75b4-140">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="f75b4-141">Wanneer we ons GCM-registratietoken van Hallo API exemplaar-ID hebt ontvangen, dit wordt gebruikt te[registreren bij Azure Notification Hub Hallo](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="f75b4-141">Once we have received our GCM registration token from hello Instance ID API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="f75b4-142">Deze registratie wordt ondersteund in Hallo achtergrond met behulp van een `IntentService` met de naam `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="f75b4-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="f75b4-143">Deze service ook is verantwoordelijk voor [het vernieuwen van ons GCM-registratietoken](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="f75b4-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="f75b4-144">Hallo na toohello AndroidManifest.xml servicedefinitiebestand binnen Hallo toevoegen `<application>` label.</span><span class="sxs-lookup"><span data-stu-id="f75b4-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="f75b4-145">Vervang Hallo `<your package>` aanduiding voor items met de werkelijke pakketnaam die wordt weergegeven boven Hallo HALLO hallo `AndroidManifest.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="f75b4-145">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="f75b4-146">Definieert een ontvanger tooreceive meldingen.</span><span class="sxs-lookup"><span data-stu-id="f75b4-146">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="f75b4-147">Hallo volgende ontvanger definitie toohello bestand AndroidManifest.xml in Hallo toevoegen `<application>` label.</span><span class="sxs-lookup"><span data-stu-id="f75b4-147">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="f75b4-148">Vervang Hallo `<your package>` aanduiding voor items met de werkelijke pakketnaam die wordt weergegeven boven Hallo HALLO hallo `AndroidManifest.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="f75b4-148">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="f75b4-149">Voeg Hallo volgende vereiste GCM gerelateerde machtigingen toe onder Hallo `</application>` label.</span><span class="sxs-lookup"><span data-stu-id="f75b4-149">Add hello following necessary GCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="f75b4-150">Zorg ervoor dat tooreplace `<your package>` met Hallo pakketnaam weergegeven boven Hallo Hallo `AndroidManifest.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="f75b4-150">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="f75b4-151">Zie [Een GCM Client-app instellen voor Android](https://developers.google.com/cloud-messaging/android/client#manifest) voor meer informatie over deze machtigingen.</span><span class="sxs-lookup"><span data-stu-id="f75b4-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="f75b4-152">Code toevoegen</span><span class="sxs-lookup"><span data-stu-id="f75b4-152">Adding code</span></span>
1. <span data-ttu-id="f75b4-153">Vouw in de Project-weergave hello, **app** > **src** > **belangrijkste** > **java**.</span><span class="sxs-lookup"><span data-stu-id="f75b4-153">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="f75b4-154">Klik met de rechtermuisknop op de pakketmap onder **java**, klik op **Nieuw** en klik vervolgens op **Java-klasse**.</span><span class="sxs-lookup"><span data-stu-id="f75b4-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="f75b4-155">Voeg een nieuwe klasse met de naam `NotificationSettings` toe.</span><span class="sxs-lookup"><span data-stu-id="f75b4-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - nieuwe Java-klasse][6]
   
    <span data-ttu-id="f75b4-157">Zorg ervoor dat tooupdate deze drie tijdelijke aanduidingen in de volgende code voor Hallo HALLO hallo `NotificationSettings` klasse:</span><span class="sxs-lookup"><span data-stu-id="f75b4-157">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="f75b4-158">**SenderId**: Hallo projectnummer dat u eerder in Hallo verkregen [Google Cloud Console](http://cloud.google.com/console).</span><span class="sxs-lookup"><span data-stu-id="f75b4-158">**SenderId**: hello project number you obtained earlier in hello [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="f75b4-159">**HubListenConnectionString**: Hallo **DefaultListenAccessSignature** verbindingsreeks voor uw hub.</span><span class="sxs-lookup"><span data-stu-id="f75b4-159">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="f75b4-160">U kunt deze verbindingsreeks kopiëren door te klikken op **toegangsbeleid** op Hallo **instellingen** hubblade op Hallo [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="f75b4-160">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="f75b4-161">**HubName**: gebruik Hallo de naam van uw notification hub die wordt weergegeven in de hubblade Hallo in Hallo [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="f75b4-161">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="f75b4-162">`NotificationSettings`-code:</span><span class="sxs-lookup"><span data-stu-id="f75b4-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="f75b4-163">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="f75b4-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="f75b4-164">}</span><span class="sxs-lookup"><span data-stu-id="f75b4-164">}</span></span>
2. <span data-ttu-id="f75b4-165">Een andere nieuwe klasse met de naam met behulp van Hallo bovenstaande stappen toevoegen `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="f75b4-165">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="f75b4-166">Dit is de implementatie van onze exemplaar-id listenerservice.</span><span class="sxs-lookup"><span data-stu-id="f75b4-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="f75b4-167">Hallo-code voor deze klasse roept onze `IntentService` te[vernieuwen Hallo GCM-token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="f75b4-167">hello code for this class will call our `IntentService` too[refresh hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
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


1. <span data-ttu-id="f75b4-168">Toevoegen van een andere nieuwe klasse tooyour project met de naam `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="f75b4-168">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="f75b4-169">Dit is Hallo-implementatie voor onze `IntentService` die wordt afgehandeld [vernieuwen Hallo GCM-token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) en [registreren bij Hallo notification hub](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="f75b4-169">This will be hello implementation for our `IntentService` that will handle [refreshing hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="f75b4-170">Gebruik hello na de code voor deze klasse.</span><span class="sxs-lookup"><span data-stu-id="f75b4-170">Use hello following code for this class.</span></span>
   
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
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="f75b4-171">In uw `MainActivity` klasse, voeg de volgende Hallo `import` instructies hierboven Hallo klasse declaratie.</span><span class="sxs-lookup"><span data-stu-id="f75b4-171">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="f75b4-172">Hallo volgende privé-leden Hallo boven aan het Hallo-klasse toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f75b4-172">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="f75b4-173">We gebruiken deze [Hallo-beschikbaarheid van Google Play Services te controleren, zoals aanbevolen door Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="f75b4-173">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="f75b4-174">In uw `MainActivity` klasse, het toevoegen van Hallo methode toohello beschikbaarheid van Google Play Services te volgen.</span><span class="sxs-lookup"><span data-stu-id="f75b4-174">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
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
5. <span data-ttu-id="f75b4-175">In uw `MainActivity` klasse, het toevoegen van Hallo na de code die wordt gecontroleerd op Google Play Services voordat u uw `IntentService` tooget uw GCM-registratietoken en registreren voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="f75b4-175">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="f75b4-176">In Hallo `OnCreate` methode Hallo `MainActivity` klasse, het toevoegen van Hallo code toostart Hallo registratieproces volgen wanneer activiteit wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f75b4-176">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="f75b4-177">Voeg deze extra methoden toohello `MainActivity` tooverify app status en het rapport status in uw app.</span><span class="sxs-lookup"><span data-stu-id="f75b4-177">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="f75b4-178">Hallo `ToastNotify` methode maakt gebruik van Hallo *"Hallo wereld"* `TextView` tooreport status en kennisgevingen permanent in Hallo app beheren.</span><span class="sxs-lookup"><span data-stu-id="f75b4-178">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="f75b4-179">In de indeling activity_main.XML voegt Hallo volgende-id voor het besturingselement.</span><span class="sxs-lookup"><span data-stu-id="f75b4-179">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="f75b4-180">Vervolgens wordt een subklasse toevoegen voor de ontvanger die is gedefinieerd in AndroidManifest.xml Hallo.</span><span class="sxs-lookup"><span data-stu-id="f75b4-180">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="f75b4-181">Voeg een andere nieuwe klasse tooyour-project met de naam `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="f75b4-181">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="f75b4-182">Toevoegen van de volgende importinstructies boven Hallo aan Hallo `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="f75b4-182">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="f75b4-183">Toevoegen na de code voor Hallo Hallo `MyHandler` waardoor een subklasse zijn van klasse `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="f75b4-183">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="f75b4-184">Deze code overschrijft Hallo `OnReceive` methode, dus Hallo handler ontvangen meldingen rapporteert.</span><span class="sxs-lookup"><span data-stu-id="f75b4-184">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="f75b4-185">Hallo-handler verzendt ook Hallo push notification toohello Android notification manager met behulp van Hallo `sendNotification()` methode.</span><span class="sxs-lookup"><span data-stu-id="f75b4-185">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="f75b4-186">Hallo `sendNotification()` methode moet worden uitgevoerd wanneer het Hallo-app niet actief is en een melding wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="f75b4-186">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="f75b4-187">Klik in Android Studio in de menubalk Hallo **bouwen** > **Project opnieuw opbouwen** toomake ervoor dat er geen fouten in uw code zijn.</span><span class="sxs-lookup"><span data-stu-id="f75b4-187">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="f75b4-188">Pushmeldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="f75b4-188">Sending push notifications</span></span>
<span data-ttu-id="f75b4-189">U kunt testen ontvangen van pushmeldingen in uw app door ze te verzenden via Hallo [Azure Portal] -Hallo zoekt **probleemoplossing** sectie in de hubblade hello, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f75b4-189">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Azure Notification Hubs - Verzenden testen](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="f75b4-191">(Optioneel) Pushmeldingen rechtstreeks vanuit het Hallo-app verzenden</span><span class="sxs-lookup"><span data-stu-id="f75b4-191">(Optional) Send push notifications directly from hello app</span></span>
<span data-ttu-id="f75b4-192">Normaal gesproken verzendt u meldingen via een back-endserver.</span><span class="sxs-lookup"><span data-stu-id="f75b4-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="f75b4-193">Voor sommige gevallen kunt u toobe kunnen toosend pushmeldingen rechtstreeks vanuit de clienttoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="f75b4-193">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="f75b4-194">Deze sectie wordt uitgelegd hoe toosend meldingen van client in Hallo Hallo [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="f75b4-194">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="f75b4-195">Vouw in de Project-weergave van Android Studio-Project **App** > **src** > **main** > **res** > **layout** uit.</span><span class="sxs-lookup"><span data-stu-id="f75b4-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="f75b4-196">Open Hallo `activity_main.xml` lay-bestand en klik op Hallo **tekst** tabblad tooupdate Hallo tekstinhoud van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="f75b4-196">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="f75b4-197">Werk deze bij met de Hallo onderstaande code, waarmee nieuwe toegevoegd `Button` en `EditText` besturingselementen voor het verzenden van push-melding berichten toohello notification hub.</span><span class="sxs-lookup"><span data-stu-id="f75b4-197">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="f75b4-198">Voeg deze code onderin Hallo net voor `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="f75b4-198">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="f75b4-199">Vouw in de Project-weergave van Android Studio-Project **App** > **src** > **main** > **res** > **values** uit.</span><span class="sxs-lookup"><span data-stu-id="f75b4-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="f75b4-200">Open Hallo `strings.xml` bestands- en toevoegen van tekenreekswaarden Hallo waarnaar wordt verwezen door nieuwe Hallo `Button` en `EditText` besturingselementen.</span><span class="sxs-lookup"><span data-stu-id="f75b4-200">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="f75b4-201">Deze onderin Hallo van Hallo-bestand, net voor toevoegen `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="f75b4-201">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="f75b4-202">In uw `NotificationSetting.java` bestand, het toevoegen van Hallo na instelling toohello `NotificationSettings` klasse.</span><span class="sxs-lookup"><span data-stu-id="f75b4-202">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="f75b4-203">Update `HubFullAccess` Hello **DefaultFullSharedAccessSignature** verbindingsreeks voor uw hub.</span><span class="sxs-lookup"><span data-stu-id="f75b4-203">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="f75b4-204">U kunt deze verbindingsreeks kopiëren van Hallo [Azure Portal] door te klikken op **toegangsbeleid** op Hallo **instellingen** blade voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="f75b4-204">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="f75b4-205">In uw `MainActivity.java` bestand, voeg de volgende Hallo `import` instructies hierboven Hallo `MainActivity` klasse.</span><span class="sxs-lookup"><span data-stu-id="f75b4-205">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="f75b4-206">In uw `MainActivity.java` bestand, het toevoegen van de volgende leden boven Hallo HALLO hallo `MainActivity` klasse.</span><span class="sxs-lookup"><span data-stu-id="f75b4-206">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="f75b4-207">Een POST-aanvraag toosend berichten tooyour notification hub, moet u een token tooauthenticate Software Access Signature (SaS) maken.</span><span class="sxs-lookup"><span data-stu-id="f75b4-207">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="f75b4-208">Dit wordt gedaan bij het parseren van belangrijke gegevens uit de verbindingsreeks Hallo Hallo en maak vervolgens Hallo SaS-token, zoals vermeld in Hallo [algemene concepten](http://msdn.microsoft.com/library/azure/dn495627.aspx) naslaginformatie over REST API.</span><span class="sxs-lookup"><span data-stu-id="f75b4-208">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="f75b4-209">Hallo na de code is een voorbeeld van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="f75b4-209">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="f75b4-210">In `MainActivity.java`, toevoegen na methode toohello hello `MainActivity` klasse tooparse de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="f75b4-210">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
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
7. <span data-ttu-id="f75b4-211">In `MainActivity.java`, toevoegen na methode toohello hello `MainActivity` klasse toocreate een SaS-verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="f75b4-211">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
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
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
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
8. <span data-ttu-id="f75b4-212">In `MainActivity.java`, Hallo na methode toohello toevoegen `MainActivity` klasse toohandle hello **melding verzenden** knop klikken en Hallo push-melding bericht toohello hub met behulp van Hallo ingebouwde REST-API te verzenden.</span><span class="sxs-lookup"><span data-stu-id="f75b4-212">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
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
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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

## <a name="testing-your-app"></a><span data-ttu-id="f75b4-213">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="f75b4-213">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="f75b4-214">Pushmeldingen in Hallo-emulator</span><span class="sxs-lookup"><span data-stu-id="f75b4-214">Push notifications in hello emulator</span></span>
<span data-ttu-id="f75b4-215">Als u pushmeldingen tootest binnen een emulator wilt, zorg dat de installatiekopie van de emulator Hallo Google API-niveau die u hebt gekozen voor uw app ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="f75b4-215">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="f75b4-216">Als uw installatiekopie biedt geen ondersteuning voor native Google APIs, u uiteindelijk Hello **SERVICE\_niet\_beschikbaar** uitzondering.</span><span class="sxs-lookup"><span data-stu-id="f75b4-216">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="f75b4-217">Bovendien toohello hierboven, zorg ervoor dat u hebt toegevoegd aan uw Google-account tooyour die emulator onder **instellingen** > **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="f75b4-217">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="f75b4-218">Anders wordt uw tooregister pogingen bij GCM kan leiden tot Hallo **verificatie\_mislukt** uitzondering.</span><span class="sxs-lookup"><span data-stu-id="f75b4-218">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="f75b4-219">Uitvoeren van de toepassing hello</span><span class="sxs-lookup"><span data-stu-id="f75b4-219">Running hello application</span></span>
1. <span data-ttu-id="f75b4-220">Hallo-app uitvoeren en u ziet dat Hallo registratie-ID voor een succesvolle registratie wordt gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="f75b4-220">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
      ![Testen op Android - Kanaalregistratie][18]
2. <span data-ttu-id="f75b4-222">Voer een melding bericht toobe tooall Android-apparaten die zijn geregistreerd met de hub Hallo verzonden.</span><span class="sxs-lookup"><span data-stu-id="f75b4-222">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
      ![Testen op Android - een bericht verzenden][19]

3. <span data-ttu-id="f75b4-224">Druk op **Melding verzenden**.</span><span class="sxs-lookup"><span data-stu-id="f75b4-224">Press **Send Notification**.</span></span> <span data-ttu-id="f75b4-225">Alle apparaten waarop Hallo app actief wordt weergegeven een `AlertDialog` -exemplaar met de Hallo pushmelding.</span><span class="sxs-lookup"><span data-stu-id="f75b4-225">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="f75b4-226">Apparaten die geen Hallo app wordt uitgevoerd, maar die eerder zijn geregistreerd voor pushmeldingen ontvangt een melding in Hallo Android Notification Manager.</span><span class="sxs-lookup"><span data-stu-id="f75b4-226">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="f75b4-227">Die kunnen worden bekeken door omlaag te vegen vanuit de linkerbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="f75b4-227">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
      ![Testen op Android - meldingen][21]

## <a name="next-steps"></a><span data-ttu-id="f75b4-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f75b4-229">Next steps</span></span>
<span data-ttu-id="f75b4-230">Hallo wordt aangeraden [Notification Hubs gebruiken toopush meldingen toousers] zelfstudie Hallo volgende stap.</span><span class="sxs-lookup"><span data-stu-id="f75b4-230">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="f75b4-231">Hierin ziet u hoe toosend meldingen vanuit een ASP.NET-back-end met tags voor specifieke gebruikers tootarget.</span><span class="sxs-lookup"><span data-stu-id="f75b4-231">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="f75b4-232">Als u uw gebruikers op belangengroepen toosegment wilt, bekijk Hallo [Notification Hubs gebruiken toosend belangrijk nieuws] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f75b4-232">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="f75b4-233">toolearn meer algemene informatie over Notification Hubs, Zie onze [richtlijnen voor Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="f75b4-233">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

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
[richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs gebruiken toopush meldingen toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[Notification Hubs gebruiken toosend belangrijk nieuws]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure Portal]: https://portal.azure.com
