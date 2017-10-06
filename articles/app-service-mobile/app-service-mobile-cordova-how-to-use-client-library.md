---
title: aaaHow tooUse Apache Cordova-invoegtoepassing voor Azure Mobile Apps
description: Hoe tooUse Apache Cordova-invoegtoepassing voor Azure Mobile Apps
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a>Hoe toouse Apache Cordova-clientbibliotheek voor Azure Mobile Apps
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Deze handleiding leert u tooperform algemene scenario's met Hallo nieuwste [Apache Cordova-invoegtoepassing voor Azure Mobile Apps]. Als u nieuwe tooAzure Mobile Apps, eerst voltooien [Azure Mobile Apps Quick Start] toocreate een back-end van een tabel maken en een vooraf samengestelde Apache Cordova-project hebt gedownload. In deze handleiding we richten op Hallo clientzijde Apache Cordova-invoegtoepassing.

## <a name="supported-platforms"></a>Ondersteunde platforms
Deze SDK biedt ondersteuning voor Apache Cordova-v6.0.0 en later op iOS, Android en Windows apparaten.  Hallo platformondersteuning is als volgt:

* Android-API 19-24 (KitKat via deze).
* iOS 8.0 en hoger.
* Windows Phone 8.1.
* Universele Windows-Platform.

## <a name="Setup"></a>Het installatieprogramma en vereisten
Deze handleiding wordt ervan uitgegaan dat u een back-end hebt gemaakt met een tabel. Deze handleiding wordt ervan uitgegaan dat tabel Hallo Hallo hetzelfde schema Hallo tabellen in deze zelfstudies. Deze handleiding wordt ervan uitgegaan dat u Hallo Apache Cordova-invoegtoepassing tooyour code hebt toegevoegd.  Als u dit niet gedaan hebt, kunt u op de opdrachtregel Hallo mag Hallo Apache Cordova-invoegtoepassing tooyour project toevoegen:

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

Voor meer informatie over het maken van [uw eerste Apache Cordova-app], Zie de documentatie.

## <a name="ionic"></a>Instellen van een app ionische v2

tooproperly configureren van een project ionische v2, eerst een eenvoudige app maken en toevoegen van Hallo Cordova-invoegtoepassing:

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

Toevoegen van de volgende regels te Hallo`app.component.ts` object toocreate Hallo-client:

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

U kunt nu bouwen en uitvoeren van Hallo-project in de browser Hallo:

```
ionic platform add browser
ionic run browser
```

Hello Azure Mobile Apps Cordova-invoegtoepassing biedt ondersteuning voor beide ionische v1- en v2-apps.  Alleen apps Hallo ionische v2 aanvullende verklaring voor Hallo vereisen `WindowsAzure` object.

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Procedure: verificatie van gebruikers
Azure App Service biedt ondersteuning voor verificatie en autorisatie van app-gebruikers met behulp van verschillende externe id-providers: Facebook, Google, Microsoft-Account en Twitter. U kunt machtigingen instellen voor tabellen toorestrict toegang voor specifieke bewerkingen tooonly geverifieerde gebruikers. U kunt ook Hallo identiteit van autorisatieregels voor geverifieerde gebruikers tooimplement in server-scripts gebruiken. Zie voor meer informatie, Hallo [aan de slag met verificatie] zelfstudie.

Wanneer u verificatie gebruikt in een Apache Cordova-app, moet Hallo na Cordova plugins beschikbaar zijn:

* [cordova-invoegtoepassing-apparaat]
* [cordova-invoegtoepassing-inappbrowser]

Twee verificatie stromen worden ondersteund: de stroom van een server en een client-stroom.  Hallo server stroom biedt Hallo eenvoudigste verificatie-ervaring, is afhankelijk van de webinterface verificatie Hallo-provider. Hallo stroom kunt u betere integratie met apparaatspecifieke mogelijkheden, zoals single-sign-on zoals is afhankelijk van de provider-specifieke apparaat-specifieke SDK's.

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Procedure: het configureren van uw mobiele App Service voor externe Omleidings-URL's.
Verschillende soorten Apache Cordova-toepassingen gebruiken een loopback mogelijkheid toohandle die OAuth UI loopt.  OAuth UI-overdrachten op localhost problemen veroorzaken omdat Hallo verificatieservice alleen weet hoe tooutilize uw service standaard.  Voorbeelden van problematisch OAuth UI stromen zijn:

