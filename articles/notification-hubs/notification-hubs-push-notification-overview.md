---
title: aaaAzure Notification Hubs
description: Meer informatie over hoe tooadd push-melding mogelijkheden met Azure Notification Hubs.
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: 
ms.assetid: fcfb0ce8-0e19-4fa8-b777-6b9f9cdda178
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 1/17/2017
ms.author: yuaxu
ms.openlocfilehash: 78ce34b6b094b560c8002ab9652f7ba4563c5c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs"></a>Azure Notification Hubs
## <a name="overview"></a>Overzicht
Azure Notification Hubs bieden een eenvoudig te gebruiken, meerdere platforms, uitgebreid push-engine. Met een enkel platformoverschrijdende API-aanroep kunt u eenvoudig gerichte en gepersonaliseerde push notifications tooany mobiel platform verzenden vanaf elke cloud of on-premises back-end.

Notification Hubs werkt prima voor enterprise- als consumentenscenario's. Hier volgen enkele voorbeelden klanten Notification Hubs voor gebruiken:

* Belangrijk nieuws meldingen toomillions verzenden met een lage latentie.
* Locatie gebaseerde coupons toointerested gebruikerssegmenten verzenden.
* Gebeurtenis-gerelateerde meldingen toousers of groepen voor media/Sport/Financiën/games verzenden.
* Push-aanbiedingen inhoud tooapps tooengage en het marktaandeel toocustomers.
* Waarschuw gebruikers van bedrijfsgebeurtenissen zoals nieuwe berichten en werkitems.
* Codes voor multi-factor authentication verzenden.

## <a name="what-are-push-notifications"></a>Wat zijn pushmeldingen?
Pushmeldingen is een vorm van app-naar-gebruiker communicatie waar gebruikers van mobiele apps bepaalde gewenste gegevens, meestal in een pop-upvenster of dialoogvenster worden gewaarschuwd. Gebruikers kunnen doorgaans tooview kiezen of het Hallo-bericht negeren en Hallo mobiele Apps die waren uitgewisseld Hallo melding Hallo voormalige kiezen wordt geopend.

Pushmeldingen is essentieel voor consumenten-apps in oplopende betrokkenheid van Apps en het gebruik en voor zakelijke apps bij het communiceren up-to-date bedrijfsgegevens. Hallo aanbevolen app aan gebruiker communicatie is omdat het energie-efficiënte voor mobiele apparaten, flexibele voor Hallo meldingen afzenders en beschikbaar is terwijl de overeenkomstige apps zijn niet actief.

