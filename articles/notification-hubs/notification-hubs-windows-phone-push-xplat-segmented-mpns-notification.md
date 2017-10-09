---
title: aaaUse Notification Hubs toosend belangrijk nieuws (Windows Phone)
description: Gebruik Azure Notification Hubs toouse tag in registraties toosend nieuws tooa Windows Phone-app op te splitsen.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 3519a8701105f88198afe288e59e9204420234db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="1413f-103">Gebruik Notification Hubs toosend belangrijk nieuws</span><span class="sxs-lookup"><span data-stu-id="1413f-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="1413f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1413f-104">Overview</span></span>
<span data-ttu-id="1413f-105">Dit onderwerp leest u hoe toouse Azure Notification Hubs toobroadcast belangrijk nieuws meldingen tooa Windows Phone 8.0/8.1 Silverlight-app.</span><span class="sxs-lookup"><span data-stu-id="1413f-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="1413f-106">Als u voor Windows Store of Windows Phone 8.1-app ontwikkelt, raadpleegt u tootoohello [universele Windows-](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) versie.</span><span class="sxs-lookup"><span data-stu-id="1413f-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="1413f-107">Als u klaar gaat u kunnen tooregister voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen.</span><span class="sxs-lookup"><span data-stu-id="1413f-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="1413f-108">Dit scenario is een algemene patroon voor veel apps waar meldingen hebt verzonden toobe toogroups van gebruikers die interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort eerder is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="1413f-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="1413f-109">Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in Hallo notification hub.</span><span class="sxs-lookup"><span data-stu-id="1413f-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="1413f-110">Wanneer meldingen worden verzonden tooa label, ontvangen alle apparaten die zijn geregistreerd voor de tag Hallo Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="1413f-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="1413f-111">Omdat tags gewoon tekenreeksen zijn, hebben geen toobe vooraf is ingericht.</span><span class="sxs-lookup"><span data-stu-id="1413f-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="1413f-112">Raadpleeg te voor meer informatie over tags[Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="1413f-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1413f-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1413f-113">Prerequisites</span></span>
<span data-ttu-id="1413f-114">In dit onderwerp is gebaseerd op Hallo-app die u hebt gemaakt in [aan de slag met Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1413f-114">This topic builds on hello app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="1413f-115">Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1413f-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="1413f-116">Categorie selectie toohello app toevoegen</span><span class="sxs-lookup"><span data-stu-id="1413f-116">Add category selection toohello app</span></span>
<span data-ttu-id="1413f-117">de eerste stap Hallo is tooadd Hallo UI-elementen tooyour bestaande hoofdpagina waarmee Hallo gebruiker tooselect categorieën tooregister.</span><span class="sxs-lookup"><span data-stu-id="1413f-117">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="1413f-118">Hallo categorieën geselecteerd door een gebruiker zijn op Hallo apparaat opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1413f-118">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="1413f-119">Wanneer Hallo-app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met Hallo geselecteerd categorieën gemaakt als labels.</span><span class="sxs-lookup"><span data-stu-id="1413f-119">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="1413f-120">Hallo MainPage.xaml projectbestand openen en vervolgens vervangen Hallo **raster** elementen met de naam `TitlePanel` en `ContentPanel` Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="1413f-120">Open hello MainPage.xaml project file, then replace hello **Grid** elements named `TitlePanel` and `ContentPanel` with hello following code:</span></span>
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. <span data-ttu-id="1413f-121">In Hallo-project maakt u een nieuwe klasse met de naam **meldingen**, Hallo toevoegen **openbare** aanpassingsfunctie toohello definitie klasse, voeg dan Hallo volgende **met** instructies nieuwe codebestand toohello:</span><span class="sxs-lookup"><span data-stu-id="1413f-121">In hello project, create a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="1413f-122">Kopiëren Hallo volgende code in nieuwe Hallo **meldingen** klasse:</span><span class="sxs-lookup"><span data-stu-id="1413f-122">Copy hello following code into hello new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task toocomplete registration in hello ChannelUriUpdated event handler
        private TaskCompletionSource<Registration> registrationTask;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
            return categories != null ? categories.Split(',') : new string[0];
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            var categoriesAsString = string.Join(",", categories);
            var settings = IsolatedStorageSettings.ApplicationSettings;
            if (!settings.Contains("categories"))
            {
                settings.Add("categories", categoriesAsString);
            }
            else
            {
                settings["categories"] = categoriesAsString;
            }
            settings.Save();
   
            return await SubscribeToCategories();
        }
   
        public async Task<Registration> SubscribeToCategories()
        {
            registrationTask = new TaskCompletionSource<Registration>();
   
            var channel = HttpNotificationChannel.Find("MyPushChannel");
   
            if (channel == null)
            {
                channel = new HttpNotificationChannel("MyPushChannel");
                channel.Open();
                channel.BindToShellToast();
                channel.ChannelUriUpdated += channel_ChannelUriUpdated;
   
                // This is optional, used tooreceive notifications while hello app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete hello registrationTask here.  
            // If it is null, hello registrationTask will be completed in hello ChannelUriUpdated event handler.
            if (channel.ChannelUri != null)
            {
                await RegisterTemplate(channel.ChannelUri);
            }
   
            return await registrationTask.Task;
        }
   
        async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            await RegisterTemplate(e.ChannelUri);
        }
   
        async Task<Registration> RegisterTemplate(Uri channelUri)
        {
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // hello stored categories tags are passed with hello template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used tooreceive notifications while hello app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out hello information that was part of hello message.
            foreach (string key in e.Collection.Keys)
            {
                message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);
   
                if (string.Compare(
                    key,
                    "wp:Param",
                    System.Globalization.CultureInfo.InvariantCulture,
                    System.Globalization.CompareOptions.IgnoreCase) == 0)
                {
                    relativeUri = e.Collection[key];
                }
            }
   
            // Display a dialog of all hello fields in hello toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="1413f-123">Hallo geïsoleerde opslag toostore Hallo categorieën van nieuws dat dit apparaat tooreceive is maakt gebruik van deze klasse.</span><span class="sxs-lookup"><span data-stu-id="1413f-123">This class uses hello isolated storage toostore hello categories of news that this device is tooreceive.</span></span> <span data-ttu-id="1413f-124">Het bevat ook methoden tooregister voor deze categorieën met behulp van een [sjabloon](notification-hubs-templates-cross-platform-push-messages.md) registratie.</span><span class="sxs-lookup"><span data-stu-id="1413f-124">It also contains methods tooregister for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="1413f-125">Hallo projectbestand App.XAML.cs, voeg Hallo eigenschap toohello na **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="1413f-125">In hello App.xaml.cs project file, add hello following property toohello **App** class.</span></span> <span data-ttu-id="1413f-126">Vervang Hallo `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultListenSharedAccessSignature* die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="1413f-126">Replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="1413f-127">Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u alleen Hallo-sleutel voor listen toegang distribueren met uw clientapp.</span><span class="sxs-lookup"><span data-stu-id="1413f-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="1413f-128">Luisteren toegang kunnen die uw app tooregister voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden.</span><span class="sxs-lookup"><span data-stu-id="1413f-128">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="1413f-129">Hallo volledige toegang tot de sleutel wordt gebruikt in een beveiligde back endservice voor het verzenden van meldingen en bestaande registraties wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1413f-129">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="1413f-130">Voeg in uw MainPage.xaml.cs Hallo volgt regel:</span><span class="sxs-lookup"><span data-stu-id="1413f-130">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="1413f-131">Voeg Hallo volgende methode in Hallo MainPage.xaml.cs project-bestand:</span><span class="sxs-lookup"><span data-stu-id="1413f-131">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
          var categories = new HashSet<string>();
          if (WorldCheckBox.IsChecked == true) categories.Add("World");
          if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
          if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
          if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
          if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
          if (SportsCheckBox.IsChecked == true) categories.Add("Sports");
   
          var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
          MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
             result.RegistrationId);
        }
   
    <span data-ttu-id="1413f-132">Deze methode maakt u een lijst met categorieën en maakt gebruik van Hallo **meldingen** toostore Hallo lijst in de lokale opslag Hallo klasse en bijbehorende labels Hallo registreren voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="1413f-132">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="1413f-133">Wanneer categorieën worden gewijzigd, wordt met de nieuwe categorieën Hallo Hallo registratie nagemaakt.</span><span class="sxs-lookup"><span data-stu-id="1413f-133">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="1413f-134">Uw app is nu kunnen toostore een aantal categorieën in lokale opslag op Hallo-apparaat en registreren bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën.</span><span class="sxs-lookup"><span data-stu-id="1413f-134">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="1413f-135">Registreren voor meldingen</span><span class="sxs-lookup"><span data-stu-id="1413f-135">Register for notifications</span></span>
