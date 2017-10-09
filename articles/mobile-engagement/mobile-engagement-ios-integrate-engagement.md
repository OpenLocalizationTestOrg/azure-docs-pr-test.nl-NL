---
title: aaaAzure Mobile Engagement iOS SDK-integratie | Microsoft Docs
description: Meest recente updates en procedures voor iOS SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a>Hoe tooIntegrate Engagement voor iOS
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
>
>

Deze procedure wordt beschreven Hallo eenvoudigste manier tooactivate Engagement Analytics en bewaking van functies in uw iOS-toepassing.

Hallo Engagement SDK vereist iOS7 + en Xcode 8 +: Hallo implementatie het doel van uw toepassing moet ten minste iOS 7.

> [!NOTE]
> Als u echt XCode 7 afhankelijk wordt u Hallo [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Er is een bekend probleem op Hallo Reach-module van de vorige versie bij het uitvoeren op iOS-10-apparaten Zie [Hallo reach-module integratie](mobile-engagement-ios-integrate-engagement-reach.md) voor meer informatie. Als u kiest toouse Hallo SDK v3.2.4 maar overslaan Hallo `UserNotifications.framework` importeren in de volgende stap Hallo.
>
>

Hallo stappen te volgen zijn dat onvoldoende tooactivate Hallo rapport van Logboeken nodig toocompute alle statistische gegevens over gebruikers, sessies, activiteiten, Crashes en Technicals. rapport van Logboeken Hallo nodig toocompute andere statistieken zoals gebeurtenissen, fouten en taken moeten worden uitgevoerd handmatig met Hallo Engagement API (Zie [hoe toouse Hallo Mobile Engagement tags API in uw iOS-app geavanceerde](mobile-engagement-ios-use-engagement-api.md) sinds deze statistieken afhankelijk zijn van toepassing.

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a>Hallo Engagement SDK in uw iOS-project insluiten
* Hallo iOS SDK downloaden van [hier](http://aka.ms/qk2rnj).
* Add Hallo Engagement SDK tooyour iOS-project: in Xcode, klik met de rechtermuisknop op uw project en selecteer **' bestanden te toevoegen... '** en kies Hallo `EngagementSDK` map.
* Engagement vereist aanvullende frameworks toowork: in Projectverkenner Hallo opent u het deelvenster van uw project en selecteer de juiste doel Hallo. Open vervolgens Hallo **'Buildfasen'** tabblad en in Hallo **'Link Binary With Libraries'** menu deze frameworks toevoegen:

  * `UserNotifications.framework`-set Hallo koppelen als`Optional`
  * `AdSupport.framework`-set Hallo koppelen als`Optional`
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> Hallo AdSupport framework kan worden verwijderd. Engagement moet dit framework toocollect hello IDFA. Echter, IDFA-verzameling kan worden uitgeschakeld \<ios sdk-engagement idfa\> toocomply met Hallo nieuw Apple beleid met betrekking tot deze ID.
>
>

## <a name="initialize-hello-engagement-sdk"></a>Hallo Engagement SDK initialiseren
U moet uw Toepassingsgemachtigde toomodify:

* Importeer Hallo Engagement agent Hallo bovenaan uw implementatiebestand in:

      [...]
      #import "EngagementAgent.h"
* Initialiseren van Engagement binnen Hallo-methode '**applicationDidFinishLaunching:**'of'**toepassing: didFinishLaunchingWithOptions:**':

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a>Basic-rapportage
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a>Aanbevolen methode: overbelasting uw `UIViewController` klassen
In volgorde tooactivate Hallo rapport van alle Hallo Logboeken door Engagement toocompute gebruikers, sessies, activiteiten, Crashes en technische statistieken vereist, kunt u gewoon zodat alle uw `UIViewController` onderliggende klassen overnemen van Hallo `EngagementViewController` klassen (dezelfde regel voor `UITableViewController`  - \> `EngagementTableViewController`).

**Zonder Engagement:**

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

**Met Engagement:**

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a>Alternatieve methode: call `startActivity()` handmatig
Als u niet kunt of toooverload niet wilt dat uw `UIViewController` klassen, in plaats daarvan kunt u uw activiteiten starten door het aanroepen van `EngagementAgent`van methoden rechtstreeks.

> [!IMPORTANT]
> Hallo iOS SDK roept automatisch Hallo `endActivity()` methode wanneer de toepassing hello wordt gesloten. Het is dus *maximaal* toocall Hallo aanbevolen `startActivity` methode wanneer Hallo activiteit van Hallo gebruiker wijzigt, en te*nooit* aanroep Hallo `endActivity` -methode sinds het zorgt ervoor dat deze methode aanroepen Hallo huidige sessie toobe beëindigd.
>
>

## <a name="location-reporting"></a>Locatierapportage
Apple servicevoorwaarden is niet toegestaan toepassingen toouse locatie voor statistische doeleinden alleen bijhouden. Het verdient tooenable locatie rapporten dus alleen als uw toepassing hello locatie bijhouden in een andere reden ook gebruiken.

Beginnen met iOS 8, moet u een beschrijving van hoe uw app gebruikmaakt van locatie-services door in te stellen van een tekenreeks op voor de sleutel Hallo opgeven [NSLocationWhenInUseUsageDescription] of [NSLocationAlwaysUsageDescription]in uw app Info.plist-bestand. Als u een locatie op de achtergrond Hallo met Engagement tooreport wilt, kunt u Hallo key NSLocationAlwaysUsageDescription toevoegen. In andere gevallen moet u Hallo key NSLocationWhenInUseUsageDescription toevoegen. Houd er rekening mee dat u zowel NSLocationAlwaysAndWhenInUseUsageDescription NSLocationWhenInUseUsageDescription tooreport achtergrond locatie en op iOS 11 moet.

### <a name="lazy-area-location-reporting"></a>Vertraagde locatiemelding
Vertraagde locatiemelding kunt tooreport Hallo land, streek en plaats die zijn gekoppeld toodevices. Dit type locatie reporting maakt alleen gebruik van netwerklocaties (gebaseerd op de cel-ID of Wi-Fi). Hallo apparaat gebied wordt maximaal eenmaal per sessie gerapporteerd. Hallo GPS wordt nooit gebruikt en dit type locatie rapport heeft slechts weinig dus (geen toosay geen) impact op de accu Hallo.

Gerapporteerde gebieden zijn gebruikte toocompute geografische statistieken over gebruikers, sessies, gebeurtenissen en fouten. Ze kunnen ook worden gebruikt als criterium in Reach-campagnes. Hallo laatste bekende gebied gerapporteerd voor een apparaat kan opgehaalde Bedankt toohello [apparaat-API].

tooenable vertraagde locatie voor rapportage, Hallo volgt regel na tijdens de initialisatie van Hallo Engagement agent toevoegen:

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a>Rapportage van realtime locatie
Rapportage van realtime locatie kunt tooreport Hallo breedtegraad en lengtegraad gekoppeld toodevices. Standaard alleen gebruik van dit type locatie reporting netwerklocaties (gebaseerd op de cel-ID of Wi-Fi), en Hallo reporting is alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (dat wil zeggen tijdens een sessie).

Realtime-locaties zijn *niet* toocompute statistieken gebruikt. Het enige doel is tooallow Hallo gebruik van realtime geofencing \<Reach-doelgroep-geofencing\> criterium in Reach-campagnes.

tooenable realtime locatie rapportage, Hallo volgt regel na tijdens de initialisatie van Hallo Engagement agent toevoegen:

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a>GPS op basis van rapportage
Rapportage van realtime locatie alleen gebruikt standaard op basis van netwerklocaties. tooenable hello gebruik van GPS op basis van locaties (die veel meer nauwkeurige), toevoegen:

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a>Achtergrond rapportage
Rapportage van realtime locatie is standaard alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (dat wil zeggen tijdens een sessie). tooenable hello reporting ook op de achtergrond, toevoegen:

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> Wanneer de toepassing hello wordt uitgevoerd op de achtergrond, alleen op basis van netwerklocaties worden gerapporteerd, zelfs als u ingeschakeld Hallo GPS.
>
>

Implementatie van deze functie moet worden gebeld [startMonitoringSignificantLocationChanges] wanneer uw toepassing probeert het Hallo-achtergrond. Let erop dat deze automatisch opnieuw uw toepassing in de achtergrond Hallo Start wordt als een nieuwe locatie gebeurtenis binnenkomt.

## <a name="advanced-reporting"></a>Geavanceerde rapportage
Eventueel, als u tooreport toepassing specifieke gebeurtenissen, fouten en taken wilt, moet u toouse Hallo Engagement API via de methoden Hallo Hallo `EngagementAgent` klasse. Een object van deze klasse kan worden opgehaald door de aanroepende Hallo `[EngagementAgent shared]` statische methode.

Hallo Engagement API toouse kunnen alle Engagement geavanceerde mogelijkheden en wordt beschreven in Hallo hoe tooUse de Engagement-API voor iOS (en van de technische documentatie Hallo Hallo `EngagementAgent` klasse).

## <a name="disable-idfa-collection"></a>Uitschakelen van IDFA-verzameling
Standaard gebruikt Engagement Hallo [IDFA] toouniquely identificatie van een gebruiker. Maar als u reclame elders in Hallo-app niet gebruikt, kunt u geweigerd door Hallo controleproces App Store. IDFA-verzameling kan worden uitgeschakeld door toe te voegen Hallo preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in uw pch-bestand (of in Hallo `Build Settings` van uw toepassing). Dit zorgt ervoor dat er geen verwijzingen te is`ASIdentifierManager`, `advertisingIdentifier` of `isAdvertisingTrackingEnabled` Hallo toepassing gebouwd.

Integratie in Hallo **prefix.pch** bestand:

    #define ENGAGEMENT_DISABLE_IDFA
    ...

U kunt controleren of Hallo IDFA-verzameling is goed uitgeschakeld in uw toepassing door Hallo Engagement test logboeken controleren. Zie integratie testen Hallo\<ios-sdk-engagement-test-idfa\> documentatie voor meer informatie.

## <a name="disable-log-reporting"></a>Melden van logboek uitschakelen
### <a name="using-a-method-call"></a>Met behulp van een methodeaanroep van
Als u Engagement toostop logboeken verzenden wilt, kunt u bellen:

    [[EngagementAgent shared] setEnabled:NO];

Deze aanroep is permanent: hierbij `NSUserDefaults` toostore Hallo informatie.

U kunt reporting opnieuw door het aanroepen van dezelfde functie met Hallo logboek inschakelen `YES`.

### <a name="integration-in-your-settings-bundle"></a>Integratie in de bundel van uw instellingen
In plaats van deze functie aanroept, kunt u deze instelling ook integreren rechtstreeks in uw bestaande `Settings.bundle` bestand. Hallo tekenreeks `engagement_agent_enabled` moet worden gebruikt als een id van de voorkeursextensie Hallo en bijbehorende tooa schakeloptie moet zijn (`PSToggleSwitchSpecifier`).

Hallo volgende voorbeeld van `Settings.bundle` ziet u hoe tooimplement het:

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
[apparaat-API]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
