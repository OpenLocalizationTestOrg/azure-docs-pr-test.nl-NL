---
title: aaaGet de slag met Azure Notification Hubs voor universele Windows-Platform-Apps | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toopush meldingen tooa universele Windows-Platform-toepassing.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>Aan de slag met Notification Hubs voor Windows Universal Platform-apps
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Universal Windows Platform (UWP)-app.

In deze zelfstudie maakt u een lege Windows Store-app die pushmeldingen ontvangt via Hallo Windows Push Notification Service (WNS). Wanneer u klaar bent, moet u kunnen toouse push uw notification hub toobroadcast meldingen tooall Hallo apparaten waarop uw app wordt uitgevoerd.

## <a name="before-you-begin"></a>Voordat u begint
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Hallo voltooid code voor deze zelfstudie kunt u vinden op GitHub [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).

## <a name="prerequisites"></a>Vereisten
Deze zelfstudie vereist de volgende Hallo:

* [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) of later
* [Universal Windows App Development Tools geïnstalleerd](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* Een actief Azure-account <br/>Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F) voor meer informatie.
* Een actief Windows Store-account

Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Windows Universal Platform-apps.

## <a name="register-your-app-for-hello-windows-store"></a>Uw app registreren voor Hallo Windows Store
toosend push notifications tooUWP apps, moet u uw app toohello Windows Store koppelen. Vervolgens moet u uw notification hub toointegrate configureren met WNS.