<span data-ttu-id="1413f-136">Deze stappen registreren bij Hallo notification hub bij het opstarten met behulp van Hallo categorieën die zijn opgeslagen in de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="1413f-136">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="1413f-137">Omdat Hallo kanaal-URI toegewezen door Hallo Microsoft Push Notification Service (MPNS) op elk gewenst moment wijzigen kunt, moet u registreren voor meldingen vaak tooavoid melding fouten.</span><span class="sxs-lookup"><span data-stu-id="1413f-137">Because hello channel URI assigned by hello Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="1413f-138">In dit voorbeeld registreert voor meldingen telkens wanneer die Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="1413f-138">This example registers for notifications every time that hello app starts.</span></span> <span data-ttu-id="1413f-139">Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie toopreserve bandbreedte als minder dan een dag is verstreken sinds de vorige registratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="1413f-139">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="1413f-140">Hallo App.xaml.cs bestand openen en het toevoegen van Hallo **asynchrone** aanpassingsfunctie te**Application_Launching** methode en vervang Hallo Notification Hubs registratiecode die u hebt toegevoegd in [aan de slag met Notification Hubs] Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="1413f-140">Open hello App.xaml.cs file and add hello **async** modifier too**Application_Launching** method and replace hello Notification Hubs registration code that you added in [Get started with Notification Hubs] with hello following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="1413f-141">Dit zorgt ervoor dat telkens wanneer Hallo-app wordt gestart het Hallo-categorieën opgehaald uit de lokale opslag en een registratie voor deze categorieën vraagt.</span><span class="sxs-lookup"><span data-stu-id="1413f-141">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="1413f-142">In Hallo MainPage.xaml.cs project-bestand toevoegen na de code die wordt geïmplementeerd Hallo Hallo **OnNavigatedTo** methode:</span><span class="sxs-lookup"><span data-stu-id="1413f-142">In hello MainPage.xaml.cs project file, add hello following code that implements hello **OnNavigatedTo** method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
            if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
            if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
            if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
            if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
            if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
        }
   
    <span data-ttu-id="1413f-143">Deze updates Hallo hoofdpagina op basis van Hallo status van de eerder opgeslagen categorieën.</span><span class="sxs-lookup"><span data-stu-id="1413f-143">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="1413f-144">Hallo-app is nu voltooid en kan een set van categorieën worden opgeslagen in Hallo apparaat gebruikt voor lokale opslag tooregister bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën.</span><span class="sxs-lookup"><span data-stu-id="1413f-144">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="1413f-145">Vervolgens definiëren we een back-end die categorie meldingen toothis app kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="1413f-145">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="1413f-146">Verzenden van meldingen met tags</span><span class="sxs-lookup"><span data-stu-id="1413f-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="1413f-147">Hallo-app uitvoeren en meldingen genereren</span><span class="sxs-lookup"><span data-stu-id="1413f-147">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="1413f-148">Druk op F5 toocompile in Visual Studio en Hallo-app te starten.</span><span class="sxs-lookup"><span data-stu-id="1413f-148">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="1413f-149">Opmerking die Hallo app die gebruikersinterface een set biedt-of kunt u Hallo categorieën toosubscribe te kiezen.</span><span class="sxs-lookup"><span data-stu-id="1413f-149">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="1413f-150">Een of meer categorieën Schakelknoppen inschakelen en klik vervolgens op **abonneren**.</span><span class="sxs-lookup"><span data-stu-id="1413f-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="1413f-151">Hallo-app geselecteerd Hallo categorieën converteert naar labels en vraagt een nieuwe apparaatregistratie voor Hallo geselecteerd tags van Hallo notification hub.</span><span class="sxs-lookup"><span data-stu-id="1413f-151">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="1413f-152">Hallo geregistreerde categorieën worden geretourneerd en in een dialoogvenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1413f-152">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="1413f-153">Voer na de ontvangst van een bevestiging dat uw categorieën abonnement voltooid zijn, Hallo console app toosend meldingen voor elke categorieën.</span><span class="sxs-lookup"><span data-stu-id="1413f-153">After receiving a confirmation that your categories were subscription completed, run hello console app toosend notifications for each categories.</span></span> <span data-ttu-id="1413f-154">Controleer of er alleen een melding voor Hallo categorieën die u bent geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="1413f-154">Verify you only receive a notification for hello categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="1413f-155">U kunt in dit onderwerp hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="1413f-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how toobroadcast breaking news by category. Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs toobroadcast localized breaking news]

    Learn how tooexpand hello breaking news app tooenable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how toopush notifications toospecific authenticated users. This is a good solution for sending notifications only toospecific users.
-->

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[aan de slag met Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/
[Use Notification Hubs toobroadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Phone]: ??

