---
title: iOS-pushmeldingen met Notification Hubs voor Xamarin-apps | Microsoft Docs
description: In deze zelfstudie leert u hoe u met Azure Notification Hubs pushmeldingen verzendt naar een Xamarin iOS-toepassing.
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
ms.openlocfilehash: 72a81fa0deb34ace77b8fb9b1a4e6b24ee164b35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="057ae-104">iOS-pushmeldingen met Notification Hubs voor Xamarin-apps</span><span class="sxs-lookup"><span data-stu-id="057ae-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="057ae-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="057ae-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="057ae-106">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="057ae-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="057ae-107">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="057ae-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="057ae-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="057ae-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="057ae-109">In deze zelfstudie wordt gedemonstreerd hoe u met Azure Notification Hubs pushmeldingen verzendt naar een iOS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="057ae-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span>
<span data-ttu-id="057ae-110">U maakt een lege Xamarin.iOS-app die pushmeldingen ontvangt met de [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="057ae-110">You'll create a blank Xamarin.iOS app that receives push notifications by using the [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="057ae-111">Als u klaar bent, kunt u de Notification Hub gebruiken om pushmeldingen uit te zenden naar alle apparaten waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="057ae-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="057ae-112">De voltooide code is beschikbaar in het [NotificationHubs-app][GitHub]-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="057ae-112">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="057ae-113">In deze zelfstudie wordt een eenvoudig scenario voor het uitzenden van pushmeldingen met Notification Hubs beschreven.</span><span class="sxs-lookup"><span data-stu-id="057ae-113">This tutorial demonstrates the simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="057ae-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="057ae-114">Prerequisites</span></span>
<span data-ttu-id="057ae-115">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="057ae-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="057ae-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="057ae-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="057ae-117">Een apparaat dat compatibel is met iOS 7.0 (of een hogere versie)</span><span class="sxs-lookup"><span data-stu-id="057ae-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="057ae-118">iOS Developer Program-lidmaatschap</span><span class="sxs-lookup"><span data-stu-id="057ae-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="057ae-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="057ae-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="057ae-120">Vanwege configuratievereisten voor iOS-pushmeldingen moet u de voorbeeldtoepassing op een fysiek iOS-apparaat (iPhone of iPad) implementeren en testen in plaats van in de simulator.</span><span class="sxs-lookup"><span data-stu-id="057ae-120">Because of configuration requirements for iOS push notifications, you must deploy and test the sample application on a physical iOS device (iPhone or iPad) instead of in the simulator.</span></span>
  > 
  > 

<span data-ttu-id="057ae-121">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Xamarin iOS-apps.</span><span class="sxs-lookup"><span data-stu-id="057ae-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="057ae-122">Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="057ae-122">Configure your notification hub</span></span>
<span data-ttu-id="057ae-123">In deze sectie wordt u begeleid bij het maken van een nieuwe Notification Hub en het configureren van verificatie met APNs met het **.p12**-pushcertificaat dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="057ae-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="057ae-124">Als u een Notification Hub wilt gebruiken die u al hebt gemaakt, kunt u doorgaan naar stap 5.</span><span class="sxs-lookup"><span data-stu-id="057ae-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="057ae-125">Omdat wij de APNs-verbinding willen configureren, opent u in Azure Portal de Notification Hub-instellingen en klikt u achtereenvolgens op <b>Notification Services</b> en het item <b>Apple (APNS)</b> in de lijst.</span><span class="sxs-lookup"><span data-stu-id="057ae-125">As we want to configure the APNS connection, in the Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click the <b>Apple (APNS)</b> item in the list.</span></span> <span data-ttu-id="057ae-126">Hierna klikt u op <b>Certificaat uploaden</b> en selecteert u het <b>.p12</b>-certificaat dat u eerder hebt geëxporteerd, evenals het wachtwoord voor het certificaat.</span><span class="sxs-lookup"><span data-stu-id="057ae-126">Once done, click on <b>Upload Certificate</b> and select the <b>.p12</b> certificate that you exported earlier, as well as the password for the certificate.</span></span></p>

<p><span data-ttu-id="057ae-127">Zorg ervoor dat u de <b>Sandbox</b>-modus selecteert, omdat u pushberichten in een ontwikkelomgeving gaat verzenden.</span><span class="sxs-lookup"><span data-stu-id="057ae-127">Make sure to select <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="057ae-128">Gebruik de instelling <b>Productie</b> alleen als u pushmeldingen wilt verzenden naar gebruikers die uw app al in de winkel hebben aangeschaft.</span><span class="sxs-lookup"><span data-stu-id="057ae-128">Only use the <b>Production</b> setting if you want to send push notifications to users who already purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="057ae-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="057ae-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="057ae-130">De Notification Hub is nu geconfigureerd om te werken met APNs en u hebt de verbindingsreeksen om uw app te registreren en pushmeldingen te verzenden.</span><span class="sxs-lookup"><span data-stu-id="057ae-130">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="057ae-131">Uw app verbinden met de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="057ae-131">Connect your app to the notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="057ae-132">Een nieuw project maken</span><span class="sxs-lookup"><span data-stu-id="057ae-132">Create a new project</span></span>
1. <span data-ttu-id="057ae-133">Maak in Xamarin Studio een nieuw iOS-project en selecteer de sjabloon **Unified API** > **Toepassing voor één weergave**.</span><span class="sxs-lookup"><span data-stu-id="057ae-133">In Xamarin Studio, create a new iOS project and select the **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - Toepassingstype selecteren][31]
2. <span data-ttu-id="057ae-135">Voeg een verwijzing toe aan het Azure Messaging-onderdeel.</span><span class="sxs-lookup"><span data-stu-id="057ae-135">Add a reference to the Azure Messaging component.</span></span> <span data-ttu-id="057ae-136">Klik in de oplossingsweergave met de rechtermuisknop op de map **Onderdelen** voor uw project en kies **Meer onderdelen ophalen**.</span><span class="sxs-lookup"><span data-stu-id="057ae-136">In the Solution view, right-click the **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="057ae-137">Zoek het onderdeel **Azure Messaging** en voeg het onderdeel toe aan het project.</span><span class="sxs-lookup"><span data-stu-id="057ae-137">Search for the **Azure Messaging** component and add the component to your project.</span></span>
3. <span data-ttu-id="057ae-138">Voeg in **AppDelegate.cs** de volgende instructie toe:</span><span class="sxs-lookup"><span data-stu-id="057ae-138">In **AppDelegate.cs**, add the following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="057ae-139">Declareer een exemplaar van **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="057ae-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="057ae-140">Maak een klasse **Constants.cs** met de volgende variabelen:</span><span class="sxs-lookup"><span data-stu-id="057ae-140">Create a **Constants.cs** class with the following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="057ae-141">Werk in **AppDelegate.cs** het item **FinishedLaunching()** zo bij dat het overeenkomt met het volgende:</span><span class="sxs-lookup"><span data-stu-id="057ae-141">In **AppDelegate.cs**, update **FinishedLaunching()** to match the following:</span></span>
   
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
7. <span data-ttu-id="057ae-142">Overschrijf de **RegisteredForRemoteNotifications()**-methode in **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="057ae-142">Override the **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
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
8. <span data-ttu-id="057ae-143">Overschrijf de **ReceivedRemoteNotification()**-methode in **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="057ae-143">Override the **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="057ae-144">Maak de volgende **ProcessNotification()**-methode in **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="057ae-144">Create the following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check to see if the dictionary has the aps key.  This is the notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get the aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract the alert text
                // NOTE: If you're using the simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from the aps dictionary will be another NSDictionary.
                // Basically the JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from the ReceivedRemoteNotification while the app was running,
                // we of course need to manually process things like the sound, badge, and alert.
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
   > <span data-ttu-id="057ae-145">U kunt ervoor kiezen **FailedToRegisterForRemoteNotifications()** te overschrijven om situaties zoals het ontbreken van een netwerkverbinding af te handelen.</span><span class="sxs-lookup"><span data-stu-id="057ae-145">You can choose to override **FailedToRegisterForRemoteNotifications()** to handle situations such as no network connection.</span></span> <span data-ttu-id="057ae-146">Dit is vooral belangrijk wanneer de gebruiker de toepassing in de offlinemodus start (bijvoorbeeld in een vliegtuig) en u scenario's voor het verzenden van pushberichten wilt afhandelen die specifiek zijn voor uw app.</span><span class="sxs-lookup"><span data-stu-id="057ae-146">This is especially important where the user might start your application in offline mode (e.g. Airplane) and you want to handle push messaging scenarios specific to your app.</span></span>
   > 
   > 
