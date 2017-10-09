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
# <a name="use-notification-hubs-toosend-breaking-news"></a>Gebruik Notification Hubs toosend belangrijk nieuws
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Overzicht
Dit onderwerp leest u hoe toouse Azure Notification Hubs toobroadcast belangrijk nieuws meldingen tooa Windows Phone 8.0/8.1 Silverlight-app. Als u voor Windows Store of Windows Phone 8.1-app ontwikkelt, raadpleegt u tootoohello [universele Windows-](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) versie. Als u klaar gaat u kunnen tooregister voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen. Dit scenario is een algemene patroon voor veel apps waar meldingen hebt verzonden toobe toogroups van gebruikers die interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort eerder is gedeclareerd.

Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in Hallo notification hub. Wanneer meldingen worden verzonden tooa label, ontvangen alle apparaten die zijn geregistreerd voor de tag Hallo Hallo-bericht. Omdat tags gewoon tekenreeksen zijn, hebben geen toobe vooraf is ingericht. Raadpleeg te voor meer informatie over tags[Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Vereisten
In dit onderwerp is gebaseerd op Hallo-app die u hebt gemaakt in [aan de slag met Notification Hubs]. Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs].

## <a name="add-category-selection-toohello-app"></a>Categorie selectie toohello app toevoegen
de eerste stap Hallo is tooadd Hallo UI-elementen tooyour bestaande hoofdpagina waarmee Hallo gebruiker tooselect categorieën tooregister. Hallo categorieën geselecteerd door een gebruiker zijn op Hallo apparaat opgeslagen. Wanneer Hallo-app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met Hallo geselecteerd categorieën gemaakt als labels.

1. Hallo MainPage.xaml projectbestand openen en vervolgens vervangen Hallo **raster** elementen met de naam `TitlePanel` en `ContentPanel` Hello code te volgen:
   
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
2. In Hallo-project maakt u een nieuwe klasse met de naam **meldingen**, Hallo toevoegen **openbare** aanpassingsfunctie toohello definitie klasse, voeg dan Hallo volgende **met** instructies nieuwe codebestand toohello:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. Kopiëren Hallo volgende code in nieuwe Hallo **meldingen** klasse:
   
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

    Hallo geïsoleerde opslag toostore Hallo categorieën van nieuws dat dit apparaat tooreceive is maakt gebruik van deze klasse. Het bevat ook methoden tooregister voor deze categorieën met behulp van een [sjabloon](notification-hubs-templates-cross-platform-push-messages.md) registratie.


1. Hallo projectbestand App.XAML.cs, voeg Hallo eigenschap toohello na **App** klasse. Vervang Hallo `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultListenSharedAccessSignature* die u eerder hebt verkregen.
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u alleen Hallo-sleutel voor listen toegang distribueren met uw clientapp. Luisteren toegang kunnen die uw app tooregister voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden. Hallo volledige toegang tot de sleutel wordt gebruikt in een beveiligde back endservice voor het verzenden van meldingen en bestaande registraties wijzigen.
   > 
   > 
2. Voeg in uw MainPage.xaml.cs Hallo volgt regel:
   
        using Windows.UI.Popups;
3. Voeg Hallo volgende methode in Hallo MainPage.xaml.cs project-bestand:
   
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
   
    Deze methode maakt u een lijst met categorieën en maakt gebruik van Hallo **meldingen** toostore Hallo lijst in de lokale opslag Hallo klasse en bijbehorende labels Hallo registreren voor uw notification hub. Wanneer categorieën worden gewijzigd, wordt met de nieuwe categorieën Hallo Hallo registratie nagemaakt.

Uw app is nu kunnen toostore een aantal categorieën in lokale opslag op Hallo-apparaat en registreren bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën.

## <a name="register-for-notifications"></a>Registreren voor meldingen
Deze stappen registreren bij Hallo notification hub bij het opstarten met behulp van Hallo categorieën die zijn opgeslagen in de lokale opslag.

> [!NOTE]
> Omdat Hallo kanaal-URI toegewezen door Hallo Microsoft Push Notification Service (MPNS) op elk gewenst moment wijzigen kunt, moet u registreren voor meldingen vaak tooavoid melding fouten. In dit voorbeeld registreert voor meldingen telkens wanneer die Hallo-app wordt gestart. Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie toopreserve bandbreedte als minder dan een dag is verstreken sinds de vorige registratie Hallo.
> 
> 

1. Hallo App.xaml.cs bestand openen en het toevoegen van Hallo **asynchrone** aanpassingsfunctie te**Application_Launching** methode en vervang Hallo Notification Hubs registratiecode die u hebt toegevoegd in [aan de slag met Notification Hubs] Hello code te volgen:
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    Dit zorgt ervoor dat telkens wanneer Hallo-app wordt gestart het Hallo-categorieën opgehaald uit de lokale opslag en een registratie voor deze categorieën vraagt.
2. In Hallo MainPage.xaml.cs project-bestand toevoegen na de code die wordt geïmplementeerd Hallo Hallo **OnNavigatedTo** methode:
   
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
   
    Deze updates Hallo hoofdpagina op basis van Hallo status van de eerder opgeslagen categorieën.

Hallo-app is nu voltooid en kan een set van categorieën worden opgeslagen in Hallo apparaat gebruikt voor lokale opslag tooregister bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën. Vervolgens definiëren we een back-end die categorie meldingen toothis app kunt verzenden.

## <a name="sending-tagged-notifications"></a>Verzenden van meldingen met tags
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Hallo-app uitvoeren en meldingen genereren
1. Druk op F5 toocompile in Visual Studio en Hallo-app te starten.
   
    ![][1]
   
    Opmerking die Hallo app die gebruikersinterface een set biedt-of kunt u Hallo categorieën toosubscribe te kiezen.
2. Een of meer categorieën Schakelknoppen inschakelen en klik vervolgens op **abonneren**.
   
    Hallo-app geselecteerd Hallo categorieën converteert naar labels en vraagt een nieuwe apparaatregistratie voor Hallo geselecteerd tags van Hallo notification hub. Hallo geregistreerde categorieën worden geretourneerd en in een dialoogvenster weergegeven.
   
    ![][2]
3. Voer na de ontvangst van een bevestiging dat uw categorieën abonnement voltooid zijn, Hallo console app toosend meldingen voor elke categorieën. Controleer of er alleen een melding voor Hallo categorieën die u bent geabonneerd.
   
    ![][3]

U kunt in dit onderwerp hebt voltooid.

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

