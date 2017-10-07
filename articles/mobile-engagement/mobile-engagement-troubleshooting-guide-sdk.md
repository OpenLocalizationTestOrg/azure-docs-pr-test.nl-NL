---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: Het oplossen van problemen van de SDK-integratie in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="37f94-103">Gids voor probleemoplossing voor problemen met SDK-integratie</span><span class="sxs-lookup"><span data-stu-id="37f94-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="37f94-104">Hallo volgen mogelijke problemen die optreden bij hoe Azure Mobile Engagement is geïntegreerd in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="37f94-104">hello following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="37f94-105">SDK-problemen gedetecteerd door een fout in een ander aspect van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="37f94-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="37f94-106">Probleem</span><span class="sxs-lookup"><span data-stu-id="37f94-106">Issue</span></span>
* <span data-ttu-id="37f94-107">Gebruikersinterface data collection is mislukt (in Analytics, bewaking, segmentering of Dashboards).</span><span class="sxs-lookup"><span data-stu-id="37f94-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="37f94-108">Mislukte push (Pushes werken niet in-app uit de app, of beide).</span><span class="sxs-lookup"><span data-stu-id="37f94-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="37f94-109">Geavanceerde functie fouten (bijhouden, Geolocatie of niet op specifieke Pushes werken platform).</span><span class="sxs-lookup"><span data-stu-id="37f94-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="37f94-110">API-fouten (API's mislukken vaak zonder interactie en zonder foutberichten).</span><span class="sxs-lookup"><span data-stu-id="37f94-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="37f94-111">Servicefouten (geen Azure Mobile Engagement werkt voor uw toepassing).</span><span class="sxs-lookup"><span data-stu-id="37f94-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="37f94-112">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="37f94-112">Causes</span></span>
* <span data-ttu-id="37f94-113">De meeste problemen die toobe opgelost met Azure Mobile Engagement SDK Hallo moet worden gedetecteerd door een fout in uw toepassing (zoals een verzameling van gebruikersinterface gegevensfout, push-fout, geavanceerde functie mislukt, API-fout, applicatiecrashes of duidelijk service uitval).</span><span class="sxs-lookup"><span data-stu-id="37f94-113">Most issues that need toobe resolved with hello Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="37f94-114">Als een bepaalde functie van Azure Mobile Engagement nooit in uw app voordat heeft gewerkt, moet u toocomplete Hallo-integratie.</span><span class="sxs-lookup"><span data-stu-id="37f94-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need toocomplete hello integration.</span></span> 
* <span data-ttu-id="37f94-115">Als een bepaalde functie van Azure Mobile Engagement werkte en gestopt, moet u mogelijk tooupgrade toohello laatste versie Hello Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="37f94-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need tooupgrade toohello last version with hello Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="37f94-116">Vergeet niet dat er een andere versie van hello Azure Mobile Engagement SDK voor elk platform dat wordt ondersteund door Azure Mobile Engagement (Android, iOS, Windows en Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="37f94-116">Remember that there is a different version of hello Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="37f94-117">Integratie met SDK</span><span class="sxs-lookup"><span data-stu-id="37f94-117">SDK Integration</span></span>
* <span data-ttu-id="37f94-118">Azure Mobile Engagement is niet goed geïntegreerd in de SDK (Analytics).</span><span class="sxs-lookup"><span data-stu-id="37f94-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="37f94-119">Bereiken niet goed worden geïntegreerd in de SDK (In-App en buiten App Pushmeldingen).</span><span class="sxs-lookup"><span data-stu-id="37f94-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="37f94-120">Het certificaat is verlopen of onjuist PROD vs. Developer (alleen iOS).</span><span class="sxs-lookup"><span data-stu-id="37f94-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="37f94-121">GCM of ADM niet goed geïntegreerd in de SDK (Android alleen - Service specifieke Pushes).</span><span class="sxs-lookup"><span data-stu-id="37f94-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="37f94-122">Bijhouden niet juist geïntegreerd in de SDK (installatie store bijhouden).</span><span class="sxs-lookup"><span data-stu-id="37f94-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="37f94-123">Vertraagde locatie of GPS-locatie niet goed geïntegreerd in de SDK (Targeting door geografische locatie).</span><span class="sxs-lookup"><span data-stu-id="37f94-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="37f94-124">**Zie ook:**</span><span class="sxs-lookup"><span data-stu-id="37f94-124">**See also:**</span></span>