10. <span data-ttu-id="057ae-147">Voer de app uit op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="057ae-147">Run the app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="057ae-148">Pushmeldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="057ae-148">Sending Push Notifications</span></span>
<span data-ttu-id="057ae-149">U kunt het ontvangen van pushmeldingen in uw app testen door in [Azure Portal] via de mogelijkheid **Test verzenden** in de werkset **Probleemoplossing** direct op de pagina van de Notification Hub meldingen te verzenden (zie onderstaand scherm).</span><span class="sxs-lookup"><span data-stu-id="057ae-149">You can test receiving push notifications in your app by sending notifications in the [Azure Portal] via the **Test Send** capability in the **Troubleshooting** toolset, right in the notification hub page, as shown in the screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="057ae-150">Pushmeldingen worden gewoonlijk met een compatibele bibliotheek verzonden via een back-endservice zoals Mobile Services of ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="057ae-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="057ae-151">U kunt de REST API ook direct gebruiken om pushmeldingen te verzenden als er geen bibliotheek beschikbaar is voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="057ae-151">You can also use the REST API directly to send push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="057ae-152">In deze zelfstudie houden we het eenvoudig en wordt alleen gedemonstreerd hoe u uw clientapp test door meldingen te verzenden met de .NET SDK voor Notification Hubs in een consoletoepassing in plaats van een back-endservice.</span><span class="sxs-lookup"><span data-stu-id="057ae-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="057ae-153">U kunt het beste de zelfstudie [Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) doornemen voor informatie over het verzenden van meldingen vanuit een ASP.NET-back-end.</span><span class="sxs-lookup"><span data-stu-id="057ae-153">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="057ae-154">Voor het verzenden van meldingen kunt u echter de volgende methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="057ae-154">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="057ae-155">**REST-interface**: u kunt pushmeldingen op elk back-endplatform ondersteunen met de [REST-interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="057ae-155">**REST Interface**:  You can support push notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="057ae-156">**Microsoft Azure Notification Hubs .NET SDK**: in NuGet Package Manager voor Visual Studio voert u [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) uit.</span><span class="sxs-lookup"><span data-stu-id="057ae-156">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="057ae-157">**Node.js**: [Notification Hubs gebruiken vanuit Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="057ae-157">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="057ae-158">**Mobile Apps**: zie [Pushmeldingen toevoegen voor mobiele apps](../app-service-mobile/app-service-mobile-ios-get-started-push.md) voor een voorbeeld van hoe u meldingen verzendt vanuit een Azure App Service Mobile Apps-backend die is geïntegreerd met Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="057ae-158">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="057ae-159">**Java/PHP**: zie 'Notification Hubs gebruiken vanuit Java/PHP' voor een voorbeeld van hoe u pushmeldingen verzendt met de REST API's ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="057ae-159">**Java / PHP**: For an example of how to send push notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="057ae-160">(Optioneel) Pushmeldingen verzenden vanuit een .NET-console-app</span><span class="sxs-lookup"><span data-stu-id="057ae-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="057ae-161">In deze sectie worden pushmeldingen verzonden met een eenvoudige .NET-console-app.</span><span class="sxs-lookup"><span data-stu-id="057ae-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="057ae-162">Voor dit voorbeeld wordt overgeschakeld naar een Windows-ontwikkelomgeving waarin Visual Studio al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="057ae-162">For the purposes of this example, we will switch to a Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="057ae-163">Maak in Visual Studio een nieuwe Visual C#-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="057ae-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="057ae-164">Klik in Visual Studio achtereenvolgens op **Extra**, **NuGet Package Manager** en **Package Manager-console**.</span><span class="sxs-lookup"><span data-stu-id="057ae-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="057ae-165">De Package Manager-console moet vastgezet aan de onderkant van de Visual Studio-werkruimte worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="057ae-165">The package manager console should appear docked to the bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="057ae-166">Stel in het venster Package Manager-console het **standaardproject** in op uw nieuwe consoletoepassingsproject en voer vervolgens in het consolevenster de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="057ae-166">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="057ae-167">Hiermee wordt een verwijzing toegevoegd aan de Azure Notification Hubs SDK met het <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="057ae-167">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="057ae-168">Open het bestand `Program.cs` en voeg de volgende `using`-instructie toe, waarbij u ervoor zorgt dat we Azure-klassen en -functies binnen uw hoofdklasse kunnen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="057ae-168">Open the `Program.cs` file and add the following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="057ae-169">Voeg in de klasse `Program` de volgende methode toe (vergeet niet om de **verbindingsreeks** en **hubnaam** te vervangen):</span><span class="sxs-lookup"><span data-stu-id="057ae-169">In your `Program` class, add the following method (don't forget to replace the **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="057ae-170">Voeg de volgende regels in de `Main`-methode toe:</span><span class="sxs-lookup"><span data-stu-id="057ae-170">Add the following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="057ae-171">Druk op de toets F5 om de app uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="057ae-171">Press the F5 key to run the app.</span></span> <span data-ttu-id="057ae-172">Binnen enkele seconden wordt een pushmelding op uw apparaat weergegeven.</span><span class="sxs-lookup"><span data-stu-id="057ae-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="057ae-173">Zorg ervoor dat u via Wi-Fi of een mobiele verbinding voor dataverkeer een actieve internetverbinding op het apparaat hebt.</span><span class="sxs-lookup"><span data-stu-id="057ae-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on the device.</span></span>

<span data-ttu-id="057ae-174">U kunt alle mogelijke nettoladingen vinden in de [Programmeerhandleiding voor lokale en pushmeldingen] van Apple.</span><span class="sxs-lookup"><span data-stu-id="057ae-174">You can find all the possible payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="057ae-175">(Optioneel) Meldingen verzenden vanuit een mobiele service</span><span class="sxs-lookup"><span data-stu-id="057ae-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="057ae-176">In deze sectie worden pushmeldingen verzonden met een mobiele service via een knooppuntscript.</span><span class="sxs-lookup"><span data-stu-id="057ae-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="057ae-177">Als u een melding wilt verzenden met een mobiele service, volgt u [Aan de slag met Mobile Services] en gaat u daarna als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="057ae-177">To send a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="057ae-178">Meld u aan bij de [Klassieke Azure-portal] en selecteer uw mobiele service.</span><span class="sxs-lookup"><span data-stu-id="057ae-178">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="057ae-179">Selecteer het tabblad **Scheduler** aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="057ae-179">Select the **Scheduler** tab on the top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="057ae-180">Maak een nieuwe geplande taak, voeg een naam in en selecteer **Op aanvraag**.</span><span class="sxs-lookup"><span data-stu-id="057ae-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="057ae-181">Wanneer de taak is gemaakt, klikt u op de taaknaam.</span><span class="sxs-lookup"><span data-stu-id="057ae-181">When the job is created, click the job name.</span></span> <span data-ttu-id="057ae-182">Klik vervolgens op het tabblad **Script** op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="057ae-182">Then click the **Script** tab on the top bar.</span></span>
5. <span data-ttu-id="057ae-183">Voeg het volgende script in de plannerfunctie in.</span><span class="sxs-lookup"><span data-stu-id="057ae-183">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="057ae-184">Zorg ervoor dat de tijdelijke aanduidingen worden vervangen door de Notification Hub-naam en de verbindingsreeks voor *DefaultFullSharedAccessSignature* die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="057ae-184">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="057ae-185">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="057ae-185">Click **Save**.</span></span>
   
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
6. <span data-ttu-id="057ae-186">Klik op **Eenmaal uitvoeren** op de balk onderaan.</span><span class="sxs-lookup"><span data-stu-id="057ae-186">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="057ae-187">U ontvangt een waarschuwing op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="057ae-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="057ae-188">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="057ae-188">Next steps</span></span>
<span data-ttu-id="057ae-189">In dit eenvoudige voorbeeld hebt u pushmeldingen uitgezonden naar al uw iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="057ae-189">In this simple example, you broadcasted push notifications to all your iOS devices.</span></span> <span data-ttu-id="057ae-190">Als u zich op specifieke gebruikers wilt richten, raadpleegt u de zelfstudie [Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden].</span><span class="sxs-lookup"><span data-stu-id="057ae-190">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="057ae-191">Als u gebruikers wilt indelen op belangengroepen, raadpleegt u [Notification Hubs gebruiken om belangrijk nieuws te verzenden].</span><span class="sxs-lookup"><span data-stu-id="057ae-191">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="057ae-192">Lees meer over het gebruik van Notification Hubs in [Richtlijnen voor Notification Hubs] en in [Notification Hubs-procedure voor iOS].</span><span class="sxs-lookup"><span data-stu-id="057ae-192">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for iOS].</span></span>

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

<span data-ttu-id="057ae-193">[Aan de slag met Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span><span class="sxs-lookup"><span data-stu-id="057ae-193">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span></span>
<span data-ttu-id="057ae-194">[Klassieke Azure-portal]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="057ae-194">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="057ae-195">[Richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="057ae-195">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="057ae-196">[Notification Hubs-procedure voor iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span><span class="sxs-lookup"><span data-stu-id="057ae-196">[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span></span>
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

<span data-ttu-id="057ae-197">[Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="057ae-197">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="057ae-198">[Notification Hubs gebruiken om belangrijk nieuws te verzenden]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="057ae-198">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

<span data-ttu-id="057ae-199">[Programmeerhandleiding voor lokale en pushmeldingen]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span><span class="sxs-lookup"><span data-stu-id="057ae-199">[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span></span>
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="057ae-200">[Xamarin Studio]: http://xamarin.com/download</span><span class="sxs-lookup"><span data-stu-id="057ae-200">[Xamarin Studio]: http://xamarin.com/download</span></span>
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
<span data-ttu-id="057ae-201">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="057ae-201">[Azure Portal]: https://portal.azure.com</span></span>
