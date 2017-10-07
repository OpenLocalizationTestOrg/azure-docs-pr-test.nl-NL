---
title: Notification Hubs Rich Push aaaAzure
description: Meer informatie over hoe toosend rich push-meldingen tooan iOS-app van Azure. Codevoorbeelden geschreven in Objective-C en C#.
documentationcenter: ios
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: 590304df-c0a4-46c5-8ef5-6a6486bb3340
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5432d8bf47777371bea3521a0c0176ade75fbd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-rich-push"></a>Azure Notification Hubs Rich Push
## <a name="overview"></a>Overzicht
In volgorde tooengage gebruikers met instant uitgebreide inhoud eventueel een toepassing toopush afgezien van tekst zonder opmaak. Deze meldingen promoveren gebruikersinteracties en aanwezig inhoud zoals URL's, geluiden en afbeeldingen/coupons. Deze zelfstudie bouwt voort op Hallo [gebruikers waarschuwen](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) onderwerp en ziet u hoe toosend pushmeldingen die gebruikmaken van nettoladingen (bijvoorbeeld afbeelding).

Deze zelfstudie is compatibel met iOS 7 en 8.

  ![][IOS1]

Op hoog niveau:

1. Hallo back-end app:
   * Winkels Hallo uitgebreide nettolading (in dit geval installatiekopie) in Hallo back-end-database/lokale opslag
   * ID van dit uitgebreide melding toohello apparaat verzendt
2. De App op Hallo apparaat:
   * Contactpersonen Hallo back-end Hallo uitgebreide nettolading met Hallo-ID ontvangen aanvragen
   * Meldingen voor gebruikers verzendt op Hallo apparaat bij het ophalen van gegevens is voltooid en toont Hallo nettolading zodra gebruikers tikken op meer toolearn

## <a name="webapi-project"></a>WebAPI-Project
1. Open in Visual Studio Hallo **AppBackend** project dat u hebt gemaakt in Hallo [gebruikers waarschuwen](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) zelfstudie.
2. Verkrijgen van een installatiekopie die u wilt toonotify gebruikers met, en plaats deze in een **img** map in uw projectmap.
3. Klik op **alle bestanden weergeven** Hallo in Solution Explorer en te met de rechtermuisknop op de map Hallo**opnemen In Project**.
4. Hallo-afbeelding is geselecteerd en ook de actie bouwen in het venster Eigenschappen wijzigen**ingesloten bron**.
   
    ![][IOS2]
5. In **Notifications.cs**, voeg de volgende Hallo met de instructie:
   
        using System.Reflection;
