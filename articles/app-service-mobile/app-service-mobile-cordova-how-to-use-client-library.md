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
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="d4be5-103">Hoe toouse Apache Cordova-clientbibliotheek voor Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="d4be5-103">How toouse Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="d4be5-104">Deze handleiding leert u tooperform algemene scenario's met Hallo nieuwste [Apache Cordova-invoegtoepassing voor Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="d4be5-104">This guide teaches you tooperform common scenarios using hello latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="d4be5-105">Als u nieuwe tooAzure Mobile Apps, eerst voltooien [Azure Mobile Apps Quick Start] toocreate een back-end van een tabel maken en een vooraf samengestelde Apache Cordova-project hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="d4be5-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="d4be5-106">In deze handleiding we richten op Hallo clientzijde Apache Cordova-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="d4be5-106">In this guide, we focus on hello client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="d4be5-107">Ondersteunde platforms</span><span class="sxs-lookup"><span data-stu-id="d4be5-107">Supported platforms</span></span>
<span data-ttu-id="d4be5-108">Deze SDK biedt ondersteuning voor Apache Cordova-v6.0.0 en later op iOS, Android en Windows apparaten.</span><span class="sxs-lookup"><span data-stu-id="d4be5-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="d4be5-109">Hallo platformondersteuning is als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4be5-109">hello platform support is as follows:</span></span>

