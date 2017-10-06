---
title: "aaaAzure AD v2.0 .NET AngularJS één pagina app aan de slag | Microsoft Docs"
description: "Hoe toobuild een hoek JS één pagina app die zich aanmeldt gebruikers met beide persoonlijke Microsoft-accounts en werk of schoolaccounts."
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
ms.openlocfilehash: bd3fc8dce91eb0bedcbfed47a9b3ef52c5568c6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a>Aanmelden tooan AngularJS één pagina app - .NET toevoegen
In dit artikel gaan we Meld u aan met ingeschakeld Microsoft-accounts tooan AngularJS app met hello Azure Active Directory v2.0-eindpunt toevoegen.  Hallo v2.0-eindpunt kunt u een één-integratie in uw app tooperform en verifiëren van gebruikers met een persoonlijke en zakelijke/school-account.

Dit voorbeeld is een eenvoudige takenlijst één pagina app waarmee taken worden opgeslagen in een back-end REST API, geschreven met .NET 4.5 MVC-framework Hallo en beveiligd met OAuth bearer-tokens van Azure AD.  Hallo AngularJS app gebruikt onze JavaScript-verificatiebibliotheek voor open-source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle Hallo gehele aanmelden proces en tokens voor aanroepen Hallo REST-API te verkrijgen.  Hallo hetzelfde patroon kan worden toegepast tooauthenticate tooother REST-API's, zoals Hallo [Microsoft Graph](https://graph.microsoft.com).

> [!NOTE]
> Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.  toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 
> 

## <a name="download"></a>Downloaden
tooget gestart, hebt u nodig toodownload & Installeer Visual Studio.  Vervolgens kunt u een kloon of [downloaden](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) een geraamte app:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

Hallo geraamte app bevat alle Hallo standaardcode voor een eenvoudige AngularJS-app, maar alle Hallo identity-gerelateerde onderdelen ontbreken.  Als u toofollow langs niet wilt, kunt u in plaats daarvan klonen of [downloaden](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) voorbeeld Hallo voltooid.

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a>Een app registreren
Maak eerst een app in Hallo [App-Portal voor Wachtwoordregistratie](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).  Zorg ervoor dat:

* Hallo toevoegen **Web** platform voor uw app.
* Voer de juiste Hallo **omleidings-URI**. Hallo standaardwaarde voor dit voorbeeld is `https://localhost:44326/`.
* Hallo laat **impliciete stromen toestaan** selectievakje ingeschakeld. 

Noteer Hallo **toepassings-ID** die is toegewezen tooyour-app, moet u deze binnenkort. 

