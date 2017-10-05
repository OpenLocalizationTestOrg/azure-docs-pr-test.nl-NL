---
title: Notification Hubs gebruiken om belangrijk nieuws (Windows Phone) te verzenden
description: Gebruik Azure Notification Hubs tag in registraties belangrijk nieuws verzenden naar een Windows Phone-app.
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
ms.openlocfilehash: 3a6a69bf555c7267d3fbeb03ff6c03054991960f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="3c95e-103">Notification Hubs gebruiken om belangrijk nieuws te verzenden</span><span class="sxs-lookup"><span data-stu-id="3c95e-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="3c95e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3c95e-104">Overview</span></span>
<span data-ttu-id="3c95e-105">Dit onderwerp leest u het gebruik van Azure Notification Hubs voor belangrijk nieuws meldingen naar een Windows Phone 8.0/8.1 Silverlight-app-broadcast.</span><span class="sxs-lookup"><span data-stu-id="3c95e-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="3c95e-106">Als u voor Windows Store of Windows Phone 8.1-app ontwikkelt, Raadpleeg naar de [universele Windows-](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) versie.</span><span class="sxs-lookup"><span data-stu-id="3c95e-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer to to the [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="3c95e-107">Als u klaar gaat u kunnen registreren voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3c95e-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="3c95e-108">Dit scenario is een algemene patroon voor veel apps waarbij moeten meldingen worden verzonden naar groepen gebruikers die interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort eerder is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="3c95e-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="3c95e-109">Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in de notification hub.</span><span class="sxs-lookup"><span data-stu-id="3c95e-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="3c95e-110">Wanneer u meldingen worden verzonden naar een label, ontvangen alle apparaten die zijn geregistreerd voor het label de melding.</span><span class="sxs-lookup"><span data-stu-id="3c95e-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="3c95e-111">Omdat tags gewoon tekenreeksen zijn, hoeven niet vooraf zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="3c95e-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="3c95e-112">Raadpleeg voor meer informatie over tags [Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="3c95e-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c95e-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3c95e-113">Prerequisites</span></span>
<span data-ttu-id="3c95e-114">In dit onderwerp is gebaseerd op de app die u hebt gemaakt in [aan de slag met Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="3c95e-114">This topic builds on the app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="3c95e-115">Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="3c95e-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="3c95e-116">Categorieselectie toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="3c95e-116">Add category selection to the app</span></span>
<span data-ttu-id="3c95e-117">De eerste stap is het toevoegen van de UI-elementen naar uw bestaande hoofdpagina waarmee de gebruiker kan de categorieën selecteren om te registreren.</span><span class="sxs-lookup"><span data-stu-id="3c95e-117">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="3c95e-118">De categorieën die door een gebruiker is geselecteerd worden op het apparaat opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3c95e-118">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="3c95e-119">Wanneer de app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met de geselecteerde categorieën gemaakt als labels.</span><span class="sxs-lookup"><span data-stu-id="3c95e-119">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="3c95e-120">Open het projectbestand MainPage.xaml en vervang de **raster** elementen met de naam `TitlePanel` en `ContentPanel` met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="3c95e-120">Open the MainPage.xaml project file, then replace the **Grid** elements named `TitlePanel` and `ContentPanel` with the following code:</span></span>
   
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
2. <span data-ttu-id="3c95e-121">In het project, maakt u een nieuwe klasse met de naam **meldingen**, toevoegen de **openbare** aanpassingsfunctie naar de klassendefinitie, voegt u de volgende **met** instructies op het nieuwe codebestand :</span><span class="sxs-lookup"><span data-stu-id="3c95e-121">In the project, create a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="3c95e-122">Kopieer de volgende code naar de nieuwe **meldingen** klasse:</span><span class="sxs-lookup"><span data-stu-id="3c95e-122">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task to complete registration in the ChannelUriUpdated event handler
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
   
                // This is optional, used to receive notifications while the app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete the registrationTask here.  
            // If it is null, the registrationTask will be completed in the ChannelUriUpdated event handler.
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
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // The stored categories tags are passed with the template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used to receive notifications while the app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out the information that was part of the message.
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
   
            // Display a dialog of all the fields in the toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="3c95e-123">Deze klasse maakt gebruik van geïsoleerde opslag voor het opslaan van de categorieën van nieuws die dit apparaat moet ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3c95e-123">This class uses the isolated storage to store the categories of news that this device is to receive.</span></span> <span data-ttu-id="3c95e-124">Het bevat ook methoden om te registreren voor deze categorieën met behulp van een [sjabloon](notification-hubs-templates-cross-platform-push-messages.md) registratie.</span><span class="sxs-lookup"><span data-stu-id="3c95e-124">It also contains methods to register for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="3c95e-125">In het projectbestand App.xaml.cs de volgende eigenschap toevoegen aan de **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="3c95e-125">In the App.xaml.cs project file, add the following property to the **App** class.</span></span> <span data-ttu-id="3c95e-126">Vervang de `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen door de naam van uw notification hub en de verbindingsreeks voor *DefaultListenSharedAccessSignature* die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="3c95e-126">Replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="3c95e-127">Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u de sleutel voor listen toegang alleen distribueren met uw clientapp.</span><span class="sxs-lookup"><span data-stu-id="3c95e-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="3c95e-128">Luisteren toegang kunnen uw app registreren voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden.</span><span class="sxs-lookup"><span data-stu-id="3c95e-128">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="3c95e-129">De volledige toegang tot de sleutel wordt gebruikt in een beveiligde back-endservice voor het verzenden van meldingen en bestaande registraties wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3c95e-129">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="3c95e-130">Voeg de volgende regel in uw MainPage.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="3c95e-130">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="3c95e-131">In het projectbestand MainPage.xaml.cs voegt u de volgende methode toe:</span><span class="sxs-lookup"><span data-stu-id="3c95e-131">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
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
   
    <span data-ttu-id="3c95e-132">Deze methode maakt u een lijst met categorieën en gebruikt de **meldingen** klasse voor het opslaan van de lijst in de lokale opslag en registreren van de bijbehorende tags voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="3c95e-132">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="3c95e-133">Wanneer categorieën worden gewijzigd, wordt de registratie opnieuw gemaakt met de nieuwe categorieën.</span><span class="sxs-lookup"><span data-stu-id="3c95e-133">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="3c95e-134">Uw app is nu in staat een aantal categorieën opslaan in lokale opslag op het apparaat en registreren bij de notification hub wanneer de gebruiker de selectie van categorieën wijzigt.</span><span class="sxs-lookup"><span data-stu-id="3c95e-134">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="3c95e-135">Registreren voor meldingen</span><span class="sxs-lookup"><span data-stu-id="3c95e-135">Register for notifications</span></span>
<span data-ttu-id="3c95e-136">Deze stappen registreren bij de notification hub bij het opstarten met behulp van de categorieën die zijn opgeslagen in de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="3c95e-136">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="3c95e-137">Omdat de kanaal-URI is toegewezen door de Microsoft Push Notification Service (MPNS) op elk gewenst moment wijzigen kunt, kunt u moet registreren voor meldingen vaak ter voorkoming van fouten van de melding.</span><span class="sxs-lookup"><span data-stu-id="3c95e-137">Because the channel URI assigned by the Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="3c95e-138">In dit voorbeeld wordt elke keer dat de app wordt gestart voor meldingen die worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="3c95e-138">This example registers for notifications every time that the app starts.</span></span> <span data-ttu-id="3c95e-139">Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie om bandbreedte te besparen als minder dan een dag is verstreken sinds de vorige registratie.</span><span class="sxs-lookup"><span data-stu-id="3c95e-139">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="3c95e-140">Open het bestand App.xaml.cs en voeg de **asynchrone** wijzigingsfunctie voor **Application_Launching** methode en vervang de registratie van Notification Hubs code die u hebt toegevoegd in [aan de slag met Notification Hubs] met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="3c95e-140">Open the App.xaml.cs file and add the **async** modifier to **Application_Launching** method and replace the Notification Hubs registration code that you added in [Get started with Notification Hubs] with the following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="3c95e-141">Dit zorgt ervoor dat telkens wanneer de app wordt gestart de categorieën van lokale opslag haalt en een registratie voor deze categorieën vraagt.</span><span class="sxs-lookup"><span data-stu-id="3c95e-141">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="3c95e-142">Voeg in het projectbestand MainPage.xaml.cs de volgende code waarmee de **OnNavigatedTo** methode:</span><span class="sxs-lookup"><span data-stu-id="3c95e-142">In the MainPage.xaml.cs project file, add the following code that implements the **OnNavigatedTo** method:</span></span>
   
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
   
    <span data-ttu-id="3c95e-143">Hiermee wordt de hoofdpagina op basis van de status van de eerder opgeslagen categorieën bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="3c95e-143">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="3c95e-144">De app is nu voltooid en een set categorieën kunt opslaan in de lokale opslag gebruikt om u te registreren bij de notification hub wanneer de gebruiker de selectie van categorieën wijzigt van apparaat.</span><span class="sxs-lookup"><span data-stu-id="3c95e-144">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="3c95e-145">Vervolgens definiëren we een back-end die categorie meldingen naar deze app kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="3c95e-145">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="3c95e-146">Verzenden van meldingen met tags</span><span class="sxs-lookup"><span data-stu-id="3c95e-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="3c95e-147">Voer de app en meldingen genereren</span><span class="sxs-lookup"><span data-stu-id="3c95e-147">Run the app and generate notifications</span></span>
1. <span data-ttu-id="3c95e-148">Druk in Visual Studio op F5 om te compileren en de app te starten.</span><span class="sxs-lookup"><span data-stu-id="3c95e-148">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="3c95e-149">Opmerking dat de UI-app biedt een reeks Schakelknoppen waarmee u kunt kiezen uit de categorieën om u te abonneren op.</span><span class="sxs-lookup"><span data-stu-id="3c95e-149">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="3c95e-150">Een of meer categorieën Schakelknoppen inschakelen en klik vervolgens op **abonneren**.</span><span class="sxs-lookup"><span data-stu-id="3c95e-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="3c95e-151">De app de geselecteerde categorieën converteert naar labels en een nieuwe apparaatregistratie voor de geselecteerde codes aanvragen van de notification hub.</span><span class="sxs-lookup"><span data-stu-id="3c95e-151">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="3c95e-152">De geregistreerde categorieën worden geretourneerd en in een dialoogvenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c95e-152">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="3c95e-153">Na de ontvangst van een bevestiging dat uw categorieën abonnement voltooid zijn, moet u de console-app voor het verzenden van meldingen voor elke categorieën uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3c95e-153">After receiving a confirmation that your categories were subscription completed, run the console app to send notifications for each categories.</span></span> <span data-ttu-id="3c95e-154">Controleer of er alleen een melding voor de categorieën die u bent geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="3c95e-154">Verify you only receive a notification for the categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="3c95e-155">U kunt in dit onderwerp hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="3c95e-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how to broadcast breaking news by category. Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs to broadcast localized breaking news]

    Learn how to expand the breaking news app to enable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how to push notifications to specific authenticated users. This is a good solution for sending notifications only to specific users.
-->

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
<span data-ttu-id="3c95e-156">[aan de slag met Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span><span class="sxs-lookup"><span data-stu-id="3c95e-156">[Get started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span></span>
[Use Notification Hubs to broadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Phone]: ??

