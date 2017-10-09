---
title: 'Azure Notification Hubs: Frequently Asked Questions (FAQ''s) | Microsoft Docs'
description: Veelgestelde vragen over het ontwerpen/implementeren van oplossingen voor Notification Hubs
services: notification-hubs
documentationcenter: mobile
author: ysxu
manager: erikre
keywords: push-melding, pushmeldingen, pushmeldingen voor iOS, android pushmeldingen, push ios, android push
editor: 
ms.assetid: 7b385713-ef3b-4f01-8b1f-ffe3690bbd40
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 01/19/2017
ms.author: yuaxu
ms.openlocfilehash: a70efa7fc5954966847d5a173e9b10accf4b737e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="push-notifications-with-azure-notification-hubs-frequently-asked-questions"></a>Pushmeldingen met Azure Notification Hubs: veelgestelde vragen
## <a name="general"></a>Algemeen
### <a name="what-is-hello-resource-structure-of-notification-hubs"></a>Wat is Hallo resource structuur van Notification Hubs?

Azure Notification Hubs heeft twee niveaus van de resource: hubs en naamruimten. Een hub is een enkel push-resource die Hallo platformoverschrijdende push-informatie van een app kan bevatten. Een naamruimte is een verzameling van hubs in één regio.

Aanbevolen toewijzing komt overeen met een naamruimte met een app. U kunt een productie-hub die geschikt is voor uw productie-app, een test-hub die geschikt is voor uw test-app, enzovoort hebben binnen een naamruimte.

### <a name="what-is-hello-price-model-for-notification-hubs"></a>Wat is Hallo prijsmodel voor Notification Hubs?
Hallo laatste prijsinformatie vindt u op Hallo [Notification Hubs prijzen] pagina. Notification Hubs wordt gefactureerd op Hallo naamruimte niveau. (Klik voor Hallo definitie van een naamruimte, Zie 'Wat is Hallo resource structuur van Notification Hubs?') Notification Hubs biedt drie lagen:

* **Gratis**: deze laag is een goed uitgangspunt voor het verkennen van push-mogelijkheden. Dit wordt niet aanbevolen voor productie-apps. Registreren van 500 apparaten en 1 miljoen pushes per naamruimte per maand, opgenomen met geen garantie van service level agreement (SLA).
* **Basic**: deze laag (of Hallo standaardcategorie) wordt aanbevolen voor kleinere productie-apps. Registreren van 200.000 apparaten en 10 miljoen pushes per naamruimte per maand als basislijn opgenomen. Quotum groei van de opties zijn opgenomen.
* **Standaard**: deze laag wordt aanbevolen voor middelgrote toolarge productie apps. U krijgt 10 miljoen apparaten en 10 miljoen pushes per naamruimte per maand als basislijn opgenomen. Quotum verhogen opties en uitgebreide telemetrie mogelijkheden zijn opgenomen.

Standard-laag functies:
* **Uitgebreide telemetrie**: Notification Hubs Per bericht telemetrie tootrack kunt u een push-aanvragen en Platform Notification System Feedback voor foutopsporing.
* **Multitenancy**: U kunt werken met Platform Notification System referenties op het niveau van een naamruimte. Met deze optie kunt u tooeasily tenants splitsen in hubs binnen Hallo dezelfde naamruimte.
* **Geplande push**: U kunt meldingen toobe verzonden op elk gewenst moment plannen.

