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
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a>Azure Notification Hubs gebruikers waarschuwen met .NET back-end
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Overzicht
Push notification-ondersteuning in Azure kunt u tooaccess een eenvoudig te gebruiken, multiplatform en uitgebreid pushinfrastructuur, die sterk vereenvoudigd Hallo-implementatie van pushmeldingen voor consumenten- en enterprise-toepassingen voor mobiele telefoons -platforms. Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa specifieke app gebruiker op een specifiek apparaat. Een ASP.NET WebAPI-back-end is gebruikte tooauthenticate clients. Hallo geverifieerde clientgebruiker en label automatisch worden toegevoegd door Hallo back-end toonotification registratie. Deze tag worden gebruikte toosend Hallo back-end toogenerate meldingen voor een specifieke gebruiker. Zie voor meer informatie over het registreren voor meldingen met behulp van een back-end voor de app Hallo richtlijnen onderwerp [registreren van uw app back-end](http://msdn.microsoft.com/library/dn743807.aspx). Deze zelfstudie bouwt voort op Hallo notification hub en project dat u hebt gemaakt in Hallo [aan de slag met Notification Hubs] zelfstudie.

Deze zelfstudie is ook de vereiste toohello hello [Secure Push] zelfstudie. Nadat u Hallo-stappen in deze zelfstudie hebt voltooid, kunt u doorgaan met toohello [Secure Push] zelfstudie, dat toont hoe toomodify Hallo code in deze zelfstudie toosend een push-melding veilig.

## <a name="before-you-begin"></a>Voordat u begint
We nemen uw feedback heel serieus. Als er problemen bij het voltooien van dit onderwerp of aanbevelingen voor het verbeteren van de inhoud, zou wij stellen uw feedback onder Hallo van Hallo pagina.

Hallo voltooid code voor deze zelfstudie kunt u vinden op GitHub [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). 

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u al hebt voltooid deze zelfstudies voor Mobile Services:

* [aan de slag met Notification Hubs]<br/>U maakt de notification hub en Hallo app-naam reserveren en tooreceive meldingen registreren in deze zelfstudie. Deze zelfstudie wordt ervan uitgegaan dat u al deze stappen hebt voltooid. Als dit niet het geval is, volg stappen Hallo in [aan de slag met Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); in het bijzonder Hallo secties [uw app registreren voor Windows Store Hallo](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) en [configureren uw Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). In het bijzonder, zorg ervoor dat u hebt ingevoerd Hallo **pakket-SID** en **Clientgeheim** waarden in Hallo Hallo Portal **configureren** tabblad voor uw notification hub. Deze configuratieprocedure wordt beschreven in de sectie Hallo [uw Notification Hub configureren](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Dit is een belangrijke stap: als het Hallo-referenties op Hallo portal komen niet overeen die zijn opgegeven voor Hallo-app die u kiest, Hallo push-melding niet slaagt.

> [!NOTE]
> Als u mobiele Apps in Azure App Service als uw back-endservice gebruikt, raadpleegt u Hallo [Mobile Apps-versie](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) van deze zelfstudie.
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a>Hallo-code voor het clientproject Hallo bijwerken
In deze sectie maakt u Hallo-code in Hallo-project u voltooid voor Hallo bijwerken [aan de slag met Notification Hubs] zelfstudie. Hallo moet al gekoppeld aan Hallo store en geconfigureerd voor uw notification hub. In deze sectie kunt u code toocall Hallo nieuwe WebAPI back-end toevoegen en gebruiken voor het registreren en verzenden van meldingen.

1. Open in Visual Studio Hallo Hallo oplossing die u hebt gemaakt voor Hallo [aan de slag met Notification Hubs] zelfstudie.
2. Klik in Solution Explorer met de rechtermuisknop op Hallo **(Windows 8.1)** project en klik vervolgens op **NuGet-pakketten beheren**.
3. Aan de linkerkant Hallo en klikt u op **Online**.
4. In Hallo **Search** in het vak **HTTP-Client**.
5. Klik in de lijst met resultaten Hallo op **Microsoft HTTP-clientbibliotheken**, en klik vervolgens op **installeren**. Hallo-installatie voltooien.
6. Terug in Hallo NuGet **Search** in het vak **Json.net**. Hallo installeren **Json.NET** pakket en sluit Hallo NuGet Package Manager-venster.
7. Hallo bovenstaande stappen herhalen voor Hallo **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet-pakket voor Windows Phone-project Hallo.
8. Klik in Solution Explorer in Hallo **(Windows 8.1)** project, dubbelklikt u op **MainPage.xaml** tooopen in Hallo Visual Studio-editor.
9. In Hallo **MainPage.xaml** XML-code, vervangen Hallo `<Grid>` sectie Hello code te volgen. Deze code wordt toegevoegd met een gebruikersnaam en wachtwoord tekstvak die gebruiker Hallo verifieert. Bovendien worden de tekstvakken voor meldingen het Hallo-bericht en Hallo gebruikersnaam label dat Hallo melding moet ontvangen toegevoegd:
   
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
10. Klik in Solution Explorer in Hallo **(Windows Phone 8.1)** project, open **MainPage.xaml** en vervang Hallo Windows Phone 8.1 `<Grid>` sectie met de bovenstaande die dezelfde code. Hallo-interface moet eruitzien vergelijkbare toowhats hieronder weergegeven.
    
    ![][13]
11. Open in Solution Explorer Hallo **MainPage.xaml.cs** -bestand voor Hallo **(Windows 8.1)** en **(Windows Phone 8.1)** projecten. Voeg de volgende Hallo `using` instructies boven Hallo van beide bestanden:
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. In **MainPage.xaml.cs** voor Hallo **(Windows 8.1)** en **(Windows Phone 8.1)** projecten, toevoegen na lid toohello hello `MainPage` klasse. Ervoor tooreplace worden `<Enter Your Backend Endpoint>` Hello uw werkelijke back-end-eindpunt eerder hebt verkregen. Bijvoorbeeld `http://mybackend.azurewebsites.net`.
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. Hallo-code hieronder toohello MainPage klasse in toevoegen **MainPage.xaml.cs** voor Hallo **(Windows 8.1)** en **(Windows Phone 8.1)** projecten.
    
    Hallo `PushClick` methode is Hallo klikt u op de handler voor Hallo **verzenden Push** knop. Apparaten met een gebruikersnaam tag die overeenkomt met de Hallo Hallo back-end tootrigger een tooall melding ontvangt `to_tag` parameter. Hallo-melding wordt verzonden als JSON-inhoud in de aanvraagtekst Hallo.
    
    Hallo `LoginAndRegisterClick` methode is Hallo klikt u op de handler voor Hallo **aanmelden en registreren** knop. Hallo basic worden opgeslagen verificatietoken in lokale opslag (Let erop dat dit verwijst naar een token uw verificatiemethode wordt gebruikt), gebruikt vervolgens `RegisterClient` tooregister voor meldingen met Hallo back-end.

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



1. Klik in Solution Explorer onder Hallo **gedeelde** project, open Hallo **App.xaml.cs** bestand. Hallo-aanroep te vinden`InitNotificationsAsync()` in Hallo `OnLaunched()` gebeurtenis-handler. Uitcommentariëren of te verwijderen van Hallo aanroep`InitNotificationsAsync()`. Hallo knop-handler die hierboven staan vermeld, wordt melding registraties initialiseren.

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. Klik in Solution Explorer met de rechtermuisknop op Hallo **gedeelde** project en klik vervolgens op **toevoegen**, en klik vervolgens op **klasse**. Naam Hallo klasse **RegisterClient.cs**, klikt u vervolgens op **OK** toogenerate Hallo-klasse.
   
   Deze klasse wordt Hallo REST-aanroepen vereist toocontact Hallo back-end app verpakken in volgorde tooregister voor pushmeldingen. Hallo ook lokaal worden opgeslagen *registrationIds* gemaakt door Hallo Notification Hub, zoals beschreven in [registreren van uw app back-end](http://msdn.microsoft.com/library/dn743807.aspx). Opmerking die gebruikmaakt van een verificatietoken opgeslagen in de lokale opslag, wanneer u klikt op Hallo **aanmelden en registreren** knop.
2. Voeg de volgende Hallo `using` instructies bovenaan Hallo Hallo RegisterClient.cs bestand:
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. Toevoegen van de volgende code in Hallo Hallo `RegisterClient` klasse definitie.
   
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
4. Sla al uw wijzigingen op.

## <a name="testing-hello-application"></a>Hallo toepassing testen
1. Hallo toepassing starten op zowel Windows 8.1 en Windows Phone 8.1. U kunt voor Windows Phone 8.1 Hallo exemplaar uitvoeren in Hallo emulator of een daadwerkelijk apparaat.
2. Voer in Windows 8.1 Hallo exemplaar van Hallo-app, een **gebruikersnaam** en **wachtwoord** zoals weergegeven in onderstaande welkomstscherm. Het moet verschillen van het Hallo-gebruikersnaam en het wachtwoord op Windows Phone.
3. Klik op **aanmelden en registreren** en controleer of er wordt een dialoogvenster weergegeven dat u zich hebt aangemeld. Hierdoor kan ook Hallo **verzenden Push** knop.
   
    ![][14]
4. Voer op Hallo Windows Phone 8.1-exemplaar, een tekenreeks met de gebruiker in beide Hallo **gebruikersnaam** en **wachtwoord** velden, klikt u vervolgens op **aanmelden en registreren**.
5. Klik dan in Hallo **ontvanger gebruikersnaam Tag** en voer de naam van de gebruiker Hallo geregistreerd op Windows 8.1. Geef een bericht en klik op **verzenden Push**.
   
    ![][16]
6. Hallo alleen apparaten die zijn geregistreerd met de overeenkomende gebruikersnaam tag Hallo ontvangen melding het Hallo-bericht.
   
    ![][15]

## <a name="next-steps"></a>Volgende stappen
* Als u wilt dat toosegment gebruikers op belangengroepen, raadpleegt u [Notification Hubs gebruiken toosend belangrijk nieuws].
* meer informatie over hoe toolearn toouse Notification Hubs, Zie [richtlijnen voor Notification Hubs].

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
