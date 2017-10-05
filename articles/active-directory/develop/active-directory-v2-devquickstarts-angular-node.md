---
title: "Azure AD v2.0 NodeJS AngularJS één pagina app aan de slag | Microsoft Docs"
description: "Het bouwen van een hoek JS één pagina app die gebruikers met beide persoonlijke Microsoft-accounts en werk-of schoolaccounts aanmeldt."
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
ms.openlocfilehash: 0e90171afd9c4c782fbb18375ab2d147497ef442
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---nodejs"></a><span data-ttu-id="1a6f4-103">Aanmelden toevoegen aan een app met één pagina AngularJS - NodeJS</span><span class="sxs-lookup"><span data-stu-id="1a6f4-103">Add sign-in to an AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="1a6f4-104">In dit artikel gaan we Meld u aan met ingeschakeld Microsoft-accounts toevoegen aan een AngularJS-app met behulp van het Azure Active Directory v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="1a6f4-105">het v2.0-eindpunt kunt u een één-integratie in uw app uitvoeren en gebruikers met een persoonlijke en zakelijke/school-account te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-105">the v2.0 endpoint enable you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="1a6f4-106">Dit voorbeeld is een eenvoudige takenlijst één pagina app waarmee taken worden opgeslagen in een back-end REST API, geschreven in NodeJS en beveiligd met OAuth bearer-tokens van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="1a6f4-107">De AngularJS-app gebruikt onze JavaScript-verificatiebibliotheek voor open-source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) te verwerken van het hele proces aanmelden en tokens voor het aanroepen van de REST-API te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="1a6f4-108">Hetzelfde patroon kan worden toegepast om te verifiëren bij andere REST-API's, zoals de [Microsoft Graph](https://graph.microsoft.com) of de Azure Resource Manager-API's.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com) or the Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="1a6f4-109">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="1a6f4-110">Meer informatie over om te bepalen of moet u het v2.0-eindpunt, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="1a6f4-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="1a6f4-111">Downloaden</span><span class="sxs-lookup"><span data-stu-id="1a6f4-111">Download</span></span>
<span data-ttu-id="1a6f4-112">Om te beginnen, moet u downloaden en installeren [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="1a6f4-112">To get started, you'll need to download & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="1a6f4-113">Vervolgens kunt u een kloon of [downloaden](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) een geraamte app:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="1a6f4-114">De geraamte app bevat alle standaardcode voor een eenvoudige AngularJS-app, maar alle benodigde onderdelen identiteitsgerelateerde ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="1a6f4-115">Als u niet volgen wilt, kunt u in plaats daarvan klonen of [downloaden](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) voltooide voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="1a6f4-116">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="1a6f4-116">Register an app</span></span>
<span data-ttu-id="1a6f4-117">Maak eerst een app in de [App-Portal voor Wachtwoordregistratie](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="1a6f4-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="1a6f4-118">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-118">Make sure to:</span></span>

* <span data-ttu-id="1a6f4-119">Voeg de **Web** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="1a6f4-120">Voer de juiste **omleidings-URI**.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="1a6f4-121">De standaardwaarde voor dit voorbeeld is `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-121">The default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="1a6f4-122">Laat de **impliciete stromen toestaan** selectievakje ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="1a6f4-123">Noteer de **toepassings-ID** die is toegewezen aan uw app, moet u deze binnenkort.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="1a6f4-124">Adal.js installeren</span><span class="sxs-lookup"><span data-stu-id="1a6f4-124">Install adal.js</span></span>
<span data-ttu-id="1a6f4-125">Als u wilt starten, navigeert u gedownload projecteren en adal.js installeren.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="1a6f4-126">Als u hebt [bower](http://bower.io/) geïnstalleerd, kunt u alleen deze opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="1a6f4-127">Voor afhankelijkheid versie verschillen worden ontdekt, kiest u de hogere versie.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="1a6f4-128">U kunt ook kunt u handmatig downloaden [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) en [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="1a6f4-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="1a6f4-129">Beide bestanden toevoegt aan de `app/lib/adal-angular-experimental/dist` directory.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="1a6f4-130">Open het project in uw favoriete teksteditor nu en adal.js aan het einde van de Paginahoofdtekst van de te laden:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-130">Now open the project in your favorite text editor, and load adal.js at the end of the page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="1a6f4-131">Instellen van de REST-API</span><span class="sxs-lookup"><span data-stu-id="1a6f4-131">Set up the REST API</span></span>
<span data-ttu-id="1a6f4-132">Terwijl we alles wordt ingesteld, kunt de back-end REST-API kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-132">While we're setting things up, lets get the backend REST API working.</span></span>  <span data-ttu-id="1a6f4-133">In een opdrachtprompt, installeert u de vereiste pakketten door te voeren (Zorg ervoor dat u zich in de map op het hoogste niveau van het project):</span><span class="sxs-lookup"><span data-stu-id="1a6f4-133">In a command prompt, install all the necessary packages by running (make sure you're in the top-level directory of the project):</span></span>

```
npm install
```

<span data-ttu-id="1a6f4-134">Open nu `config.js` en vervang de `audience` waarde:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-134">Now open `config.js` and replace the `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with the Application ID from the registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="1a6f4-135">De REST-API gebruikt deze waarde om tokens die worden ontvangen van de hoek app op AJAX-aanvragen te valideren.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-135">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>  <span data-ttu-id="1a6f4-136">Opmerking waarop deze eenvoudige REST-API worden opgeslagen gegevens in het geheugen - dus elke tijd voor het stoppen van de server, verliest u alle eerder gemaakte taken.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-136">Note that this simple REST API stores data in-memory - so each time to stop the server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="1a6f4-137">Dat is de tijd die we willen besteden bespreking van de werking van de REST-API.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-137">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="1a6f4-138">Maak rond in de code, maar als u meer informatie wilt over het beveiligen van web-API's in Azure AD, Bekijk gerust [in dit artikel](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="1a6f4-138">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="1a6f4-139">Gebruikers aanmelden</span><span class="sxs-lookup"><span data-stu-id="1a6f4-139">Sign users in</span></span>
<span data-ttu-id="1a6f4-140">Tijd voor de identiteitscode schrijven.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-140">Time to write some identity code.</span></span>  <span data-ttu-id="1a6f4-141">Hebt misschien u al opgemerkt dat adal.js bevat een AngularJS-provider, waarmee mooi met Hoekvormige routering mechanismen speelt.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="1a6f4-142">Door de adal-module toe te voegen aan de app start:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-142">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="1a6f4-143">U kunt nu initialiseren de `adalProvider` met toepassings-ID:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-143">You can now initialize the `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for the public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // The 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from the registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - the default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="1a6f4-144">Goede, adal.js heeft nu alle informatie die nodig is voor het beveiligen van uw app en meld u aan gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-144">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="1a6f4-145">Als u wilt afdwingen voor een bepaalde route in de app aanmelden, is een kwestie van één regel code:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-145">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that the user must be logged in to access the route
})

