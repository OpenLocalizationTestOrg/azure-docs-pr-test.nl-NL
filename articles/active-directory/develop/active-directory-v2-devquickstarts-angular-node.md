---
title: "aaaAzure AD v2.0 NodeJS AngularJS één pagina app aan de slag | Microsoft Docs"
description: "Hoe toobuild een hoek JS één pagina app die zich aanmeldt gebruikers met beide persoonlijke Microsoft-accounts en werk of schoolaccounts."
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 1ab450caf08ab05fba140b94b1b8de652e99cbc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a><span data-ttu-id="5c0ad-103">Aanmelden tooan AngularJS één pagina app - NodeJS toevoegen</span><span class="sxs-lookup"><span data-stu-id="5c0ad-103">Add sign-in tooan AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="5c0ad-104">In dit artikel gaan we Meld u aan met ingeschakeld Microsoft-accounts tooan AngularJS app met hello Azure Active Directory v2.0-eindpunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="5c0ad-105">Hallo v2.0-eindpunt kunt u een één-integratie in uw app tooperform en verifiëren van gebruikers met een persoonlijke en zakelijke/school-account.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-105">hello v2.0 endpoint enable you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="5c0ad-106">Dit voorbeeld is een eenvoudige takenlijst één pagina app waarmee taken worden opgeslagen in een back-end REST API, geschreven in NodeJS en beveiligd met OAuth bearer-tokens van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="5c0ad-107">Hallo AngularJS app gebruikt onze JavaScript-verificatiebibliotheek voor open-source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle Hallo gehele aanmelden proces en tokens voor aanroepen Hallo REST-API te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="5c0ad-108">Hallo hetzelfde patroon kan worden toegepast tooauthenticate tooother REST-API's, zoals Hallo [Microsoft Graph](https://graph.microsoft.com) of hello Azure Resource Manager-API's.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com) or hello Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="5c0ad-109">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="5c0ad-110">toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="5c0ad-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="5c0ad-111">Downloaden</span><span class="sxs-lookup"><span data-stu-id="5c0ad-111">Download</span></span>
<span data-ttu-id="5c0ad-112">tooget gestart, moet u toodownload & installatie [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="5c0ad-112">tooget started, you'll need toodownload & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="5c0ad-113">Vervolgens kunt u een kloon of [downloaden](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) een geraamte app:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="5c0ad-114">Hallo geraamte app bevat alle Hallo standaardcode voor een eenvoudige AngularJS-app, maar alle Hallo identity-gerelateerde onderdelen ontbreken.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="5c0ad-115">Als u toofollow langs niet wilt, kunt u in plaats daarvan klonen of [downloaden](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) voorbeeld Hallo voltooid.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="5c0ad-116">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="5c0ad-116">Register an app</span></span>
<span data-ttu-id="5c0ad-117">Maak eerst een app in Hallo [App-Portal voor Wachtwoordregistratie](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="5c0ad-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="5c0ad-118">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-118">Make sure to:</span></span>

* <span data-ttu-id="5c0ad-119">Hallo toevoegen **Web** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="5c0ad-120">Voer de juiste Hallo **omleidings-URI**.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="5c0ad-121">Hallo standaardwaarde voor dit voorbeeld is `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-121">hello default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="5c0ad-122">Hallo laat **impliciete stromen toestaan** selectievakje ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="5c0ad-123">Noteer Hallo **toepassings-ID** die is toegewezen tooyour-app, moet u deze binnenkort.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="5c0ad-124">Adal.js installeren</span><span class="sxs-lookup"><span data-stu-id="5c0ad-124">Install adal.js</span></span>
<span data-ttu-id="5c0ad-125">toostart, gaat u tooproject die u hebt gedownload en adal.js installeren.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="5c0ad-126">Als u hebt [bower](http://bower.io/) geïnstalleerd, kunt u alleen deze opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="5c0ad-127">Voor afhankelijkheid versie verschillen worden ontdekt, kiest u Hallo hogere versie.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="5c0ad-128">U kunt ook kunt u handmatig downloaden [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) en [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="5c0ad-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="5c0ad-129">Toevoegen van beide bestanden toohello `app/lib/adal-angular-experimental/dist` directory.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="5c0ad-130">Nu Hallo-project in uw favoriete teksteditor openen en laden adal.js achter Hallo Hallo pagina instantie:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-130">Now open hello project in your favorite text editor, and load adal.js at hello end of hello page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="5c0ad-131">Hallo REST-API instellen</span><span class="sxs-lookup"><span data-stu-id="5c0ad-131">Set up hello REST API</span></span>
<span data-ttu-id="5c0ad-132">Terwijl we alles wordt ingesteld, kunt get Hallo back-end REST-API werken.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-132">While we're setting things up, lets get hello backend REST API working.</span></span>  <span data-ttu-id="5c0ad-133">In een opdrachtprompt door alle benodigde hello-pakketten te installeren door te voeren (Zorg ervoor dat u zich in de hoogste map Hallo van Hallo-project):</span><span class="sxs-lookup"><span data-stu-id="5c0ad-133">In a command prompt, install all hello necessary packages by running (make sure you're in hello top-level directory of hello project):</span></span>

```
npm install
```

<span data-ttu-id="5c0ad-134">Open nu `config.js` en vervang Hallo `audience` waarde:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-134">Now open `config.js` and replace hello `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="5c0ad-135">Hallo REST-API maakt gebruik van deze waarde toovalidate tokens die worden ontvangen van Hallo Hoekvormige app op AJAX-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-135">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>  <span data-ttu-id="5c0ad-136">Houd er rekening mee dat deze eenvoudige REST-API worden opgeslagen gegevens in het geheugen - dus elke keer toostop Hallo-server, verliest u alle eerder gemaakte taken.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-136">Note that this simple REST API stores data in-memory - so each time toostop hello server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="5c0ad-137">Dit is alles Hallo tijd gaan we toospend bespreking van de werking van Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-137">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="5c0ad-138">Gratis toopoke rond denken in Hallo code, maar als u meer over het beveiligen van web-API's met Azure AD toolearn wilt, Bekijk [in dit artikel](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="5c0ad-138">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="5c0ad-139">Gebruikers aanmelden</span><span class="sxs-lookup"><span data-stu-id="5c0ad-139">Sign users in</span></span>
<span data-ttu-id="5c0ad-140">Tijd toowrite identiteitscode.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-140">Time toowrite some identity code.</span></span>  <span data-ttu-id="5c0ad-141">Hebt misschien u al opgemerkt dat adal.js bevat een AngularJS-provider, waarmee mooi met Hoekvormige routering mechanismen speelt.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="5c0ad-142">Starten door Hallo adal module toohello app toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-142">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="5c0ad-143">U kunt nu Hallo initialiseren `adalProvider` met toepassings-ID:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-143">You can now initialize hello `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for hello public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // hello 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from hello registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - hello default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="5c0ad-144">Goede nu adal.js alle informatie over het Hallo heeft moet toosecure uw app en meld u aan gebruikers in.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-144">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="5c0ad-145">aanmelden voor een bepaalde route in alle duurt het Hallo-app tooforce is één regel code:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-145">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that hello user must be logged in tooaccess hello route
})

