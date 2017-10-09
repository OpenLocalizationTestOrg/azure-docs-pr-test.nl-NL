1. In uw **app** project, open Hallo bestand `AndroidManifest.xml`. Vervang in Hallo-code in de volgende twee stappen hello,  *`**my_app_package**`*  met de naam van de Hallo van Hallo app-pakket voor uw project. Dit is de waarde Hallo Hallo `package` kenmerk Hallo `manifest` label.
2. Toevoegen van de volgende nieuwe machtigingen na Hallo bestaande Hallo `uses-permission` element:

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. Hallo code volgen na Hallo toevoegen `application` bij begincode:

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. Open Hallo bestand *ToDoActivity.java*, en voeg Hallo volgende importinstructie toe:

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. Hallo na persoonlijke variabele toohello klasse toevoegen. Vervang  *`<PROJECT_NUMBER>`*  met Hallo-projectnummer door Google tooyour-app in de voorgaande procedure Hallo toegewezen.

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. Hallo-definitie van wijzigen *MobileServiceClient* van **persoonlijke** te**openbare statische**, zodat er nu als volgt uitziet:

        public static MobileServiceClient mClient;
7. Een nieuwe klasse toohandle meldingen toevoegen. Open in Projectverkenner Hallo **src** > **belangrijkste** > **java** knooppunten en met de rechtermuisknop op Hallo pakket naam knooppunt. Klik op **nieuw**, en klik vervolgens op **Java-klasse**.
8. In **naam**, type `MyHandler`, en klik vervolgens op **OK**.

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. Vervang in Hallo MyHandler bestand, de klassendeclaratie Hallo met:

        public class MyHandler extends NotificationsHandler {
10. Toevoegen van de volgende importinstructies voor Hallo Hallo `MyHandler` klasse:

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. Naast deze toohello lid toevoegen `MyHandler` klasse:

        public static final int NOTIFICATION_ID = 1;
12. In Hallo `MyHandler` klasse, toevoegen van de volgende code toooverride Hallo Hallo **onRegistered** methode, waarmee u uw apparaat voor Hallo mobiele service notification hub geregistreerd.

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       }
13. In Hallo `MyHandler` klasse, toevoegen van de volgende code toooverride Hallo Hallo **onReceive** methode waardoor Hallo melding toodisplay wanneer het is ontvangen.

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       }
14. Terug in bestand TodoActivity.java hello, bijwerken Hallo **onCreate** methode Hallo *ToDoActivity* tooregister hello meldingsklasse handler klasse. Zorg ervoor dat tooadd deze code na Hallo *MobileServiceClient* wordt geïnstantieerd.

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    Uw app is nu bijgewerkte toosupport pushmeldingen.