* <span data-ttu-id="37f94-125">[SDK-documentatie - integratie handleidingen][Link 5]</span><span class="sxs-lookup"><span data-stu-id="37f94-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="37f94-126">[Troubleshooting Guide - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="37f94-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="37f94-127">SDK-Upgrade</span><span class="sxs-lookup"><span data-stu-id="37f94-127">SDK Upgrade</span></span>
* <span data-ttu-id="37f94-128">Moet tooupgrade SDK tooresolve problemen met oudere versies van Hallo SDK (vaak gerelateerde toonewer versies van het besturingssysteem van het apparaat Hallo).</span><span class="sxs-lookup"><span data-stu-id="37f94-128">Need tooupgrade SDK tooresolve issues with older versions of hello SDK (often related toonewer versions of hello device OS).</span></span>
* <span data-ttu-id="37f94-129">Verwijder alle vorige versies van uw app op uw apparaat en Hallo nieuwste versie van uw app opnieuw te installeren, Hallo opnieuw uw apparaat-ID van hello Azure Mobile Engagement UI tooconfirm dat uw apparaat van de nieuwste versie Hallo van uw app gebruikmaakt te registreren.</span><span class="sxs-lookup"><span data-stu-id="37f94-129">Uninstall all previous versions of your app from your device and reinstall hello newest version of your app, hello re-register your Device ID from hello Azure Mobile Engagement UI tooconfirm that your device is using hello newest version of your app.</span></span>

<span data-ttu-id="37f94-130">**Zie ook:**</span><span class="sxs-lookup"><span data-stu-id="37f94-130">**See also:**</span></span>

