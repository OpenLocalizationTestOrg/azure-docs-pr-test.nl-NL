---
title: aaaAzure AD AngularJS aan de slag | Microsoft Docs
description: "Hoe een single-page application ' AngularJS toobuild die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-beveiligde API aanroept met behulp van OAuth."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>AngularJS één pagina apps beveiligen met Azure AD

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD) maakt het eenvoudig en snel voor u tooadd aanmelden, afmelden en beveiligde OAuth-API-aanroepen tooyour apps van één pagina.  Deze kunnen uw gebruikers apps tooauthenticate met hun Windows Server Active Directory-accounts en een web-API die Azure AD beveiligen kunt, zoals Office 365-API's Hallo of hello Azure-API gebruiken.

Voor JavaScript-toepassingen die zijn uitgevoerd in een browser, Azure AD levert Hallo Active Directory Authentication Library (ADAL) of adal.js. Hallo enig doel adal.js toomake is het eenvoudig voor uw app tooget-toegangstokens. toodemonstrate hoe gemakkelijk het is, hier gaan we gaat verder met een AngularJS tooDo toepassing List die:

* Tekenen Hallo gebruiker in toohello app met Azure AD als Hallo id-provider.

* Sommige geeft informatie weer over Hallo-gebruiker.
* Veilig Hallo aanroepen van app-tooDo lijst API met behulp van Azure AD-bearer-tokens.
* Tekenen Hallo gebruiker buiten het Hallo-app.

toobuild hello voltooid werkende toepassing, moet u:

1. Uw app registreren bij Azure AD.
2. ADAL installeren en configureren van Hallo één pagina app.
3. ADAL toohelp beveiligde pagina's in Hallo één pagina app gebruiken.

tooget gestart, [Hallo app basisproject downloaden](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip). U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren. Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).

## <a name="step-1-register-hello-directorysearcher-application"></a>Stap 1: Hallo DirectorySearcher toepassing registreren
tooenable uw app tooauthenticate gebruikers en de get-tokens, moet u eerst tooregister in uw Azure AD-tenant:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Als u mappen toomultiple bent aangemeld, moet u mogelijk tooensure u bekijkt hello correcte directory. toodo dus op de bovenste balk hello, klikt u op uw account. Onder Hallo **Directory** Kies waar u tooregister hello Azure AD-tenant van uw toepassing.
3. Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.
4. Klik op **App registraties**, en selecteer vervolgens **toevoegen**.
5. Volg de aanwijzingen Hallo en maak een nieuwe webtoepassing en/of web-API:
  * **Naam** beschrijft de toousers van uw toepassing.
  * **Omleidings-Uri** is Hallo locatie toowhich Azure AD tokens wordt geretourneerd. Hallo-standaardlocatie voor dit voorbeeld is `https://localhost:44326/`.
6. Nadat u de registratie, wijst een unieke toepassingsnaam ID tooyour app in Azure AD toe.  U moet deze waarde in de volgende secties hello, dus kopieer het van Hallo toepassingstabblad.
7. Hallo OAuth impliciete stroom toocommunicate Adal.js gebruikt met Azure AD. U moet Hallo impliciete stroom inschakelen voor uw toepassing:
  1. Klik op de toepassing hello en selecteer **Manifest** tooopen Hallo inline manifest editor.
  2. Zoek Hallo `oauth2AllowImplicitFlow` eigenschap. Stel de waarde te`true`.
  3. Klik op **opslaan** toosave Hallo manifest.
8. Machtigingen toekennen voor uw tenant voor uw toepassing. Ga te**instellingen** > **eigenschappen** > **Required Permissions**, en klik op Hallo **machtiging verlenen**knop op Hallo bovenste balk. Klik op **Ja** tooconfirm.

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>Stap 2: Installeer ADAL en Hallo één pagina app configureren
Nu dat u een toepassing in Azure AD hebt, kunt u adal.js installeert en uw identiteitsgerelateerde code schrijven.

