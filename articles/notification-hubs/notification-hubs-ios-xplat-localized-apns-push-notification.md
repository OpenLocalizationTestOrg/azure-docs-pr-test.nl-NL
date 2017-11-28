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
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a><span data-ttu-id="e26ff-103">Notification Hubs toosend gelokaliseerd belangrijk nieuws tooiOS apparaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="e26ff-103">Use Notification Hubs toosend localized breaking news tooiOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e26ff-104">Windows Store in C#</span><span class="sxs-lookup"><span data-stu-id="e26ff-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="e26ff-105">iOS</span><span class="sxs-lookup"><span data-stu-id="e26ff-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e26ff-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e26ff-106">Overview</span></span>
<span data-ttu-id="e26ff-107">Dit onderwerp leest u hoe toouse hello [sjablonen](notification-hubs-templates-cross-platform-push-messages.md) functie van Azure Notification Hubs toobroadcast nieuws meldingen gelokaliseerde taal en het apparaat op te splitsen.</span><span class="sxs-lookup"><span data-stu-id="e26ff-107">This topic shows you how toouse hello [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="e26ff-108">In deze zelfstudie begint u met Hallo iOS-app gemaakt in [Notification Hubs gebruiken toosend belangrijk nieuws].</span><span class="sxs-lookup"><span data-stu-id="e26ff-108">In this tutorial you start with hello iOS app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="e26ff-109">Wanneer voltooid, dat kunt u zich kunt tooregister voor u geïnteresseerd bent in categorieën, een taal opgeven in welke tooreceive Hallo-berichten en pushmeldingen voor Hallo geselecteerd categorieën in die taal ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e26ff-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="e26ff-110">Er zijn twee onderdelen toothis scenario:</span><span class="sxs-lookup"><span data-stu-id="e26ff-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="e26ff-111">iOS-app kan client apparaten toospecify een taal en toosubscribe toodifferent nieuwscategorieën; splitsen</span><span class="sxs-lookup"><span data-stu-id="e26ff-111">iOS app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="e26ff-112">Hallo back-end zendt Hallo meldingen, met behulp van Hallo **tag** en **sjabloon** funcites van Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e26ff-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e26ff-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e26ff-113">Prerequisites</span></span>
<span data-ttu-id="e26ff-114">U moet al hebt voltooid Hallo [Notification Hubs gebruiken toosend belangrijk nieuws] zelfstudie en Hallo code beschikbaar is, hebben omdat deze zelfstudie is gebaseerd rechtstreeks op die code.</span><span class="sxs-lookup"><span data-stu-id="e26ff-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="e26ff-115">Visual Studio 2012 of later is optioneel.</span><span class="sxs-lookup"><span data-stu-id="e26ff-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="e26ff-116">Sjabloon-concepten</span><span class="sxs-lookup"><span data-stu-id="e26ff-116">Template concepts</span></span>
<span data-ttu-id="e26ff-117">In [Notification Hubs gebruiken toosend belangrijk nieuws] u een app die gebruikt gebouwd **labels** toosubscribe toonotifications voor verschillende nieuwscategorieën.</span><span class="sxs-lookup"><span data-stu-id="e26ff-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="e26ff-118">Veel apps echter meerdere markten zijn gericht en lokalisatie vereisen.</span><span class="sxs-lookup"><span data-stu-id="e26ff-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="e26ff-119">Dit betekent dat Hallo inhoud van het Hallo-meldingen zelf toobe gelokaliseerd en geleverde toohello corrigeren set apparaten.</span><span class="sxs-lookup"><span data-stu-id="e26ff-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="e26ff-120">In dit onderwerp we tonen hoe toouse hello **sjabloon** functie van Notification Hubs tooeasily leveren belangrijk nieuws meldingen gelokaliseerd.</span><span class="sxs-lookup"><span data-stu-id="e26ff-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="e26ff-121">Opmerking: eenrichtingssessie toosend gelokaliseerd meldingen toocreate meerdere versies van elke tag is.</span><span class="sxs-lookup"><span data-stu-id="e26ff-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="e26ff-122">Bijvoorbeeld: toosupport Engels, Frans en Mandarijn, zou moeten we drie verschillende tags voor wereldnieuws: 'world_en', 'world_fr' en 'world_ch'.</span><span class="sxs-lookup"><span data-stu-id="e26ff-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="e26ff-123">We hebben toosend een gelokaliseerde versie van Hallo wereld nieuws tooeach van deze labels.</span><span class="sxs-lookup"><span data-stu-id="e26ff-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="e26ff-124">In dit onderwerp gebruiken we sjablonen tooavoid Hallo verspreiding van tags en Hallo vereiste van meerdere berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="e26ff-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="e26ff-125">Op een hoog niveau sjablonen zijn een manier toospecify hoe een specifiek apparaat een melding moet ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e26ff-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="e26ff-126">indeling van de exacte nettolading Hallo geeft Hallo sjabloon door te verwijzen tooproperties die deel van het Hallo-bericht verzonden door back-end van uw app uitmaken.</span><span class="sxs-lookup"><span data-stu-id="e26ff-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="e26ff-127">In ons geval ontvangt van ons een landinstelling networkdirect-bericht met alle ondersteunde talen:</span><span class="sxs-lookup"><span data-stu-id="e26ff-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="e26ff-128">Vervolgens we zorgt ervoor dat apparaten registreren met een sjabloon die de juiste eigenschap toohello verwijst.</span><span class="sxs-lookup"><span data-stu-id="e26ff-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="e26ff-129">Een iOS-app die wil tooregister voor Franse nieuws wordt bijvoorbeeld Hallo volgende registreren:</span><span class="sxs-lookup"><span data-stu-id="e26ff-129">For instance,  an iOS app that wants tooregister for French news will register hello following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="e26ff-130">Sjablonen zijn een zeer krachtige functie voor meer informatie over in onze [sjablonen](notification-hubs-templates-cross-platform-push-messages.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="e26ff-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="hello-app-user-interface"></a><span data-ttu-id="e26ff-131">Hallo-app-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="e26ff-131">hello app user interface</span></span>
<span data-ttu-id="e26ff-132">We zullen nu Hallo nieuws op te splitsen app die u hebt gemaakt in Hallo onderwerp wijzigen [Notification Hubs gebruiken toosend belangrijk nieuws] toosend gelokaliseerd belangrijk nieuws met behulp van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e26ff-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="e26ff-133">Voeg een gesegmenteerde besturingselement met Hallo drie talen die wordt ondersteund in uw MainStoryboard_iPhone.storyboard: Engels, Frans en Mandarijn.</span><span class="sxs-lookup"><span data-stu-id="e26ff-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with hello three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="e26ff-134">Breng ervoor tooadd een IBOutlet in uw ViewController.h zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e26ff-134">Then make sure tooadd an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-hello-ios-app"></a><span data-ttu-id="e26ff-135">Hallo iOS-app bouwen</span><span class="sxs-lookup"><span data-stu-id="e26ff-135">Building hello iOS app</span></span>
1. <span data-ttu-id="e26ff-136">Voeg in uw Notification.h hello *retrieveLocale* methode, en wijzig Hallo store en abonneren methoden, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e26ff-136">In your Notification.h add hello *retrieveLocale* method, and modify hello store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="e26ff-137">Wijzig in uw Notification.m hello *storeCategoriesAndSubscribe* methode door Hallo landinstelling-parameter toe te voegen en het opslaan in de standaardinstellingen voor Hallo gebruiker:</span><span class="sxs-lookup"><span data-stu-id="e26ff-137">In your Notification.m, modify hello *storeCategoriesAndSubscribe* method, by adding hello locale parameter and storing it in hello user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="e26ff-138">Wijzig vervolgens Hallo *abonneren* methode tooinclude Hallo landinstellingen:</span><span class="sxs-lookup"><span data-stu-id="e26ff-138">Then modify hello *subscribe* method tooinclude hello locale:</span></span>
   
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
   
    <span data-ttu-id="e26ff-139">Houd er rekening mee hoe we nu gebruiken Hallo methode *registerTemplateWithDeviceToken*, in plaats van *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="e26ff-139">Note how we are now using hello method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="e26ff-140">Wanneer er zich voor een sjabloon registreert hebben we tooprovide Hallo json-sjabloon en ook een naam voor de sjabloon hello (als de app tooregister verschillende sjablonen wilt mogelijk).</span><span class="sxs-lookup"><span data-stu-id="e26ff-140">When we register for a template we have tooprovide hello json template and also a name for hello template (as our app might want tooregister different templates).</span></span> <span data-ttu-id="e26ff-141">Zorg ervoor dat tooregister uw categorieën als labels, zoals we toomake ervoor tooreceive hello notifciations voor deze nieuws willen.</span><span class="sxs-lookup"><span data-stu-id="e26ff-141">Make sure tooregister your categories as tags, as we want toomake sure tooreceive hello notifciations for those news.</span></span>
   
    <span data-ttu-id="e26ff-142">Een methode tooretrieve Hallo landinstelling van standaardinstellingen voor Hallo gebruiker toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e26ff-142">Add a method tooretrieve hello locale from hello user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="e26ff-143">Nu dat we onze klasse meldingen hebt gewijzigd, hebben we toomake ervoor dat onze ViewController maakt gebruik van Hallo nieuwe UISegmentControl.</span><span class="sxs-lookup"><span data-stu-id="e26ff-143">Now that we modified our Notifications class, we have toomake sure that our ViewController makes use of hello new UISegmentControl.</span></span> <span data-ttu-id="e26ff-144">Toevoegen van de volgende regel in Hallo Hallo *viewDidLoad* methode toomake ervoor tooshow Hallo landinstellingen die momenteel is geselecteerd:</span><span class="sxs-lookup"><span data-stu-id="e26ff-144">Add hello following line in hello *viewDidLoad* method toomake sure tooshow hello locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="e26ff-145">Klik op uw *abonneren* methode, wijzigt de aanroep toohello *storeCategoriesAndSubscribe* toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="e26ff-145">Then, in your *subscribe* method, change your call toohello *storeCategoriesAndSubscribe* toohello following:</span></span>
   
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
3. <span data-ttu-id="e26ff-146">Ten slotte het hebben van tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* methode in uw AppDelegate.m, zodat u uw inschrijving correct vernieuwen kunt wanneer uw app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="e26ff-146">Finally, you have tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="e26ff-147">Wijzigen van de aanroep toohello *abonneren* methode van meldingen door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="e26ff-147">Change your call toohello *subscribe* method of notifications with hello following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="e26ff-148">(optioneel) Gelokaliseerde Sjabloonmeldingen verzenden vanuit .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="e26ff-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a><span data-ttu-id="e26ff-149">(optioneel) Gelokaliseerde Sjabloonmeldingen verzenden vanuit Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="e26ff-149">(optional) Send localized template notifications from hello device</span></span>
<span data-ttu-id="e26ff-150">Als u geen toegang tooVisual Studio hebt of wilt toojust test verzenden van meldingen voor gelokaliseerde Hallo-sjabloon rechtstreeks vanuit de app Hallo op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="e26ff-150">If you don't have access tooVisual Studio, or want toojust test sending hello localized template notifications directly from hello app on hello device.</span></span>  <span data-ttu-id="e26ff-151">U kunt eenvoudig hello gelokaliseerd sjabloon parameters toohello toevoegen `SendNotificationRESTAPI` methode die u hebt gedefinieerd in de vorige zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="e26ff-151">You can simple add hello localized template parameters toohello `SendNotificationRESTAPI` method you defined in hello previous tutorial.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="e26ff-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e26ff-152">Next Steps</span></span>
<span data-ttu-id="e26ff-153">Zie voor meer informatie over het gebruik van sjablonen:</span><span class="sxs-lookup"><span data-stu-id="e26ff-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="e26ff-154">[Waarschuw gebruikers met Notification Hubs: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="e26ff-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="e26ff-155">[Waarschuw gebruikers met Notification Hubs: Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="e26ff-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

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
