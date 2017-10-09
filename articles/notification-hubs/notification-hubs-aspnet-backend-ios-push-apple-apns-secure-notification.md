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
# <a name="azure-notification-hubs-secure-push"></a>Azure Notification Hubs beveiligde Push
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Overzicht
Push notification-ondersteuning in Microsoft Azure kunt u tooaccess een eenvoudig te gebruiken, meerdere platforms, uitgebreid pushinfrastructuur, die sterk vereenvoudigd Hallo-implementatie van pushmeldingen voor consumenten- en enterprise-toepassingen voor mobiele telefoons -platforms.

Vanwege beperkingen voor tooregulatory of beveiliging kunt soms een toepassing tooinclude iets in Hallo-bericht dat via Hallo standaard push notification-infrastructuur kan niet worden verzonden. Deze zelfstudie wordt beschreven hoe tooachieve dezelfde ervaring Hallo door te sturen van gevoelige gegevens via een veilige en geverifieerde verbinding tussen clientapparaat Hallo en back-end Hallo app.

Op een hoog niveau is Hallo-stroom als volgt uit:

1. Hallo back-end van app:
   * Winkels beveiligde nettolading in back-enddatabase.
   * Hallo-ID van deze melding toohello apparaat (geen beveiligde gegevens verzonden) verzendt.
2. Hallo-app op Hallo apparaat tijdens het Hallo-bericht ontvangen:
   * Hallo-apparaat neemt contact Hallo back-end aanvragende Hallo beveiligde nettolading.
   * Hallo-app kunt Hallo nettolading weergeven als een melding op Hallo-apparaat.

Het is belangrijk dat in de voorgaande stroom Hallo (en in deze zelfstudie), gaan we ervan uit dat apparaat Hallo toonote slaat geen verificatietoken in lokale opslag nadat Hallo gebruiker zich aanmeldt. Dit garandeert een volledig naadloze ervaring als apparaat Hallo Hallo melding van beveiligde nettolading met dit token kan ophalen. Als uw toepassing slaat geen verificatietokens op Hallo-apparaat, of als deze tokens kunnen verlopen, hello apparaattoepassing bij Hallo melding moet worden weergegeven een algemene melding Hallo gebruiker toolaunch Hallo app te vragen. Hallo-app vervolgens verifieert de gebruiker Hallo en toont de nettolading van de Hallo-meldingen.

Deze Secure Push-zelfstudie laat zien hoe een push-melding toosend veilig. Hallo-zelfstudie bouwt voort op Hallo [gebruikers waarschuwen](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) zelfstudie, dus u moet eerst de voltooit Hallo stappen in deze zelfstudie.

> [!NOTE]
> Deze zelfstudie wordt ervan uitgegaan dat u hebt gemaakt en uw notification hub geconfigureerd zoals beschreven in [aan de slag met Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a>Hallo iOS-project wijzigen
Nu dat u uw app back-end toosend alleen Hallo gewijzigd *id* van een melding hebt toochange uw iOS-app toohandle melding en terugbellen secure uw back-end tooretrieve Hallo bericht toobe weergegeven.

tooachieve deze doelstelling krijgen we toowrite Hallo logica tooretrieve Hallo beveiligde inhoud van back-end app Hallo hebben.

1. In **AppDelegate.m**, ervoor Hallo app registers voor stille meldingen maken zodat Hallo melding id verzonden vanuit Hallo back-end worden verwerkt. Hallo toevoegen **UIRemoteNotificationTypeNewsstandContentAvailability** optie in didFinishLaunchingWithOptions:
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. In uw **AppDelegate.m** een Implementatiesectie toevoegen boven Hallo Hello declaratie te volgen:
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. Voeg in Hallo implementatie sectie Hallo code de volgende, waarbij Hallo tijdelijke aanduiding vervangt `{back-end endpoint}` met Hallo-eindpunt voor uw back-end eerder hebt verkregen:

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

1. Nu we hebben toohandle Hallo binnenkomende melding en Hallo methode hierboven tooretrieve Hallo inhoud toodisplay gebruiken. Eerst, hebben we tooenable uw iOS-app toorun op Hallo achtergrond tijdens het ontvangen van een pushmelding. In **XCode**, selecteert u uw app-project in het linkerdeelvenster Hallo en klik op het doel van uw belangrijkste app in Hallo **doelen** sectie uit Hallo centrale deelvenster.
2. Klik vervolgens op uw **mogelijkheden** tabblad Hallo boven aan uw centrale deelvenster en controleer Hallo **Remote Notifications** selectievakje.
   
    ![][IOS1]
3. In **AppDelegate.m** Hallo na methode toohandle pushmeldingen toevoegen:
   
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
   
    Houd er rekening mee dat het is beter toohandle Hallo gevallen van eigenschap van de header ontbreekt verificatie of afwijzing door Hallo back-end. Hallo specifieke verwerking van deze gevallen afhankelijk zijn van voornamelijk op de doel-gebruikerservaring. Een mogelijkheid is toodisplay een melding met een algemene Hallo tooauthenticate tooretrieve Hallo werkelijke gebruikersmelding wordt gevraagd.

## <a name="run-hello-application"></a>Hallo toepassing uitvoeren
toorun toepassing hello, Hallo te volgen:

1. Uitvoeren in XCode Hallo-app op een fysiek iOS-apparaat (push meldingen niet in de simulator Hallo werken).
2. Voer een gebruikersnaam en wachtwoord in Hallo iOS-app gebruikersinterface. Deze kunnen zich een willekeurige tekenreeks, maar ze moet dezelfde waarde Hallo.
3. Klik in Hallo iOS-app UI **aanmelden**. Klik vervolgens op **push verzenden**. Hier ziet u beveiligde Hallo-melding wordt weergegeven in het meldingencentrum.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
