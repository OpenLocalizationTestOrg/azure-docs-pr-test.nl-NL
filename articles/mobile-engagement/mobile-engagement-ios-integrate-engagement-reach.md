---
title: Mobile Engagement iOS SDK-integratie bereiken aaaAzure | Microsoft Docs
description: Meest recente updates en procedures voor iOS SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a>Hoe tooIntegrate Engagement bereiken op iOS
U moet volgen Hallo integratie procedure wordt beschreven in Hallo [hoe tooIntegrate Engagement voor iOS-document](mobile-engagement-ios-integrate-engagement.md) voordat u deze handleiding.

Deze documentatie vereist XCode 8. Als u echt XCode 7 afhankelijk wordt u Hallo [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Er is een bekend probleem in de vorige versie bij het uitvoeren op iOS-10-apparaten: Er zijn geen kennisgevingen systeem waarop actie is ondernomen. toofix dit hebt u tooimplement Hallo API afgeschaft `application:didReceiveRemoteNotification:` in uw app delegeren als volgt:

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Deze tijdelijke oplossing wordt niet aanbevolen** zoals dit gedrag in een toekomstige (zelfs secundaire) iOS-versie-upgrade wijzigen kunt omdat deze API voor iOS is afgeschaft. Zo snel mogelijk moet u tooXCode 8 overschakelen.
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Uw app tooreceive achtergrond-Pushmeldingen inschakelen
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a>Stappen voor integratie
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a>Hallo Engagement bereiken SDK in uw iOS-project insluiten
* Hallo Reach-sdk toevoegen aan uw Xcode-project. Ga te in Xcode**Project \> toevoegen tooproject** en kies Hallo `EngagementReach` map.

### <a name="modify-your-application-delegate"></a>Uw toepassingsgemachtigde wijzigen
* Hallo bovenaan uw implementatiebestand in Hallo Engagement bereiken module te importeren:

      [...]
      #import "AEReachModule.h"
* In de methode `applicationDidFinishLaunching:` of `application:didFinishLaunchingWithOptions:`, maakt u een reach-module en geef dit door bestaande initialisatieregel tooyour:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* Wijzig **'icon.png'** tekenreeks met de naam van de installatiekopie Hallo u wilt gebruiken als uw meldingspictogram.
* Als u wilt dat toouse Hallo optie *Update badge waarde* in Reach-campagnes of als u wilt dat de native pushberichten toouse \<SaaS/Reach API/campagne indeling Native Push\> campagnes, moet u laten Hallo Reach-module beheren Hallo badge pictogram zelf (deze wordt automatisch gewist Hallo toepassing badge en ook opnieuw instellen Engagement opgeslagen telkens wanneer de toepassing hello gestart of foregrounded is Hallo-waarde). Dit wordt gedaan door Hallo volgt regel na de initialisatie van de Reach-module toe te voegen:

      [reach setAutoBadgeEnabled:YES];
* Als u toohandle Reach gegevens-push wilt, moet u uw toepassingsgemachtigde toohello voldoen laten `AEReachDataPushDelegate` protocol. Hallo volgt regel na de initialisatie van de Reach-module toevoegen:

      [reach setDataPushDelegate:self];
* Vervolgens kunt u methoden Hallo implementeren `onDataPushStringReceived:` en `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in uw toepassingsgemachtigde:

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a>Category
Hallo categorieparameter is optioneel bij het maken van een campagne Push-gegevens en kunt dat u gegevens toofilter pushes. Dit is handig als u wilt dat de verschillende typen toopush van `Base64` gegevens en wilt tooidentify hun type voordat ze worden geparseerd.

**Uw toepassing is nu gereed tooreceive en weergave inhoud bereiken!**

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a>Hoe tooreceive aankondigingen en polls op elk gewenst moment
Engagement kunt Reach meldingen verzenden tooyour eindgebruikers op elk gewenst moment via Hallo Apple Push Notification Service.

tooenable deze functionaliteit u tooprepare hebben uw aanvraag voor Apple pushmeldingen en uw toepassingsgemachtigde wijzigen.

### <a name="prepare-your-application-for-apple-push-notifications"></a>Uw aanvraag voor Apple pushmeldingen voorbereiden
Volg Hallo guide: [hoe tooPrepare uw aanvraag voor Apple Pushmeldingen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

### <a name="add-hello-necessary-client-code"></a>Hallo nodig clientcode toevoegen
*Uw toepassing hebt op dit moment een geregistreerde Apple push-certificaat in Hallo Engagement frontend.*

Als deze niet al gebeurt, moet u tooregister uw toepassing tooreceive-pushmeldingen.

* Importeren Hallo `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>
* Toevoegen van Hallo volgt regel wanneer uw toepassing wordt gestart (meestal in `application:didFinishLaunchingWithOptions:`):

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

Vervolgens moet u tooprovide tooEngagement hello apparaattoken geretourneerd door de servers van Apple. Dit doet u in het Hallo-methode met de naam `application:didRegisterForRemoteNotificationsWithDeviceToken:` in uw toepassingsgemachtigde:

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

U hebt ten slotte tooinform Hallo Engagement SDK wanneer uw toepassing een externe melding ontvangt. toodo die aanroepen Hallo methode `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in uw toepassingsgemachtigde:

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> Standaard controleert de Hallo completionHandler Engagement bereiken. Als u wilt dat toomanually reageren toohello `handler` blokkeren in uw code, kunt u nil voor Hallo doorgeven `handler` argument en beheer Hallo voltooiing blokkeren zelf. Zie Hallo `UIBackgroundFetchResult` type voor een lijst van mogelijke waarden.
>
>

### <a name="full-example"></a>Compleet voorbeeld
Hier volgt een voorbeeld van een volledige integratie:

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>UNUserNotificationCenter gemachtigde conflicten oplossen

*Als uw toepassing noch een van de bibliotheken van de derde partij implementeert een `UNUserNotificationCenterDelegate` en vervolgens kunt u dit gedeelte overslaan.*

Een `UNUserNotificationCenter` gemachtigde wordt gebruikt door Hallo SDK toomonitor Hallo levenscyclus van de Engagement-meldingen op apparaten waarop iOS 10 of hoger. Hallo SDK heeft een eigen implementatie Hallo `UNUserNotificationCenterDelegate` protocol, maar er mag slechts één `UNUserNotificationCenter` delegeren per toepassing. Geen andere gedelegeerde toegevoegd toohello `UNUserNotificationCenter` object Hello Engagement een conflict veroorzaken. Als Hallo SDK uw of een andere leveranciers gemachtigde detecteert en maakt geen gebruik van een eigen implementatie toogive Hallo u een kans tooresolve conflicten. Hebt u tooadd Hallo Engagement logica tooyour eigenaar gemachtigde in volgorde tooresolve Hallo conflicten.

Er zijn twee manieren tooachieve dit.

Voorstel 1, door de gemachtigde doorsturen roept toohello SDK:

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

Of voorstel 2, door het overnemen van Hallo `AEUserNotificationHandler` klasse

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> U kunt bepalen of een melding afkomstig van Engagement of niet door het doorgeven van is de `userInfo` woordenlijst toohello Agent `isEngagementPushPayload:` klasse-methode.

Zorg ervoor dat Hallo `UNUserNotificationCenter` gemachtigde van het object is ingesteld tooyour gemachtigde binnen een Hallo `application:willFinishLaunchingWithOptions:` of Hallo `application:didFinishLaunchingWithOptions:` methode van de toepassingsgemachtigde van uw.
Bijvoorbeeld, als u Hallo hierboven voorstel 1 geïmplementeerd:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a>Hoe toocustomize campagnes
### <a name="notifications"></a>Meldingen
Er zijn twee typen meldingen: systeem en in-app-meldingen.

Systeemmeldingen worden afgehandeld door iOS en kunnen niet worden aangepast.

In-app-meldingen zijn gemaakt van een weergave die de huidige toepassingsvenster toohello wordt dynamisch worden toegevoegd. Dit is een melding overlay genoemd. Melding overlays zijn ideaal voor een snelle integratie omdat ze geen vereist toomodify u elke weergave in uw toepassing.

#### <a name="layout"></a>Lay-out
toomodify hello uiterlijk van uw in-app-meldingen, kunt u eenvoudig hello bestand wijzigen `AENotificationView.xib` tooyour moet, zolang u Hallo labelwaarden en typen van de bestaande subweergaven Hallo houden.

Standaard worden in-app-meldingen weergegeven onder Hallo van welkomstscherm. Als u liever toodisplay opgegeven ze Hallo boven aan het scherm bewerken Hallo `AENotificationView.xib` en wijzig Hallo `AutoSizing` eigenschap van hoofdweergave Hallo zodat het Hallo boven aan de superview kan worden bewaard.

#### <a name="categories"></a>Categorieën
Als u Hallo opgegeven lay-out wijzigt, wijzigt u Hallo uiterlijk van al uw meldingen. Categorieën kunnen toodefine u die verschillende gericht lijkt (mogelijk gedrag) voor meldingen. Een categorie kan worden opgegeven wanneer u een Reach-campagne maken. Houd er rekening mee dat categorieën ook kunnen u aanpassen aankondigingen en polls, die verderop in dit document wordt beschreven.

tooregister een categorie-handler voor uw meldingen, moet u tooadd een aanroep van zodra Hallo reach-module is geïnitialiseerd.

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

`myNotifier`moet een exemplaar van een object dat toohello protocol voldoet `AENotifier`.

U kunt Hallo protocolmethoden implementeren door uzelf of u kunt bestaande klasse van tooreimplement hello `AEDefaultNotifier` al uitvoert, wordt de meeste Hallo werk.

Bijvoorbeeld, als u de weergave van meldingen Hallo tooredefine voor een specifieke categorie wilt, kunt u dit voorbeeld:

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

Dit eenvoudige voorbeeld van de categorie wordt ervan uitgegaan dat u hebt een bestand met de naam `MyNotificationView.xib` in de bundel hoofdtoepassing. Als het Hallo-methode is niet kunnen toofind een overeenkomstige `.xib`, Hallo-melding worden niet weergegeven en Engagement wordt een bericht in de console Hallo uitvoer.

Hallo opgegeven kroontjespen bestand moet inachtneming van Hallo volgens de regels voor:

* Het moet slechts één weergave bevatten.
* Subweergaven moet van dezelfde zoals Hallo zijn binnen de opgegeven Hallo kroontjespen bestand met de naam typen Hallo`AENotificationView.xib`
* Subweergaven moeten Hallo dezelfde labels als Hallo zijn binnen de opgegeven Hallo kroontjespen bestand met de naam hebben`AENotificationView.xib`

> [!TIP]
> Alleen opgegeven Hallo kroontjespen bestand kopiëren, met de naam `AENotificationView.xib`, en beginnen met werken vanaf daar. Maar wees voorzichtig, Hallo weergeven binnen dit kroontjespen-bestand is gekoppeld aan de klasse toohello `AENotificationView`. Deze klasse gedefinieerd Hallo methode `layoutSubViews` toomove en het formaat ervan subweergaven volgens toocontext. U kunt tooreplace deze met een `UIView` of u aangepaste weergave-klasse.
>
>

Als u diepere aanpassing van uw meldingen (als u wilt bijvoorbeeld tooload uw weergave rechtstreeks vanuit Hallo code), het verdient aanbeveling tootake bekijkt hello code en klasse documentatie bij de gegevensbron van opgegeven `Protocol ReferencesDefaultNotifier` en `AENotifier`.

Let op: u kunt dezelfde melder voor verschillende categorieën Hallo.

U kunt ook opnieuw gedefinieerde Hallo standaard melder als volgt:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a>Afhandeling van melding
Wanneer u de standaardcategorie hello, een aantal methoden levenscyclus worden aangeroepen op Hallo `AEReachContent` tooreport statistieken en update Hallo campagne status object:

* Wanneer Hallo melding wordt weergegeven in de toepassing, Hallo `displayNotification` methode (die statistieken) wordt aangeroepen door `AEReachModule` als `handleNotification:` retourneert `YES`.
* Als het Hallo-melding wordt gesloten, Hallo `exitNotification` methode wordt aangeroepen, statistiek wordt gerapporteerd en volgende campagnes kunnen nu worden verwerkt.
* Als u Hallo melding klikt, `actionNotification` is aangeroepen, statistiek is gerapporteerd en Hallo gekoppeld actie wordt uitgevoerd.

Als uw implementatie van `AENotifier` omleidingen Hallo standaardgedrag, hebt u toocall deze methoden van de levenscyclus van de door u zelf. Hallo volgen voorbeelden illustreren bepaalde gevallen waarbij Hallo standaardgedrag wordt overgeslagen:

* U kunt niet uitbreiden `AEDefaultNotifier`, zoals u categorie verwerking helemaal geïmplementeerd.
* U overrode `prepareNotificationView:forContent:`, moet u ervoor dat toomap ten minste `onNotificationActioned` of `onNotificationExited` tooone uw U.I-besturingselementen.

> [!WARNING]
> Als `handleNotification:` er wordt een uitzondering, Hallo inhoud is verwijderd en `drop` is aangeroepen, dit wordt gemeld in statistieken en volgende campagnes kunnen nu worden verwerkt.
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a>Melding als onderdeel van een bestaande weergave opnemen
Overlays zijn ideaal voor een snelle integratie, maar kunnen worden soms niet handig of ongewenste neveneffecten hebben.

Als u niet tevreden met Hallo overlay systeem in een aantal weergaven bent, kunt u deze kunt aanpassen voor deze weergaven.

U kunt tooinclude onze lay-out voor de melding in uw bestaande weergaven. toodo twee implementatie stijlen dus er is:

1. Weergave van meldingen Hallo met interface builder toevoegen

   * Open *Builder Interface*
   * Een 320 x 60 (of als u op iPad 768 x 60) plaatst `UIView` waar u Hallo melding tooappear
   * Hallo tagwaarde voor deze weergave te stellen: **36822491**
2. Weergave van meldingen Hallo programmatisch toevoegen. Hallo code volgen wanneer de weergave is geïnitialiseerd alleen toe te voegen:

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

`NOTIFICATION_AREA_VIEW_TAG`macro vindt u in `AEDefaultNotifier.h`.

> [!NOTE]
> Standaard-melder Hallo detecteert automatisch die Hallo notification-indeling is opgenomen in deze weergave en wordt een overlay niet toevoegen voor.
>
>

### <a name="announcements-and-polls"></a>Aankondigingen en polls
#### <a name="layouts"></a>Indelingen
U kunt bestanden Hallo wijzigen `AEDefaultAnnouncementView.xib` en `AEDefaultPollView.xib` , zolang u Hallo labelwaarden en typen van de bestaande subweergaven Hallo houden.

#### <a name="categories"></a>Categorieën
##### <a name="alternate-layouts"></a>Alternatieve indelingen
Zoals meldingen, kan de categorie van de campagne Hallo gebruikte toohave alternatieve indelingen voor uw aankondigingen en polls zijn.

een categorie voor een aankondiging toocreate, moet u uitbreiden **AEAnnouncementViewController** en registreer deze zodra Hallo reach-module is geïnitialiseerd:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> Telkens wanneer een gebruiker wordt klikt u op een melding naar een aankondiging met Hallo categorie "Mijn\_categorie ', uw geregistreerde weergavebesturing (in dat geval `MyCustomAnnouncementViewController`) wordt geïnitialiseerd door het Hallo-methode aanroepen `initWithAnnouncement:` en Hallo weergave toegevoegde toohello huidige toepassingsvenster.
>
>

Bij de implementatie van Hallo `AEAnnouncementViewController` klasse hebt u tooread Hallo eigenschap `announcement` tooinitialize uw subweergaven. Overweeg het Hallo-voorbeeld hieronder, waarbij twee labels zijn geïnitialiseerd met behulp van `title` en `body` eigenschappen van Hallo `AEReachAnnouncement` klasse:

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

Als u niet wilt dat tooload uw weergaven door uzelf, maar u alleen tooreuse Hallo aankondiging weergave standaardindeling wilt, kunt u gewoon de aangepaste weergave-controller Hallo opgegeven klasse uitbreidt `AEDefaultAnnouncementViewController`. In dat geval dubbele Hallo kroontjespen bestand `AEDefaultAnnouncementView.xib` en wijzig deze zodat deze kan worden geladen door de aangepaste weergave-controller (voor een domeincontroller met de naam `CustomAnnouncementViewController`, moet u het bestand kroontjespen aanroepen `CustomAnnouncementView.xib`).

tooreplace hello standaardcategorie van aankondigingen, registreren gewoon de besturing van de aangepaste weergave voor Hallo categorie gedefinieerd in `kAEReachDefaultCategory`:

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

Polls kunnen worden aangepast Hallo dezelfde manier:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

Deze tijd, Hallo opgegeven `MyCustomPollViewController` moet uitbreiden `AEPollViewController`. Of u kunt tooextend van Hallo standaard domeincontroller: `AEDefaultPollViewController`.

> [!IMPORTANT]
> Vergeet niet toocall ofwel `action` (`submitAnswers:` voor aangepaste poll weergave domeincontrollers) of `exit` methode voordat de weergavebesturing hello wordt gesloten. Anders statistieken niet verzonden (d.w.z. geen analytics op Hallo campagne) en meer belangrijker nog volgende campagnes wordt niet gewaarschuwd als het toepassingsproces Hallo opnieuw is gestart.
>
>

##### <a name="implementation-example"></a>Voorbeeldimplementatie
In deze implementatie is Hallo aangepaste aankondiging weergave geladen uit een externe xib-bestand.

Net als voor geavanceerde melding aanpassing, wordt aangeraden toolook op Hallo broncode van de standaardimplementatie Hallo.

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
