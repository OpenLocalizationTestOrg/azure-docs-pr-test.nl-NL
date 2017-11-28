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
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a><span data-ttu-id="fcd4c-103">Gebruik Notification Hubs toosend gelokaliseerd belangrijk nieuws</span><span class="sxs-lookup"><span data-stu-id="fcd4c-103">Use Notification Hubs toosend localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fcd4c-104">Windows Store in C#</span><span class="sxs-lookup"><span data-stu-id="fcd4c-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="fcd4c-105">iOS</span><span class="sxs-lookup"><span data-stu-id="fcd4c-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="fcd4c-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="fcd4c-106">Overview</span></span>
<span data-ttu-id="fcd4c-107">Dit onderwerp leest u hoe toouse hello **sjabloon** functie van Azure Notification Hubs toobroadcast nieuws meldingen gelokaliseerde taal en het apparaat op te splitsen.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-107">This topic shows you how toouse hello **template** feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="fcd4c-108">In deze zelfstudie begint u met de Hallo Windows Store-app gemaakt in [Notification Hubs gebruiken toosend belangrijk nieuws].</span><span class="sxs-lookup"><span data-stu-id="fcd4c-108">In this tutorial you start with hello Windows Store app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="fcd4c-109">Wanneer voltooid, dat kunt u zich kunt tooregister voor u geïnteresseerd bent in categorieën, een taal opgeven in welke tooreceive Hallo-berichten en pushmeldingen voor Hallo geselecteerd categorieën in die taal ontvangen.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="fcd4c-110">Er zijn twee onderdelen toothis scenario:</span><span class="sxs-lookup"><span data-stu-id="fcd4c-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="fcd4c-111">Hallo Windows Store-app kan client apparaten toospecify een taal en toosubscribe toodifferent nieuwscategorieën; splitsen</span><span class="sxs-lookup"><span data-stu-id="fcd4c-111">hello Windows Store app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="fcd4c-112">Hallo back-end zendt Hallo meldingen, met behulp van Hallo **tag** en **sjabloon** funcites van Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcd4c-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fcd4c-113">Prerequisites</span></span>
<span data-ttu-id="fcd4c-114">U moet al hebt voltooid Hallo [Notification Hubs gebruiken toosend belangrijk nieuws] zelfstudie en Hallo code beschikbaar is, hebben omdat deze zelfstudie is gebaseerd rechtstreeks op die code.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="fcd4c-115">U moet ook Visual Studio 2012 of later.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="fcd4c-116">Sjabloon-concepten</span><span class="sxs-lookup"><span data-stu-id="fcd4c-116">Template concepts</span></span>
<span data-ttu-id="fcd4c-117">In [Notification Hubs gebruiken toosend belangrijk nieuws] u een app die gebruikt gebouwd **labels** toosubscribe toonotifications voor verschillende nieuwscategorieën.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="fcd4c-118">Veel apps echter meerdere markten zijn gericht en lokalisatie vereisen.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="fcd4c-119">Dit betekent dat Hallo inhoud van het Hallo-meldingen zelf toobe gelokaliseerd en geleverde toohello corrigeren set apparaten.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="fcd4c-120">In dit onderwerp we tonen hoe toouse hello **sjabloon** functie van Notification Hubs tooeasily leveren belangrijk nieuws meldingen gelokaliseerd.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="fcd4c-121">Opmerking: eenrichtingssessie toosend gelokaliseerd meldingen toocreate meerdere versies van elke tag is.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="fcd4c-122">Bijvoorbeeld: toosupport Engels, Frans en Mandarijn, zou moeten we drie verschillende tags voor wereldnieuws: 'world_en', 'world_fr' en 'world_ch'.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="fcd4c-123">We hebben toosend een gelokaliseerde versie van Hallo wereld nieuws tooeach van deze labels.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="fcd4c-124">In dit onderwerp gebruiken we sjablonen tooavoid Hallo verspreiding van tags en Hallo vereiste van meerdere berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="fcd4c-125">Op een hoog niveau sjablonen zijn een manier toospecify hoe een specifiek apparaat een melding moet ontvangen.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="fcd4c-126">indeling van de exacte nettolading Hallo geeft Hallo sjabloon door te verwijzen tooproperties die deel van het Hallo-bericht verzonden door back-end van uw app uitmaken.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="fcd4c-127">In ons geval ontvangt van ons een landinstelling networkdirect-bericht met alle ondersteunde talen:</span><span class="sxs-lookup"><span data-stu-id="fcd4c-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="fcd4c-128">Vervolgens we zorgt ervoor dat apparaten registreren met een sjabloon die de juiste eigenschap toohello verwijst.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="fcd4c-129">Bijvoorbeeld Windows Store-Apps die tooreceive wil een eenvoudige pop-up bericht registreert Hallo sjabloon met een overeenkomende labels te volgen:</span><span class="sxs-lookup"><span data-stu-id="fcd4c-129">For instance, a Windows Store app that wants tooreceive a simple toast message will register for hello following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="fcd4c-130">Sjablonen zijn een zeer krachtige functie voor meer informatie over in onze [sjablonen](notification-hubs-templates-cross-platform-push-messages.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="hello-app-user-interface"></a><span data-ttu-id="fcd4c-131">Hallo-app-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="fcd4c-131">hello app user interface</span></span>
<span data-ttu-id="fcd4c-132">We zullen nu Hallo nieuws op te splitsen app die u hebt gemaakt in Hallo onderwerp wijzigen [Notification Hubs gebruiken toosend belangrijk nieuws] toosend gelokaliseerd belangrijk nieuws met behulp van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="fcd4c-133">In de Windows Store-app:</span><span class="sxs-lookup"><span data-stu-id="fcd4c-133">In your Windows Store app:</span></span>

