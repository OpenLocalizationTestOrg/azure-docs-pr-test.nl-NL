---
title: Notification Hubs Secure Push aaaAzure
description: Meer informatie over hoe toosend beveiligde pushmeldingen in Azure. Codevoorbeelden geschreven in C# met Hallo .NET API.
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Azure Notification Hubs beveiligde Push
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Overzicht
Push notification-ondersteuning in Microsoft Azure kunt u tooaccess een eenvoudig te gebruiken, meerdere platforms, uitgebreid pushinfrastructuur, die sterk vereenvoudigd Hallo-implementatie van pushmeldingen voor consumenten- en enterprise-toepassingen voor mobiele telefoons -platforms.

Vanwege beperkingen voor tooregulatory of beveiliging kunt soms een toepassing tooinclude iets in Hallo-bericht dat via Hallo standaard push notification-infrastructuur kan niet worden verzonden. Deze zelfstudie wordt beschreven hoe tooachieve dezelfde ervaring Hallo door te sturen van gevoelige gegevens via een veilige en geverifieerde verbinding tussen clientapparaat Hallo en back-end Hallo app.

Op een hoog niveau is Hallo-stroom als volgt uit:

1. Hallo back-end van app:
   * Winkels beveiligde nettolading in back-enddatabase.
   * Hallo-ID van deze melding toohello apparaat (geen beveiligde gegevens verzonden) verzendt.
2. Hallo-app op Hallo apparaat tijdens het Hallo-bericht ontvangen:
   * Hallo-apparaat neemt contact Hallo back-end aanvragende Hallo beveiligde nettolading.
   * Hallo-app kunt Hallo nettolading weergeven als een melding op Hallo-apparaat.

Het is belangrijk dat in de voorgaande stroom Hallo (en in deze zelfstudie), gaan we ervan uit dat apparaat Hallo toonote slaat geen verificatietoken in lokale opslag nadat Hallo gebruiker zich aanmeldt. Dit garandeert een volledig naadloze ervaring als apparaat Hallo Hallo melding van beveiligde nettolading met dit token kan ophalen. Als uw toepassing slaat geen verificatietokens op Hallo-apparaat, of als deze tokens kunnen verlopen, hello apparaattoepassing bij Hallo melding moet worden weergegeven een algemene melding Hallo gebruiker toolaunch Hallo app te vragen. Hallo-app vervolgens verifieert de gebruiker Hallo en toont de nettolading van de Hallo-meldingen.

Deze Secure Push-zelfstudie laat zien hoe een push-melding toosend veilig. Hallo-zelfstudie bouwt voort op Hallo [gebruikers waarschuwen](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) zelfstudie, dus u moet eerst de voltooit Hallo stappen in deze zelfstudie.

> [!NOTE]
> Deze zelfstudie wordt ervan uitgegaan dat u hebt gemaakt en uw notification hub geconfigureerd zoals beschreven in [aan de slag met Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).
> Ook, houd er rekening mee dat Windows Phone 8.1 (geen Windows Phone) voor Windows-referenties vereist en achtergrondtaken werken niet op Windows Phone 8.0 of Silverlight 8.1. Voor Windows Store-toepassingen, kunt u meldingen via een achtergrondtaak ontvangen alleen als Hallo app vergrendelingsscherm ingeschakeld (Klik op Hallo checkbox in Hallo Appmanifest).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a>Hallo Windows Phone-Project wijzigen
1. In Hallo **NotifyUserWindowsPhone** project, het toevoegen van Hallo code tooApp.xaml.cs tooregister Hallo push achtergrondtaak te volgen. Toevoegen van de volgende regel code achter Hallo HALLO hallo `OnLaunched()` methode:
   
        RegisterBackgroundTask();
2. Voeg nog steeds in App.xaml.cs Hallo volgende code direct na Hallo `OnLaunched()` methode:
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. Voeg de volgende Hallo `using` instructies Hallo boven aan het bestand Hallo-App.xaml.cs:
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. Van Hallo **bestand** menu in Visual Studio, klikt u op **Alles opslaan**.

## <a name="create-hello-push-background-component"></a>Hallo Push achtergrond onderdeel maken
de volgende stap Hallo is toocreate Hallo push achtergrond onderdeel.