## <a name="install-adaljs"></a>Adal.js installeren
toostart, gaat u tooproject die u hebt gedownload en adal.js installeren.  Als u hebt [bower](http://bower.io/) geïnstalleerd, kunt u alleen deze opdracht uitvoeren.  Voor afhankelijkheid versie verschillen worden ontdekt, kiest u Hallo hogere versie.

```
bower install adal-angular#experimental
```

U kunt ook kunt u handmatig downloaden [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) en [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).  Toevoegen van beide bestanden toohello `app/lib/adal-angular-experimental/dist` map Hallo `TodoSPA` project.

Nu Hallo project openen in Visual Studio en adal.js achter Hallo Hallo hoofdpagina van hoofdtekst laden:

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a>Hallo REST-API instellen
Terwijl we alles wordt ingesteld, gaan we Hallo back-end REST-API werkende worden opgehaald.  Open in de hoofdmap van de Hallo van Hallo-project, `web.config` en vervang Hallo `audience` waarde.  Hallo REST-API maakt gebruik van deze waarde toovalidate tokens die worden ontvangen van Hallo Hoekvormige app op AJAX-aanvragen.

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

Dit is alles Hallo tijd gaan we toospend bespreking van de werking van Hallo REST-API.  Gratis toopoke rond denken in Hallo code, maar als u meer over het beveiligen van web-API's met Azure AD toolearn wilt, Bekijk [in dit artikel](active-directory-v2-devquickstarts-dotnet-api.md). 

## <a name="sign-users-in"></a>Gebruikers aanmelden
Tijd toowrite identiteitscode.  Hebt misschien u al opgemerkt dat adal.js bevat een AngularJS-provider, waarmee mooi met Hoekvormige routering mechanismen speelt.  Starten door Hallo adal module toohello app toe te voegen:

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

U kunt nu Hallo initialiseren `adalProvider` met toepassings-ID:

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

Goede nu adal.js alle informatie over het Hallo heeft moet toosecure uw app en meld u aan gebruikers in.  aanmelden voor een bepaalde route in alle duurt het Hallo-app tooforce is één regel code:

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

Nu wanneer een gebruiker klikt op Hallo `TodoList` koppeling adal.js worden automatisch omgeleid tooAzure AD voor aanmelden indien nodig.  U kunt ook expliciet aanmelden en afmeldingsaanvragen te verzenden door aan te roepen adal.js in uw domeincontrollers verzenden:

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

## <a name="display-user-info"></a>Gebruikersgegevens weergeven
Nu dat hello gebruiker is aangemeld, moet waarschijnlijk u tooaccess Hallo aangemelde gebruiker de verificatiegegevens in uw toepassing.  Adal.js beschrijft deze informatie voor u in Hallo `userInfo` object.  tooaccess dit object in een weergave eerst adal.js toohello hoofdmap bereik van de bijbehorende controller Hallo toevoegen:

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

Vervolgens kunt u rechtstreeks hello te houden `userInfo` object in de weergave: 

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

U kunt ook Hallo `userInfo` toodetermine object als het Hallo-gebruiker is aangemeld of niet.

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

## <a name="call-hello-rest-api"></a>Hallo REST-API aanroepen
Ten slotte is het tijd tooget sommige tokens en aanroep Hallo toocreate REST-API, lezen, bijwerken en verwijderen van taken.  Ook goed nieuws!  U hebt geen toodo *een ding*.  Adal.js zorgt automatisch voor het ophalen, opslaan in cache en vernieuwen van tokens.  Deze ook zorgt voor het koppelen van deze tokens die toooutgoing AJAX-aanvragen toohello REST-API te sturen.  

Hoe werkt dit? Alle Bedankt toohello magie van is [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), waardoor adal.js tootransform uitgaande en binnenkomende HTTP-berichten.  Bovendien adal.js wordt aangenomen dat de verzoeken van toohello verzenden hetzelfde domein als Hallo-venster moet tokens die zijn bedoeld voor gebruik Hallo dezelfde toepassings-ID zoals Hallo AngularJS-app.  Daarom hebben we Hallo gebruikt dezelfde toepassings-ID in beide Hoekvormige app hello en in Hallo NodeJS REST-API.  Natuurlijk kunt u dit gedrag negeren en vertel adal.js tooget tokens voor andere REST-API's zo nodig - maar voor deze eenvoudige scenario Hallo standaardwaarden doet.

Hier volgt een codefragment die laat zien hoe eenvoudig het is toosend aanvragen met bearer-tokens van Azure AD:

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

Gefeliciteerd.  Uw Azure AD-geïntegreerde één pagina app is nu voltooid.  Opwekken op. een boeg.  U kunt verificatie van gebruikers, veilig aanroepen van de back-end REST-API met OpenID Connect en basisinformatie over Hallo gebruiker ophalen.  Out of box hello, biedt ondersteuning voor elke gebruiker met een persoonlijk Microsoft-Account of een werk schoolaccount van Azure AD.  Hallo-app uitvoeren en in een browser navigeren te`https://localhost:44326/`.  Meld u aan met een persoonlijk Microsoft-account of een werk/school-account.  Takenlijst taken toohello gebruiker toevoegen en meld u af.  Meld u aan met Hallo andere type account. Als u een Azure AD-tenant toocreate werk/school-gebruikers moet [meer informatie over hoe een hier tooget](active-directory-howto-tenant.md) (het is gratis).

leren over Hallo v2.0-eindpunt, head back tooour toocontinue [v2.0 ontwikkelaarshandleiding](active-directory-appmodel-v2-overview.md).  Voor aanvullende bronnen voor uitchecken:

* [Azure-voorbeelden op GitHub >>](https://github.com/Azure-Samples)
* [Azure AD op de Stack-overloop >>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* Azure AD-documentatie op [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)

## <a name="get-security-updates-for-our-products"></a>Beveiligingsupdates voor onze producten downloaden
We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.