* <span data-ttu-id="d4be5-110">Android-API 19-24 (KitKat via deze).</span><span class="sxs-lookup"><span data-stu-id="d4be5-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="d4be5-111">iOS 8.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="d4be5-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="d4be5-112">Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="d4be5-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="d4be5-113">Universele Windows-Platform.</span><span class="sxs-lookup"><span data-stu-id="d4be5-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="d4be5-114"><a name="Setup"></a>Het installatieprogramma en vereisten</span><span class="sxs-lookup"><span data-stu-id="d4be5-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="d4be5-115">Deze handleiding wordt ervan uitgegaan dat u een back-end hebt gemaakt met een tabel.</span><span class="sxs-lookup"><span data-stu-id="d4be5-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="d4be5-116">Deze handleiding wordt ervan uitgegaan dat tabel Hallo Hallo hetzelfde schema Hallo tabellen in deze zelfstudies.</span><span class="sxs-lookup"><span data-stu-id="d4be5-116">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="d4be5-117">Deze handleiding wordt ervan uitgegaan dat u Hallo Apache Cordova-invoegtoepassing tooyour code hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d4be5-117">This guide also assumes that you have added hello Apache Cordova Plugin tooyour code.</span></span>  <span data-ttu-id="d4be5-118">Als u dit niet gedaan hebt, kunt u op de opdrachtregel Hallo mag Hallo Apache Cordova-invoegtoepassing tooyour project toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d4be5-118">If you have not done so, you may add hello Apache Cordova plugin tooyour project on hello command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="d4be5-119">Voor meer informatie over het maken van [uw eerste Apache Cordova-app], Zie de documentatie.</span><span class="sxs-lookup"><span data-stu-id="d4be5-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="d4be5-120"><a name="ionic"></a>Instellen van een app ionische v2</span><span class="sxs-lookup"><span data-stu-id="d4be5-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="d4be5-121">tooproperly configureren van een project ionische v2, eerst een eenvoudige app maken en toevoegen van Hallo Cordova-invoegtoepassing:</span><span class="sxs-lookup"><span data-stu-id="d4be5-121">tooproperly configure an Ionic v2 project, first create a basic app and add hello Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="d4be5-122">Toevoegen van de volgende regels te Hallo`app.component.ts` object toocreate Hallo-client:</span><span class="sxs-lookup"><span data-stu-id="d4be5-122">Add hello following lines too`app.component.ts` toocreate hello client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="d4be5-123">U kunt nu bouwen en uitvoeren van Hallo-project in de browser Hallo:</span><span class="sxs-lookup"><span data-stu-id="d4be5-123">You can now build and run hello project in hello browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="d4be5-124">Hello Azure Mobile Apps Cordova-invoegtoepassing biedt ondersteuning voor beide ionische v1- en v2-apps.</span><span class="sxs-lookup"><span data-stu-id="d4be5-124">hello Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="d4be5-125">Alleen apps Hallo ionische v2 aanvullende verklaring voor Hallo vereisen `WindowsAzure` object.</span><span class="sxs-lookup"><span data-stu-id="d4be5-125">Only hello Ionic v2 apps require the additional declaration for hello `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="d4be5-126"><a name="auth"></a>Procedure: verificatie van gebruikers</span><span class="sxs-lookup"><span data-stu-id="d4be5-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="d4be5-127">Azure App Service biedt ondersteuning voor verificatie en autorisatie van app-gebruikers met behulp van verschillende externe id-providers: Facebook, Google, Microsoft-Account en Twitter.</span><span class="sxs-lookup"><span data-stu-id="d4be5-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="d4be5-128">U kunt machtigingen instellen voor tabellen toorestrict toegang voor specifieke bewerkingen tooonly geverifieerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d4be5-128">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="d4be5-129">U kunt ook Hallo identiteit van autorisatieregels voor geverifieerde gebruikers tooimplement in server-scripts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d4be5-129">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="d4be5-130">Zie voor meer informatie, Hallo [aan de slag met verificatie] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d4be5-130">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="d4be5-131">Wanneer u verificatie gebruikt in een Apache Cordova-app, moet Hallo na Cordova plugins beschikbaar zijn:</span><span class="sxs-lookup"><span data-stu-id="d4be5-131">When using authentication in an Apache Cordova app, hello following Cordova plugins must be available:</span></span>

* <span data-ttu-id="d4be5-132">[cordova-invoegtoepassing-apparaat]</span><span class="sxs-lookup"><span data-stu-id="d4be5-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="d4be5-133">[cordova-invoegtoepassing-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="d4be5-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="d4be5-134">Twee verificatie stromen worden ondersteund: de stroom van een server en een client-stroom.</span><span class="sxs-lookup"><span data-stu-id="d4be5-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="d4be5-135">Hallo server stroom biedt Hallo eenvoudigste verificatie-ervaring, is afhankelijk van de webinterface verificatie Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="d4be5-135">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="d4be5-136">Hallo stroom kunt u betere integratie met apparaatspecifieke mogelijkheden, zoals single-sign-on zoals is afhankelijk van de provider-specifieke apparaat-specifieke SDK's.</span><span class="sxs-lookup"><span data-stu-id="d4be5-136">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="d4be5-137"><a name="configure-external-redirect-urls"></a>Procedure: het configureren van uw mobiele App Service voor externe Omleidings-URL's.</span><span class="sxs-lookup"><span data-stu-id="d4be5-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="d4be5-138">Verschillende soorten Apache Cordova-toepassingen gebruiken een loopback mogelijkheid toohandle die OAuth UI loopt.</span><span class="sxs-lookup"><span data-stu-id="d4be5-138">Several types of Apache Cordova applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="d4be5-139">OAuth UI-overdrachten op localhost problemen veroorzaken omdat Hallo verificatieservice alleen weet hoe tooutilize uw service standaard.</span><span class="sxs-lookup"><span data-stu-id="d4be5-139">OAuth UI flows on localhost cause problems since hello authentication service only knows how tooutilize your service by default.</span></span>  <span data-ttu-id="d4be5-140">Voorbeelden van problematisch OAuth UI stromen zijn:</span><span class="sxs-lookup"><span data-stu-id="d4be5-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="d4be5-141">Hallo Rimpel emulator.</span><span class="sxs-lookup"><span data-stu-id="d4be5-141">hello Ripple emulator.</span></span>
* <span data-ttu-id="d4be5-142">Live opnieuw laden met ionische.</span><span class="sxs-lookup"><span data-stu-id="d4be5-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="d4be5-143">Hallo mobiele back-end lokaal uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="d4be5-143">Running hello mobile backend locally</span></span>
* <span data-ttu-id="d4be5-144">Hallo mobiele back-end in een andere Azure App Service dan Hallo één verstrekken verificatie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d4be5-144">Running hello mobile backend in a different Azure App Service than hello one providing authentication.</span></span>

<span data-ttu-id="d4be5-145">Volg deze instructies tooadd uw lokale instellingen toohello configuratie:</span><span class="sxs-lookup"><span data-stu-id="d4be5-145">Follow these instructions tooadd your local settings toohello configuration:</span></span>

1. <span data-ttu-id="d4be5-146">Meld u bij toohello [Azure-portal]</span><span class="sxs-lookup"><span data-stu-id="d4be5-146">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="d4be5-147">Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="d4be5-147">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="d4be5-148">Klik op **hulpprogramma's**</span><span class="sxs-lookup"><span data-stu-id="d4be5-148">Click **Tools**</span></span>
4. <span data-ttu-id="d4be5-149">Klik op **resourceverkenner** in Hallo OBSERVE menu, klikt u **gaat**.</span><span class="sxs-lookup"><span data-stu-id="d4be5-149">Click **Resource explorer** in hello OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="d4be5-150">Een nieuw venster of tabblad wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="d4be5-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="d4be5-151">Vouw Hallo **config**, **authsettings** knooppunten voor uw site in de linkernavigatiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4be5-151">Expand hello **config**, **authsettings** nodes for your site in hello left-hand navigation.</span></span>
6. <span data-ttu-id="d4be5-152">Klik op **bewerken**</span><span class="sxs-lookup"><span data-stu-id="d4be5-152">Click **Edit**</span></span>
7. <span data-ttu-id="d4be5-153">Zoek naar Hallo 'allowedExternalRedirectUrls'-element.</span><span class="sxs-lookup"><span data-stu-id="d4be5-153">Look for hello "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="d4be5-154">Worden kan ingesteld toonull of een matrix met waarden.</span><span class="sxs-lookup"><span data-stu-id="d4be5-154">It may be set toonull or an array of values.</span></span>  <span data-ttu-id="d4be5-155">Hallo waarde toohello na waarde wijzigen:</span><span class="sxs-lookup"><span data-stu-id="d4be5-155">Change hello value toohello following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="d4be5-156">Hallo-URL's vervangen door Hallo-URL's van uw service.</span><span class="sxs-lookup"><span data-stu-id="d4be5-156">Replace hello URLs with hello URLs of your service.</span></span>  <span data-ttu-id="d4be5-157">Voorbeelden zijn "http://localhost: 3000' (voor Node.js-voorbeeld service Hallo) of 'http://localhost:4400' (voor Hallo Rimpel service).</span><span class="sxs-lookup"><span data-stu-id="d4be5-157">Examples include "http://localhost:3000" (for hello Node.js sample service), or "http://localhost:4400" (for hello Ripple service).</span></span>  <span data-ttu-id="d4be5-158">Deze URL's zijn echter voorbeelden - uw situatie, met inbegrip van Hallo diensten vermeld in de voorbeelden hello, kunnen afwijken.</span><span class="sxs-lookup"><span data-stu-id="d4be5-158">However, these URLs are examples - your situation, including for hello services mentioned in hello examples, may be different.</span></span>
8. <span data-ttu-id="d4be5-159">Klik op Hallo **lezen/schrijven** knop in Hallo rechterbovenhoek van het welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="d4be5-159">Click hello **Read/Write** button in hello top-right corner of hello screen.</span></span>
9. <span data-ttu-id="d4be5-160">Klik op Hallo groen **plaatsen** knop.</span><span class="sxs-lookup"><span data-stu-id="d4be5-160">Click hello green **PUT** button.</span></span>

<span data-ttu-id="d4be5-161">Hallo-instellingen worden op dit moment opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d4be5-161">hello settings are saved at this point.</span></span>  <span data-ttu-id="d4be5-162">Hallo-browservenster niet sluiten totdat Hallo-instellingen hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d4be5-162">Do not close hello browser window until hello settings have finished saving.</span></span>
<span data-ttu-id="d4be5-163">Ook deze loopback-URL's toohello CORS-instellingen voor uw App Service toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d4be5-163">Also add these loopback URLs toohello CORS settings for your App Service:</span></span>

1. <span data-ttu-id="d4be5-164">Meld u bij toohello [Azure-portal]</span><span class="sxs-lookup"><span data-stu-id="d4be5-164">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="d4be5-165">Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="d4be5-165">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="d4be5-166">de blade instellingen Hello wordt automatisch geopend.</span><span class="sxs-lookup"><span data-stu-id="d4be5-166">hello Settings blade opens automatically.</span></span>  <span data-ttu-id="d4be5-167">Als dit niet zo is, klikt u op **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="d4be5-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="d4be5-168">Klik op **CORS** onder Hallo API-menu.</span><span class="sxs-lookup"><span data-stu-id="d4be5-168">Click **CORS** under hello API menu.</span></span>
5. <span data-ttu-id="d4be5-169">Voer Hallo-URL die u wenst dat tooadd in Hallo daarvoor bestemde vak in en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="d4be5-169">Enter hello URL that you wish tooadd in hello box provided and press Enter.</span></span>
6. <span data-ttu-id="d4be5-170">Geef extra URL's desgewenst.</span><span class="sxs-lookup"><span data-stu-id="d4be5-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="d4be5-171">Klik op **opslaan** toosave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="d4be5-171">Click **Save** toosave hello settings.</span></span>

<span data-ttu-id="d4be5-172">Het duurt ongeveer 10-15 seconden voor Hallo nieuwe instellingen tootake effect.</span><span class="sxs-lookup"><span data-stu-id="d4be5-172">It takes approximately 10-15 seconds for hello new settings tootake effect.</span></span>

## <span data-ttu-id="d4be5-173"><a name="register-for-push"></a>Hoe: registreren voor pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="d4be5-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="d4be5-174">Hallo installeren [phonegap-invoegtoepassing-push] toohandle pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="d4be5-174">Install hello [phonegap-plugin-push] toohandle push notifications.</span></span>  <span data-ttu-id="d4be5-175">Deze invoegtoepassing gemakkelijk kan worden toegevoegd met de `cordova plugin add` opdracht op de opdrachtregel Hallo of via Hallo Git-invoegtoepassing installatieprogramma vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4be5-175">This plugin can be easily added using the `cordova plugin add` command on hello command line, or via hello Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="d4be5-176">De volgende code in uw Apache Cordova-app registreert uw apparaat voor pushmeldingen:</span><span class="sxs-lookup"><span data-stu-id="d4be5-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

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

<span data-ttu-id="d4be5-177">Hallo Notification Hubs SDK toosend pushmeldingen vanuit Hallo-server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d4be5-177">Use hello Notification Hubs SDK toosend push notifications from hello server.</span></span>  <span data-ttu-id="d4be5-178">Nooit pushmeldingen rechtstreeks vanuit clients verzenden.</span><span class="sxs-lookup"><span data-stu-id="d4be5-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="d4be5-179">Hierdoor kan dus worden gebruikte tootrigger een denial of service-aanval tegen Notification Hubs of Hallo PNS.</span><span class="sxs-lookup"><span data-stu-id="d4be5-179">Doing so could be used tootrigger a denial of service attack against Notification Hubs or hello PNS.</span></span>  <span data-ttu-id="d4be5-180">Hallo PNS kan verkeer als gevolg van dergelijke aanvallen been.</span><span class="sxs-lookup"><span data-stu-id="d4be5-180">hello PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="d4be5-181">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="d4be5-181">More information</span></span>

<span data-ttu-id="d4be5-182">U vindt gedetailleerde informatie voor API in onze [API-documentatie](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="d4be5-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

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