Voor meer informatie over pushmeldingen voor enkele populaire platforms:
* [iOS](https://developer.apple.com/notifications/)
* [Android](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [Windows](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a>Hoe werken pushmeldingen?
Pushmeldingen worden geleverd via een platformspecifieke infrastructuur, het zogenaamde *Platformmeldingssystemen* (PNSes). Ze bieden barebone push functionaliteiten toodelivery bericht tooa apparaat met een opgegeven verwerken en hebben geen algemene interface. een melding toosend tooall klanten over Hallo iOS, Android en Windows versies van een app Hallo ontwikkelaar moet werken met APNS (Apple Push Notification Service), FCM (Firebase Cloud Messaging) en WNS (Windows Notification Service) tijdens de batchverwerking Hallo verzendt.

Op hoog niveau, moet u dit is de werking van push:

1. Hallo client-app kunt u besluit dat deze wil tooreceive pushes daarom contactpersonen Hallo PNS tooretrieve overeenkomt bijbehorende unieke en tijdelijke push-ingang. Hallo ingangstype is afhankelijk van Hallo-systeem (bijvoorbeeld WNS heeft URI's terwijl APNS tokens heeft).
2. Hallo-clientapp slaat deze ingang op in de back-end Hallo app of de provider.
3. toosend een push-melding, back-end Hallo app contactpersonen Hallo PNS Hallo ingang tootarget met een specifieke client-app.
4. Hallo PNS stuurt Hallo toohello meldingsapparaten door Hallo-ingang is opgegeven.

![][0]

## <a name="hello-challenges-of-push-notifications"></a>Hallo uitdagingen van Pushmeldingen
Hoewel PNSes krachtige, laat ze veel werk toohello app-ontwikkelaar in volgorde tooimplement zelfs algemene push notification scenario's, zoals het uitzenden of verzenden van pushmeldingen meldingen toosegmented gebruikers.

Push is een van de Hallo meest stellen aangevraagde functies in mobiele cloudservices, omdat de werking complexe infrastructuur die van niet-verwante toohello app zakelijke logica zijn vereist. Enkele van Hallo infrastructurele uitdagingen zijn:

* **Platformafhankelijkheid**: 

  * Hallo back-end moet toohave complex en moeilijk te onderhouden platformafhankelijk logica toosend meldingen toodevices op verschillende platformen, zoals PNSes zijn geen unified.
* **Schaal**:

  * Per PNS-richtlijnen moeten de apparaattokens bij elke starten van de app worden vernieuwd. Dit betekent Hallo back-end is omgaan met een grote hoeveelheid verkeer en database toegang alleen tookeep Hallo tokens up-to-date. Wanneer het aantal apparaten Hallo toohundreds en miljarden groeit, is Hallo kosten van het maken en onderhouden van deze infrastructuur enorme.
  * De meeste PNSes bieden geen ondersteuning voor uitzending toomultiple apparaten. Dit betekent dat een eenvoudig broadcast tooa miljoenen apparaten leidt tot een miljoen aanroepen toohello PNSes. Deze hoeveelheid verkeer schalen met een minimale latentie is zeer lastig.
* **Routering**:
  
  * Hoewel PNSes een manier toosend berichten toodevices bieden, worden de meeste apps meldingen gericht op gebruikers of belangengroepen. Dit betekent dat Hallo back-end moet ervoor zorgen dat een register tooassociate-apparaten met belangengroepen, gebruikers, eigenschappen, enzovoort. Deze overhead toevoegen toohello tijd toomarket onderhoudskosten en een app

## <a name="why-use-notification-hubs"></a>Waarom werken met Notification Hubs?
Notification Hubs elimineert alle complexiteit die zijn gekoppeld aan het inschakelen van push op uw eigen. De infrastructuur van meerdere platforms, uitgebreid push notification minder push-gerelateerde codes en vereenvoudigt uw back-end. Apparaten zijn alleen verantwoordelijk voor het registreren van hun PNS-ingangen met een hub, terwijl het Hallo-back-end verzendt berichten toousers of belangengroepen, zoals wordt weergegeven in de volgende afbeelding Hallo met Notification Hubs:

![][1]

Notification hubs is uw kant-en-klare push-engine met Hallo volgende voordelen:

* **Cross-platforms**

  * Ondersteuning voor alle primaire push-platforms, waaronder iOS, Android, Windows, en Kindle en Baidu.
  * Een algemene interface toopush tooall platforms in platformspecifieke of platformonafhankelijk indelingen met geen platform-specifieke werk.
  * Apparaat verwerken op één plek.
* **Cross-back-ends**
  
  * Cloud of on-premises
  * .NET, Node.js, Java, enzovoort.
* **Groot aantal afleveringswijzen**:

  * *Uitzenden tooone of meerdere platforms*: U kunt direct toomillions van apparaten op platforms met één API-aanroep uitzenden.
  * *Push toodevice*: U kunt meldingen tooindividual apparaten richten.
  * *Push toouser*: functies Tags en sjablonen kunt u alle apparaten van een gebruiker die meerdere platforms.
  * *Push-toosegment met dynamische labels*: functie labels kunt u apparaten segmenteren en push toothem tooyour behoeften, volgens of van tooone segment of een expressie van segmenten (bijvoorbeeld active en leven in Seattle niet voor de nieuwe gebruiker verzenden). In plaats van alleen beperkte toopub-sub, kunt u bijwerken apparaat labels overal en altijd en overal.
  * *Gelokaliseerde push*: sjablonen functie helpt u bij het bereiken van lokalisatie zonder back endcode.
  * *Achtergrond push*: U kunt Hallo push-pull-patroon door toodevices achtergrond meldingen verzenden en activering van toocomplete kunnen bepaalde worden of acties.
  * *Geplande push*: U kunt op elk gewenst moment toosend meldingen plannen.
  * *Direct push*: U kunt registreren apparaten met onze service en rechtstreeks batch push tooa lijst met apparaten ingangen overslaan.
  * *Persoonlijke push*: apparaat push variabelen helpt bij het verzenden van apparaat-specifieke persoonlijke pushmeldingen met aangepaste sleutel / waarde-paren.
* **Uitgebreide telemetrie**
  
  * Algemene push, apparaat, fout en bewerking telemetrie is beschikbaar in hello Azure-portal en programmatisch.
  * Per bericht telemetrie houdt implementeert elke push van uw eerste aanvraag-aanroep tooour service is batchverwerking Hallo.
  * Platform Notification System Feedback communiceert alle feedback van platform Notification System tooassist bij foutopsporing.
* **Schaalbaarheid** 
  
  * Toomillions van apparaten zonder dat moet worden veranderd of het apparaat sharding snelle berichten verzenden.
* **Beveiliging**

  * Shared Access Secret (SAS) of federatieve verificatie.

## <a name="integration-with-app-service-mobile-apps"></a>Integratie met App Service Mobile Apps
een naadloze en een uniforme ervaring alle Azure-services, toofacilitate [App Service Mobile Apps] ingebouwde ondersteuning voor pushmeldingen via Notification Hubs. [App Service Mobile Apps] biedt een mobiele toepassing in hoge mate schaalbaar, algemeen beschikbaar ontwikkelplatform voor ontwikkelaars van ondernemingen en systeemintegrators die ook een uitgebreide reeks mogelijkheden toomobile ontwikkelaars.

Mobiele Apps van ontwikkelaars kunnen gebruikmaken van Notification Hubs Hello workflow volgen:

1. PNS-ingang van het apparaat ophalen
2. Apparaten registreren met Notification Hubs via de handige Client SDK voor Mobile Apps registreren API
   * Om beveiligingsreden worden alle tags op registraties door mobiele apps verwijderd. Werken met Notification Hubs vanuit uw back-end rechtstreeks tooassociate tags aan apparaten.
3. Meldingen verzenden vanuit de back-end van uw app met Notification Hubs

Hier volgen een aantal voordelen toodevelopers bij deze integratie:

* **Mobiele Apps Client-SDK's**: deze SDK's van meerdere platforms bieden eenvoudige API's voor registratie en het contact toohello notification hub die automatisch de mobiele App Hallo gekoppeld. Ontwikkelaars niet toodig via Notification Hubs referenties nodig en werken met een extra service.

  * *Push toouser*: Hallo SDK's label automatisch Hallo apparaat met Mobile Apps geverifieerde gebruikers-ID tooenable push toouser scenario gegeven.
  * *Push toodevice*: Hallo SDK's Hallo Mobile Apps-installatie-ID automatisch als GUID tooregister met Notification Hubs, Hierdoor hoeven Hallo problemen van het onderhouden van meerdere service-GUID's gebruiken.
* **Installatiemodel**: mobiele Apps werken met Notification Hubs nieuwste push model toorepresent alle eigenschappen die zijn gekoppeld aan een apparaat in een JSON-installatie die wordt uitgelijnd met een Push Notification Services en eenvoudig toouse push.
* **Flexibiliteit**: ontwikkelaars kunnen altijd beslissen toowork rechtstreeks met Notification Hubs zelfs met Hallo-integratie in plaats.
* **Geïntegreerde ervaring in [Azure-portal]**: Push-als een mogelijkheid visueel wordt weergegeven in Mobile Apps en ontwikkelaars eenvoudig met de bijbehorende notification hub Hallo via mobiele Apps werken kunnen.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over de Notification Hubs vindt u in de volgende onderwerpen:

* **[Hoe klanten Notification Hubs gebruiken]**
* **[Zelfstudies en handleidingen voor Notification Hubs]**
* **Notification Hubs aan de slag zelfstudies**: [iOS], [Android], [universele Windows-], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
[Hoe klanten Notification Hubs gebruiken]: http://azure.microsoft.com/services/notification-hubs
[Zelfstudies en handleidingen voor Notification Hubs]: http://azure.microsoft.com/documentation/services/notification-hubs
[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started
[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started
[universele Windows-]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started
[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started
[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started
[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started
[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
[App Service Mobile Apps]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/
[templates]: notification-hubs-templates-cross-platform-push-messages.md
[Azure-portal]: https://portal.azure.com
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
