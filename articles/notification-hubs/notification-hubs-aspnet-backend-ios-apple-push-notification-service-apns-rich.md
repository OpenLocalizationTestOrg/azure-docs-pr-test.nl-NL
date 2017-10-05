---
title: Azure Notification Hubs Rich Push
description: Informatie over het uitgebreide pushmeldingen verzendt naar een iOS-app van Azure. Codevoorbeelden geschreven in Objective-C en C#.
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
ms.openlocfilehash: 394efdc2dfaff0666bc23d8a448b0a00d414da99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="cb5ef-104">Azure Notification Hubs Rich Push</span><span class="sxs-lookup"><span data-stu-id="cb5ef-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="cb5ef-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="cb5ef-105">Overview</span></span>
<span data-ttu-id="cb5ef-106">Om gebruikers met instant uitgebreide inhoud, wilt een toepassing pushen naast tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-106">In order to engage users with instant rich contents, an application might want to push beyond plain text.</span></span> <span data-ttu-id="cb5ef-107">Deze meldingen promoveren gebruikersinteracties en aanwezig inhoud zoals URL's, geluiden en afbeeldingen/coupons.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="cb5ef-108">Deze zelfstudie bouwt voort op de [gebruikers waarschuwen](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) onderwerp en het verzenden van pushmeldingen die gebruikmaken van nettoladingen (bijvoorbeeld installatiekopie) wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-108">This tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how to send push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="cb5ef-109">Deze zelfstudie is compatibel met iOS 7 en 8.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="cb5ef-110">Op hoog niveau:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-110">At a high level:</span></span>

1. <span data-ttu-id="cb5ef-111">De app back-end:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-111">The app backend:</span></span>
   * <span data-ttu-id="cb5ef-112">De nettolading van de uitgebreide opgeslagen (in dit geval installatiekopie) in de back-end-database/lokale opslag</span><span class="sxs-lookup"><span data-stu-id="cb5ef-112">Stores the rich payload (in this case, image) in the backend database/local storage</span></span>
   * <span data-ttu-id="cb5ef-113">ID van deze uitgebreide melding verzendt naar het apparaat</span><span class="sxs-lookup"><span data-stu-id="cb5ef-113">Sends ID of this rich notification to the device</span></span>
2. <span data-ttu-id="cb5ef-114">De App op het apparaat:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-114">App on the device:</span></span>
   * <span data-ttu-id="cb5ef-115">Neemt contact op met de back-end aanvragen van de uitgebreide nettolading met de ID die wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="cb5ef-115">Contacts the backend requesting the rich payload with the ID it receives</span></span>
   * <span data-ttu-id="cb5ef-116">Meldingen voor gebruikers verzendt op het apparaat bij het ophalen van gegevens is voltooid en toont de nettolading van de zodra gebruikers Tik voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="cb5ef-116">Sends users notifications on the device when data retrieval is complete, and shows the payload immediately when users tap to learn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="cb5ef-117">WebAPI-Project</span><span class="sxs-lookup"><span data-stu-id="cb5ef-117">WebAPI Project</span></span>