### <a name="what-is-hello-notification-hubs-sla"></a>Wat is Hallo Notification Hubs SLA?
Voor Basic en Standard Notification Hubs-lagen toepassingen correct is geconfigureerd om pushmeldingen te verzenden of registratie beheerbewerkingen uitvoeren minimaal 99,9 procent van Hallo tijd. meer informatie over Hallo SLA, Ga toohello toolearn [Notification Hubs SLA](https://azure.microsoft.com/support/legal/sla/notification-hubs/) pagina.

> [!NOTE]
> Omdat pushmeldingen is afhankelijk van derden Platform Notification System (zoals Apple APNS en Google FCM), is er geen SLA-garantie voor de levering van Hallo van deze berichten. Nadat de Notification Hubs stuurt Hallo batches tooPlatform Notification System (SLA gegarandeerd), is het Hallo-verantwoordelijkheid Hallo Platform Notification System toodeliver Hallo pushes (geen SLA gegarandeerd).

### <a name="which-customers-are-using-notification-hubs"></a>Welke klanten Notification Hubs gebruiken?
Veel klanten Notification Hubs gebruiken. Sommige opmerkelijke die worden hier weergegeven:

* Sochi 2014: Honderden belangengroepen, 3 miljoen apparaten en 150 miljoen meldingen verzonden in twee weken. [Casestudy: Sochi]
* Skanska: [casestudy: Skanska]
* Seattle tijden: [casestudy: Seattle keren]
* Mural.LY: [casestudy: Mural.ly]
* 7Digital: [casestudy: 7Digital]
* Bing-Apps: Tientallen miljoenen apparaten verzenden 3 miljoen meldingen per dag.

### <a name="how-do-i-upgrade-or-downgrade-my-hub-or-namespace-tooa-different-tier"></a>Hoe ik upgraden of mijn-hub of -naamruimte tooa andere tier downgraden?
Ga toohello  **[Azure-portal]** > **Notification Hubs naamruimten** of **Notification Hubs**. Selecteer Hallo resource u wilt tooupdate en ga te**prijscategorie**. Houd er rekening mee Hallo volgens de vereisten:

* Hallo bijgewerkte prijscategorie geldt te*alle* hubs in Hallo naamruimte waarmee u werkt.
* Als uw apparaat aantal de limiet Hallo van Hallo laag die uw abonnement overschrijdt tot beperkt bent, moet u toodelete apparaten voordat u downgraden.


## <a name="design-and-development"></a>Ontwerpen en ontwikkelen
### <a name="which-server-side-platforms-do-you-support"></a>Welke platforms serverzijde ondersteund?
Server SDK's zijn beschikbaar voor .NET, Java, Node.js, PHP en Python. Notification Hubs-API's zijn gebaseerd op de REST-interfaces, zodat u rechtstreeks met de REST-API's werken kunt als u met verschillende platforms of niet dat extra afhankelijkheid wilt. Ga voor meer informatie, toohello [Notification Hubs REST-API's] pagina.

### <a name="which-client-platforms-do-you-support"></a>Welke clientplatforms ondersteund?
Pushmeldingen worden ondersteund voor [iOS](notification-hubs-ios-apple-push-notification-apns-get-started.md), [Android](notification-hubs-android-push-notification-google-gcm-get-started.md), [universele Windows-](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), [Windows Phone](notification-hubs-windows-mobile-push-notifications-mpns.md), [Kindle](notification-hubs-kindle-amazon-adm-push-notification.md), [Android China (via Baidu)](notification-hubs-baidu-china-android-notifications-get-started.md), Xamarin ([iOS](xamarin-notification-hubs-ios-push-notification-apns-get-started.md) en [Android](xamarin-notification-hubs-push-notifications-android-gcm.md)), [Chrome-Apps](notification-hubs-chrome-push-notifications-get-started.md), en [Safari](https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSafari). Ga voor meer informatie, toohello [Notification Hubs aan de slag zelfstudies] pagina.

### <a name="do-you-support-text-message-email-or-web-notifications"></a>Ondersteund SMS-bericht, e-mail of web meldingen?
Notification Hubs is voornamelijk ontworpen toosend meldingen toomobile apps. Biedt geen e-mailadres of tekst bericht mogelijkheden. Echter platforms van derden die deze mogelijkheden bieden kunnen worden geïntegreerd met Notification Hubs toosend native pushmeldingen met behulp van [Mobile Apps].

Notification Hubs beschikt niet over een service in de browser push notification levering out of box Hallo. Klanten kunnen deze functie SignalR boven op Hallo ondersteund serverzijde platforms met implementeren. Als u toosend meldingen toobrowser apps in Hallo Chrome sandbox wilt, raadpleegt u Hallo [Chrome-Apps zelfstudie].

