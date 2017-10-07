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
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a>Aan de slag met Azure Notification Hubs voor Kindle-apps
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Kindle-toepassing.
U maakt een lege Kindle-app die pushmeldingen ontvangt via Amazon Device Messaging (ADM).

## <a name="prerequisites"></a>Vereisten
Deze zelfstudie vereist de volgende Hallo:

* Hallo Android SDK (Aannemende dat u Eclipse) niet ophalen uit Hallo <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android-site</a>.
* Volg de stappen Hallo in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">uw ontwikkelingsomgeving instellen</a> tooset van uw ontwikkelingsomgeving voor Kindle.

## <a name="add-a-new-app-toohello-developer-portal"></a>Voeg een nieuwe app toohello developer-portal
1. Maak eerst een app in Hallo [Amazon-portal voor ontwikkelaars].
   
    ![][0]
2. Kopiëren Hallo **Toepassingssleutel**.
   
    ![][1]
3. Klik op de naam van uw app Hallo in Hallo-portal en klik vervolgens op Hallo **Device Messaging** tabblad.
   
    ![][2]
4. Klik op **Een nieuw beveiligingsprofiel maken** en maak vervolgens een nieuw beveiligingsprofiel (bijvoorbeeld **TestAdm-beveiligingsprofiel**). Klik vervolgens op **Opslaan**.
   
    ![][3]
5. Klik op **beveiligingsprofielen** tooview Hallo beveiligingsprofiel die u zojuist hebt gemaakt. Kopiëren Hallo **Client-ID** en **Clientgeheim** waarden voor later gebruik.
   
    ![][4]

## <a name="create-an-api-key"></a>Maak een API-sleutel.
1. Open een opdrachtprompt met beheerdersbevoegdheden.
2. Navigeer toohello Android SDK-map.
3. Voer Hallo volgende opdracht:
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. Voor Hallo **keystore** wachtwoord, type **android**.
5. Kopiëren Hallo **MD5** vingerafdruk.
6. Terug in de ontwikkelaarsportal Hallo op Hallo **Messaging** tabblad **Android/Kindle** en voer de naam Hallo van Hallo-pakket voor uw app (bijvoorbeeld **com.sample.notificationhubtest**) en Hallo **MD5** waarde en klik vervolgens op **API-sleutel genereren**.

## <a name="add-credentials-toohello-hub"></a>Referenties toohello hub toevoegen
Voeg in Hallo portal Hallo client geheim en client-ID toohello **configureren** tabblad van uw notification hub.

## <a name="set-up-your-application"></a>Uw toepassing instellen
> [!NOTE]
> Wanneer u een toepassing maakt, gebruikt u ten minste API-niveau 17.
> 
> 

Hallo ADM-bibliotheken tooyour Eclipse-project toevoegen:

1. tooobtain hello ADM-bibliotheek [Hallo SDK downloaden]. Hallo SDK zip-bestand extraheren.
2. Klik in Eclipse met de rechtermuisknop op het project en klik vervolgens op **Eigenschappen**. Selecteer **Javabuild-pad** op Hallo links en selecteer vervolgens Hallo ** bibliotheken ** Hallo boven op tabblad. Klik op **externe Jar toevoegen**, en selecteer Hallo bestand `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` uit Hallo directory waarin u Hallo Amazon SDK hebt uitgepakt.
3. Download Hallo NotificationHubs Android-SDK (koppeling).
4. Pak Hallo pakket uit en sleep Hallo bestand `notification-hubs-sdk.jar` in Hallo `libs` map in Eclipse.

Uw app-manifest toosupport ADM bewerken:

1. Hallo Amazon-naamruimte op Hallo basismanifestelement toevoegen:

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. Machtigingen toevoegen als eerste element onder het manifestelement Hallo Hallo. Vervang **[naam van uw pakket]** met Hallo-pakket dat u toocreate uw app gebruikt.
   
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
2. Hallo element als eerste onderliggende Hallo Hallo toepassingselement na invoegen. Houd er rekening mee toosubstitute **[naam van uw SERVICE]** met de naam van uw ADM-berichtenhandler die u maakt in Hallo volgende gedeelte (inclusief Hallo-pakket) en vervangen Hallo **[naam van uw pakket]** Hello de pakketnaam waarmee u uw app hebt gemaakt.
   
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

## <a name="create-your-adm-message-handler"></a>De ADM-berichtenhandler maken
1. Maak een nieuwe klasse die eigenschappen van overneemt `com.amazon.device.messaging.ADMMessageHandlerBase` en noem deze `MyADMMessageHandler`, zoals weergegeven in de volgende afbeelding Hallo:
   
    ![][6]
2. Voeg de volgende Hallo `import` instructies:
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. Voeg Hallo na de code in Hallo-klasse die u hebt gemaakt. Houd er rekening mee toosubstitute Hallo hub en de verbindingsreeks (luisteren):
   
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
4. Hallo na code toohello toevoegen `OnMessage()` methode:
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. Hallo na code toohello toevoegen `OnRegistered` methode:
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. Hallo na code toohello toevoegen `OnUnregistered` methode:
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. In Hallo `MainActivity` methode Hallo volgende importinstructie toevoegen:
   
        import com.amazon.device.messaging.ADM;
8. Toevoegen van de volgende code achter Hallo HALLO hallo `OnCreate` methode:
   
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

## <a name="add-your-api-key-tooyour-app"></a>Uw API-sleutel tooyour app toevoegen
1. Maak in Eclipse een nieuw bestand met de naam **api_key.txt** in Hallo map van uw project.
2. Open Hallo-bestand en kopieer Hallo API-sleutel die u hebt gegenereerd in Hallo Amazon-portal voor ontwikkelaars.

## <a name="run-hello-app"></a>Hallo-app uitvoeren
1. Hallo-emulator wordt gestart.
2. Veeg vanaf de bovenkant Hallo in Hallo-emulator en klik op **instellingen**, en klik vervolgens op **Mijn account** en registreren met een geldig Amazon-account.
3. Voer Hallo-app in Eclipse.

> [!NOTE]
> Als een probleem optreedt, controleert u Hallo-tijd van het Hallo-emulator (of apparaat). Hallo tijdswaarde moet juist zijn. toochange Hallo-tijd van Hallo Kindle-emulator, u kunt uitvoeren Hallo volgende opdracht uit de directory van uw Android SDK platform-hulpprogramma's:
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a>Een bericht verzenden
een bericht met behulp van .NET toosend:

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
