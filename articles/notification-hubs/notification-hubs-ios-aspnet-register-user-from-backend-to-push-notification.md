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
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="1fe59-103">De huidige gebruiker Hallo voor pushmeldingen registreren met behulp van ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1fe59-103">Register hello current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fe59-104">iOS</span><span class="sxs-lookup"><span data-stu-id="1fe59-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="1fe59-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1fe59-105">Overview</span></span>
<span data-ttu-id="1fe59-106">Dit onderwerp leest u hoe toorequest registratie voor pushmeldingen met Azure Notification Hubs wanneer de registratie wordt uitgevoerd door ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="1fe59-106">This topic shows you how toorequest push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="1fe59-107">In dit onderwerp breidt Hallo zelfstudie [meldingen verzenden naar gebruikers met Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1fe59-107">This topic extends hello tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="1fe59-108">U moet Hallo vereiste stappen in deze zelfstudie toocreate Hallo geverifieerde mobiele service al hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="1fe59-108">You must have already completed hello required steps in that tutorial toocreate hello authenticated mobile service.</span></span> <span data-ttu-id="1fe59-109">Zie voor meer informatie over het Hallo melden gebruikers scenario, [meldingen verzenden naar gebruikers met Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1fe59-109">For more information on hello notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="1fe59-110">Uw app bijwerken</span><span class="sxs-lookup"><span data-stu-id="1fe59-110">Update your app</span></span>
1. <span data-ttu-id="1fe59-111">In uw MainStoryboard_iPhone.storyboard toevoegen Hallo onderdelen van de objectbibliotheek hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="1fe59-111">In your MainStoryboard_iPhone.storyboard, add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="1fe59-112">**Label**: "Push tooUser met Notification Hubs"</span><span class="sxs-lookup"><span data-stu-id="1fe59-112">**Label**: "Push tooUser with Notification Hubs"</span></span>
   * <span data-ttu-id="1fe59-113">**Label**: 'Omwille van'</span><span class="sxs-lookup"><span data-stu-id="1fe59-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="1fe59-114">**Label**: 'Gebruiker'</span><span class="sxs-lookup"><span data-stu-id="1fe59-114">**Label**: "User"</span></span>
   * <span data-ttu-id="1fe59-115">**Tekstveld**: 'Gebruiker'</span><span class="sxs-lookup"><span data-stu-id="1fe59-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="1fe59-116">**Label**: 'Password'</span><span class="sxs-lookup"><span data-stu-id="1fe59-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="1fe59-117">**Tekstveld**: 'Password'</span><span class="sxs-lookup"><span data-stu-id="1fe59-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="1fe59-118">**Knop**: 'Aanmelding'</span><span class="sxs-lookup"><span data-stu-id="1fe59-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="1fe59-119">Een storyboard ziet op dit moment uit Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="1fe59-119">At this point, your storyboard looks like hello following:</span></span>
     
      ![][0]
2. <span data-ttu-id="1fe59-120">In Hallo assistent editor aansluitingen voor alle Hallo overgeschakeld besturingselementen maken en ze aanroept, Hallo tekstvelden verbinden met Hallo View-Controller (gemachtigde) en maken een **actie** voor Hallo **aanmelding** knop.</span><span class="sxs-lookup"><span data-stu-id="1fe59-120">In hello assistant editor, create outlets for all hello switched controls and call them, connect hello text fields with hello View Controller (delegate), and create an **Action** for hello **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="1fe59-121">Maak een klasse met de naam **DeviceInfo**, en kopiëren Hallo code in Hallo interface sectie van het Hallo-bestand DeviceInfo.h te volgen:</span><span class="sxs-lookup"><span data-stu-id="1fe59-121">Create a class named **DeviceInfo**, and copy hello following code into hello interface section of hello file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="1fe59-122">Hallo na de code in de Implementatiesectie Hallo van Hallo DeviceInfo.m bestand kopiëren:</span><span class="sxs-lookup"><span data-stu-id="1fe59-122">Copy hello following code in hello implementation section of hello DeviceInfo.m file:</span></span>
   
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
5. <span data-ttu-id="1fe59-123">Voeg in PushToUserAppDelegate.h, Hallo eigenschap singleton te volgen:</span><span class="sxs-lookup"><span data-stu-id="1fe59-123">In PushToUserAppDelegate.h, add hello following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="1fe59-124">In Hallo **didFinishLaunchingWithOptions** methode in PushToUserAppDelegate.m, Hallo na code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1fe59-124">In hello **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add hello following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="1fe59-125">de eerste regel Hallo initialiseert Hallo **DeviceInfo** singleton.</span><span class="sxs-lookup"><span data-stu-id="1fe59-125">hello first line initializes hello **DeviceInfo** singleton.</span></span> <span data-ttu-id="1fe59-126">Hallo tweede regel begint Hallo registratie voor pushmeldingen, die al aanwezig is Hallo al is voltooid [aan de slag met Notification Hubs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1fe59-126">hello second line starts hello registration for push notifications, which is already present is you have already completed hello [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="1fe59-127">In PushToUserAppDelegate.m, Hallo methode implementeren **didRegisterForRemoteNotificationsWithDeviceToken** in uw AppDelegate en Hallo volgende code toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="1fe59-127">In PushToUserAppDelegate.m, implement hello method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add hello following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="1fe59-128">Hiermee stelt u Hallo apparaattoken voor Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="1fe59-128">This sets hello device token for hello request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1fe59-129">Op dit moment moet niet er een andere code in deze methode.</span><span class="sxs-lookup"><span data-stu-id="1fe59-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="1fe59-130">Als u al een aanroep van toohello **registerNativeWithDeviceToken** methode die is toegevoegd wanneer u Hallo voltooid [aan de slag met Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) zelfstudie, moet u commentarieer of verwijderen die aanroepen.</span><span class="sxs-lookup"><span data-stu-id="1fe59-130">If you already have a call toohello **registerNativeWithDeviceToken** method that was added when you completed hello [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="1fe59-131">Toevoegen in Hallo PushToUserAppDelegate.m bestand Hallo handler-methode te volgen:</span><span class="sxs-lookup"><span data-stu-id="1fe59-131">In hello PushToUserAppDelegate.m file, add hello following handler method:</span></span>
   
   * <span data-ttu-id="1fe59-132">(leeg) toepassing:(UIApplication *) toepassing didReceiveRemoteNotification:(NSDictionary *) gebruikersgegevens {NSLog (@"% @", gebruikersgegevens);   UIAlertView * waarschuwing = [[UIAlertView toewijzingseenheid] initWithTitle:@"Notification' bericht: [gebruikersgegevens objectForKey:@"inAppMessage]' gemachtigde: nil cancelButtonTitle: @ 'OK' otherButtonTitles:nil, nil];   [waarschuwing weergeven]; }</span><span class="sxs-lookup"><span data-stu-id="1fe59-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="1fe59-133">Deze methode wordt een waarschuwing weergegeven in de gebruikersinterface Hallo wanneer uw app meldingen ontvangt terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1fe59-133">This method displays an alert in hello UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="1fe59-134">Hallo PushToUserViewController.m bestands- en return Hallo toetsenbord openen in Hallo na implementatie:</span><span class="sxs-lookup"><span data-stu-id="1fe59-134">Open hello PushToUserViewController.m file, and return hello keyboard in hello following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="1fe59-135">In Hallo **viewDidLoad** methode in Hallo PushToUserViewController.m bestand initialiseren Hallo omwille van label als volgt:</span><span class="sxs-lookup"><span data-stu-id="1fe59-135">In hello **viewDidLoad** method in hello PushToUserViewController.m file, initialize hello installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="1fe59-136">Hallo volgende eigenschappen in de interface in PushToUserViewController.m toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1fe59-136">Add hello following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="1fe59-137">Vervolgens voegt u Hallo na implementatie:</span><span class="sxs-lookup"><span data-stu-id="1fe59-137">Then, add hello following implementation:</span></span>
    
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
13. <span data-ttu-id="1fe59-138">Kopiëren Hallo volgende code in Hallo **aanmelding** gemaakt door XCode handler-methode:</span><span class="sxs-lookup"><span data-stu-id="1fe59-138">Copy hello following code into hello **login** handler method created by XCode:</span></span>
    
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
    
    <span data-ttu-id="1fe59-139">Deze methode opgehaald van een installatie-ID en de kanaal voor pushmeldingen en verzendt, samen met het type apparaat hello, toohello geverifieerd Web API-methode die een registratie in Notification Hubs maakt.</span><span class="sxs-lookup"><span data-stu-id="1fe59-139">This method gets both an installation ID and channel for push notifications and sends it, along with hello device type, toohello authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="1fe59-140">Deze Web-API is gedefinieerd in [meldingen verzenden naar gebruikers met Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1fe59-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="1fe59-141">Nu dat hello client-app is bijgewerkt, retourneren toohello [meldingen verzenden naar gebruikers met Notification Hubs] en Hallo mobiele service toosend meldingen bijwerken met behulp van Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="1fe59-141">Now that hello client app has been updated, return toohello [Notify users with Notification Hubs] and update hello mobile service toosend notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[meldingen verzenden naar gebruikers met Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet

[aan de slag met Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-ios