* [<span data-ttu-id="37f94-131">SDK-documentatie - Release-opmerkingen</span><span class="sxs-lookup"><span data-stu-id="37f94-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="37f94-132">SDK-documentatie - Upgrade handleidingen</span><span class="sxs-lookup"><span data-stu-id="37f94-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="37f94-133">Andere SDK</span><span class="sxs-lookup"><span data-stu-id="37f94-133">SDK Other</span></span>
* <span data-ttu-id="37f94-134">Fouten in het Manifest 'AndroidManifest.xml' van de toepassing kunnen leiden tot Azure Mobile Engagement niet toowork (alleen Android).</span><span class="sxs-lookup"><span data-stu-id="37f94-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not toowork (Android only).</span></span>
* <span data-ttu-id="37f94-135">Een veelvoorkomend probleem met de SDK-integratie en het gebruik van de API is tooconfuse Hallo SDK-sleutel en Hallo API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="37f94-135">A common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>

<span data-ttu-id="37f94-136">**Zie ook:**</span><span class="sxs-lookup"><span data-stu-id="37f94-136">**See also:**</span></span>

* <span data-ttu-id="37f94-137">[Concepten - verklarende woordenlijst][Link 6]</span><span class="sxs-lookup"><span data-stu-id="37f94-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="37f94-138">Geavanceerde problemen coderen</span><span class="sxs-lookup"><span data-stu-id="37f94-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="37f94-139">Probleem</span><span class="sxs-lookup"><span data-stu-id="37f94-139">Issue</span></span>
* <span data-ttu-id="37f94-140">Platform-specifieke code niet direct gerelateerd tooAzure die Mobile Engagement problemen voor iOS, Android en veroorzaken kan Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="37f94-140">Platform specific code not directly related tooAzure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="37f94-141">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="37f94-141">Causes</span></span>
* <span data-ttu-id="37f94-142">Vele geavanceerde codering problemen met Azure Mobile Engagement worden veroorzaakt door onjuist geschreven platform specifieke code niet direct gerelateerd zijn tooAzure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="37f94-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related tooAzure Mobile Engagement.</span></span> <span data-ttu-id="37f94-143">U moet tooconsult documentatie specifieke toohello platform die u voor bovendien tooAzure Mobile Engagement documentatie (Android, iOS, Web, Windows en Windows Phone ontwikkelt).</span><span class="sxs-lookup"><span data-stu-id="37f94-143">You will need tooconsult documentation specific toohello platform you are developing for in addition tooAzure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="37f94-144">Niet juist configureren 'categorieën', voorkomt u dat koppelen vanuit een melding tooanother locatie binnen of buiten het Hallo-app (alleen Android).</span><span class="sxs-lookup"><span data-stu-id="37f94-144">Not correctly configuring "categories", prevents linking from a notification tooanother location either inside or outside of hello app (Android only).</span></span> 
* <span data-ttu-id="37f94-145">De instelling 'UIKit.framework' te 'optioneel' in uw iOS-code bevat een 'Symbool fout niet gevonden' en/of vastloopt op oudere iOS-apparaten (alleen iOS).</span><span class="sxs-lookup"><span data-stu-id="37f94-145">Not setting "UIKit.framework" too"optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="37f94-146">Certificaten verlopen of niet goed met Hallo DEV of Prod-versie van het Hallo-certificaat, oorzaken push problemen (alleen iOS).</span><span class="sxs-lookup"><span data-stu-id="37f94-146">Expired certificates or not correctly using hello DEV or Prod version of hello cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="37f94-147">Er zijn enkele beperkingen inherente tooa-platform die Azure Mobile Engagement niet beheren (zoals hoe Hallo system center werkt voor buiten de app in Android en iOS pushmeldingen).</span><span class="sxs-lookup"><span data-stu-id="37f94-147">There are some limitations inherent tooa platform that Azure Mobile Engagement can't control (like how hello system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="37f94-148">Azure Mobile Engagement publiceert een volledige lijst met interne hello-pakketten gebruikt door Azure Mobile Engagement voor iOS en Android ter referentie.</span><span class="sxs-lookup"><span data-stu-id="37f94-148">Azure Mobile Engagement publishes a full list of hello internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="37f94-149">Houd er rekening mee dat sommige functies van Azure Mobile Engagement specifieke toohello platform (Android, iOS, Web, Windows en Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="37f94-149">Keep in mind that some features of Azure Mobile Engagement are specific toohello platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="37f94-150">Zie ook</span><span class="sxs-lookup"><span data-stu-id="37f94-150">See also</span></span>
* <span data-ttu-id="37f94-151">[Troubleshooting Guide - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="37f94-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="37f94-152">[SDK-documentatie - Release-opmerkingen][Link 5]</span><span class="sxs-lookup"><span data-stu-id="37f94-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="37f94-153">[SDK-documentatie - Upgrade handleidingen][Link 5]</span><span class="sxs-lookup"><span data-stu-id="37f94-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="37f94-154">Vastlopen van de toepassing</span><span class="sxs-lookup"><span data-stu-id="37f94-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="37f94-155">Probleem</span><span class="sxs-lookup"><span data-stu-id="37f94-155">Issue</span></span>
* <span data-ttu-id="37f94-156">Uw toepassing is vastgelopen op Hallo eindgebruikers apparaat.</span><span class="sxs-lookup"><span data-stu-id="37f94-156">Your application crashes on hello end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="37f94-157">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="37f94-157">Causes</span></span>
* <span data-ttu-id="37f94-158">Informatie over de crash kan worden weergegeven in Hallo *Analytics UI* of Hallo *Analytics-API*</span><span class="sxs-lookup"><span data-stu-id="37f94-158">Crash information can be viewed in hello *Analytics UI* or hello *Analytics API*</span></span>
* <span data-ttu-id="37f94-159">Vindt u apparaat-ID van uw testapparaat Hallo en nemen Hallo dezelfde actie waardoor uw toepassing toocrash voor een eindgebruiker toohelp Hallo oorzaak van de crash identificeren.</span><span class="sxs-lookup"><span data-stu-id="37f94-159">You can find hello Device ID of your test device and take hello same action that caused your application toocrash for an end user toohelp identify hello cause of your crash.</span></span>
* <span data-ttu-id="37f94-160">Bekende problemen met hello Azure Mobile Engagement SDK die ervoor zorgen toepassingen toocrash dat soms opgelost door het upgraden van de meest recente versie toohello Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="37f94-160">Known issues with hello Azure Mobile Engagement SDK that cause applications toocrash are sometimes resolved by upgrading toohello latest version of hello SDK.</span></span> <span data-ttu-id="37f94-161">Zorg ervoor dat toocheck Hallo release-opmerkingen over uw platform bij het onderzoeken van crashes.</span><span class="sxs-lookup"><span data-stu-id="37f94-161">Make sure toocheck hello release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="37f94-162">Zie ook</span><span class="sxs-lookup"><span data-stu-id="37f94-162">See also</span></span>
* <span data-ttu-id="37f94-163">[SDK-documentatie - Release-opmerkingen][Link 5]</span><span class="sxs-lookup"><span data-stu-id="37f94-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="37f94-164">[SDK-documentatie - Upgrade handleidingen][Link 5]</span><span class="sxs-lookup"><span data-stu-id="37f94-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="37f94-165">Mislukte App store</span><span class="sxs-lookup"><span data-stu-id="37f94-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="37f94-166">Probleem</span><span class="sxs-lookup"><span data-stu-id="37f94-166">Issue</span></span>
* <span data-ttu-id="37f94-167">Fouten gerelateerd toouploading Hallo meest recente versie van uw app tooApple, Google of Hallo Windows-App store.</span><span class="sxs-lookup"><span data-stu-id="37f94-167">Errors related toouploading hello latest version of your app tooApple, Google, or hello Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="37f94-168">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="37f94-168">Causes</span></span>
* <span data-ttu-id="37f94-169">App slaat soms blokkeren voor apps met bepaalde functies ingeschakeld (bijvoorbeeld Hallo Apple Store wordt voorkomen dat Hallo gebruik van IDFV in Hallo store-apps en Hallo GooglePlay store voorkomt dat Hallo delen van informatie over de toepassing tussen apps).</span><span class="sxs-lookup"><span data-stu-id="37f94-169">App stores sometimes block apps with certain features enabled (e.g. hello Apple Store prevents hello use of IDFV in apps in hello store and hello GooglePlay store prevents hello sharing of application information between apps).</span></span> 
* <span data-ttu-id="37f94-170">Zorg ervoor dat u Hallo release-opmerkingen over uw platform en de huidige versie van Hallo SDK controleren als u problemen ondervindt bij het uploaden van een toohello appstore.</span><span class="sxs-lookup"><span data-stu-id="37f94-170">Make sure that you check hello release notes about your platform and current version of hello SDK if you have difficulty uploading an app toohello store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

