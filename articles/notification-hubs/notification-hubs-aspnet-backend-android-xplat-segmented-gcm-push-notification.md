---
title: Notification Hubs voor belangrijk nieuws zelfstudie - Android
description: Informatie over het gebruik van Azure Service Bus Notification Hubs voor belangrijk nieuws meldingen verzenden naar Android-apparaten.
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
ms.openlocfilehash: 76ec01c874fceedab7d76b2ef58e4b45b5489f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="7318b-103">Notification Hubs gebruiken om belangrijk nieuws te verzenden</span><span class="sxs-lookup"><span data-stu-id="7318b-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="7318b-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7318b-104">Overview</span></span>
<span data-ttu-id="7318b-105">Dit onderwerp leest u het gebruik van Azure Notification Hubs voor belangrijk nieuws meldingen naar een Android-app-broadcast.</span><span class="sxs-lookup"><span data-stu-id="7318b-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span></span> <span data-ttu-id="7318b-106">Als u klaar gaat u kunnen registreren voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7318b-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="7318b-107">Dit scenario is een algemene patroon voor veel apps waarbij moeten meldingen worden verzonden naar groepen gebruikers die interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort eerder is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="7318b-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="7318b-108">Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in de notification hub.</span><span class="sxs-lookup"><span data-stu-id="7318b-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="7318b-109">Wanneer u meldingen worden verzonden naar een label, ontvangen alle apparaten die zijn geregistreerd voor het label de melding.</span><span class="sxs-lookup"><span data-stu-id="7318b-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="7318b-110">Omdat tags gewoon tekenreeksen zijn, hoeven niet vooraf zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="7318b-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="7318b-111">Raadpleeg voor meer informatie over tags [Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="7318b-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7318b-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7318b-112">Prerequisites</span></span>
<span data-ttu-id="7318b-113">In dit onderwerp is gebaseerd op de app die u hebt gemaakt in [aan de slag met Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="7318b-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="7318b-114">Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="7318b-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="7318b-115">Categorieselectie toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="7318b-115">Add category selection to the app</span></span>
<span data-ttu-id="7318b-116">De eerste stap is het toevoegen van de UI-elementen naar uw bestaande belangrijkste activiteit waarmee de gebruiker kan de categorieën selecteren om te registreren.</span><span class="sxs-lookup"><span data-stu-id="7318b-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span></span> <span data-ttu-id="7318b-117">De categorieën die door een gebruiker is geselecteerd worden op het apparaat opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7318b-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="7318b-118">Wanneer de app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met de geselecteerde categorieën gemaakt als labels.</span><span class="sxs-lookup"><span data-stu-id="7318b-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="7318b-119">Open het bestand res/layout/activity_main.xml en vervang de inhoud met de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="7318b-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span></span>
   
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
2. <span data-ttu-id="7318b-120">Open uw bestand res/values/strings.xml en voeg de volgende regels:</span><span class="sxs-lookup"><span data-stu-id="7318b-120">Open your res/values/strings.xml file and add the following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="7318b-121">De grafische indeling main_activity.xml ziet er nu als volgt:</span><span class="sxs-lookup"><span data-stu-id="7318b-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="7318b-122">Maak nu een klasse **meldingen** in hetzelfde pakket als uw **MainActivity** klasse.</span><span class="sxs-lookup"><span data-stu-id="7318b-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span></span>
   
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
                            Log.e("MainActivity", "Failed to register - " + e.getMessage());
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
   
    <span data-ttu-id="7318b-123">Deze klasse maakt gebruik van de lokale opslag voor het opslaan van de categorieën van nieuws die dit apparaat heeft ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7318b-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="7318b-124">Het bevat ook methoden om te registreren voor deze categorieën.</span><span class="sxs-lookup"><span data-stu-id="7318b-124">It also contains methods to register for these categories.</span></span>
4. <span data-ttu-id="7318b-125">In uw **MainActivity** klasse verwijdert u uw persoonlijke velden voor **NotificationHub** en **GoogleCloudMessaging**, en voeg een veld voor **meldingen**:</span><span class="sxs-lookup"><span data-stu-id="7318b-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="7318b-126">Klik in de **onCreate** methode, verwijdert u de initialisatie van de **hub** veld en de **registerWithNotificationHubs** methode.</span><span class="sxs-lookup"><span data-stu-id="7318b-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="7318b-127">Voeg de volgende regels met initialiseren van een exemplaar van de **meldingen** klasse.</span><span class="sxs-lookup"><span data-stu-id="7318b-127">Then add the following lines which initialize an instance of the **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="7318b-128">`HubName`en `HubListenConnectionString` al moet zijn ingesteld met de `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen door de naam van uw notification hub en de verbindingsreeks voor *DefaultListenSharedAccessSignature* die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="7318b-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="7318b-129">Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u de sleutel voor listen toegang alleen distribueren met uw clientapp.</span><span class="sxs-lookup"><span data-stu-id="7318b-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="7318b-130">Luisteren toegang kunnen uw app registreren voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden.</span><span class="sxs-lookup"><span data-stu-id="7318b-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="7318b-131">De volledige toegang tot de sleutel wordt gebruikt in een beveiligde back-endservice voor het verzenden van meldingen en bestaande registraties wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7318b-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="7318b-132">Vervolgens voegt u de volgende import en `subscribe` methode voor het afhandelen van de knop aanmelden klikt u op de gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="7318b-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="7318b-133">Deze methode maakt u een lijst met categorieën en gebruikt de **meldingen** klasse voor het opslaan van de lijst in de lokale opslag en registreren van de bijbehorende tags voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="7318b-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="7318b-134">Wanneer categorieën worden gewijzigd, wordt de registratie opnieuw gemaakt met de nieuwe categorieën.</span><span class="sxs-lookup"><span data-stu-id="7318b-134">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="7318b-135">Uw app is nu in staat een aantal categorieën opslaan in lokale opslag op het apparaat en registreren bij de notification hub wanneer de gebruiker de selectie van categorieën wijzigt.</span><span class="sxs-lookup"><span data-stu-id="7318b-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="7318b-136">Registreren voor meldingen</span><span class="sxs-lookup"><span data-stu-id="7318b-136">Register for notifications</span></span>
<span data-ttu-id="7318b-137">Deze stappen registreren bij de notification hub bij het opstarten met behulp van de categorieën die zijn opgeslagen in de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="7318b-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="7318b-138">Omdat de registratie-id toegewezen door Google Cloud Messaging (GCM) op elk gewenst moment wijzigen kunt, kunt u moet registreren voor meldingen vaak ter voorkoming van fouten van de melding.</span><span class="sxs-lookup"><span data-stu-id="7318b-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="7318b-139">In dit voorbeeld registreert voor melding van elke keer dat de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7318b-139">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="7318b-140">Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie om bandbreedte te besparen als minder dan een dag is verstreken sinds de vorige registratie.</span><span class="sxs-lookup"><span data-stu-id="7318b-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="7318b-141">Voeg de volgende code toe aan het einde van de **onCreate** methode in de **MainActivity** klasse:</span><span class="sxs-lookup"><span data-stu-id="7318b-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="7318b-142">Dit zorgt ervoor dat telkens wanneer de app wordt gestart de categorieën van lokale opslag haalt en een registratie voor deze categorieën vraagt.</span><span class="sxs-lookup"><span data-stu-id="7318b-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="7318b-143">Werk vervolgens de `onStart()` methode van de `MainActivity` klasse als volgt:</span><span class="sxs-lookup"><span data-stu-id="7318b-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="7318b-144">@Overridevoid onStart() {beveiligd</span><span class="sxs-lookup"><span data-stu-id="7318b-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="7318b-145">}</span><span class="sxs-lookup"><span data-stu-id="7318b-145">}</span></span>
   
    <span data-ttu-id="7318b-146">Hiermee vernieuwt u de belangrijkste activiteit op basis van de status van de eerder opgeslagen categorieën.</span><span class="sxs-lookup"><span data-stu-id="7318b-146">This updates the main activity based on the status of previously saved categories.</span></span>

<span data-ttu-id="7318b-147">De app is nu voltooid en een set categorieën kunt opslaan in de lokale opslag gebruikt om u te registreren bij de notification hub wanneer de gebruiker de selectie van categorieën wijzigt van apparaat.</span><span class="sxs-lookup"><span data-stu-id="7318b-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="7318b-148">Vervolgens definiëren we een back-end die categorie meldingen naar deze app kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="7318b-148">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="7318b-149">Verzenden van meldingen met tags</span><span class="sxs-lookup"><span data-stu-id="7318b-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="7318b-150">Voer de app en meldingen genereren</span><span class="sxs-lookup"><span data-stu-id="7318b-150">Run the app and generate notifications</span></span>
1. <span data-ttu-id="7318b-151">In Android Studio bouwen van de app en start deze op een apparaat of emulator.</span><span class="sxs-lookup"><span data-stu-id="7318b-151">In Android Studio, build the app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="7318b-152">Opmerking dat de UI-app biedt een reeks Schakelknoppen waarmee u kunt kiezen uit de categorieën om u te abonneren op.</span><span class="sxs-lookup"><span data-stu-id="7318b-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="7318b-153">Een of meer categorieën Schakelknoppen inschakelen en klik vervolgens op **abonneren**.</span><span class="sxs-lookup"><span data-stu-id="7318b-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="7318b-154">De app de geselecteerde categorieën converteert naar labels en een nieuwe apparaatregistratie voor de geselecteerde codes aanvragen van de notification hub.</span><span class="sxs-lookup"><span data-stu-id="7318b-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="7318b-155">De geregistreerde categorieën worden geretourneerd en weergegeven in een pop-upmelding.</span><span class="sxs-lookup"><span data-stu-id="7318b-155">The registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="7318b-156">Een nieuwe melding verzenden door het uitvoeren van de .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="7318b-156">Send a new notification by running the .NET Console app.</span></span>  <span data-ttu-id="7318b-157">U kunt ook met tags Sjabloonmeldingen met behulp van het foutopsporingstabblad van uw notification hub in verzenden de [klassieke Azure-Portal].</span><span class="sxs-lookup"><span data-stu-id="7318b-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="7318b-158">Meldingen voor de geselecteerde categorieën weergegeven als pop-upmeldingen.</span><span class="sxs-lookup"><span data-stu-id="7318b-158">Notifications for the selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7318b-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7318b-159">Next steps</span></span>
<span data-ttu-id="7318b-160">In deze zelfstudie hebt u geleerd hoe belangrijk nieuws per categorie-broadcast.</span><span class="sxs-lookup"><span data-stu-id="7318b-160">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="7318b-161">Houd rekening met het voltooien van een van de volgende zelfstudies die andere geavanceerde scenario's voor Notification Hubs markeren:</span><span class="sxs-lookup"><span data-stu-id="7318b-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="7318b-162">[Notification Hubs gebruiken voor het uitzenden van gelokaliseerde belangrijk nieuws]</span><span class="sxs-lookup"><span data-stu-id="7318b-162">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="7318b-163">Informatie over het uitbreiden van de app belangrijk nieuws zodat gelokaliseerde verzenden van meldingen.</span><span class="sxs-lookup"><span data-stu-id="7318b-163">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
<span data-ttu-id="7318b-164">[Notification Hubs gebruiken voor het uitzenden van gelokaliseerde belangrijk nieuws]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="7318b-164">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="7318b-165">[klassieke Azure-Portal]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="7318b-165">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
