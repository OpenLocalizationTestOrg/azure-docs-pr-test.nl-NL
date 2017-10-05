---
title: Notification Hubs belangrijk nieuws zelfstudie - iOS
description: Informatie over het gebruik van Azure Service Bus Notification Hubs voor belangrijk nieuws meldingen verzenden naar iOS-apparaten.
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
ms.openlocfilehash: dc47250db6fb3a2853dae24e02bda236154d93fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="de1a0-103">Notification Hubs gebruiken om belangrijk nieuws te verzenden</span><span class="sxs-lookup"><span data-stu-id="de1a0-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="de1a0-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="de1a0-104">Overview</span></span>
<span data-ttu-id="de1a0-105">Dit onderwerp leest u het gebruik van Azure Notification Hubs voor belangrijk nieuws meldingen naar een iOS-app-broadcast.</span><span class="sxs-lookup"><span data-stu-id="de1a0-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an iOS app.</span></span> <span data-ttu-id="de1a0-106">Als u klaar gaat u kunnen registreren voor nieuwscategorieën die u geïnteresseerd bent in op te splitsen en pushmeldingen voor deze categorieën ontvangen.</span><span class="sxs-lookup"><span data-stu-id="de1a0-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="de1a0-107">Dit scenario is een algemene patroon voor veel apps waarbij moeten meldingen worden verzonden naar groepen gebruikers die interesse in deze, zoals RSS-lezer, apps voor muziek ventilatoren, enzovoort eerder is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="de1a0-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="de1a0-108">Broadcast-scenario's zijn ingeschakeld door een of meer *labels* bij het maken van een registratie in de notification hub.</span><span class="sxs-lookup"><span data-stu-id="de1a0-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="de1a0-109">Wanneer u meldingen worden verzonden naar een label, ontvangen alle apparaten die zijn geregistreerd voor het label de melding.</span><span class="sxs-lookup"><span data-stu-id="de1a0-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="de1a0-110">Omdat tags gewoon tekenreeksen zijn, hoeven niet vooraf zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="de1a0-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="de1a0-111">Raadpleeg voor meer informatie over tags [Notification Hubs-Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="de1a0-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de1a0-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="de1a0-112">Prerequisites</span></span>
<span data-ttu-id="de1a0-113">In dit onderwerp is gebaseerd op de app die u hebt gemaakt in [aan de slag met Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="de1a0-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="de1a0-114">Voordat u deze zelfstudie begint, u moet al hebt voltooid [aan de slag met Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="de1a0-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="de1a0-115">Categorieselectie toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="de1a0-115">Add category selection to the app</span></span>
<span data-ttu-id="de1a0-116">De eerste stap is het toevoegen van de UI-elementen naar uw bestaande storyboard waarmee de gebruiker kan de categorieën selecteren om te registreren.</span><span class="sxs-lookup"><span data-stu-id="de1a0-116">The first step is to add the UI elements to your existing storyboard that enable the user to select categories to register.</span></span> <span data-ttu-id="de1a0-117">De categorieën die door een gebruiker is geselecteerd worden op het apparaat opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="de1a0-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="de1a0-118">Wanneer de app wordt gestart, wordt de apparaatregistratie van een in uw notification hub met de geselecteerde categorieën gemaakt als labels.</span><span class="sxs-lookup"><span data-stu-id="de1a0-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="de1a0-119">Voeg de volgende onderdelen van de objectbibliotheek in uw MainStoryboard_iPhone.storyboard:</span><span class="sxs-lookup"><span data-stu-id="de1a0-119">In your MainStoryboard_iPhone.storyboard add the following components from the object library:</span></span>
   
   * <span data-ttu-id="de1a0-120">Een label met 'Op te splitsen nieuws'-tekst</span><span class="sxs-lookup"><span data-stu-id="de1a0-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="de1a0-121">Labels met Categorieteksten "Wereld", 'Politiek', 'Business', 'Technologie', 'Wetenschappelijke', 'Sport'</span><span class="sxs-lookup"><span data-stu-id="de1a0-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="de1a0-122">Zes switches, één per categorie instellen elke switch **status** worden **uit** standaard.</span><span class="sxs-lookup"><span data-stu-id="de1a0-122">Six switches, one per category, set each switch **State** to be **Off** by default.</span></span>
   * <span data-ttu-id="de1a0-123">Een knop met het label 'Abonneren'</span><span class="sxs-lookup"><span data-stu-id="de1a0-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="de1a0-124">Een storyboard ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="de1a0-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="de1a0-125">In de editor assistent aansluitingen voor alle schakelopties maken en het aanroepen van 'WorldSwitch', 'PoliticsSwitch', 'BusinessSwitch', 'TechnologySwitch', 'ScienceSwitch', 'SportsSwitch'</span><span class="sxs-lookup"><span data-stu-id="de1a0-125">In the assistant editor, create outlets for all the switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="de1a0-126">Een actie voor de knop met de naam 'abonneren' maken.</span><span class="sxs-lookup"><span data-stu-id="de1a0-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="de1a0-127">Uw ViewController.h moeten het volgende bevatten:</span><span class="sxs-lookup"><span data-stu-id="de1a0-127">Your ViewController.h should contain the following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="de1a0-128">Maak een nieuwe **Cocoa Touch klasse** aangeroepen `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="de1a0-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="de1a0-129">Kopieer de volgende code in de sectie interface van het bestand Notifications.h:</span><span class="sxs-lookup"><span data-stu-id="de1a0-129">Copy the following code in the interface section of the file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="de1a0-130">De volgende importinstructie aan Notifications.m toevoegen:</span><span class="sxs-lookup"><span data-stu-id="de1a0-130">Add the following import directive to Notifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="de1a0-131">Kopieer de volgende code in de Implementatiesectie van het bestand Notifications.m.</span><span class="sxs-lookup"><span data-stu-id="de1a0-131">Copy the following code in the implementation section of the file Notifications.m.</span></span>
   
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



    <span data-ttu-id="de1a0-132">Deze klasse maakt gebruik van lokale opslag op te slaan en het ophalen van de categorieën van nieuws dat dit apparaat ontvangt.</span><span class="sxs-lookup"><span data-stu-id="de1a0-132">This class uses local storage to store and retrieve the categories of news that this device will receive.</span></span> <span data-ttu-id="de1a0-133">Het bevat ook, een methode om te registreren voor deze categorieën met behulp van een [sjabloon](notification-hubs-templates-cross-platform-push-messages.md) registratie.</span><span class="sxs-lookup"><span data-stu-id="de1a0-133">Also, it contains a method to register for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="de1a0-134">In het bestand AppDelegate.h een importinstructie voor Notifications.h toevoegen en een eigenschap voor een exemplaar van de klasse meldingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="de1a0-134">In the AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of the Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="de1a0-135">In de **didFinishLaunchingWithOptions** methode in AppDelegate.m, voeg de code voor het initialiseren van het exemplaar van de meldingen aan het begin van de methode.</span><span class="sxs-lookup"><span data-stu-id="de1a0-135">In the **didFinishLaunchingWithOptions** method in AppDelegate.m, add the code to initialize the notifications instance at the beginning of the method.</span></span>  
   
    <span data-ttu-id="de1a0-136">`HUBNAME`en `HUBLISTENACCESS` (gedefinieerd in hubinfo.h) al de `<hub name>` en `<connection string with listen access>` tijdelijke aanduidingen vervangen door de naam van uw notification hub en de verbindingsreeks voor *DefaultListenSharedAccessSignature* die u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="de1a0-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have the `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="de1a0-137">Omdat de referenties die worden gedistribueerd met een client-app niet over het algemeen veilig, moet u de sleutel voor listen toegang alleen distribueren met uw clientapp.</span><span class="sxs-lookup"><span data-stu-id="de1a0-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="de1a0-138">Luisteren toegang kunnen uw app registreren voor meldingen, maar bestaande registraties kan niet worden gewijzigd en kunnen niet worden meldingen verzonden.</span><span class="sxs-lookup"><span data-stu-id="de1a0-138">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="de1a0-139">De volledige toegang tot de sleutel wordt gebruikt in een beveiligde back-endservice voor het verzenden van meldingen en bestaande registraties wijzigen.</span><span class="sxs-lookup"><span data-stu-id="de1a0-139">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="de1a0-140">In de **didRegisterForRemoteNotificationsWithDeviceToken** methode in AppDelegate.m, vervang de code in de methode met de volgende code naar het apparaattoken doorgeven aan de klasse meldingen.</span><span class="sxs-lookup"><span data-stu-id="de1a0-140">In the **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace the code in the method with the following code to pass the device token to the notifications class.</span></span> <span data-ttu-id="de1a0-141">De klasse meldingen wordt uitgevoerd om het registreren voor meldingen met de categorieën.</span><span class="sxs-lookup"><span data-stu-id="de1a0-141">The notifications class will perform the registering for notifications with the categories.</span></span> <span data-ttu-id="de1a0-142">Als de gebruiker categorieselecties wijzigt, noemen we de `subscribeWithCategories` methode in reactie op de **abonneren** knop bijwerken.</span><span class="sxs-lookup"><span data-stu-id="de1a0-142">If the user changes category selections, we call the `subscribeWithCategories` method in response to the **subscribe** button to update them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="de1a0-143">Omdat het apparaattoken toegewezen door de Apple Push Notification Service (APNS) kan op elk gewenst moment kans, kunt u moet registreren voor meldingen vaak ter voorkoming van fouten van de melding.</span><span class="sxs-lookup"><span data-stu-id="de1a0-143">Because the device token assigned by the Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="de1a0-144">In dit voorbeeld registreert voor melding van elke keer dat de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="de1a0-144">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="de1a0-145">Voor apps die vaak worden uitgevoerd, kunt meer dan één keer per dag, u waarschijnlijk overslaan registratie om bandbreedte te besparen als minder dan een dag is verstreken sinds de vorige registratie.</span><span class="sxs-lookup"><span data-stu-id="de1a0-145">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves the categories from local storage and requests a registration for these categories
        // each time the app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="de1a0-146">Houd er rekening mee dat op dit moment moet er geen andere code in de **didRegisterForRemoteNotificationsWithDeviceToken** methode.</span><span class="sxs-lookup"><span data-stu-id="de1a0-146">Note that at this point there should be no other code in the **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="de1a0-147">De volgende methoden moeten al aanwezig zijn in AppDelegate.m voltooid de [aan de slag met Notification Hubs] [ get-started] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="de1a0-147">The following methods should already be present in AppDelegate.m from completing the [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="de1a0-148">Als dat niet het geval is, toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="de1a0-148">If not, add them.</span></span>
   
    <span data-ttu-id="de1a0-149">-(leeg) MessageBox:(NSString *) Titel bericht:(NSString *) tekstbericht {</span><span class="sxs-lookup"><span data-stu-id="de1a0-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="de1a0-150">}</span><span class="sxs-lookup"><span data-stu-id="de1a0-150">}</span></span>
   
   * <span data-ttu-id="de1a0-151">(leeg) toepassing:(UIApplication *) toepassing didReceiveRemoteNotification: (NSDictionary *) gebruikersgegevens {NSLog (@"% @", gebruikersgegevens);   [self MessageBox:@"Notification' bericht: [[gebruikersgegevens objectForKey:@"aps]' valueForKey:@"alert']]; }</span><span class="sxs-lookup"><span data-stu-id="de1a0-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="de1a0-152">Deze methode meldingen ontvangen wanneer de app wordt uitgevoerd door een eenvoudige weer te geven afhandelt **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="de1a0-152">This method handles notifications received when the app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="de1a0-153">Voeg een importinstructie voor AppDelegate.h in ViewController.m, en kopieer de volgende code in XCode gegenereerde **abonneren** methode.</span><span class="sxs-lookup"><span data-stu-id="de1a0-153">In ViewController.m, add a import statement for AppDelegate.h and copy the following code into the XCode-generated **subscribe** method.</span></span> <span data-ttu-id="de1a0-154">Deze code wordt de registratie voor het gebruik van de nieuwe categorielabels die de gebruiker heeft gekozen in de gebruikersinterface worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="de1a0-154">This code will update the notification registration to use the new category tags the user has chosen in the user interface.</span></span>
   
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
   
   <span data-ttu-id="de1a0-155">Deze methode maakt u een **NSMutableArray** van de categorieën en gebruikt de **meldingen** klasse voor het opslaan van de lijst in de lokale opslag en registreert de bijbehorende tags voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="de1a0-155">This method creates an **NSMutableArray** of categories and uses the **Notifications** class to store the list in the local storage and registers the corresponding tags with your notification hub.</span></span> <span data-ttu-id="de1a0-156">Wanneer categorieën worden gewijzigd, wordt de registratie opnieuw gemaakt met de nieuwe categorieën.</span><span class="sxs-lookup"><span data-stu-id="de1a0-156">When categories are changed, the registration is recreated with the new categories.</span></span>
3. <span data-ttu-id="de1a0-157">In ViewController.m, voeg de volgende code in de **viewDidLoad** methode de gebruikersinterface instellen op basis van de eerder opgeslagen categorieën.</span><span class="sxs-lookup"><span data-stu-id="de1a0-157">In ViewController.m, add the following code in the **viewDidLoad** method to set the user interface based on the previously saved categories.</span></span>

        // This updates the UI on startup based on the status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="de1a0-158">De app kan nu een set van categorieën worden opgeslagen in de lokale opslag van apparaat wordt gebruikt om u te registreren bij de notification hub wanneer de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="de1a0-158">The app can now store a set of categories in the device local storage used to register with the notification hub whenever the app starts.</span></span>  <span data-ttu-id="de1a0-159">De gebruiker kan de selectie van categorieën op runtime en klik op wijzigen de **abonneren** methode voor het bijwerken van de registratie voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="de1a0-159">The user can change the selection of categories at runtime and click the **subscribe** method to update the registration for the device.</span></span> <span data-ttu-id="de1a0-160">Vervolgens kunt u de app het laatste nieuws om meldingen te verzenden rechtstreeks in de app zelf wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="de1a0-160">Next, you will update the app to send the breaking news notifications directly in the app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="de1a0-161">(optioneel) Verzenden van meldingen met tags</span><span class="sxs-lookup"><span data-stu-id="de1a0-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="de1a0-162">Als u geen toegang tot Visual Studio hebt, kunt u met de volgende sectie overslaan en meldingen verzenden vanuit de app zelf.</span><span class="sxs-lookup"><span data-stu-id="de1a0-162">If you don't have access to Visual Studio, you can skip to the next section and send notifications from the app itself.</span></span> <span data-ttu-id="de1a0-163">U kunt ook de juiste sjabloon melding verzenden de [klassieke Azure-Portal] met behulp van het foutopsporingstabblad voor uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="de1a0-163">You can also send the proper template notification from the [Azure Classic Portal] using the debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-the-device"></a><span data-ttu-id="de1a0-164">(optioneel) Meldingen verzenden vanuit het apparaat</span><span class="sxs-lookup"><span data-stu-id="de1a0-164">(optional) Send notifications from the device</span></span>
<span data-ttu-id="de1a0-165">Normaal gesproken meldingen moeten worden verzonden door een back-endservice maar belangrijk nieuws om meldingen te verzenden rechtstreeks vanuit de app.</span><span class="sxs-lookup"><span data-stu-id="de1a0-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from the app.</span></span> <span data-ttu-id="de1a0-166">Hiervoor wordt bijgewerkt de `SendNotificationRESTAPI` methode die is gedefinieerd in de [aan de slag met Notification Hubs] [ get-started] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="de1a0-166">To do this we will update the `SendNotificationRESTAPI` method that we defined in the [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="de1a0-167">In de update ViewController.m de `SendNotificationRESTAPI` methode als volgt zodat het accepteert de parameter voor het label categorie en verzendt de juiste [sjabloon](notification-hubs-templates-cross-platform-push-messages.md) melding.</span><span class="sxs-lookup"><span data-stu-id="de1a0-167">In ViewController.m update the `SendNotificationRESTAPI` method as follows so that it accepts a parameter for the category tag and sends the proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct the messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated the token to be used in the authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the template notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add the category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
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
2. <span data-ttu-id="de1a0-168">In de update ViewController.m de **melding verzenden** actie, zoals wordt weergegeven in de volgende code.</span><span class="sxs-lookup"><span data-stu-id="de1a0-168">In ViewController.m update the **Send Notification** action as shown in the code that follows.</span></span> <span data-ttu-id="de1a0-169">Zodat het wordt verzenden van meldingen met elke tag afzonderlijk en naar meerdere platforms verzenden.</span><span class="sxs-lookup"><span data-stu-id="de1a0-169">So that it will send the notifications using each tag individually and send to multiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send the message as breaking news for each category to WNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="de1a0-170">Bouw het project opnieuw op en controleer of er geen fouten in de build.</span><span class="sxs-lookup"><span data-stu-id="de1a0-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="de1a0-171">Voer de app en meldingen genereren</span><span class="sxs-lookup"><span data-stu-id="de1a0-171">Run the app and generate notifications</span></span>
1. <span data-ttu-id="de1a0-172">Druk op de knop uitvoeren op het project bouwen en de app te starten.</span><span class="sxs-lookup"><span data-stu-id="de1a0-172">Press the Run button to build the project and start the app.</span></span> <span data-ttu-id="de1a0-173">Sommige belangrijk nieuws opties selecteren om te abonneren op en druk vervolgens op de **abonneren** knop.</span><span class="sxs-lookup"><span data-stu-id="de1a0-173">Select some breaking news options to subscribe to and then press the **Subscribe** button.</span></span> <span data-ttu-id="de1a0-174">U ziet een dialoogvenster waarmee wordt aangegeven in dat de meldingen bent geabonneerd op.</span><span class="sxs-lookup"><span data-stu-id="de1a0-174">You should see a dialog indicating the notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="de1a0-175">Wanneer u de optie **abonneren**, de app de geselecteerde categorieën converteert naar labels en een nieuwe apparaatregistratie voor de geselecteerde codes aanvragen van de notification hub.</span><span class="sxs-lookup"><span data-stu-id="de1a0-175">When you choose **Subscribe**, the app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span>
2. <span data-ttu-id="de1a0-176">Voer een bericht wordt verzonden als belangrijk nieuws druk de **melding verzenden** knop.</span><span class="sxs-lookup"><span data-stu-id="de1a0-176">Enter a message to be sent as breaking news then press the **Send Notification** button.</span></span> <span data-ttu-id="de1a0-177">Ook uitvoeren van de .NET-consoletoepassing om meldingen te genereren.</span><span class="sxs-lookup"><span data-stu-id="de1a0-177">Alternatively, run the .NET console app to generate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="de1a0-178">Elk apparaat geabonneerd op belangrijk nieuws ontvangt de belangrijk nieuws-meldingen die u zojuist hebt verzonden.</span><span class="sxs-lookup"><span data-stu-id="de1a0-178">Each device subscribed to breaking news will receive the breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de1a0-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de1a0-179">Next steps</span></span>
<span data-ttu-id="de1a0-180">In deze zelfstudie hebt u geleerd hoe belangrijk nieuws per categorie-broadcast.</span><span class="sxs-lookup"><span data-stu-id="de1a0-180">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="de1a0-181">Houd rekening met het voltooien van een van de volgende zelfstudies die andere geavanceerde scenario's voor Notification Hubs markeren:</span><span class="sxs-lookup"><span data-stu-id="de1a0-181">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="de1a0-182">**[Notification Hubs gebruiken voor het uitzenden van gelokaliseerde belangrijk nieuws]**</span><span class="sxs-lookup"><span data-stu-id="de1a0-182">**[Use Notification Hubs to broadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="de1a0-183">Informatie over het uitbreiden van de app belangrijk nieuws zodat gelokaliseerde verzenden van meldingen.</span><span class="sxs-lookup"><span data-stu-id="de1a0-183">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="de1a0-184">[Notification Hubs gebruiken voor het uitzenden van gelokaliseerde belangrijk nieuws]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="de1a0-184">[Use Notification Hubs to broadcast localized breaking news]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
<span data-ttu-id="de1a0-185">[klassieke Azure-Portal]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="de1a0-185">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
