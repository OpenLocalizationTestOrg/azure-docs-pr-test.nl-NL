---
title: Azure Mobile Engagement Troubleshooting Guide - SDK
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
ms.openlocfilehash: 4d9d6165deb4bd0c65f1841aa7c457363a1f2865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="92ff7-103">Gids voor probleemoplossing voor problemen met SDK-integratie</span><span class="sxs-lookup"><span data-stu-id="92ff7-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="92ff7-104">Hieronder vindt u mogelijke problemen die optreden bij hoe Azure Mobile Engagement is geïntegreerd in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="92ff7-104">The following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="92ff7-105">SDK-problemen gedetecteerd door een fout in een ander aspect van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="92ff7-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="92ff7-106">Probleem</span><span class="sxs-lookup"><span data-stu-id="92ff7-106">Issue</span></span>
* <span data-ttu-id="92ff7-107">Gebruikersinterface data collection is mislukt (in Analytics, bewaking, segmentering of Dashboards).</span><span class="sxs-lookup"><span data-stu-id="92ff7-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="92ff7-108">Mislukte push (Pushes werken niet in-app uit de app, of beide).</span><span class="sxs-lookup"><span data-stu-id="92ff7-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="92ff7-109">Geavanceerde functie fouten (bijhouden, Geolocatie of niet op specifieke Pushes werken platform).</span><span class="sxs-lookup"><span data-stu-id="92ff7-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="92ff7-110">API-fouten (API's mislukken vaak zonder interactie en zonder foutberichten).</span><span class="sxs-lookup"><span data-stu-id="92ff7-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="92ff7-111">Servicefouten (geen Azure Mobile Engagement werkt voor uw toepassing).</span><span class="sxs-lookup"><span data-stu-id="92ff7-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="92ff7-112">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="92ff7-112">Causes</span></span>
* <span data-ttu-id="92ff7-113">De meeste problemen die moeten worden opgelost met Azure Mobile Engagement SDK wordt gedetecteerd door een fout in uw toepassing (zoals een verzameling van gebruikersinterface gegevensfout, push-fout, geavanceerde functie mislukt, API-fout, applicatiecrashes of duidelijk servicestoring) .</span><span class="sxs-lookup"><span data-stu-id="92ff7-113">Most issues that need to be resolved with the Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="92ff7-114">Als een bepaalde functie van Azure Mobile Engagement nooit in uw app voordat heeft gewerkt, moet u de integratie worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="92ff7-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need to complete the integration.</span></span> 
* <span data-ttu-id="92ff7-115">Als een bepaalde functie van Azure Mobile Engagement werkte en gestopt, moet u wellicht bijwerken naar de laatste versie met Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="92ff7-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need to upgrade to the last version with the Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="92ff7-116">Vergeet niet dat er een andere versie van Azure Mobile Engagement SDK voor elk platform dat wordt ondersteund door Azure Mobile Engagement (Android, iOS, Windows en Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="92ff7-116">Remember that there is a different version of the Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="92ff7-117">Integratie met SDK</span><span class="sxs-lookup"><span data-stu-id="92ff7-117">SDK Integration</span></span>
* <span data-ttu-id="92ff7-118">Azure Mobile Engagement is niet goed geïntegreerd in de SDK (Analytics).</span><span class="sxs-lookup"><span data-stu-id="92ff7-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="92ff7-119">Bereiken niet goed worden geïntegreerd in de SDK (In-App en buiten App Pushmeldingen).</span><span class="sxs-lookup"><span data-stu-id="92ff7-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="92ff7-120">Het certificaat is verlopen of onjuist PROD vs. Developer (alleen iOS).</span><span class="sxs-lookup"><span data-stu-id="92ff7-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="92ff7-121">GCM of ADM niet goed geïntegreerd in de SDK (Android alleen - Service specifieke Pushes).</span><span class="sxs-lookup"><span data-stu-id="92ff7-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="92ff7-122">Bijhouden niet juist geïntegreerd in de SDK (installatie store bijhouden).</span><span class="sxs-lookup"><span data-stu-id="92ff7-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="92ff7-123">Vertraagde locatie of GPS-locatie niet goed geïntegreerd in de SDK (Targeting door geografische locatie).</span><span class="sxs-lookup"><span data-stu-id="92ff7-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="92ff7-124">**Zie ook:**</span><span class="sxs-lookup"><span data-stu-id="92ff7-124">**See also:**</span></span>