### <a name="configure-hello-javascript-client"></a>Hallo JavaScript-client configureren
Beginnen met het adal.js toohello TodoSPA project toe te voegen met behulp van Hallo Package Manager-Console:
  1. Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) en toe te voegen toohello `App/Scripts/` projectmap.
  2. Download [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) en toe te voegen toohello `App/Scripts/` projectmap.
  3. Laden van elk script voor einde Hallo Hallo `</body>` in `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Hallo back-end-server configureren
Voor Hallo één pagina app back-end tooDo lijst API tooaccept tokens van Hallo browser moet Hallo back-end configuratie-informatie over het registreren van Hallo-app. Open in Hallo TodoSPA project `web.config`. Vervang de waarden Hallo Hallo-elementen in Hallo `<appSettings>` sectie tooreflect Hallo waarden die u gebruikt in hello Azure-portal. Uw code zal naar deze waarden verwijzen wanneer deze gebruikmaakt van ADAL.
  * `ida:Tenant`Hallo-domein van uw Azure AD-tenant bijvoorbeeld: contoso.onmicrosoft.com is.
  * `ida:Audience`client-ID van uw toepassing die u hebt gekopieerd uit de portal Hallo Hallo is.

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>Stap 3: Gebruik ADAL toohelp beveiligde pagina's in Hallo single-page-app
Adal.js integreert met AngularJS route en HTTP-providers, zodat u beveiligde afzonderlijke weergaven in uw app met één pagina kunt.

1. In `App/Scripts/app.js`, breng in Hallo adal.js module:

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. Initialiseren `adalProvider` met behulp van Hallo configuratiewaarden die van de toepassingsregistratie van uw, ook in `App/Scripts/app.js`:

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. Beveiligde Hallo Help `TodoList` weergave in de app met behulp van slechts één regel code Hallo: `requireADLogin`.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>Samenvatting
U hebt nu een veilige één pagina app waarmee u kunt gebruikers aanmelden en uitgeven van bearer-token-beveiligde aanvragen tooits back-end-API. Wanneer een gebruiker klikt op Hallo **TodoList** koppeling adal.js worden automatisch omgeleid tooAzure AD voor aanmelden indien nodig. Bovendien koppelen adal.js automatisch een access token tooany Ajax-aanvragen die afkomstig zijn van de app toohello back-end.  

Hallo voorgaande stappen zijn Hallo bare minimaal benodigde toobuild een app met één pagina met behulp van adal.js. Maar een aantal andere functies zijn handig in één pagina app:

* tooexplicitly uitgeven aanmelden en afmeldingsaanvragen te verzenden, kunt u de functies in uw domeincontrollers die gebruikmaken van adal.js definiëren.  In `App/Scripts/homeCtrl.js`:

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* U kunt de gebruikersgegevens toopresent in de gebruikersinterface van de app Hallo. Hallo ADAL-service is al toegevoegd toohello `userDataCtrl` -controller, zodat u toegang hebt tot Hallo `userInfo` -object in Hallo gekoppelde weergave, `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* Er zijn veel scenario's waarin moet u tooknow als Hallo gebruiker is aangemeld of niet. U kunt ook Hallo `userInfo` object toogather deze informatie.  Bijvoorbeeld in `index.html`, kunt u beide Hallo weergeven **aanmelding** of **afmelding** knop op basis van de status van verificatie:

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

Uw Azure AD-geïntegreerde één pagina app kan verifiëren van gebruikers, veilig aanroepen van de back-end via OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen. Als u nog niet gedaan hebt, is nu Hallo tijd toopopulate uw tenant waarbij sommige gebruikers. Uitvoeren van uw app tooDo lijst met één pagina en meld u aan met een van deze gebruikers. Takenlijst taken toohello gebruiker toevoegen, meld u af en meld u opnieuw aan.

Adal.js maakt het eenvoudig tooincorporate veelvoorkomende identity-functies in uw toepassing. Dit zorgt voor alle Hallo dirty werk voor u: cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmeldingspagina-gebruikersinterface vernieuwen van tokens verlopen en meer.

Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) is beschikbaar in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).

## <a name="next-steps"></a>Volgende stappen
U kunt nu verplaatsen op tooadditional scenario's. U kunt tootry: [een CORS-web-API aanroepen vanuit een app met één pagina](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
