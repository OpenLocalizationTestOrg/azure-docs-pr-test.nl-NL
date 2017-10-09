---
title: aaaRegister hello huidige gebruiker voor pushmeldingen met behulp van Web-API | Microsoft Docs
description: Meer informatie over hoe toorequest registratie voor pushmeldingen in een iOS-app met Azure Notification Hubs wanneer de registratie wordt uitgevoerd door ASP.NET Web API.
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a>De huidige gebruiker Hallo voor pushmeldingen registreren met behulp van ASP.NET
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a>Overzicht
Dit onderwerp leest u hoe toorequest registratie voor pushmeldingen met Azure Notification Hubs wanneer de registratie wordt uitgevoerd door ASP.NET Web API. In dit onderwerp breidt Hallo zelfstudie [meldingen verzenden naar gebruikers met Notification Hubs]. U moet Hallo vereiste stappen in deze zelfstudie toocreate Hallo geverifieerde mobiele service al hebt voltooid. Zie voor meer informatie over het Hallo melden gebruikers scenario, [meldingen verzenden naar gebruikers met Notification Hubs].

## <a name="update-your-app"></a>Uw app bijwerken
1. In uw MainStoryboard_iPhone.storyboard toevoegen Hallo onderdelen van de objectbibliotheek hello te volgen:
   
   * **Label**: "Push tooUser met Notification Hubs"
   * **Label**: 'Omwille van'
   * **Label**: 'Gebruiker'
   * **Tekstveld**: 'Gebruiker'
   * **Label**: 'Password'
   * **Tekstveld**: 'Password'
   * **Knop**: 'Aanmelding'
     
     Een storyboard ziet op dit moment uit Hallo volgende:
     
      ![][0]
2. In Hallo assistent editor aansluitingen voor alle Hallo overgeschakeld besturingselementen maken en ze aanroept, Hallo tekstvelden verbinden met Hallo View-Controller (gemachtigde) en maken een **actie** voor Hallo **aanmelding** knop.
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. Maak een klasse met de naam **DeviceInfo**, en kopiëren Hallo code in Hallo interface sectie van het Hallo-bestand DeviceInfo.h te volgen:
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. Hallo na de code in de Implementatiesectie Hallo van Hallo DeviceInfo.m bestand kopiëren:
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store hello install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. Voeg in PushToUserAppDelegate.h, Hallo eigenschap singleton te volgen:
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. In Hallo **didFinishLaunchingWithOptions** methode in PushToUserAppDelegate.m, Hallo na code toevoegen:
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    de eerste regel Hallo initialiseert Hallo **DeviceInfo** singleton. Hallo tweede regel begint Hallo registratie voor pushmeldingen, die al aanwezig is Hallo al is voltooid [aan de slag met Notification Hubs] zelfstudie.
7. In PushToUserAppDelegate.m, Hallo methode implementeren **didRegisterForRemoteNotificationsWithDeviceToken** in uw AppDelegate en Hallo volgende code toe te voegen:
   
        self.deviceInfo.deviceToken = deviceToken;
   
    Hiermee stelt u Hallo apparaattoken voor Hallo-aanvraag.
   
   > [!NOTE]
   > Op dit moment moet niet er een andere code in deze methode. Als u al een aanroep van toohello **registerNativeWithDeviceToken** methode die is toegevoegd wanneer u Hallo voltooid [aan de slag met Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) zelfstudie, moet u commentarieer of verwijderen die aanroepen.
   > 
   > 
8. Toevoegen in Hallo PushToUserAppDelegate.m bestand Hallo handler-methode te volgen:
   
   * (leeg) toepassing:(UIApplication *) toepassing didReceiveRemoteNotification:(NSDictionary *) gebruikersgegevens {NSLog (@"% @", gebruikersgegevens);   UIAlertView * waarschuwing = [[UIAlertView toewijzingseenheid] initWithTitle:@"Notification' bericht: [gebruikersgegevens objectForKey:@"inAppMessage]' gemachtigde: nil cancelButtonTitle: @ 'OK' otherButtonTitles:nil, nil];   [waarschuwing weergeven]; }
   
   Deze methode wordt een waarschuwing weergegeven in de gebruikersinterface Hallo wanneer uw app meldingen ontvangt terwijl deze wordt uitgevoerd.
9. Hallo PushToUserViewController.m bestands- en return Hallo toetsenbord openen in Hallo na implementatie:
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. In Hallo **viewDidLoad** methode in Hallo PushToUserViewController.m bestand initialiseren Hallo omwille van label als volgt:
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. Hallo volgende eigenschappen in de interface in PushToUserViewController.m toevoegen:
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. Vervolgens voegt u Hallo na implementatie:
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. Kopiëren Hallo volgende code in Hallo **aanmelding** gemaakt door XCode handler-methode:
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    Deze methode opgehaald van een installatie-ID en de kanaal voor pushmeldingen en verzendt, samen met het type apparaat hello, toohello geverifieerd Web API-methode die een registratie in Notification Hubs maakt. Deze Web-API is gedefinieerd in [meldingen verzenden naar gebruikers met Notification Hubs].

Nu dat hello client-app is bijgewerkt, retourneren toohello [meldingen verzenden naar gebruikers met Notification Hubs] en Hallo mobiele service toosend meldingen bijwerken met behulp van Notification Hubs.

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[meldingen verzenden naar gebruikers met Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet

[aan de slag met Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-ios
