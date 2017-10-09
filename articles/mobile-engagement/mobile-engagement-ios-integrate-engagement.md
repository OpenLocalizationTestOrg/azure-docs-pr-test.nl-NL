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
# <a name="how-toointegrate-engagement-on-ios"></a><span data-ttu-id="1c681-103">Hoe tooIntegrate Engagement voor iOS</span><span class="sxs-lookup"><span data-stu-id="1c681-103">How tooIntegrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c681-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="1c681-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="1c681-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="1c681-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="1c681-106">iOS</span><span class="sxs-lookup"><span data-stu-id="1c681-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="1c681-107">Android</span><span class="sxs-lookup"><span data-stu-id="1c681-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="1c681-108">Deze procedure wordt beschreven Hallo eenvoudigste manier tooactivate Engagement Analytics en bewaking van functies in uw iOS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1c681-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="1c681-109">Hallo Engagement SDK vereist iOS7 + en Xcode 8 +: Hallo implementatie het doel van uw toepassing moet ten minste iOS 7.</span><span class="sxs-lookup"><span data-stu-id="1c681-109">hello Engagement SDK requires iOS7+ and Xcode 8+: hello deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="1c681-110">Als u echt XCode 7 afhankelijk wordt u Hallo [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="1c681-110">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="1c681-111">Er is een bekend probleem op Hallo Reach-module van de vorige versie bij het uitvoeren op iOS-10-apparaten Zie [Hallo reach-module integratie](mobile-engagement-ios-integrate-engagement-reach.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1c681-111">There is a known bug on hello Reach module of this previous version while running on iOS 10 devices see [hello reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="1c681-112">Als u kiest toouse Hallo SDK v3.2.4 maar overslaan Hallo `UserNotifications.framework` importeren in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c681-112">If you choose toouse hello SDK v3.2.4 then just skip hello `UserNotifications.framework` import in hello next step.</span></span>
>
>