* Hallo Rimpel emulator.
* Live opnieuw laden met ionische.
* Hallo mobiele back-end lokaal uitgevoerd
* Hallo mobiele back-end in een andere Azure App Service dan Hallo één verstrekken verificatie uitgevoerd.

Volg deze instructies tooadd uw lokale instellingen toohello configuratie:

1. Meld u bij toohello [Azure-portal]
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van uw mobiele App.
3. Klik op **hulpprogramma's**
4. Klik op **resourceverkenner** in Hallo OBSERVE menu, klikt u **gaat**.  Een nieuw venster of tabblad wordt geopend.
5. Vouw Hallo **config**, **authsettings** knooppunten voor uw site in de linkernavigatiebalk Hallo.
6. Klik op **bewerken**
7. Zoek naar Hallo 'allowedExternalRedirectUrls'-element.  Worden kan ingesteld toonull of een matrix met waarden.  Hallo waarde toohello na waarde wijzigen:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Hallo-URL's vervangen door Hallo-URL's van uw service.  Voorbeelden zijn "http://localhost: 3000' (voor Node.js-voorbeeld service Hallo) of 'http://localhost:4400' (voor Hallo Rimpel service).  Deze URL's zijn echter voorbeelden - uw situatie, met inbegrip van Hallo diensten vermeld in de voorbeelden hello, kunnen afwijken.
8. Klik op Hallo **lezen/schrijven** knop in Hallo rechterbovenhoek van het welkomstscherm.
9. Klik op Hallo groen **plaatsen** knop.

Hallo-instellingen worden op dit moment opgeslagen.  Hallo-browservenster niet sluiten totdat Hallo-instellingen hebt opgeslagen.
Ook deze loopback-URL's toohello CORS-instellingen voor uw App Service toevoegen:

1. Meld u bij toohello [Azure-portal]
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van uw mobiele App.
3. de blade instellingen Hello wordt automatisch geopend.  Als dit niet zo is, klikt u op **alle instellingen**.
4. Klik op **CORS** onder Hallo API-menu.
5. Voer Hallo-URL die u wenst dat tooadd in Hallo daarvoor bestemde vak in en druk op Enter.
6. Geef extra URL's desgewenst.
7. Klik op **opslaan** toosave Hallo instellingen.

Het duurt ongeveer 10-15 seconden voor Hallo nieuwe instellingen tootake effect.

## <a name="register-for-push"></a>Hoe: registreren voor pushmeldingen
Hallo installeren [phonegap-invoegtoepassing-push] toohandle pushmeldingen.  Deze invoegtoepassing gemakkelijk kan worden toegevoegd met de `cordova plugin add` opdracht op de opdrachtregel Hallo of via Hallo Git-invoegtoepassing installatieprogramma vanuit Visual Studio.  De volgende code in uw Apache Cordova-app registreert uw apparaat voor pushmeldingen:

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

Hallo Notification Hubs SDK toosend pushmeldingen vanuit Hallo-server gebruiken.  Nooit pushmeldingen rechtstreeks vanuit clients verzenden. Hierdoor kan dus worden gebruikte tootrigger een denial of service-aanval tegen Notification Hubs of Hallo PNS.  Hallo PNS kan verkeer als gevolg van dergelijke aanvallen been.

## <a name="more-information"></a>Meer informatie

U vindt gedetailleerde informatie voor API in onze [API-documentatie](http://azure.github.io/azure-mobile-apps-js-client/).

<!-- URLs. -->
[Azure-portal]: https://portal.azure.com
[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md
[aan de slag met verificatie]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Apache Cordova-invoegtoepassing voor Azure Mobile Apps]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[uw eerste Apache Cordova-app]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap-invoegtoepassing-push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-invoegtoepassing-apparaat]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-invoegtoepassing-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
