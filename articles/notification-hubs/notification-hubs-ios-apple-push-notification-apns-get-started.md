---
title: Pushmeldingen verzenden naar iOS met Azure Notification Hubs | Microsoft Docs
description: In deze zelfstudie leert u hoe u met Azure Notification Hubs pushmeldingen verzendt naar een iOS-toepassing.
services: notification-hubs
documentationcenter: ios
keywords: pushmelding,pushmeldingen,ios-pushmeldingen
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: ab0777f859e80afcd61e371056b44d018c7b7ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-ios-with-azure-notification-hubs"></a><span data-ttu-id="0cd69-104">Pushmeldingen verzenden naar iOS met Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="0cd69-104">Sending push notifications to iOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0cd69-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0cd69-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="0cd69-106">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="0cd69-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="0cd69-107">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="0cd69-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0cd69-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0cd69-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="0cd69-109">In deze zelfstudie wordt gedemonstreerd hoe u met Azure Notification Hubs pushmeldingen verzendt naar een iOS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0cd69-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span> <span data-ttu-id="0cd69-110">U maakt een lege iOS-app die pushmeldingen ontvangt met de [Apple Push Notification Service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="0cd69-110">You'll create a blank iOS app that receives push notifications by using the [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="0cd69-111">Als u klaar bent, kunt u de Notification Hub gebruiken om pushmeldingen uit te zenden naar alle apparaten waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0cd69-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0cd69-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="0cd69-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="0cd69-113">De volledige code voor deze zelfstudie vindt u [op GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="0cd69-113">The completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0cd69-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0cd69-114">Prerequisites</span></span>
<span data-ttu-id="0cd69-115">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="0cd69-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="0cd69-116">[iOS SDK Mobile Services versie 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="0cd69-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="0cd69-117">Meest recente versie van [Xcode]</span><span class="sxs-lookup"><span data-stu-id="0cd69-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="0cd69-118">Een apparaat dat compatibel is met iOS 8 (of een hogere versie)</span><span class="sxs-lookup"><span data-stu-id="0cd69-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="0cd69-119">[Apple Developer Program](https://developer.apple.com/programs/)-lidmaatschap</span><span class="sxs-lookup"><span data-stu-id="0cd69-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="0cd69-120">Vanwege configuratievereisten voor pushmeldingen moet u pushmeldingen op een fysiek iOS-apparaat (iPhone of iPad) implementeren en testen in plaats van in de iOS-simulator.</span><span class="sxs-lookup"><span data-stu-id="0cd69-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of the iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="0cd69-121">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor iOS-apps.</span><span class="sxs-lookup"><span data-stu-id="0cd69-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="0cd69-122">De Notification Hub voor iOS-pushmeldingen configureren</span><span class="sxs-lookup"><span data-stu-id="0cd69-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="0cd69-123">In deze sectie wordt u begeleid bij het maken van een nieuwe Notification Hub en het configureren van verificatie met APNs met het **.p12**-pushcertificaat dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0cd69-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="0cd69-124">Als u een Notification Hub wilt gebruiken die u al hebt gemaakt, kunt u doorgaan naar stap 5.</span><span class="sxs-lookup"><span data-stu-id="0cd69-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="0cd69-125">Klik op de knop <b>Notification Services</b> op de blade <b>Instellingen</b> en selecteer vervolgens <b>Apple (APNs)</b>.</span><span class="sxs-lookup"><span data-stu-id="0cd69-125">Click the <b>Notification Services</b> button in the <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="0cd69-126">Klik op <b>Certificaat uploaden</b> en selecteer het <b>.p12</b>-bestand dat u eerder hebt geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="0cd69-126">Click on <b>Upload Certificate</b> and select the <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="0cd69-127">Zorg ervoor dat u het juiste wachtwoord opgeeft.</span><span class="sxs-lookup"><span data-stu-id="0cd69-127">Make sure you also specify the correct password.</span></span></p>

<p><span data-ttu-id="0cd69-128">Zorg ervoor dat u de modus <b>Sandbox</b> selecteert. Dit is de juiste ontwikkelingsmodus.</span><span class="sxs-lookup"><span data-stu-id="0cd69-128">Make sure to select <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="0cd69-129">Gebruik <b>Productie</b> alleen als u pushmeldingen wilt verzenden naar gebruikers die uw app in de winkel hebben aangeschaft.</span><span class="sxs-lookup"><span data-stu-id="0cd69-129">Only use the <b>Production</b> if you want to send push notifications to users who purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="0cd69-130">&emsp;&emsp;&emsp;&emsp;![APNS configureren in Azure-Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="0cd69-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![APNs-certificering in Azure Portal configureren](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="0cd69-132">De Notification Hub is nu geconfigureerd om te werken met APNs en u hebt de verbindingsreeksen om uw app te registreren en pushmeldingen te verzenden.</span><span class="sxs-lookup"><span data-stu-id="0cd69-132">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-to-notification-hubs"></a><span data-ttu-id="0cd69-133">Uw iOS-app verbinden met Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="0cd69-133">Connect your iOS app to Notification Hubs</span></span>
1. <span data-ttu-id="0cd69-134">Maak in Xcode een nieuw iOS-project en selecteer de sjabloon **Single View Application** (Toepassing met één weergave).</span><span class="sxs-lookup"><span data-stu-id="0cd69-134">In Xcode, create a new iOS project and select the **Single View Application** template.</span></span>
   
    ![Xcode - Toepassing voor één weergave][8]
    
2. <span data-ttu-id="0cd69-136">Bij het instellen van de opties voor het nieuwe project moet u dezelfde **productnaam** en **organisatie-id** gebruiken als bij het instellen van de bundel-id op de Apple Developer portal.</span><span class="sxs-lookup"><span data-stu-id="0cd69-136">When setting the options for your new project, make sure to use the same **Product Name** and **Organization Identifier** that you used when you previously set the bundle ID on the Apple Developer portal.</span></span>
   
    ![Xcode - Projectopties][11]
    
3. <span data-ttu-id="0cd69-138">Klik onder **Targets** op de projectnaam, klik op het tabblad **Build Settings** (Instellingen opbouwen) en vouw **Code Signing Identity** (Identiteit voor ondertekening) uit. Stel vervolgens onder **Debug** (Fouten opsporen) uw identiteit voor ondertekening van programmacode in.</span><span class="sxs-lookup"><span data-stu-id="0cd69-138">Under **Targets**, click your project name, click the **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="0cd69-139">Schakel **Levels** (Niveaus) van **Basic** (Basis) naar **All** (Alle) en stel **Provisioning Profile** (Profiel voor inrichting) in op het profiel voor inrichting dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0cd69-139">Toggle **Levels** from **Basic** to **All**, and set **Provisioning Profile** to the provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="0cd69-140">Als u het nieuwe profiel voor inrichting dat u hebt gemaakt in Xcode niet ziet, vernieuwt u de profielen voor uw identiteit voor ondertekening.</span><span class="sxs-lookup"><span data-stu-id="0cd69-140">If you don't see the new provisioning profile that you created in Xcode, try refreshing the profiles for your signing identity.</span></span> <span data-ttu-id="0cd69-141">Klik op **Xcode** in de menubalk, klik op **Preferences** (Voorkeuren), klik op het tabblad **Account** en klik op de knop **View Details** (Details weergeven), klik op uw identiteit voor ondertekening en klik vervolgens op de knop voor vernieuwen in de rechterbenedenhoek.</span><span class="sxs-lookup"><span data-stu-id="0cd69-141">Click **Xcode** on the menu bar, click **Preferences**, click the **Account** tab, click the **View Details** button, click your signing identity, and then click the refresh button in the bottom-right corner.</span></span>
   
    ![Xcode - Profiel voor inrichting][9]
4. <span data-ttu-id="0cd69-143">Download de [iOS SDK Mobile Services versie 1.2.4] en pak het bestand uit.</span><span class="sxs-lookup"><span data-stu-id="0cd69-143">Download the [Mobile Services iOS SDK version 1.2.4] and unzip the file.</span></span> <span data-ttu-id="0cd69-144">Klik met de rechtermuisknop op uw project in Xcode en klik op de optie **Add Files to** (Bestanden toevoegen aan) om de map **WindowsAzureMessaging.framework** aan uw Xcode-project toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="0cd69-144">In Xcode, right-click your project and click the **Add Files to** option to add the **WindowsAzureMessaging.framework** folder to your Xcode project.</span></span> <span data-ttu-id="0cd69-145">Selecteer **Copy items if needed** (Items kopiëren indien nodig) en klik vervolgens op **Add**.</span><span class="sxs-lookup"><span data-stu-id="0cd69-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0cd69-146">Op dit moment biedt de Notification Hubs SDK geen ondersteuning voor bitcode op Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="0cd69-146">The notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="0cd69-147">U moet **Enable Bitcode** (Bitcode inschakelen) instellen op **No** (Nee) in **Build Options** (Opties voor opbouwen) voor uw project.</span><span class="sxs-lookup"><span data-stu-id="0cd69-147">You must set **Enable Bitcode** to **No** in the **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Azure SDK uitpakken][10]
5. <span data-ttu-id="0cd69-149">Voeg een nieuw headerbestand toe aan uw project met de naam `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="0cd69-149">Add a new header file to your project named `HubInfo.h`.</span></span> <span data-ttu-id="0cd69-150">Dit bestand is bedoeld voor de constanten voor uw Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="0cd69-150">This file will hold the constants for your notification hub.</span></span>  <span data-ttu-id="0cd69-151">Voeg de volgende definities toe en vervang de tijdelijke aanduidingen voor tekenreeksen door uw *hubnaam* en de *DefaultListenSharedAccessSignature* die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="0cd69-151">Add the following definitions and replace the string literal placeholders with your *hub name* and the *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter the name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="0cd69-152">Open uw bestand `AppDelegate.h` en voeg de volgende instructies voor importeren toe:</span><span class="sxs-lookup"><span data-stu-id="0cd69-152">Open your `AppDelegate.h` file add the following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="0cd69-153">Voeg in uw `AppDelegate.m file` de volgende code toe in de `didFinishLaunchingWithOptions`-methode op basis van uw versie van iOS.</span><span class="sxs-lookup"><span data-stu-id="0cd69-153">In your `AppDelegate.m file`, add the following code in the `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="0cd69-154">Deze code registreert uw apparaatingang met APNs:</span><span class="sxs-lookup"><span data-stu-id="0cd69-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="0cd69-155">Voor iOS 8:</span><span class="sxs-lookup"><span data-stu-id="0cd69-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="0cd69-156">Voor oudere iOS-versies:</span><span class="sxs-lookup"><span data-stu-id="0cd69-156">For iOS versions prior to 8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="0cd69-157">Voeg in hetzelfde bestand de volgende methoden toe.</span><span class="sxs-lookup"><span data-stu-id="0cd69-157">In the same file, add the following methods.</span></span> <span data-ttu-id="0cd69-158">Deze code maakt verbinding met de Notification Hub met de verbindingsgegevens die u hebt opgegeven in HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="0cd69-158">This code connects to the notification hub using the connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="0cd69-159">Er wordt vervolgens een apparaattoken aan de Notification Hub toegekend, zodat de Notification Hub meldingen kan verzenden:</span><span class="sxs-lookup"><span data-stu-id="0cd69-159">It then gives the device token to the notification hub so that the notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="0cd69-160">Voeg in hetzelfde bestand de volgende methode toe om een **UIAlert** weer te geven als de melding is ontvangen terwijl de app actief is:</span><span class="sxs-lookup"><span data-stu-id="0cd69-160">In the same file, add the following method to display a **UIAlert** if the notification is received while the app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="0cd69-161">Ontwikkel en voer de app op uw apparaat uit om te controleren of er geen fouten zijn.</span><span class="sxs-lookup"><span data-stu-id="0cd69-161">Build and run the app on your device to verify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="0cd69-162">Testpushmeldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="0cd69-162">Send test push notifications</span></span>
<span data-ttu-id="0cd69-163">U kunt testen of u meldingen in uw app ontvangt door pushmeldingen te verzenden via [Azure Portal]. Ga naar het gedeelte **Probleemoplossing** in de hubblade (en gebruik de optie *Test verzenden*).</span><span class="sxs-lookup"><span data-stu-id="0cd69-163">You can test receiving notifications in your app by sending push notifications in the [Azure Portal] via the **Troubleshooting** section in the hub blade (use the *Test Send* option).</span></span>

![Azure -portal - Test verzenden][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-the-app"></a><span data-ttu-id="0cd69-165">(Optioneel) Pushmeldingen vanuit de app verzenden</span><span class="sxs-lookup"><span data-stu-id="0cd69-165">(Optional) Send push notifications from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0cd69-166">Dit voorbeeld van het verzenden van meldingen vanuit de client-app wordt uitsluitend voor educatieve doeleinden aangeboden.</span><span class="sxs-lookup"><span data-stu-id="0cd69-166">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="0cd69-167">Aangezien het hiervoor noodzakelijk is dat de `DefaultFullSharedAccessSignature` aanwezig is op de client-app, loopt uw Notification Hub het risico dat een gebruiker toegang kan krijgen en onbevoegd meldingen naar uw clients kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="0cd69-167">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="0cd69-168">Als u pushmeldingen vanuit een app wilt verzenden, vindt u in deze sectie een voorbeeld van hoe u dit doet met de REST-interface.</span><span class="sxs-lookup"><span data-stu-id="0cd69-168">If you want to send push notifications from within an app, this section provides an example of how to do this using the REST interface.</span></span>

1. <span data-ttu-id="0cd69-169">Open `Main.storyboard` in Xcode en voeg de volgende gebruikersinterfaceonderdelen van de objectbibliotheek toe om in te stellen dat de gebruiker pushmeldingen in de app kan verzenden:</span><span class="sxs-lookup"><span data-stu-id="0cd69-169">In Xcode, open `Main.storyboard` and add the following UI components from the object library to allow the user to send push notifications in the app:</span></span>
   
   * <span data-ttu-id="0cd69-170">Een label zonder labeltekst.</span><span class="sxs-lookup"><span data-stu-id="0cd69-170">A label with no label text.</span></span> <span data-ttu-id="0cd69-171">Dit wordt gebruikt om fouten tijdens het verzenden van meldingen te rapporteren.</span><span class="sxs-lookup"><span data-stu-id="0cd69-171">It will be used to report errors in sending notifications.</span></span> <span data-ttu-id="0cd69-172">De eigenschap **Rules** (Regels) moet worden ingesteld op **0**, zodat de grootte naar de rechter- en linkermarges en de bovenkant van de weergave automatisch wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="0cd69-172">The **Lines** property should be set to **0** so that it will automatically size constrained to the right and left margins and the top of the view.</span></span>
   * <span data-ttu-id="0cd69-173">Een tekstveld met **tijdelijke** tekst ingesteld op **Enter Notification Message** (Meldingstekst invoeren).</span><span class="sxs-lookup"><span data-stu-id="0cd69-173">A text field with **Placeholder** text set to **Enter Notification Message**.</span></span> <span data-ttu-id="0cd69-174">Beperk het veld onder het label, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0cd69-174">Constrain the field just below the label as shown below.</span></span> <span data-ttu-id="0cd69-175">Stel de weergavebesturing in als de gemachtigde voor de aansluiting.</span><span class="sxs-lookup"><span data-stu-id="0cd69-175">Set the View Controller as the outlet delegate.</span></span>
   * <span data-ttu-id="0cd69-176">Een knop met de naam **Send Notification** (Melding verzenden) die direct onder het tekstveld en in horizontale richting is beperkt.</span><span class="sxs-lookup"><span data-stu-id="0cd69-176">A button titled **Send Notification** constrained just below the text field and in the horizontal center.</span></span>
     
     <span data-ttu-id="0cd69-177">De weergave ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="0cd69-177">The view should look as follows:</span></span>
     
     ![Xcode designer][32]
2. <span data-ttu-id="0cd69-179">[Voeg aansluitingen](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) voor het label en het tekstveld in uw weergave toe en werk uw `interface`-definitie bij om `UITextFieldDelegate` en `NSXMLParserDelegate` te ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="0cd69-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for the label and text field connected your view, and update your `interface` definition to support `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="0cd69-180">Voeg de drie eigenschapdeclaraties die hieronder worden weergegeven toe om het aanroepen van de REST-API en het parseren van het antwoord te ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="0cd69-180">Add the three property declarations shown below to help support calling the REST API and parsing the response.</span></span>
   
    <span data-ttu-id="0cd69-181">Uw ViewController.h-bestand moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="0cd69-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected to your UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="0cd69-182">Open `HubInfo.h` en voeg de volgende constanten toe, die worden gebruikt voor het verzenden van meldingen naar de hub.</span><span class="sxs-lookup"><span data-stu-id="0cd69-182">Open `HubInfo.h` and add the following constants which will be used for sending notifications to your hub.</span></span> <span data-ttu-id="0cd69-183">Vervang de tijdelijke aanduiding voor tekenreeksen door uw werkelijke *DefaultFullSharedAccessSignature*-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="0cd69-183">Replace the placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="0cd69-184">Voeg de volgende instructies voor `#import` toe aan uw `ViewController.h`-bestand.</span><span class="sxs-lookup"><span data-stu-id="0cd69-184">Add the following `#import` statements to your `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="0cd69-185">Voeg in `ViewController.m` de volgende code toe aan de implementatie van de interface.</span><span class="sxs-lookup"><span data-stu-id="0cd69-185">In `ViewController.m` add the following code to the interface implementation.</span></span> <span data-ttu-id="0cd69-186">Deze code parseert uw *DefaultFullSharedAccessSignature*-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="0cd69-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="0cd69-187">Zoals vermeld in de [REST-API-verwijzing](http://msdn.microsoft.com/library/azure/dn495627.aspx) wordt deze geparseerde informatie gebruikt om een SaS-token te genereren voor de aanvraagheader **Authorization** (Autorisatie).</span><span class="sxs-lookup"><span data-stu-id="0cd69-187">As mentioned in the [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used to generate a SaS token for the **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="0cd69-188">Werk in `ViewController.m` de `viewDidLoad`-methode bij voor het parseren van de verbindingsreeks zodra de weergave wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="0cd69-188">In `ViewController.m`, update the `viewDidLoad` method to parse the connection string when the view loads.</span></span> <span data-ttu-id="0cd69-189">Voeg ook de hulpprogrammamethoden die hieronder worden weergegeven toe aan de implementatie van de interface.</span><span class="sxs-lookup"><span data-stu-id="0cd69-189">Also add the utility methods, shown below, to the interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="0cd69-190">Voeg in `ViewController.m` de volgende code toe aan de implementatie van de interface om het SaS-autorisatietoken te genereren dat beschikbaar wordt gesteld in de koptekst **Authorization** (Autorisatie), zoals vermeld de [REST-API-verwijzing](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cd69-190">In `ViewController.m`, add the following code to the interface implementation to generate the SaS authorization token that will be provided in the **Authorization** header, as mentioned in the [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="0cd69-191">Houd CTRL ingedrukt en sleep vanaf de knop **Send Notification** (Melding verzenden) om `ViewController.m` een actie met de naam **SendNotificationMessage** voor de **Touch Down**-gebeurtenis toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="0cd69-191">Ctrl+drag from the **Send Notification** button to `ViewController.m` to add an action named **SendNotificationMessage** for the **Touch Down** event.</span></span> <span data-ttu-id="0cd69-192">Werk de methode bij met de volgende code om de melding via de REST-API te verzenden.</span><span class="sxs-lookup"><span data-stu-id="0cd69-192">Update method with the following code to send the notification using the REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of the notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct the message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate the token to be used in the authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the APNs notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="0cd69-193">Voeg in `ViewController.m` de volgende gemachtigdenmethode toe om het toetsenbord te sluiten voor het tekstveld.</span><span class="sxs-lookup"><span data-stu-id="0cd69-193">In `ViewController.m`, add the following delegate method to support closing the keyboard for the text field.</span></span> <span data-ttu-id="0cd69-194">Houd CTRL ingedrukt en sleep vanuit het tekstveld naar het pictogram voor weergavebesturing in de interface-ontwerper om de weergavebesturing instellen als de gemachtigde voor de aansluiting.</span><span class="sxs-lookup"><span data-stu-id="0cd69-194">Ctrl+drag from the text field to the View Controller icon in the interface designer to set the view controller as the outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="0cd69-195">Voeg in `ViewController.m` de volgende gemachtigdenmethoden toe om het antwoord via `NSXMLParser` te kunnen parseren.</span><span class="sxs-lookup"><span data-stu-id="0cd69-195">In `ViewController.m`, add the following delegate methods to support parsing the response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set the status label text on the UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="0cd69-196">Bouw het project en controleer of er geen fouten zijn.</span><span class="sxs-lookup"><span data-stu-id="0cd69-196">Build the project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="0cd69-197">Als u in Xcode7 een opbouwfout ontdekt met betrekking tot ondersteuning voor bitcode, moet u **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** (Instellingen voor opbouwen - Bitcode inschakelen) instellen op **No** (Nee) in Xcode.</span><span class="sxs-lookup"><span data-stu-id="0cd69-197">If you encounter a build error in Xcode7 about bitcode support, you should change the **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** to **NO** in Xcode.</span></span> <span data-ttu-id="0cd69-198">Op dit moment biedt de Notification Hubs SDK geen ondersteuning voor bitcode.</span><span class="sxs-lookup"><span data-stu-id="0cd69-198">The Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="0cd69-199">U vindt alle mogelijke nettoladingen van meldingen in de [Programmeerhandleiding voor lokale en pushmeldingen] van Apple.</span><span class="sxs-lookup"><span data-stu-id="0cd69-199">You can find all the possible notification payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="0cd69-200">Controleren of een app pushmeldingen kan ontvangen</span><span class="sxs-lookup"><span data-stu-id="0cd69-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="0cd69-201">Als u pushmeldingen op iOS wilt testen, moet u de app implementeren op een fysiek iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="0cd69-201">To test push notifications on iOS, you must deploy the app to a physical iOS device.</span></span> <span data-ttu-id="0cd69-202">U kunt geen Apple pushmeldingen verzenden via de iOS-simulator.</span><span class="sxs-lookup"><span data-stu-id="0cd69-202">You cannot send Apple push notifications by using the iOS Simulator.</span></span>

1. <span data-ttu-id="0cd69-203">Voer de app uit en controleer of de registratie is gelukt en druk vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0cd69-203">Run the app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![De registratie van pushmeldingen in iOS-apps testen][33]
2. <span data-ttu-id="0cd69-205">U kunt een pushmelding verzenden via [Azure Portal], zoals hierboven beschreven.</span><span class="sxs-lookup"><span data-stu-id="0cd69-205">You can send a test push notification from the [Azure Portal], as described above.</span></span> <span data-ttu-id="0cd69-206">Als u code voor het verzenden van pushmeldingen in de app hebt toegevoegd, gaat u naar het tekstvak om een meldingsbericht in te voeren.</span><span class="sxs-lookup"><span data-stu-id="0cd69-206">If you added code for sending push notifications in the app, touch inside the text field to enter a notification message.</span></span> <span data-ttu-id="0cd69-207">Druk op de knop **Verzenden** op het toetsenbord of op de knop **Melding verzenden** in de weergave om het meldingsbericht te verzenden.</span><span class="sxs-lookup"><span data-stu-id="0cd69-207">Then press the **Send** button on the keyboard or the **Send Notification** button in the view to send the notification message.</span></span>
   
    ![Het verzenden van pushmeldingen in iOS-apps testen][34]
3. <span data-ttu-id="0cd69-209">De pushmelding wordt verzonden naar alle apparaten die zijn geregistreerd voor het ontvangen van meldingen van de specifieke Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="0cd69-209">The push notification is sent to all devices that are registered to receive the notifications from the particular Notification Hub.</span></span>
   
    ![Het ontvangen van pushmeldingen in iOS-apps testen][35]

## <a name="next-steps"></a><span data-ttu-id="0cd69-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0cd69-211">Next steps</span></span>
<span data-ttu-id="0cd69-212">In dit eenvoudige voorbeeld hebt u pushmeldingen uitgezonden naar al uw geregistreerde iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="0cd69-212">In this simple example, you broadcasted push notifications to all your registered iOS devices.</span></span> <span data-ttu-id="0cd69-213">U kunt het beste de zelfstudie [Azure Notification Hubs - Een melding naar iOS-gebruikers verzenden met .NET back-end] doornemen. Hierin leert u hoe u een back-end kunt maken om pushmeldingen te verzenden met tags.</span><span class="sxs-lookup"><span data-stu-id="0cd69-213">We suggest as a next step in your learning that you proceed to the [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend to send push notifications using tags.</span></span> 

<span data-ttu-id="0cd69-214">Zie de zelfstudie [Notification Hubs gebruiken om belangrijk nieuws te verzenden] als u gebruikers wilt indelen op belangengroep.</span><span class="sxs-lookup"><span data-stu-id="0cd69-214">If you want to segment your users by interest groups, you can additionally move on to the [Use Notification Hubs to send breaking news] tutorial.</span></span> 

<span data-ttu-id="0cd69-215">Zie [Richtlijnen voor Notification Hubs] voor algemene informatie over Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="0cd69-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
<span data-ttu-id="0cd69-216">[iOS SDK Mobile Services versie 1.2.4]: http://aka.ms/kymw2g</span><span class="sxs-lookup"><span data-stu-id="0cd69-216">[Mobile Services iOS SDK version 1.2.4]: http://aka.ms/kymw2g</span></span>
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="0cd69-217">[Richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="0cd69-217">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="0cd69-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span><span class="sxs-lookup"><span data-stu-id="0cd69-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span></span>
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
<span data-ttu-id="0cd69-219">[Azure Notification Hubs - Een melding naar iOS-gebruikers verzenden met .NET back-end]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span><span class="sxs-lookup"><span data-stu-id="0cd69-219">[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span></span>
<span data-ttu-id="0cd69-220">[Notification Hubs gebruiken om belangrijk nieuws te verzenden]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="0cd69-220">[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span></span>

<span data-ttu-id="0cd69-221">[Programmeerhandleiding voor lokale en pushmeldingen]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span><span class="sxs-lookup"><span data-stu-id="0cd69-221">[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span></span>
<span data-ttu-id="0cd69-222">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="0cd69-222">[Azure Portal]: https://portal.azure.com</span></span>
