---
title: aaaAdd push notifications tooyour Xamarin.iOS-app met Azure App Service
description: Meer informatie over hoe Azure App Service-toosend toouse push-meldingen tooyour Xamarin.iOS-app
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
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a><span data-ttu-id="bd3bb-103">Push notifications tooyour Xamarin.iOS-App toevoegen</span><span class="sxs-lookup"><span data-stu-id="bd3bb-103">Add push notifications tooyour Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="bd3bb-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="bd3bb-104">Overview</span></span>
<span data-ttu-id="bd3bb-105">In deze zelfstudie maakt u een push notifications toohello toevoegen [Xamarin.iOS snel starten](app-service-mobile-xamarin-ios-get-started.md) project, zodat een push-melding toohello apparaat verzonden telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-105">In this tutorial, you add push notifications toohello [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="bd3bb-106">Als u geen gebruik Hallo snel starten-serverproject gedownload, u moet Hallo push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="bd3bb-107">Zie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd3bb-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bd3bb-108">Prerequisites</span></span>
* <span data-ttu-id="bd3bb-109">Volledige Hallo [Xamarin.iOS Quick Start](app-service-mobile-xamarin-ios-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-109">Complete hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="bd3bb-110">Een fysiek iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-110">A physical iOS device.</span></span> <span data-ttu-id="bd3bb-111">Pushmeldingen worden niet ondersteund door Hallo iOS-simulator.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-111">Push notifications are not supported by hello iOS simulator.</span></span>

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="bd3bb-112">Hallo-app voor pushmeldingen op Apple developer-portal te registreren</span><span class="sxs-lookup"><span data-stu-id="bd3bb-112">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a><span data-ttu-id="bd3bb-113">Uw mobiele App toosend-pushmeldingen configureren</span><span class="sxs-lookup"><span data-stu-id="bd3bb-113">Configure your Mobile App toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="bd3bb-114">Hallo server project toosend-pushmeldingen bijwerken</span><span class="sxs-lookup"><span data-stu-id="bd3bb-114">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="bd3bb-115">Configureer uw Xamarin.iOS-project</span><span class="sxs-lookup"><span data-stu-id="bd3bb-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="bd3bb-116">Push notifications tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="bd3bb-116">Add push notifications tooyour app</span></span>
1. <span data-ttu-id="bd3bb-117">In **QSTodoService**, Hallo na eigenschap toevoegen zodat **AppDelegate** Hallo mobiele clients kunt verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="bd3bb-117">In **QSTodoService**, add hello following property so that **AppDelegate** can acquire hello mobile client:</span></span>
   
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
2. <span data-ttu-id="bd3bb-118">Voeg de volgende Hallo `using` instructie toohello bovenaan Hallo **AppDelegate.cs** bestand.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-118">Add hello following `using` statement toohello top of hello **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="bd3bb-119">In **AppDelegate**, overschrijven Hallo **FinishedLaunching** gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="bd3bb-119">In **AppDelegate**, override hello **FinishedLaunching** event:</span></span>
   
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
4. <span data-ttu-id="bd3bb-120">In hetzelfde bestand Hallo, overschrijven Hallo **RegisteredForRemoteNotifications** gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-120">In hello same file, override hello **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="bd3bb-121">In deze code registreert u voor een eenvoudige sjabloon melding die door Hallo-server worden verzonden voor alle ondersteunde platforms.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by hello server.</span></span>
   
    <span data-ttu-id="bd3bb-122">Zie voor meer informatie over sjablonen met Notification Hubs [sjablonen](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="bd3bb-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

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


1. <span data-ttu-id="bd3bb-123">Vervolgens overschrijven Hallo **DidReceivedRemoteNotification** gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="bd3bb-123">Then, override hello **DidReceivedRemoteNotification** event:</span></span>
   
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

<span data-ttu-id="bd3bb-124">Uw app is nu bijgewerkte toosupport pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-124">Your app is now updated toosupport push notifications.</span></span>

## <span data-ttu-id="bd3bb-125"><a name="test"></a>Pushmeldingen testen in uw app</span><span class="sxs-lookup"><span data-stu-id="bd3bb-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="bd3bb-126">Druk op Hallo **uitvoeren** toobuild Hallo project knop Hallo-app te starten in een compatibele iOS-apparaat, en klikt u op **OK** tooaccept pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-126">Press hello **Run** button toobuild hello project and start hello app in an iOS capable device, then click **OK** tooaccept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bd3bb-127">U moet expliciet pushmeldingen accepteren van uw app.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="bd3bb-128">Deze aanvraag is alleen sprake Hallo eerste keer is dat Hallo app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-128">This request only occurs hello first time that hello app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="bd3bb-129">Typ een taak in Hallo-app en klik vervolgens op Hallo plus (**+**) pictogram.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-129">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
3. <span data-ttu-id="bd3bb-130">Controleer of een melding wordt ontvangen en klik op **OK** toodismiss Hallo melding.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-130">Verify that a notification is received, then click **OK** toodismiss hello notification.</span></span>
4. <span data-ttu-id="bd3bb-131">Herhaal stap 2 en onmiddellijk sluiten Hallo app en controleer of er een melding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-131">Repeat step 2 and immediately close hello app, then verify that a notification is shown.</span></span>

<span data-ttu-id="bd3bb-132">Deze zelfstudie hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="bd3bb-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



