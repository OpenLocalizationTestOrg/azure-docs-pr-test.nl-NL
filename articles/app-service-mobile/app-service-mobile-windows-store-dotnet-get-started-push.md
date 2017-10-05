---
title: Pushmeldingen toevoegen aan uw app Universal Windows Platform (UWP) | Microsoft Docs
description: Informatie over het gebruik van Azure App Service Mobile Apps en Azure Notification Hubs pushmeldingen verzendt naar uw app Universal Windows Platform (UWP).
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
ms.openlocfilehash: a14bb0320c1f6a563f766a6a0fad5cf556fe7b70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="574ae-103">Pushmeldingen toevoegen aan uw Windows-app</span><span class="sxs-lookup"><span data-stu-id="574ae-103">Add push notifications to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="574ae-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="574ae-104">Overview</span></span>
<span data-ttu-id="574ae-105">In deze zelfstudie hebt u pushmeldingen toevoegen de [snel starten van Windows](app-service-mobile-windows-store-dotnet-get-started.md) project, zodat een pushmelding wordt verzonden naar het apparaat telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="574ae-105">In this tutorial, you add push notifications to the [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="574ae-106">Als u het gedownloade quick start-serverproject niet gebruikt, moet u het push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="574ae-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="574ae-107">Zie [werken met de .NET-back-endserver SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="574ae-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="574ae-108"><a name="configure-hub"></a>Een Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="574ae-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="574ae-109">Uw app voor pushmeldingen registreren</span><span class="sxs-lookup"><span data-stu-id="574ae-109">Register your app for push notifications</span></span>
<span data-ttu-id="574ae-110">U moet uw app naar de Windows Store verzenden, moet u uw serverproject voor de integratie met Windows Notification Services (WNS) voor het verzenden van pushmeldingen configureren.</span><span class="sxs-lookup"><span data-stu-id="574ae-110">You need to submit your app to the Windows Store, then configure your server project to integrate with Windows Notification Services (WNS) to send push.</span></span>

1. <span data-ttu-id="574ae-111">Klik in Visual Studio Solution Explorer met de rechtermuisknop op de UWP-app-project, klikt u op **Store** > **App aan de Store koppelen...** .</span><span class="sxs-lookup"><span data-stu-id="574ae-111">In Visual Studio Solution Explorer, right-click the UWP app project, click **Store** > **Associate App with the Store...**.</span></span>

    ![App aan Windows Store koppelen](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="574ae-113">Klik in de wizard op **volgende**, meld u aan met uw Microsoft-account, typ een naam voor uw app in **een nieuwe appnaam reserveren**, klikt u vervolgens op **Reserve**.</span><span class="sxs-lookup"><span data-stu-id="574ae-113">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="574ae-114">Nadat de registratie van de app is gemaakt, selecteert u de naam van de nieuwe app, klikt u op **volgende**, en klik vervolgens op **koppelen**.</span><span class="sxs-lookup"><span data-stu-id="574ae-114">After the app registration is successfully created, select the new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="574ae-115">Hierdoor worden de vereiste registratiegegevens voor Windows Store toegevoegd aan het toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="574ae-115">This adds the required Windows Store registration information to the application manifest.</span></span>  
4. <span data-ttu-id="574ae-116">Navigeer naar de [Windows-ontwikkelaarscentrum](https://dev.windows.com/en-us/overview), voor het aanmelden met je Microsoft-account, klikt u op de nieuwe app-registratie in **mijn apps**, vouw vervolgens **Services** > **Pushmeldingen**.</span><span class="sxs-lookup"><span data-stu-id="574ae-116">Navigate to the [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click the new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="574ae-117">In de **Pushmeldingen** pagina, klikt u op **Live Services site** onder **Microsoft Azure Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="574ae-117">In the **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="574ae-118">In de registratiepagina Noteer de waarde onder **toepassing geheimen** en de **pakket-SID**, die u vervolgens worden gebruikt voor het configureren van uw back-end voor de mobiele app.</span><span class="sxs-lookup"><span data-stu-id="574ae-118">In the registration page, make a note of the value under **Application secrets** and the **Package SID**, which you will next use to configure your mobile app backend.</span></span>

    ![App aan Windows Store koppelen](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="574ae-120">Het clientgeheim en de pakket-SID zijn belangrijke beveiligingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="574ae-120">The client secret and package SID are important security credentials.</span></span> <span data-ttu-id="574ae-121">Deel deze waarden met niemand en distribueer ze niet met uw app.</span><span class="sxs-lookup"><span data-stu-id="574ae-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="574ae-122">De **toepassings-Id** wordt gebruikt met het geheim verificatie van de Microsoft-Account configureren.</span><span class="sxs-lookup"><span data-stu-id="574ae-122">The **Application Id** is used with the secret to configure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-the-backend-to-send-push-notifications"></a><span data-ttu-id="574ae-123">Configureer de back-end om pushmeldingen te verzenden</span><span class="sxs-lookup"><span data-stu-id="574ae-123">Configure the backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="574ae-124"><a id="update-service"></a>Werk de beheerserver om pushmeldingen te verzenden</span><span class="sxs-lookup"><span data-stu-id="574ae-124"><a id="update-service"></a>Update the server to send push notifications</span></span>
<span data-ttu-id="574ae-125">Gebruik de procedure hieronder die overeenkomt met uw back-end-projecttype&mdash;beide [.NET back-end](#dotnet) of [back-end voor Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="574ae-125">Use the procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="574ae-126"><a name="dotnet"></a>.NET-back-endproject</span><span class="sxs-lookup"><span data-stu-id="574ae-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="574ae-127">In Visual Studio met de rechtermuisknop op het serverproject en klik op **NuGet-pakketten beheren**, zoekt u Microsoft.Azure.NotificationHubs en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="574ae-127">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="574ae-128">Hiermee installeert u de clientbibliotheek van Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="574ae-128">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="574ae-129">Vouw **domeincontrollers**, opent u TodoItemController.cs en voeg de volgende using-instructies:</span><span class="sxs-lookup"><span data-stu-id="574ae-129">Expand **Controllers**, open TodoItemController.cs, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="574ae-130">In de **PostTodoItem** methode, voeg de volgende code na het aanroepen van **InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="574ae-130">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create the notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send the push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="574ae-131">Deze code geeft aan dat de notification hub een push-melding verzenden wanneer een nieuw item invoegen is.</span><span class="sxs-lookup"><span data-stu-id="574ae-131">This code tells the notification hub to send a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="574ae-132">Het serverproject publiceren.</span><span class="sxs-lookup"><span data-stu-id="574ae-132">Republish the server project.</span></span>

### <span data-ttu-id="574ae-133"><a name="nodejs"></a>Back-endproject node.js</span><span class="sxs-lookup"><span data-stu-id="574ae-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="574ae-134">Als u dit nog niet hebt gedaan, [downloaden van het snelstartproject](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) of gebruik anders de [online-editor in Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="574ae-134">If you haven't already done so, [download the quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="574ae-135">Vervang de bestaande code in het bestand todoitem.js door het volgende:</span><span class="sxs-lookup"><span data-stu-id="574ae-135">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the WNS payload that contains the new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="574ae-136">Hierdoor wordt een pop-upmelding WNS waarin de item.text tijdens het invoegen van een nieuwe takenlijstitem verzonden.</span><span class="sxs-lookup"><span data-stu-id="574ae-136">This sends a WNS toast notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="574ae-137">Bij het bewerken van het bestand op uw lokale computer opnieuw publiceren het serverproject.</span><span class="sxs-lookup"><span data-stu-id="574ae-137">When editing the file on your local computer, republish the server project.</span></span>

## <span data-ttu-id="574ae-138"><a id="update-app"></a>Pushmeldingen toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="574ae-138"><a id="update-app"></a>Add push notifications to your app</span></span>
<span data-ttu-id="574ae-139">Vervolgens moet uw app registreren voor pushmeldingen op opstarten.</span><span class="sxs-lookup"><span data-stu-id="574ae-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="574ae-140">Wanneer u verificatie al hebt ingeschakeld, zorg ervoor dat de gebruiker zich aanmeldt voordat u probeert te registreren voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="574ae-140">When you have already enabled authentication, make sure that the user signs-in before trying to register for push notifications.</span></span>

1. <span data-ttu-id="574ae-141">Open de **App.xaml.cs** projectbestand en voeg de volgende `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="574ae-141">Open the **App.xaml.cs** project file and add the following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="574ae-142">Voeg in hetzelfde bestand de volgende **InitNotificationsAsync** methodedefinitie naar de **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="574ae-142">In the same file, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register the channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="574ae-143">Deze code de ChannelURI voor de app opgehaald uit WNS en wordt vervolgens die ChannelURI geregistreerd met uw App Service-mobiele App.</span><span class="sxs-lookup"><span data-stu-id="574ae-143">This code retrieves the ChannelURI for the app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="574ae-144">Aan de bovenkant van de **OnLaunched** gebeurtenis-handler in **App.xaml.cs**, toevoegen de **asynchrone** aanpassingsfunctie voor de methodedefinitie en voeg de volgende oproep verzenden naar de nieuwe **InitNotificationsAsync** methode, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="574ae-144">At the top of the **OnLaunched** event handler in **App.xaml.cs**, add the **async** modifier to the method definition and add the following call to the new **InitNotificationsAsync** method, as in the following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="574ae-145">Dit zorgt ervoor dat de tijdelijke ChannelURI wordt geregistreerd telkens wanneer die de toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="574ae-145">This guarantees that the short-lived ChannelURI is registered each time the application is launched.</span></span>
4. <span data-ttu-id="574ae-146">Uw UWP-app-project opnieuw worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="574ae-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="574ae-147">Uw app is nu gereed om pop-upmeldingen te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="574ae-147">Your app is now ready to receive toast notifications.</span></span>

## <span data-ttu-id="574ae-148"><a id="test"></a>Pushmeldingen testen in uw app</span><span class="sxs-lookup"><span data-stu-id="574ae-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="574ae-149"><a id="more"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="574ae-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="574ae-150">Meer informatie over pushmeldingen:</span><span class="sxs-lookup"><span data-stu-id="574ae-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="574ae-151">De beheerde client gebruiken voor Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="574ae-151">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="574ae-152">Sjablonen bieden u de flexibiliteit om platformoverschrijdende pushes en gelokaliseerde pushes te verzenden.</span><span class="sxs-lookup"><span data-stu-id="574ae-152">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="574ae-153">Informatie over het registreren van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="574ae-153">Learn how to register templates.</span></span>
* [<span data-ttu-id="574ae-154">Push notification problemen vaststellen</span><span class="sxs-lookup"><span data-stu-id="574ae-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="574ae-155">Er zijn diverse redenen waarom meldingen mogelijk ophalen verwijderd of kunnen niet eindigen op apparaten.</span><span class="sxs-lookup"><span data-stu-id="574ae-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="574ae-156">Dit onderwerp leest u hoe te analyseren en te achterhalen van de hoofdoorzaken van fouten voor push-melding.</span><span class="sxs-lookup"><span data-stu-id="574ae-156">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="574ae-157">U kunt u verder gaat u aan bij een van de volgende zelfstudies:</span><span class="sxs-lookup"><span data-stu-id="574ae-157">Consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="574ae-158">Verificatie toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="574ae-158">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="574ae-159">Ontdek hoe u gebruikers van uw app verifieert met een id-provider.</span><span class="sxs-lookup"><span data-stu-id="574ae-159">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="574ae-160">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="574ae-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="574ae-161">Informatie over het toevoegen van offlineondersteuning aan uw app met een back-end voor mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="574ae-161">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="574ae-162">Met offlinesynchronisatie kunnen eindgebruikers interactie aangaan met een mobiele app&mdash;gegevens weergeven, toevoegen of wijzigen&mdash;ook als er geen netwerkverbinding is.</span><span class="sxs-lookup"><span data-stu-id="574ae-162">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