* <span data-ttu-id="92ff7-125">[SDK-documentatie - integratie handleidingen][Link 5]</span><span class="sxs-lookup"><span data-stu-id="92ff7-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="92ff7-126">[Troubleshooting Guide - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="92ff7-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="92ff7-127">SDK-Upgrade</span><span class="sxs-lookup"><span data-stu-id="92ff7-127">SDK Upgrade</span></span>
* <span data-ttu-id="92ff7-128">Moet een upgrade van de SDK voor het oplossen van problemen met oudere versies van de SDK (vaak in verband met nieuwere versies van het besturingssysteem van het apparaat).</span><span class="sxs-lookup"><span data-stu-id="92ff7-128">Need to upgrade SDK to resolve issues with older versions of the SDK (often related to newer versions of the device OS).</span></span>
* <span data-ttu-id="92ff7-129">Alle eerdere versies van uw app op uw apparaat te verwijderen en opnieuw te installeren de nieuwste versie van uw app, het opnieuw registreren van uw apparaat-ID van de Azure Mobile Engagement-gebruikersinterface om te bevestigen dat het apparaat de nieuwste versie van uw app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="92ff7-129">Uninstall all previous versions of your app from your device and reinstall the newest version of your app, the re-register your Device ID from the Azure Mobile Engagement UI to confirm that your device is using the newest version of your app.</span></span>

<span data-ttu-id="92ff7-130">**Zie ook:**</span><span class="sxs-lookup"><span data-stu-id="92ff7-130">**See also:**</span></span>

