---
title: aaaAzure Notification Hubs gebruikers waarschuwen met .NET back-end
description: Meer informatie over hoe toosend beveiligde pushmeldingen in Azure. Codevoorbeelden geschreven in C# met Hallo .NET API.
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="47ce9-104">Azure Notification Hubs gebruikers waarschuwen met .NET back-end</span><span class="sxs-lookup"><span data-stu-id="47ce9-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="47ce9-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="47ce9-105">Overview</span></span>
<span data-ttu-id="47ce9-106">Push notification-ondersteuning in Azure kunt u tooaccess een eenvoudig te gebruiken, multiplatform en uitgebreid pushinfrastructuur, die sterk vereenvoudigd Hallo-implementatie van pushmeldingen voor consumenten- en enterprise-toepassingen voor mobiele telefoons -platforms.</span><span class="sxs-lookup"><span data-stu-id="47ce9-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="47ce9-107">Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa specifieke app gebruiker op een specifiek apparaat.</span><span class="sxs-lookup"><span data-stu-id="47ce9-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="47ce9-108">Een ASP.NET WebAPI-back-end is gebruikte tooauthenticate clients.</span><span class="sxs-lookup"><span data-stu-id="47ce9-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="47ce9-109">Hallo geverifieerde clientgebruiker en label automatisch worden toegevoegd door Hallo back-end toonotification registratie.</span><span class="sxs-lookup"><span data-stu-id="47ce9-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="47ce9-110">Deze tag worden gebruikte toosend Hallo back-end toogenerate meldingen voor een specifieke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="47ce9-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="47ce9-111">Zie voor meer informatie over het registreren voor meldingen met behulp van een back-end voor de app Hallo richtlijnen onderwerp [registreren van uw app back-end](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="47ce9-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="47ce9-112">Deze zelfstudie bouwt voort op Hallo notification hub en project dat u hebt gemaakt in Hallo [aan de slag met Notification Hubs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="47ce9-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="47ce9-113">Deze zelfstudie is ook de vereiste toohello hello [Secure Push] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="47ce9-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="47ce9-114">Nadat u Hallo-stappen in deze zelfstudie hebt voltooid, kunt u doorgaan met toohello [Secure Push] zelfstudie, dat toont hoe toomodify Hallo code in deze zelfstudie toosend een push-melding veilig.</span><span class="sxs-lookup"><span data-stu-id="47ce9-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="47ce9-115">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="47ce9-115">Before you begin</span></span>
<span data-ttu-id="47ce9-116">We nemen uw feedback heel serieus.</span><span class="sxs-lookup"><span data-stu-id="47ce9-116">We do take your feedback seriously.</span></span> <span data-ttu-id="47ce9-117">Als er problemen bij het voltooien van dit onderwerp of aanbevelingen voor het verbeteren van de inhoud, zou wij stellen uw feedback onder Hallo van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="47ce9-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="47ce9-118">Hallo voltooid code voor deze zelfstudie kunt u vinden op GitHub [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="47ce9-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="47ce9-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="47ce9-119">Prerequisites</span></span>
<span data-ttu-id="47ce9-120">Voordat u deze zelfstudie begint, moet u al hebt voltooid deze zelfstudies voor Mobile Services:</span><span class="sxs-lookup"><span data-stu-id="47ce9-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="47ce9-121">[aan de slag met Notification Hubs]</span><span class="sxs-lookup"><span data-stu-id="47ce9-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="47ce9-122">U maakt de notification hub en Hallo app-naam reserveren en tooreceive meldingen registreren in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="47ce9-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="47ce9-123">Deze zelfstudie wordt ervan uitgegaan dat u al deze stappen hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="47ce9-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="47ce9-124">Als dit niet het geval is, volg stappen Hallo in [aan de slag met Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); in het bijzonder Hallo secties [uw app registreren voor Windows Store Hallo](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) en [configureren uw Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="47ce9-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="47ce9-125">In het bijzonder, zorg ervoor dat u hebt ingevoerd Hallo **pakket-SID** en **Clientgeheim** waarden in Hallo Hallo Portal **configureren** tabblad voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="47ce9-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="47ce9-126">Deze configuratieprocedure wordt beschreven in de sectie Hallo [uw Notification Hub configureren](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="47ce9-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="47ce9-127">Dit is een belangrijke stap: als het Hallo-referenties op Hallo portal komen niet overeen die zijn opgegeven voor Hallo-app die u kiest, Hallo push-melding niet slaagt.</span><span class="sxs-lookup"><span data-stu-id="47ce9-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="47ce9-128">Als u mobiele Apps in Azure App Service als uw back-endservice gebruikt, raadpleegt u Hallo [Mobile Apps-versie](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="47ce9-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="47ce9-129">Hallo-code voor het clientproject Hallo bijwerken</span><span class="sxs-lookup"><span data-stu-id="47ce9-129">Update hello code for hello client project</span></span>
<span data-ttu-id="47ce9-130">In deze sectie maakt u Hallo-code in Hallo-project u voltooid voor Hallo bijwerken [aan de slag met Notification Hubs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="47ce9-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="47ce9-131">Hallo moet al gekoppeld aan Hallo store en geconfigureerd voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="47ce9-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="47ce9-132">In deze sectie kunt u code toocall Hallo nieuwe WebAPI back-end toevoegen en gebruiken voor het registreren en verzenden van meldingen.</span><span class="sxs-lookup"><span data-stu-id="47ce9-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="47ce9-133">Open in Visual Studio Hallo Hallo oplossing die u hebt gemaakt voor Hallo [aan de slag met Notification Hubs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="47ce9-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="47ce9-134">Klik in Solution Explorer met de rechtermuisknop op Hallo **(Windows 8.1)** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="47ce9-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="47ce9-135">Aan de linkerkant Hallo en klikt u op **Online**.</span><span class="sxs-lookup"><span data-stu-id="47ce9-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="47ce9-136">In Hallo **Search** in het vak **HTTP-Client**.</span><span class="sxs-lookup"><span data-stu-id="47ce9-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="47ce9-137">Klik in de lijst met resultaten Hallo op **Microsoft HTTP-clientbibliotheken**, en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="47ce9-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="47ce9-138">Hallo-installatie voltooien.</span><span class="sxs-lookup"><span data-stu-id="47ce9-138">Complete hello installation.</span></span>
6. <span data-ttu-id="47ce9-139">Terug in Hallo NuGet **Search** in het vak **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="47ce9-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="47ce9-140">Hallo installeren **Json.NET** pakket en sluit Hallo NuGet Package Manager-venster.</span><span class="sxs-lookup"><span data-stu-id="47ce9-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="47ce9-141">Hallo bovenstaande stappen herhalen voor Hallo **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet-pakket voor Windows Phone-project Hallo.</span><span class="sxs-lookup"><span data-stu-id="47ce9-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="47ce9-142">Klik in Solution Explorer in Hallo **(Windows 8.1)** project, dubbelklikt u op **MainPage.xaml** tooopen in Hallo Visual Studio-editor.</span><span class="sxs-lookup"><span data-stu-id="47ce9-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="47ce9-143">In Hallo **MainPage.xaml** XML-code, vervangen Hallo `<Grid>` sectie Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="47ce9-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="47ce9-144">Deze code wordt toegevoegd met een gebruikersnaam en wachtwoord tekstvak die gebruiker Hallo verifieert.</span><span class="sxs-lookup"><span data-stu-id="47ce9-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="47ce9-145">Bovendien worden de tekstvakken voor meldingen het Hallo-bericht en Hallo gebruikersnaam label dat Hallo melding moet ontvangen toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="47ce9-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="47ce9-146">Klik in Solution Explorer in Hallo **(Windows Phone 8.1)** project, open **MainPage.xaml** en vervang Hallo Windows Phone 8.1 `<Grid>` sectie met de bovenstaande die dezelfde code.</span><span class="sxs-lookup"><span data-stu-id="47ce9-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="47ce9-147">Hallo-interface moet eruitzien vergelijkbare toowhats hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="47ce9-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="47ce9-148">Open in Solution Explorer Hallo **MainPage.xaml.cs** -bestand voor Hallo **(Windows 8.1)** en **(Windows Phone 8.1)** projecten.</span><span class="sxs-lookup"><span data-stu-id="47ce9-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="47ce9-149">Voeg de volgende Hallo `using` instructies boven Hallo van beide bestanden:</span><span class="sxs-lookup"><span data-stu-id="47ce9-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="47ce9-150">In **MainPage.xaml.cs** voor Hallo **(Windows 8.1)** en **(Windows Phone 8.1)** projecten, toevoegen na lid toohello hello `MainPage` klasse.</span><span class="sxs-lookup"><span data-stu-id="47ce9-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="47ce9-151">Ervoor tooreplace worden `<Enter Your Backend Endpoint>` Hello uw werkelijke back-end-eindpunt eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="47ce9-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="47ce9-152">Bijvoorbeeld `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="47ce9-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="47ce9-153">Hallo-code hieronder toohello MainPage klasse in toevoegen **MainPage.xaml.cs** voor Hallo **(Windows 8.1)** en **(Windows Phone 8.1)** projecten.</span><span class="sxs-lookup"><span data-stu-id="47ce9-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="47ce9-154">Hallo `PushClick` methode is Hallo klikt u op de handler voor Hallo **verzenden Push** knop.</span><span class="sxs-lookup"><span data-stu-id="47ce9-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="47ce9-155">Apparaten met een gebruikersnaam tag die overeenkomt met de Hallo Hallo back-end tootrigger een tooall melding ontvangt `to_tag` parameter.</span><span class="sxs-lookup"><span data-stu-id="47ce9-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="47ce9-156">Hallo-melding wordt verzonden als JSON-inhoud in de aanvraagtekst Hallo.</span><span class="sxs-lookup"><span data-stu-id="47ce9-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="47ce9-157">Hallo `LoginAndRegisterClick` methode is Hallo klikt u op de handler voor Hallo **aanmelden en registreren** knop.</span><span class="sxs-lookup"><span data-stu-id="47ce9-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="47ce9-158">Hallo basic worden opgeslagen verificatietoken in lokale opslag (Let erop dat dit verwijst naar een token uw verificatiemethode wordt gebruikt), gebruikt vervolgens `RegisterClient` tooregister voor meldingen met Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="47ce9-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. <span data-ttu-id="47ce9-159">Klik in Solution Explorer onder Hallo **gedeelde** project, open Hallo **App.xaml.cs** bestand.</span><span class="sxs-lookup"><span data-stu-id="47ce9-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="47ce9-160">Hallo-aanroep te vinden`InitNotificationsAsync()` in Hallo `OnLaunched()` gebeurtenis-handler.</span><span class="sxs-lookup"><span data-stu-id="47ce9-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="47ce9-161">Uitcommentariëren of te verwijderen van Hallo aanroep`InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="47ce9-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="47ce9-162">Hallo knop-handler die hierboven staan vermeld, wordt melding registraties initialiseren.</span><span class="sxs-lookup"><span data-stu-id="47ce9-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="47ce9-163">Klik in Solution Explorer met de rechtermuisknop op Hallo **gedeelde** project en klik vervolgens op **toevoegen**, en klik vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="47ce9-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="47ce9-164">Naam Hallo klasse **RegisterClient.cs**, klikt u vervolgens op **OK** toogenerate Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="47ce9-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="47ce9-165">Deze klasse wordt Hallo REST-aanroepen vereist toocontact Hallo back-end app verpakken in volgorde tooregister voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="47ce9-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="47ce9-166">Hallo ook lokaal worden opgeslagen *registrationIds* gemaakt door Hallo Notification Hub, zoals beschreven in [registreren van uw app back-end](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="47ce9-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="47ce9-167">Opmerking die gebruikmaakt van een verificatietoken opgeslagen in de lokale opslag, wanneer u klikt op Hallo **aanmelden en registreren** knop.</span><span class="sxs-lookup"><span data-stu-id="47ce9-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="47ce9-168">Voeg de volgende Hallo `using` instructies bovenaan Hallo Hallo RegisterClient.cs bestand:</span><span class="sxs-lookup"><span data-stu-id="47ce9-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="47ce9-169">Toevoegen van de volgende code in Hallo Hallo `RegisterClient` klasse definitie.</span><span class="sxs-lookup"><span data-stu-id="47ce9-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. <span data-ttu-id="47ce9-170">Sla al uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="47ce9-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="47ce9-171">Hallo toepassing testen</span><span class="sxs-lookup"><span data-stu-id="47ce9-171">Testing hello Application</span></span>
1. <span data-ttu-id="47ce9-172">Hallo toepassing starten op zowel Windows 8.1 en Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="47ce9-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="47ce9-173">U kunt voor Windows Phone 8.1 Hallo exemplaar uitvoeren in Hallo emulator of een daadwerkelijk apparaat.</span><span class="sxs-lookup"><span data-stu-id="47ce9-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="47ce9-174">Voer in Windows 8.1 Hallo exemplaar van Hallo-app, een **gebruikersnaam** en **wachtwoord** zoals weergegeven in onderstaande welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="47ce9-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="47ce9-175">Het moet verschillen van het Hallo-gebruikersnaam en het wachtwoord op Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="47ce9-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="47ce9-176">Klik op **aanmelden en registreren** en controleer of er wordt een dialoogvenster weergegeven dat u zich hebt aangemeld.</span><span class="sxs-lookup"><span data-stu-id="47ce9-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="47ce9-177">Hierdoor kan ook Hallo **verzenden Push** knop.</span><span class="sxs-lookup"><span data-stu-id="47ce9-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="47ce9-178">Voer op Hallo Windows Phone 8.1-exemplaar, een tekenreeks met de gebruiker in beide Hallo **gebruikersnaam** en **wachtwoord** velden, klikt u vervolgens op **aanmelden en registreren**.</span><span class="sxs-lookup"><span data-stu-id="47ce9-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="47ce9-179">Klik dan in Hallo **ontvanger gebruikersnaam Tag** en voer de naam van de gebruiker Hallo geregistreerd op Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="47ce9-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="47ce9-180">Geef een bericht en klik op **verzenden Push**.</span><span class="sxs-lookup"><span data-stu-id="47ce9-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="47ce9-181">Hallo alleen apparaten die zijn geregistreerd met de overeenkomende gebruikersnaam tag Hallo ontvangen melding het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="47ce9-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="47ce9-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="47ce9-182">Next Steps</span></span>
* <span data-ttu-id="47ce9-183">Als u wilt dat toosegment gebruikers op belangengroepen, raadpleegt u [Notification Hubs gebruiken toosend belangrijk nieuws].</span><span class="sxs-lookup"><span data-stu-id="47ce9-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="47ce9-184">meer informatie over hoe toolearn toouse Notification Hubs, Zie [richtlijnen voor Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="47ce9-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[aan de slag met Notification Hubs]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[Notification Hubs gebruiken toosend belangrijk nieuws]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
