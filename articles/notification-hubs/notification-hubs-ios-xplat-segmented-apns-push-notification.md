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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="a9b8d-103">Gebruik Notification Hubs toosend belangrijk nieuws</span><span class="sxs-lookup"><span data-stu-id="a9b8d-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="a9b8d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a9b8d-104">Overview</span></span>
<span data-ttu-id="a9b8d-105">Dit onderwerp leest u hoe toouse Azure Notification Hubs toobroadcast belangrijk nieuws meldingen tooan iOS-app.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan iOS app.</span></span> <span data-ttu-id="a9b8d-106">Als u klaar gaat u kunnen tooregister voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="a9b8d-107">Dit scenario is een algemene patroon voor veel apps waar meldingen hebt verzonden toobe toogroups van gebruikers die interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort eerder is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="a9b8d-108">Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in Hallo notification hub.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="a9b8d-109">Wanneer meldingen worden verzonden tooa label, ontvangen alle apparaten die zijn geregistreerd voor de tag Hallo Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="a9b8d-110">Omdat tags gewoon tekenreeksen zijn, hebben geen toobe vooraf is ingericht.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="a9b8d-111">Raadpleeg te voor meer informatie over tags[Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="a9b8d-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9b8d-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a9b8d-112">Prerequisites</span></span>
<span data-ttu-id="a9b8d-113">In dit onderwerp is gebaseerd op Hallo-app die u hebt gemaakt in [aan de slag met Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="a9b8d-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="a9b8d-114">Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="a9b8d-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="a9b8d-115">Categorie selectie toohello app toevoegen</span><span class="sxs-lookup"><span data-stu-id="a9b8d-115">Add category selection toohello app</span></span>
<span data-ttu-id="a9b8d-116">de eerste stap Hallo is tooadd Hallo UI-elementen tooyour bestaande storyboard waarmee Hallo gebruiker tooselect categorieën tooregister.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-116">hello first step is tooadd hello UI elements tooyour existing storyboard that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="a9b8d-117">Hallo categorieën geselecteerd door een gebruiker zijn op Hallo apparaat opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="a9b8d-118">Wanneer Hallo-app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met Hallo geselecteerd categorieën gemaakt als labels.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="a9b8d-119">Voeg in uw MainStoryboard_iPhone.storyboard Hallo volgende onderdelen uit de objectbibliotheek Hallo:</span><span class="sxs-lookup"><span data-stu-id="a9b8d-119">In your MainStoryboard_iPhone.storyboard add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="a9b8d-120">Een label met 'Op te splitsen nieuws'-tekst</span><span class="sxs-lookup"><span data-stu-id="a9b8d-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="a9b8d-121">Labels met Categorieteksten "Wereld", 'Politiek', 'Business', 'Technologie', 'Wetenschappelijke', 'Sport'</span><span class="sxs-lookup"><span data-stu-id="a9b8d-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="a9b8d-122">Zes switches, één per categorie instellen elke switch **status** toobe **uit** standaard.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-122">Six switches, one per category, set each switch **State** toobe **Off** by default.</span></span>
   * <span data-ttu-id="a9b8d-123">Een knop met het label 'Abonneren'</span><span class="sxs-lookup"><span data-stu-id="a9b8d-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="a9b8d-124">Een storyboard ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="a9b8d-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="a9b8d-125">In de editor voor Hallo-assistent aansluitingen voor alle Hallo switches maken en het aanroepen van 'WorldSwitch', 'PoliticsSwitch', 'BusinessSwitch', 'TechnologySwitch', 'ScienceSwitch', 'SportsSwitch'</span><span class="sxs-lookup"><span data-stu-id="a9b8d-125">In hello assistant editor, create outlets for all hello switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="a9b8d-126">Een actie voor de knop met de naam 'abonneren' maken.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="a9b8d-127">Uw ViewController.h moeten Hallo volgende bevatten:</span><span class="sxs-lookup"><span data-stu-id="a9b8d-127">Your ViewController.h should contain hello following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="a9b8d-128">Maak een nieuwe **Cocoa Touch klasse** aangeroepen `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="a9b8d-129">Kopieer Hallo code Hallo interface sectie van Hallo bestand Notifications.h te volgen:</span><span class="sxs-lookup"><span data-stu-id="a9b8d-129">Copy hello following code in hello interface section of hello file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="a9b8d-130">Hallo importeren richtlijn tooNotifications.m volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a9b8d-130">Add hello following import directive tooNotifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="a9b8d-131">Kopieer Hallo code in de Implementatiesectie Hallo van Hallo bestand Notifications.m te volgen.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-131">Copy hello following code in hello implementation section of hello file Notifications.m.</span></span>
   
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



    <span data-ttu-id="a9b8d-132">Deze klasse maakt gebruik van lokale opslag toostore en ophalen van de categorieën Hallo van nieuws dat dit apparaat ontvangt.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-132">This class uses local storage toostore and retrieve hello categories of news that this device will receive.</span></span> <span data-ttu-id="a9b8d-133">Het bevat ook, een tooregister methode voor deze categorieën met behulp van een [sjabloon](notification-hubs-templates-cross-platform-push-messages.md) registratie.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-133">Also, it contains a method tooregister for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="a9b8d-134">Toevoegen van een instructie importeren voor Notifications.h in Hallo AppDelegate.h bestand en een eigenschap voor een exemplaar van Hallo meldingen klasse toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a9b8d-134">In hello AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of hello Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="a9b8d-135">In Hallo **didFinishLaunchingWithOptions** methode in AppDelegate.m, Hallo code tooinitialize Hallo meldingen exemplaar aan begin van de methode Hallo Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-135">In hello **didFinishLaunchingWithOptions** method in AppDelegate.m, add hello code tooinitialize hello notifications instance at hello beginning of hello method.</span></span>  
   
    <span data-ttu-id="a9b8d-136">`HUBNAME`en `HUBLISTENACCESS` (gedefinieerd in hubinfo.h) moet al Hallo `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen vervangen door uw notification hub naam en het Hallo-verbindingsreeks voor *DefaultListenSharedAccessSignature*die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have hello `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="a9b8d-137">Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u alleen Hallo-sleutel voor listen toegang distribueren met uw clientapp.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="a9b8d-138">Luisteren toegang kunnen die uw app tooregister voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-138">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="a9b8d-139">Hallo volledige toegang tot de sleutel wordt gebruikt in een beveiligde back endservice voor het verzenden van meldingen en bestaande registraties wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-139">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="a9b8d-140">In Hallo **didRegisterForRemoteNotificationsWithDeviceToken** methode in AppDelegate.m, vervang Hallo-code in Hallo methode Hello toopass Hallo apparaat token toohello meldingen codeklasse te volgen.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-140">In hello **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace hello code in hello method with hello following code toopass hello device token toohello notifications class.</span></span> <span data-ttu-id="a9b8d-141">Hallo meldingen klasse voert Hallo registreren voor meldingen met Hallo categorieën.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-141">hello notifications class will perform hello registering for notifications with hello categories.</span></span> <span data-ttu-id="a9b8d-142">Als Hallo gebruiker categorieselecties wijzigt, noemen we Hallo `subscribeWithCategories` methode in antwoord toohello **abonneren** knop tooupdate ze.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-142">If hello user changes category selections, we call hello `subscribeWithCategories` method in response toohello **subscribe** button tooupdate them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a9b8d-143">Omdat het apparaattoken Hallo toegewezen door Hallo Apple Push Notification Service (APNS) kan op elk gewenst moment kans, moet u registreren voor meldingen vaak tooavoid melding fouten.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-143">Because hello device token assigned by hello Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="a9b8d-144">In dit voorbeeld registreert voor melding telkens wanneer die Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-144">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="a9b8d-145">Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie toopreserve bandbreedte als minder dan een dag is verstreken sinds de vorige registratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-145">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
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

    <span data-ttu-id="a9b8d-146">Houd er rekening mee dat op dit moment er geen andere code in Hallo moet **didRegisterForRemoteNotificationsWithDeviceToken** methode.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-146">Note that at this point there should be no other code in hello **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="a9b8d-147">Hallo volgende methoden moeten al aanwezig zijn in AppDelegate.m voltooid Hallo [aan de slag met Notification Hubs] [ get-started] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-147">hello following methods should already be present in AppDelegate.m from completing hello [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="a9b8d-148">Als dat niet het geval is, toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-148">If not, add them.</span></span>
   
    <span data-ttu-id="a9b8d-149">-(leeg) MessageBox:(NSString *) Titel bericht:(NSString *) tekstbericht {</span><span class="sxs-lookup"><span data-stu-id="a9b8d-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="a9b8d-150">}</span><span class="sxs-lookup"><span data-stu-id="a9b8d-150">}</span></span>
   
   * <span data-ttu-id="a9b8d-151">(leeg) toepassing:(UIApplication *) toepassing didReceiveRemoteNotification: (NSDictionary *) gebruikersgegevens {NSLog (@"% @", gebruikersgegevens);   [self MessageBox:@"Notification' bericht: [[gebruikersgegevens objectForKey:@"aps]' valueForKey:@"alert']]; }</span><span class="sxs-lookup"><span data-stu-id="a9b8d-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="a9b8d-152">Deze methode meldingen ontvangen wanneer het Hallo-app wordt uitgevoerd door een eenvoudige weer te geven afhandelt **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-152">This method handles notifications received when hello app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="a9b8d-153">Voeg een importinstructie voor AppDelegate.h en kopieer Hallo na de code in Hallo in ViewController.m, XCode gegenereerde **abonneren** methode.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-153">In ViewController.m, add a import statement for AppDelegate.h and copy hello following code into hello XCode-generated **subscribe** method.</span></span> <span data-ttu-id="a9b8d-154">Deze code wordt Hallo melding registratie toouse Hallo nieuwe categorie tags Hallo gebruiker ervoor in de gebruikersinterface Hallo gekozen heeft bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-154">This code will update hello notification registration toouse hello new category tags hello user has chosen in hello user interface.</span></span>
   
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
   
   <span data-ttu-id="a9b8d-155">Deze methode maakt u een **NSMutableArray** categorieën en maakt gebruik van Hallo **meldingen** klasse toostore Hallo lijst in Hallo lokale opslag en registers Hallo bijbehorende labels voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-155">This method creates an **NSMutableArray** of categories and uses hello **Notifications** class toostore hello list in hello local storage and registers hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="a9b8d-156">Wanneer categorieën worden gewijzigd, wordt met de nieuwe categorieën Hallo Hallo registratie nagemaakt.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-156">When categories are changed, hello registration is recreated with hello new categories.</span></span>
3. <span data-ttu-id="a9b8d-157">Voeg in ViewController.m, na de code in Hallo Hallo **viewDidLoad** methode tooset Hallo-gebruikersinterface op basis van categorieën Hallo eerder hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-157">In ViewController.m, add hello following code in hello **viewDidLoad** method tooset hello user interface based on hello previously saved categories.</span></span>

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="a9b8d-158">Hallo-app kunt nu een set categorieën opslaan in Hallo apparaat gebruikt voor lokale opslag tooregister bij Hallo notification hub als Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-158">hello app can now store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello app starts.</span></span>  <span data-ttu-id="a9b8d-159">Hallo-gebruiker kunt wijzigen Hallo selectie van categorieën tijdens runtime en klikt u op Hallo **abonneren** methode tooupdate Hallo registratie voor Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-159">hello user can change hello selection of categories at runtime and click hello **subscribe** method tooupdate hello registration for hello device.</span></span> <span data-ttu-id="a9b8d-160">Vervolgens wordt u Hallo app toosend Hallo nieuws meldingen rechtstreeks in het Hallo-app zelf op te splitsen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-160">Next, you will update hello app toosend hello breaking news notifications directly in hello app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="a9b8d-161">(optioneel) Verzenden van meldingen met tags</span><span class="sxs-lookup"><span data-stu-id="a9b8d-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="a9b8d-162">Als u geen toegang tot tooVisual Studio hebt, kunt u de volgende sectie toohello overslaan en meldingen verzenden vanuit Hallo app zelf.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-162">If you don't have access tooVisual Studio, you can skip toohello next section and send notifications from hello app itself.</span></span> <span data-ttu-id="a9b8d-163">U kunt ook Hallo juiste sjabloon melding verzenden vanuit Hallo [klassieke Azure-Portal] foutopsporingstabblad hello gebruiken voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-163">You can also send hello proper template notification from hello [Azure Classic Portal] using hello debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a><span data-ttu-id="a9b8d-164">(optioneel) Meldingen verzenden vanuit Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="a9b8d-164">(optional) Send notifications from hello device</span></span>
<span data-ttu-id="a9b8d-165">Normaal gesproken meldingen moeten worden verzonden door een back-endservice maar belangrijk nieuws om meldingen te verzenden rechtstreeks vanuit Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from hello app.</span></span> <span data-ttu-id="a9b8d-166">toodo dit hello wordt bijgewerkt `SendNotificationRESTAPI` methode die is gedefinieerd in Hallo [aan de slag met Notification Hubs] [ get-started] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-166">toodo this we will update hello `SendNotificationRESTAPI` method that we defined in hello [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="a9b8d-167">In ViewController.m update Hallo `SendNotificationRESTAPI` methode als volgt zodat het accepteert de parameter voor Hallo categorie label en verzendt Hallo juiste [sjabloon](notification-hubs-templates-cross-platform-push-messages.md) melding.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-167">In ViewController.m update hello `SendNotificationRESTAPI` method as follows so that it accepts a parameter for hello category tag and sends hello proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
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
2. <span data-ttu-id="a9b8d-168">In ViewController.m update Hallo **melding verzenden** actie, zoals wordt weergegeven in het Hallo-code die volgt.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-168">In ViewController.m update hello **Send Notification** action as shown in hello code that follows.</span></span> <span data-ttu-id="a9b8d-169">Zodat het wordt elke tag afzonderlijk met Hallo-meldingen verzenden en toomultiple platforms verzenden.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-169">So that it will send hello notifications using each tag individually and send toomultiple platforms.</span></span>

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



1. <span data-ttu-id="a9b8d-170">Bouw het project opnieuw op en controleer of er geen fouten in de build.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="a9b8d-171">Hallo-app uitvoeren en meldingen genereren</span><span class="sxs-lookup"><span data-stu-id="a9b8d-171">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="a9b8d-172">Druk op Hallo knop toobuild Hallo project uitvoeren en Hallo-app te starten.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-172">Press hello Run button toobuild hello project and start hello app.</span></span> <span data-ttu-id="a9b8d-173">Sommige belangrijk nieuws opties toosubscribe tooand selecteren en druk op Hallo **abonneren** knop.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-173">Select some breaking news options toosubscribe tooand then press hello **Subscribe** button.</span></span> <span data-ttu-id="a9b8d-174">U ziet een dialoogvenster Hallo meldingen bent geabonneerd op waarmee wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-174">You should see a dialog indicating hello notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="a9b8d-175">Wanneer u de optie **abonneren**, Hallo app converteert Hallo geselecteerd categorieën in tags en vraagt een nieuwe apparaatregistratie voor Hallo geselecteerd tags van Hallo notification hub.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-175">When you choose **Subscribe**, hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span>
2. <span data-ttu-id="a9b8d-176">Voer een bericht toobe verstuurd als belangrijk nieuws druk Hallo **melding verzenden** knop.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-176">Enter a message toobe sent as breaking news then press hello **Send Notification** button.</span></span> <span data-ttu-id="a9b8d-177">U kunt ook Hallo .NET-console-app toogenerate meldingen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-177">Alternatively, run hello .NET console app toogenerate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="a9b8d-178">Elk apparaat geabonneerd toobreaking nieuws ontvangt Hallo belangrijk nieuws meldingen die hebben verzonden.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-178">Each device subscribed toobreaking news will receive hello breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9b8d-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a9b8d-179">Next steps</span></span>
<span data-ttu-id="a9b8d-180">In deze zelfstudie hebt u geleerd hoe toobroadcast belangrijk nieuws per categorie.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-180">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="a9b8d-181">Houd rekening met een van de volgende zelfstudies waarin andere geavanceerde scenario's voor Notification Hubs Markeer Hallo voltooien:</span><span class="sxs-lookup"><span data-stu-id="a9b8d-181">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="a9b8d-182">**[Gebruik Notification Hubs toobroadcast gelokaliseerd belangrijk nieuws]**</span><span class="sxs-lookup"><span data-stu-id="a9b8d-182">**[Use Notification Hubs toobroadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="a9b8d-183">Meer informatie over hoe tooexpand Hallo nieuws app tooenable verzenden op te splitsen meldingen gelokaliseerd.</span><span class="sxs-lookup"><span data-stu-id="a9b8d-183">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