...
```

<span data-ttu-id="5c0ad-146">Nu wanneer een gebruiker klikt op Hallo `TodoList` koppeling adal.js worden automatisch omgeleid tooAzure AD voor aanmelden indien nodig.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-146">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="5c0ad-147">U kunt ook expliciet aanmelden en afmeldingsaanvragen te verzenden door aan te roepen adal.js in uw domeincontrollers verzenden:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js hello same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect hello user toosign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect hello user toolog out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="5c0ad-148">Gebruikersgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="5c0ad-148">Display user info</span></span>
<span data-ttu-id="5c0ad-149">Nu dat hello gebruiker is aangemeld, moet waarschijnlijk u tooaccess Hallo aangemelde gebruiker de verificatiegegevens in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-149">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="5c0ad-150">Adal.js beschrijft deze informatie voor u in Hallo `userInfo` object.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-150">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="5c0ad-151">tooaccess dit object in een weergave eerst adal.js toohello hoofdmap bereik van de bijbehorende controller Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-151">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="5c0ad-152">Vervolgens kunt u rechtstreeks hello te houden `userInfo` object in de weergave:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-152">Then you can directly address hello `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get hello user's profile information from hello ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="5c0ad-153">U kunt ook Hallo `userInfo` toodetermine object als het Hallo-gebruiker is aangemeld of niet.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-153">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use hello ADAL userInfo object tooshow hello right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-hello-rest-api"></a><span data-ttu-id="5c0ad-154">Hallo REST-API aanroepen</span><span class="sxs-lookup"><span data-stu-id="5c0ad-154">Call hello REST API</span></span>
<span data-ttu-id="5c0ad-155">Ten slotte is het tijd tooget sommige tokens en aanroep Hallo toocreate REST-API, lezen, bijwerken en verwijderen van taken.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-155">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="5c0ad-156">Ook goed nieuws!</span><span class="sxs-lookup"><span data-stu-id="5c0ad-156">Well guess what?</span></span>  <span data-ttu-id="5c0ad-157">U hebt geen toodo *een ding*.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-157">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="5c0ad-158">Adal.js zorgt automatisch voor het ophalen, opslaan in cache en vernieuwen van tokens.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="5c0ad-159">Deze ook zorgt voor het koppelen van deze tokens die toooutgoing AJAX-aanvragen toohello REST-API te sturen.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-159">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="5c0ad-160">Hoe werkt dit?</span><span class="sxs-lookup"><span data-stu-id="5c0ad-160">How exactly does this work?</span></span> <span data-ttu-id="5c0ad-161">Alle Bedankt toohello magie van is [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), waardoor adal.js tootransform uitgaande en binnenkomende HTTP-berichten.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-161">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="5c0ad-162">Bovendien adal.js wordt aangenomen dat de verzoeken van toohello verzenden hetzelfde domein als Hallo-venster moet tokens die zijn bedoeld voor gebruik Hallo dezelfde toepassings-ID zoals Hallo AngularJS-app.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-162">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="5c0ad-163">Daarom hebben we Hallo gebruikt dezelfde toepassings-ID in beide Hoekvormige app hello en in Hallo NodeJS REST-API.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-163">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="5c0ad-164">Natuurlijk kunt u dit gedrag negeren en vertel adal.js tooget tokens voor andere REST-API's zo nodig - maar voor deze eenvoudige scenario Hallo standaardwaarden doet.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-164">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="5c0ad-165">Hier volgt een codefragment die laat zien hoe eenvoudig het is toosend aanvragen met bearer-tokens van Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-165">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="5c0ad-166">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-166">Congratulations!</span></span>  <span data-ttu-id="5c0ad-167">Uw Azure AD-geïntegreerde één pagina app is nu voltooid.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="5c0ad-168">Opwekken op. een boeg.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="5c0ad-169">U kunt verificatie van gebruikers, veilig aanroepen van de back-end REST-API met OpenID Connect en basisinformatie over Hallo gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="5c0ad-170">Out of box hello, biedt ondersteuning voor elke gebruiker met een persoonlijk Microsoft-Account of een werk schoolaccount van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-170">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="5c0ad-171">Probeer app Hallo door te voeren:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-171">Give hello app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="5c0ad-172">In een browser navigeren te`http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-172">In a browser navigate too`http://localhost:8080`.</span></span>  <span data-ttu-id="5c0ad-173">Meld u aan met een persoonlijk Microsoft-account of een werk/school-account.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="5c0ad-174">Takenlijst taken toohello gebruiker toevoegen en meld u af.  Meld u aan met Hallo andere type account.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-174">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="5c0ad-175">Als u een Azure AD-tenant toocreate werk/school-gebruikers moet [meer informatie over hoe een hier tooget](active-directory-howto-tenant.md) (het is gratis).</span><span class="sxs-lookup"><span data-stu-id="5c0ad-175">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="5c0ad-176">toocontinue leren over Hallo Hallo v2.0-eindpunt, head back tooour [v2.0 ontwikkelaarshandleiding](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c0ad-176">toocontinue learning about hello hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="5c0ad-177">Voor aanvullende bronnen voor uitchecken:</span><span class="sxs-lookup"><span data-stu-id="5c0ad-177">For additional resources, check out:</span></span>

* [<span data-ttu-id="5c0ad-178">Azure-voorbeelden op GitHub >></span><span class="sxs-lookup"><span data-stu-id="5c0ad-178">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="5c0ad-179">Azure AD op de Stack-overloop >></span><span class="sxs-lookup"><span data-stu-id="5c0ad-179">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="5c0ad-180">Azure AD-documentatie op [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="5c0ad-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="5c0ad-181">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="5c0ad-181">Get security updates for our products</span></span>
<span data-ttu-id="5c0ad-182">We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-182">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