1. <span data-ttu-id="cb5ef-118">Open in Visual Studio de **AppBackend** project dat u hebt gemaakt in de [gebruikers waarschuwen](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-118">In Visual Studio, open the **AppBackend** project that you created in the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="cb5ef-119">Verkrijgen van een installatiekopie die u wilt melden gebruikers met en plaatsen een **img** map in uw projectmap.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-119">Obtain an image you would like to notify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="cb5ef-120">Klik op **alle bestanden weergeven** in Solution Explorer met de rechtermuisknop op de map **opnemen In Project**.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-120">Click **Show All Files** in the Solution Explorer, and right-click the folder to **Include In Project**.</span></span>
4. <span data-ttu-id="cb5ef-121">Met de afbeelding is geselecteerd en de actie bouwen in het venster Eigenschappen te wijzigen **ingesloten bron**.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-121">With the image selected, change its Build Action in Properties window to **Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="cb5ef-122">In **Notifications.cs**, Voeg het volgende toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-122">In **Notifications.cs**, add the following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="cb5ef-123">Bijwerken van de gehele **meldingen** klasse met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-123">Update the whole **Notifications** class with the following code.</span></span> <span data-ttu-id="cb5ef-124">Zorg ervoor dat de tijdelijke aanduidingen vervangt door uw notification hub-referenties en de bestandsnaam van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-124">Be sure to replace the placeholders with your notification hub credentials and image file name.</span></span>
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message to display to users
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
                // Placeholders: replace with the connection string (with full access) for your notification hub and the hub name from the Azure Classics Portal
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
   > <span data-ttu-id="cb5ef-125">(optioneel) Raadpleeg [het insluiten van en toegang krijgen tot bronnen met behulp van Visual C#](http://support.microsoft.com/kb/319292) voor meer informatie over het toevoegen en projectresources verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-125">(optional) Refer to [How to embed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how to add and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="cb5ef-126">In **NotificationsController.cs**, definiëren **NotificationsController** met de volgende codefragmenten.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-126">In **NotificationsController.cs**, redefine **NotificationsController**  with the following snippets.</span></span> <span data-ttu-id="cb5ef-127">Hiermee verzendt een initiële melding voor de achtergrond uitgebreide id naar apparaat te kunnen aan de clientzijde voor het ophalen van afbeelding:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-127">This sends an initial silent rich notification id to device and allows client-side retrieval of image:</span></span>
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) to client
        public async Task<HttpResponseMessage> Post() {
            // Replace the placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification to apns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. <span data-ttu-id="cb5ef-128">Er wordt nu opnieuw deze app wordt een Azure-Website zodat deze toegankelijk is vanaf alle apparaten implementeren.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-128">Now we will re-deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="cb5ef-129">Klik met de rechtermuisknop op het project **AppBackend** en selecteer **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-129">Right-click on the **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="cb5ef-130">Selecteer de Azure-Website als uw doel publiceren.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="cb5ef-131">Meld u aan met uw Azure-account en selecteer een bestaande of nieuwe Website en noteer de **doel-URL** eigenschap in de **verbinding** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-131">Log in with your Azure account and select an existing or new Website, and make a note of the **destination URL** property in the **Connection** tab.</span></span> <span data-ttu-id="cb5ef-132">Naar deze URL wordt verderop in deze zelfstudie verwezen als uw *back-endeindpunt*.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-132">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="cb5ef-133">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-133">Click **Publish**.</span></span>

## <a name="modify-the-ios-project"></a><span data-ttu-id="cb5ef-134">Wijzigen van het iOS-project</span><span class="sxs-lookup"><span data-stu-id="cb5ef-134">Modify the iOS project</span></span>
<span data-ttu-id="cb5ef-135">Nu dat u hebt uw app back-end verzendt gewijzigd alleen de *id* van een melding, wijzigt u uw iOS-app voor het verwerken van die id en het uitgebreide bericht ophalen vanuit uw back-end.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-135">Now that you have modified your app backend to send just the *id* of a notification, you will change your iOS app to handle that id and retrieve the rich message from your backend.</span></span>

1. <span data-ttu-id="cb5ef-136">Open uw iOS-project en externe meldingen inschakelen door te gaan naar het doel van uw belangrijkste app in de **doelen** sectie.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-136">Open your iOS project, and enable remote notifications by going to your main app target in the **Targets** section.</span></span>
2. <span data-ttu-id="cb5ef-137">Klik op **mogelijkheden**, schakelt u **Achtergrondmodi**, en controleer de **Remote Notifications** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-137">Click on **Capabilities**, turn on **Background Modes**, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="cb5ef-138">Ga naar **Main.storyboard**, en zorg ervoor dat u hebt een View-Controller (zoals als Start weergavebesturing in deze zelfstudie) van [gebruiker inlichten](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-138">Go to **Main.storyboard**, and make sure you have a View Controller (refered to as Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="cb5ef-139">Toevoegen een **navigatie Controller** tot uw storyboard en besturingselement en sleep naar Start weergavebesturing zodat deze de **hoofdmap weergave** van navigatie.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-139">Add a **Navigation Controller** to your storyboard, and control-drag to Home View Controller to make it the **root view** of navigation.</span></span> <span data-ttu-id="cb5ef-140">Zorg ervoor dat de **initiële View-Controller Is** in kenmerken inspector voor alleen de navigatie-Controller wordt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-140">Make sure the **Is Initial View Controller** in Attributes inspector is selected for the Navigation Controller only.</span></span>
5. <span data-ttu-id="cb5ef-141">Voeg een **weergavebesturing** voor storyboard en toevoegen van een **Afbeeldingsweergave**.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-141">Add a **View Controller** to storyboard and add an **Image View**.</span></span> <span data-ttu-id="cb5ef-142">Dit is de pagina die gebruikers zien wanneer ze kiezen voor meer informatie door te klikken op de notifiication.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-142">This is the page users will see once they choose to learn more by clicking on the notifiication.</span></span> <span data-ttu-id="cb5ef-143">Een storyboard ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-143">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="cb5ef-144">Klik op de **start weergavebesturing** storyboard en zorg ervoor dat zij heeft **homeViewController** als de **aangepaste klasse** en **Storyboard ID**onder de identiteit inspector.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-144">Click on the **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under the Identity inspector.</span></span>
7. <span data-ttu-id="cb5ef-145">Doe hetzelfde voor weergavebesturing installatiekopie als **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-145">Do the same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="cb5ef-146">Vervolgens maakt u een nieuwe weergavebesturing klasse met de titel **imageViewController** voor het afhandelen van de gebruikersinterface die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-146">Then, create a new View Controller class titled **imageViewController** to handle the UI you just created.</span></span>
9. <span data-ttu-id="cb5ef-147">In **imageViewController.h**, Voeg het volgende toe aan de controller interface-declaraties.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-147">In **imageViewController.h**, add the following to the controller's interface declarations.</span></span> <span data-ttu-id="cb5ef-148">Zorg ervoor dat besturingselement en sleep vanuit de weergave van de installatiekopie storyboard naar deze eigenschappen om te koppelen van de twee:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-148">Make sure to control-drag from the storyboard image view to these properties to link the two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="cb5ef-149">In **imageViewController.m**, Voeg het volgende toe aan het einde van **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-149">In **imageViewController.m**, add the following at the end of **viewDidload**:</span></span>
    
        // Display the UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="cb5ef-150">In **AppDelegate.m**, importeert u de installatiekopie-domeincontroller die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-150">In **AppDelegate.m**, import the image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="cb5ef-151">Een sectie interface met de volgende declaratie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-151">Add an interface section with the following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect to Image View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="cb5ef-152">In **AppDelegate**, zorg ervoor dat uw app registreert voor de achtergrond meldingen in **toepassing: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-152">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="cb5ef-153">Subsitute in de volgende implementatie voor **toepassing: didRegisterForRemoteNotificationsWithDeviceToken** naar het storyboard UI wordt gewijzigd in aanmerking nemen:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-153">Subsitute in the following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** to take the storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at the root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="cb5ef-154">Vervolgens voegt u de volgende methoden om **AppDelegate.m** ophalen van de installatiekopie van uw eindpunt en een lokale melding verzendt wanneer ophalen voltooid is.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-154">Then, add the following methods to **AppDelegate.m** to retrieve the image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="cb5ef-155">Vervang de tijdelijke aanduiding door `{backend endpoint}` met uw back-end-eindpunt:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-155">Make sure to substitute the placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
                   // From NSData to UIImage
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
   
                       // "5" is arbitrary here to give you enough time to quit out of the app and receive push notifications
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
           // Add "else if" here to handle more types of rich content such as url, sound files, etc.
       }
3. <span data-ttu-id="cb5ef-156">De lokale melding hierboven verwerkt door het openen van de installatiekopie weergavebesturing in **AppDelegate.m** met de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="cb5ef-156">Handle the local notification above by opening up the image view controller in **AppDelegate.m** with the following methods:</span></span>
   
       // Helper: redirect users to image view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image to image view controller
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
           // Add "else if" here to handle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-the-application"></a><span data-ttu-id="cb5ef-157">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cb5ef-157">Run the Application</span></span>
1. <span data-ttu-id="cb5ef-158">Voer de app op een fysiek iOS-apparaat (push notifications niet in de simulator werkt) in XCode.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-158">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="cb5ef-159">Voer een gebruikersnaam en wachtwoord van dezelfde waarde voor verificatie en klik in de iOS-app UI **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-159">In the iOS app UI, enter a username and password of the same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="cb5ef-160">Klik op **push verzenden** en ziet u een waarschuwing in-app.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-160">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="cb5ef-161">Als u op klikt **meer**, u naar de installatiekopie die u wilt opnemen in uw back-end voor de app wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-161">If you click on **More**, you will be brought to the image you chose to include in your app backend.</span></span>
4. <span data-ttu-id="cb5ef-162">U kunt ook klikken op **push verzenden** en druk onmiddellijk op de knop Start van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-162">You can also click **Send push** and immediately press the home button of your device.</span></span> <span data-ttu-id="cb5ef-163">Het over enkele ogenblikken ontvangt u een push-melding.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-163">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="cb5ef-164">Als u erop tik of klik op meer, wordt u in uw app en de inhoud van de uitgebreide gebracht.</span><span class="sxs-lookup"><span data-stu-id="cb5ef-164">If you tap on it or click More, you will be brought to your app and the rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
