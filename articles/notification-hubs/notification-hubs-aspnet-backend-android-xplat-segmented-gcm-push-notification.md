---
title: aaaNotification Hubs op te splitsen nieuws zelfstudie - Android
description: Meer informatie over hoe toouse Azure Service Bus Notification Hubs toosend nieuws meldingen tooAndroid apparaten op te splitsen.
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Gebruik Notification Hubs toosend belangrijk nieuws
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Overzicht
Dit onderwerp leest u hoe toouse Azure Notification Hubs toobroadcast belangrijk nieuws meldingen tooan Android-app. Als u klaar gaat u kunnen tooregister voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen. Dit scenario is een algemene patroon voor veel apps waar meldingen hebt verzonden toobe toogroups van gebruikers die interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort eerder is gedeclareerd.

Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in Hallo notification hub. Wanneer meldingen worden verzonden tooa label, ontvangen alle apparaten die zijn geregistreerd voor de tag Hallo Hallo-bericht. Omdat tags gewoon tekenreeksen zijn, hebben geen toobe vooraf is ingericht. Raadpleeg te voor meer informatie over tags[Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Vereisten
In dit onderwerp is gebaseerd op Hallo-app die u hebt gemaakt in [aan de slag met Notification Hubs][get-started]. Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Categorie selectie toohello app toevoegen
de eerste stap Hallo is tooadd Hallo UI-elementen tooyour bestaande belangrijkste activiteit waarmee Hallo gebruiker tooselect categorieën tooregister. Hallo categorieën geselecteerd door een gebruiker zijn op Hallo apparaat opgeslagen. Wanneer Hallo-app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met Hallo geselecteerd categorieën gemaakt als labels.

1. Open het bestand res/layout/activity_main.xml en vervang Hallo inhoud met de volgende Hallo:
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. Open uw bestand res/values/strings.xml en Hallo volgende regels toevoegen:
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    De grafische indeling main_activity.xml ziet er nu als volgt:
   
    ![][A1]
3. Maak nu een klasse **meldingen** in Hallo dezelfde pakket als uw **MainActivity** klasse.
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    Hallo lokale opslag toostore Hallo categorieën van nieuws dat dit apparaat tooreceive heeft maakt gebruik van deze klasse. Het bevat ook methoden tooregister voor deze categorieën.
4. In uw **MainActivity** klasse verwijdert u uw persoonlijke velden voor **NotificationHub** en **GoogleCloudMessaging**, en voeg een veld voor **meldingen**:
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. Klik op Hallo **onCreate** methode verwijderen Hallo initialisatie van Hallo **hub** veld en Hallo **registerWithNotificationHubs** methode. Voeg vervolgens de volgende regels die een exemplaar van Hallo initialiseren Hallo **meldingen** klasse. 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    `HubName`en `HubListenConnectionString` al moet zijn ingesteld door hello `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultListenSharedAccessSignature* die u hebt verkregen oudere versies.

    > [AZURE.NOTE] Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u alleen Hallo-sleutel voor listen toegang distribueren met uw clientapp. Luisteren toegang kunnen die uw app tooregister voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden. Hallo volledige toegang tot de sleutel wordt gebruikt in een beveiligde back endservice voor het verzenden van meldingen en bestaande registraties wijzigen.


1. Vervolgens voegt u Hallo na importeert en `subscribe` methode toohandle Hallo abonneren knop klikt u op de gebeurtenis:
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    Deze methode maakt u een lijst met categorieën en maakt gebruik van Hallo **meldingen** toostore Hallo lijst in de lokale opslag Hallo klasse en bijbehorende labels Hallo registreren voor uw notification hub. Wanneer categorieën worden gewijzigd, wordt met de nieuwe categorieën Hallo Hallo registratie nagemaakt.

Uw app is nu kunnen toostore een aantal categorieën in lokale opslag op Hallo-apparaat en registreren bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën.

## <a name="register-for-notifications"></a>Registreren voor meldingen
Deze stappen registreren bij Hallo notification hub bij het opstarten met behulp van Hallo categorieën die zijn opgeslagen in de lokale opslag.

> [!NOTE]
> Omdat Hallo registrationId toegewezen door Google Cloud Messaging (GCM) op elk gewenst moment wijzigen kunt, moet u registreren voor meldingen vaak tooavoid melding fouten. In dit voorbeeld registreert voor melding telkens wanneer die Hallo-app wordt gestart. Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie toopreserve bandbreedte als minder dan een dag is verstreken sinds de vorige registratie Hallo.
> 
> 

1. Toevoegen van de volgende code achter Hallo HALLO hallo **onCreate** methode in Hallo **MainActivity** klasse:
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    Dit zorgt ervoor dat telkens wanneer Hallo-app wordt gestart het Hallo-categorieën opgehaald uit de lokale opslag en een registratie voor deze categorieën vraagt. 
2. Werk vervolgens Hallo `onStart()` methode Hallo `MainActivity` klasse als volgt:
   
    @Overridevoid onStart() {beveiligd
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    }
   
    Hiermee wordt Hallo belangrijkste activiteit op basis van status van de eerder opgeslagen categorieën Hallo bijgewerkt.

Hallo-app is nu voltooid en kan een set van categorieën worden opgeslagen in Hallo apparaat gebruikt voor lokale opslag tooregister bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën. Vervolgens definiëren we een back-end die categorie meldingen toothis app kunt verzenden.

## <a name="sending-tagged-notifications"></a>Verzenden van meldingen met tags
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Hallo-app uitvoeren en meldingen genereren
1. In Android Studio Hallo app bouwen en start deze op een apparaat of emulator.
   
    Opmerking die Hallo app die gebruikersinterface een set biedt-of kunt u Hallo categorieën toosubscribe te kiezen.
2. Een of meer categorieën Schakelknoppen inschakelen en klik vervolgens op **abonneren**.
   
    Hallo-app geselecteerd Hallo categorieën converteert naar labels en vraagt een nieuwe apparaatregistratie voor Hallo geselecteerd tags van Hallo notification hub. Hallo worden geregistreerde categorieën geretourneerd en weergegeven in een pop-upmelding.
3. Een nieuwe melding verzenden door te voeren Hallo .NET-consoletoepassing.  U kunt ook met tags Sjabloonmeldingen Hallo foutopsporingstabblad van uw notification hub met in Hallo verzenden [klassieke Azure-Portal].
   
    Meldingen voor Hallo geselecteerd categorieën weergegeven als pop-upmeldingen.

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toobroadcast belangrijk nieuws per categorie. Houd rekening met een van de volgende zelfstudies waarin andere geavanceerde scenario's voor Notification Hubs Markeer Hallo voltooien:

* [Gebruik Notification Hubs toobroadcast gelokaliseerd belangrijk nieuws]
  
    Meer informatie over hoe tooexpand Hallo nieuws app tooenable verzenden op te splitsen meldingen gelokaliseerd.

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[Gebruik Notification Hubs toobroadcast gelokaliseerd belangrijk nieuws]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[klassieke Azure-Portal]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
