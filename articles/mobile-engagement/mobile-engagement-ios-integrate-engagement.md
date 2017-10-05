---
title: Azure Mobile Engagement iOS SDK-integratie | Microsoft Docs
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
ms.openlocfilehash: 01fdbb43c21ac6932e8462f4a6507fc63e50542d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-on-ios"></a><span data-ttu-id="c1312-103">Hoe integreren Engagement voor iOS</span><span class="sxs-lookup"><span data-stu-id="c1312-103">How to Integrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1312-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="c1312-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="c1312-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="c1312-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="c1312-106">iOS</span><span class="sxs-lookup"><span data-stu-id="c1312-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="c1312-107">Android</span><span class="sxs-lookup"><span data-stu-id="c1312-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="c1312-108">Deze procedure beschrijft de eenvoudigste manier Engagement Analytics en bewaking van functies in uw iOS-toepassing te activeren.</span><span class="sxs-lookup"><span data-stu-id="c1312-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="c1312-109">De Engagement SDK vereist iOS7 + en Xcode 8 +: het implementatiedoel van uw toepassing moet ten minste iOS 7.</span><span class="sxs-lookup"><span data-stu-id="c1312-109">The Engagement SDK requires iOS7+ and Xcode 8+: the deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="c1312-110">Als u echt afhankelijk van XCode 7 zijn en u kunt de [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="c1312-110">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="c1312-111">Er is een bekend probleem in de vorige versie van de Reach-module tijdens het uitvoeren van de iOS-10-apparaten Zie [de reach-module integratie](mobile-engagement-ios-integrate-engagement-reach.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1312-111">There is a known bug on the Reach module of this previous version while running on iOS 10 devices see [the reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="c1312-112">Als u kiest voor het gebruik van de SDK-v3.2.4 en maar overslaan de `UserNotifications.framework` importeren in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="c1312-112">If you choose to use the SDK v3.2.4 then just skip the `UserNotifications.framework` import in the next step.</span></span>
>
>

<span data-ttu-id="c1312-113">De volgende stappen zijn voldoende is voor het activeren van het rapport van logboeken die nodig zijn voor alle statistische gegevens over gebruikers, sessies, activiteiten, Crashes en Technicals berekenen.</span><span class="sxs-lookup"><span data-stu-id="c1312-113">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="c1312-114">Het rapport van logboeken die nodig zijn voor het berekenen van andere statistieken zoals gebeurtenissen, fouten en taken worden uitgevoerd handmatig met behulp van de Engagement-API (Zie [hoe u de geavanceerde Mobile Engagement API in uw iOS-app-tagging](mobile-engagement-ios-use-engagement-api.md) aangezien deze statistieken afhankelijk van de toepassing zijn.</span><span class="sxs-lookup"><span data-stu-id="c1312-114">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API  (see [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="c1312-115">De SDK Engagement insluiten in uw iOS-project</span><span class="sxs-lookup"><span data-stu-id="c1312-115">Embed the Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="c1312-116">De iOS SDK downloaden van [hier](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="c1312-116">Download the iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="c1312-117">De Engagement-SDK toevoegen aan uw iOS-project: in Xcode, klik met de rechtermuisknop op uw project en selecteer **'Add files to...'** en kies de `EngagementSDK` map.</span><span class="sxs-lookup"><span data-stu-id="c1312-117">Add the Engagement SDK to your iOS project: in Xcode, right click on your project and select **"Add files to ..."** and choose the `EngagementSDK` folder.</span></span>
* <span data-ttu-id="c1312-118">Engagement vereist aanvullende frameworks werkt: in de Projectverkenner, opent u het deelvenster van uw project en selecteer het juiste doel.</span><span class="sxs-lookup"><span data-stu-id="c1312-118">Engagement requires additional frameworks to work: in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="c1312-119">Open vervolgens de **'Buildfasen'** tabblad en in de **'Link Binary With Libraries'** menu deze frameworks toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c1312-119">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="c1312-120">`UserNotifications.framework`-de koppeling als instellen`Optional`</span><span class="sxs-lookup"><span data-stu-id="c1312-120">`UserNotifications.framework` - set the link as `Optional`</span></span>
  * <span data-ttu-id="c1312-121">`AdSupport.framework`-de koppeling als instellen`Optional`</span><span class="sxs-lookup"><span data-stu-id="c1312-121">`AdSupport.framework` - set the link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="c1312-122">Het framework AdSupport kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c1312-122">The AdSupport framework can be removed.</span></span> <span data-ttu-id="c1312-123">Engagement moet dit framework voor het verzamelen van de IDFA.</span><span class="sxs-lookup"><span data-stu-id="c1312-123">Engagement needs this framework to collect the IDFA.</span></span> <span data-ttu-id="c1312-124">Echter, IDFA-verzameling kan worden uitgeschakeld \<ios sdk-engagement idfa\> om te voldoen aan het nieuwe Apple-beleid met betrekking tot deze ID.</span><span class="sxs-lookup"><span data-stu-id="c1312-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> to comply with the new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="c1312-125">Initialiseren van de Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="c1312-125">Initialize the Engagement SDK</span></span>
<span data-ttu-id="c1312-126">U moet uw Toepassingsgemachtigde wijzigen:</span><span class="sxs-lookup"><span data-stu-id="c1312-126">You need to modify your Application Delegate:</span></span>

* <span data-ttu-id="c1312-127">Importeer de Engagement-agent aan de bovenkant van het implementatiebestand van uw:</span><span class="sxs-lookup"><span data-stu-id="c1312-127">At the top of your implementation file, import the Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="c1312-128">Engagement te initialiseren in de methode '**applicationDidFinishLaunching:**'of'**toepassing: didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="c1312-128">Initialize Engagement inside the method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="c1312-129">Basic-rapportage</span><span class="sxs-lookup"><span data-stu-id="c1312-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="c1312-130">Aanbevolen methode: overbelasting uw `UIViewController` klassen</span><span class="sxs-lookup"><span data-stu-id="c1312-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="c1312-131">Om het rapport van de logboeken die zijn vereist voor Engagement berekenen gebruikers, sessies, activiteiten, Crashes en technische statistieken activeert, kunt u gewoon aanbrengen alle uw `UIViewController` onderliggende klassen overnemen van de `EngagementViewController` klassen (dezelfde regel voor `UITableViewController`  - \> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="c1312-131">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from the `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="c1312-132">**Zonder Engagement:**</span><span class="sxs-lookup"><span data-stu-id="c1312-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="c1312-133">**Met Engagement:**</span><span class="sxs-lookup"><span data-stu-id="c1312-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="c1312-134">Alternatieve methode: call `startActivity()` handmatig</span><span class="sxs-lookup"><span data-stu-id="c1312-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="c1312-135">Als u niet kunt of niet wilt overbelasten uw `UIViewController` klassen, in plaats daarvan kunt u uw activiteiten starten door het aanroepen van `EngagementAgent`van methoden rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="c1312-135">If you cannot or do not want to overload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1312-136">Het bestand iOS SDK automatisch roept de `endActivity()` methode wanneer de toepassing wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="c1312-136">The iOS SDK automatically calls the `endActivity()` method when the application is closed.</span></span> <span data-ttu-id="c1312-137">Het is dus *maximaal* aanbevolen om aan te roepen de `startActivity` methode wanneer de activiteit van de gebruiker wijzigt, en zo de *nooit* aanroepen de `endActivity` methode, aangezien u deze methode aanroept zorgt ervoor dat de huidige sessie moet worden beëindigd.</span><span class="sxs-lookup"><span data-stu-id="c1312-137">Thus, it is *HIGHLY* recommended to call the `startActivity` method whenever the activity of the user change, and to *NEVER* call the `endActivity` method, since calling this method forces the current session to be ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="c1312-138">Locatierapportage</span><span class="sxs-lookup"><span data-stu-id="c1312-138">Location reporting</span></span>
<span data-ttu-id="c1312-139">Toepassingen kunnen gebruikmaken van locatie bijhouden voor statistische doeleinden alleen toegestaan Apple gebruiksrechtovereenkomst niet.</span><span class="sxs-lookup"><span data-stu-id="c1312-139">Apple terms of service do not allow applications to use location tracking for statistics purpose only.</span></span> <span data-ttu-id="c1312-140">Het verdient dus locatie-rapporten alleen inschakelen als uw toepassingen ook gebruikmaken van de locatie voor een andere reden bijhouden.</span><span class="sxs-lookup"><span data-stu-id="c1312-140">Thus, it is recommended to enable location reports only if your application also use the location tracking for another reason.</span></span>

<span data-ttu-id="c1312-141">Beginnen met iOS 8, moet u een beschrijving van hoe uw app gebruikmaakt van locatie-services door in te stellen van een tekenreeks op voor de sleutel opgeven [NSLocationWhenInUseUsageDescription] of [NSLocationAlwaysUsageDescription] in uw app Info.plist-bestand.</span><span class="sxs-lookup"><span data-stu-id="c1312-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for the key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="c1312-142">Als u de Rapportlocatie van het op de achtergrond met Engagement wilt, kunt u de sleutel NSLocationAlwaysUsageDescription toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c1312-142">If you want to report location in the background with Engagement, add the key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="c1312-143">In andere gevallen moet u de sleutel NSLocationWhenInUseUsageDescription toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c1312-143">In all other cases, add the key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="c1312-144">Houd er rekening mee dat u zowel NSLocationAlwaysAndWhenInUseUsageDescription als NSLocationWhenInUseUsageDescription rapport achtergrond locatie op iOS 11 moet.</span><span class="sxs-lookup"><span data-stu-id="c1312-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription to report background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="c1312-145">Vertraagde locatiemelding</span><span class="sxs-lookup"><span data-stu-id="c1312-145">Lazy area location reporting</span></span>
<span data-ttu-id="c1312-146">Vertraagde locatiemelding kunt voor het rapporteren van het land, streek en plaats die is gekoppeld aan apparaten.</span><span class="sxs-lookup"><span data-stu-id="c1312-146">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="c1312-147">Dit type locatie reporting maakt alleen gebruik van netwerklocaties (gebaseerd op de cel-ID of Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="c1312-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="c1312-148">Het gebied van het apparaat wordt maximaal eenmaal per sessie gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="c1312-148">The device area is reported at most once per session.</span></span> <span data-ttu-id="c1312-149">De GPS wordt nooit gebruikt en dit type locatie rapport heeft slechts weinig (en niet naar Nee zeggen) dus impact op de accu.</span><span class="sxs-lookup"><span data-stu-id="c1312-149">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="c1312-150">Gerapporteerde gebieden worden gebruikt voor het berekenen van geografische statistieken over gebruikers, sessies, gebeurtenissen en fouten.</span><span class="sxs-lookup"><span data-stu-id="c1312-150">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="c1312-151">Ze kunnen ook worden gebruikt als criterium in Reach-campagnes.</span><span class="sxs-lookup"><span data-stu-id="c1312-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="c1312-152">De laatste bekende area gerapporteerd voor een apparaat kan worden opgehaald dank aan de [apparaat-API].</span><span class="sxs-lookup"><span data-stu-id="c1312-152">The last known area reported for a device can be retrieved thanks to the [Device API].</span></span>

<span data-ttu-id="c1312-153">Voeg de volgende regel na tijdens de initialisatie van de agent Engagement zodat vertraagde locatiemelding:</span><span class="sxs-lookup"><span data-stu-id="c1312-153">To enable lazy area location reporting, add the following line after initializing the Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="c1312-154">Rapportage van realtime locatie</span><span class="sxs-lookup"><span data-stu-id="c1312-154">Real time location reporting</span></span>
<span data-ttu-id="c1312-155">Rapportage van realtime locatie kunt voor het rapporteren van de breedtegraad en lengtegraad die is gekoppeld aan apparaten.</span><span class="sxs-lookup"><span data-stu-id="c1312-155">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="c1312-156">Standaard alleen gebruik van dit type locatie reporting netwerklocaties (gebaseerd op de cel-ID of Wi-Fi), en de rapportage is alleen beschikbaar wanneer de toepassing wordt uitgevoerd in de voorgrond (dat wil zeggen tijdens een sessie).</span><span class="sxs-lookup"><span data-stu-id="c1312-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="c1312-157">Realtime-locaties zijn *niet* om te berekenen van statistieken.</span><span class="sxs-lookup"><span data-stu-id="c1312-157">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="c1312-158">Hun enige doel is dat het gebruik van realtime geofencing \<Reach-doelgroep-geofencing\> criterium in Reach-campagnes.</span><span class="sxs-lookup"><span data-stu-id="c1312-158">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="c1312-159">Voeg de volgende regel na tijdens de initialisatie van de agent Engagement zodat rapportage van realtime locatie:</span><span class="sxs-lookup"><span data-stu-id="c1312-159">To enable real time location reporting, add the following line after initializing the Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="c1312-160">GPS op basis van rapportage</span><span class="sxs-lookup"><span data-stu-id="c1312-160">GPS based reporting</span></span>
<span data-ttu-id="c1312-161">Rapportage van realtime locatie alleen gebruikt standaard op basis van netwerklocaties.</span><span class="sxs-lookup"><span data-stu-id="c1312-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="c1312-162">Als u wilt het gebruik van een GPS inschakelen op basis van locaties (die veel meer nauwkeurige), toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c1312-162">To enable the use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="c1312-163">Achtergrond rapportage</span><span class="sxs-lookup"><span data-stu-id="c1312-163">Background reporting</span></span>
<span data-ttu-id="c1312-164">Rapportage van realtime locatie is standaard alleen actief wanneer de toepassing wordt uitgevoerd in de voorgrond (dat wil zeggen tijdens een sessie).</span><span class="sxs-lookup"><span data-stu-id="c1312-164">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="c1312-165">Schakel de rapportage ook op de achtergrond door toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c1312-165">To enable the reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="c1312-166">Wanneer de toepassing op de achtergrond, wordt alleen uitgevoerd op het netwerk locaties worden gerapporteerd, zelfs als u de GPS ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c1312-166">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
>
>

<span data-ttu-id="c1312-167">Implementatie van deze functie moet worden gebeld [startMonitoringSignificantLocationChanges] wanneer uw toepassing gaat in de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="c1312-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into the background.</span></span> <span data-ttu-id="c1312-168">Let erop dat deze automatisch opnieuw uw toepassing in de achtergrond Start wordt als een nieuwe locatie gebeurtenis binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="c1312-168">Be aware that it will automatically relaunch your application into the background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="c1312-169">Geavanceerde rapportage</span><span class="sxs-lookup"><span data-stu-id="c1312-169">Advanced reporting</span></span>
<span data-ttu-id="c1312-170">Eventueel, als u rapporteren toepassing specifieke gebeurtenissen, fouten en taken wilt, moet u de Engagement-API gebruiken via de methoden van de `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="c1312-170">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="c1312-171">Een object van deze klasse kan worden opgehaald door het aanroepen van de `[EngagementAgent shared]` statische methode.</span><span class="sxs-lookup"><span data-stu-id="c1312-171">An object of this class can be retrieved by calling the `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="c1312-172">De Engagement-API kunt u alle Engagement geavanceerde mogelijkheden gebruiken en wordt beschreven in de manier waarop de Engagement-API gebruiken voor iOS (en van de technische documentatie over de `EngagementAgent` klasse).</span><span class="sxs-lookup"><span data-stu-id="c1312-172">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on iOS (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="c1312-173">Uitschakelen van IDFA-verzameling</span><span class="sxs-lookup"><span data-stu-id="c1312-173">Disable IDFA collection</span></span>
<span data-ttu-id="c1312-174">Standaard Engagement gebruikt de [IDFA] voor het aanduiden van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c1312-174">By default, Engagement will use the [IDFA] to uniquely identify a user.</span></span> <span data-ttu-id="c1312-175">Maar als u reclame elders in de app niet gebruikt, kunt u geweigerd door het controleproces App Store.</span><span class="sxs-lookup"><span data-stu-id="c1312-175">But if you’re not using advertising elsewhere in the app, you might be rejected by the App Store review process.</span></span> <span data-ttu-id="c1312-176">IDFA-verzameling kan worden uitgeschakeld door het toevoegen van de preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in uw pch-bestand (of in de `Build Settings` van uw toepassing).</span><span class="sxs-lookup"><span data-stu-id="c1312-176">IDFA collection can be disabled by adding the preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in the `Build Settings` of your application).</span></span> <span data-ttu-id="c1312-177">Dit zorgt ervoor dat er geen verwijzingen naar is `ASIdentifierManager`, `advertisingIdentifier` of `isAdvertisingTrackingEnabled` bij het opbouwen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1312-177">This will ensure that there is no references to `ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in the application build.</span></span>

<span data-ttu-id="c1312-178">Integratie in de **prefix.pch** bestand:</span><span class="sxs-lookup"><span data-stu-id="c1312-178">Integration in the **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="c1312-179">U kunt controleren of de IDFA-verzameling is goed uitgeschakeld in uw toepassing door het controleren van de logboeken van de Engagement-test.</span><span class="sxs-lookup"><span data-stu-id="c1312-179">You can verify that the IDFA collection is properly disabled in your application by checking the Engagement test logs.</span></span> <span data-ttu-id="c1312-180">Zie de integratie testen\<ios-sdk-engagement-test-idfa\> documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1312-180">See the Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="c1312-181">Melden van logboek uitschakelen</span><span class="sxs-lookup"><span data-stu-id="c1312-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="c1312-182">Met behulp van een methodeaanroep van</span><span class="sxs-lookup"><span data-stu-id="c1312-182">Using a method call</span></span>
<span data-ttu-id="c1312-183">Als u stoppen met het verzenden van Logboeken Engagement wilt, kunt u bellen:</span><span class="sxs-lookup"><span data-stu-id="c1312-183">If you want Engagement to stop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="c1312-184">Deze aanroep is permanent: hierbij `NSUserDefaults` de gegevens op te slaan.</span><span class="sxs-lookup"><span data-stu-id="c1312-184">This call is persistent: it uses `NSUserDefaults` to store the information.</span></span>

<span data-ttu-id="c1312-185">U kunt reporting opnieuw door het aanroepen van dezelfde functie met logboek inschakelen `YES`.</span><span class="sxs-lookup"><span data-stu-id="c1312-185">You can enable log reporting again by calling the same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="c1312-186">Integratie in de bundel van uw instellingen</span><span class="sxs-lookup"><span data-stu-id="c1312-186">Integration in your settings bundle</span></span>
<span data-ttu-id="c1312-187">In plaats van deze functie aanroept, kunt u deze instelling ook integreren rechtstreeks in uw bestaande `Settings.bundle` bestand.</span><span class="sxs-lookup"><span data-stu-id="c1312-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="c1312-188">De tekenreeks `engagement_agent_enabled` moeten worden gebruikt als een de voorkeur-id en het moeten zijn gekoppeld aan een schakeloptie (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="c1312-188">The string `engagement_agent_enabled` must be used as a the preference identifier and it must be associated to a toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="c1312-189">Het volgende voorbeeld van `Settings.bundle` ziet u hoe u deze implementeert:</span><span class="sxs-lookup"><span data-stu-id="c1312-189">The following example of `Settings.bundle` shows how to implement it:</span></span>

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
<span data-ttu-id="c1312-190">[apparaat-API]: http://go.microsoft.com/?linkid=9876094</span><span class="sxs-lookup"><span data-stu-id="c1312-190">[Device API]: http://go.microsoft.com/?linkid=9876094</span></span>
<span data-ttu-id="c1312-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span><span class="sxs-lookup"><span data-stu-id="c1312-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span></span>
<span data-ttu-id="c1312-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span><span class="sxs-lookup"><span data-stu-id="c1312-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span></span>
<span data-ttu-id="c1312-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span><span class="sxs-lookup"><span data-stu-id="c1312-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span></span>
<span data-ttu-id="c1312-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span><span class="sxs-lookup"><span data-stu-id="c1312-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span></span>
