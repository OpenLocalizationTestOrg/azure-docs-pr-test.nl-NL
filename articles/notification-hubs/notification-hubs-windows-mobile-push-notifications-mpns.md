---
title: aaaSending pushmeldingen verzenden met Azure Notification Hubs op Windows Phone | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toopush meldingen tooa Windows Phone 8 of Windows Phone 8.1 Silverlight-toepassing.
services: notification-hubs
documentationcenter: windows
keywords: pushmelding,pushmelding,windows phone-push
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>Pushmeldingen verzenden met Azure Notification Hubs op Windows Phone
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Overzicht
> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F) voor meer informatie.
> 
> 

Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Windows Phone 8 of Windows Phone 8.1 Silverlight-toepassing. Als u ontwikkelt voor Windows Phone 8.1 (zonder Silverlight), raadpleegt u toohello [universele Windows-](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) versie.
In deze zelfstudie maakt u een lege Windows Phone 8-app die pushmeldingen ontvangt via Hallo Microsoft Push Notification Service (MPNS). Wanneer u klaar bent, moet u kunnen toouse push uw notification hub toobroadcast meldingen tooall Hallo apparaten waarop uw app wordt uitgevoerd.

> [!NOTE]
> Hallo Notification Hubs Windows Phone SDK biedt geen ondersteuning voor het gebruik van Hallo Windows Push Notification Service (WNS) met Windows Phone 8.1 Silverlight-apps. toouse WNS (in plaats van MPNS) met Windows Phone 8.1 Silverlight-apps, volgt u Hallo [Notification Hubs - Windows Phone Silverlight-zelfstudie], waarin REST API's.
> 
> 

Hallo zelfstudie wordt Hallo eenvoudige scenario uitzenden met Notification hubs beschreven.

## <a name="prerequisites"></a>Vereisten
Deze zelfstudie vereist de volgende Hallo:

* [Visual Studio 2012 Express voor Windows Phone] of een hogere versie.

Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Windows Phone 8-apps.

## <a name="create-your-notification-hub"></a>Een Notification Hub maken
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Klik op Hallo <b>Notification Services</b> sectie (binnen <i>instellingen</i>), klikt u op <b>Windows Phone (MPNS)</b> en klik vervolgens op Hallo <b>niet-geverifieerde pushmeldingen inschakelen </b> selectievakje.</p>
</li>
</ol>

