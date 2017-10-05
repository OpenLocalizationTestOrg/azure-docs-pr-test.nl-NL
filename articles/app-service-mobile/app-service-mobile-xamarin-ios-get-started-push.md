---
title: Pushmeldingen toevoegen aan uw Xamarin.iOS-app met Azure App Service
description: Informatie over het gebruik van Azure App Service om pushmeldingen te verzenden naar uw Xamarin.iOS-app
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: bf922e49c4c92d0065817a5dd6c7d10a04737304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinios-app"></a><span data-ttu-id="8def7-103">Pushmeldingen toevoegen aan uw App voor Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="8def7-103">Add push notifications to your Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="8def7-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8def7-104">Overview</span></span>
<span data-ttu-id="8def7-105">In deze zelfstudie hebt u pushmeldingen toevoegen de [Xamarin.iOS snel starten](app-service-mobile-xamarin-ios-get-started.md) project, zodat een pushmelding wordt verzonden naar het apparaat telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="8def7-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="8def7-106">Als u het gedownloade quick start-serverproject niet gebruikt, moet u het push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="8def7-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="8def7-107">Zie [werken met de .NET-back-endserver SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8def7-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8def7-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8def7-108">Prerequisites</span></span>
* <span data-ttu-id="8def7-109">Voltooi de [Xamarin.iOS Quick Start](app-service-mobile-xamarin-ios-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8def7-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="8def7-110">Een fysiek iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="8def7-110">A physical iOS device.</span></span> <span data-ttu-id="8def7-111">Pushmeldingen worden niet ondersteund door de iOS-simulator.</span><span class="sxs-lookup"><span data-stu-id="8def7-111">Push notifications are not supported by the iOS simulator.</span></span>

## <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="8def7-112">De app voor pushmeldingen op Apple developer-portal te registreren</span><span class="sxs-lookup"><span data-stu-id="8def7-112">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-to-send-push-notifications"></a><span data-ttu-id="8def7-113">Configureer uw mobiele App om pushmeldingen te verzenden</span><span class="sxs-lookup"><span data-stu-id="8def7-113">Configure your Mobile App to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="8def7-114">Bijwerken van het serverproject om pushmeldingen te verzenden</span><span class="sxs-lookup"><span data-stu-id="8def7-114">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="8def7-115">Configureer uw Xamarin.iOS-project</span><span class="sxs-lookup"><span data-stu-id="8def7-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="8def7-116">Pushmeldingen toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="8def7-116">Add push notifications to your app</span></span>
1. <span data-ttu-id="8def7-117">In **QSTodoService**, de volgende eigenschap toevoegen zodat **AppDelegate** mobiele clients kunt verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="8def7-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="8def7-118">Voeg de volgende `using` instructie boven aan de **AppDelegate.cs** bestand.</span><span class="sxs-lookup"><span data-stu-id="8def7-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="8def7-119">In **AppDelegate**, overschrijven de **FinishedLaunching** gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="8def7-119">In **AppDelegate**, override the **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="8def7-120">In hetzelfde bestand, overschrijven de **RegisteredForRemoteNotifications** gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8def7-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="8def7-121">In deze code registreert u voor een eenvoudige sjabloon melding die door de server worden verzonden voor alle ondersteunde platforms.</span><span class="sxs-lookup"><span data-stu-id="8def7-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span></span>
   
    <span data-ttu-id="8def7-122">Zie voor meer informatie over sjablonen met Notification Hubs [sjablonen](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="8def7-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="8def7-123">Vervolgens, overschrijven de **DidReceivedRemoteNotification** gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="8def7-123">Then, override the **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="8def7-124">Uw app is nu bijgewerkt ter ondersteuning van pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="8def7-124">Your app is now updated to support push notifications.</span></span>

## <span data-ttu-id="8def7-125"><a name="test"></a>Pushmeldingen testen in uw app</span><span class="sxs-lookup"><span data-stu-id="8def7-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="8def7-126">Druk op de **uitvoeren** klikken om het project bouwen en starten van de app in een compatibele iOS-apparaat en klik vervolgens op **OK** pushmeldingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="8def7-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8def7-127">U moet expliciet pushmeldingen accepteren van uw app.</span><span class="sxs-lookup"><span data-stu-id="8def7-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="8def7-128">Deze aanvraag treedt alleen op de eerste keer dat de app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8def7-128">This request only occurs the first time that the app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="8def7-129">Typ een taak in de app en klik vervolgens op het plusteken (**+**) pictogram.</span><span class="sxs-lookup"><span data-stu-id="8def7-129">In the app, type a task, and then click the plus (**+**) icon.</span></span>
3. <span data-ttu-id="8def7-130">Controleer of een melding wordt ontvangen en klik op **OK** kunnen worden verwijderd van de melding.</span><span class="sxs-lookup"><span data-stu-id="8def7-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span></span>
4. <span data-ttu-id="8def7-131">Herhaal stap 2 en onmiddellijk sluit de app en controleer of er een melding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8def7-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span></span>

<span data-ttu-id="8def7-132">Deze zelfstudie hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="8def7-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



