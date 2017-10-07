---
title: aaaHow tooUse Hallo JavaScript SDK voor Azure Mobile Apps
description: Hoe tooUse v voor Azure Mobile Apps
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>Hoe tooUse JavaScript-clientbibliotheek Hallo voor Azure Mobile Apps
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Deze handleiding leert u tooperform algemene scenario's met Hallo nieuwste [JavaScript SDK voor Azure Mobile Apps]. Als u nieuwe tooAzure Mobile Apps, eerst voltooien [Azure Mobile Apps Quick Start] toocreate een back-end en een tabel te maken. In deze handleiding richten we op het gebruik van Hallo mobiele back-end in de HTML/JavaScript-webtoepassingen.

## <a name="supported-platforms"></a>Ondersteunde platforms
We beperken browser ondersteuning toohello huidige en versies van Hallo laatste belangrijke browsers: Google Chrome, Microsoft Edge Microsoft Internet Explorer en Mozilla Firefox.  We verwachten Hallo SDK toofunction met relatief moderne browsers.

Hallo-pakket wordt gedistribueerd als een universeel JavaScript-Module, zodat deze globale variabelen, AMD, ondersteunt en CommonJS indelingen.

## <a name="Setup"></a>Het installatieprogramma en vereisten
Deze handleiding wordt ervan uitgegaan dat u een back-end hebt gemaakt met een tabel. Deze handleiding wordt ervan uitgegaan dat tabel Hallo Hallo hetzelfde schema Hallo tabellen in deze zelfstudies.

Hello Azure Mobile Apps JavaScript SDK installeren kan worden uitgevoerd via Hallo `npm` opdracht:

```
npm install azure-mobile-apps-client --save
```

Hallo-bibliotheek kan ook worden gebruikt als een module ES2015 binnen CommonJS omgevingen zoals Browserify en Webpack en als een AMD-bibliotheek.  Bijvoorbeeld:

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

U kunt ook een vooraf samengestelde versie Hallo SDK gebruiken door rechtstreeks uit onze CDN te downloaden:

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Procedure: verificatie van gebruikers
Azure App Service biedt ondersteuning voor verificatie en autorisatie van app-gebruikers met behulp van verschillende externe id-providers: Facebook, Google, Microsoft-Account en Twitter. U kunt machtigingen instellen voor tabellen toorestrict toegang voor specifieke bewerkingen tooonly geverifieerde gebruikers. U kunt ook Hallo identiteit van autorisatieregels voor geverifieerde gebruikers tooimplement in server-scripts gebruiken. Zie voor meer informatie, Hallo [aan de slag met verificatie] zelfstudie.

Twee verificatie stromen worden ondersteund: de stroom van een server en een client-stroom.  Hallo server stroom biedt Hallo eenvoudigste verificatie-ervaring, is afhankelijk van de webinterface verificatie Hallo-provider. Hallo stroom kunt u betere integratie met apparaatspecifieke mogelijkheden, zoals single-sign-on zoals is afhankelijk van de provider-specifieke SDK's.

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Procedure: het configureren van uw mobiele App Service voor externe Omleidings-URL's.
Verschillende soorten toepassingen van JavaScript gebruiken een loopback mogelijkheid toohandle die OAuth UI loopt.  Deze mogelijkheden zijn:

* Uw service lokaal uitgevoerd
* Gebruik van Live opnieuw laden met Hallo ionische Framework
* Omleiden tooApp Service voor verificatie.

Die lokaal wordt uitgevoerd kan problemen veroorzaken omdat standaard App Service-verificatie alleen is geconfigureerd tooallow toegang vanaf uw mobiele App back-end. Gebruik Hallo volgende stappen toochange Hallo App Service-instellingen tooenable verificatie wanneer Hallo server lokaal wordt uitgevoerd:

1. Meld u bij toohello [Azure-portal]
2. Navigeer tooyour mobiele App back-end.
3. Selecteer **resourceverkenner** in Hallo **ONTWIKKELINGSPROGRAMMA's** menu.
4. Klik op **gaat** tooopen Hallo resource explorer voor backend voor mobiele apps in een nieuw tabblad of venster.
5. Vouw Hallo **config** > **authsettings** knooppunt voor uw app.
6. Klik op Hallo **bewerken** knop tooenable van Hallo bron bewerken.
7. Hallo zoeken **allowedExternalRedirectUrls** -element moet null zijn. De URL's in een matrix toevoegen:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Hallo-URL's in de matrix Hallo vervangen door Hallo-URL's van uw service, die in dit voorbeeld is `http://localhost:3000` voor Hallo lokale Node.js-voorbeeld-service. U kunt ook `http://localhost:4400` voor Hallo Rimpel service of een andere URL, afhankelijk van hoe uw app is geconfigureerd.
8. Bovenaan Hallo Hallo pagina, klikt u op **lezen/schrijven**, klikt u vervolgens op **plaatsen** toosave je updates.

U moet ook tooadd Hallo dezelfde loopback-URL's toohello CORS geaccepteerde instellingen:

1. Navigeer terug toohello [Azure-portal].
2. Navigeer tooyour mobiele App back-end.
3. Klik op **CORS** in Hallo **API** menu.
4. Elke URL opgeven in Hallo leeg **toegestane oorsprongen** in het tekstvak.  Een nieuw tekstvak wordt gemaakt.
5. Klik op **opslaan**

Nadat het Hallo-back-end-updates, kunt u zich kunt toouse Hallo nieuwe loopback-URL's in uw app.

<!-- URLs. -->
[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md
[aan de slag met verificatie]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure-portal]: https://portal.azure.com/
[JavaScript SDK voor Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