* [<span data-ttu-id="92ff7-131">SDK-documentatie - Release-opmerkingen</span><span class="sxs-lookup"><span data-stu-id="92ff7-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="92ff7-132">SDK-documentatie - Upgrade handleidingen</span><span class="sxs-lookup"><span data-stu-id="92ff7-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="92ff7-133">Andere SDK</span><span class="sxs-lookup"><span data-stu-id="92ff7-133">SDK Other</span></span>
* <span data-ttu-id="92ff7-134">Fouten in het Manifest 'AndroidManifest.xml' van de toepassing kunnen leiden tot Azure Mobile Engagement niet te werken (alleen Android).</span><span class="sxs-lookup"><span data-stu-id="92ff7-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not to work (Android only).</span></span>
* <span data-ttu-id="92ff7-135">Een veelvoorkomend probleem met de SDK-integratie en het gebruik van de API is gehaald de SDK-sleutel en de API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="92ff7-135">A common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>

<span data-ttu-id="92ff7-136">**Zie ook:**</span><span class="sxs-lookup"><span data-stu-id="92ff7-136">**See also:**</span></span>

* <span data-ttu-id="92ff7-137">[Concepten - verklarende woordenlijst][Link 6]</span><span class="sxs-lookup"><span data-stu-id="92ff7-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="92ff7-138">Geavanceerde problemen coderen</span><span class="sxs-lookup"><span data-stu-id="92ff7-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="92ff7-139">Probleem</span><span class="sxs-lookup"><span data-stu-id="92ff7-139">Issue</span></span>
* <span data-ttu-id="92ff7-140">Specifieke platformcode niet direct gerelateerd aan Azure Mobile Engagement kan problemen veroorzaken op iOS, Android en Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="92ff7-140">Platform specific code not directly related to Azure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="92ff7-141">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="92ff7-141">Causes</span></span>
* <span data-ttu-id="92ff7-142">Vele geavanceerde codering problemen met Azure Mobile Engagement worden veroorzaakt door onjuist geschreven platform-specifieke code niet direct gerelateerd aan Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="92ff7-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related to Azure Mobile Engagement.</span></span> <span data-ttu-id="92ff7-143">U moet de documentatie is specifiek voor het platform dat u voor naast Azure Mobile Engagement-documentatie (Android, iOS, Web, Windows en Windows Phone ontwikkelt).</span><span class="sxs-lookup"><span data-stu-id="92ff7-143">You will need to consult documentation specific to the platform you are developing for in addition to Azure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="92ff7-144">Niet juist configureren 'categorieën', voorkomt u dat koppelen vanuit een melding naar een andere locatie binnen of buiten de app (alleen Android).</span><span class="sxs-lookup"><span data-stu-id="92ff7-144">Not correctly configuring "categories", prevents linking from a notification to another location either inside or outside of the app (Android only).</span></span> 
* <span data-ttu-id="92ff7-145">De instelling 'UIKit.framework' naar 'optioneel' in uw iOS-code bevat een 'Symbool fout niet gevonden' en/of vastloopt op oudere iOS-apparaten (alleen iOS).</span><span class="sxs-lookup"><span data-stu-id="92ff7-145">Not setting "UIKit.framework" to "optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="92ff7-146">Certificaten verlopen of niet goed met de ontwikkeling of Prod-versie van het certificaat, oorzaken push problemen (alleen iOS).</span><span class="sxs-lookup"><span data-stu-id="92ff7-146">Expired certificates or not correctly using the DEV or Prod version of the cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="92ff7-147">Er zijn enkele beperkingen deel uitmaken van een platform waarmee Azure Mobile Engagement niet beheren (zoals hoe de system center werkt voor buiten de app in Android en iOS pushmeldingen).</span><span class="sxs-lookup"><span data-stu-id="92ff7-147">There are some limitations inherent to a platform that Azure Mobile Engagement can't control (like how the system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="92ff7-148">Azure Mobile Engagement publiceert een volledige lijst van de interne pakketten gebruikt door Azure Mobile Engagement voor iOS en Android ter referentie.</span><span class="sxs-lookup"><span data-stu-id="92ff7-148">Azure Mobile Engagement publishes a full list of the internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="92ff7-149">Houd er rekening mee dat sommige functies van Azure Mobile Engagement specifiek voor het platform (Android, iOS, Web, Windows en Windows Phone zijn).</span><span class="sxs-lookup"><span data-stu-id="92ff7-149">Keep in mind that some features of Azure Mobile Engagement are specific to the platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="92ff7-150">Zie ook</span><span class="sxs-lookup"><span data-stu-id="92ff7-150">See also</span></span>
* <span data-ttu-id="92ff7-151">[Troubleshooting Guide - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="92ff7-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="92ff7-152">[SDK-documentatie - Release-opmerkingen][Link 5]</span><span class="sxs-lookup"><span data-stu-id="92ff7-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="92ff7-153">[SDK-documentatie - Upgrade handleidingen][Link 5]</span><span class="sxs-lookup"><span data-stu-id="92ff7-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="92ff7-154">Vastlopen van de toepassing</span><span class="sxs-lookup"><span data-stu-id="92ff7-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="92ff7-155">Probleem</span><span class="sxs-lookup"><span data-stu-id="92ff7-155">Issue</span></span>
* <span data-ttu-id="92ff7-156">Uw toepassing is vastgelopen op apparaat voor de eindgebruikers.</span><span class="sxs-lookup"><span data-stu-id="92ff7-156">Your application crashes on the end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="92ff7-157">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="92ff7-157">Causes</span></span>
* <span data-ttu-id="92ff7-158">Informatie over de crash kan worden weergegeven in de *Analytics UI* of de *Analytics-API*</span><span class="sxs-lookup"><span data-stu-id="92ff7-158">Crash information can be viewed in the *Analytics UI* or the *Analytics API*</span></span>
* <span data-ttu-id="92ff7-159">U kunt de apparaat-ID van uw testapparaat vinden en de dezelfde maatregelen waardoor de toepassing vastloopt voor een eindgebruiker om de oorzaak van de crash te identificeren.</span><span class="sxs-lookup"><span data-stu-id="92ff7-159">You can find the Device ID of your test device and take the same action that caused your application to crash for an end user to help identify the cause of your crash.</span></span>
* <span data-ttu-id="92ff7-160">Bekende problemen met Azure Mobile Engagement SDK die ervoor zorgen dat crashes soms opgelost door te upgraden naar de nieuwste versie van de SDK.</span><span class="sxs-lookup"><span data-stu-id="92ff7-160">Known issues with the Azure Mobile Engagement SDK that cause applications to crash are sometimes resolved by upgrading to the latest version of the SDK.</span></span> <span data-ttu-id="92ff7-161">Zorg ervoor dat de release-opmerkingen over uw platform controleren bij het onderzoeken van crashes.</span><span class="sxs-lookup"><span data-stu-id="92ff7-161">Make sure to check the release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="92ff7-162">Zie ook</span><span class="sxs-lookup"><span data-stu-id="92ff7-162">See also</span></span>
* <span data-ttu-id="92ff7-163">[SDK-documentatie - Release-opmerkingen][Link 5]</span><span class="sxs-lookup"><span data-stu-id="92ff7-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="92ff7-164">[SDK-documentatie - Upgrade handleidingen][Link 5]</span><span class="sxs-lookup"><span data-stu-id="92ff7-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="92ff7-165">Mislukte App store</span><span class="sxs-lookup"><span data-stu-id="92ff7-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="92ff7-166">Probleem</span><span class="sxs-lookup"><span data-stu-id="92ff7-166">Issue</span></span>
* <span data-ttu-id="92ff7-167">Fouten met betrekking tot de nieuwste versie van uw app uploaden naar Apple, Google of de App Windows store.</span><span class="sxs-lookup"><span data-stu-id="92ff7-167">Errors related to uploading the latest version of your app to Apple, Google, or the Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="92ff7-168">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="92ff7-168">Causes</span></span>
* <span data-ttu-id="92ff7-169">App slaat soms blokkeren voor apps met bepaalde functies ingeschakeld (bijvoorbeeld de Apple Store voorkomt dat het gebruik van IDFV in apps in de store en de store GooglePlay voorkomt dat het delen van informatie over de toepassing tussen apps).</span><span class="sxs-lookup"><span data-stu-id="92ff7-169">App stores sometimes block apps with certain features enabled (e.g. the Apple Store prevents the use of IDFV in apps in the store and the GooglePlay store prevents the sharing of application information between apps).</span></span> 
* <span data-ttu-id="92ff7-170">Zorg ervoor dat u de release-opmerkingen over uw platform en de huidige versie van de SDK controleren als u problemen ondervindt bij het uploaden van een app naar de store.</span><span class="sxs-lookup"><span data-stu-id="92ff7-170">Make sure that you check the release notes about your platform and current version of the SDK if you have difficulty uploading an app to the store.</span></span>

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

