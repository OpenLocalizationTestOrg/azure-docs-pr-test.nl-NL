---
title: aaaGet de slag met Azure Notification Hubs voor Kindle-apps | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Kindle-toepassing.
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
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="6e216-103">Aan de slag met Azure Notification Hubs voor Kindle-apps</span><span class="sxs-lookup"><span data-stu-id="6e216-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="6e216-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6e216-104">Overview</span></span>
<span data-ttu-id="6e216-105">Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Kindle-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e216-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="6e216-106">U maakt een lege Kindle-app die pushmeldingen ontvangt via Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="6e216-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e216-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e216-107">Prerequisites</span></span>
<span data-ttu-id="6e216-108">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="6e216-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="6e216-109">Hallo Android SDK (Aannemende dat u Eclipse) niet ophalen uit Hallo <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android-site</a>.</span><span class="sxs-lookup"><span data-stu-id="6e216-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="6e216-110">Volg de stappen Hallo in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">uw ontwikkelingsomgeving instellen</a> tooset van uw ontwikkelingsomgeving voor Kindle.</span><span class="sxs-lookup"><span data-stu-id="6e216-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="6e216-111">Voeg een nieuwe app toohello developer-portal</span><span class="sxs-lookup"><span data-stu-id="6e216-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="6e216-112">Maak eerst een app in Hallo [Amazon-portal voor ontwikkelaars].</span><span class="sxs-lookup"><span data-stu-id="6e216-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="6e216-113">Kopiëren Hallo **Toepassingssleutel**.</span><span class="sxs-lookup"><span data-stu-id="6e216-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="6e216-114">Klik op de naam van uw app Hallo in Hallo-portal en klik vervolgens op Hallo **Device Messaging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6e216-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="6e216-115">Klik op **Een nieuw beveiligingsprofiel maken** en maak vervolgens een nieuw beveiligingsprofiel (bijvoorbeeld **TestAdm-beveiligingsprofiel**).</span><span class="sxs-lookup"><span data-stu-id="6e216-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="6e216-116">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6e216-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="6e216-117">Klik op **beveiligingsprofielen** tooview Hallo beveiligingsprofiel die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e216-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="6e216-118">Kopiëren Hallo **Client-ID** en **Clientgeheim** waarden voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="6e216-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="6e216-119">Maak een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="6e216-119">Create an API key</span></span>
1. <span data-ttu-id="6e216-120">Open een opdrachtprompt met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="6e216-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="6e216-121">Navigeer toohello Android SDK-map.</span><span class="sxs-lookup"><span data-stu-id="6e216-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="6e216-122">Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6e216-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="6e216-123">Voor Hallo **keystore** wachtwoord, type **android**.</span><span class="sxs-lookup"><span data-stu-id="6e216-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="6e216-124">Kopiëren Hallo **MD5** vingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="6e216-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="6e216-125">Terug in de ontwikkelaarsportal Hallo op Hallo **Messaging** tabblad **Android/Kindle** en voer de naam Hallo van Hallo-pakket voor uw app (bijvoorbeeld **com.sample.notificationhubtest**) en Hallo **MD5** waarde en klik vervolgens op **API-sleutel genereren**.</span><span class="sxs-lookup"><span data-stu-id="6e216-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="6e216-126">Referenties toohello hub toevoegen</span><span class="sxs-lookup"><span data-stu-id="6e216-126">Add credentials toohello hub</span></span>
<span data-ttu-id="6e216-127">Voeg in Hallo portal Hallo client geheim en client-ID toohello **configureren** tabblad van uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="6e216-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="6e216-128">Uw toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="6e216-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="6e216-129">Wanneer u een toepassing maakt, gebruikt u ten minste API-niveau 17.</span><span class="sxs-lookup"><span data-stu-id="6e216-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="6e216-130">Hallo ADM-bibliotheken tooyour Eclipse-project toevoegen:</span><span class="sxs-lookup"><span data-stu-id="6e216-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="6e216-131">tooobtain hello ADM-bibliotheek [Hallo SDK downloaden].</span><span class="sxs-lookup"><span data-stu-id="6e216-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="6e216-132">Hallo SDK zip-bestand extraheren.</span><span class="sxs-lookup"><span data-stu-id="6e216-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="6e216-133">Klik in Eclipse met de rechtermuisknop op het project en klik vervolgens op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="6e216-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="6e216-134">Selecteer **Javabuild-pad** op Hallo links en selecteer vervolgens Hallo ** bibliotheken ** Hallo boven op tabblad.</span><span class="sxs-lookup"><span data-stu-id="6e216-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="6e216-135">Klik op **externe Jar toevoegen**, en selecteer Hallo bestand `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` uit Hallo directory waarin u Hallo Amazon SDK hebt uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="6e216-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="6e216-136">Download Hallo NotificationHubs Android-SDK (koppeling).</span><span class="sxs-lookup"><span data-stu-id="6e216-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="6e216-137">Pak Hallo pakket uit en sleep Hallo bestand `notification-hubs-sdk.jar` in Hallo `libs` map in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="6e216-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="6e216-138">Uw app-manifest toosupport ADM bewerken:</span><span class="sxs-lookup"><span data-stu-id="6e216-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="6e216-139">Hallo Amazon-naamruimte op Hallo basismanifestelement toevoegen:</span><span class="sxs-lookup"><span data-stu-id="6e216-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="6e216-140">Machtigingen toevoegen als eerste element onder het manifestelement Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e216-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="6e216-141">Vervang **[naam van uw pakket]** met Hallo-pakket dat u toocreate uw app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6e216-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="6e216-142">Hallo element als eerste onderliggende Hallo Hallo toepassingselement na invoegen.</span><span class="sxs-lookup"><span data-stu-id="6e216-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="6e216-143">Houd er rekening mee toosubstitute **[naam van uw SERVICE]** met de naam van uw ADM-berichtenhandler die u maakt in Hallo volgende gedeelte (inclusief Hallo-pakket) en vervangen Hallo **[naam van uw pakket]** Hello de pakketnaam waarmee u uw app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e216-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
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
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="6e216-144">De ADM-berichtenhandler maken</span><span class="sxs-lookup"><span data-stu-id="6e216-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="6e216-145">Maak een nieuwe klasse die eigenschappen van overneemt `com.amazon.device.messaging.ADMMessageHandlerBase` en noem deze `MyADMMessageHandler`, zoals weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="6e216-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="6e216-146">Voeg de volgende Hallo `import` instructies:</span><span class="sxs-lookup"><span data-stu-id="6e216-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="6e216-147">Voeg Hallo na de code in Hallo-klasse die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e216-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="6e216-148">Houd er rekening mee toosubstitute Hallo hub en de verbindingsreeks (luisteren):</span><span class="sxs-lookup"><span data-stu-id="6e216-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="6e216-149">Hallo na code toohello toevoegen `OnMessage()` methode:</span><span class="sxs-lookup"><span data-stu-id="6e216-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="6e216-150">Hallo na code toohello toevoegen `OnRegistered` methode:</span><span class="sxs-lookup"><span data-stu-id="6e216-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="6e216-151">Hallo na code toohello toevoegen `OnUnregistered` methode:</span><span class="sxs-lookup"><span data-stu-id="6e216-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="6e216-152">In Hallo `MainActivity` methode Hallo volgende importinstructie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="6e216-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="6e216-153">Toevoegen van de volgende code achter Hallo HALLO hallo `OnCreate` methode:</span><span class="sxs-lookup"><span data-stu-id="6e216-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="6e216-154">Uw API-sleutel tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="6e216-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="6e216-155">Maak in Eclipse een nieuw bestand met de naam **api_key.txt** in Hallo map van uw project.</span><span class="sxs-lookup"><span data-stu-id="6e216-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="6e216-156">Open Hallo-bestand en kopieer Hallo API-sleutel die u hebt gegenereerd in Hallo Amazon-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="6e216-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="6e216-157">Hallo-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6e216-157">Run hello app</span></span>
1. <span data-ttu-id="6e216-158">Hallo-emulator wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="6e216-158">Start hello emulator.</span></span>
2. <span data-ttu-id="6e216-159">Veeg vanaf de bovenkant Hallo in Hallo-emulator en klik op **instellingen**, en klik vervolgens op **Mijn account** en registreren met een geldig Amazon-account.</span><span class="sxs-lookup"><span data-stu-id="6e216-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="6e216-160">Voer Hallo-app in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="6e216-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="6e216-161">Als een probleem optreedt, controleert u Hallo-tijd van het Hallo-emulator (of apparaat).</span><span class="sxs-lookup"><span data-stu-id="6e216-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="6e216-162">Hallo tijdswaarde moet juist zijn.</span><span class="sxs-lookup"><span data-stu-id="6e216-162">hello time value must be accurate.</span></span> <span data-ttu-id="6e216-163">toochange Hallo-tijd van Hallo Kindle-emulator, u kunt uitvoeren Hallo volgende opdracht uit de directory van uw Android SDK platform-hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="6e216-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="6e216-164">Een bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="6e216-164">Send a message</span></span>
<span data-ttu-id="6e216-165">een bericht met behulp van .NET toosend:</span><span class="sxs-lookup"><span data-stu-id="6e216-165">toosend a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[Amazon-portal voor ontwikkelaars]: https://developer.amazon.com/home.html
[Hallo SDK downloaden]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
