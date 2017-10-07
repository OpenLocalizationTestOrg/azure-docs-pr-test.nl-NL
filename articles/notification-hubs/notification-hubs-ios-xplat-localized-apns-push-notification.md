---
title: aaaNotification Hubs gelokaliseerd op te splitsen nieuws-zelfstudie voor iOS
description: Meer informatie over hoe toouse Azure Service Bus Notification Hubs toosend gelokaliseerd voor belangrijk nieuws meldingen (iOS).
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a>Notification Hubs toosend gelokaliseerd belangrijk nieuws tooiOS apparaten gebruiken
> [!div class="op_single_selector"]
> * [Windows Store in C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Overzicht
Dit onderwerp leest u hoe toouse hello [sjablonen](notification-hubs-templates-cross-platform-push-messages.md) functie van Azure Notification Hubs toobroadcast nieuws meldingen gelokaliseerde taal en het apparaat op te splitsen. In deze zelfstudie begint u met Hallo iOS-app gemaakt in [Notification Hubs gebruiken toosend belangrijk nieuws]. Wanneer voltooid, dat kunt u zich kunt tooregister voor u geïnteresseerd bent in categorieën, een taal opgeven in welke tooreceive Hallo-berichten en pushmeldingen voor Hallo geselecteerd categorieën in die taal ontvangen.

Er zijn twee onderdelen toothis scenario:

* iOS-app kan client apparaten toospecify een taal en toosubscribe toodifferent nieuwscategorieën; splitsen
* Hallo back-end zendt Hallo meldingen, met behulp van Hallo **tag** en **sjabloon** funcites van Azure Notification Hubs.

## <a name="prerequisites"></a>Vereisten
U moet al hebt voltooid Hallo [Notification Hubs gebruiken toosend belangrijk nieuws] zelfstudie en Hallo code beschikbaar is, hebben omdat deze zelfstudie is gebaseerd rechtstreeks op die code.

Visual Studio 2012 of later is optioneel.

## <a name="template-concepts"></a>Sjabloon-concepten
In [Notification Hubs gebruiken toosend belangrijk nieuws] u een app die gebruikt gebouwd **labels** toosubscribe toonotifications voor verschillende nieuwscategorieën.
Veel apps echter meerdere markten zijn gericht en lokalisatie vereisen. Dit betekent dat Hallo inhoud van het Hallo-meldingen zelf toobe gelokaliseerd en geleverde toohello corrigeren set apparaten.
In dit onderwerp we tonen hoe toouse hello **sjabloon** functie van Notification Hubs tooeasily leveren belangrijk nieuws meldingen gelokaliseerd.

Opmerking: eenrichtingssessie toosend gelokaliseerd meldingen toocreate meerdere versies van elke tag is. Bijvoorbeeld: toosupport Engels, Frans en Mandarijn, zou moeten we drie verschillende tags voor wereldnieuws: 'world_en', 'world_fr' en 'world_ch'. We hebben toosend een gelokaliseerde versie van Hallo wereld nieuws tooeach van deze labels. In dit onderwerp gebruiken we sjablonen tooavoid Hallo verspreiding van tags en Hallo vereiste van meerdere berichten verzenden.

Op een hoog niveau sjablonen zijn een manier toospecify hoe een specifiek apparaat een melding moet ontvangen. indeling van de exacte nettolading Hallo geeft Hallo sjabloon door te verwijzen tooproperties die deel van het Hallo-bericht verzonden door back-end van uw app uitmaken. In ons geval ontvangt van ons een landinstelling networkdirect-bericht met alle ondersteunde talen:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Vervolgens we zorgt ervoor dat apparaten registreren met een sjabloon die de juiste eigenschap toohello verwijst. Een iOS-app die wil tooregister voor Franse nieuws wordt bijvoorbeeld Hallo volgende registreren:

    {
        aps:{
            alert: "$(News_French)"
        }
    }

Sjablonen zijn een zeer krachtige functie voor meer informatie over in onze [sjablonen](notification-hubs-templates-cross-platform-push-messages.md) artikel.

## <a name="hello-app-user-interface"></a>Hallo-app-gebruikersinterface
We zullen nu Hallo nieuws op te splitsen app die u hebt gemaakt in Hallo onderwerp wijzigen [Notification Hubs gebruiken toosend belangrijk nieuws] toosend gelokaliseerd belangrijk nieuws met behulp van sjablonen.

Voeg een gesegmenteerde besturingselement met Hallo drie talen die wordt ondersteund in uw MainStoryboard_iPhone.storyboard: Engels, Frans en Mandarijn.

![][13]

Breng ervoor tooadd een IBOutlet in uw ViewController.h zoals hieronder wordt weergegeven:

![][14]

## <a name="building-hello-ios-app"></a>Hallo iOS-app bouwen
1. Voeg in uw Notification.h hello *retrieveLocale* methode, en wijzig Hallo store en abonneren methoden, zoals hieronder wordt weergegeven:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    Wijzig in uw Notification.m hello *storeCategoriesAndSubscribe* methode door Hallo landinstelling-parameter toe te voegen en het opslaan in de standaardinstellingen voor Hallo gebruiker:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    Wijzig vervolgens Hallo *abonneren* methode tooinclude Hallo landinstellingen:
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    Houd er rekening mee hoe we nu gebruiken Hallo methode *registerTemplateWithDeviceToken*, in plaats van *registerNativeWithDeviceToken*. Wanneer er zich voor een sjabloon registreert hebben we tooprovide Hallo json-sjabloon en ook een naam voor de sjabloon hello (als de app tooregister verschillende sjablonen wilt mogelijk). Zorg ervoor dat tooregister uw categorieën als labels, zoals we toomake ervoor tooreceive hello notifciations voor deze nieuws willen.
   
    Een methode tooretrieve Hallo landinstelling van standaardinstellingen voor Hallo gebruiker toevoegen:
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. Nu dat we onze klasse meldingen hebt gewijzigd, hebben we toomake ervoor dat onze ViewController maakt gebruik van Hallo nieuwe UISegmentControl. Toevoegen van de volgende regel in Hallo Hallo *viewDidLoad* methode toomake ervoor tooshow Hallo landinstellingen die momenteel is geselecteerd:
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    Klik op uw *abonneren* methode, wijzigt de aanroep toohello *storeCategoriesAndSubscribe* toohello volgende:
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. Ten slotte het hebben van tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* methode in uw AppDelegate.m, zodat u uw inschrijving correct vernieuwen kunt wanneer uw app wordt gestart. Wijzigen van de aanroep toohello *abonneren* methode van meldingen door Hallo volgende:
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a>(optioneel) Gelokaliseerde Sjabloonmeldingen verzenden vanuit .NET-consoletoepassing.
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a>(optioneel) Gelokaliseerde Sjabloonmeldingen verzenden vanuit Hallo-apparaat
Als u geen toegang tooVisual Studio hebt of wilt toojust test verzenden van meldingen voor gelokaliseerde Hallo-sjabloon rechtstreeks vanuit de app Hallo op Hallo-apparaat.  U kunt eenvoudig hello gelokaliseerd sjabloon parameters toohello toevoegen `SendNotificationRESTAPI` methode die u hebt gedefinieerd in de vorige zelfstudie Hallo.

        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];

            NSString *json;

            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];

            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];

            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];

            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];

            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];

            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];

            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];

            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];

            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];

            [dataTask resume];
        }




## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het gebruik van sjablonen:

* [Waarschuw gebruikers met Notification Hubs: ASP.NET]
* [Waarschuw gebruikers met Notification Hubs: Mobile Services]

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs gebruiken toosend belangrijk nieuws]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Waarschuw gebruikers met Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Waarschuw gebruikers met Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
