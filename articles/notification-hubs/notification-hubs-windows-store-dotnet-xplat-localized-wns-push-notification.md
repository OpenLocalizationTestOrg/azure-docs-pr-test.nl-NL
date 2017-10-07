---
title: aaaNotification Hubs gelokaliseerd op te splitsen nieuws-zelfstudie
description: Meer informatie over hoe toouse Azure Notification Hubs toosend belangrijk nieuws meldingen gelokaliseerd.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: c454f5a3-a06b-45ac-91c7-f91210889b25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d273a6b384df311dea7b76ca83ccd94d9a989c4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a>Gebruik Notification Hubs toosend gelokaliseerd belangrijk nieuws
> [!div class="op_single_selector"]
> * [Windows Store in C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Overzicht
Dit onderwerp leest u hoe toouse hello **sjabloon** functie van Azure Notification Hubs toobroadcast nieuws meldingen gelokaliseerde taal en het apparaat op te splitsen. In deze zelfstudie begint u met de Hallo Windows Store-app gemaakt in [Notification Hubs gebruiken toosend belangrijk nieuws]. Wanneer voltooid, dat kunt u zich kunt tooregister voor u geïnteresseerd bent in categorieën, een taal opgeven in welke tooreceive Hallo-berichten en pushmeldingen voor Hallo geselecteerd categorieën in die taal ontvangen.

Er zijn twee onderdelen toothis scenario:

* Hallo Windows Store-app kan client apparaten toospecify een taal en toosubscribe toodifferent nieuwscategorieën; splitsen
* Hallo back-end zendt Hallo meldingen, met behulp van Hallo **tag** en **sjabloon** funcites van Azure Notification Hubs.

## <a name="prerequisites"></a>Vereisten
U moet al hebt voltooid Hallo [Notification Hubs gebruiken toosend belangrijk nieuws] zelfstudie en Hallo code beschikbaar is, hebben omdat deze zelfstudie is gebaseerd rechtstreeks op die code.

U moet ook Visual Studio 2012 of later.

## <a name="template-concepts"></a>Sjabloon-concepten
In [Notification Hubs gebruiken toosend belangrijk nieuws] u een app die gebruikt gebouwd **labels** toosubscribe toonotifications voor verschillende nieuwscategorieën.
Veel apps echter meerdere markten zijn gericht en lokalisatie vereisen. Dit betekent dat Hallo inhoud van het Hallo-meldingen zelf toobe gelokaliseerd en geleverde toohello corrigeren set apparaten.
In dit onderwerp we tonen hoe toouse hello **sjabloon** functie van Notification Hubs tooeasily leveren belangrijk nieuws meldingen gelokaliseerd.

Opmerking: eenrichtingssessie toosend gelokaliseerd meldingen toocreate meerdere versies van elke tag is. Bijvoorbeeld: toosupport Engels, Frans en Mandarijn, zou moeten we drie verschillende tags voor wereldnieuws: 'world_en', 'world_fr' en 'world_ch'. We hebben toosend een gelokaliseerde versie van Hallo wereld nieuws tooeach van deze labels. In dit onderwerp gebruiken we sjablonen tooavoid Hallo verspreiding van tags en Hallo vereiste van meerdere berichten verzenden.

Op een hoog niveau sjablonen zijn een manier toospecify hoe een specifiek apparaat een melding moet ontvangen. indeling van de exacte nettolading Hallo geeft Hallo sjabloon door te verwijzen tooproperties die deel van het Hallo-bericht verzonden door back-end van uw app uitmaken. In ons geval ontvangt van ons een landinstelling networkdirect-bericht met alle ondersteunde talen:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Vervolgens we zorgt ervoor dat apparaten registreren met een sjabloon die de juiste eigenschap toohello verwijst. Bijvoorbeeld Windows Store-Apps die tooreceive wil een eenvoudige pop-up bericht registreert Hallo sjabloon met een overeenkomende labels te volgen:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



Sjablonen zijn een zeer krachtige functie voor meer informatie over in onze [sjablonen](notification-hubs-templates-cross-platform-push-messages.md) artikel. 

## <a name="hello-app-user-interface"></a>Hallo-app-gebruikersinterface
We zullen nu Hallo nieuws op te splitsen app die u hebt gemaakt in Hallo onderwerp wijzigen [Notification Hubs gebruiken toosend belangrijk nieuws] toosend gelokaliseerd belangrijk nieuws met behulp van sjablonen.

In de Windows Store-app:

Uw MainPage.xaml tooinclude landinstelling combobox wijzigen:

    <Grid Margin="120, 58, 120, 80"  
            Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top"/>
        <ComboBox Name="Locale" HorizontalAlignment="Left" VerticalAlignment="Center" Width="200" Grid.Row="1" Grid.Column="0">
            <x:String>English</x:String>
            <x:String>French</x:String>
            <x:String>Mandarin</x:String>
        </ComboBox>
        <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="2" Grid.Column="0"/>
        <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="3" Grid.Column="0"/>
        <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="4" Grid.Column="0"/>
        <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="2" Grid.Column="1"/>
        <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="3" Grid.Column="1"/>
        <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="4" Grid.Column="1"/>
        <Button Content="Subscribe" HorizontalAlignment="Center" Grid.Row="5" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
    </Grid>

## <a name="building-hello-windows-store-client-app"></a>Hallo Windows Store-client-app bouwen
1. Voeg in uw klasse meldingen een landinstelling parameter tooyour *StoreCategoriesAndSubscribe* en *SubscribeToCateories* methoden.
   
        public async Task<Registration> StoreCategoriesAndSubscribe(string locale, IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            ApplicationData.Current.LocalSettings.Values["locale"] = locale;
            return await SubscribeToCategories(categories);
        }
   
        public async Task<Registration> SubscribeToCategories(string locale, IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration. This makes supporting notifications across other platforms much easier.
            // Using hello localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    Houd er rekening mee dat in plaats van aanroepen Hallo *RegisterNativeAsync* methode we noemen *RegisterTemplateAsync*: we bij het registreren van een specifieke notification-indeling in welke Hallo sjabloon afhankelijk Hallo landinstelling. We bieden ook een naam voor Hallo-sjabloon ('localizedWNSTemplateExample'), omdat er tooregister meer dan één sjabloon (bijvoorbeeld één voor de pop-upmeldingen) en één voor tegels wilt mogelijk en tooname moeten ze in volgorde van toobe kunnen tooupdate of verwijder ze.
   
    Houd er rekening mee dat als een apparaat meerdere sjablonen met Hallo dezelfde tag registreert, een binnenkomend bericht als doel dat label zal resulteren in meerdere meldingen toohello-apparaat (één voor elke sjabloon) geleverd. Dit gedrag is handig wanneer hello hetzelfde logische bericht tooresult in meerdere visual meldingen heeft, bijvoorbeeld zowel een badge en een pop-up wordt weergegeven in een Windows Store-toepassing.
2. Hallo na methode tooretrieve Hallo opgeslagen landinstellingen toevoegen:
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. De knop bijwerken in uw MainPage.xaml.cs, klikt u op handler door bij het ophalen van de huidige waarde Hallo van Hallo landinstelling keuzelijst met invoervak en het geven van het toohello aanroep toohello meldingen klasse, zoals wordt weergegeven:
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var locale = (string)Locale.SelectedItem;
   
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(locale,
                 categories);
   
            var dialog = new MessageDialog("Locale: " + locale + " Subscribed to: " + 
                string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
4. Ten slotte in het bestand App.xaml.cs, zorg ervoor dat tooupdate uw `InitNotificationsAsync` methode tooretrieve Hallo landinstellingen en deze gebruiken als u zich abonneert:
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a>Gelokaliseerde meldingen verzenden vanuit uw back-end
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[hello app user interface]: #ui
[Building hello Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[Notification Hubs gebruiken toosend belangrijk nieuws]: /manage/services/notification-hubs/breaking-news-dotnet

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
