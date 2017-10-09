---
title: aaaNotification Hubs op te splitsen nieuws zelfstudie - iOS
description: Meer informatie over hoe toouse Azure Service Bus Notification Hubs toosend nieuws meldingen tooiOS apparaten op te splitsen.
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Gebruik Notification Hubs toosend belangrijk nieuws
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Overzicht
Dit onderwerp leest u hoe toouse Azure Notification Hubs toobroadcast belangrijk nieuws meldingen tooan iOS-app. Als u klaar gaat u kunnen tooregister voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen. Dit scenario is een algemene patroon voor veel apps waar meldingen hebt verzonden toobe toogroups van gebruikers die interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort eerder is gedeclareerd.

Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in Hallo notification hub. Wanneer meldingen worden verzonden tooa label, ontvangen alle apparaten die zijn geregistreerd voor de tag Hallo Hallo-bericht. Omdat tags gewoon tekenreeksen zijn, hebben geen toobe vooraf is ingericht. Raadpleeg te voor meer informatie over tags[Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Vereisten
In dit onderwerp is gebaseerd op Hallo-app die u hebt gemaakt in [aan de slag met Notification Hubs][get-started]. Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Categorie selectie toohello app toevoegen
de eerste stap Hallo is tooadd Hallo UI-elementen tooyour bestaande storyboard waarmee Hallo gebruiker tooselect categorieën tooregister. Hallo categorieën geselecteerd door een gebruiker zijn op Hallo apparaat opgeslagen. Wanneer Hallo-app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met Hallo geselecteerd categorieën gemaakt als labels.

1. Voeg in uw MainStoryboard_iPhone.storyboard Hallo volgende onderdelen uit de objectbibliotheek Hallo:
   
   * Een label met 'Op te splitsen nieuws'-tekst
   * Labels met Categorieteksten "Wereld", 'Politiek', 'Business', 'Technologie', 'Wetenschappelijke', 'Sport'
   * Zes switches, één per categorie instellen elke switch **status** toobe **uit** standaard.
   * Een knop met het label 'Abonneren'
     
     Een storyboard ziet er als volgt:
     
     ![][3]
2. In de editor voor Hallo-assistent aansluitingen voor alle Hallo switches maken en het aanroepen van 'WorldSwitch', 'PoliticsSwitch', 'BusinessSwitch', 'TechnologySwitch', 'ScienceSwitch', 'SportsSwitch'
3. Een actie voor de knop met de naam 'abonneren' maken. Uw ViewController.h moeten Hallo volgende bevatten:
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. Maak een nieuwe **Cocoa Touch klasse** aangeroepen `Notifications`. Kopieer Hallo code Hallo interface sectie van Hallo bestand Notifications.h te volgen:
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. Hallo importeren richtlijn tooNotifications.m volgende toevoegen:
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. Kopieer Hallo code in de Implementatiesectie Hallo van Hallo bestand Notifications.m te volgen.
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    Deze klasse maakt gebruik van lokale opslag toostore en ophalen van de categorieën Hallo van nieuws dat dit apparaat ontvangt. Het bevat ook, een tooregister methode voor deze categorieën met behulp van een [sjabloon](notification-hubs-templates-cross-platform-push-messages.md) registratie.

1. Toevoegen van een instructie importeren voor Notifications.h in Hallo AppDelegate.h bestand en een eigenschap voor een exemplaar van Hallo meldingen klasse toevoegen:
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. In Hallo **didFinishLaunchingWithOptions** methode in AppDelegate.m, Hallo code tooinitialize Hallo meldingen exemplaar aan begin van de methode Hallo Hallo toevoegen.  
   
    `HUBNAME`en `HUBLISTENACCESS` (gedefinieerd in hubinfo.h) moet al Hallo `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen vervangen door uw notification hub naam en het Hallo-verbindingsreeks voor *DefaultListenSharedAccessSignature*die u eerder hebt verkregen.
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u alleen Hallo-sleutel voor listen toegang distribueren met uw clientapp. Luisteren toegang kunnen die uw app tooregister voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden. Hallo volledige toegang tot de sleutel wordt gebruikt in een beveiligde back endservice voor het verzenden van meldingen en bestaande registraties wijzigen.
   > 
   > 
3. In Hallo **didRegisterForRemoteNotificationsWithDeviceToken** methode in AppDelegate.m, vervang Hallo-code in Hallo methode Hello toopass Hallo apparaat token toohello meldingen codeklasse te volgen. Hallo meldingen klasse voert Hallo registreren voor meldingen met Hallo categorieën. Als Hallo gebruiker categorieselecties wijzigt, noemen we Hallo `subscribeWithCategories` methode in antwoord toohello **abonneren** knop tooupdate ze.
   
   > [!NOTE]
   > Omdat het apparaattoken Hallo toegewezen door Hallo Apple Push Notification Service (APNS) kan op elk gewenst moment kans, moet u registreren voor meldingen vaak tooavoid melding fouten. In dit voorbeeld registreert voor melding telkens wanneer die Hallo-app wordt gestart. Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie toopreserve bandbreedte als minder dan een dag is verstreken sinds de vorige registratie Hallo.
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    Houd er rekening mee dat op dit moment er geen andere code in Hallo moet **didRegisterForRemoteNotificationsWithDeviceToken** methode.

1. Hallo volgende methoden moeten al aanwezig zijn in AppDelegate.m voltooid Hallo [aan de slag met Notification Hubs] [ get-started] zelfstudie.  Als dat niet het geval is, toe te voegen.
   
    -(leeg) MessageBox:(NSString *) Titel bericht:(NSString *) tekstbericht {
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * (leeg) toepassing:(UIApplication *) toepassing didReceiveRemoteNotification: (NSDictionary *) gebruikersgegevens {NSLog (@"% @", gebruikersgegevens);   [self MessageBox:@"Notification' bericht: [[gebruikersgegevens objectForKey:@"aps]' valueForKey:@"alert']]; }
   
   Deze methode meldingen ontvangen wanneer het Hallo-app wordt uitgevoerd door een eenvoudige weer te geven afhandelt **UIAlert**.
2. Voeg een importinstructie voor AppDelegate.h en kopieer Hallo na de code in Hallo in ViewController.m, XCode gegenereerde **abonneren** methode. Deze code wordt Hallo melding registratie toouse Hallo nieuwe categorie tags Hallo gebruiker ervoor in de gebruikersinterface Hallo gekozen heeft bijgewerkt.
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   Deze methode maakt u een **NSMutableArray** categorieën en maakt gebruik van Hallo **meldingen** klasse toostore Hallo lijst in Hallo lokale opslag en registers Hallo bijbehorende labels voor uw notification hub. Wanneer categorieën worden gewijzigd, wordt met de nieuwe categorieën Hallo Hallo registratie nagemaakt.
3. Voeg in ViewController.m, na de code in Hallo Hallo **viewDidLoad** methode tooset Hallo-gebruikersinterface op basis van categorieën Hallo eerder hebt opgeslagen.

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



Hallo-app kunt nu een set categorieën opslaan in Hallo apparaat gebruikt voor lokale opslag tooregister bij Hallo notification hub als Hallo-app wordt gestart.  Hallo-gebruiker kunt wijzigen Hallo selectie van categorieën tijdens runtime en klikt u op Hallo **abonneren** methode tooupdate Hallo registratie voor Hallo-apparaat. Vervolgens wordt u Hallo app toosend Hallo nieuws meldingen rechtstreeks in het Hallo-app zelf op te splitsen bijwerken.

## <a name="optional-sending-tagged-notifications"></a>(optioneel) Verzenden van meldingen met tags
Als u geen toegang tot tooVisual Studio hebt, kunt u de volgende sectie toohello overslaan en meldingen verzenden vanuit Hallo app zelf. U kunt ook Hallo juiste sjabloon melding verzenden vanuit Hallo [klassieke Azure-Portal] foutopsporingstabblad hello gebruiken voor uw notification hub. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a>(optioneel) Meldingen verzenden vanuit Hallo-apparaat
Normaal gesproken meldingen moeten worden verzonden door een back-endservice maar belangrijk nieuws om meldingen te verzenden rechtstreeks vanuit Hallo-app. toodo dit hello wordt bijgewerkt `SendNotificationRESTAPI` methode die is gedefinieerd in Hallo [aan de slag met Notification Hubs] [ get-started] zelfstudie.

1. In ViewController.m update Hallo `SendNotificationRESTAPI` methode als volgt zodat het accepteert de parameter voor Hallo categorie label en verzendt Hallo juiste [sjabloon](notification-hubs-templates-cross-platform-push-messages.md) melding.
   
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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
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
2. In ViewController.m update Hallo **melding verzenden** actie, zoals wordt weergegeven in het Hallo-code die volgt. Zodat het wordt elke tag afzonderlijk met Hallo-meldingen verzenden en toomultiple platforms verzenden.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. Bouw het project opnieuw op en controleer of er geen fouten in de build.

## <a name="run-hello-app-and-generate-notifications"></a>Hallo-app uitvoeren en meldingen genereren
1. Druk op Hallo knop toobuild Hallo project uitvoeren en Hallo-app te starten. Sommige belangrijk nieuws opties toosubscribe tooand selecteren en druk op Hallo **abonneren** knop. U ziet een dialoogvenster Hallo meldingen bent geabonneerd op waarmee wordt aangegeven.
   
    ![][1]
   
    Wanneer u de optie **abonneren**, Hallo app converteert Hallo geselecteerd categorieën in tags en vraagt een nieuwe apparaatregistratie voor Hallo geselecteerd tags van Hallo notification hub.
2. Voer een bericht toobe verstuurd als belangrijk nieuws druk Hallo **melding verzenden** knop. U kunt ook Hallo .NET-console-app toogenerate meldingen worden uitgevoerd.
   
    ![][2]
3. Elk apparaat geabonneerd toobreaking nieuws ontvangt Hallo belangrijk nieuws meldingen die hebben verzonden.

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toobroadcast belangrijk nieuws per categorie. Houd rekening met een van de volgende zelfstudies waarin andere geavanceerde scenario's voor Notification Hubs Markeer Hallo voltooien:

* **[Gebruik Notification Hubs toobroadcast gelokaliseerd belangrijk nieuws]**
  
    Meer informatie over hoe tooexpand Hallo nieuws app tooenable verzenden op te splitsen meldingen gelokaliseerd.

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Gebruik Notification Hubs toobroadcast gelokaliseerd belangrijk nieuws]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[klassieke Azure-Portal]: https://manage.windowsazure.com
