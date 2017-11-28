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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="43b36-103">Gebruik Notification Hubs toosend belangrijk nieuws</span><span class="sxs-lookup"><span data-stu-id="43b36-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="43b36-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="43b36-104">Overview</span></span>
<span data-ttu-id="43b36-105">Dit onderwerp leest u hoe toouse Azure Notification Hubs toobroadcast belangrijk nieuws meldingen tooan Android-app.</span><span class="sxs-lookup"><span data-stu-id="43b36-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan Android app.</span></span> <span data-ttu-id="43b36-106">Als u klaar gaat u kunnen tooregister voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen.</span><span class="sxs-lookup"><span data-stu-id="43b36-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="43b36-107">Dit scenario is een algemene patroon voor veel apps waar meldingen hebt verzonden toobe toogroups van gebruikers die interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort eerder is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="43b36-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="43b36-108">Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in Hallo notification hub.</span><span class="sxs-lookup"><span data-stu-id="43b36-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="43b36-109">Wanneer meldingen worden verzonden tooa label, ontvangen alle apparaten die zijn geregistreerd voor de tag Hallo Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="43b36-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="43b36-110">Omdat tags gewoon tekenreeksen zijn, hebben geen toobe vooraf is ingericht.</span><span class="sxs-lookup"><span data-stu-id="43b36-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="43b36-111">Raadpleeg te voor meer informatie over tags[Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="43b36-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43b36-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="43b36-112">Prerequisites</span></span>
<span data-ttu-id="43b36-113">In dit onderwerp is gebaseerd op Hallo-app die u hebt gemaakt in [aan de slag met Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="43b36-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="43b36-114">Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="43b36-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="43b36-115">Categorie selectie toohello app toevoegen</span><span class="sxs-lookup"><span data-stu-id="43b36-115">Add category selection toohello app</span></span>
<span data-ttu-id="43b36-116">de eerste stap Hallo is tooadd Hallo UI-elementen tooyour bestaande belangrijkste activiteit waarmee Hallo gebruiker tooselect categorieën tooregister.</span><span class="sxs-lookup"><span data-stu-id="43b36-116">hello first step is tooadd hello UI elements tooyour existing main activity that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="43b36-117">Hallo categorieën geselecteerd door een gebruiker zijn op Hallo apparaat opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="43b36-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="43b36-118">Wanneer Hallo-app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met Hallo geselecteerd categorieën gemaakt als labels.</span><span class="sxs-lookup"><span data-stu-id="43b36-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="43b36-119">Open het bestand res/layout/activity_main.xml en vervang Hallo inhoud met de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="43b36-119">Open your res/layout/activity_main.xml file, and substitute hello content with hello following:</span></span>
   
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
2. <span data-ttu-id="43b36-120">Open uw bestand res/values/strings.xml en Hallo volgende regels toevoegen:</span><span class="sxs-lookup"><span data-stu-id="43b36-120">Open your res/values/strings.xml file and add hello following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="43b36-121">De grafische indeling main_activity.xml ziet er nu als volgt:</span><span class="sxs-lookup"><span data-stu-id="43b36-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="43b36-122">Maak nu een klasse **meldingen** in Hallo dezelfde pakket als uw **MainActivity** klasse.</span><span class="sxs-lookup"><span data-stu-id="43b36-122">Now create a class **Notifications** in hello same package as your **MainActivity** class.</span></span>
   
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
   
    <span data-ttu-id="43b36-123">Hallo lokale opslag toostore Hallo categorieën van nieuws dat dit apparaat tooreceive heeft maakt gebruik van deze klasse.</span><span class="sxs-lookup"><span data-stu-id="43b36-123">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="43b36-124">Het bevat ook methoden tooregister voor deze categorieën.</span><span class="sxs-lookup"><span data-stu-id="43b36-124">It also contains methods tooregister for these categories.</span></span>
4. <span data-ttu-id="43b36-125">In uw **MainActivity** klasse verwijdert u uw persoonlijke velden voor **NotificationHub** en **GoogleCloudMessaging**, en voeg een veld voor **meldingen**:</span><span class="sxs-lookup"><span data-stu-id="43b36-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="43b36-126">Klik op Hallo **onCreate** methode verwijderen Hallo initialisatie van Hallo **hub** veld en Hallo **registerWithNotificationHubs** methode.</span><span class="sxs-lookup"><span data-stu-id="43b36-126">Then, in hello **onCreate** method, remove hello initialization of hello **hub** field and hello **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="43b36-127">Voeg vervolgens de volgende regels die een exemplaar van Hallo initialiseren Hallo **meldingen** klasse.</span><span class="sxs-lookup"><span data-stu-id="43b36-127">Then add hello following lines which initialize an instance of hello **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="43b36-128">`HubName`en `HubListenConnectionString` al moet zijn ingesteld door hello `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultListenSharedAccessSignature* die u hebt verkregen oudere versies.</span><span class="sxs-lookup"><span data-stu-id="43b36-128">`HubName` and `HubListenConnectionString` should already be set with hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="43b36-129">Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u alleen Hallo-sleutel voor listen toegang distribueren met uw clientapp.</span><span class="sxs-lookup"><span data-stu-id="43b36-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="43b36-130">Luisteren toegang kunnen die uw app tooregister voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden.</span><span class="sxs-lookup"><span data-stu-id="43b36-130">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="43b36-131">Hallo volledige toegang tot de sleutel wordt gebruikt in een beveiligde back endservice voor het verzenden van meldingen en bestaande registraties wijzigen.</span><span class="sxs-lookup"><span data-stu-id="43b36-131">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="43b36-132">Vervolgens voegt u Hallo na importeert en `subscribe` methode toohandle Hallo abonneren knop klikt u op de gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="43b36-132">Then, add hello following imports and `subscribe` method toohandle hello subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="43b36-133">Deze methode maakt u een lijst met categorieën en maakt gebruik van Hallo **meldingen** toostore Hallo lijst in de lokale opslag Hallo klasse en bijbehorende labels Hallo registreren voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="43b36-133">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="43b36-134">Wanneer categorieën worden gewijzigd, wordt met de nieuwe categorieën Hallo Hallo registratie nagemaakt.</span><span class="sxs-lookup"><span data-stu-id="43b36-134">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="43b36-135">Uw app is nu kunnen toostore een aantal categorieën in lokale opslag op Hallo-apparaat en registreren bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën.</span><span class="sxs-lookup"><span data-stu-id="43b36-135">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="43b36-136">Registreren voor meldingen</span><span class="sxs-lookup"><span data-stu-id="43b36-136">Register for notifications</span></span>
<span data-ttu-id="43b36-137">Deze stappen registreren bij Hallo notification hub bij het opstarten met behulp van Hallo categorieën die zijn opgeslagen in de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="43b36-137">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="43b36-138">Omdat Hallo registrationId toegewezen door Google Cloud Messaging (GCM) op elk gewenst moment wijzigen kunt, moet u registreren voor meldingen vaak tooavoid melding fouten.</span><span class="sxs-lookup"><span data-stu-id="43b36-138">Because hello registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="43b36-139">In dit voorbeeld registreert voor melding telkens wanneer die Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="43b36-139">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="43b36-140">Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie toopreserve bandbreedte als minder dan een dag is verstreken sinds de vorige registratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="43b36-140">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="43b36-141">Toevoegen van de volgende code achter Hallo HALLO hallo **onCreate** methode in Hallo **MainActivity** klasse:</span><span class="sxs-lookup"><span data-stu-id="43b36-141">Add hello following code at hello end of hello **onCreate** method in hello **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="43b36-142">Dit zorgt ervoor dat telkens wanneer Hallo-app wordt gestart het Hallo-categorieën opgehaald uit de lokale opslag en een registratie voor deze categorieën vraagt.</span><span class="sxs-lookup"><span data-stu-id="43b36-142">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="43b36-143">Werk vervolgens Hallo `onStart()` methode Hallo `MainActivity` klasse als volgt:</span><span class="sxs-lookup"><span data-stu-id="43b36-143">Then update hello `onStart()` method of hello `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="43b36-144">@Overridevoid onStart() {beveiligd</span><span class="sxs-lookup"><span data-stu-id="43b36-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="43b36-145">}</span><span class="sxs-lookup"><span data-stu-id="43b36-145">}</span></span>
   
    <span data-ttu-id="43b36-146">Hiermee wordt Hallo belangrijkste activiteit op basis van status van de eerder opgeslagen categorieën Hallo bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="43b36-146">This updates hello main activity based on hello status of previously saved categories.</span></span>

<span data-ttu-id="43b36-147">Hallo-app is nu voltooid en kan een set van categorieën worden opgeslagen in Hallo apparaat gebruikt voor lokale opslag tooregister bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën.</span><span class="sxs-lookup"><span data-stu-id="43b36-147">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="43b36-148">Vervolgens definiëren we een back-end die categorie meldingen toothis app kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="43b36-148">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="43b36-149">Verzenden van meldingen met tags</span><span class="sxs-lookup"><span data-stu-id="43b36-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="43b36-150">Hallo-app uitvoeren en meldingen genereren</span><span class="sxs-lookup"><span data-stu-id="43b36-150">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="43b36-151">In Android Studio Hallo app bouwen en start deze op een apparaat of emulator.</span><span class="sxs-lookup"><span data-stu-id="43b36-151">In Android Studio, build hello app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="43b36-152">Opmerking die Hallo app die gebruikersinterface een set biedt-of kunt u Hallo categorieën toosubscribe te kiezen.</span><span class="sxs-lookup"><span data-stu-id="43b36-152">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="43b36-153">Een of meer categorieën Schakelknoppen inschakelen en klik vervolgens op **abonneren**.</span><span class="sxs-lookup"><span data-stu-id="43b36-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="43b36-154">Hallo-app geselecteerd Hallo categorieën converteert naar labels en vraagt een nieuwe apparaatregistratie voor Hallo geselecteerd tags van Hallo notification hub.</span><span class="sxs-lookup"><span data-stu-id="43b36-154">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="43b36-155">Hallo worden geregistreerde categorieën geretourneerd en weergegeven in een pop-upmelding.</span><span class="sxs-lookup"><span data-stu-id="43b36-155">hello registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="43b36-156">Een nieuwe melding verzenden door te voeren Hallo .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="43b36-156">Send a new notification by running hello .NET Console app.</span></span>  <span data-ttu-id="43b36-157">U kunt ook met tags Sjabloonmeldingen Hallo foutopsporingstabblad van uw notification hub met in Hallo verzenden [klassieke Azure-Portal].</span><span class="sxs-lookup"><span data-stu-id="43b36-157">Alternatively, you can send tagged template notifications using hello debug tab of your notification hub in hello [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="43b36-158">Meldingen voor Hallo geselecteerd categorieën weergegeven als pop-upmeldingen.</span><span class="sxs-lookup"><span data-stu-id="43b36-158">Notifications for hello selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43b36-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43b36-159">Next steps</span></span>
<span data-ttu-id="43b36-160">In deze zelfstudie hebt u geleerd hoe toobroadcast belangrijk nieuws per categorie.</span><span class="sxs-lookup"><span data-stu-id="43b36-160">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="43b36-161">Houd rekening met een van de volgende zelfstudies waarin andere geavanceerde scenario's voor Notification Hubs Markeer Hallo voltooien:</span><span class="sxs-lookup"><span data-stu-id="43b36-161">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="43b36-162">[Gebruik Notification Hubs toobroadcast gelokaliseerd belangrijk nieuws]</span><span class="sxs-lookup"><span data-stu-id="43b36-162">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="43b36-163">Meer informatie over hoe tooexpand Hallo nieuws app tooenable verzenden op te splitsen meldingen gelokaliseerd.</span><span class="sxs-lookup"><span data-stu-id="43b36-163">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