6. Update Hallo hele **meldingen** klasse Hello code te volgen. Niet zeker tooreplace Hallo tijdelijke aanduidingen door uw notification hub-referenties en de bestandsnaam van de installatiekopie.
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message toodisplay toousers
            public string Message { get; set; }
            // Type of rich payload (developer-defined)
            public string RichType { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }
   
        public class Notifications {
            public static Notifications Instance = new Notifications();
   
            private List<Notification> notifications = new List<Notification>();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                // Placeholders: replace with hello connection string (with full access) for your notification hub and hello hub name from hello Azure Classics Portal
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",  "{hub name}");
            }
   
            public Notification CreateNotification(string message, string richType, string payload) {
                var notification = new Notification() {
                    Id = notifications.Count,
                    Message = message,
                    RichType = richType,
                    Payload = payload,
                    Read = false
                };
   
                notifications.Add(notification);
   
                return notification;
            }
   
            public Stream ReadImage(int id) {
                var assembly = Assembly.GetExecutingAssembly();
                // Placeholder: image file name (for example, logo.png).
                return assembly.GetManifestResourceStream("AppBackend.img.{logo.png}");
            }
        }
   
   > [!NOTE]
   > (optioneel) Raadpleeg te[hoe tooembed en toegang tot resources met behulp van Visual C#](http://support.microsoft.com/kb/319292) voor meer informatie over het tooadd en projectresources ophalen.
   > 
   > 
7. In **NotificationsController.cs**, definiëren **NotificationsController** Hello codefragmenten te volgen. Hiermee verzendt een initiële melding voor de achtergrond uitgebreide id toodevice te kunnen aan de clientzijde voor het ophalen van afbeelding:
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) tooclient
        public async Task<HttpResponseMessage> Post() {
            // Replace hello placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification tooapns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. Nu we deze app tooan Azure-Website in volgorde toomake opnieuw implementeren deze toegankelijk is vanaf alle apparaten. Met de rechtermuisknop op Hallo **AppBackend** project en selecteer **publiceren**.
9. Selecteer de Azure-Website als uw doel publiceren. Meld u aan met uw Azure-account en selecteer een bestaande of nieuwe Website en noteer Hallo **doel-URL** eigenschap in Hallo **verbinding** tabblad. Toothis URL als wordt verwezen uw *back-end-eindpunt* verderop in deze zelfstudie. Klik op **Publish**.

## <a name="modify-hello-ios-project"></a>Hallo iOS-project wijzigen
Nu dat u hebt uw app back-end toosend alleen Hallo gewijzigd *id* van een melding die id van uw iOS-app toohandle gewijzigd en ophalen van uitgebreide het Hallo-bericht van uw back-end.

1. Open uw iOS-project en inschakelen van externe meldingen door te gaan tooyour belangrijkste doel app in Hallo **doelen** sectie.
2. Klik op **mogelijkheden**, schakelt u **Achtergrondmodi**, en controleer Hallo **Remote Notifications** selectievakje.
   
    ![][IOS3]
3. Ga te**Main.storyboard**, en zorg ervoor dat u hebt een View-Controller (zoals tooas start weergavebesturing in deze zelfstudie) van [gebruiker inlichten](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) zelfstudie.
4. Voeg een **navigatie Controller** tooyour storyboard en besturingselement en sleep tooHome weergavebesturing toomake het Hallo **hoofdmap weergave** van navigatie. Zorg ervoor dat Hallo **initiële View-Controller Is** in kenmerken inspector is geselecteerd voor alleen Hallo navigatie-Controller.
5. Voeg een **weergavebesturing** toostoryboard en voeg een **Afbeeldingsweergave**. Dit is Hallo pagina gebruikers zien wanneer ze toolearn meer door te klikken op Hallo notifiication kiezen. Een storyboard ziet er als volgt:
   
    ![][IOS4]
6. Klik op Hallo **start weergavebesturing** storyboard en zorg ervoor dat zij heeft **homeViewController** als de **aangepaste klasse** en **Storyboard ID**onder Hallo identiteit inspector.
7. Dezelfde hello voor weergavebesturing installatiekopie als **imageViewController**.
8. Vervolgens maakt u een nieuwe weergavebesturing klasse met de titel **imageViewController** toohandle Hallo gebruikersinterface die u zojuist hebt gemaakt.
9. In **imageViewController.h**, Hallo na toohello-controller interface declaraties toevoegen. Zorg ervoor dat toocontrol en sleep van Hallo storyboard installatiekopie weergave toothese eigenschappen toolink Hallo twee:
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. In **imageViewController.m**, Hallo volgende toevoegen aan Hallo einde van **viewDidload**:
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. In **AppDelegate.m**, importeren Hallo installatiekopie-domeincontroller die u hebt gemaakt:
    
        #import "imageViewController.h"
12. Een sectie interface Hello declaratie volgende toevoegen:
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. In **AppDelegate**, zorg ervoor dat uw app registreert voor de achtergrond meldingen in **toepassing: didFinishLaunchingWithOptions**:
    
        // Software version
        self.iOS8 = [[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)] && [[UIApplication sharedApplication] respondsToSelector:@selector(registerForRemoteNotifications)];
    
        // Register for remote notifications for iOS8 and previous versions
        if (self.iOS8) {
            NSLog(@"This device is running with iOS8.");
    
            // Action
            UIMutableUserNotificationAction *richPushAction = [[UIMutableUserNotificationAction alloc] init];
            richPushAction.identifier = @"richPushMore";
            richPushAction.activationMode = UIUserNotificationActivationModeForeground;
            richPushAction.authenticationRequired = NO;
            richPushAction.title = @"More";
    
            // Notification category
            UIMutableUserNotificationCategory* richPushCategory = [[UIMutableUserNotificationCategory alloc] init];
            richPushCategory.identifier = @"richPush";
            [richPushCategory setActions:@[richPushAction] forContext:UIUserNotificationActionContextDefault];
    
            // Notification categories
            NSSet* richPushCategories = [NSSet setWithObjects:richPushCategory, nil];

            UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                    UIUserNotificationTypeAlert |
                                                    UIUserNotificationTypeBadge
                                                                                     categories:richPushCategories];

            [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
            [[UIApplication sharedApplication] registerForRemoteNotifications];

        }
        else {
            // Previous iOS versions
            NSLog(@"This device is running with iOS7 or earlier versions.");

            [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
        }

        return YES;

1. Subsitute in Hallo na implementatie voor **toepassing: didRegisterForRemoteNotificationsWithDeviceToken** tootake Hallo storyboard UI in account verandert:
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. Vervolgens voegt u Hallo volgende methoden te**AppDelegate.m** tooretrieve Hallo van de installatiekopie van uw eindpunt en een lokale melding verzenden wanneer ophalen is voltooid. Zorg ervoor dat toosubstitute Hallo-tijdelijke aanduiding `{backend endpoint}` met uw back-end-eindpunt:
   
       NSString *const GetNotificationEndpoint = @"{backend endpoint}/api/notifications";
   
       // Helper: retrieve notification content from backend with rich notification id
       - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion {
           UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
           homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
           NSString* authenticationHeader = hvc.registerClient.authenticationHeader;
           // Check if authenticated
           if (!authenticationHeader) return;
   
           NSURLSession* session = [NSURLSession
                                    sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                    delegate:nil
                                    delegateQueue:nil];
   
           NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, richId]];
           NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
           [request setHTTPMethod:@"GET"];
           NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
           [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
   
           NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
   
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
               if (!error && httpResponse.statusCode == 200) {
                   // From NSData tooUIImage
                   self.imagePayload = [UIImage imageWithData:data];
   
                   completion(nil);
               }
               else {
                   NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                   if (error)
                       completion(error);
                   else {
                       completion([NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                   }
               }
           }];
           [dataTask resume];
       }
   
       // Handle silent push notifications when id is sent from backend
       - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler {
           self.userInfo = userInfo;
           int richId = [[self.userInfo objectForKey:@"richId"] intValue];
           NSString* richType = [self.userInfo objectForKey:@"richType"];
   
           // Retrieve image data
           if ([richType isEqualToString:@"img"]) {  
               [self retrieveRichImageWithId:richId completion:^(NSError* error) {
                   if (!error){
                       // Send local notification
                       UILocalNotification* localNotification = [[UILocalNotification alloc] init];
   
                       // "5" is arbitrary here toogive you enough time tooquit out of hello app and receive push notifications
                       localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:5];
                       localNotification.userInfo = self.userInfo;
                       localNotification.alertBody = [self.userInfo objectForKey:@"richMessage"];
                       localNotification.timeZone = [NSTimeZone defaultTimeZone];
   
                       // iOS8 categories
                       if (self.iOS8) {
                           localNotification.category = @"richPush";
                       }
   
                       [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                       handler(UIBackgroundFetchResultNewData);
                   }
                   else{
                       handler(UIBackgroundFetchResultFailed);
                   }
               }];
           }
           // Add "else if" here toohandle more types of rich content such as url, sound files, etc.
       }
3. Hallo lokale melding hierboven verwerkt door het openen van Hallo installatiekopie weergavebesturing in **AppDelegate.m** Hello volgende methoden:
   
       // Helper: redirect users tooimage view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image tooimage view controller
           imgViewController.imagePayload = img;
   
           // Redirect
           [navigationController pushViewController:imgViewController animated:YES];
       }
   
       // Handle local notification sent above in didReceiveRemoteNotification
       - (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
           if (application.applicationState == UIApplicationStateActive) {
               // Show in-app alert with an extra "more" button
               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:notification.alertBody delegate:self cancelButtonTitle:@"OK" otherButtonTitles:@"More", nil];
   
               [alert show];
           }
           // App becomes active from user's tap on notification
           else {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
       }
   
       // Handle buttons in in-app alerts and redirect with data/image
       - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
           // Handle "more" button
           if (buttonIndex == 1)
           {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           // Add "else if" here toohandle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-hello-application"></a>Hallo toepassing uitvoeren
1. Uitvoeren in XCode Hallo-app op een fysiek iOS-apparaat (push meldingen niet in de simulator Hallo werken).
2. Voer een gebruikersnaam en wachtwoord Hallo dezelfde waarde voor verificatie en klikt u op in Hallo iOS-app UI **aanmelden**.
3. Klik op **push verzenden** en ziet u een waarschuwing in-app. Als u op klikt **meer**, kunt u zich gebracht toohello-installatiekopie die u hebt gekozen tooinclude in uw back-end voor de app.
4. U kunt ook klikken op **push verzenden** en druk onmiddellijk op Hallo thuis-knop van uw apparaat. Het over enkele ogenblikken ontvangt u een push-melding. Als u erop tik of klik op meer, moet u aan tooyour app en Hallo uitgebreide installatiekopie inhoud gebracht.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