### <a name="how-are-mobile-apps-and-azure-notification-hubs-related-and-when-do-i-use-them"></a>Hoe worden Mobile Apps en Azure Notification Hubs gerelateerd en wanneer kan ik ze gebruiken?
Als u een bestaande mobiele app back-end en gewenste tooadd alleen Hallo mogelijkheid toosend pushmeldingen, kunt u Azure Notification Hubs. Als u tooset van uw back-end voor mobiele app helemaal wilt, kunt u overwegen Hallo Mobile Apps-functie van Azure App Service. Een mobiele app wordt automatisch een notification hub levert zodat u eenvoudig pushmeldingen vanuit Hallo back-end van mobiele app verzenden kunt. Prijzen voor Mobile Apps bevat Hallo base kosten voor een notification hub. U betaalt alleen verstuurd wanneer u Hallo opgenomen overschrijdt. Ga voor meer informatie over kosten, toohello [prijzen van App Service] pagina.

### <a name="how-many-devices-can-i-support-if-i-send-push-notifications-via-notification-hubs"></a>Hoeveel apparaten kan ik ondersteuning als het verzenden van pushmeldingen via Notification Hubs?
Raadpleeg toohello [Notification Hubs prijzen] voor informatie over Hallo aantal ondersteunde apparaten.

