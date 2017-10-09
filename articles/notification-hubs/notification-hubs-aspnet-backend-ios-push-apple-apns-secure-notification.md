---
title: Notification Hubs Secure Push aaaAzure
description: Meer informatie over hoe toosend beveiligde push-meldingen tooan iOS-app van Azure. Codevoorbeelden geschreven in Objective-C en C#.
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="788fc-104">Azure Notification Hubs beveiligde Push</span><span class="sxs-lookup"><span data-stu-id="788fc-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="788fc-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="788fc-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="788fc-106">iOS</span><span class="sxs-lookup"><span data-stu-id="788fc-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="788fc-107">Android</span><span class="sxs-lookup"><span data-stu-id="788fc-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="788fc-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="788fc-108">Overview</span></span>
<span data-ttu-id="788fc-109">Push notification-ondersteuning in Microsoft Azure kunt u tooaccess een eenvoudig te gebruiken, meerdere platforms, uitgebreid pushinfrastructuur, die sterk vereenvoudigd Hallo-implementatie van pushmeldingen voor consumenten- en enterprise-toepassingen voor mobiele telefoons -platforms.</span><span class="sxs-lookup"><span data-stu-id="788fc-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="788fc-110">Vanwege beperkingen voor tooregulatory of beveiliging kunt soms een toepassing tooinclude iets in Hallo-bericht dat via Hallo standaard push notification-infrastructuur kan niet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="788fc-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="788fc-111">Deze zelfstudie wordt beschreven hoe tooachieve dezelfde ervaring Hallo door te sturen van gevoelige gegevens via een veilige en geverifieerde verbinding tussen clientapparaat Hallo en back-end Hallo app.</span><span class="sxs-lookup"><span data-stu-id="788fc-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="788fc-112">Op een hoog niveau is Hallo-stroom als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="788fc-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="788fc-113">Hallo back-end van app:</span><span class="sxs-lookup"><span data-stu-id="788fc-113">hello app back-end:</span></span>
   * <span data-ttu-id="788fc-114">Winkels beveiligde nettolading in back-enddatabase.</span><span class="sxs-lookup"><span data-stu-id="788fc-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="788fc-115">Hallo-ID van deze melding toohello apparaat (geen beveiligde gegevens verzonden) verzendt.</span><span class="sxs-lookup"><span data-stu-id="788fc-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="788fc-116">Hallo-app op Hallo apparaat tijdens het Hallo-bericht ontvangen:</span><span class="sxs-lookup"><span data-stu-id="788fc-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="788fc-117">Hallo-apparaat neemt contact Hallo back-end aanvragende Hallo beveiligde nettolading.</span><span class="sxs-lookup"><span data-stu-id="788fc-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="788fc-118">Hallo-app kunt Hallo nettolading weergeven als een melding op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="788fc-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="788fc-119">Het is belangrijk dat in de voorgaande stroom Hallo (en in deze zelfstudie), gaan we ervan uit dat apparaat Hallo toonote slaat geen verificatietoken in lokale opslag nadat Hallo gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="788fc-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="788fc-120">Dit garandeert een volledig naadloze ervaring als apparaat Hallo Hallo melding van beveiligde nettolading met dit token kan ophalen.</span><span class="sxs-lookup"><span data-stu-id="788fc-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="788fc-121">Als uw toepassing slaat geen verificatietokens op Hallo-apparaat, of als deze tokens kunnen verlopen, hello apparaattoepassing bij Hallo melding moet worden weergegeven een algemene melding Hallo gebruiker toolaunch Hallo app te vragen.</span><span class="sxs-lookup"><span data-stu-id="788fc-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="788fc-122">Hallo-app vervolgens verifieert de gebruiker Hallo en toont de nettolading van de Hallo-meldingen.</span><span class="sxs-lookup"><span data-stu-id="788fc-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="788fc-123">Deze Secure Push-zelfstudie laat zien hoe een push-melding toosend veilig.</span><span class="sxs-lookup"><span data-stu-id="788fc-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="788fc-124">Hallo-zelfstudie bouwt voort op Hallo [gebruikers waarschuwen](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) zelfstudie, dus u moet eerst de voltooit Hallo stappen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="788fc-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="788fc-125">Deze zelfstudie wordt ervan uitgegaan dat u hebt gemaakt en uw notification hub geconfigureerd zoals beschreven in [aan de slag met Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="788fc-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a><span data-ttu-id="788fc-126">Hallo iOS-project wijzigen</span><span class="sxs-lookup"><span data-stu-id="788fc-126">Modify hello iOS project</span></span>
<span data-ttu-id="788fc-127">Nu dat u uw app back-end toosend alleen Hallo gewijzigd *id* van een melding hebt toochange uw iOS-app toohandle melding en terugbellen secure uw back-end tooretrieve Hallo bericht toobe weergegeven.</span><span class="sxs-lookup"><span data-stu-id="788fc-127">Now that you modified your app back-end toosend just hello *id* of a notification, you have toochange your iOS app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>

