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
# <a name="use-notification-hubs-toosend-breaking-news"></a>Gebruik Notification Hubs toosend belangrijk nieuws
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Overzicht
Dit onderwerp leest u hoe toouse Azure Notification Hubs toobroadcast laatste nieuws meldingen tooa Windows Store of app van Windows Phone 8.1 (zonder Silverlight). Als u voor Windows Phone 8.1 Silverlight ontwikkelt, raadpleegt u toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) versie. Als u klaar gaat u kunnen tooregister voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen. Dit scenario is een algemene patroon voor veel apps waar meldingen hebt verzonden toobe toogroups van gebruikers die hebben dit eerder is gedeclareerd interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort. 

Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in Hallo notification hub. Wanneer meldingen worden verzonden tooa label, ontvangen alle apparaten die zijn geregistreerd voor de tag Hallo Hallo-bericht. Omdat tags gewoon tekenreeksen zijn, hebben geen toobe vooraf is ingericht. Raadpleeg te voor meer informatie over tags[Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).

> [!NOTE]
> Windows Store en Windows Phone-projecten versie 8.1 en lager worden niet ondersteund in Visual Studio 2017.  Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie. 

## <a name="prerequisites"></a>Vereisten
In dit onderwerp is gebaseerd op Hallo-app die u hebt gemaakt in [aan de slag met Notification Hubs][get-started]. Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Categorie selectie toohello app toevoegen
de eerste stap Hallo is tooadd Hallo UI-elementen tooyour bestaande hoofdpagina waarmee Hallo gebruiker tooselect categorieën tooregister. Hallo categorieën geselecteerd door een gebruiker zijn op Hallo apparaat opgeslagen. Wanneer Hallo-app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met Hallo geselecteerd categorieën gemaakt als labels.

1. Open Hallo MainPage.xaml projectbestand vervolgens kopiëren Hallo na de code in Hallo **raster** element:
   
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
2. Klik met de rechtermuisknop op Hallo **gedeelde** project en voeg een nieuwe klasse met de naam **meldingen**, Hallo toevoegen **openbare** aanpassingsfunctie toohello definitie klasse, voeg dan Hallo na **met** instructies toohello nieuwe codebestand:
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. Kopiëren Hallo volgende code in nieuwe Hallo **meldingen** klasse:
   
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
   
    Hallo lokale opslag toostore Hallo categorieën van nieuws dat dit apparaat tooreceive heeft maakt gebruik van deze klasse. Houd er rekening mee dat in plaats van aanroepen Hallo *RegisterNativeAsync* methode we noemen *RegisterTemplateAsync* tooregister voor Hallo categorieën met behulp van de registratie van een sjabloon. 
   
    We bieden ook een naam voor Hallo-sjabloon ('simpleWNSTemplateExample'), omdat er tooregister meer dan één sjabloon (bijvoorbeeld één voor de pop-upmeldingen) en één voor tegels wilt mogelijk en tooname moeten ze in volgorde van toobe kunnen tooupdate of verwijder ze.
   
    Houd er rekening mee dat als een apparaat meerdere sjablonen met Hallo dezelfde tag registreert, een binnenkomend bericht als doel dat label zal resulteren in meerdere meldingen toohello-apparaat (één voor elke sjabloon) geleverd. Dit gedrag is handig wanneer hello hetzelfde logische bericht tooresult in meerdere visual meldingen heeft, bijvoorbeeld zowel een badge en een pop-up wordt weergegeven in een Windows Store-toepassing.
   
    Zie voor meer informatie over sjablonen [sjablonen](notification-hubs-templates-cross-platform-push-messages.md).
4. Hallo projectbestand App.XAML.cs, voeg Hallo eigenschap toohello na **App** klasse:
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    Deze eigenschap is gebruikte toocreate en toegang tot een **meldingen** exemplaar.
   
    Vervang in Hallo bovenstaande code Hallo `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultListenSharedAccessSignature* die u eerder hebt verkregen.
   
   > [!NOTE]
   > Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u alleen Hallo-sleutel voor listen toegang distribueren met uw clientapp. Luisteren toegang kunnen die uw app tooregister voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden. Hallo volledige toegang tot de sleutel wordt gebruikt in een beveiligde back endservice voor het verzenden van meldingen en bestaande registraties wijzigen.
   > 
   > 
5. Voeg in uw MainPage.xaml.cs Hallo volgt regel:
   
        using Windows.UI.Popups;
6. Voeg Hallo volgende methode in Hallo MainPage.xaml.cs project-bestand:
   
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
   
    Deze methode maakt u een lijst met categorieën en maakt gebruik van Hallo **meldingen** toostore Hallo lijst in de lokale opslag Hallo klasse en bijbehorende labels Hallo registreren voor uw notification hub. Wanneer categorieën worden gewijzigd, wordt met de nieuwe categorieën Hallo Hallo registratie nagemaakt.

Uw app is nu kunnen toostore een aantal categorieën in lokale opslag op Hallo-apparaat en registreren bij Hallo notification hub wanneer gebruikerswijzigingen Hallo Hallo selectie van categorieën.

## <a name="register-for-notifications"></a>Registreren voor meldingen
Deze stappen registreren bij Hallo notification hub bij het opstarten met behulp van Hallo categorieën die zijn opgeslagen in de lokale opslag.

> [!NOTE]
> Omdat Hallo kanaal-URI toegewezen door Hallo Windows Notification Service (WNS) op elk gewenst moment wijzigen kunt, moet u registreren voor meldingen vaak tooavoid melding fouten. In dit voorbeeld registreert voor melding telkens wanneer die Hallo-app wordt gestart. Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie toopreserve bandbreedte als minder dan een dag is verstreken sinds de vorige registratie Hallo.
> 
> 

1. Open Hallo App.xaml.cs bestands- en update Hallo **InitNotificationsAsync** methode toouse hello `notifications` klasse toosubscribe op basis van categorieën.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    Dit zorgt ervoor dat telkens wanneer Hallo-app wordt gestart het Hallo-categorieën opgehaald uit de lokale opslag en een registratie voor deze categorieën vraagt. Hallo **InitNotificationsAsync** methode is gemaakt als onderdeel van Hallo [aan de slag met Notification Hubs] [ get-started] zelfstudie.
2. Voeg Hallo code toohello te volgen in Hallo MainPage.xaml.cs project-bestand *OnNavigatedTo* methode:
   
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
   
    ![][19]
3. Een nieuwe melding verzenden vanuit back-end Hallo in een van de volgende manieren Hallo:
   
   * **Console-app:** Hallo console-app te starten.
   * **Java/PHP:** uw app/script uitvoeren.
     
     Meldingen voor Hallo geselecteerd categorieën weergegeven als pop-upmeldingen.
     
     ![][14]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toobroadcast belangrijk nieuws per categorie. Houd rekening met een van de volgende zelfstudies waarin andere geavanceerde scenario's voor Notification Hubs Markeer Hallo voltooien:

* [Gebruik Notification Hubs toobroadcast gelokaliseerd belangrijk nieuws]
  
    Meer informatie over hoe tooexpand Hallo nieuws app tooenable verzenden op te splitsen meldingen gelokaliseerd.

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
