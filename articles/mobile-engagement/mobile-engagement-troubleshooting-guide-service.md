---
title: aaaAzure Mobile Engagement Troubleshooting Guide - Service
description: Troubleshooting Guide voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a>Gids voor probleemoplossing voor problemen met de Service
Hallo volgen mogelijke problemen die optreden bij hoe Azure Mobile Engagement wordt uitgevoerd.

## <a name="service-outages"></a>Serviceonderbrekingen
### <a name="issue"></a>Probleem
* Problemen die worden veroorzaakt door Azure Mobile Engagement serviceonderbrekingen toobe weergegeven.

### <a name="causes"></a>Oorzaken
* Problemen die worden veroorzaakt door Azure Mobile Engagement serviceonderbrekingen toobe weergegeven kunnen zijn veroorzaakt door verschillende andere problemen:
  * Geïsoleerde problemen die oorspronkelijk al tooall van Azure Mobile Engagement weergegeven
  * Bekende problemen veroorzaakt door serverstoringen (die niet altijd wordt weergegeven in de serverstatus):
  * Voor de planning vertragingen, fouten Targeting, problemen Badge-update, statistieken stop verzamelen, werkt niet voor Push kan niet-API's meer werken, nieuwe apps of gebruikers worden gemaakt, DNS-fouten en time-outfouten in Hallo UI of API-Apps op een apparaat.
  * Afhankelijkheid uitval cloud [Azure servicestatus](http://status.azure.com/)
  * Push Notification Services (PNS) afhankelijkheid uitval
  * App Store uitval

1) tootest toosee als Hallo probleem al kunt u dezelfde functie uit een andere Hallo testen

* Azure Mobile Engagement geïntegreerde toepassing
* Testapparaat
* Testversie van het besturingssysteem van het apparaat
* Campagne
* Beheerdersaccount
* Browser (IE, Firefox, Chrome, enz.)
* Computer

2) tootest als Hallo probleem alleen betrekking heeft op Hallo UI of Hallo-API's:

* Test hello dezelfde functioneren van beide hello Azure Mobile Engagement-UI en hello Azure Mobile Engagement-API's.

3) tootest als Hallo probleem met het netwerk van uw mobiele telefoon is:

* Tijdens het verbonden toohello Internet via Wi-Fi en verbonden via het netwerk van de mobiele telefoon 3G testen.
* Controleer of de firewall niet hello Azure Mobile Engagement IP-adressen of poorten blokkeert.

4) tootest als Hallo probleem met uw apparaat is:

* Als het apparaat kunnen tooconnect tooAzure Mobile Engagement met een andere geïntegreerde Azure Mobile Engagement-app testen.
* Test die u kunt gebeurtenissen, taken en Crashes van uw telefoon die kan worden bekeken in hello Azure Mobile Engagement UI genereren. 
* Testen of u pushmeldingen verzenden vanuit hello Azure Mobile Engagement UI tooyour apparaat op basis van de apparaat-ID kunt. 

5) tootest als Hallo probleem met uw App is:

* Installeren en testen van de toepassing van een emulator in plaats van vanaf een fysiek apparaat:

6) tootest als Hallo probleem is met upgrades tooend besturingssysteemgebruiker apparaten waarvoor een upgrade tooresolve SDK:

* Test uw toepassing op verschillende apparaten met verschillende versies van Hallo OS.
* Bevestig dat u van de meest recente versie Hallo Hallo SDK gebruikmaakt.

## <a name="connectivity-and-incorrect-information-issues"></a>Connectiviteit en onjuiste informatie over problemen
### <a name="issue"></a>Probleem
* Problemen met aanmelden bij hello Azure Mobile Engagement-gebruikersinterface.
* Verbindingsfouten Hello Azure Mobile Engagement-API van.
* Problemen met het App-Info labels uploaden via Hallo apparaat-API.
* Problemen bij het downloaden van Logboeken of de geëxporteerde gegevens van Azure Mobile Engagement.
* Onjuiste gegevens in hello Azure Mobile Engagement-gebruikersinterface wordt weergegeven.
* Onjuiste informatie die wordt weergegeven in Azure Mobile Engagement-Logboeken.

### <a name="causes"></a>Oorzaken
* Bevestig dat uw gebruikersaccount heeft onvoldoende machtigingen tooperform Hallo taak.
* Bevestig dat Hallo-probleem is niet geïsoleerd tooone computer of uw lokale netwerk.
* Controleer of deze hello Azure Mobile Engagement-service geen gemelde storingen heeft.
* Bevestig dat uw App-Info label bestanden al deze regels volgen:
  * Gebruik alleen Hallo UTF8-tekenset (Hallo ANSI-tekenset wordt niet ondersteund).
  * Gebruik een komma "," als scheidingsteken hello (u kunt een scheidingsteken van service aanvraag toorequest toochange Hallo CSV openen vanuit een komma "," tooanother teken, zoals een puntkomma ';').
  * Gebruik voor Boole-waarden alle kleine letters 'true' en 'false'.
  * Gebruik een bestand dat kleiner is dan de maximale bestandsgrootte Hallo van 35MB.

