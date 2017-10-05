---
title: Aan de slag met Azure Notification Hubs voor Kindle-apps | Microsoft Docs
description: In deze zelfstudie leert u hoe u met Azure Notification Hubs pushmeldingen verstuurt naar een Kindle-toepassing.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7206f152ed7270abc62536a9ee164f7227833bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="f6ba7-103">Aan de slag met Azure Notification Hubs voor Kindle-apps</span><span class="sxs-lookup"><span data-stu-id="f6ba7-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="f6ba7-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f6ba7-104">Overview</span></span>
<span data-ttu-id="f6ba7-105">In deze zelfstudie ziet u hoe u met Azure Notification Hubs pushmeldingen verstuurt naar een Kindle-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Kindle application.</span></span>
<span data-ttu-id="f6ba7-106">U maakt een lege Kindle-app die pushmeldingen ontvangt via Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="f6ba7-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6ba7-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f6ba7-107">Prerequisites</span></span>
<span data-ttu-id="f6ba7-108">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="f6ba7-109">Download de Android-SDK (aannemende dat u Eclipse gebruikt) van de <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android-site</a>.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-109">Get the Android SDK (we assume that you will use Eclipse) from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="f6ba7-110">Volg de stappen in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Uw ontwikkelingsomgeving instellen</a> om uw ontwikkelingsomgeving voor Kindle in te stellen.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-110">Follow the steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> to set up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-to-the-developer-portal"></a><span data-ttu-id="f6ba7-111">Een nieuwe app toevoegen aan de portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="f6ba7-111">Add a new app to the developer portal</span></span>
1. <span data-ttu-id="f6ba7-112">Maak een app in de [Amazon-portal voor ontwikkelaars].</span><span class="sxs-lookup"><span data-stu-id="f6ba7-112">First, create an app in the [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="f6ba7-113">Kopieer de **toepassingssleutel**.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-113">Copy the **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="f6ba7-114">Klik in de portal op de naam van uw app en klik vervolgens op het tabblad **Device Messaging**.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-114">In the portal, click the name of your app, and then click the **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="f6ba7-115">Klik op **Een nieuw beveiligingsprofiel maken** en maak vervolgens een nieuw beveiligingsprofiel (bijvoorbeeld **TestAdm-beveiligingsprofiel**).</span><span class="sxs-lookup"><span data-stu-id="f6ba7-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="f6ba7-116">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="f6ba7-117">Klik op **Beveiligingsprofielen** om het beveiligingsprofiel weer te geven dat u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-117">Click **Security Profiles** to view the security profile that you just created.</span></span> <span data-ttu-id="f6ba7-118">Kopieer de waarden voor **Client-id** en **Clientgeheim** voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-118">Copy the **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="f6ba7-119">Maak een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-119">Create an API key</span></span>
1. <span data-ttu-id="f6ba7-120">Open een opdrachtprompt met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="f6ba7-121">Navigeer naar de map Android SDK.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-121">Navigate to the Android SDK folder.</span></span>
3. <span data-ttu-id="f6ba7-122">Voer de volgende opdracht in:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-122">Enter the following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="f6ba7-123">Voor het **KeyStore**-wachtwoord typt u **android**.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-123">For the **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="f6ba7-124">Kopieer de **MD5**-vingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-124">Copy the **MD5** fingerprint.</span></span>
6. <span data-ttu-id="f6ba7-125">Klik in de portal voor ontwikkelaars op het tabblad **Berichten**, klik op **Android/Kindle** en voer de naam in van het pakket voor uw app (bijvoorbeeld **com.sample.notificationhubtest**) en de **MD5**-waarde en klik vervolgens op **API-sleutel genereren**.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-125">Back in the developer portal, on the **Messaging** tab, click **Android/Kindle** and enter the name of the package for your app (for example, **com.sample.notificationhubtest**) and the **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-to-the-hub"></a><span data-ttu-id="f6ba7-126">Referenties aan de hub toevoegen</span><span class="sxs-lookup"><span data-stu-id="f6ba7-126">Add credentials to the hub</span></span>
<span data-ttu-id="f6ba7-127">Voeg in de portal het clientgeheim en de client-id in op het tabblad **Configureren** van uw Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-127">In the portal, add the client secret and client ID to the **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="f6ba7-128">Uw toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="f6ba7-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="f6ba7-129">Wanneer u een toepassing maakt, gebruikt u ten minste API-niveau 17.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="f6ba7-130">De ADM-bibliotheken aan uw Eclipse-project toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-130">Add the ADM libraries to your Eclipse project:</span></span>

1. <span data-ttu-id="f6ba7-131">Als u de ADM-bibliotheek wilt verkrijgen, [downloadt u de SDK].</span><span class="sxs-lookup"><span data-stu-id="f6ba7-131">To obtain the ADM library, [download the SDK].</span></span> <span data-ttu-id="f6ba7-132">Pak het SDK-zipbestand uit.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-132">Extract the SDK zip file.</span></span>
2. <span data-ttu-id="f6ba7-133">Klik in Eclipse met de rechtermuisknop op het project en klik vervolgens op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="f6ba7-134">Selecteer **Javabuild-pad** aan de linkerkant en selecteer vervolgens de ** bibliotheken ** boven op het tabblad.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-134">Select **Java Build Path** on the left, and then select the **Libraries **tab at the top.</span></span> <span data-ttu-id="f6ba7-135">Klik op **Externe jar toevoegen** en selecteer het bestand `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` in de map waaruit u de Amazon SDK hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-135">Click **Add External Jar**, and select the file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from the directory in which you extracted the Amazon SDK.</span></span>
3. <span data-ttu-id="f6ba7-136">Download de NotificationHubs Android-SDK (koppeling).</span><span class="sxs-lookup"><span data-stu-id="f6ba7-136">Download the NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="f6ba7-137">Pak het pakket uit en sleep het bestand `notification-hubs-sdk.jar` in de `libs` map in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-137">Unzip the package, and then drag the file `notification-hubs-sdk.jar` into the `libs` folder in Eclipse.</span></span>

<span data-ttu-id="f6ba7-138">Uw app-manifest bewerken voor ondersteuning van ADM:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-138">Edit your app manifest to support ADM:</span></span>

1. <span data-ttu-id="f6ba7-139">De Amazon-naamruimte in het basismanifestelement toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-139">Add the Amazon namespace in the root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="f6ba7-140">Voeg machtigingen toe als het eerste element onder het manifestelement.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-140">Add permissions as the first element under the manifest element.</span></span> <span data-ttu-id="f6ba7-141">Vervang **[NAAM VAN UW PAKKET]**door de naam het pakket dat u hebt gebruikt om uw app te maken.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-141">Substitute **[YOUR PACKAGE NAME]** with the package that you used to create your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access to receive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK to keep the processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="f6ba7-142">Voeg het volgende element in als het eerste onderliggende item van het toepassingselement.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-142">Insert the following element as the first child of the application element.</span></span> <span data-ttu-id="f6ba7-143">Vervang **[NAAM VAN UW SERVICE]** door de ADM-berichtenhandler die u maakt in het volgende gedeelte (inclusief het pakket) en wijzig **[NAAM VAN UW PAKKET]** in de pakketnaam waarmee u uw app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-143">Remember to substitute **[YOUR SERVICE NAME]** with the name of your ADM message handler that you create in the next section (including the package), and replace **[YOUR PACKAGE NAME]** with the package name with which you created your app.</span></span>
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- To interact with ADM, your app must listen for the following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace the name in the category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="f6ba7-144">De ADM-berichtenhandler maken</span><span class="sxs-lookup"><span data-stu-id="f6ba7-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="f6ba7-145">Maak een nieuwe klasse die eigenschappen overneemt van `com.amazon.device.messaging.ADMMessageHandlerBase` en geef deze de naam `MyADMMessageHandler`, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in the following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="f6ba7-146">Voeg de volgende `import` instructies toe:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-146">Add the following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="f6ba7-147">Voeg de volgende code toe aan de klasse die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-147">Add the following code in the class that you created.</span></span> <span data-ttu-id="f6ba7-148">Vervang de hubnaam en de verbindingsreeks (luisteren):</span><span class="sxs-lookup"><span data-stu-id="f6ba7-148">Remember to substitute the hub name and connection string (listen):</span></span>
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. <span data-ttu-id="f6ba7-149">Voeg de volgende code toe aan de methode `OnMessage()`:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-149">Add the following code to the `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="f6ba7-150">Voeg de volgende code toe aan de methode `OnRegistered`:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-150">Add the following code to the `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="f6ba7-151">Voeg de volgende code toe aan de methode `OnUnregistered`:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-151">Add the following code to the `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="f6ba7-152">Voeg in de methode `MainActivity` de volgende importinstructie toe:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-152">In the `MainActivity` method, add the following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="f6ba7-153">Voeg de volgende code toe aan het einde van de methode `OnCreate`:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-153">Add the following code at the end of the `OnCreate` method:</span></span>
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-to-your-app"></a><span data-ttu-id="f6ba7-154">Uw API-sleutel aan uw app toevoegen</span><span class="sxs-lookup"><span data-stu-id="f6ba7-154">Add your API key to your app</span></span>
1. <span data-ttu-id="f6ba7-155">Maak in Eclipse een nieuw bestand met de naam **api_key.txt** in de map van uw project.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-155">In Eclipse, create a new file named **api_key.txt** in the directory assets of your project.</span></span>
2. <span data-ttu-id="f6ba7-156">Open het bestand en kopieer de API-sleutel die u in de Amazon-portal voor ontwikkelaars hebt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-156">Open the file and copy the API key that you generated in the Amazon developer portal.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="f6ba7-157">De app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f6ba7-157">Run the app</span></span>
1. <span data-ttu-id="f6ba7-158">Start de emulator.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-158">Start the emulator.</span></span>
2. <span data-ttu-id="f6ba7-159">Veeg in de emulator vanaf de bovenkant en klik op **Instellingen**. Klik vervolgens op **Mijn account** en meld u aan met een geldig Amazon-account.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-159">In the emulator, swipe from the top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="f6ba7-160">Voer vervolgens de app uit in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-160">In Eclipse, run the app.</span></span>

> [!NOTE]
> <span data-ttu-id="f6ba7-161">Als er een probleem optreedt, controleert u het tijdstip van de emulator (of het apparaat).</span><span class="sxs-lookup"><span data-stu-id="f6ba7-161">If a problem occurs, check the time of the emulator (or device).</span></span> <span data-ttu-id="f6ba7-162">De tijdswaarde moet juist zijn.</span><span class="sxs-lookup"><span data-stu-id="f6ba7-162">The time value must be accurate.</span></span> <span data-ttu-id="f6ba7-163">Voer de volgende opdracht uit de map Android SDK platform-hulpprogramma's uit als u de tijd van de Kindle-emulator wilt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-163">To change the time of the Kindle emulator, you can run the following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="f6ba7-164">Een bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="f6ba7-164">Send a message</span></span>
<span data-ttu-id="f6ba7-165">Een bericht verzenden met .NET:</span><span class="sxs-lookup"><span data-stu-id="f6ba7-165">To send a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
<span data-ttu-id="f6ba7-166">[Amazon-portal voor ontwikkelaars]: https://developer.amazon.com/home.html</span><span class="sxs-lookup"><span data-stu-id="f6ba7-166">[Amazon developer portal]: https://developer.amazon.com/home.html</span></span>
<span data-ttu-id="f6ba7-167">[downloadt u de SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span><span class="sxs-lookup"><span data-stu-id="f6ba7-167">[download the SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span></span>

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
