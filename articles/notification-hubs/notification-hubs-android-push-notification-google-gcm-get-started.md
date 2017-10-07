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
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a>Push notifications tooAndroid met Azure Notification Hubs verzenden
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Overzicht
> [!IMPORTANT]
> In dit onderwerp worden pushmeldingen met Google Cloud Messaging (GCM) getoond. Als u gebruikmaakt van Google Firebase Cloud Messaging (FCM), raadpleegt u [verzenden push notifications tooAndroid met Azure Notification Hubs en FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).
> 
> 

Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooan Android-toepassing.
U maakt een lege Android-app die pushmeldingen ontvangt via Google Cloud Messaging (GCM).

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

code voor deze zelfstudie Hallo voltooid kan worden gedownload van GitHub [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).

## <a name="prerequisites"></a>Vereisten
> [!IMPORTANT]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started) voor meer informatie.
> 
> 

Bovendien tooan actief Azure-account hierboven vermeld in deze zelfstudie vereist alleen de meest recente versie van Hallo [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).

Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Android-apps.

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a>Een project maken dat Google Cloud Messaging ondersteunt
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Een nieuwe Notification Hub configureren
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   In Hallo **instellingen** blade Selecteer **Notification Services** en vervolgens **Google (GCM)**. Voer Hallo API-sleutel in en klik op **opslaan**.

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

Uw notification hub is nu geconfigureerd toowork bij GCM en u hebt Hallo verbinding tekenreeksen tooboth de tooreceive van uw app registreren en pushmeldingen te verzenden.

## <a id="connecting-app"></a>Verbinding maken met uw app toohello notification hub
### <a name="create-a-new-android-project"></a>Een nieuw Android-project maken
1. Start een nieuw Android Studio-project in Android Studio.
   
   ![Android Studio - nieuw project][13]
2. Kies Hallo **telefoon en Tablet** factor en Hallo **minimale SDK** dat u wilt dat toosupport. Klik op **Volgende**.
   
   ![Android Studio - werkstroom voor het maken van een project][14]
3. Kies **lege activiteit** Hallo belangrijkste activiteit, klikt u op **volgende**, en klik vervolgens op **voltooien**.