1. Als u uw app nog niet hebt geregistreerd, gaat u toohello [Windows-ontwikkelaarscentrum](https://dev.windows.com/overview), meld u aan met uw Microsoft-account en klik vervolgens op **maakt een nieuwe app**.

2. Typ een naam voor uw app en klik op **App-naam reserveren**. Hiermee maakt u een nieuwe Windows Store-registratie voor uw app.

3. In Visual Studio kunt u een nieuw Visual C# Store-Apps-project maken met behulp van Universal Windows hello **lege App** sjabloon en klikt u op **OK**.

4. Accepteer de standaardinstellingen Hallo voor Hallo doel en minimale platformversies.

5. Klik in Solution Explorer met de rechtermuisknop op Hallo Windows Store-app-project, klikt u op **Store**, en klik vervolgens op **App aan Hallo Store koppelen...** . Hallo **uw App koppelen aan Windows Store Hallo** wizard wordt weergegeven.

6. Klik in de wizard Hallo zich aanmelden met je Microsoft-account.

7. Klik op Hallo-app die u in stap 2 hebt geregistreerd, klikt u op **volgende**, en klik vervolgens op **koppelen**. Hallo vereist Windows Store-registratie informatie toohello toepassingsmanifest wordt toegevoegd.

8. Terug op Hallo [Windows-ontwikkelaarscentrum](http://dev.windows.com/overview) voor uw nieuwe app pagina, klikt u op **Services**, klikt u op **Pushmeldingen**, en klik vervolgens op **WNS/MPNS**.

9. Klik op **Nieuwe melding**.

10. Klik op de sjabloon **Leeg (pop-up)** en klik vervolgens op **OK**.

11. Voer een **Naam** voor de melding en een visueel **Context**bericht in. Klik vervolgens op **Opslaan als concept**.

12. Navigeer toohello [Registratieportal toepassing](http://apps.dev.microsoft.com) en zich aanmelden.

13. Klik op de naam van uw toepassing. Noteer Hallo **Toepassingsgeheim** wachtwoord en Hallo **pakket beveiligings-id (SID)** zich in Hallo **Windows Store** platform-instellingen.

     > [AZURE.WARNING]
    Hallo toepassingsgeheim en pakket-SID zijn belangrijke beveiligingsreferenties. Deel deze waarden met niemand en distribueer ze niet met uw app.

## <a name="configure-your-notification-hub"></a>Uw Notification Hub configureren
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Selecteer Hallo <b>Notification Services</b> optie en Hallo <b>Windows (WNS)</b> optie. Voer vervolgens Hallo <b>toepassingsgeheim</b> wachtwoord in Hallo <b>beveiligingssleutel</b> veld. Voer uw <b>pakket-SID</b> waarde die u hebt verkregen van WNS in de vorige sectie Hallo en klik vervolgens op <b>opslaan</b>.</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

Uw notification hub is nu geconfigureerd toowork met WNS en u uw app Hallo verbinding tekenreeksen tooregister hebt en meldingen te verzenden.

## <a name="connect-your-app-toohello-notification-hub"></a>Verbinding maken met uw app toohello notification hub
1. Met de rechtermuisknop op het Hallo-oplossing in Visual Studio en klik vervolgens op **NuGet-pakketten beheren**.
   
    U ziet nu Hallo **NuGet-pakketten beheren** in het dialoogvenster.
2. Zoeken naar `WindowsAzure.Messaging.Managed` en klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.
   
    ![][20]
   
    Hiermee downloadt, installeert en wordt een verwijzing toohello Azure Messaging-bibliotheek voor Windows hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet-pakket</a>.
3. Open Hallo projectbestand App.XAML.cs en voeg de volgende Hallo `using` instructies. 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. Voeg ook in App.xaml.cs Hallo volgende **InitNotificationsAsync** methode definitie toohello **App** klasse:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    Deze code Hallo kanaal-URI voor Hallo app opgehaald uit WNS en vervolgens die kanaal-URI voor uw notification hub geregistreerd.
   
   > [!NOTE]
   > Zorg ervoor dat tooreplace 'uw hubnaam'-tijdelijke aanduiding met de naam van Hallo notification hub die wordt weergegeven in Azure Portal Hallo HALLO hallo. Hallo verbinding de tijdelijke aanduiding voor ook vervangen door Hallo **DefaultListenSharedAccessSignature** verbindingsreeks die u hebt verkregen via Hallo **toegangsbeleid** pagina van de Notification Hub in een vorige sectie.
   > 
   > 
5. Hallo boven aan het Hallo **OnLaunched** gebeurtenis-handler in App.xaml.cs toevoegen na de aanroep toohello nieuwe Hallo **InitNotificationsAsync** methode:
   
        InitNotificationsAsync();
   
    Dit zorgt ervoor dat Hallo kanaal-URI is geregistreerd in uw notification hub die elke keer Hallo-toepassing wordt gestart.
6. Druk op Hallo **F5** key toorun Hallo app. Een pop-upvenster met de registratiesleutel hello wordt weergegeven.

Uw app is nu gereed tooreceive pop-upmeldingen.

## <a name="send-notifications"></a>Meldingen verzenden
U kunt snel testen ontvangst van meldingen in uw app door meldingen te verzenden in Hallo [Azure Portal](https://portal.azure.com/) Hallo met **Test verzenden** knop op Hallo notification hub, zoals wordt weergegeven in onderstaande welkomstscherm.

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

Pushmeldingen worden gewoonlijk in een back-endservice zoals Mobile Services of ASP.NET verzonden met een compatibele bibliotheek. U kunt ook Hallo REST-API gebruiken direct toosend worden meldingsberichten als een bibliotheek niet beschikbaar voor uw back-end is. 

In deze zelfstudie wordt Houd het eenvoudig en alleen gedemonstreerd hoe u uw clientapp test door meldingen met behulp van Hallo .NET SDK voor notification hubs in een consoletoepassing in plaats van een back-endservice te verzenden. We raden aan Hallo [Notification Hubs gebruiken toopush meldingen toousers] Hallo volgende stap voor het verzenden van meldingen vanuit een ASP.NET-back-end zelfstudie. Hallo volgende methoden kan echter worden gebruikt voor het verzenden van meldingen:

* **REST-Interface**: U kunt meldingen ondersteunen op elk back-end-platform Hallo met [REST-interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure Notification Hubs .NET SDK**: In Hallo Nuget Package Manager voor Visual Studio, voert u [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [hoe toouse Notification Hubs met Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Azure Mobile Apps**: voor een voorbeeld van hoe u meldingen vanuit een mobiele App van Azure die geïntegreerd met Notification Hubs toosend Zie [pushmeldingen toevoegen voor mobiele Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: Zie voor een voorbeeld van hoe toosend meldingen met REST-API's Hallo ' hoe toouse Notification Hubs vanuit Java/PHP ' ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-console-app"></a>(Optioneel) Meldingen verzenden vanuit een console-app
toosend meldingen met een .NET-consoletoepassing Volg deze stappen. 

1. Klik met de rechtermuisknop Hallo-oplossing, selecteer **toevoegen** en **nieuw Project...** , en klik vervolgens onder **Visual C#**, klikt u op **Windows** en **consoletoepassing**, en klik op **OK**.
   
    Hiermee wordt een nieuwe Visual C# console toepassing toohello oplossing toegevoegd. U kunt dit ook in een afzonderlijke oplossing doen.

2. Klik in Visual Studio achtereenvolgens op **Extra**, **NuGet Package Manager** en **Package Manager-console**.
   
    Hiermee geeft Hallo Package Manager-Console in Visual Studio.
3. In Hallo venster Package Manager-Console, stelt u Hallo **standaardproject** tooyour nieuwe console toepassingsproject en vervolgens in het consolevenster hello, Hallo volgende opdracht wordt uitgevoerd:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Open het bestand Program.cs hello en voeg de volgende Hallo `using` instructie:
   
        using Microsoft.Azure.NotificationHubs;
5. In Hallo **programma** klasse, Hallo volgende methode toe te voegen:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > Zorg ervoor dat u het Hallo-verbindingsreeks die is **volledige** toegang niet **luisteren** toegang. Hallo toegangsrecht luisteren tekenreeks heeft geen machtigingen toosend meldingen.
   > 
   > 
6. Toevoegen van de volgende regels in Hallo Hallo **Main** methode:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Met de rechtermuisknop op het Hallo-consoletoepassingsproject in Visual Studio en klik op **instellen als opstartproject** tooset als opstartproject Hallo. Druk op Hallo **F5** sleutel toorun Hallo-toepassing.
   
    U ontvangt een pop-upmelding op alle geregistreerde apparaten. Hallo-app, klikt of tikt Hallo toast banner wordt geladen.

U vindt alle Hallo ondersteunde nettoladingen in Hallo [pop-upcatalogus], [tegelcatalogus], en [badge-overzicht] onderwerpen op MSDN.

## <a name="next-steps"></a>Volgende stappen
In dit eenvoudige voorbeeld verzonden u broadcast meldingen tooall uw Windows-apparaten via Hallo portal of een console-app. Hallo wordt aangeraden [Notification Hubs gebruiken toopush meldingen toousers] zelfstudie Hallo volgende stap. Hierin ziet u hoe toosend meldingen vanuit een ASP.NET-back-end met tags voor specifieke gebruikers tootarget.

Als u wilt dat toosegment gebruikers op belangengroepen, raadpleegt u [Notification Hubs gebruiken toosend belangrijk nieuws]. 

toolearn Zie voor meer algemene informatie over Notification Hubs [richtlijnen voor Notification Hubs](notification-hubs-push-notification-overview.md).

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[Notification Hubs gebruiken toopush meldingen toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Notification Hubs gebruiken toosend belangrijk nieuws]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[pop-upcatalogus]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[tegelcatalogus]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[badge-overzicht]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
