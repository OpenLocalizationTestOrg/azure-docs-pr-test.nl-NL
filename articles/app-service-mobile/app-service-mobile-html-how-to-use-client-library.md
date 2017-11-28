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
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="39904-103">Hoe tooUse JavaScript-clientbibliotheek Hallo voor Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="39904-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="39904-104">Deze handleiding leert u tooperform algemene scenario's met Hallo nieuwste [JavaScript SDK voor Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="39904-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="39904-105">Als u nieuwe tooAzure Mobile Apps, eerst voltooien [Azure Mobile Apps Quick Start] toocreate een back-end en een tabel te maken.</span><span class="sxs-lookup"><span data-stu-id="39904-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="39904-106">In deze handleiding richten we op het gebruik van Hallo mobiele back-end in de HTML/JavaScript-webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="39904-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="39904-107">Ondersteunde platforms</span><span class="sxs-lookup"><span data-stu-id="39904-107">Supported platforms</span></span>
<span data-ttu-id="39904-108">We beperken browser ondersteuning toohello huidige en versies van Hallo laatste belangrijke browsers: Google Chrome, Microsoft Edge Microsoft Internet Explorer en Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="39904-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="39904-109">We verwachten Hallo SDK toofunction met relatief moderne browsers.</span><span class="sxs-lookup"><span data-stu-id="39904-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="39904-110">Hallo-pakket wordt gedistribueerd als een universeel JavaScript-Module, zodat deze globale variabelen, AMD, ondersteunt en CommonJS indelingen.</span><span class="sxs-lookup"><span data-stu-id="39904-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="39904-111"><a name="Setup"></a>Het installatieprogramma en vereisten</span><span class="sxs-lookup"><span data-stu-id="39904-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="39904-112">Deze handleiding wordt ervan uitgegaan dat u een back-end hebt gemaakt met een tabel.</span><span class="sxs-lookup"><span data-stu-id="39904-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="39904-113">Deze handleiding wordt ervan uitgegaan dat tabel Hallo Hallo hetzelfde schema Hallo tabellen in deze zelfstudies.</span><span class="sxs-lookup"><span data-stu-id="39904-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="39904-114">Hello Azure Mobile Apps JavaScript SDK installeren kan worden uitgevoerd via Hallo `npm` opdracht:</span><span class="sxs-lookup"><span data-stu-id="39904-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="39904-115">Hallo-bibliotheek kan ook worden gebruikt als een module ES2015 binnen CommonJS omgevingen zoals Browserify en Webpack en als een AMD-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="39904-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="39904-116">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="39904-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="39904-117">U kunt ook een vooraf samengestelde versie Hallo SDK gebruiken door rechtstreeks uit onze CDN te downloaden:</span><span class="sxs-lookup"><span data-stu-id="39904-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="39904-118"><a name="auth"></a>Procedure: verificatie van gebruikers</span><span class="sxs-lookup"><span data-stu-id="39904-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="39904-119">Azure App Service biedt ondersteuning voor verificatie en autorisatie van app-gebruikers met behulp van verschillende externe id-providers: Facebook, Google, Microsoft-Account en Twitter.</span><span class="sxs-lookup"><span data-stu-id="39904-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="39904-120">U kunt machtigingen instellen voor tabellen toorestrict toegang voor specifieke bewerkingen tooonly geverifieerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="39904-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="39904-121">U kunt ook Hallo identiteit van autorisatieregels voor geverifieerde gebruikers tooimplement in server-scripts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="39904-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="39904-122">Zie voor meer informatie, Hallo [aan de slag met verificatie] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="39904-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="39904-123">Twee verificatie stromen worden ondersteund: de stroom van een server en een client-stroom.</span><span class="sxs-lookup"><span data-stu-id="39904-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="39904-124">Hallo server stroom biedt Hallo eenvoudigste verificatie-ervaring, is afhankelijk van de webinterface verificatie Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="39904-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="39904-125">Hallo stroom kunt u betere integratie met apparaatspecifieke mogelijkheden, zoals single-sign-on zoals is afhankelijk van de provider-specifieke SDK's.</span><span class="sxs-lookup"><span data-stu-id="39904-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="39904-126"><a name="configure-external-redirect-urls"></a>Procedure: het configureren van uw mobiele App Service voor externe Omleidings-URL's.</span><span class="sxs-lookup"><span data-stu-id="39904-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="39904-127">Verschillende soorten toepassingen van JavaScript gebruiken een loopback mogelijkheid toohandle die OAuth UI loopt.</span><span class="sxs-lookup"><span data-stu-id="39904-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="39904-128">Deze mogelijkheden zijn:</span><span class="sxs-lookup"><span data-stu-id="39904-128">These capabilities include:</span></span>