<span data-ttu-id="1c681-113">Hallo stappen te volgen zijn dat onvoldoende tooactivate Hallo rapport van Logboeken nodig toocompute alle statistische gegevens over gebruikers, sessies, activiteiten, Crashes en Technicals.</span><span class="sxs-lookup"><span data-stu-id="1c681-113">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="1c681-114">rapport van Logboeken Hallo nodig toocompute andere statistieken zoals gebeurtenissen, fouten en taken moeten worden uitgevoerd handmatig met Hallo Engagement API (Zie [hoe toouse Hallo Mobile Engagement tags API in uw iOS-app geavanceerde](mobile-engagement-ios-use-engagement-api.md) sinds deze statistieken afhankelijk zijn van toepassing.</span><span class="sxs-lookup"><span data-stu-id="1c681-114">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API  (see [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="1c681-115">Hallo Engagement SDK in uw iOS-project insluiten</span><span class="sxs-lookup"><span data-stu-id="1c681-115">Embed hello Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="1c681-116">Hallo iOS SDK downloaden van [hier](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="1c681-116">Download hello iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="1c681-117">Add Hallo Engagement SDK tooyour iOS-project: in Xcode, klik met de rechtermuisknop op uw project en selecteer **' bestanden te toevoegen... '** en kies Hallo `EngagementSDK` map.</span><span class="sxs-lookup"><span data-stu-id="1c681-117">Add hello Engagement SDK tooyour iOS project: in Xcode, right click on your project and select **"Add files too..."** and choose hello `EngagementSDK` folder.</span></span>
* <span data-ttu-id="1c681-118">Engagement vereist aanvullende frameworks toowork: in Projectverkenner Hallo opent u het deelvenster van uw project en selecteer de juiste doel Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c681-118">Engagement requires additional frameworks toowork: in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="1c681-119">Open vervolgens Hallo **'Buildfasen'** tabblad en in Hallo **'Link Binary With Libraries'** menu deze frameworks toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1c681-119">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="1c681-120">`UserNotifications.framework`-set Hallo koppelen als`Optional`</span><span class="sxs-lookup"><span data-stu-id="1c681-120">`UserNotifications.framework` - set hello link as `Optional`</span></span>
  * <span data-ttu-id="1c681-121">`AdSupport.framework`-set Hallo koppelen als`Optional`</span><span class="sxs-lookup"><span data-stu-id="1c681-121">`AdSupport.framework` - set hello link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="1c681-122">Hallo AdSupport framework kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1c681-122">hello AdSupport framework can be removed.</span></span> <span data-ttu-id="1c681-123">Engagement moet dit framework toocollect hello IDFA.</span><span class="sxs-lookup"><span data-stu-id="1c681-123">Engagement needs this framework toocollect hello IDFA.</span></span> <span data-ttu-id="1c681-124">Echter, IDFA-verzameling kan worden uitgeschakeld \<ios sdk-engagement idfa\> toocomply met Hallo nieuw Apple beleid met betrekking tot deze ID.</span><span class="sxs-lookup"><span data-stu-id="1c681-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> toocomply with hello new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="1c681-125">Hallo Engagement SDK initialiseren</span><span class="sxs-lookup"><span data-stu-id="1c681-125">Initialize hello Engagement SDK</span></span>
<span data-ttu-id="1c681-126">U moet uw Toepassingsgemachtigde toomodify:</span><span class="sxs-lookup"><span data-stu-id="1c681-126">You need toomodify your Application Delegate:</span></span>

* <span data-ttu-id="1c681-127">Importeer Hallo Engagement agent Hallo bovenaan uw implementatiebestand in:</span><span class="sxs-lookup"><span data-stu-id="1c681-127">At hello top of your implementation file, import hello Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="1c681-128">Initialiseren van Engagement binnen Hallo-methode '**applicationDidFinishLaunching:**'of'**toepassing: didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="1c681-128">Initialize Engagement inside hello method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="1c681-129">Basic-rapportage</span><span class="sxs-lookup"><span data-stu-id="1c681-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="1c681-130">Aanbevolen methode: overbelasting uw `UIViewController` klassen</span><span class="sxs-lookup"><span data-stu-id="1c681-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="1c681-131">In volgorde tooactivate Hallo rapport van alle Hallo Logboeken door Engagement toocompute gebruikers, sessies, activiteiten, Crashes en technische statistieken vereist, kunt u gewoon zodat alle uw `UIViewController` onderliggende klassen overnemen van Hallo `EngagementViewController` klassen (dezelfde regel voor `UITableViewController`  - \> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="1c681-131">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from hello `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="1c681-132">**Zonder Engagement:**</span><span class="sxs-lookup"><span data-stu-id="1c681-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="1c681-133">**Met Engagement:**</span><span class="sxs-lookup"><span data-stu-id="1c681-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="1c681-134">Alternatieve methode: call `startActivity()` handmatig</span><span class="sxs-lookup"><span data-stu-id="1c681-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="1c681-135">Als u niet kunt of toooverload niet wilt dat uw `UIViewController` klassen, in plaats daarvan kunt u uw activiteiten starten door het aanroepen van `EngagementAgent`van methoden rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="1c681-135">If you cannot or do not want toooverload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c681-136">Hallo iOS SDK roept automatisch Hallo `endActivity()` methode wanneer de toepassing hello wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="1c681-136">hello iOS SDK automatically calls hello `endActivity()` method when hello application is closed.</span></span> <span data-ttu-id="1c681-137">Het is dus *maximaal* toocall Hallo aanbevolen `startActivity` methode wanneer Hallo activiteit van Hallo gebruiker wijzigt, en te*nooit* aanroep Hallo `endActivity` -methode sinds het zorgt ervoor dat deze methode aanroepen Hallo huidige sessie toobe beëindigd.</span><span class="sxs-lookup"><span data-stu-id="1c681-137">Thus, it is *HIGHLY* recommended toocall hello `startActivity` method whenever hello activity of hello user change, and too*NEVER* call hello `endActivity` method, since calling this method forces hello current session toobe ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="1c681-138">Locatierapportage</span><span class="sxs-lookup"><span data-stu-id="1c681-138">Location reporting</span></span>
<span data-ttu-id="1c681-139">Apple servicevoorwaarden is niet toegestaan toepassingen toouse locatie voor statistische doeleinden alleen bijhouden.</span><span class="sxs-lookup"><span data-stu-id="1c681-139">Apple terms of service do not allow applications toouse location tracking for statistics purpose only.</span></span> <span data-ttu-id="1c681-140">Het verdient tooenable locatie rapporten dus alleen als uw toepassing hello locatie bijhouden in een andere reden ook gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c681-140">Thus, it is recommended tooenable location reports only if your application also use hello location tracking for another reason.</span></span>

<span data-ttu-id="1c681-141">Beginnen met iOS 8, moet u een beschrijving van hoe uw app gebruikmaakt van locatie-services door in te stellen van een tekenreeks op voor de sleutel Hallo opgeven [NSLocationWhenInUseUsageDescription] of [NSLocationAlwaysUsageDescription]in uw app Info.plist-bestand.</span><span class="sxs-lookup"><span data-stu-id="1c681-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for hello key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="1c681-142">Als u een locatie op de achtergrond Hallo met Engagement tooreport wilt, kunt u Hallo key NSLocationAlwaysUsageDescription toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1c681-142">If you want tooreport location in hello background with Engagement, add hello key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="1c681-143">In andere gevallen moet u Hallo key NSLocationWhenInUseUsageDescription toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1c681-143">In all other cases, add hello key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="1c681-144">Houd er rekening mee dat u zowel NSLocationAlwaysAndWhenInUseUsageDescription NSLocationWhenInUseUsageDescription tooreport achtergrond locatie en op iOS 11 moet.</span><span class="sxs-lookup"><span data-stu-id="1c681-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription tooreport background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="1c681-145">Vertraagde locatiemelding</span><span class="sxs-lookup"><span data-stu-id="1c681-145">Lazy area location reporting</span></span>
<span data-ttu-id="1c681-146">Vertraagde locatiemelding kunt tooreport Hallo land, streek en plaats die zijn gekoppeld toodevices.</span><span class="sxs-lookup"><span data-stu-id="1c681-146">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="1c681-147">Dit type locatie reporting maakt alleen gebruik van netwerklocaties (gebaseerd op de cel-ID of Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="1c681-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="1c681-148">Hallo apparaat gebied wordt maximaal eenmaal per sessie gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="1c681-148">hello device area is reported at most once per session.</span></span> <span data-ttu-id="1c681-149">Hallo GPS wordt nooit gebruikt en dit type locatie rapport heeft slechts weinig dus (geen toosay geen) impact op de accu Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c681-149">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="1c681-150">Gerapporteerde gebieden zijn gebruikte toocompute geografische statistieken over gebruikers, sessies, gebeurtenissen en fouten.</span><span class="sxs-lookup"><span data-stu-id="1c681-150">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="1c681-151">Ze kunnen ook worden gebruikt als criterium in Reach-campagnes.</span><span class="sxs-lookup"><span data-stu-id="1c681-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="1c681-152">Hallo laatste bekende gebied gerapporteerd voor een apparaat kan opgehaalde Bedankt toohello [apparaat-API].</span><span class="sxs-lookup"><span data-stu-id="1c681-152">hello last known area reported for a device can be retrieved thanks toohello [Device API].</span></span>

<span data-ttu-id="1c681-153">tooenable vertraagde locatie voor rapportage, Hallo volgt regel na tijdens de initialisatie van Hallo Engagement agent toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1c681-153">tooenable lazy area location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="1c681-154">Rapportage van realtime locatie</span><span class="sxs-lookup"><span data-stu-id="1c681-154">Real time location reporting</span></span>
<span data-ttu-id="1c681-155">Rapportage van realtime locatie kunt tooreport Hallo breedtegraad en lengtegraad gekoppeld toodevices.</span><span class="sxs-lookup"><span data-stu-id="1c681-155">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="1c681-156">Standaard alleen gebruik van dit type locatie reporting netwerklocaties (gebaseerd op de cel-ID of Wi-Fi), en Hallo reporting is alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (dat wil zeggen tijdens een sessie).</span><span class="sxs-lookup"><span data-stu-id="1c681-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="1c681-157">Realtime-locaties zijn *niet* toocompute statistieken gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1c681-157">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="1c681-158">Het enige doel is tooallow Hallo gebruik van realtime geofencing \<Reach-doelgroep-geofencing\> criterium in Reach-campagnes.</span><span class="sxs-lookup"><span data-stu-id="1c681-158">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="1c681-159">tooenable realtime locatie rapportage, Hallo volgt regel na tijdens de initialisatie van Hallo Engagement agent toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1c681-159">tooenable real time location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="1c681-160">GPS op basis van rapportage</span><span class="sxs-lookup"><span data-stu-id="1c681-160">GPS based reporting</span></span>
<span data-ttu-id="1c681-161">Rapportage van realtime locatie alleen gebruikt standaard op basis van netwerklocaties.</span><span class="sxs-lookup"><span data-stu-id="1c681-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="1c681-162">tooenable hello gebruik van GPS op basis van locaties (die veel meer nauwkeurige), toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1c681-162">tooenable hello use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="1c681-163">Achtergrond rapportage</span><span class="sxs-lookup"><span data-stu-id="1c681-163">Background reporting</span></span>
<span data-ttu-id="1c681-164">Rapportage van realtime locatie is standaard alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (dat wil zeggen tijdens een sessie).</span><span class="sxs-lookup"><span data-stu-id="1c681-164">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="1c681-165">tooenable hello reporting ook op de achtergrond, toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1c681-165">tooenable hello reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="1c681-166">Wanneer de toepassing hello wordt uitgevoerd op de achtergrond, alleen op basis van netwerklocaties worden gerapporteerd, zelfs als u ingeschakeld Hallo GPS.</span><span class="sxs-lookup"><span data-stu-id="1c681-166">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
>
>

<span data-ttu-id="1c681-167">Implementatie van deze functie moet worden gebeld [startMonitoringSignificantLocationChanges] wanneer uw toepassing probeert het Hallo-achtergrond.</span><span class="sxs-lookup"><span data-stu-id="1c681-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into hello background.</span></span> <span data-ttu-id="1c681-168">Let erop dat deze automatisch opnieuw uw toepassing in de achtergrond Hallo Start wordt als een nieuwe locatie gebeurtenis binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="1c681-168">Be aware that it will automatically relaunch your application into hello background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="1c681-169">Geavanceerde rapportage</span><span class="sxs-lookup"><span data-stu-id="1c681-169">Advanced reporting</span></span>
<span data-ttu-id="1c681-170">Eventueel, als u tooreport toepassing specifieke gebeurtenissen, fouten en taken wilt, moet u toouse Hallo Engagement API via de methoden Hallo Hallo `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="1c681-170">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="1c681-171">Een object van deze klasse kan worden opgehaald door de aanroepende Hallo `[EngagementAgent shared]` statische methode.</span><span class="sxs-lookup"><span data-stu-id="1c681-171">An object of this class can be retrieved by calling hello `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="1c681-172">Hallo Engagement API toouse kunnen alle Engagement geavanceerde mogelijkheden en wordt beschreven in Hallo hoe tooUse de Engagement-API voor iOS (en van de technische documentatie Hallo Hallo `EngagementAgent` klasse).</span><span class="sxs-lookup"><span data-stu-id="1c681-172">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on iOS (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="1c681-173">Uitschakelen van IDFA-verzameling</span><span class="sxs-lookup"><span data-stu-id="1c681-173">Disable IDFA collection</span></span>
<span data-ttu-id="1c681-174">Standaard gebruikt Engagement Hallo [IDFA] toouniquely identificatie van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1c681-174">By default, Engagement will use hello [IDFA] toouniquely identify a user.</span></span> <span data-ttu-id="1c681-175">Maar als u reclame elders in Hallo-app niet gebruikt, kunt u geweigerd door Hallo controleproces App Store.</span><span class="sxs-lookup"><span data-stu-id="1c681-175">But if you’re not using advertising elsewhere in hello app, you might be rejected by hello App Store review process.</span></span> <span data-ttu-id="1c681-176">IDFA-verzameling kan worden uitgeschakeld door toe te voegen Hallo preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in uw pch-bestand (of in Hallo `Build Settings` van uw toepassing).</span><span class="sxs-lookup"><span data-stu-id="1c681-176">IDFA collection can be disabled by adding hello preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in hello `Build Settings` of your application).</span></span> <span data-ttu-id="1c681-177">Dit zorgt ervoor dat er geen verwijzingen te is`ASIdentifierManager`, `advertisingIdentifier` of `isAdvertisingTrackingEnabled` Hallo toepassing gebouwd.</span><span class="sxs-lookup"><span data-stu-id="1c681-177">This will ensure that there is no references too`ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in hello application build.</span></span>

<span data-ttu-id="1c681-178">Integratie in Hallo **prefix.pch** bestand:</span><span class="sxs-lookup"><span data-stu-id="1c681-178">Integration in hello **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="1c681-179">U kunt controleren of Hallo IDFA-verzameling is goed uitgeschakeld in uw toepassing door Hallo Engagement test logboeken controleren.</span><span class="sxs-lookup"><span data-stu-id="1c681-179">You can verify that hello IDFA collection is properly disabled in your application by checking hello Engagement test logs.</span></span> <span data-ttu-id="1c681-180">Zie integratie testen Hallo\<ios-sdk-engagement-test-idfa\> documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1c681-180">See hello Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="1c681-181">Melden van logboek uitschakelen</span><span class="sxs-lookup"><span data-stu-id="1c681-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="1c681-182">Met behulp van een methodeaanroep van</span><span class="sxs-lookup"><span data-stu-id="1c681-182">Using a method call</span></span>
<span data-ttu-id="1c681-183">Als u Engagement toostop logboeken verzenden wilt, kunt u bellen:</span><span class="sxs-lookup"><span data-stu-id="1c681-183">If you want Engagement toostop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="1c681-184">Deze aanroep is permanent: hierbij `NSUserDefaults` toostore Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="1c681-184">This call is persistent: it uses `NSUserDefaults` toostore hello information.</span></span>

<span data-ttu-id="1c681-185">U kunt reporting opnieuw door het aanroepen van dezelfde functie met Hallo logboek inschakelen `YES`.</span><span class="sxs-lookup"><span data-stu-id="1c681-185">You can enable log reporting again by calling hello same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="1c681-186">Integratie in de bundel van uw instellingen</span><span class="sxs-lookup"><span data-stu-id="1c681-186">Integration in your settings bundle</span></span>
<span data-ttu-id="1c681-187">In plaats van deze functie aanroept, kunt u deze instelling ook integreren rechtstreeks in uw bestaande `Settings.bundle` bestand.</span><span class="sxs-lookup"><span data-stu-id="1c681-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="1c681-188">Hallo tekenreeks `engagement_agent_enabled` moet worden gebruikt als een id van de voorkeursextensie Hallo en bijbehorende tooa schakeloptie moet zijn (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="1c681-188">hello string `engagement_agent_enabled` must be used as a hello preference identifier and it must be associated tooa toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="1c681-189">Hallo volgende voorbeeld van `Settings.bundle` ziet u hoe tooimplement het:</span><span class="sxs-lookup"><span data-stu-id="1c681-189">hello following example of `Settings.bundle` shows how tooimplement it:</span></span>

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