Als u ondersteuning nodig hebt voor meer dan 10 miljoen geregistreerde apparaten, [contact met ons opnemen](https://azure.microsoft.com/overview/contact-us/) rechtstreeks en wij helpen u schalen van uw oplossing.

### <a name="how-many-push-notifications-can-i-send-out"></a>Hoeveel pushmeldingen kunnen ik verzenden?
Afhankelijk van de geselecteerde laag hello schaalt Azure Notification Hubs automatisch op basis van het aantal meldingen tot Hallo system Hallo.

> [!NOTE]
> Hallo kunt algehele gebruikskosten verhogen op basis van Hallo aantal pushmeldingen worden geleverd. Zorg ervoor dat u rekening houden met de Hallo laag limieten die worden beschreven op Hallo [Notification Hubs prijzen] pagina.
> 
> 

Onze klanten Notification Hubs toosend miljoenen pushmeldingen dagelijks gebruiken. U hoeft geen toodo iets speciale tooscale Hallo bereiken van uw pushmeldingen, zolang u Azure Notification Hubs.

### <a name="how-long-does-it-take-for-sent-push-notifications-tooreach-my-device"></a>Hoe lang duurt het nemen voor verzonden push notifications tooreach mijn apparaat?
In een normaal gebruik scenario waarbij inkomende hello-load consistent en zelfs, Azure Notification Hubs kunnen worden verwerkt ten minste *1 miljoen push-melding verzendt een minuut*. Deze snelheid kan variëren afhankelijk van het aantal tags hello, Hallo aard van inkomende hello-verzendt en andere externe factoren.

Tijdens het Hallo geschatte leveringstijd, Hallo service berekent Hallo doelen per platform en routeert berichten toohello Push Notification Service (PNS) op basis van Hallo geregistreerd tags of code-expressies. Het is de verantwoordelijkheid Hallo Hallo PNS toosend meldingen toohello apparaat.

Hallo PNS wordt niet gegarandeerd dat een SLA om meldingen te bezorgen. De meeste pushmeldingen worden tootarget apparaten echter geleverd binnen een paar minuten (meestal binnen 10 minuten) van Hallo tijd die ze tooNotification Hubs worden verzonden. Enkele meldingen mogelijk meer tijd vergen.

> [!NOTE]
> Azure Notification Hubs heeft een beleid in place toodrop pushmeldingen die toohello PNS niet worden bezorgd binnen 30 minuten. Deze vertraging kan optreden voor een aantal oorzaken hebben, maar de meeste meestal omdat Hallo PNS is beperking uw toepassing.
> 
> 

### <a name="is-there-any-latency-guarantee"></a>Is er garantie latentie?
Vanwege de aard van de Hallo van pushmeldingen (ze worden geleverd door een externe, platform-specifieke PNS), is er geen garantie latentie. Hallo meerderheid van pushmeldingen worden gewoonlijk bezorgd binnen een paar minuten.

### <a name="what-do-i-need-tooconsider-when-designing-a-solution-with-namespaces-and-notification-hubs"></a>Wat kan ik tooconsider nodig bij het ontwerpen van een oplossing met naamruimten en notification hubs?
#### <a name="mobile-appenvironment"></a>Mobiele app/omgeving
* Een notification hub per mam per omgeving gebruiken.
* In een multitenant-scenario, moet elke tenant een afzonderlijke hub hebben.
* Share Hallo nooit dezelfde notification hub voor productie- en testomgevingen. Hierdoor kan problemen veroorzaken als u meldingen verzendt. (Apple biedt Sandbox en productie Push eindpunten, elk met afzonderlijke referenties).
* U kunt standaard verzenden van meldingen tooyour geregistreerd testapparaten via hello Azure-portal of hello Azure geïntegreerde onderdeel in Visual Studio. drempelwaarde voor Hallo ingesteld too10-apparaten die zijn willekeurig geselecteerd uit Hallo registratie groep.

> [!NOTE]
> Als uw hub oorspronkelijk is geconfigureerd met een certificaat voor Apple sandbox en vervolgens een productiecertificaat Apple opnieuw geconfigureerde toouse is, wordt de oorspronkelijke apparaattokens Hallo zijn ongeldig. Ongeldige tokens veroorzaken pushes toofail. Uw productie- en testomgevingen afzonderlijke en gebruik van verschillende hubs voor verschillende omgevingen.
> 
> 

#### <a name="pns-credentials"></a>PNS-referenties
Als een mobiele app is geregistreerd met een platform-portal voor ontwikkelaars (bijvoorbeeld van Apple of Google), worden een app-id en security-tokens verzonden. Hallo app back-end biedt deze tokens toohello platform PNS, zodat pushmeldingen toodevices kunnen worden verzonden. Beveiligingstokens worden weergegeven in de vorm Hallo van certificaten (bijvoorbeeld Apple iOS of Windows Phone) of beveiligingssleutels (bijvoorbeeld Google Android of Windows). Ze moeten worden geconfigureerd in notification hubs. Configuratie wordt doorgaans uitgevoerd op Hallo notification hub-niveau, maar kan ook worden gedaan op Hallo naamruimte niveau in een multitenant-scenario.

#### <a name="namespaces"></a>Naamruimten
Naamruimten kan worden gebruikt voor het groeperen van de implementatie. Ze kunnen gebruikte toorepresent ook worden alle notification hubs voor alle tenants van dezelfde app in een multitenant scenario Hallo.

#### <a name="geo-distribution"></a>Geo-distributie
Geo-distributie is niet altijd kritieke in push notification-scenario's. Verschillende PNSes (bijvoorbeeld APNS of GCM) die push notifications toodevices leveren zijn niet gelijkmatig verdeeld.

Als u een toepassing die wordt gebruikt globaal hebt, kunt u hubs in verschillende naamruimten met behulp van Hallo Notification Hubs-service in verschillende Azure-regio's Hallo wereld.

> [!NOTE]
> Deze regeling wordt niet aanbevolen omdat de bijbehorende waarde uw beheerkosten, met name voor registraties stijgt. Worden moet gedaan alleen als er een expliciete nodig is.
> 
> 

### <a name="should-i-do-registrations-from-hello-app-back-end-or-directly-through-client-devices"></a>Moet ik doen registraties van Hallo app back-end of rechtstreeks via de client apparaten?
Registraties van Hallo app back-end zijn nuttig wanneer u clients tooauthenticate voordat het Hallo-registratie maakt. Ze zijn ook handig wanneer u de labels die moeten worden gemaakt of gewijzigd door Hallo app back-end op basis van logica van de app hebt. Ga voor meer informatie, toohello [back-end-registratie richtlijnen] en [richtlijnen voor back-end-registratie 2] pagina's.

### <a name="what-is-hello-push-notification-delivery-security-model"></a>Wat is Hallo push notification levering van het beveiligingsmodel?
Azure Notification Hubs maakt gebruik van een [shared access signature voor](../storage/common/storage-dotnet-shared-access-signature-part-1.md)-gebaseerd beveiligingsmodel. Kunt u gedeelde Hallo-toegangstokens handtekening op Hallo naamruimte hoofdniveau of op Hallo gedetailleerde notification hub niveau. Shared access signature-tokens kunnen worden ingesteld toofollow verschillende autorisatieregels, bijvoorbeeld toosend berichtmachtigingen of toolisten voor melding machtigingen. Zie voor meer informatie, Hallo [Notification Hubs beveiligingsmodel] document.

### <a name="how-should-i-handle-sensitive-payload-in-push-notifications"></a>Hoe moet ik gevoelige nettolading in pushmeldingen verwerken?
Alle meldingen worden tootarget apparaten geleverd door de PNS Hallo-platform. Wanneer een melding wordt verzonden tooAzure Notification Hubs, wordt deze verwerkt en toohello doorgegeven respectieve PNS.

Alle verbindingen van Hallo afzender toohello Azure Notification Hubs toohello PNS, gebruik van HTTPS.

> [!NOTE]
> Hallo-nettolading van berichten wordt niet door Azure Notification Hubs op een manier worden geregistreerd.
> 
> 

toosend gevoelige nettoladingen, wordt u aangeraden een patroon Secure Push. Hallo afzender biedt een ping-bericht met een bericht-id toohello apparaat zonder Hallo gevoelige nettolading. Wanneer het Hallo-app op Hallo apparaat Hallo nettolading ontvangt, roept Hallo app een beveiligde API direct toofetch Hallo details van bericht. Ga voor een handleiding op hoe tooimplement van dit patroon toohello [Notification Hubs Secure Push zelfstudie] pagina.

## <a name="operations"></a>Bewerkingen
### <a name="what-support-is-provided-for-disaster-recovery"></a>Wat wordt ondersteund voor herstel na noodgevallen?
We bieden metagegevens disaster recovery dekking aan onze kant (Hallo Notification Hubs naam, de verbindingsreeks Hallo en andere essentiële informatie). Wanneer een noodherstelscenario wordt geactiveerd, registratiegegevens Hallo is *alleen segmenteren* van Hallo Notification Hubs-infrastructuur die verloren gaat. U moet een oplossing toorepopulate tooimplement deze gegevens in uw nieuwe hub na herstel:

1. Maak een secundaire Notification hubs in een ander datacenter. We raden u één van Hallo begin tooshield aan u uit een disaster recovery-gebeurtenis die invloed kan zijn op de beheermogelijkheden. U kunt ook een voor Hallo van Hallo disaster recovery gebeurtenis maken.

2. Vul Hallo secundaire notification hub met Hallo registraties van uw primaire notification hub. We niet kunt het beste poging toomaintain registraties op beide hubs en houden synchroon registraties komen. Deze procedure werkt niet goed vanwege Hallo inherente neiging van registraties tooexpire op Hallo PNS aan clientzijde. Notification Hubs ruimt ze ontvangen PNS feedback over registraties verlopen of ongeldig.  

Wij hebben twee aanbevelingen voor back-ends van app:

* Gebruik een app back-end die wordt onderhouden door een bepaalde set registraties aan het einde. Vervolgens kan een bulksgewijs invoegen in Hallo secundaire notification hub uitvoeren.

* Gebruik een app back-end waarin een reguliere dump van registraties van Hallo primaire notification hub als een back-up worden opgehaald. Vervolgens kan een bulksgewijs invoegen in Hallo secundaire notification hub uitvoeren.

> [!NOTE]
> Functionaliteit voor exporteren/importeren registraties beschikbaar in Standard-laag hello wordt beschreven in Hallo [registraties exporteren/importeren] document.
> 
> 

Als u geen back-end wanneer Hallo-app wordt gestart op doelapparaten, uitvoeren een nieuwe registratie ze in Hallo secundaire notification hub. Uiteindelijk heeft hello secundaire notification hub alle Hallo actieve apparaten geregistreerd.

Er is een periode apparaten met niet-geopende apps wanneer geen meldingen ontvangt.

### <a name="is-there-audit-log-capability"></a>Is er audit log mogelijkheid?
Alle beheerbewerkingen voor Notification Hubs gaat toooperation Logboeken, die beschikbaar worden gesteld in Hallo [klassieke Azure-portal].

## <a name="monitoring-and-troubleshooting"></a>Bewaking en probleemoplossing
### <a name="what-troubleshooting-capabilities-are-available"></a>Welke mogelijkheden voor probleemoplossing zijn beschikbaar?
Azure Notification Hubs biedt verschillende functies voor het oplossen van problemen met name voor de meest voorkomende scenario Hallo van verwijderde meldingen. Zie voor meer informatie, Hallo [Notification Hubs probleemoplossing] witboek.

### <a name="what-telemetry-features-are-available"></a>Welke telemetrie-functies zijn beschikbaar?
Azure Notification Hubs kunt bekijken van telemetriegegevens in Hallo [klassieke Azure-portal]. Details van Hallo metrische gegevens zijn beschikbaar op Hallo [Notification Hubs metrische gegevens] pagina.

> [!NOTE]
> Geslaagde meldingen gewoon betekenen dat pushmeldingen zijn geleverd toohello externe PNS (bijvoorbeeld APNS voor Apple) of GCM voor Google. Het is de verantwoordelijkheid Hallo Hallo PNS toodeliver Hallo meldingen tootarget apparaten. Hallo PNS maakt normaal gesproken niet beschikbaar voor levering metrische gegevens toothird partijen.  
> 
> 

We bieden ook Hallo mogelijkheid tooexport Hallo telemetrische gegevens via een programma (in Hallo Standard-laag). Zie voor meer informatie, Hallo [Notification Hubs metrische gegevens voorbeeld].

[klassieke Azure-portal]: https://manage.windowsazure.com
[Notification Hubs prijzen]: http://azure.microsoft.com/pricing/details/notification-hubs/
[Notification Hubs SLA]: http://azure.microsoft.com/support/legal/sla/
[Casestudy: Sochi]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=7942
[Casestudy: Skanska]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5847
[Casestudy: Seattle keren]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=8354
[Casestudy: Mural.ly]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=11592
[Casestudy: 7Digital]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=3684
[Notification Hubs REST-API's]: https://msdn.microsoft.com/library/azure/dn530746.aspx
[Notification Hubs aan de slag zelfstudies]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Chrome-Apps zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-chrome-get-started/
[Mobile Services Pricing]: http://azure.microsoft.com/pricing/details/mobile-services/
[back-end-registratie richtlijnen]: https://msdn.microsoft.com/library/azure/dn743807.aspx
[richtlijnen voor back-end-registratie 2]: https://msdn.microsoft.com/library/azure/dn530747.aspx
[Notification Hubs beveiligingsmodel]: https://msdn.microsoft.com/library/azure/dn495373.aspx
[Notification Hubs Secure Push zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-aspnet-backend-ios-secure-push/
[Notification Hubs probleemoplossing]: http://azure.microsoft.com/documentation/articles/notification-hubs-diagnosing/
[Notification Hubs metrische gegevens]: https://msdn.microsoft.com/library/dn458822.aspx
[Notification Hubs metrische gegevens voorbeeld]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel
[registraties exporteren/importeren]: https://msdn.microsoft.com/library/dn790624.aspx
[Azure-portal]: https://portal.azure.com
[complete samples]: https://github.com/Azure/azure-notificationhubs-samples
[Mobile Apps]: https://azure.microsoft.com/services/app-service/mobile/
[prijzen van App Service]: https://azure.microsoft.com/pricing/details/app-service/