&emsp;&emsp;![Azure Portal - Niet-geverifieerde pushmeldingen inschakelen](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

De hub is nu gemaakt en geconfigureerd toosend niet-geverifieerde meldingen voor Windows Phone.

> [!NOTE]
> In deze zelfstudie wordt MPNS in niet-geverifieerde modus gebruikt. Niet-geverifieerde MPNS-modus gelden beperkingen voor meldingen dat u tooeach kanaal kunt verzenden. Notification Hubs ondersteunt [geverifieerde MPNS-modus](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) doordat u tooupload uw certificaat.
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>Verbinding maken met uw app toohello notification hub
1. Maak een nieuwe Windows Phone 8-toepassing in Visual Studio.
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    In Visual Studio 2013 Update 2 of hoger maakt u daarentegen een Windows Phone Silverlight-toepassing.
   
    ![Visual Studio - Nieuw project - Lege app - Windows Phone Silverlight][11]
2. Met de rechtermuisknop op het Hallo-oplossing in Visual Studio en klik vervolgens op **NuGet-pakketten beheren**.
   
    U ziet nu Hallo **NuGet-pakketten beheren** in het dialoogvenster.
3. Zoeken naar `WindowsAzure.Messaging.Managed` en klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.
   
    ![Visual Studio - NuGet Package Manager][20]
   
    Hiermee downloadt, installeert en wordt een verwijzing toohello Azure Messaging-bibliotheek voor Windows hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet-pakket</a>.
4. Open Hallo bestand App.xaml.cs en voeg de volgende Hallo `using` instructies:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. Hallo code Hallo boven aan het volgende toevoegen **Application_Launching** methode in App.xaml.cs:
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > Hallo waarde **MyPushChannel** is een index die is gebruikt toolookup een bestaand kanaal in Hallo [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) verzameling. Als het kanaal niet wordt gevonden, maakt u een nieuwe vermelding met die naam.
   > 
   > 
   
    Zorg ervoor dat tooinsert Hallo-naam van uw hub en Hallo-verbindingsreeks aangeroepen **DefaultListenSharedAccessSignature** die u hebt verkregen in de vorige sectie Hallo.
    Deze code Hallo kanaal-URI voor Hallo app opgehaald uit MPNS en vervolgens die kanaal-URI voor uw notification hub geregistreerd. Ook wordt hiermee gegarandeerd dat Hallo kanaal-URI is geregistreerd in uw notification hub die elke keer Hallo-toepassing wordt gestart.
   
   > [!NOTE]
   > Deze zelfstudie wordt een toast-melding toohello apparaat verzonden. Wanneer u een tegelmelding verzendt, moet u in plaats daarvan Hallo aanroepen **BindToShellTile** methode op het Hallo-kanaal. toosupport toast en de tegel meldingen, roept **BindToShellTile** en **BindToShellToast**.
   > 
   > 
6. Vouw in Solution Explorer **eigenschappen**Open Hallo `WMAppManifest.xml` bestand, klikt u op Hallo **mogelijkheden** tabblad en zorg ervoor dat Hallo **ID_CAP_PUSH_NOTIFICATION** is ingeschakeld.
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. Druk op Hallo `F5` key toorun Hallo app.
   
    Een registratiebericht wordt weergegeven in het Hallo-app.
8. Sluit Hallo-app.  
   
   > [!NOTE]
   > een pop-upmelding tooreceive, Hallo toepassing moet niet worden uitgevoerd op de voorgrond Hallo.
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>Pushmeldingen verzenden vanuit uw back-end
U kunt pushmeldingen verzenden via Notification Hubs vanuit elke back-end via openbare Hallo <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST-interface</a>. In deze zelfstudie verzendt u pushmeldingen met een .NET-consoletoepassing. 

Zie voor een voorbeeld van hoe toosend pushmeldingen vanuit een back-end voor een ASP.NET WebAPI die geïntegreerd met Notification Hubs [Azure Notification Hubs gebruikers waarschuwen met .NET back-end](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).  

Voor een voorbeeld van hoe toosend pushmeldingen met Hallo [REST-API's](https://msdn.microsoft.com/library/azure/dn223264.aspx), Bekijk [hoe toouse Notification Hubs vanuit Java](notification-hubs-java-push-notification-tutorial.md) en [hoe toouse Notification Hubs vanuit PHP](notification-hubs-php-push-notification-tutorial.md) .

1. Klik met de rechtermuisknop Hallo-oplossing, selecteer **toevoegen** en **nieuw Project...** , en klik vervolgens onder **Visual C#**, klikt u op **Windows** en **consoletoepassing**, en klik op **OK**.
   
       ![Visual Studio - New Project - Console Application][6]
   
    Hiermee wordt een nieuwe Visual C# console toepassing toohello oplossing toegevoegd. U kunt dit ook in een afzonderlijke oplossing doen.
2. Klik achtereenvolgens op **Extra**, **Library Package Manager** en **Package Manager-console**.
   
    Hallo Package Manager-Console worden weergegeven.
3. In Hallo **Package Manager Console** venster, set Hallo **standaardproject** tooyour nieuwe console toepassingsproject en vervolgens in het consolevenster hello, Hallo volgende opdracht wordt uitgevoerd:
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.
4. Open Hallo `Program.cs` -bestand en voeg de volgende Hallo `using` instructie:
   
        using Microsoft.Azure.NotificationHubs;
5. In Hallo `Program` klasse, Hallo volgende methode toe te voegen:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    Zorg ervoor dat tooreplace hello `<hub name>` tijdelijke aanduiding met de naam van Hallo notification hub die wordt weergegeven in de portal Hallo Hallo. Vervang ook Hallo connection string tijdelijke aanduiding door Hallo verbindingsreeks genaamd **DefaultFullSharedAccessSignature** die u hebt verkregen in de sectie Hallo 'Uw notification hub configureren'.
   
   > [!NOTE]
   > Zorg ervoor dat u de verbindingsreeks Hallo met **volledige** toegang niet **luisteren** toegang. Hallo toegangsrecht luisteren tekenreeks heeft geen machtigingen toosend pushmeldingen.
   > 
   > 
6. Toevoegen van Hallo volgende regel in uw `Main` methode:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Met uw Windows Phone-emulator wordt uitgevoerd en uw app gesloten, stel Hallo consoletoepassingsproject als Hallo standaard opstartproject en druk vervolgens op Hallo `F5` key toorun Hallo app.
   
    U ontvangt een pop-uppushmelding. Hallo-app te tikken op Hallo toast banner worden geladen.

U vindt alle mogelijke nettoladingen van Hallo in Hallo [pop-upcatalogus] en [tegelcatalogus] onderwerpen op MSDN.

## <a name="next-steps"></a>Volgende stappen
In dit eenvoudige voorbeeld hebt u uitgezonden push notifications tooall uw Windows Phone 8-apparaten. 

In de volgorde tootarget specifieke gebruikers, raadpleeg dan toohello [Notification Hubs gebruiken toopush meldingen toousers] zelfstudie. 

Als u wilt dat toosegment gebruikers op belangengroepen, kunt u lezen [Notification Hubs gebruiken toosend belangrijk nieuws]. 

Meer informatie over het toouse Notification Hubs in [richtlijnen voor Notification Hubs].

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express voor Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[Notification Hubs gebruiken toopush meldingen toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Notification Hubs gebruiken toosend belangrijk nieuws]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[pop-upcatalogus]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[tegelcatalogus]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Notification Hubs - Windows Phone Silverlight-zelfstudie]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

