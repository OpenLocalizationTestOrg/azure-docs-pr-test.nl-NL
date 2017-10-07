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
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a>Gids voor probleemoplossing voor problemen met SDK-integratie
Hallo volgen mogelijke problemen die optreden bij hoe Azure Mobile Engagement is geïntegreerd in uw toepassing.

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a>SDK-problemen gedetecteerd door een fout in een ander aspect van uw toepassing
### <a name="issue"></a>Probleem
* Gebruikersinterface data collection is mislukt (in Analytics, bewaking, segmentering of Dashboards).
* Mislukte push (Pushes werken niet in-app uit de app, of beide).
* Geavanceerde functie fouten (bijhouden, Geolocatie of niet op specifieke Pushes werken platform).
* API-fouten (API's mislukken vaak zonder interactie en zonder foutberichten).
* Servicefouten (geen Azure Mobile Engagement werkt voor uw toepassing).

### <a name="causes"></a>Oorzaken
* De meeste problemen die toobe opgelost met Azure Mobile Engagement SDK Hallo moet worden gedetecteerd door een fout in uw toepassing (zoals een verzameling van gebruikersinterface gegevensfout, push-fout, geavanceerde functie mislukt, API-fout, applicatiecrashes of duidelijk service uitval).  
* Als een bepaalde functie van Azure Mobile Engagement nooit in uw app voordat heeft gewerkt, moet u toocomplete Hallo-integratie. 
* Als een bepaalde functie van Azure Mobile Engagement werkte en gestopt, moet u mogelijk tooupgrade toohello laatste versie Hello Azure Mobile Engagement SDK. Vergeet niet dat er een andere versie van hello Azure Mobile Engagement SDK voor elk platform dat wordt ondersteund door Azure Mobile Engagement (Android, iOS, Windows en Windows Phone).

#### <a name="sdk-integration"></a>Integratie met SDK
* Azure Mobile Engagement is niet goed geïntegreerd in de SDK (Analytics).
* Bereiken niet goed worden geïntegreerd in de SDK (In-App en buiten App Pushmeldingen).
* Het certificaat is verlopen of onjuist PROD vs. Developer (alleen iOS).
* GCM of ADM niet goed geïntegreerd in de SDK (Android alleen - Service specifieke Pushes).
* Bijhouden niet juist geïntegreerd in de SDK (installatie store bijhouden).
* Vertraagde locatie of GPS-locatie niet goed geïntegreerd in de SDK (Targeting door geografische locatie).

**Zie ook:**

* [SDK-documentatie - integratie handleidingen][Link 5] 
* [Troubleshooting Guide - Push][Link 23]

#### <a name="sdk-upgrade"></a>SDK-Upgrade
* Moet tooupgrade SDK tooresolve problemen met oudere versies van Hallo SDK (vaak gerelateerde toonewer versies van het besturingssysteem van het apparaat Hallo).
* Verwijder alle vorige versies van uw app op uw apparaat en Hallo nieuwste versie van uw app opnieuw te installeren, Hallo opnieuw uw apparaat-ID van hello Azure Mobile Engagement UI tooconfirm dat uw apparaat van de nieuwste versie Hallo van uw app gebruikmaakt te registreren.

**Zie ook:**

* [SDK-documentatie - Release-opmerkingen](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [SDK-documentatie - Upgrade handleidingen](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a>Andere SDK
* Fouten in het Manifest 'AndroidManifest.xml' van de toepassing kunnen leiden tot Azure Mobile Engagement niet toowork (alleen Android).
* Een veelvoorkomend probleem met de SDK-integratie en het gebruik van de API is tooconfuse Hallo SDK-sleutel en Hallo API-sleutel.

**Zie ook:**

* [Concepten - verklarende woordenlijst][Link 6]

## <a name="advanced-coding-issues"></a>Geavanceerde problemen coderen
### <a name="issue"></a>Probleem
* Platform-specifieke code niet direct gerelateerd tooAzure die Mobile Engagement problemen voor iOS, Android en veroorzaken kan Windows Phone.

### <a name="causes"></a>Oorzaken
* Vele geavanceerde codering problemen met Azure Mobile Engagement worden veroorzaakt door onjuist geschreven platform specifieke code niet direct gerelateerd zijn tooAzure Mobile Engagement. U moet tooconsult documentatie specifieke toohello platform die u voor bovendien tooAzure Mobile Engagement documentatie (Android, iOS, Web, Windows en Windows Phone ontwikkelt).
* Niet juist configureren 'categorieën', voorkomt u dat koppelen vanuit een melding tooanother locatie binnen of buiten het Hallo-app (alleen Android). 
* De instelling 'UIKit.framework' te 'optioneel' in uw iOS-code bevat een 'Symbool fout niet gevonden' en/of vastloopt op oudere iOS-apparaten (alleen iOS).
* Certificaten verlopen of niet goed met Hallo DEV of Prod-versie van het Hallo-certificaat, oorzaken push problemen (alleen iOS).
* Er zijn enkele beperkingen inherente tooa-platform die Azure Mobile Engagement niet beheren (zoals hoe Hallo system center werkt voor buiten de app in Android en iOS pushmeldingen).
* Azure Mobile Engagement publiceert een volledige lijst met interne hello-pakketten gebruikt door Azure Mobile Engagement voor iOS en Android ter referentie. Houd er rekening mee dat sommige functies van Azure Mobile Engagement specifieke toohello platform (Android, iOS, Web, Windows en Windows Phone).

### <a name="see-also"></a>Zie ook
* [Troubleshooting Guide - Push][Link 23] 
* [SDK-documentatie - Release-opmerkingen][Link 5]
* [SDK-documentatie - Upgrade handleidingen][Link 5]

## <a name="application-crashes"></a>Vastlopen van de toepassing
### <a name="issue"></a>Probleem
* Uw toepassing is vastgelopen op Hallo eindgebruikers apparaat.

### <a name="causes"></a>Oorzaken
* Informatie over de crash kan worden weergegeven in Hallo *Analytics UI* of Hallo *Analytics-API*
* Vindt u apparaat-ID van uw testapparaat Hallo en nemen Hallo dezelfde actie waardoor uw toepassing toocrash voor een eindgebruiker toohelp Hallo oorzaak van de crash identificeren.
* Bekende problemen met hello Azure Mobile Engagement SDK die ervoor zorgen toepassingen toocrash dat soms opgelost door het upgraden van de meest recente versie toohello Hallo SDK. Zorg ervoor dat toocheck Hallo release-opmerkingen over uw platform bij het onderzoeken van crashes.

### <a name="see-also"></a>Zie ook
* [SDK-documentatie - Release-opmerkingen][Link 5]
* [SDK-documentatie - Upgrade handleidingen][Link 5]

## <a name="app-store-upload-failures"></a>Mislukte App store
### <a name="issue"></a>Probleem
* Fouten gerelateerd toouploading Hallo meest recente versie van uw app tooApple, Google of Hallo Windows-App store.

### <a name="causes"></a>Oorzaken
* App slaat soms blokkeren voor apps met bepaalde functies ingeschakeld (bijvoorbeeld Hallo Apple Store wordt voorkomen dat Hallo gebruik van IDFV in Hallo store-apps en Hallo GooglePlay store voorkomt dat Hallo delen van informatie over de toepassing tussen apps). 
* Zorg ervoor dat u Hallo release-opmerkingen over uw platform en de huidige versie van Hallo SDK controleren als u problemen ondervindt bij het uploaden van een toohello appstore.

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