### <a name="add-google-play-services-toohello-project"></a>Google Play services toohello project toevoegen
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Azure Notification Hubs-bibliotheken toevoegen
1. In Hallo `Build.Gradle` -bestand voor Hallo **app**, toevoegen van de volgende regels in Hallo Hallo **afhankelijkheden** sectie.
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. Toevoegen van de volgende opslagplaats na Hallo Hallo **afhankelijkheden** sectie.
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a>Hallo AndroidManifest.xml bijwerken.
1. toosupport GCM, moet er een exemplaar-ID listenerservice implementeren in de code die wordt gebruikt te[verkrijgen van registratietokens](https://developers.google.com/cloud-messaging/android/client#sample-register) met [van Google API voor exemplaar-ID](https://developers.google.com/instance-id/). In deze zelfstudie noemen we Hallo klasse `MyInstanceIDService`. 
   
    Hallo na toohello AndroidManifest.xml servicedefinitiebestand binnen Hallo toevoegen `<application>` label. Vervang Hallo `<your package>` aanduiding voor items met de werkelijke pakketnaam die wordt weergegeven boven Hallo HALLO hallo `AndroidManifest.xml` bestand.
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. Wanneer we ons GCM-registratietoken van Hallo API exemplaar-ID hebt ontvangen, dit wordt gebruikt te[registreren bij Azure Notification Hub Hallo](notification-hubs-push-notification-registration-management.md). Deze registratie wordt ondersteund in Hallo achtergrond met behulp van een `IntentService` met de naam `RegistrationIntentService`. Deze service ook is verantwoordelijk voor [het vernieuwen van ons GCM-registratietoken](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).
   
    Hallo na toohello AndroidManifest.xml servicedefinitiebestand binnen Hallo toevoegen `<application>` label. Vervang Hallo `<your package>` aanduiding voor items met de werkelijke pakketnaam die wordt weergegeven boven Hallo HALLO hallo `AndroidManifest.xml` bestand. 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. Definieert een ontvanger tooreceive meldingen. Hallo volgende ontvanger definitie toohello bestand AndroidManifest.xml in Hallo toevoegen `<application>` label. Vervang Hallo `<your package>` aanduiding voor items met de werkelijke pakketnaam die wordt weergegeven boven Hallo HALLO hallo `AndroidManifest.xml` bestand.
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. Voeg Hallo volgende vereiste GCM gerelateerde machtigingen toe onder Hallo `</application>` label. Zorg ervoor dat tooreplace `<your package>` met Hallo pakketnaam weergegeven boven Hallo Hallo `AndroidManifest.xml` bestand.
   
    Zie [Een GCM Client-app instellen voor Android](https://developers.google.com/cloud-messaging/android/client#manifest) voor meer informatie over deze machtigingen.
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a>Code toevoegen
1. Vouw in de Project-weergave hello, **app** > **src** > **belangrijkste** > **java**. Klik met de rechtermuisknop op de pakketmap onder **java**, klik op **Nieuw** en klik vervolgens op **Java-klasse**. Voeg een nieuwe klasse met de naam `NotificationSettings` toe. 
   
    ![Android Studio - nieuwe Java-klasse][6]
   
    Zorg ervoor dat tooupdate deze drie tijdelijke aanduidingen in de volgende code voor Hallo HALLO hallo `NotificationSettings` klasse:
   
   * **SenderId**: Hallo projectnummer dat u eerder in Hallo verkregen [Google Cloud Console](http://cloud.google.com/console).
   * **HubListenConnectionString**: Hallo **DefaultListenAccessSignature** verbindingsreeks voor uw hub. U kunt deze verbindingsreeks kopiëren door te klikken op **toegangsbeleid** op Hallo **instellingen** hubblade op Hallo [Azure Portal].
   * **HubName**: gebruik Hallo de naam van uw notification hub die wordt weergegeven in de hubblade Hallo in Hallo [Azure Portal].
     
     `NotificationSettings`-code:
     
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       }
2. Een andere nieuwe klasse met de naam met behulp van Hallo bovenstaande stappen toevoegen `MyInstanceIDService`. Dit is de implementatie van onze exemplaar-id listenerservice.
   
    Hallo-code voor deze klasse roept onze `IntentService` te[vernieuwen Hallo GCM-token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) op Hallo achtergrond.
   
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


1. Toevoegen van een andere nieuwe klasse tooyour project met de naam `RegistrationIntentService`. Dit is Hallo-implementatie voor onze `IntentService` die wordt afgehandeld [vernieuwen Hallo GCM-token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) en [registreren bij Hallo notification hub](notification-hubs-push-notification-registration-management.md).
   
    Gebruik hello na de code voor deze klasse.
   
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
2. In uw `MainActivity` klasse, voeg de volgende Hallo `import` instructies hierboven Hallo klasse declaratie.
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. Hallo volgende privé-leden Hallo boven aan het Hallo-klasse toevoegen. We gebruiken deze [Hallo-beschikbaarheid van Google Play Services te controleren, zoals aanbevolen door Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. In uw `MainActivity` klasse, het toevoegen van Hallo methode toohello beschikbaarheid van Google Play Services te volgen. 
   
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
5. In uw `MainActivity` klasse, het toevoegen van Hallo na de code die wordt gecontroleerd op Google Play Services voordat u uw `IntentService` tooget uw GCM-registratietoken en registreren voor uw notification hub.
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. In Hallo `OnCreate` methode Hallo `MainActivity` klasse, het toevoegen van Hallo code toostart Hallo registratieproces volgen wanneer activiteit wordt gemaakt.
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. Voeg deze extra methoden toohello `MainActivity` tooverify app status en het rapport status in uw app.
   
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
8. Hallo `ToastNotify` methode maakt gebruik van Hallo *"Hallo wereld"* `TextView` tooreport status en kennisgevingen permanent in Hallo app beheren. In de indeling activity_main.XML voegt Hallo volgende-id voor het besturingselement.
   
       android:id="@+id/text_hello"
9. Vervolgens wordt een subklasse toevoegen voor de ontvanger die is gedefinieerd in AndroidManifest.xml Hallo. Voeg een andere nieuwe klasse tooyour-project met de naam `MyHandler`.
10. Toevoegen van de volgende importinstructies boven Hallo aan Hallo `MyHandler.java`:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. Toevoegen na de code voor Hallo Hallo `MyHandler` waardoor een subklasse zijn van klasse `com.microsoft.windowsazure.notifications.NotificationsHandler`.
    
    Deze code overschrijft Hallo `OnReceive` methode, dus Hallo handler ontvangen meldingen rapporteert. Hallo-handler verzendt ook Hallo push notification toohello Android notification manager met behulp van Hallo `sendNotification()` methode. Hallo `sendNotification()` methode moet worden uitgevoerd wanneer het Hallo-app niet actief is en een melding wordt ontvangen.
    
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
12. Klik in Android Studio in de menubalk Hallo **bouwen** > **Project opnieuw opbouwen** toomake ervoor dat er geen fouten in uw code zijn.

## <a name="sending-push-notifications"></a>Pushmeldingen verzenden
U kunt testen ontvangen van pushmeldingen in uw app door ze te verzenden via Hallo [Azure Portal] -Hallo zoekt **probleemoplossing** sectie in de hubblade hello, zoals hieronder wordt weergegeven.

![Azure Notification Hubs - Verzenden testen](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a>(Optioneel) Pushmeldingen rechtstreeks vanuit het Hallo-app verzenden
Normaal gesproken verzendt u meldingen via een back-endserver. Voor sommige gevallen kunt u toobe kunnen toosend pushmeldingen rechtstreeks vanuit de clienttoepassing Hallo. Deze sectie wordt uitgelegd hoe toosend meldingen van client in Hallo Hallo [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).

1. Vouw in de Project-weergave van Android Studio-Project **App** > **src** > **main** > **res** > **layout** uit. Open Hallo `activity_main.xml` lay-bestand en klik op Hallo **tekst** tabblad tooupdate Hallo tekstinhoud van Hallo-bestand. Werk deze bij met de Hallo onderstaande code, waarmee nieuwe toegevoegd `Button` en `EditText` besturingselementen voor het verzenden van push-melding berichten toohello notification hub. Voeg deze code onderin Hallo net voor `</RelativeLayout>`.
   
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
2. Vouw in de Project-weergave van Android Studio-Project **App** > **src** > **main** > **res** > **values** uit. Open Hallo `strings.xml` bestands- en toevoegen van tekenreekswaarden Hallo waarnaar wordt verwezen door nieuwe Hallo `Button` en `EditText` besturingselementen. Deze onderin Hallo van Hallo-bestand, net voor toevoegen `</resources>`.
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. In uw `NotificationSetting.java` bestand, het toevoegen van Hallo na instelling toohello `NotificationSettings` klasse.
   
    Update `HubFullAccess` Hello **DefaultFullSharedAccessSignature** verbindingsreeks voor uw hub. U kunt deze verbindingsreeks kopiëren van Hallo [Azure Portal] door te klikken op **toegangsbeleid** op Hallo **instellingen** blade voor uw notification hub.
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. In uw `MainActivity.java` bestand, voeg de volgende Hallo `import` instructies hierboven Hallo `MainActivity` klasse.
   
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
5. In uw `MainActivity.java` bestand, het toevoegen van de volgende leden boven Hallo HALLO hallo `MainActivity` klasse.    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. Een POST-aanvraag toosend berichten tooyour notification hub, moet u een token tooauthenticate Software Access Signature (SaS) maken. Dit wordt gedaan bij het parseren van belangrijke gegevens uit de verbindingsreeks Hallo Hallo en maak vervolgens Hallo SaS-token, zoals vermeld in Hallo [algemene concepten](http://msdn.microsoft.com/library/azure/dn495627.aspx) naslaginformatie over REST API. Hallo na de code is een voorbeeld van de implementatie.
   
    In `MainActivity.java`, toevoegen na methode toohello hello `MainActivity` klasse tooparse de verbindingsreeks.
   
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
7. In `MainActivity.java`, toevoegen na methode toohello hello `MainActivity` klasse toocreate een SaS-verificatietoken.
   
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
8. In `MainActivity.java`, Hallo na methode toohello toevoegen `MainActivity` klasse toohandle hello **melding verzenden** knop klikken en Hallo push-melding bericht toohello hub met behulp van Hallo ingebouwde REST-API te verzenden.
   
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

## <a name="testing-your-app"></a>Uw app testen
#### <a name="push-notifications-in-hello-emulator"></a>Pushmeldingen in Hallo-emulator
Als u pushmeldingen tootest binnen een emulator wilt, zorg dat de installatiekopie van de emulator Hallo Google API-niveau die u hebt gekozen voor uw app ondersteunt. Als uw installatiekopie biedt geen ondersteuning voor native Google APIs, u uiteindelijk Hello **SERVICE\_niet\_beschikbaar** uitzondering.

Bovendien toohello hierboven, zorg ervoor dat u hebt toegevoegd aan uw Google-account tooyour die emulator onder **instellingen** > **Accounts**. Anders wordt uw tooregister pogingen bij GCM kan leiden tot Hallo **verificatie\_mislukt** uitzondering.

#### <a name="running-hello-application"></a>Uitvoeren van de toepassing hello
1. Hallo-app uitvoeren en u ziet dat Hallo registratie-ID voor een succesvolle registratie wordt gerapporteerd.
   
      ![Testen op Android - Kanaalregistratie][18]
2. Voer een melding bericht toobe tooall Android-apparaten die zijn geregistreerd met de hub Hallo verzonden.
   
      ![Testen op Android - een bericht verzenden][19]

3. Druk op **Melding verzenden**. Alle apparaten waarop Hallo app actief wordt weergegeven een `AlertDialog` -exemplaar met de Hallo pushmelding. Apparaten die geen Hallo app wordt uitgevoerd, maar die eerder zijn geregistreerd voor pushmeldingen ontvangt een melding in Hallo Android Notification Manager. Die kunnen worden bekeken door omlaag te vegen vanuit de linkerbovenhoek Hallo.
   
      ![Testen op Android - meldingen][21]

## <a name="next-steps"></a>Volgende stappen
Hallo wordt aangeraden [Notification Hubs gebruiken toopush meldingen toousers] zelfstudie Hallo volgende stap. Hierin ziet u hoe toosend meldingen vanuit een ASP.NET-back-end met tags voor specifieke gebruikers tootarget.

Als u uw gebruikers op belangengroepen toosegment wilt, bekijk Hallo [Notification Hubs gebruiken toosend belangrijk nieuws] zelfstudie.

toolearn meer algemene informatie over Notification Hubs, Zie onze [richtlijnen voor Notification Hubs].

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
