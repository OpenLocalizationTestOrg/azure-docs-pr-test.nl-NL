
<span data-ttu-id="2cba0-101">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="2cba0-101">**Objective-C**:</span></span>

1. <span data-ttu-id="2cba0-102">In **QSAppDelegate.m**, Hallo iOS SDK importeren en **QSTodoService.h**:</span><span class="sxs-lookup"><span data-stu-id="2cba0-102">In **QSAppDelegate.m**, import hello iOS SDK and **QSTodoService.h**:</span></span>
   
        #import <MicrosoftAzureMobile/MicrosoftAzureMobile.h>
        #import "QSTodoService.h"
2. <span data-ttu-id="2cba0-103">In `didFinishLaunchingWithOptions` in **QSAppDelegate.m**, insert Hallo volgende regels precies vóór `return YES;`:</span><span class="sxs-lookup"><span data-stu-id="2cba0-103">In `didFinishLaunchingWithOptions` in **QSAppDelegate.m**, insert hello following lines right before `return YES;`:</span></span>
   
        UIUserNotificationSettings* notificationSettings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeAlert | UIUserNotificationTypeBadge | UIUserNotificationTypeSound categories:nil];
        [[UIApplication sharedApplication] registerUserNotificationSettings:notificationSettings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
3. <span data-ttu-id="2cba0-104">In **QSAppDelegate.m**, Hallo volgende handler methoden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2cba0-104">In **QSAppDelegate.m**, add hello following handler methods.</span></span> <span data-ttu-id="2cba0-105">Uw app is nu bijgewerkte toosupport pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="2cba0-105">Your app is now updated toosupport push notifications.</span></span> 
   
        // Registration with APNs is successful
        - (void)application:(UIApplication *)application
        didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
   
            QSTodoService *todoService = [QSTodoService defaultService];
            MSClient *client = todoService.client;
   
            [client.push registerDeviceToken:deviceToken completion:^(NSError *error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
            }];
        }
   
        // Handle any failure tooregister
        - (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:
        (NSError *)error {
            NSLog(@"Failed tooregister for remote notifications: %@", error);
        }
   
        // Use userInfo in hello payload toodisplay an alert.
        - (void)application:(UIApplication *)application
              didReceiveRemoteNotification:(NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
   
            NSDictionary *apsPayload = userInfo[@"aps"];
            NSString *alertString = apsPayload[@"alert"];
   
            // Create alert with notification content.
            UIAlertController *alertController = [UIAlertController
                                          alertControllerWithTitle:@"Notification"
                                          message:alertString
                                          preferredStyle:UIAlertControllerStyleAlert];
   
            UIAlertAction *cancelAction = [UIAlertAction
                                           actionWithTitle:NSLocalizedString(@"Cancel", @"Cancel")
                                           style:UIAlertActionStyleCancel
                                           handler:^(UIAlertAction *action)
                                           {
                                               NSLog(@"Cancel");
                                           }];
   
            UIAlertAction *okAction = [UIAlertAction
                                       actionWithTitle:NSLocalizedString(@"OK", @"OK")
                                       style:UIAlertActionStyleDefault
                                       handler:^(UIAlertAction *action)
                                       {
                                           NSLog(@"OK");
                                       }];
   
            [alertController addAction:cancelAction];
            [alertController addAction:okAction];
   
            // Get current view controller.
            UIViewController *currentViewController = [[[[UIApplication sharedApplication] delegate] window] rootViewController];
            while (currentViewController.presentedViewController)
            {
                currentViewController = currentViewController.presentedViewController;
            }
   
            // Display alert.
            [currentViewController presentViewController:alertController animated:YES completion:nil];
   
        }

<span data-ttu-id="2cba0-106">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="2cba0-106">**Swift**:</span></span>

1. <span data-ttu-id="2cba0-107">Bestand toevoegen **ClientManager.swift** Hello inhoud te volgen.</span><span class="sxs-lookup"><span data-stu-id="2cba0-107">Add file **ClientManager.swift** with hello following contents.</span></span> <span data-ttu-id="2cba0-108">Vervang *App-URL %* met Hallo-URL van back-end van hello Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="2cba0-108">Replace *%AppUrl%* with hello URL of hello Azure Mobile App backend.</span></span>
   
        class ClientManager {
            static let sharedClient = MSClient(applicationURLString: "%AppUrl%")
        }
2. <span data-ttu-id="2cba0-109">In **ToDoTableViewController.swift**, vervang Hallo `let client` regel die initialiseert een `MSClient` met deze regel:</span><span class="sxs-lookup"><span data-stu-id="2cba0-109">In **ToDoTableViewController.swift**, replace hello `let client` line that initializes an `MSClient` with this line:</span></span>
   
        let client = ClientManager.sharedClient
3. <span data-ttu-id="2cba0-110">In **AppDelegate.swift**, vervangen van de tekst hello `func application` als volgt:</span><span class="sxs-lookup"><span data-stu-id="2cba0-110">In **AppDelegate.swift**, replace hello body of `func application` as follows:</span></span>
   
        func application(application: UIApplication,
          didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
           application.registerUserNotificationSettings(
               UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound],
                   categories: nil))
           application.registerForRemoteNotifications()
           return true
        }
4. <span data-ttu-id="2cba0-111">In **AppDelegate.swift**, Hallo volgende handler methoden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2cba0-111">In **AppDelegate.swift**, add hello following handler methods.</span></span> <span data-ttu-id="2cba0-112">Uw app is nu bijgewerkte toosupport pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="2cba0-112">Your app is now updated toosupport push notifications.</span></span>
   
        func application(application: UIApplication,
           didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
            ClientManager.sharedClient.push?.registerDeviceToken(deviceToken) { error in
                print("Error registering for notifications: ", error?.description)
            }
        }
   
        func application(application: UIApplication,
           didFailToRegisterForRemoteNotificationsWithError error: NSError) {
            print("Failed tooregister for remote notifications: ", error.description)
        }
   
        func application(application: UIApplication,
           didReceiveRemoteNotification userInfo: [NSObject: AnyObject]) {
   
            print(userInfo)
   
            let apsNotification = userInfo["aps"] as? NSDictionary
            let apsString       = apsNotification?["alert"] as? String
   
            let alert = UIAlertController(title: aaa"Alert", message: apsString, preferredStyle: .Alert)
            let okAction = UIAlertAction(title: aaa"OK", style: .Default) { _ in
                print("OK")
            }
            let cancelAction = UIAlertAction(title: aaa"Cancel", style: .Default) { _ in
                print("Cancel")
            }
   
            alert.addAction(okAction)
            alert.addAction(cancelAction)
   
            var currentViewController = self.window?.rootViewController
            while currentViewController?.presentedViewController != nil {
                currentViewController = currentViewController?.presentedViewController
            }
   
            currentViewController?.presentViewController(alert, animated: true) {}
   
        }

