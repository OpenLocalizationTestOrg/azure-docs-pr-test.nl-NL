---
title: "Azure AD v2.0 .NET AngularJS één pagina-app aan de slag | Microsoft Docs"
description: "Het bouwen van een hoek JS één pagina app die gebruikers met beide persoonlijke Microsoft-accounts en werk-of schoolaccounts aanmeldt."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 6a341781-278f-461b-92ca-7572a06e6852
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c68180c0ecabf5c0732f0db77ef1f3cc93be965b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---net"></a><span data-ttu-id="5a0fb-103">Aanmelden toevoegen aan een app met één pagina AngularJS - .NET</span><span class="sxs-lookup"><span data-stu-id="5a0fb-103">Add sign-in to an AngularJS single page app - .NET</span></span>
<span data-ttu-id="5a0fb-104">In dit artikel gaan we Meld u aan met ingeschakeld Microsoft-accounts toevoegen aan een AngularJS-app met behulp van het Azure Active Directory v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="5a0fb-105">Het v2.0-eindpunt kunt u voor het uitvoeren van een enkele integratie in uw app en verifiëren van gebruikers met een persoonlijke en zakelijke/school-account.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-105">The v2.0 endpoint enables you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="5a0fb-106">Dit voorbeeld is een eenvoudige takenlijst één pagina app waarmee taken worden opgeslagen in een back-end REST API, geschreven met .NET 4.5 MVC framework en beveiligd met OAuth bearer-tokens van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using the .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="5a0fb-107">De AngularJS-app gebruikt onze JavaScript-verificatiebibliotheek voor open-source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) te verwerken van het hele proces aanmelden en tokens voor het aanroepen van de REST-API te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="5a0fb-108">Hetzelfde patroon kan worden toegepast om te verifiëren bij andere REST-API's, zoals de [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5a0fb-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="5a0fb-109">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="5a0fb-110">Meer informatie over om te bepalen of moet u het v2.0-eindpunt, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="5a0fb-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="5a0fb-111">Downloaden</span><span class="sxs-lookup"><span data-stu-id="5a0fb-111">Download</span></span>
<span data-ttu-id="5a0fb-112">Om te beginnen, moet u downloaden en installeren van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-112">To get started, you'll need to download & install Visual Studio.</span></span>  <span data-ttu-id="5a0fb-113">Vervolgens kunt u een kloon of [downloaden](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) een geraamte app:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="5a0fb-114">De geraamte app bevat alle standaardcode voor een eenvoudige AngularJS-app, maar alle benodigde onderdelen identiteitsgerelateerde ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="5a0fb-115">Als u niet volgen wilt, kunt u in plaats daarvan klonen of [downloaden](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) voltooide voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="5a0fb-116">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="5a0fb-116">Register an app</span></span>
<span data-ttu-id="5a0fb-117">Maak eerst een app in de [App-Portal voor Wachtwoordregistratie](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="5a0fb-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="5a0fb-118">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-118">Make sure to:</span></span>

* <span data-ttu-id="5a0fb-119">Voeg de **Web** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="5a0fb-120">Voer de juiste **omleidings-URI**.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="5a0fb-121">De standaardwaarde voor dit voorbeeld is `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-121">The default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="5a0fb-122">Laat de **impliciete stromen toestaan** selectievakje ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="5a0fb-123">Noteer de **toepassings-ID** die is toegewezen aan uw app, moet u deze binnenkort.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="5a0fb-124">Adal.js installeren</span><span class="sxs-lookup"><span data-stu-id="5a0fb-124">Install adal.js</span></span>
<span data-ttu-id="5a0fb-125">Als u wilt starten, navigeert u gedownload projecteren en adal.js installeren.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="5a0fb-126">Als u hebt [bower](http://bower.io/) geïnstalleerd, kunt u alleen deze opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="5a0fb-127">Voor afhankelijkheid versie verschillen worden ontdekt, kiest u de hogere versie.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="5a0fb-128">U kunt ook kunt u handmatig downloaden [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) en [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="5a0fb-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="5a0fb-129">Beide bestanden toevoegt aan de `app/lib/adal-angular-experimental/dist` map van de `TodoSPA` project.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory of the `TodoSPA` project.</span></span>

<span data-ttu-id="5a0fb-130">Nu opent u het project in Visual Studio en adal.js aan het einde van de hoofdpagina hoofdtekst laden:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-130">Now open the project in Visual Studio, and load adal.js at the end of the main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="5a0fb-131">Instellen van de REST-API</span><span class="sxs-lookup"><span data-stu-id="5a0fb-131">Set up the REST API</span></span>
<span data-ttu-id="5a0fb-132">Terwijl we alles wordt ingesteld, krijgen we de werking van de REST-API-back-end.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-132">While we're setting things up, let's get the backend REST API working.</span></span>  <span data-ttu-id="5a0fb-133">Open in de hoofdmap van het project `web.config` en vervang de `audience` waarde.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-133">In the root of the project, open `web.config` and replace the `audience` value.</span></span>  <span data-ttu-id="5a0fb-134">De REST-API gebruikt deze waarde om tokens die worden ontvangen van de hoek app op AJAX-aanvragen te valideren.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-134">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="5a0fb-135">Dat is de tijd die we willen besteden bespreking van de werking van de REST-API.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-135">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="5a0fb-136">Maak rond in de code, maar als u meer informatie wilt over het beveiligen van web-API's in Azure AD, Bekijk gerust [in dit artikel](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="5a0fb-136">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="5a0fb-137">Gebruikers aanmelden</span><span class="sxs-lookup"><span data-stu-id="5a0fb-137">Sign users in</span></span>
<span data-ttu-id="5a0fb-138">Tijd voor de identiteitscode schrijven.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-138">Time to write some identity code.</span></span>  <span data-ttu-id="5a0fb-139">Hebt misschien u al opgemerkt dat adal.js bevat een AngularJS-provider, waarmee mooi met Hoekvormige routering mechanismen speelt.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="5a0fb-140">Door de adal-module toe te voegen aan de app start:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-140">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="5a0fb-141">U kunt nu initialiseren de `adalProvider` met toepassings-ID:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-141">You can now initialize the `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="5a0fb-142">Goede, adal.js heeft nu alle informatie die nodig is voor het beveiligen van uw app en meld u aan gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-142">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="5a0fb-143">Als u wilt afdwingen voor een bepaalde route in de app aanmelden, is een kwestie van één regel code:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-143">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="5a0fb-144">Nu wanneer een gebruiker klikt op de `TodoList` koppeling adal.js worden automatisch omgeleid naar Azure AD voor aanmelden indien nodig.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-144">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="5a0fb-145">U kunt ook expliciet aanmelden en afmeldingsaanvragen te verzenden door aan te roepen adal.js in uw domeincontrollers verzenden:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="5a0fb-146">Gebruikersgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="5a0fb-146">Display user info</span></span>
<span data-ttu-id="5a0fb-147">Nu dat de gebruiker is aangemeld, moet u waarschijnlijk voor toegang tot gegevens van de aangemelde gebruiker de verificatie in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-147">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="5a0fb-148">Adal.js beschrijft deze informatie voor u in de `userInfo` object.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-148">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="5a0fb-149">Voor toegang tot dit object in een weergave, moet u eerst adal.js toevoegen aan het bereik van de hoofdmap van de bijbehorende controller:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-149">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="5a0fb-150">En u kunt rechtstreeks verband met de `userInfo` object in de weergave:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-150">Then you can directly address the `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="5a0fb-151">U kunt ook de `userInfo` object om te bepalen of aan de gebruiker is aangemeld of niet.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-151">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

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

## <a name="call-the-rest-api"></a><span data-ttu-id="5a0fb-152">De REST-API aanroepen</span><span class="sxs-lookup"><span data-stu-id="5a0fb-152">Call the REST API</span></span>
<span data-ttu-id="5a0fb-153">Ten slotte is het tijd om sommige tokens verkrijgen en roept u de REST-API als u wilt maken, lezen, bijwerken en verwijderen van taken.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-153">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="5a0fb-154">Ook goed nieuws!</span><span class="sxs-lookup"><span data-stu-id="5a0fb-154">Well guess what?</span></span>  <span data-ttu-id="5a0fb-155">U hoeft te doen *een ding*.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-155">You don't have to do *a thing*.</span></span>  <span data-ttu-id="5a0fb-156">Adal.js zorgt automatisch voor het ophalen, opslaan in cache en vernieuwen van tokens.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="5a0fb-157">Deze ook zorgt voor het koppelen van deze tokens aan uitgaande AJAX-aanvragen die u naar de REST-API verzendt.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-157">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="5a0fb-158">Hoe werkt dit?</span><span class="sxs-lookup"><span data-stu-id="5a0fb-158">How exactly does this work?</span></span> <span data-ttu-id="5a0fb-159">Het is alle dankzij de magie van [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), waardoor adal.js voor het transformeren van uitgaande en binnenkomende HTTP-berichten.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-159">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="5a0fb-160">Bovendien adal.js wordt ervan uitgegaan dat alle aanvragen tot hetzelfde domein verzenden als tokens die zijn bedoeld voor dezelfde toepassings-ID als de AngularJS-app moet worden gebruikt in het venster.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-160">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="5a0fb-161">Daarom hebben we gebruikt dezelfde toepassings-ID in de hoek app en in de NodeJS REST-API.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-161">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="5a0fb-162">Natuurlijk kunt u dit gedrag negeren en vertel adal.js ophalen van tokens van andere REST-API's zo nodig - maar doet voor dit eenvoudige scenario de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-162">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="5a0fb-163">Hier volgt een codefragment die laat hoe eenvoudig het is zien voor het verzenden van aanvragen met bearer-tokens van Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-163">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="5a0fb-164">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-164">Congratulations!</span></span>  <span data-ttu-id="5a0fb-165">Uw Azure AD-geïntegreerde één pagina app is nu voltooid.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="5a0fb-166">Opwekken op. een boeg.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="5a0fb-167">U kunt verificatie van gebruikers, veilig aanroepen van de back-end REST-API met OpenID Connect en basisinformatie over de gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="5a0fb-168">Buiten het vak biedt ondersteuning voor elke gebruiker met een persoonlijk Microsoft-Account of een werk schoolaccount van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-168">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="5a0fb-169">Voer de app en navigeer in een browser naar `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-169">Run the app, and in a browser navigate to `https://localhost:44326/`.</span></span>  <span data-ttu-id="5a0fb-170">Meld u aan met een persoonlijk Microsoft-account of een werk/school-account.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="5a0fb-171">Taken toevoegen aan de takenlijst van de gebruiker en meld u af.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-171">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="5a0fb-172">Probeer aanmelden met het andere type account.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-172">Try signing in with the other type of account.</span></span> <span data-ttu-id="5a0fb-173">Als u een Azure AD-tenant maken werk/school gebruikers, moet [Lees hoe u een hier](active-directory-howto-tenant.md) (het is gratis).</span><span class="sxs-lookup"><span data-stu-id="5a0fb-173">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="5a0fb-174">Om door te gaan leren over het v2.0-eindpunt head terug naar onze [v2.0 ontwikkelaarshandleiding](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a0fb-174">To continue learning about the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="5a0fb-175">Voor aanvullende bronnen voor uitchecken:</span><span class="sxs-lookup"><span data-stu-id="5a0fb-175">For additional resources, check out:</span></span>

* [<span data-ttu-id="5a0fb-176">Azure-voorbeelden op GitHub >></span><span class="sxs-lookup"><span data-stu-id="5a0fb-176">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="5a0fb-177">Azure AD op de Stack-overloop >></span><span class="sxs-lookup"><span data-stu-id="5a0fb-177">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="5a0fb-178">Azure AD-documentatie op [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="5a0fb-178">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="5a0fb-179">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="5a0fb-179">Get security updates for our products</span></span>
<span data-ttu-id="5a0fb-180">We raden u aan in te stellen dat u meldingen ontvangt wanneer er beveiligingsincidenten optreden. Ga hiervoor naar [deze pagina](https://technet.microsoft.com/security/dd252948) en abonneer u op Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="5a0fb-180">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