...
```

<span data-ttu-id="1a6f4-146">Nu wanneer een gebruiker klikt op de `TodoList` koppeling adal.js worden automatisch omgeleid naar Azure AD voor aanmelden indien nodig.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-146">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="1a6f4-147">U kunt ook expliciet aanmelden en afmeldingsaanvragen te verzenden door aan te roepen adal.js in uw domeincontrollers verzenden:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js the same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect the user to sign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect the user to log out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="1a6f4-148">Gebruikersgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="1a6f4-148">Display user info</span></span>
<span data-ttu-id="1a6f4-149">Nu dat de gebruiker is aangemeld, moet u waarschijnlijk voor toegang tot gegevens van de aangemelde gebruiker de verificatie in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-149">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="1a6f4-150">Adal.js beschrijft deze informatie voor u in de `userInfo` object.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-150">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="1a6f4-151">Voor toegang tot dit object in een weergave, moet u eerst adal.js toevoegen aan het bereik van de hoofdmap van de bijbehorende controller:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-151">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="1a6f4-152">En u kunt rechtstreeks verband met de `userInfo` object in de weergave:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-152">Then you can directly address the `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get the user's profile information from the ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="1a6f4-153">U kunt ook de `userInfo` object om te bepalen of aan de gebruiker is aangemeld of niet.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-153">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use the ADAL userInfo object to show the right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-the-rest-api"></a><span data-ttu-id="1a6f4-154">De REST-API aanroepen</span><span class="sxs-lookup"><span data-stu-id="1a6f4-154">Call the REST API</span></span>
<span data-ttu-id="1a6f4-155">Ten slotte is het tijd om sommige tokens verkrijgen en roept u de REST-API als u wilt maken, lezen, bijwerken en verwijderen van taken.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-155">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="1a6f4-156">Ook goed nieuws!</span><span class="sxs-lookup"><span data-stu-id="1a6f4-156">Well guess what?</span></span>  <span data-ttu-id="1a6f4-157">U hoeft te doen *een ding*.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-157">You don't have to do *a thing*.</span></span>  <span data-ttu-id="1a6f4-158">Adal.js zorgt automatisch voor het ophalen, opslaan in cache en vernieuwen van tokens.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="1a6f4-159">Deze ook zorgt voor het koppelen van deze tokens aan uitgaande AJAX-aanvragen die u naar de REST-API verzendt.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-159">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="1a6f4-160">Hoe werkt dit?</span><span class="sxs-lookup"><span data-stu-id="1a6f4-160">How exactly does this work?</span></span> <span data-ttu-id="1a6f4-161">Het is alle dankzij de magie van [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), waardoor adal.js voor het transformeren van uitgaande en binnenkomende HTTP-berichten.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-161">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="1a6f4-162">Bovendien adal.js wordt ervan uitgegaan dat alle aanvragen tot hetzelfde domein verzenden als tokens die zijn bedoeld voor dezelfde toepassings-ID als de AngularJS-app moet worden gebruikt in het venster.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-162">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="1a6f4-163">Daarom hebben we gebruikt dezelfde toepassings-ID in de hoek app en in de NodeJS REST-API.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-163">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="1a6f4-164">Natuurlijk kunt u dit gedrag negeren en vertel adal.js ophalen van tokens van andere REST-API's zo nodig - maar doet voor dit eenvoudige scenario de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-164">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="1a6f4-165">Hier volgt een codefragment die laat hoe eenvoudig het is zien voor het verzenden van aanvragen met bearer-tokens van Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-165">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="1a6f4-166">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-166">Congratulations!</span></span>  <span data-ttu-id="1a6f4-167">Uw Azure AD-geïntegreerde één pagina app is nu voltooid.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="1a6f4-168">Opwekken op. een boeg.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="1a6f4-169">U kunt verificatie van gebruikers, veilig aanroepen van de back-end REST-API met OpenID Connect en basisinformatie over de gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="1a6f4-170">Buiten het vak biedt ondersteuning voor elke gebruiker met een persoonlijk Microsoft-Account of een werk schoolaccount van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-170">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="1a6f4-171">Probeer de app door te voeren:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-171">Give the app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="1a6f4-172">Navigeer in een browser naar `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-172">In a browser navigate to `http://localhost:8080`.</span></span>  <span data-ttu-id="1a6f4-173">Meld u aan met een persoonlijk Microsoft-account of een werk/school-account.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="1a6f4-174">Taken toevoegen aan de takenlijst van de gebruiker en meld u af.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-174">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="1a6f4-175">Probeer aanmelden met het andere type account.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-175">Try signing in with the other type of account.</span></span> <span data-ttu-id="1a6f4-176">Als u een Azure AD-tenant maken werk/school gebruikers, moet [Lees hoe u een hier](active-directory-howto-tenant.md) (het is gratis).</span><span class="sxs-lookup"><span data-stu-id="1a6f4-176">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="1a6f4-177">Om door te gaan leren over de het v2.0-eindpunt, head terug naar onze [v2.0 ontwikkelaarshandleiding](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a6f4-177">To continue learning about the the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="1a6f4-178">Voor aanvullende bronnen voor uitchecken:</span><span class="sxs-lookup"><span data-stu-id="1a6f4-178">For additional resources, check out:</span></span>

* [<span data-ttu-id="1a6f4-179">Azure-voorbeelden op GitHub >></span><span class="sxs-lookup"><span data-stu-id="1a6f4-179">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="1a6f4-180">Azure AD op de Stack-overloop >></span><span class="sxs-lookup"><span data-stu-id="1a6f4-180">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="1a6f4-181">Azure AD-documentatie op [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="1a6f4-181">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="1a6f4-182">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="1a6f4-182">Get security updates for our products</span></span>
<span data-ttu-id="1a6f4-183">We raden u aan in te stellen dat u meldingen ontvangt wanneer er beveiligingsincidenten optreden. Ga hiervoor naar [deze pagina](https://technet.microsoft.com/security/dd252948) en abonneer u op Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="1a6f4-183">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

