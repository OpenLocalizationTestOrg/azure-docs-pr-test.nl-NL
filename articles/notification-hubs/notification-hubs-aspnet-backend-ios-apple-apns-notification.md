---
title: aaaAzure Notification Hubs gebruikers waarschuwen voor iOS met .NET back-end
description: Meer informatie over hoe toosend push-meldingen toousers in Azure. Codevoorbeelden geschreven in Objective-C en Hallo .NET API voor Hallo back-end.
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="2a220-104">Azure Notification Hubs - Een melding naar iOS-gebruikers verzenden met .NET back-end</span><span class="sxs-lookup"><span data-stu-id="2a220-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="2a220-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2a220-105">Overview</span></span>
<span data-ttu-id="2a220-106">Push notification-ondersteuning in Azure kunt u tooaccess een eenvoudig te gebruiken, multiplatform en uitgebreid pushinfrastructuur, die sterk vereenvoudigd Hallo-implementatie van pushmeldingen voor consumenten- en enterprise-toepassingen voor mobiele telefoons -platforms.</span><span class="sxs-lookup"><span data-stu-id="2a220-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="2a220-107">Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa specifieke app gebruiker op een specifiek apparaat.</span><span class="sxs-lookup"><span data-stu-id="2a220-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="2a220-108">Een ASP.NET WebAPI-back-end is gebruikte tooauthenticate clients en toogenerate meldingen, zoals in Hallo richtlijnen onderwerp [registreren van uw app back-end](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="2a220-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="2a220-109">Deze zelfstudie wordt ervan uitgegaan dat u hebt gemaakt en uw notification hub geconfigureerd zoals beschreven in [aan de slag met Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2a220-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="2a220-110">Deze zelfstudie is ook de vereiste toohello hello [(iOS) beveiligen Push](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2a220-110">This tutorial is also hello prerequisite toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="2a220-111">Als u toouse Mobile Apps als uw back-endservice wilt, raadpleegt u Hallo [Mobile Apps aan de slag met Pushmeldingen](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="2a220-111">If you want toouse Mobile Apps as your backend service, see hello [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="2a220-112">Uw iOS-app wijzigen</span><span class="sxs-lookup"><span data-stu-id="2a220-112">Modify your iOS app</span></span>
1. <span data-ttu-id="2a220-113">Open Hallo één pagina weergave app u hebt gemaakt in Hallo [aan de slag met Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2a220-113">Open hello Single Page view app you created in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2a220-114">In deze sectie gaan we ervan uit dat het project is geconfigureerd met een leeg organisatienaam.</span><span class="sxs-lookup"><span data-stu-id="2a220-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="2a220-115">Als dat niet het geval is, moet u tooprepend de namen van uw organisatie naam tooall klassen.</span><span class="sxs-lookup"><span data-stu-id="2a220-115">If not, you will need tooprepend your organization name tooall class names.</span></span>
   > 
   > 
2. <span data-ttu-id="2a220-116">In uw Main.storyboard toevoegen weergegeven in Hallo schermafbeelding hieronder in objectbibliotheek Hallo Hallo-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="2a220-116">In your Main.storyboard add hello components shown in hello screenshot below from hello object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="2a220-117">**Gebruikersnaam**: A UITextField met tijdelijke tekst *gebruikersnaam invoeren*, onmiddellijk onder Hallo verzendt resultaten label en beperkte toohello links en marges naar rechts en onder Hallo verzenden resultaten label.</span><span class="sxs-lookup"><span data-stu-id="2a220-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath hello send results label and constrained toohello left and right margins and beneath hello send results label.</span></span>
   * <span data-ttu-id="2a220-118">**Wachtwoord**: A UITextField met tijdelijke tekst *wachtwoord invoeren*, direct onderliggende hello gebruikersnaam tekstveld en beperkte toohello links en marges rechts en onder het tekstveld Hallo-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="2a220-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath hello username text field and constrained toohello left and right margins and beneath hello username text field.</span></span> <span data-ttu-id="2a220-119">Controleer Hallo **tekstinvoer Secure** onder de optie in Hallo kenmerk Inspector, *retourneren sleutel*.</span><span class="sxs-lookup"><span data-stu-id="2a220-119">Check hello **Secure Text Entry** option in hello Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="2a220-120">**Meld u bij**: A UIButton gelabeld onmiddellijk onder de wachtwoordveld tekst hello en schakelt u Hallo **ingeschakeld** onder de optie in Hallo kenmerken-Inspector *-inhoud*</span><span class="sxs-lookup"><span data-stu-id="2a220-120">**Log in**: A UIButton labeled immediately beneath hello password text field and uncheck hello **Enabled** option in hello Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="2a220-121">**WNS**: Label en het verzenden van switch tooenable Hallo melding Windows Notification Service als deze ingesteld op Hallo hub is.</span><span class="sxs-lookup"><span data-stu-id="2a220-121">**WNS**: Label and switch tooenable sending hello notification Windows Notification Service if it has been setup on hello hub.</span></span> <span data-ttu-id="2a220-122">Zie Hallo [Windows aan de slag](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2a220-122">See hello [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="2a220-123">**GCM**: Label en het verzenden van switch tooenable Hallo melding tooGoogle Cloud Messaging als deze ingesteld op Hallo hub is.</span><span class="sxs-lookup"><span data-stu-id="2a220-123">**GCM**: Label and switch tooenable sending hello notification tooGoogle Cloud Messaging if it has been setup on hello hub.</span></span> <span data-ttu-id="2a220-124">Zie [Android aan de slag](notification-hubs-android-push-notification-google-gcm-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2a220-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="2a220-125">**APNS**: Label en het verzenden van switch tooenable Hallo melding toohello Apple Platform Notification Service.</span><span class="sxs-lookup"><span data-stu-id="2a220-125">**APNS**: Label and switch tooenable sending hello notification toohello Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="2a220-126">**Recipent Username**: A UITextField met tijdelijke tekst *ontvanger gebruikersnaam tag*, onmiddellijk onder Hallo GCM labelen en beperkte toohello links en rechts marges en onder Hallo GCM labelen.</span><span class="sxs-lookup"><span data-stu-id="2a220-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath hello GCM label and constrained toohello left and right margins and beneath hello GCM label.</span></span>

    <span data-ttu-id="2a220-127">Sommige onderdelen zijn toegevoegd in Hallo [aan de slag met Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2a220-127">Some components were added in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="2a220-128">**CTRL** slepen vanuit het Hallo-onderdelen in Hallo weergave tooViewController.h en voeg deze nieuwe uitgangen.</span><span class="sxs-lookup"><span data-stu-id="2a220-128">**Ctrl** drag from hello components in hello view tooViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="2a220-129">Voeg de volgende Hallo in ViewController.h, `#define` onder uw importinstructies.</span><span class="sxs-lookup"><span data-stu-id="2a220-129">In ViewController.h, add hello following `#define` just below your import statements.</span></span> <span data-ttu-id="2a220-130">Vervang Hallo *< Voer uw back-end eindpunt\>*  aanduiding voor items met de doel-URL die u gebruikt toodeploy back-end van uw app in de vorige sectie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a220-130">Substitute hello *<Enter Your Backend Endpoint\>* placeholder with hello Destination URL you used toodeploy your app backend in hello previous section.</span></span> <span data-ttu-id="2a220-131">Bijvoorbeeld: *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="2a220-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="2a220-132">In het project, maak een nieuwe **klasse Raak Cocoa** met de naam **RegisterClient** toointerface Hello ASP.NET back-end-u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2a220-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** toointerface with hello ASP.NET back-end you created.</span></span> <span data-ttu-id="2a220-133">Maak Hallo klasse is overgenomen van `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="2a220-133">Create hello class inheriting from `NSObject`.</span></span> <span data-ttu-id="2a220-134">Voeg vervolgens Hallo code in Hallo RegisterClient.h te volgen.</span><span class="sxs-lookup"><span data-stu-id="2a220-134">Then add hello following code in hello RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="2a220-135">Werk in Hallo RegisterClient.m hello `@interface` sectie:</span><span class="sxs-lookup"><span data-stu-id="2a220-135">In hello RegisterClient.m update hello `@interface` section:</span></span>
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. <span data-ttu-id="2a220-136">Vervang Hallo `@implementation` sectie in Hallo RegisterClient.m Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="2a220-136">Replace hello `@implementation` section in hello RegisterClient.m with hello following code.</span></span>

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    <span data-ttu-id="2a220-137">Hallo bovenstaande code implementeert Hallo logica beschreven in artikel Hallo [registreren van uw app back-end](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) met NSURLSession tooperform REST roept tooyour app back-end en NSUserDefaults toolocally store Hallo registratie-id die wordt geretourneerd door Hallo notification hub.</span><span class="sxs-lookup"><span data-stu-id="2a220-137">hello code above implements hello logic explained in hello guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession tooperform REST calls tooyour app backend, and NSUserDefaults toolocally store hello registrationId returned by hello notification hub.</span></span>

    <span data-ttu-id="2a220-138">Opmerking dat deze klasse is vereist voor de eigenschap **authorizationHeader** toobe in volgorde toowork correct ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2a220-138">Note that this class requires its property **authorizationHeader** toobe set in order toowork properly.</span></span> <span data-ttu-id="2a220-139">Deze eigenschap is ingesteld door Hallo **ViewController** klasse nadat Hallo aanmelden.</span><span class="sxs-lookup"><span data-stu-id="2a220-139">This property is set by hello **ViewController** class after hello log in.</span></span>

1. <span data-ttu-id="2a220-140">Voeg in ViewController.h, een `#import` -instructie voor RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="2a220-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="2a220-141">Vervolgens een declaratie voor Hallo apparaattoken toevoegt en verwijzen naar tooa `RegisterClient` exemplaar in Hallo `@interface` sectie:</span><span class="sxs-lookup"><span data-stu-id="2a220-141">Then add a declaration for hello device token and reference tooa `RegisterClient` instance in hello `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="2a220-142">Voeg een persoonlijke methodedeclaratie in Hallo in ViewController.m, `@interface` sectie:</span><span class="sxs-lookup"><span data-stu-id="2a220-142">In ViewController.m, add a private method declaration in hello `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="2a220-143">Hallo volgende fragment is niet een beveiligde verificatieschema, vervang Hallo-implementatie van Hallo **createAndSetAuthenticationHeaderWithUsername:AndPassword:** met uw specifieke verificatiemechanisme een token toobe van verificatie wordt gebruikt door Hallo registreren client-klasse, zoals OAuth, Active Directory, die wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="2a220-143">hello following snippet is not a secure authentication scheme, you should substitute hello implementation of hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token toobe consumed by hello register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="2a220-144">Klik dan in Hallo `@implementation` sectie van ViewController.m Hallo na de code die wordt toegevoegd Hallo-implementatie voor de instelling Hallo apparaat token en de verificatie-header toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2a220-144">Then in hello `@implementation` section of ViewController.m add hello following code which adds hello implementation for setting hello device token and authentication header.</span></span>
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    <span data-ttu-id="2a220-145">Houd er rekening mee hoe instelling Hallo apparaattoken kunt Hallo knop aanmelden.</span><span class="sxs-lookup"><span data-stu-id="2a220-145">Note how setting hello device token enables hello log in button.</span></span> <span data-ttu-id="2a220-146">Dit is omdat als onderdeel van Hallo aanmelding actie Hallo weergavebesturing zich voor pushmeldingen met Hallo app back-end registreert.</span><span class="sxs-lookup"><span data-stu-id="2a220-146">This is becasue as a part of hello login action, hello view controller registers for push notifications with hello app backend.</span></span> <span data-ttu-id="2a220-147">Daarom wil we niet aanmelden actie toobe toegankelijk totdat het apparaattoken Hallo correct is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2a220-147">Hence, we do not want Log In action toobe accessible till hello device token has been properly set up.</span></span> <span data-ttu-id="2a220-148">Kan geval ontkoppelt u aanmelden van Hallo push registratie Hallo zolang Hallo voormalige voordat de laatste Hallo gebeurt.</span><span class="sxs-lookup"><span data-stu-id="2a220-148">You can decouple hello log in from hello push registration as long as hello former happens before hello latter.</span></span>
2. <span data-ttu-id="2a220-149">Gebruik in ViewController.m, Hallo volgende codefragmenten tooimplement Hallo actiemethode voor uw **aanmelden** knop en een methode toosend Hallo melding bericht met Hallo ASP.NET-back-end.</span><span class="sxs-lookup"><span data-stu-id="2a220-149">In ViewController.m, use hello following snippets tooimplement hello action method for your **Log In** button and a method toosend hello notification message using hello ASP.NET backend.</span></span>
   
       - <span data-ttu-id="2a220-150">(IBAction) LogInAction: (id) afzender {/ / verificatieheader en stel deze in het register client NSString * gebruikersnaam = zelf. UsernameField.text;   NSString * wachtwoord = zelf. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="2a220-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="2a220-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="2a220-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="2a220-152">__weak ViewController * selfie = eigen;   [self.registerClient registerWithDeviceToken:self.deviceToken tags: nil andCompletion:^(NSError* error) {Als (! fout) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success' message:@"Registered met succes! "];});}}];}</span><span class="sxs-lookup"><span data-stu-id="2a220-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="2a220-153">-SendNotificationASPNETBackend (leeg): (NSString*) pns UsernameTag: (NSString*) usernameTag bericht: (NSString*) bericht {NSURLSession* sessie = [NSURLSession sessionWithConfiguration: [NSURLSessionConfiguration defaultSessionConfiguration] gemachtigde: nil delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="2a220-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="2a220-154">Hallo pns- en gebruikersnaam tag doorgeven als parameters met Hallo REST-URL toohello ASP.NET-back-end NSURL * Aanvraagurl = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="2a220-154">// Pass hello pns and username tag as parameters with hello REST URL toohello ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="2a220-155">NSMutableURLRequest * aanvraag = [NSMutableURLRequest requestWithURL:requestURL];    [aanvragen setHTTPMethod:@"POST"];</span><span class="sxs-lookup"><span data-stu-id="2a220-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="2a220-156">Hallo mock authenticationheader ophalen van Hallo registreren client NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [aanvragen setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span><span class="sxs-lookup"><span data-stu-id="2a220-156">// Get hello mock authenticationheader from hello register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="2a220-157">Hoofdtekst van het Hallo-bericht melding toevoegen [setValue:@"application/json;charset=utf-8 aanvragen ' forHTTPHeaderField:@"Content-Type'];    [setHTTPBody aanvragen: [bericht dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="2a220-157">//Add hello notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="2a220-158">Hallo send notification REST-API niet uitvoeren op Hallo ASP.NET-back-end NSURLSessionDataTask * dataTask = [sessie dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *fout) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) antwoord;        Als (fout || httpResponse.statusCode! = 200) {NSString* status = [NSString stringWithFormat:@"Error Status voor % @: % d\nError: %@\n', pns, httpResponse.statusCode, fout];            dispatch_async(dispatch_get_main_queue(), ^ {/ / tekst toevoegen, omdat alle 3 PNS aanroepen ook informatie tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status wellicht]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="2a220-158">// Execute hello send notification REST API on hello ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information tooview                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="2a220-159">}];    [dataTask hervatten]; }</span><span class="sxs-lookup"><span data-stu-id="2a220-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="2a220-160">Hallo-actie voor Hallo bijwerken **melding verzenden** knop toouse Hallo ASP.NET back-end en tooany PNS ingeschakeld door een switch te verzenden.</span><span class="sxs-lookup"><span data-stu-id="2a220-160">Update hello action for hello **Send Notification** button toouse hello ASP.NET backend and send tooany PNS enabled by a switch.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. <span data-ttu-id="2a220-161">In de functie **ViewDidLoad**, het toevoegen van Hallo tooinstantiate hello RegisterClient exemplaar te volgen en Hallo gemachtigde voor de tekstvelden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2a220-161">In function **ViewDidLoad**, add hello following tooinstantiate hello RegisterClient instance and set hello delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="2a220-162">Nu in **AppDelegate.m**, verwijdert u alle Hallo inhoud van de methode Hallo **toepassing: didRegisterForPushNotificationWithDeviceToken:** en vervang deze door Hallo toomake zeker te volgen die Hallo weergeven controller bevat Hallo nieuwste apparaattoken opgehaald uit APNs:</span><span class="sxs-lookup"><span data-stu-id="2a220-162">Now in **AppDelegate.m**, remove all hello content of hello method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with hello following toomake sure that hello view controller contains hello latest device token retrieved from APNs:</span></span>
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="2a220-163">Ten slotte in **AppDelegate.m**, Controleer of er Hallo methode te volgen:</span><span class="sxs-lookup"><span data-stu-id="2a220-163">Finally in **AppDelegate.m**, make sure you have hello following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a><span data-ttu-id="2a220-164">Test Hallo toepassing</span><span class="sxs-lookup"><span data-stu-id="2a220-164">Test hello Application</span></span>
1. <span data-ttu-id="2a220-165">Uitvoeren in XCode Hallo-app op een fysiek iOS-apparaat (push meldingen niet in de simulator Hallo werken).</span><span class="sxs-lookup"><span data-stu-id="2a220-165">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="2a220-166">Voer een gebruikersnaam en wachtwoord in Hallo iOS-app gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="2a220-166">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="2a220-167">Dit kunnen een willekeurige tekenreeks, maar ze moeten beide Hallo dezelfde tekenreekswaarde.</span><span class="sxs-lookup"><span data-stu-id="2a220-167">These can be any string, but they must both be hello same string value.</span></span> <span data-ttu-id="2a220-168">Klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="2a220-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="2a220-169">U ziet een melding van de registratie geslaagd pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="2a220-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="2a220-170">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a220-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="2a220-171">In Hallo **ontvanger gebruikersnaam tag* tekst Voer Hallo naam gebruikerstag gebruikt met inschrijving Hallo vanaf een ander apparaat.</span><span class="sxs-lookup"><span data-stu-id="2a220-171">In hello **Recipient username tag* text field, enter hello user name tag used with hello registration from another device.</span></span>
5. <span data-ttu-id="2a220-172">Geef een bericht en klik op **melding verzenden**.</span><span class="sxs-lookup"><span data-stu-id="2a220-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="2a220-173">Alleen Hallo-apparaten waarvoor een registratie met Hallo geadresseerde gebruiker naamtag ontvangen melding het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="2a220-173">Only hello devices that have a registration with hello recipient user name tag receive hello notification message.</span></span>  <span data-ttu-id="2a220-174">Toothose gebruikers wordt alleen verzonden.</span><span class="sxs-lookup"><span data-stu-id="2a220-174">It is only sent toothose users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
