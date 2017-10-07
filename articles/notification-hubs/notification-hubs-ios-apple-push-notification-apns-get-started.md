---
title: aaaSending push notifications tooiOS met Azure Notification Hubs | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooan iOS-toepassing.
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
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="c0042-104">Push notifications tooiOS met Azure Notification Hubs verzenden</span><span class="sxs-lookup"><span data-stu-id="c0042-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c0042-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c0042-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="c0042-106">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="c0042-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c0042-107">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="c0042-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c0042-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c0042-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="c0042-109">Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooan iOS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c0042-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="c0042-110">Maakt u een lege iOS-app die pushmeldingen ontvangt via Hallo [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="c0042-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="c0042-111">Wanneer u klaar bent, moet u kunnen toouse push uw notification hub toobroadcast meldingen tooall Hallo apparaten waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c0042-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c0042-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c0042-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="c0042-113">Hallo voltooid code voor deze zelfstudie vindt [op GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="c0042-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c0042-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c0042-114">Prerequisites</span></span>
<span data-ttu-id="c0042-115">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="c0042-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="c0042-116">[iOS SDK Mobile Services versie 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="c0042-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="c0042-117">Meest recente versie van [Xcode]</span><span class="sxs-lookup"><span data-stu-id="c0042-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="c0042-118">Een apparaat dat compatibel is met iOS 8 (of een hogere versie)</span><span class="sxs-lookup"><span data-stu-id="c0042-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="c0042-119">[Apple Developer Program](https://developer.apple.com/programs/)-lidmaatschap</span><span class="sxs-lookup"><span data-stu-id="c0042-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c0042-120">Vanwege configuratievereisten voor pushmeldingen, moet u implementeren en testen van pushmeldingen op een fysiek iOS-apparaat (iPhone of iPad) in plaats van Hallo iOS-Simulator.</span><span class="sxs-lookup"><span data-stu-id="c0042-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="c0042-121">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor iOS-apps.</span><span class="sxs-lookup"><span data-stu-id="c0042-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="c0042-122">De Notification Hub voor iOS-pushmeldingen configureren</span><span class="sxs-lookup"><span data-stu-id="c0042-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="c0042-123">Deze sectie leidt u door een nieuwe notification hub maken en configureren van verificatie met APNS met Hallo **.p12** pushcertificaat dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c0042-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="c0042-124">Als u toouse een notification hub die u al hebt gemaakt wilt, kunt u toostep 5 overslaan.</span><span class="sxs-lookup"><span data-stu-id="c0042-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="c0042-125">Klik op Hallo <b>Notification Services</b> knop in Hallo <b>instellingen</b> blade Selecteer <b>Apple (APNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="c0042-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="c0042-126">Klik op <b>certificaat uploaden</b> en selecteer Hallo <b>.p12</b> -bestand dat u eerder hebt geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="c0042-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="c0042-127">Zorg ervoor dat u ook het juiste wachtwoord Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="c0042-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="c0042-128">Zorg ervoor dat tooselect <b>Sandbox</b> modus, aangezien dit voor ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="c0042-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="c0042-129">Gebruik alleen Hallo <b>productie</b> als u wilt dat toosend push notifications toousers die uw app uit de store Hallo aangeschaft.</span><span class="sxs-lookup"><span data-stu-id="c0042-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="c0042-130">&emsp;&emsp;&emsp;&emsp;![APNS configureren in Azure-Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="c0042-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![APNs-certificering in Azure Portal configureren](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="c0042-132">Uw notification hub is nu geconfigureerd toowork met APNS en u hebt Hallo verbinding tekenreeksen tooregister uw app en om pushmeldingen te verzenden.</span><span class="sxs-lookup"><span data-stu-id="c0042-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="c0042-133">Verbinding maken met uw iOS-app tooNotification Hubs</span><span class="sxs-lookup"><span data-stu-id="c0042-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="c0042-134">Maak een nieuw iOS-project in Xcode en selecteer Hallo **enkele toepassingsweergave** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c0042-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode - Toepassing voor één weergave][8]
    
2. <span data-ttu-id="c0042-136">Wanneer u opties voor het nieuwe project hello, zorg ervoor dat toouse Hallo dezelfde **Productnaam** en **organisatie-id** dat u gebruikt wanneer u eerder Hallo bundel-ID ingesteld op Hallo Apple Developer Portal.</span><span class="sxs-lookup"><span data-stu-id="c0042-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode - Projectopties][11]
    
3. <span data-ttu-id="c0042-138">Onder **doelen**, klik op de projectnaam van uw, Hallo **Build Settings** tabblad en vouw **Code Signing Identity**, en klik vervolgens onder **Debug**, instellen van uw identiteit voor ondertekening van programmacode.</span><span class="sxs-lookup"><span data-stu-id="c0042-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="c0042-139">Wisselknop **niveaus** van **Basic** te**alle**, en stel **profiel inrichting** toohello inrichtingsprofiel die u eerder hebt gemaakt .</span><span class="sxs-lookup"><span data-stu-id="c0042-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="c0042-140">Als u Hallo nieuwe inrichtingsprofiel die u hebt gemaakt in Xcode niet ziet, vernieuw u Hallo profielen voor uw identiteit voor ondertekening.</span><span class="sxs-lookup"><span data-stu-id="c0042-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="c0042-141">Klik op **Xcode** op de menubalk hello, klikt u op **voorkeuren**, klikt u op Hallo **Account** en klik op Hallo **Details weergeven** knop, klikt u op uw ondertekening van de identiteit en klik vervolgens op Hallo de knop Vernieuwen in de rechterbenedenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0042-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode - Profiel voor inrichting][9]
4. <span data-ttu-id="c0042-143">Hallo downloaden [iOS SDK Mobile Services versie 1.2.4] en pak Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="c0042-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="c0042-144">Met de rechtermuisknop op uw project in Xcode en klik op Hallo **bestanden toevoegen aan** optie tooadd hello **WindowsAzureMessaging.framework** map tooyour Xcode-project.</span><span class="sxs-lookup"><span data-stu-id="c0042-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="c0042-145">Selecteer **Copy items if needed** (Items kopiëren indien nodig) en klik vervolgens op **Add**.</span><span class="sxs-lookup"><span data-stu-id="c0042-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c0042-146">Hallo notification hubs SDK geen momenteel ondersteuning voor bitcode op Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="c0042-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="c0042-147">U moet instellen **Bitcode inschakelen** te**Nee** in Hallo **opties bouwen** voor uw project.</span><span class="sxs-lookup"><span data-stu-id="c0042-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Azure SDK uitpakken][10]
5. <span data-ttu-id="c0042-149">Voeg een nieuw tooyour project voor header-bestand met de naam `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="c0042-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="c0042-150">Dit bestand bevatten Hallo constanten voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="c0042-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="c0042-151">Toevoegen van de volgende definities Hallo en vervang Hallo string literal tijdelijke aanduidingen door uw *hubnaam* en Hallo *DefaultListenSharedAccessSignature* die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="c0042-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="c0042-152">Open uw `AppDelegate.h` bestand toevoegen Hallo importeren richtlijnen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c0042-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="c0042-153">In uw `AppDelegate.m file`, toevoegen van de volgende code in Hallo Hallo `didFinishLaunchingWithOptions` methode op basis van uw iOS-versie.</span><span class="sxs-lookup"><span data-stu-id="c0042-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="c0042-154">Deze code registreert uw apparaatingang met APNs:</span><span class="sxs-lookup"><span data-stu-id="c0042-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="c0042-155">Voor iOS 8:</span><span class="sxs-lookup"><span data-stu-id="c0042-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="c0042-156">Voor eerdere too8 voor de iOS-versies:</span><span class="sxs-lookup"><span data-stu-id="c0042-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="c0042-157">In hetzelfde bestand Hallo, Hallo volgende methoden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c0042-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="c0042-158">Deze code maakt verbinding toohello notification hub is met Hallo-verbindingsgegevens die u hebt opgegeven in HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="c0042-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="c0042-159">Deze geeft vervolgens Hallo apparaat token toohello notification hub zodat hello notification hub meldingen kan verzenden:</span><span class="sxs-lookup"><span data-stu-id="c0042-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
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
9. <span data-ttu-id="c0042-160">In hetzelfde bestand hello, het toevoegen van Hallo methode toodisplay na een **UIAlert** als Hallo melding is ontvangen terwijl Hallo app actief is:</span><span class="sxs-lookup"><span data-stu-id="c0042-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="c0042-161">Ontwikkel en Voer Hallo-app op uw apparaat tooverify dat er geen fouten zijn.</span><span class="sxs-lookup"><span data-stu-id="c0042-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="c0042-162">Testpushmeldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="c0042-162">Send test push notifications</span></span>
<span data-ttu-id="c0042-163">U kunt testen door meldingen in uw app ontvangt door pushmeldingen te verzenden in Hallo [Azure Portal] via Hallo **probleemoplossing** sectie in de hubblade hello (hello gebruiken *Testverzenden* optie).</span><span class="sxs-lookup"><span data-stu-id="c0042-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Azure -portal - Test verzenden][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="c0042-165">(Optioneel) Pushmeldingen verzenden vanuit Hallo-app</span><span class="sxs-lookup"><span data-stu-id="c0042-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c0042-166">In dit voorbeeld van het verzenden van meldingen vanuit Hallo client-app is beschikbaar voor uitsluitend leren.</span><span class="sxs-lookup"><span data-stu-id="c0042-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="c0042-167">Aangezien hiervoor Hallo `DefaultFullSharedAccessSignature` toobe aanwezig is op de client-app Hallo, beschrijft deze uw notification hub toohello risico dat een gebruiker kan toegang toosend unauthorized Toegangsmeldingen tooyour clients.</span><span class="sxs-lookup"><span data-stu-id="c0042-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="c0042-168">Als u toosend pushmeldingen vanuit een app wilt, deze sectie bevat een voorbeeld van hoe toodo deze met Hallo REST-interface.</span><span class="sxs-lookup"><span data-stu-id="c0042-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="c0042-169">Open in Xcode, `Main.storyboard` en Hallo volgende UI-onderdelen uit Hallo object bibliotheek tooallow Hallo gebruiker toosend pushmeldingen in Hallo app toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="c0042-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="c0042-170">Een label zonder labeltekst.</span><span class="sxs-lookup"><span data-stu-id="c0042-170">A label with no label text.</span></span> <span data-ttu-id="c0042-171">Gebruikte tooreport fouten tijdens het verzenden van meldingen zal zijn.</span><span class="sxs-lookup"><span data-stu-id="c0042-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="c0042-172">Hallo **regels** eigenschap te moet worden ingesteld**0** zodat deze wordt het formaat automatisch beperkte toohello rechts en linkermarges en Hallo Hallo weergave bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c0042-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="c0042-173">Een tekstveld met **tijdelijke aanduiding voor** tekst ingesteld te**meldingstekst invoeren**.</span><span class="sxs-lookup"><span data-stu-id="c0042-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="c0042-174">Beperken Hallo veld onder Hallo label, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c0042-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="c0042-175">Hallo weergavebesturing instellen als Hallo aansluiting gemachtigde.</span><span class="sxs-lookup"><span data-stu-id="c0042-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="c0042-176">Een knop met de titel **melding verzenden** beperkte direct onder het tekstveld hello en in horizontale richting Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0042-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="c0042-177">Hallo weergave ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="c0042-177">hello view should look as follows:</span></span>
     
     ![Xcode designer][32]
2. <span data-ttu-id="c0042-179">[Voeg aansluitingen](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) voor het label en het tekstveld veld Hallo uw weergave verbonden en werk uw `interface` definitie toosupport `UITextFieldDelegate` en `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="c0042-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="c0042-180">Hallo drie eigenschapdeclaraties toohelp ondersteuning Hallo REST-API aanroepen en parseren van antwoord Hallo hieronder toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c0042-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="c0042-181">Uw ViewController.h-bestand moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="c0042-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="c0042-182">Open `HubInfo.h` en voeg de volgende constanten die worden gebruikt voor het verzenden van meldingen tooyour hub Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0042-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="c0042-183">Hallo tijdelijke aanduiding voor letterlijke tekenreeks vervangen door uw werkelijke *DefaultFullSharedAccessSignature* verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="c0042-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="c0042-184">Voeg de volgende Hallo `#import` instructies tooyour `ViewController.h` bestand.</span><span class="sxs-lookup"><span data-stu-id="c0042-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="c0042-185">In `ViewController.m` Hallo na de implementatie van de interface toohello code toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c0042-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="c0042-186">Deze code parseert uw *DefaultFullSharedAccessSignature*-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="c0042-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="c0042-187">Zoals vermeld in Hallo [naslaginformatie over REST API](http://msdn.microsoft.com/library/azure/dn495627.aspx), worden deze geparseerde informatie gebruikt toogenerate een SaS-token voor Hallo **autorisatie** aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="c0042-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
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
6. <span data-ttu-id="c0042-188">In `ViewController.m`, update Hallo `viewDidLoad` methode tooparse Hallo verbindingsreeks wanneer Hallo weergave wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="c0042-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="c0042-189">Ook toevoegen Hallo hulpprogrammamethoden die hieronder worden weergegeven toohello interface-implementatie.</span><span class="sxs-lookup"><span data-stu-id="c0042-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

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





1. <span data-ttu-id="c0042-190">In `ViewController.m`, toevoegen van de volgende code toohello interface implementatie toogenerate Hallo SaS-Autorisatietoken die worden vermeld in Hallo Hallo **autorisatie** -kop, zoals vermeld in Hallo [REST-API Verwijzing](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0042-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
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
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
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
2. <span data-ttu-id="c0042-191">CTRL + Sleep vanuit Hallo **melding verzenden** te knop`ViewController.m` tooadd een actie met de naam **SendNotificationMessage** voor Hallo **Touch Down** gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="c0042-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="c0042-192">De methode Update Hello na de code toosend Hallo kennisgeving Hallo REST-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c0042-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
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
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
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
3. <span data-ttu-id="c0042-193">In `ViewController.m`, Hallo gemachtigde methode toosupport Hallo toetsenbord voor Hallo tekstveld sluiten na toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c0042-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="c0042-194">CTRL + Sleep vanuit Hallo tekst veld toohello pictogram voor weergavebesturing in Hallo interface designer tooset Hallo weergeven controller Hallo aansluiting gemachtigde.</span><span class="sxs-lookup"><span data-stu-id="c0042-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="c0042-195">In `ViewController.m`, voeg Hallo volgende antwoord Hallo bij het parseren van methoden toosupport delegeren met behulp van `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="c0042-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
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
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="c0042-196">Hallo-project te bouwen en controleer of er zijn geen fouten.</span><span class="sxs-lookup"><span data-stu-id="c0042-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="c0042-197">Als u een opbouwfout in Xcode7 ondersteuning voor bitcode optreden, moet u Hallo **Build Settings** > **inschakelen Bitcode (ENABLE_BITCODE)** te**Nee** in Xcode.</span><span class="sxs-lookup"><span data-stu-id="c0042-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="c0042-198">Hallo Notification Hubs SDK biedt momenteel geen ondersteuning voor bitcode.</span><span class="sxs-lookup"><span data-stu-id="c0042-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="c0042-199">U vindt alle Hallo mogelijke nettoladingen van meldingen in Hallo Apple [Local and Push Notification Programming Guide].</span><span class="sxs-lookup"><span data-stu-id="c0042-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="c0042-200">Controleren of een app pushmeldingen kan ontvangen</span><span class="sxs-lookup"><span data-stu-id="c0042-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="c0042-201">tootest pushmeldingen op iOS, moet u Hallo app tooa fysiek iOS-apparaat implementeren.</span><span class="sxs-lookup"><span data-stu-id="c0042-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="c0042-202">U kunt geen Apple pushmeldingen verzenden met behulp van Hallo iOS-Simulator.</span><span class="sxs-lookup"><span data-stu-id="c0042-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="c0042-203">Hallo-app uitvoeren en controleer of de registratie is gelukt en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0042-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![De registratie van pushmeldingen in iOS-apps testen][33]
2. <span data-ttu-id="c0042-205">U kunt een pushmelding verzenden vanuit Hallo [Azure Portal], zoals hierboven beschreven.</span><span class="sxs-lookup"><span data-stu-id="c0042-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="c0042-206">Als u de code voor het verzenden van pushmeldingen in Hallo-app hebt toegevoegd, touch binnen Hallo tekst veld tooenter een melding.</span><span class="sxs-lookup"><span data-stu-id="c0042-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="c0042-207">Druk op Hallo **verzenden** knop op Hallo toetsenbord of Hallo **melding verzenden** knop in Hallo weergave toosend Hallo-melding.</span><span class="sxs-lookup"><span data-stu-id="c0042-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![Het verzenden van pushmeldingen in iOS-apps testen][34]
3. <span data-ttu-id="c0042-209">Hallo pushmelding wordt verzonden tooall-apparaten die geregistreerd tooreceive Hallo meldingen van de zijn specifieke Notification Hub Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0042-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![Het ontvangen van pushmeldingen in iOS-apps testen][35]

## <a name="next-steps"></a><span data-ttu-id="c0042-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c0042-211">Next steps</span></span>
<span data-ttu-id="c0042-212">In dit eenvoudige voorbeeld hebt u uitgezonden push notifications tooall uw geregistreerde iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="c0042-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="c0042-213">We raden een volgende stap in uw learning dat u verder gaan toohello [Azure Notification Hubs gebruikers waarschuwen voor iOS met .NET back-end] zelfstudie, dat u helpt bij het maken van een back-end toosend push meldingen met tags.</span><span class="sxs-lookup"><span data-stu-id="c0042-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="c0042-214">Als u uw gebruikers op belangengroepen toosegment wilt, kunt u verder gaan toohello [Notification Hubs gebruiken toosend belangrijk nieuws] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c0042-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="c0042-215">Zie [Richtlijnen voor Notification Hubs] voor algemene informatie over Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="c0042-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

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
[iOS SDK Mobile Services versie 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs gebruikers waarschuwen voor iOS met .NET back-end]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[Notification Hubs gebruiken toosend belangrijk nieuws]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure Portal]: https://portal.azure.com
