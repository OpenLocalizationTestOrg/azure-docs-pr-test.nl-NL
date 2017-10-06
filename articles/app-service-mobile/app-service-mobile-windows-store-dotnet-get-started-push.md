---
title: aaaAdd push notifications tooyour Universal Windows Platform (UWP)-app | Microsoft Docs
description: Meer informatie over hoe toouse Azure App Service Mobile Apps en Azure Notification Hubs toosend push notifications tooyour Universal Windows Platform (UWP)-app.
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a>Push notifications tooyour Windows-app toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Overzicht
In deze zelfstudie maakt u een push notifications toohello toevoegen [snel starten van Windows](app-service-mobile-windows-store-dotnet-get-started.md) project, zodat een push-melding toohello apparaat verzonden telkens wanneer een record wordt ingevoegd.

Als u geen gebruik Hallo snel starten-serverproject gedownload, u moet Hallo push notification-uitbreidingspakket. Zie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor meer informatie.

## <a name="configure-hub"></a>Een Notification Hub configureren
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a>Uw app voor pushmeldingen registreren
U moet toosubmit uw toohello app Windows Store en vervolgens uw project server toointegrate configureren met Windows Notification Services (WNS) toosend push.

1. Klik in Visual Studio Solution Explorer met de rechtermuisknop op Hallo UWP-app-project, klikt u op **Store** > **App aan Hallo Store koppelen...** .

    ![App aan Windows Store koppelen](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. Klik in de wizard Hallo op **volgende**, meld u aan met uw Microsoft-account, typ een naam voor uw app in **een nieuwe appnaam reserveren**, klikt u vervolgens op **Reserve**.
3. Klik na registratie van de app Hallo Hallo is gemaakt, selecteer nieuwe app-naam **volgende**, en klik vervolgens op **koppelen**. Hallo vereist Windows Store-registratie informatie toohello toepassingsmanifest wordt toegevoegd.  
4. Navigeer toohello [Windows-ontwikkelaarscentrum](https://dev.windows.com/en-us/overview), voor het aanmelden met je Microsoft-account, klikt u op Hallo nieuwe app-registratie in **mijn apps**, vouw vervolgens **Services**  >  **Pushmeldingen**.
5. In Hallo **Pushmeldingen** pagina, klikt u op **Live Services site** onder **Microsoft Azure Mobile Services**.
6. In de registratiepagina hello, maak een notitie van Hallo waarde onder **toepassing geheimen** en Hallo **pakket-SID**, die vervolgens gebruikt u tooconfigure back-end van uw mobiele app.

    ![App aan Windows Store koppelen](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > Hallo-clientgeheim en de pakket-SID zijn belangrijke beveiligingsreferenties. Deel deze waarden met niemand en distribueer ze niet met uw app. Hallo **toepassings-Id** met Hallo geheime tooconfigure Microsoft-Account verificatie wordt gebruikt.
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a>Hallo back-end toosend-pushmeldingen configureren
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a>Hallo server toosend pushmeldingen bijwerken
Gebruik Hallo procedure hieronder die overeenkomt met uw back-end-projecttype&mdash;beide [.NET back-end](#dotnet) of [back-end voor Node.js](#nodejs).

### <a name="dotnet"></a>.NET-back-endproject
1. In Visual Studio met de rechtermuisknop op het serverproject Hallo en klikt u op **NuGet-pakketten beheren**, zoekt u Microsoft.Azure.NotificationHubs en klik vervolgens op **installeren**. Hiermee installeert u Hallo Notification Hubs-clientbibliotheek.
2. Vouw **domeincontrollers**, opent u TodoItemController.cs en voeg de volgende Hallo using-instructies:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. In Hallo **PostTodoItem** methode toevoegen Hallo code te volgen na de aanroep Hallo**InsertAsync**:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Deze code vertelt Hallo notification hub toosend een push-melding nadat een nieuw item invoegen is.
4. Hallo serverproject publiceren.

### <a name="nodejs"></a>Back-endproject node.js
1. Als u dit nog niet hebt gedaan, [Hallo Quick Start-project downloaden](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) of gebruik anders Hallo [online-editor in Azure-portal Hallo](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Vervang bestaande code in Hallo todoitem.js bestand Hallo door Hallo volgende:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    Hierdoor wordt een pop-upmelding WNS hello item.text met tijdens het invoegen van een nieuwe takenlijstitem verzonden.
3. Wanneer u bewerkt Hallo-bestand op uw lokale computer, opnieuw publiceren Hallo serverproject.

## <a id="update-app"></a>Push notifications tooyour app toevoegen
Vervolgens moet uw app registreren voor pushmeldingen op opstarten. Als u verificatie al hebt ingeschakeld, moet u die Hallo-gebruiker zich aanmeldt voordat u probeert tooregister voor pushmeldingen.

1. Open Hallo **App.xaml.cs** bestand project en voeg de volgende Hallo `using` instructies:

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. In hetzelfde bestand Hallo, voeg de volgende Hallo **InitNotificationsAsync** methode definitie toohello **App** klasse:

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    Deze code Hallo ChannelURI voor Hallo app opgehaald uit WNS en wordt vervolgens die ChannelURI geregistreerd met uw App Service-mobiele App.
3. Hallo boven aan het Hallo **OnLaunched** gebeurtenis-handler in **App.xaml.cs**, Hallo toevoegen **asynchrone** aanpassingsfunctie toohello methodedefinitie en Hallo volgende aanroep toohello nieuwe toevoegen **InitNotificationsAsync** methode, zoals in het volgende voorbeeld Hallo:

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    Dit zorgt ervoor dat Hallo die tijdelijke ChannelURI wordt geregistreerd telkens wanneer de toepassing hello wordt gestart.
4. Uw UWP-app-project opnieuw worden opgebouwd. Uw app is nu gereed tooreceive pop-upmeldingen.

## <a id="test"></a>Pushmeldingen testen in uw app
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a>Volgende stappen
Meer informatie over pushmeldingen:

* [Hoe toouse Hallo-client voor mobiele Apps van Azure beheerd](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  Sjablonen bieden u de flexibiliteit toosend platformoverschrijdende pushes en gelokaliseerde pushes. Meer informatie over hoe tooregister sjablonen.
* [Push notification problemen vaststellen](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  Er zijn diverse redenen waarom meldingen mogelijk ophalen verwijderd of kunnen niet eindigen op apparaten. Dit onderwerp leest u hoe tooanalyze en uitzoeken Hallo hoofdmap push notification fouten veroorzaken.

Houd rekening met tooone Hallo volgende zelfstudies verder te gaan:

* [Verificatie tooyour app toevoegen](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Meer informatie over hoe tooauthenticate gebruikers van uw app met een id-provider.
* [Offlinesynchronisatie voor uw app inschakelen](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Meer informatie over hoe tooadd offline ondersteuning bieden voor uw app met een back-end voor de mobiele App. Offlinesynchronisatie kunnen eindgebruikers toointeract met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
