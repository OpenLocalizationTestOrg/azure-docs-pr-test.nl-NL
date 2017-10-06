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
# <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="90e4c-103">Push notifications tooyour Windows-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="90e4c-103">Add push notifications tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="90e4c-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="90e4c-104">Overview</span></span>
<span data-ttu-id="90e4c-105">In deze zelfstudie maakt u een push notifications toohello toevoegen [snel starten van Windows](app-service-mobile-windows-store-dotnet-get-started.md) project, zodat een push-melding toohello apparaat verzonden telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="90e4c-105">In this tutorial, you add push notifications toohello [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="90e4c-106">Als u geen gebruik Hallo snel starten-serverproject gedownload, u moet Hallo push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="90e4c-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="90e4c-107">Zie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="90e4c-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="90e4c-108"><a name="configure-hub"></a>Een Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="90e4c-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="90e4c-109">Uw app voor pushmeldingen registreren</span><span class="sxs-lookup"><span data-stu-id="90e4c-109">Register your app for push notifications</span></span>
<span data-ttu-id="90e4c-110">U moet toosubmit uw toohello app Windows Store en vervolgens uw project server toointegrate configureren met Windows Notification Services (WNS) toosend push.</span><span class="sxs-lookup"><span data-stu-id="90e4c-110">You need toosubmit your app toohello Windows Store, then configure your server project toointegrate with Windows Notification Services (WNS) toosend push.</span></span>

1. <span data-ttu-id="90e4c-111">Klik in Visual Studio Solution Explorer met de rechtermuisknop op Hallo UWP-app-project, klikt u op **Store** > **App aan Hallo Store koppelen...** .</span><span class="sxs-lookup"><span data-stu-id="90e4c-111">In Visual Studio Solution Explorer, right-click hello UWP app project, click **Store** > **Associate App with hello Store...**.</span></span>

    ![App aan Windows Store koppelen](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="90e4c-113">Klik in de wizard Hallo op **volgende**, meld u aan met uw Microsoft-account, typ een naam voor uw app in **een nieuwe appnaam reserveren**, klikt u vervolgens op **Reserve**.</span><span class="sxs-lookup"><span data-stu-id="90e4c-113">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="90e4c-114">Klik na registratie van de app Hallo Hallo is gemaakt, selecteer nieuwe app-naam **volgende**, en klik vervolgens op **koppelen**.</span><span class="sxs-lookup"><span data-stu-id="90e4c-114">After hello app registration is successfully created, select hello new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="90e4c-115">Hallo vereist Windows Store-registratie informatie toohello toepassingsmanifest wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="90e4c-115">This adds hello required Windows Store registration information toohello application manifest.</span></span>  
4. <span data-ttu-id="90e4c-116">Navigeer toohello [Windows-ontwikkelaarscentrum](https://dev.windows.com/en-us/overview), voor het aanmelden met je Microsoft-account, klikt u op Hallo nieuwe app-registratie in **mijn apps**, vouw vervolgens **Services**  >  **Pushmeldingen**.</span><span class="sxs-lookup"><span data-stu-id="90e4c-116">Navigate toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click hello new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="90e4c-117">In Hallo **Pushmeldingen** pagina, klikt u op **Live Services site** onder **Microsoft Azure Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="90e4c-117">In hello **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="90e4c-118">In de registratiepagina hello, maak een notitie van Hallo waarde onder **toepassing geheimen** en Hallo **pakket-SID**, die vervolgens gebruikt u tooconfigure back-end van uw mobiele app.</span><span class="sxs-lookup"><span data-stu-id="90e4c-118">In hello registration page, make a note of hello value under **Application secrets** and hello **Package SID**, which you will next use tooconfigure your mobile app backend.</span></span>

    ![App aan Windows Store koppelen](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="90e4c-120">Hallo-clientgeheim en de pakket-SID zijn belangrijke beveiligingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="90e4c-120">hello client secret and package SID are important security credentials.</span></span> <span data-ttu-id="90e4c-121">Deel deze waarden met niemand en distribueer ze niet met uw app.</span><span class="sxs-lookup"><span data-stu-id="90e4c-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="90e4c-122">Hallo **toepassings-Id** met Hallo geheime tooconfigure Microsoft-Account verificatie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="90e4c-122">hello **Application Id** is used with hello secret tooconfigure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a><span data-ttu-id="90e4c-123">Hallo back-end toosend-pushmeldingen configureren</span><span class="sxs-lookup"><span data-stu-id="90e4c-123">Configure hello backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="90e4c-124"><a id="update-service"></a>Hallo server toosend pushmeldingen bijwerken</span><span class="sxs-lookup"><span data-stu-id="90e4c-124"><a id="update-service"></a>Update hello server toosend push notifications</span></span>
<span data-ttu-id="90e4c-125">Gebruik Hallo procedure hieronder die overeenkomt met uw back-end-projecttype&mdash;beide [.NET back-end](#dotnet) of [back-end voor Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="90e4c-125">Use hello procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="90e4c-126"><a name="dotnet"></a>.NET-back-endproject</span><span class="sxs-lookup"><span data-stu-id="90e4c-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="90e4c-127">In Visual Studio met de rechtermuisknop op het serverproject Hallo en klikt u op **NuGet-pakketten beheren**, zoekt u Microsoft.Azure.NotificationHubs en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="90e4c-127">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="90e4c-128">Hiermee installeert u Hallo Notification Hubs-clientbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="90e4c-128">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="90e4c-129">Vouw **domeincontrollers**, opent u TodoItemController.cs en voeg de volgende Hallo using-instructies:</span><span class="sxs-lookup"><span data-stu-id="90e4c-129">Expand **Controllers**, open TodoItemController.cs, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="90e4c-130">In Hallo **PostTodoItem** methode toevoegen Hallo code te volgen na de aanroep Hallo**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="90e4c-130">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>

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

    <span data-ttu-id="90e4c-131">Deze code vertelt Hallo notification hub toosend een push-melding nadat een nieuw item invoegen is.</span><span class="sxs-lookup"><span data-stu-id="90e4c-131">This code tells hello notification hub toosend a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="90e4c-132">Hallo serverproject publiceren.</span><span class="sxs-lookup"><span data-stu-id="90e4c-132">Republish hello server project.</span></span>

### <span data-ttu-id="90e4c-133"><a name="nodejs"></a>Back-endproject node.js</span><span class="sxs-lookup"><span data-stu-id="90e4c-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="90e4c-134">Als u dit nog niet hebt gedaan, [Hallo Quick Start-project downloaden](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) of gebruik anders Hallo [online-editor in Azure-portal Hallo](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="90e4c-134">If you haven't already done so, [download hello quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="90e4c-135">Vervang bestaande code in Hallo todoitem.js bestand Hallo door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="90e4c-135">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

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

    <span data-ttu-id="90e4c-136">Hierdoor wordt een pop-upmelding WNS hello item.text met tijdens het invoegen van een nieuwe takenlijstitem verzonden.</span><span class="sxs-lookup"><span data-stu-id="90e4c-136">This sends a WNS toast notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="90e4c-137">Wanneer u bewerkt Hallo-bestand op uw lokale computer, opnieuw publiceren Hallo serverproject.</span><span class="sxs-lookup"><span data-stu-id="90e4c-137">When editing hello file on your local computer, republish hello server project.</span></span>

## <span data-ttu-id="90e4c-138"><a id="update-app"></a>Push notifications tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="90e4c-138"><a id="update-app"></a>Add push notifications tooyour app</span></span>
<span data-ttu-id="90e4c-139">Vervolgens moet uw app registreren voor pushmeldingen op opstarten.</span><span class="sxs-lookup"><span data-stu-id="90e4c-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="90e4c-140">Als u verificatie al hebt ingeschakeld, moet u die Hallo-gebruiker zich aanmeldt voordat u probeert tooregister voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="90e4c-140">When you have already enabled authentication, make sure that hello user signs-in before trying tooregister for push notifications.</span></span>

1. <span data-ttu-id="90e4c-141">Open Hallo **App.xaml.cs** bestand project en voeg de volgende Hallo `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="90e4c-141">Open hello **App.xaml.cs** project file and add hello following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="90e4c-142">In hetzelfde bestand Hallo, voeg de volgende Hallo **InitNotificationsAsync** methode definitie toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="90e4c-142">In hello same file, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="90e4c-143">Deze code Hallo ChannelURI voor Hallo app opgehaald uit WNS en wordt vervolgens die ChannelURI geregistreerd met uw App Service-mobiele App.</span><span class="sxs-lookup"><span data-stu-id="90e4c-143">This code retrieves hello ChannelURI for hello app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="90e4c-144">Hallo boven aan het Hallo **OnLaunched** gebeurtenis-handler in **App.xaml.cs**, Hallo toevoegen **asynchrone** aanpassingsfunctie toohello methodedefinitie en Hallo volgende aanroep toohello nieuwe toevoegen **InitNotificationsAsync** methode, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="90e4c-144">At hello top of hello **OnLaunched** event handler in **App.xaml.cs**, add hello **async** modifier toohello method definition and add hello following call toohello new **InitNotificationsAsync** method, as in hello following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="90e4c-145">Dit zorgt ervoor dat Hallo die tijdelijke ChannelURI wordt geregistreerd telkens wanneer de toepassing hello wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="90e4c-145">This guarantees that hello short-lived ChannelURI is registered each time hello application is launched.</span></span>
4. <span data-ttu-id="90e4c-146">Uw UWP-app-project opnieuw worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="90e4c-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="90e4c-147">Uw app is nu gereed tooreceive pop-upmeldingen.</span><span class="sxs-lookup"><span data-stu-id="90e4c-147">Your app is now ready tooreceive toast notifications.</span></span>

## <span data-ttu-id="90e4c-148"><a id="test"></a>Pushmeldingen testen in uw app</span><span class="sxs-lookup"><span data-stu-id="90e4c-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="90e4c-149"><a id="more"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="90e4c-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="90e4c-150">Meer informatie over pushmeldingen:</span><span class="sxs-lookup"><span data-stu-id="90e4c-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="90e4c-151">Hoe toouse Hallo-client voor mobiele Apps van Azure beheerd</span><span class="sxs-lookup"><span data-stu-id="90e4c-151">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="90e4c-152">Sjablonen bieden u de flexibiliteit toosend platformoverschrijdende pushes en gelokaliseerde pushes.</span><span class="sxs-lookup"><span data-stu-id="90e4c-152">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="90e4c-153">Meer informatie over hoe tooregister sjablonen.</span><span class="sxs-lookup"><span data-stu-id="90e4c-153">Learn how tooregister templates.</span></span>
* [<span data-ttu-id="90e4c-154">Push notification problemen vaststellen</span><span class="sxs-lookup"><span data-stu-id="90e4c-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="90e4c-155">Er zijn diverse redenen waarom meldingen mogelijk ophalen verwijderd of kunnen niet eindigen op apparaten.</span><span class="sxs-lookup"><span data-stu-id="90e4c-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="90e4c-156">Dit onderwerp leest u hoe tooanalyze en uitzoeken Hallo hoofdmap push notification fouten veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="90e4c-156">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="90e4c-157">Houd rekening met tooone Hallo volgende zelfstudies verder te gaan:</span><span class="sxs-lookup"><span data-stu-id="90e4c-157">Consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="90e4c-158">Verificatie tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="90e4c-158">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="90e4c-159">Meer informatie over hoe tooauthenticate gebruikers van uw app met een id-provider.</span><span class="sxs-lookup"><span data-stu-id="90e4c-159">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="90e4c-160">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="90e4c-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="90e4c-161">Meer informatie over hoe tooadd offline ondersteuning bieden voor uw app met een back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="90e4c-161">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="90e4c-162">Offlinesynchronisatie kunnen eindgebruikers toointeract met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="90e4c-162">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