<span data-ttu-id="fcd4c-134">Uw MainPage.xaml tooinclude landinstelling combobox wijzigen:</span><span class="sxs-lookup"><span data-stu-id="fcd4c-134">Change your MainPage.xaml tooinclude a locale combobox:</span></span>

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

## <a name="building-hello-windows-store-client-app"></a><span data-ttu-id="fcd4c-135">Hallo Windows Store-client-app bouwen</span><span class="sxs-lookup"><span data-stu-id="fcd4c-135">Building hello Windows Store client app</span></span>
1. <span data-ttu-id="fcd4c-136">Voeg in uw klasse meldingen een landinstelling parameter tooyour *StoreCategoriesAndSubscribe* en *SubscribeToCateories* methoden.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-136">In your Notifications class, add a locale parameter tooyour  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
   
    <span data-ttu-id="fcd4c-137">Houd er rekening mee dat in plaats van aanroepen Hallo *RegisterNativeAsync* methode we noemen *RegisterTemplateAsync*: we bij het registreren van een specifieke notification-indeling in welke Hallo sjabloon afhankelijk Hallo landinstelling.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-137">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which hello template depends on hello locale.</span></span> <span data-ttu-id="fcd4c-138">We bieden ook een naam voor Hallo-sjabloon ('localizedWNSTemplateExample'), omdat er tooregister meer dan één sjabloon (bijvoorbeeld één voor de pop-upmeldingen) en één voor tegels wilt mogelijk en tooname moeten ze in volgorde van toobe kunnen tooupdate of verwijder ze.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-138">We also provide a name for hello template ("localizedWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="fcd4c-139">Houd er rekening mee dat als een apparaat meerdere sjablonen met Hallo dezelfde tag registreert, een binnenkomend bericht als doel dat label zal resulteren in meerdere meldingen toohello-apparaat (één voor elke sjabloon) geleverd.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-139">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="fcd4c-140">Dit gedrag is handig wanneer hello hetzelfde logische bericht tooresult in meerdere visual meldingen heeft, bijvoorbeeld zowel een badge en een pop-up wordt weergegeven in een Windows Store-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fcd4c-140">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="fcd4c-141">Hallo na methode tooretrieve Hallo opgeslagen landinstellingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="fcd4c-141">Add hello following method tooretrieve hello stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="fcd4c-142">De knop bijwerken in uw MainPage.xaml.cs, klikt u op handler door bij het ophalen van de huidige waarde Hallo van Hallo landinstelling keuzelijst met invoervak en het geven van het toohello aanroep toohello meldingen klasse, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="fcd4c-142">In your MainPage.xaml.cs, update your button click handler by retrieving hello current value of hello Locale combo box and providing it toohello call toohello Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="fcd4c-143">Ten slotte in het bestand App.xaml.cs, zorg ervoor dat tooupdate uw `InitNotificationsAsync` methode tooretrieve Hallo landinstellingen en deze gebruiken als u zich abonneert:</span><span class="sxs-lookup"><span data-stu-id="fcd4c-143">Finally, in your App.xaml.cs file, make sure tooupdate your `InitNotificationsAsync` method tooretrieve hello locale and use it when subscribing:</span></span>
   
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

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="fcd4c-144">Gelokaliseerde meldingen verzenden vanuit uw back-end</span><span class="sxs-lookup"><span data-stu-id="fcd4c-144">Send localized notifications from your back-end</span></span>
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
