---
title: Notification Hubs gelokaliseerd belangrijk nieuws zelfstudie
description: Informatie over het gebruik van Azure Notification Hubs om gelokaliseerde belangrijk nieuws meldingen te verzenden.
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
ms.openlocfilehash: e864e832b4c50644bf4062dee29d34ff9fe2774e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news"></a><span data-ttu-id="e1e9a-103">Notification Hubs gebruiken om gelokaliseerde belangrijk nieuws te verzenden</span><span class="sxs-lookup"><span data-stu-id="e1e9a-103">Use Notification Hubs to send localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1e9a-104">Windows Store in C#</span><span class="sxs-lookup"><span data-stu-id="e1e9a-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="e1e9a-105">iOS</span><span class="sxs-lookup"><span data-stu-id="e1e9a-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e1e9a-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e1e9a-106">Overview</span></span>
<span data-ttu-id="e1e9a-107">Dit onderwerp leest u hoe u de **sjabloon** functie van Azure Notification Hubs voor belangrijk nieuws meldingen die door de taal en het apparaat zijn gelokaliseerd uitzending.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-107">This topic shows you how to use the **template** feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="e1e9a-108">In deze zelfstudie begint u met de Windows Store-app gemaakt in [Notification Hubs gebruiken om belangrijk nieuws te verzenden].</span><span class="sxs-lookup"><span data-stu-id="e1e9a-108">In this tutorial you start with the Windows Store app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="e1e9a-109">Als u klaar is, kunt u zich registreren voor u geïnteresseerd bent in categorieën, geeft u de taal waarin u de meldingen ontvangen en pushmeldingen voor de geselecteerde categorieën in die taal ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="e1e9a-110">Er zijn twee delen in dit scenario:</span><span class="sxs-lookup"><span data-stu-id="e1e9a-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="e1e9a-111">de Windows Store-app kan client apparaten een taal op te geven en zich abonneren op andere belangrijk nieuwscategorieën;</span><span class="sxs-lookup"><span data-stu-id="e1e9a-111">the Windows Store app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="e1e9a-112">de back-end zendt de meldingen, met behulp van de **tag** en **sjabloon** funcites van Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1e9a-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e1e9a-113">Prerequisites</span></span>
<span data-ttu-id="e1e9a-114">U moet al hebt voltooid de [Notification Hubs gebruiken om belangrijk nieuws te verzenden] zelfstudie en hebben de code die beschikbaar zijn, omdat deze zelfstudie is gebaseerd rechtstreeks op die code.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="e1e9a-115">U moet ook Visual Studio 2012 of later.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="e1e9a-116">Sjabloon-concepten</span><span class="sxs-lookup"><span data-stu-id="e1e9a-116">Template concepts</span></span>
<span data-ttu-id="e1e9a-117">In [Notification Hubs gebruiken om belangrijk nieuws te verzenden] u een app die gebruikt gebouwd **labels** abonneren op meldingen voor verschillende nieuwscategorieën.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="e1e9a-118">Veel apps echter meerdere markten zijn gericht en lokalisatie vereisen.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="e1e9a-119">Dit betekent dat de inhoud van de meldingen zelf hebt kunnen worden gelokaliseerd en verzonden naar de juiste set met apparaten.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="e1e9a-120">In dit onderwerp wordt wordt getoond hoe u de **sjabloon** functie van Notification Hubs eenvoudig leveren gelokaliseerde belangrijk nieuws meldingen.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="e1e9a-121">Opmerking: Er is een manier om gelokaliseerde meldingen te verzenden is om meerdere versies van elke tag te maken.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="e1e9a-122">Bijvoorbeeld ter ondersteuning van Engels, Frans en Mandarijn, zou moeten we drie verschillende tags voor wereldnieuws: 'world_en', 'world_fr' en 'world_ch'.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="e1e9a-123">Er moet een gelokaliseerde versie van de wereldnieuws verzenden naar elk van deze tags.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="e1e9a-124">In dit onderwerp gebruiken we sjablonen om te voorkomen dat de komst van tags en de vereiste van meerdere berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="e1e9a-125">Sjablonen zijn op een hoog niveau een manier om op te geven hoe een specifiek apparaat een melding moet ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="e1e9a-126">De sjabloon geeft de indeling van de exacte nettolading door te verwijzen naar de eigenschappen die deel van het bericht is verzonden door back-end van uw app uitmaken.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="e1e9a-127">In ons geval ontvangt van ons een landinstelling networkdirect-bericht met alle ondersteunde talen:</span><span class="sxs-lookup"><span data-stu-id="e1e9a-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="e1e9a-128">Vervolgens we zorgt ervoor dat apparaten registreren met een sjabloon die naar de juiste eigenschap verwijst.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="e1e9a-129">Windows Store-Apps die wil een eenvoudige pop-up bericht wordt bijvoorbeeld registreren voor de volgende sjabloon met een overeenkomende labels:</span><span class="sxs-lookup"><span data-stu-id="e1e9a-129">For instance, a Windows Store app that wants to receive a simple toast message will register for the following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="e1e9a-130">Sjablonen zijn een zeer krachtige functie voor meer informatie over in onze [sjablonen](notification-hubs-templates-cross-platform-push-messages.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="the-app-user-interface"></a><span data-ttu-id="e1e9a-131">De gebruikersinterface van de app</span><span class="sxs-lookup"><span data-stu-id="e1e9a-131">The app user interface</span></span>
<span data-ttu-id="e1e9a-132">Er wordt nu de op te splitsen nieuws-app die u hebt gemaakt in het onderwerp wijzigen [Notification Hubs gebruiken om belangrijk nieuws te verzenden] gelokaliseerd belangrijk nieuws met behulp van sjablonen om te verzenden.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="e1e9a-133">In de Windows Store-app:</span><span class="sxs-lookup"><span data-stu-id="e1e9a-133">In your Windows Store app:</span></span>