* <span data-ttu-id="39904-129">Uw service lokaal uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="39904-129">Running your service locally</span></span>
* <span data-ttu-id="39904-130">Gebruik van Live opnieuw laden met Hallo ionische Framework</span><span class="sxs-lookup"><span data-stu-id="39904-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="39904-131">Omleiden tooApp Service voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="39904-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="39904-132">Die lokaal wordt uitgevoerd kan problemen veroorzaken omdat standaard App Service-verificatie alleen is geconfigureerd tooallow toegang vanaf uw mobiele App back-end.</span><span class="sxs-lookup"><span data-stu-id="39904-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="39904-133">Gebruik Hallo volgende stappen toochange Hallo App Service-instellingen tooenable verificatie wanneer Hallo server lokaal wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="39904-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="39904-134">Meld u bij toohello [Azure-portal]</span><span class="sxs-lookup"><span data-stu-id="39904-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="39904-135">Navigeer tooyour mobiele App back-end.</span><span class="sxs-lookup"><span data-stu-id="39904-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="39904-136">Selecteer **resourceverkenner** in Hallo **ONTWIKKELINGSPROGRAMMA's** menu.</span><span class="sxs-lookup"><span data-stu-id="39904-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="39904-137">Klik op **gaat** tooopen Hallo resource explorer voor backend voor mobiele apps in een nieuw tabblad of venster.</span><span class="sxs-lookup"><span data-stu-id="39904-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="39904-138">Vouw Hallo **config** > **authsettings** knooppunt voor uw app.</span><span class="sxs-lookup"><span data-stu-id="39904-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="39904-139">Klik op Hallo **bewerken** knop tooenable van Hallo bron bewerken.</span><span class="sxs-lookup"><span data-stu-id="39904-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="39904-140">Hallo zoeken **allowedExternalRedirectUrls** -element moet null zijn.</span><span class="sxs-lookup"><span data-stu-id="39904-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="39904-141">De URL's in een matrix toevoegen:</span><span class="sxs-lookup"><span data-stu-id="39904-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="39904-142">Hallo-URL's in de matrix Hallo vervangen door Hallo-URL's van uw service, die in dit voorbeeld is `http://localhost:3000` voor Hallo lokale Node.js-voorbeeld-service.</span><span class="sxs-lookup"><span data-stu-id="39904-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="39904-143">U kunt ook `http://localhost:4400` voor Hallo Rimpel service of een andere URL, afhankelijk van hoe uw app is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="39904-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="39904-144">Bovenaan Hallo Hallo pagina, klikt u op **lezen/schrijven**, klikt u vervolgens op **plaatsen** toosave je updates.</span><span class="sxs-lookup"><span data-stu-id="39904-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="39904-145">U moet ook tooadd Hallo dezelfde loopback-URL's toohello CORS geaccepteerde instellingen:</span><span class="sxs-lookup"><span data-stu-id="39904-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="39904-146">Navigeer terug toohello [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="39904-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="39904-147">Navigeer tooyour mobiele App back-end.</span><span class="sxs-lookup"><span data-stu-id="39904-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="39904-148">Klik op **CORS** in Hallo **API** menu.</span><span class="sxs-lookup"><span data-stu-id="39904-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="39904-149">Elke URL opgeven in Hallo leeg **toegestane oorsprongen** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="39904-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="39904-150">Een nieuw tekstvak wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39904-150">A new text box is created.</span></span>
5. <span data-ttu-id="39904-151">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="39904-151">Click **SAVE**</span></span>

<span data-ttu-id="39904-152">Nadat het Hallo-back-end-updates, kunt u zich kunt toouse Hallo nieuwe loopback-URL's in uw app.</span><span class="sxs-lookup"><span data-stu-id="39904-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md
[aan de slag met verificatie]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure-portal]: https://portal.azure.com/
[JavaScript SDK voor Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