<span data-ttu-id="788fc-128">tooachieve deze doelstelling krijgen we toowrite Hallo logica tooretrieve Hallo beveiligde inhoud van back-end app Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="788fc-128">tooachieve this goal, we have toowrite hello logic tooretrieve hello secure content from hello app back-end.</span></span>

1. <span data-ttu-id="788fc-129">In **AppDelegate.m**, ervoor Hallo app registers voor stille meldingen maken zodat Hallo melding id verzonden vanuit Hallo back-end worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="788fc-129">In **AppDelegate.m**, make sure hello app registers for silent notifications so it processes hello notification id sent from hello backend.</span></span> <span data-ttu-id="788fc-130">Hallo toevoegen **UIRemoteNotificationTypeNewsstandContentAvailability** optie in didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="788fc-130">Add hello **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="788fc-131">In uw **AppDelegate.m** een Implementatiesectie toevoegen boven Hallo Hello declaratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="788fc-131">In your **AppDelegate.m** add an implementation section at hello top with hello following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="788fc-132">Voeg in Hallo implementatie sectie Hallo code de volgende, waarbij Hallo tijdelijke aanduiding vervangt `{back-end endpoint}` met Hallo-eindpunt voor uw back-end eerder hebt verkregen:</span><span class="sxs-lookup"><span data-stu-id="788fc-132">Then add in hello implementation section hello following code, substituting hello placeholder `{back-end endpoint}` with hello endpoint for your back-end obtained previously:</span></span>

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. <span data-ttu-id="788fc-133">Nu we hebben toohandle Hallo binnenkomende melding en Hallo methode hierboven tooretrieve Hallo inhoud toodisplay gebruiken.</span><span class="sxs-lookup"><span data-stu-id="788fc-133">Now we have toohandle hello incoming notification and use hello method above tooretrieve hello content toodisplay.</span></span> <span data-ttu-id="788fc-134">Eerst, hebben we tooenable uw iOS-app toorun op Hallo achtergrond tijdens het ontvangen van een pushmelding.</span><span class="sxs-lookup"><span data-stu-id="788fc-134">First, we have tooenable your iOS app toorun in hello background when receiving a push notification.</span></span> <span data-ttu-id="788fc-135">In **XCode**, selecteert u uw app-project in het linkerdeelvenster Hallo en klik op het doel van uw belangrijkste app in Hallo **doelen** sectie uit Hallo centrale deelvenster.</span><span class="sxs-lookup"><span data-stu-id="788fc-135">In **XCode**, select your app project on hello left panel, then click your main app target in hello **Targets** section from hello central pane.</span></span>
2. <span data-ttu-id="788fc-136">Klik vervolgens op uw **mogelijkheden** tabblad Hallo boven aan uw centrale deelvenster en controleer Hallo **Remote Notifications** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="788fc-136">Then click your **Capabilities** tab at hello top of your central pane, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="788fc-137">In **AppDelegate.m** Hallo na methode toohandle pushmeldingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="788fc-137">In **AppDelegate.m** add hello following method toohandle push notifications:</span></span>
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    <span data-ttu-id="788fc-138">Houd er rekening mee dat het is beter toohandle Hallo gevallen van eigenschap van de header ontbreekt verificatie of afwijzing door Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="788fc-138">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="788fc-139">Hallo specifieke verwerking van deze gevallen afhankelijk zijn van voornamelijk op de doel-gebruikerservaring.</span><span class="sxs-lookup"><span data-stu-id="788fc-139">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="788fc-140">Een mogelijkheid is toodisplay een melding met een algemene Hallo tooauthenticate tooretrieve Hallo werkelijke gebruikersmelding wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="788fc-140">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="788fc-141">Hallo toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="788fc-141">Run hello Application</span></span>
<span data-ttu-id="788fc-142">toorun toepassing hello, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="788fc-142">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="788fc-143">Uitvoeren in XCode Hallo-app op een fysiek iOS-apparaat (push meldingen niet in de simulator Hallo werken).</span><span class="sxs-lookup"><span data-stu-id="788fc-143">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="788fc-144">Voer een gebruikersnaam en wachtwoord in Hallo iOS-app gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="788fc-144">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="788fc-145">Deze kunnen zich een willekeurige tekenreeks, maar ze moet dezelfde waarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="788fc-145">These can be any string, but they must be hello same value.</span></span>
3. <span data-ttu-id="788fc-146">Klik in Hallo iOS-app UI **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="788fc-146">In hello iOS app UI, click **Log in**.</span></span> <span data-ttu-id="788fc-147">Klik vervolgens op **push verzenden**.</span><span class="sxs-lookup"><span data-stu-id="788fc-147">Then click **Send push**.</span></span> <span data-ttu-id="788fc-148">Hier ziet u beveiligde Hallo-melding wordt weergegeven in het meldingencentrum.</span><span class="sxs-lookup"><span data-stu-id="788fc-148">You should see hello secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