<span data-ttu-id="e1e9a-134">Uw MainPage.xaml als u wilt opnemen een combobox landinstelling wijzigen:</span><span class="sxs-lookup"><span data-stu-id="e1e9a-134">Change your MainPage.xaml to include a locale combobox:</span></span>

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

## <a name="building-the-windows-store-client-app"></a><span data-ttu-id="e1e9a-135">De client Windows Store-app bouwen</span><span class="sxs-lookup"><span data-stu-id="e1e9a-135">Building the Windows Store client app</span></span>
1. <span data-ttu-id="e1e9a-136">In uw klasse meldingen toevoegen een landinstellingenparameter voor uw *StoreCategoriesAndSubscribe* en *SubscribeToCateories* methoden.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-136">In your Notifications class, add a locale parameter to your  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
            // Using the localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="e1e9a-137">Houd er rekening mee dat in plaats van het aanroepen van de *RegisterNativeAsync* methode we noemen *RegisterTemplateAsync*: we bij het registreren van een specifieke notification-indeling op waarin de sjabloon is afhankelijk van de landinstelling.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-137">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which the template depends on the locale.</span></span> <span data-ttu-id="e1e9a-138">We bieden ook een naam voor de sjabloon ('localizedWNSTemplateExample'), omdat we willen mogelijk meer dan één sjabloon (bijvoorbeeld één voor de pop-upmeldingen) en één voor tegels registreren en moeten deze de naam om te kunnen bijwerken of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-138">We also provide a name for the template ("localizedWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="e1e9a-139">Houd er rekening mee dat als een apparaat meerdere sjablonen met dezelfde tag registreert, een binnenkomende bericht doelen die tag in meerdere meldingen resulteren geleverd aan het apparaat (één voor elke sjabloon).</span><span class="sxs-lookup"><span data-stu-id="e1e9a-139">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="e1e9a-140">Dit gedrag is handig wanneer hetzelfde logische bericht moet resulteren in meerdere visual meldingen, bijvoorbeeld zowel een badge en een pop-up wordt weergegeven in een Windows Store-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e1e9a-140">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="e1e9a-141">Voeg de volgende methode voor het ophalen van de opgeslagen landinstellingen:</span><span class="sxs-lookup"><span data-stu-id="e1e9a-141">Add the following method to retrieve the stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="e1e9a-142">De knop bijwerken in uw MainPage.xaml.cs, klikt u op handler door bij het ophalen van de huidige waarde van de landinstelling keuzelijst met invoervak en beschikbaar stellen de aanroep van de klasse meldingen, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e1e9a-142">In your MainPage.xaml.cs, update your button click handler by retrieving the current value of the Locale combo box and providing it to the call to the Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="e1e9a-143">Controleer ten slotte, in het bestand App.xaml.cs om bij te werken uw `InitNotificationsAsync` methode voor het ophalen van de landinstelling en deze gebruiken als u zich abonneert:</span><span class="sxs-lookup"><span data-stu-id="e1e9a-143">Finally, in your App.xaml.cs file, make sure to update your `InitNotificationsAsync` method to retrieve the locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="e1e9a-144">Gelokaliseerde meldingen verzenden vanuit uw back-end</span><span class="sxs-lookup"><span data-stu-id="e1e9a-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[The app user interface]: #ui
[Building the Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
<span data-ttu-id="e1e9a-145">[Notification Hubs gebruiken om belangrijk nieuws te verzenden]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="e1e9a-145">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
