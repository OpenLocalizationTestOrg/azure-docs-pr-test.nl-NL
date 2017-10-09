---
title: aaaiOS Pushmeldingen met Notification Hubs voor Xamarin-apps | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Xamarin iOS-toepassing.
services: notification-hubs
keywords: ios-pushmeldingen,pushberichten,pushmeldingen,pushbericht
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="7af79-104">iOS-pushmeldingen met Notification Hubs voor Xamarin-apps</span><span class="sxs-lookup"><span data-stu-id="7af79-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="7af79-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7af79-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7af79-106">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="7af79-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="7af79-107">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="7af79-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7af79-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7af79-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="7af79-109">Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooan iOS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7af79-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span>
<span data-ttu-id="7af79-110">Maakt u een lege Xamarin.iOS-app die pushmeldingen ontvangt via Hallo [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="7af79-110">You'll create a blank Xamarin.iOS app that receives push notifications by using hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="7af79-111">Wanneer u klaar bent, moet u kunnen toouse push uw notification hub toobroadcast meldingen tooall Hallo apparaten waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7af79-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="7af79-112">Hallo voltooide code is beschikbaar in Hallo [NotificationHubs-app] [ GitHub] voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7af79-112">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="7af79-113">Deze zelfstudie wordt Hallo eenvoudige push bericht scenario uitzenden met Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="7af79-113">This tutorial demonstrates hello simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7af79-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7af79-114">Prerequisites</span></span>
<span data-ttu-id="7af79-115">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="7af79-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="7af79-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="7af79-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="7af79-117">Een apparaat dat compatibel is met iOS 7.0 (of een hogere versie)</span><span class="sxs-lookup"><span data-stu-id="7af79-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="7af79-118">iOS Developer Program-lidmaatschap</span><span class="sxs-lookup"><span data-stu-id="7af79-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="7af79-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="7af79-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="7af79-120">Vanwege configuratievereisten voor iOS-pushmeldingen, moet u implementeren en testen van de voorbeeldtoepassing Hallo op een fysiek iOS-apparaat (iPhone of iPad) in plaats van in Hallo simulator.</span><span class="sxs-lookup"><span data-stu-id="7af79-120">Because of configuration requirements for iOS push notifications, you must deploy and test hello sample application on a physical iOS device (iPhone or iPad) instead of in hello simulator.</span></span>
  > 
  > 

<span data-ttu-id="7af79-121">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Xamarin iOS-apps.</span><span class="sxs-lookup"><span data-stu-id="7af79-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="7af79-122">Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="7af79-122">Configure your notification hub</span></span>
<span data-ttu-id="7af79-123">Deze sectie leidt u door een nieuwe notification hub maken en configureren van verificatie met APNS met Hallo **.p12** pushcertificaat dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7af79-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="7af79-124">Als u toouse een notification hub die u al hebt gemaakt wilt, kunt u toostep 5 overslaan.</span><span class="sxs-lookup"><span data-stu-id="7af79-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="7af79-125">Als we tooconfigure hello APNS-verbinding in Azure Portal hello wilt open uw Notification Hub-instellingen, en klik op <b>Notification Services</b>, en klik vervolgens op Hallo <b>Apple (APNS)</b> item in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="7af79-125">As we want tooconfigure hello APNS connection, in hello Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click hello <b>Apple (APNS)</b> item in hello list.</span></span> <span data-ttu-id="7af79-126">Hierna klikt u op <b>certificaat uploaden</b> en selecteer Hallo <b>.p12</b> certificaat dat u eerder, evenals het Hallo-wachtwoord voor Hallo certificaat hebt geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="7af79-126">Once done, click on <b>Upload Certificate</b> and select hello <b>.p12</b> certificate that you exported earlier, as well as hello password for hello certificate.</span></span></p>

<p><span data-ttu-id="7af79-127">Zorg ervoor dat tooselect <b>Sandbox</b> modus, aangezien u pushmeldingen verzenden van berichten in een ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="7af79-127">Make sure tooselect <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="7af79-128">Gebruik alleen Hallo <b>productie</b> instelling als u wilt dat toosend push notifications toousers die al in uw app uit de store Hallo bezit.</span><span class="sxs-lookup"><span data-stu-id="7af79-128">Only use hello <b>Production</b> setting if you want toosend push notifications toousers who already purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="7af79-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="7af79-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="7af79-130">Uw notification hub is nu geconfigureerd toowork met APNS en u hebt Hallo verbinding tekenreeksen tooregister uw app en om pushmeldingen te verzenden.</span><span class="sxs-lookup"><span data-stu-id="7af79-130">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="7af79-131">Verbinding maken met uw app toohello notification hub</span><span class="sxs-lookup"><span data-stu-id="7af79-131">Connect your app toohello notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="7af79-132">Een nieuw project maken</span><span class="sxs-lookup"><span data-stu-id="7af79-132">Create a new project</span></span>
1. <span data-ttu-id="7af79-133">In Xamarin Studio een nieuw iOS-project maken en selecteer Hallo **Unified API** > **enkele toepassingsweergave** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7af79-133">In Xamarin Studio, create a new iOS project and select hello **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - Toepassingstype selecteren][31]
2. <span data-ttu-id="7af79-135">Voeg een verwijzing toohello Azure Messaging-onderdeel.</span><span class="sxs-lookup"><span data-stu-id="7af79-135">Add a reference toohello Azure Messaging component.</span></span> <span data-ttu-id="7af79-136">Hallo weergave oplossing, met de rechtermuisknop op Hallo **onderdelen** map voor uw project en kies **meer onderdelen ophalen**.</span><span class="sxs-lookup"><span data-stu-id="7af79-136">In hello Solution view, right-click hello **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="7af79-137">Zoeken naar Hallo **Azure Messaging** onderdeel en Hallo onderdeel tooyour project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7af79-137">Search for hello **Azure Messaging** component and add hello component tooyour project.</span></span>
3. <span data-ttu-id="7af79-138">In **AppDelegate.cs**, voeg de volgende Hallo met de instructie:</span><span class="sxs-lookup"><span data-stu-id="7af79-138">In **AppDelegate.cs**, add hello following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="7af79-139">Declareer een exemplaar van **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="7af79-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="7af79-140">Maak een **Constants.cs** klasse Hello variabelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7af79-140">Create a **Constants.cs** class with hello following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="7af79-141">In **AppDelegate.cs**, bijwerken **FinishedLaunching()** toomatch Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="7af79-141">In **AppDelegate.cs**, update **FinishedLaunching()** toomatch hello following:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. <span data-ttu-id="7af79-142">Hallo overschrijven **RegisteredForRemoteNotifications()** methode in **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="7af79-142">Override hello **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. <span data-ttu-id="7af79-143">Hallo overschrijven **ReceivedRemoteNotification()** methode in **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="7af79-143">Override hello **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="7af79-144">Maak de volgende Hallo **ProcessNotification()** methode in **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="7af79-144">Create hello following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="7af79-145">U kunt toooverride **FailedToRegisterForRemoteNotifications()** toohandle situaties zoals geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="7af79-145">You can choose toooverride **FailedToRegisterForRemoteNotifications()** toohandle situations such as no network connection.</span></span> <span data-ttu-id="7af79-146">Dit is vooral belangrijk waar Hallo gebruiker uw toepassing bijvoorbeeld starten in de offlinemodus bevindt (bijvoorbeeld in een vliegtuig) en u wilt dat toohandle pushberichten-scenario's voor specifieke tooyour app.</span><span class="sxs-lookup"><span data-stu-id="7af79-146">This is especially important where hello user might start your application in offline mode (e.g. Airplane) and you want toohandle push messaging scenarios specific tooyour app.</span></span>
   > 
   > 
10. <span data-ttu-id="7af79-147">Hallo-app uitvoeren op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="7af79-147">Run hello app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="7af79-148">Pushmeldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="7af79-148">Sending Push Notifications</span></span>
<span data-ttu-id="7af79-149">U kunt testen ontvangen van pushmeldingen in uw app door meldingen te verzenden in Hallo [Azure Portal] via Hallo **Test verzenden** mogelijkheden in Hallo **probleemoplossing** hulpmiddelenset, rechts op Hallo notification hub pagina, zoals weergegeven in onderstaande welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="7af79-149">You can test receiving push notifications in your app by sending notifications in hello [Azure Portal] via hello **Test Send** capability in hello **Troubleshooting** toolset, right in hello notification hub page, as shown in hello screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="7af79-150">Pushmeldingen worden gewoonlijk met een compatibele bibliotheek verzonden via een back-endservice zoals Mobile Services of ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7af79-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="7af79-151">U kunt ook Hallo REST-API gebruiken direct push toosend berichten als een bibliotheek niet beschikbaar in uw scenario is.</span><span class="sxs-lookup"><span data-stu-id="7af79-151">You can also use hello REST API directly toosend push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="7af79-152">In deze zelfstudie wordt Houd het eenvoudig en alleen gedemonstreerd hoe u uw clientapp test door meldingen met behulp van Hallo .NET SDK voor notification hubs in een consoletoepassing in plaats van een back-endservice te verzenden.</span><span class="sxs-lookup"><span data-stu-id="7af79-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="7af79-153">We raden aan Hallo [Notification Hubs gebruiken toopush meldingen toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) Hallo volgende stap voor het verzenden van meldingen vanuit een ASP.NET-back-end zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7af79-153">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="7af79-154">Hallo volgende methoden kan echter worden gebruikt voor het verzenden van meldingen:</span><span class="sxs-lookup"><span data-stu-id="7af79-154">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="7af79-155">**REST-Interface**: U kunt push-melding ondersteunen op elk back-end-platform met Hallo [REST-interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="7af79-155">**REST Interface**:  You can support push notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="7af79-156">**Microsoft Azure Notification Hubs .NET SDK**: In Hallo Nuget Package Manager voor Visual Studio, voert u [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="7af79-156">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="7af79-157">**Node.js** : [hoe toouse Notification Hubs met Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="7af79-157">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="7af79-158">**Mobile Apps**: voor een voorbeeld van hoe u meldingen vanuit een back-end voor een Azure App Service Mobile Apps die geïntegreerd met Notification Hubs toosend Zie [Add push notifications tooyour mobiele app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="7af79-158">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="7af79-159">**Java / PHP**: Zie voor een voorbeeld van hoe toosend pushmeldingen met behulp van REST-API's Hallo ' hoe toouse Notification Hubs vanuit Java/PHP ' ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="7af79-159">**Java / PHP**: For an example of how toosend push notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="7af79-160">(Optioneel) Pushmeldingen verzenden vanuit een .NET-console-app</span><span class="sxs-lookup"><span data-stu-id="7af79-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="7af79-161">In deze sectie worden pushmeldingen verzonden met een eenvoudige .NET-console-app.</span><span class="sxs-lookup"><span data-stu-id="7af79-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="7af79-162">Ter Hallo van dit voorbeeld wordt overgeschakeld tooa Windows-ontwikkelomgeving waarin Visual Studio al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7af79-162">For hello purposes of this example, we will switch tooa Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="7af79-163">Maak in Visual Studio een nieuwe Visual C#-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="7af79-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="7af79-164">Klik in Visual Studio achtereenvolgens op **Extra**, **NuGet Package Manager** en **Package Manager-console**.</span><span class="sxs-lookup"><span data-stu-id="7af79-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="7af79-165">Hallo package manager-console moet worden weergegeven onder gedokte toohello van uw Visual Studio-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="7af79-165">hello package manager console should appear docked toohello bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="7af79-166">In Hallo venster Package Manager-Console, stelt u Hallo **standaardproject** tooyour nieuwe console toepassingsproject en vervolgens in het consolevenster hello, Hallo volgende opdracht wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="7af79-166">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="7af79-167">Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="7af79-167">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="7af79-168">Open Hallo `Program.cs` -bestand en voeg de volgende Hallo `using` instructie, waarbij u ervoor zorgt dat we Azure-klassen en functies binnen uw hoofdklasse kunnen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7af79-168">Open hello `Program.cs` file and add hello following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="7af79-169">In uw `Program` klasse, Hallo volgende methode toe te voegen (Vergeet niet tooreplace hello **verbindingsreeks** en **hubnaam**):</span><span class="sxs-lookup"><span data-stu-id="7af79-169">In your `Program` class, add hello following method (don't forget tooreplace hello **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="7af79-170">Toevoegen van de volgende regels in Hallo uw `Main` methode:</span><span class="sxs-lookup"><span data-stu-id="7af79-170">Add hello following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="7af79-171">Druk op Hallo F5 sleutel toorun Hallo app.</span><span class="sxs-lookup"><span data-stu-id="7af79-171">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="7af79-172">Binnen enkele seconden wordt een pushmelding op uw apparaat weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7af79-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="7af79-173">Of u Wi-Fi of een mobiel dataverkeer netwerk gebruikt, zorg ervoor dat er een actieve internetverbinding op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7af79-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on hello device.</span></span>

<span data-ttu-id="7af79-174">U vindt alle mogelijke nettoladingen van Hallo in Hallo Apple [Local and Push Notification Programming Guide].</span><span class="sxs-lookup"><span data-stu-id="7af79-174">You can find all hello possible payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="7af79-175">(Optioneel) Meldingen verzenden vanuit een mobiele service</span><span class="sxs-lookup"><span data-stu-id="7af79-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="7af79-176">In deze sectie worden pushmeldingen verzonden met een mobiele service via een knooppuntscript.</span><span class="sxs-lookup"><span data-stu-id="7af79-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="7af79-177">een melding met behulp van een mobiele service toosend Volg [aan de slag met Mobile Services], en vervolgens:</span><span class="sxs-lookup"><span data-stu-id="7af79-177">toosend a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="7af79-178">Meld u aan toohello [klassieke Azure-Portal], en selecteer uw mobiele service.</span><span class="sxs-lookup"><span data-stu-id="7af79-178">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="7af79-179">Selecteer Hallo **Scheduler** tabblad Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="7af79-179">Select hello **Scheduler** tab on hello top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="7af79-180">Maak een nieuwe geplande taak, voeg een naam in en selecteer **Op aanvraag**.</span><span class="sxs-lookup"><span data-stu-id="7af79-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="7af79-181">Wanneer het Hallo-taak is gemaakt, klikt u op Hallo taaknaam.</span><span class="sxs-lookup"><span data-stu-id="7af79-181">When hello job is created, click hello job name.</span></span> <span data-ttu-id="7af79-182">Klik vervolgens op Hallo **Script** tabblad op Hallo bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="7af79-182">Then click hello **Script** tab on hello top bar.</span></span>
5. <span data-ttu-id="7af79-183">Hallo volgende script in de plannerfunctie invoegen.</span><span class="sxs-lookup"><span data-stu-id="7af79-183">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="7af79-184">Zorg ervoor dat tooreplace Hallo tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultFullSharedAccessSignature* die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="7af79-184">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="7af79-185">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7af79-185">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. <span data-ttu-id="7af79-186">Klik op **eenmaal uitvoeren** op de balk onderaan Hallo.</span><span class="sxs-lookup"><span data-stu-id="7af79-186">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="7af79-187">U ontvangt een waarschuwing op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="7af79-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7af79-188">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7af79-188">Next steps</span></span>
<span data-ttu-id="7af79-189">In dit eenvoudige voorbeeld hebt u uitgezonden push notifications tooall uw iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="7af79-189">In this simple example, you broadcasted push notifications tooall your iOS devices.</span></span> <span data-ttu-id="7af79-190">In order tootarget specifieke gebruikers, raadpleegt u de zelfstudie toohello [Notification Hubs gebruiken toopush meldingen toousers].</span><span class="sxs-lookup"><span data-stu-id="7af79-190">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="7af79-191">Als u wilt dat toosegment gebruikers op belangengroepen, kunt u lezen [Notification Hubs gebruiken toosend belangrijk nieuws].</span><span class="sxs-lookup"><span data-stu-id="7af79-191">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="7af79-192">Meer informatie over het toouse Notification Hubs in [richtlijnen voor Notification Hubs] en in Hallo [Notification Hubs hoe-toofor iOS].</span><span class="sxs-lookup"><span data-stu-id="7af79-192">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor iOS].</span></span>

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[aan de slag met Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios
[klassieke Azure-Portal]: https://manage.windowsazure.com/
[richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs hoe-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Notification Hubs gebruiken toopush meldingen toousers]: /manage/services/notification-hubs/notify-users-aspnet
[Notification Hubs gebruiken toosend belangrijk nieuws]: /manage/services/notification-hubs/breaking-news-dotnet

[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure Portal]: https://portal.azure.com
