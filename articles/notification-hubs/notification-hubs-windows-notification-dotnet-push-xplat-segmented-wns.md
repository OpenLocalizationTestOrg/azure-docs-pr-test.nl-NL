---
title: aaaUse Notification Hubs toosend belangrijk nieuws (Universal Windows)
description: Azure Notification Hubs gebruiken met labels in Hallo registratie toosend nieuws tooa universele Windows-app op te splitsen.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f102d286d2c7bd387fcfa2c7eab2ba31a0298517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="908c9-103">Gebruik Notification Hubs toosend belangrijk nieuws</span><span class="sxs-lookup"><span data-stu-id="908c9-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="908c9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="908c9-104">Overview</span></span>
<span data-ttu-id="908c9-105">Dit onderwerp leest u hoe toouse Azure Notification Hubs toobroadcast laatste nieuws meldingen tooa Windows Store of app van Windows Phone 8.1 (zonder Silverlight).</span><span class="sxs-lookup"><span data-stu-id="908c9-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="908c9-106">Als u voor Windows Phone 8.1 Silverlight ontwikkelt, raadpleegt u toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) versie.</span><span class="sxs-lookup"><span data-stu-id="908c9-106">If you are targeting Windows Phone 8.1 Silverlight, please refer toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="908c9-107">Als u klaar gaat u kunnen tooregister voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen.</span><span class="sxs-lookup"><span data-stu-id="908c9-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="908c9-108">Dit scenario is een algemene patroon voor veel apps waar meldingen hebt verzonden toobe toogroups van gebruikers die hebben dit eerder is gedeclareerd interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="908c9-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="908c9-109">Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in Hallo notification hub.</span><span class="sxs-lookup"><span data-stu-id="908c9-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="908c9-110">Wanneer meldingen worden verzonden tooa label, ontvangen alle apparaten die zijn geregistreerd voor de tag Hallo Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="908c9-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="908c9-111">Omdat tags gewoon tekenreeksen zijn, hebben geen toobe vooraf is ingericht.</span><span class="sxs-lookup"><span data-stu-id="908c9-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="908c9-112">Raadpleeg te voor meer informatie over tags[Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="908c9-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="908c9-113">Windows Store en Windows Phone-projecten versie 8.1 en lager worden niet ondersteund in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="908c9-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="908c9-114">Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="908c9-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="908c9-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="908c9-115">Prerequisites</span></span>
<span data-ttu-id="908c9-116">In dit onderwerp is gebaseerd op Hallo-app die u hebt gemaakt in [aan de slag met Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="908c9-116">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="908c9-117">Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="908c9-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="908c9-118">Categorie selectie toohello app toevoegen</span><span class="sxs-lookup"><span data-stu-id="908c9-118">Add category selection toohello app</span></span>
<span data-ttu-id="908c9-119">de eerste stap Hallo is tooadd Hallo UI-elementen tooyour bestaande hoofdpagina waarmee Hallo gebruiker tooselect categorieën tooregister.</span><span class="sxs-lookup"><span data-stu-id="908c9-119">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="908c9-120">Hallo categorieën geselecteerd door een gebruiker zijn op Hallo apparaat opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="908c9-120">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="908c9-121">Wanneer Hallo-app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met Hallo geselecteerd categorieën gemaakt als labels.</span><span class="sxs-lookup"><span data-stu-id="908c9-121">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="908c9-122">Open Hallo MainPage.xaml projectbestand vervolgens kopiëren Hallo na de code in Hallo **raster** element:</span><span class="sxs-lookup"><span data-stu-id="908c9-122">Open hello MainPage.xaml project file, then copy hello following code in hello **Grid** element:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>
2. <span data-ttu-id="908c9-123">Klik met de rechtermuisknop op Hallo **gedeelde** project en voeg een nieuwe klasse met de naam **meldingen**, Hallo toevoegen **openbare** aanpassingsfunctie toohello definitie klasse, voeg dan Hallo na **met** instructies toohello nieuwe codebestand:</span><span class="sxs-lookup"><span data-stu-id="908c9-123">Right click hello **Shared** project and add a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="908c9-124">Kopiëren Hallo volgende code in nieuwe Hallo **meldingen** klasse:</span><span class="sxs-lookup"><span data-stu-id="908c9-124">Copy hello following code into hello new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            return await SubscribeToCategories(categories);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
            return categories != null ? categories.Split(','): new string[0];
        }
   
        public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    <span data-ttu-id="908c9-125">Hallo lokale opslag toostore Hallo categorieën van nieuws dat dit apparaat tooreceive heeft maakt gebruik van deze klasse.</span><span class="sxs-lookup"><span data-stu-id="908c9-125">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="908c9-126">Houd er rekening mee dat in plaats van aanroepen Hallo *RegisterNativeAsync* methode we noemen *RegisterTemplateAsync* tooregister voor Hallo categorieën met behulp van de registratie van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="908c9-126">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync* tooregister for hello categories using a template registration.</span></span> 
   
    <span data-ttu-id="908c9-127">We bieden ook een naam voor Hallo-sjabloon ('simpleWNSTemplateExample'), omdat er tooregister meer dan één sjabloon (bijvoorbeeld één voor de pop-upmeldingen) en één voor tegels wilt mogelijk en tooname moeten ze in volgorde van toobe kunnen tooupdate of verwijder ze.</span><span class="sxs-lookup"><span data-stu-id="908c9-127">We also provide a name for hello template ("simpleWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="908c9-128">Houd er rekening mee dat als een apparaat meerdere sjablonen met Hallo dezelfde tag registreert, een binnenkomend bericht als doel dat label zal resulteren in meerdere meldingen toohello-apparaat (één voor elke sjabloon) geleverd.</span><span class="sxs-lookup"><span data-stu-id="908c9-128">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="908c9-129">Dit gedrag is handig wanneer hello hetzelfde logische bericht tooresult in meerdere visual meldingen heeft, bijvoorbeeld zowel een badge en een pop-up wordt weergegeven in een Windows Store-toepassing.</span><span class="sxs-lookup"><span data-stu-id="908c9-129">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="908c9-130">Zie voor meer informatie over sjablonen [sjablonen](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="908c9-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="908c9-131">Hallo projectbestand App.XAML.cs, voeg Hallo eigenschap toohello na **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="908c9-131">In hello App.xaml.cs project file, add hello following property toohello **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="908c9-132">Deze eigenschap is gebruikte toocreate en toegang tot een **meldingen** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="908c9-132">This property is used toocreate and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="908c9-133">Vervang in Hallo bovenstaande code Hallo `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultListenSharedAccessSignature* die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="908c9-133">In hello above code, replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="908c9-134">Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u alleen Hallo-sleutel voor listen toegang distribueren met uw clientapp.</span><span class="sxs-lookup"><span data-stu-id="908c9-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="908c9-135">Luisteren toegang kunnen die uw app tooregister voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden.</span><span class="sxs-lookup"><span data-stu-id="908c9-135">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="908c9-136">Hallo volledige toegang tot de sleutel wordt gebruikt in een beveiligde back endservice voor het verzenden van meldingen en bestaande registraties wijzigen.</span><span class="sxs-lookup"><span data-stu-id="908c9-136">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="908c9-137">Voeg in uw MainPage.xaml.cs Hallo volgt regel:</span><span class="sxs-lookup"><span data-stu-id="908c9-137">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="908c9-138">Voeg Hallo volgende methode in Hallo MainPage.xaml.cs project-bestand:</span><span class="sxs-lookup"><span data-stu-id="908c9-138">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
            var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
   
    <span data-ttu-id="908c9-139">Deze methode maakt u een lijst met categorieën en maakt gebruik van Hallo **meldingen** toostore Hallo lijst in de lokale opslag Hallo klasse en bijbehorende labels Hallo registreren voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="908c9-139">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="908c9-140">Wanneer categorieën worden gewijzigd, wordt met de nieuwe categorieën Hallo Hallo registratie nagemaakt.</span><span class="sxs-lookup"><span data-stu-id="908c9-140">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="908c9-141">Uw app is nu kunnen toostore een aantal categorieën in lokale opslag op Hallo-apparaat en registreren bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën.</span><span class="sxs-lookup"><span data-stu-id="908c9-141">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="908c9-142">Registreren voor meldingen</span><span class="sxs-lookup"><span data-stu-id="908c9-142">Register for notifications</span></span>
<span data-ttu-id="908c9-143">Deze stappen registreren bij Hallo notification hub bij het opstarten met behulp van Hallo categorieën die zijn opgeslagen in de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="908c9-143">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="908c9-144">Omdat Hallo kanaal-URI toegewezen door Hallo Windows Notification Service (WNS) op elk gewenst moment wijzigen kunt, moet u registreren voor meldingen vaak tooavoid melding fouten.</span><span class="sxs-lookup"><span data-stu-id="908c9-144">Because hello channel URI assigned by hello Windows Notification Service (WNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="908c9-145">In dit voorbeeld registreert voor melding telkens wanneer die Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="908c9-145">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="908c9-146">Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie toopreserve bandbreedte als minder dan een dag is verstreken sinds de vorige registratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="908c9-146">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="908c9-147">Open Hallo App.xaml.cs bestands- en update Hallo **InitNotificationsAsync** methode toouse hello `notifications` klasse toosubscribe op basis van categorieën.</span><span class="sxs-lookup"><span data-stu-id="908c9-147">Open hello App.xaml.cs file and update hello **InitNotificationsAsync** method toouse hello `notifications` class toosubscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="908c9-148">Dit zorgt ervoor dat telkens wanneer Hallo-app wordt gestart het Hallo-categorieën opgehaald uit de lokale opslag en een registratie voor deze categorieën vraagt.</span><span class="sxs-lookup"><span data-stu-id="908c9-148">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="908c9-149">Hallo **InitNotificationsAsync** methode is gemaakt als onderdeel van Hallo [aan de slag met Notification Hubs] [ get-started] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="908c9-149">hello **InitNotificationsAsync** method was created as part of hello [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="908c9-150">Voeg Hallo code toohello te volgen in Hallo MainPage.xaml.cs project-bestand *OnNavigatedTo* methode:</span><span class="sxs-lookup"><span data-stu-id="908c9-150">In hello MainPage.xaml.cs project file, add hello following code toohello *OnNavigatedTo* method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldToggle.IsOn = true;
            if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
            if (categories.Contains("Business")) BusinessToggle.IsOn = true;
            if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
            if (categories.Contains("Science")) ScienceToggle.IsOn = true;
            if (categories.Contains("Sports")) SportsToggle.IsOn = true;
        }
   
    <span data-ttu-id="908c9-151">Deze updates Hallo hoofdpagina op basis van Hallo status van de eerder opgeslagen categorieën.</span><span class="sxs-lookup"><span data-stu-id="908c9-151">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="908c9-152">Hallo-app is nu voltooid en kan een set van categorieën worden opgeslagen in Hallo apparaat gebruikt voor lokale opslag tooregister bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën.</span><span class="sxs-lookup"><span data-stu-id="908c9-152">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="908c9-153">Vervolgens definiëren we een back-end die categorie meldingen toothis app kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="908c9-153">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="908c9-154">Verzenden van meldingen met tags</span><span class="sxs-lookup"><span data-stu-id="908c9-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="908c9-155">Hallo-app uitvoeren en meldingen genereren</span><span class="sxs-lookup"><span data-stu-id="908c9-155">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="908c9-156">Druk op F5 toocompile in Visual Studio en Hallo-app te starten.</span><span class="sxs-lookup"><span data-stu-id="908c9-156">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="908c9-157">Opmerking die Hallo app die gebruikersinterface een set biedt-of kunt u Hallo categorieën toosubscribe te kiezen.</span><span class="sxs-lookup"><span data-stu-id="908c9-157">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="908c9-158">Een of meer categorieën Schakelknoppen inschakelen en klik vervolgens op **abonneren**.</span><span class="sxs-lookup"><span data-stu-id="908c9-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="908c9-159">Hallo-app geselecteerd Hallo categorieën converteert naar labels en vraagt een nieuwe apparaatregistratie voor Hallo geselecteerd tags van Hallo notification hub.</span><span class="sxs-lookup"><span data-stu-id="908c9-159">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="908c9-160">Hallo geregistreerde categorieën worden geretourneerd en in een dialoogvenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="908c9-160">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="908c9-161">Een nieuwe melding verzenden vanuit back-end Hallo in een van de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="908c9-161">Send a new notification from hello backend in one of hello following ways:</span></span>
   
   * <span data-ttu-id="908c9-162">**Console-app:** Hallo console-app te starten.</span><span class="sxs-lookup"><span data-stu-id="908c9-162">**Console app:** start hello console app.</span></span>
   * <span data-ttu-id="908c9-163">**Java/PHP:** uw app/script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="908c9-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="908c9-164">Meldingen voor Hallo geselecteerd categorieën weergegeven als pop-upmeldingen.</span><span class="sxs-lookup"><span data-stu-id="908c9-164">Notifications for hello selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="908c9-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="908c9-165">Next steps</span></span>
<span data-ttu-id="908c9-166">In deze zelfstudie hebt u geleerd hoe toobroadcast belangrijk nieuws per categorie.</span><span class="sxs-lookup"><span data-stu-id="908c9-166">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="908c9-167">Houd rekening met een van de volgende zelfstudies waarin andere geavanceerde scenario's voor Notification Hubs Markeer Hallo voltooien:</span><span class="sxs-lookup"><span data-stu-id="908c9-167">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="908c9-168">[Gebruik Notification Hubs toobroadcast gelokaliseerd belangrijk nieuws]</span><span class="sxs-lookup"><span data-stu-id="908c9-168">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="908c9-169">Meer informatie over hoe tooexpand Hallo nieuws app tooenable verzenden op te splitsen meldingen gelokaliseerd.</span><span class="sxs-lookup"><span data-stu-id="908c9-169">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[Gebruik Notification Hubs toobroadcast gelokaliseerd belangrijk nieuws]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