1. In Solution Explorer met de rechtermuisknop op het hoogste niveau knooppunt Hallo Hallo-oplossing (**oplossing SecurePush** in dit geval), klikt u vervolgens op **toevoegen**, klikt u vervolgens op **nieuw Project**.
2. Vouw **Store-Apps**, klikt u vervolgens op **Windows Phone-Apps**, klikt u vervolgens op **Windows Runtime-onderdeel (Windows Phone)**. Naam Hallo project **PushBackgroundComponent**, en klik vervolgens op **OK** toocreate Hallo project.
   
    ![][12]
3. Klik in Solution Explorer met de rechtermuisknop op Hallo **PushBackgroundComponent (Windows Phone 8.1)** project en klik vervolgens op **toevoegen**, klikt u vervolgens op **klasse**. Naam nieuwe klasse Hallo **PushBackgroundTask.cs**. Klik op **toevoegen** toogenerate Hallo-klasse.
4. Vervang de volledige inhoud Hallo Hallo **PushBackgroundComponent** naamruimtedefinitie Hello code de volgende, waarbij Hallo tijdelijke aanduiding vervangt `{back-end endpoint}` met Hallo backend-eindpunt is verkregen tijdens de implementatie van uw back-end:
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. Klik in Solution Explorer met de rechtermuisknop op Hallo **PushBackgroundComponent (Windows Phone 8.1)** project en klik vervolgens op **NuGet-pakketten beheren**.
6. Aan de linkerkant Hallo en klikt u op **Online**.
7. In Hallo **Search** in het vak **HTTP-Client**.
8. Klik in de lijst met resultaten Hallo op **Microsoft HTTP-clientbibliotheken**, en klik vervolgens op **installeren**. Hallo-installatie voltooien.
9. Terug in Hallo NuGet **Search** in het vak **Json.net**. Hallo installeren **Json.NET** pakket en klik op sluiten Hallo NuGet Package Manager-venster.
10. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **PushBackgroundTask.cs** bestand:
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. Klik in Solution Explorer in Hallo **NotifyUserWindowsPhone (Windows Phone 8.1)** project, met de rechtermuisknop op **verwijzingen**, klikt u vervolgens op **verwijzing toevoegen...** . In het dialoogvenster Reference Manager Hallo Hallo het selectievakje naast te**PushBackgroundComponent**, en klik vervolgens op **OK**.
12. Dubbelklik in Solution Explorer op **Package.appxmanifest** in Hallo **NotifyUserWindowsPhone (Windows Phone 8.1)** project. Onder **meldingen**stelt **Toast geschikt** te**Ja**.
    
    ![][3]
13. Nog steeds in **Package.appxmanifest**, klikt u op Hallo **declaraties** menu aan de bovenkant Hallo. In Hallo **beschikbaar declaraties** dropdown, klikt u op **achtergrondtaken**, en klik vervolgens op **toevoegen**.
14. In **Package.appxmanifest**onder **eigenschappen**, Controleer **Push-melding**.
15. In **Package.appxmanifest**onder **Appinstellingen**, type **PushBackgroundComponent.PushBackgroundTask** in Hallo **toegangspunt** veld.
    
    ![][13]
16. Van Hallo **bestand** menu, klikt u op **Alles opslaan**.

## <a name="run-hello-application"></a>Hallo toepassing uitvoeren
toorun toepassing hello, Hallo te volgen:

1. In Visual Studio, voert u Hallo **AppBackend** Web API-toepassing. Een ASP.NET-webpagina wordt weergegeven.
2. In Visual Studio, voert u Hallo **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone-app. Hallo Windows Phone-emulator wordt uitgevoerd en Hallo app automatisch wordt geladen.
3. In Hallo **NotifyUserWindowsPhone** app-gebruikersinterface een gebruikersnaam en wachtwoord invoeren. Deze kunnen zich een willekeurige tekenreeks, maar ze moet dezelfde waarde Hallo.
4. In Hallo **NotifyUserWindowsPhone** app-gebruikersinterface Klik **aanmelden en registreren**. Klik vervolgens op **push verzenden**.

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
