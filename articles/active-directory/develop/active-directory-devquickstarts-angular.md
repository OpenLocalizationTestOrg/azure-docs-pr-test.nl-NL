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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="67bb4-103">AngularJS één pagina apps beveiligen met Azure AD</span><span class="sxs-lookup"><span data-stu-id="67bb4-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="67bb4-104">Azure Active Directory (Azure AD) maakt het eenvoudig en snel voor u tooadd aanmelden, afmelden en beveiligde OAuth-API-aanroepen tooyour apps van één pagina.</span><span class="sxs-lookup"><span data-stu-id="67bb4-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="67bb4-105">Deze kunnen uw gebruikers apps tooauthenticate met hun Windows Server Active Directory-accounts en een web-API die Azure AD beveiligen kunt, zoals Office 365-API's Hallo of hello Azure-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="67bb4-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="67bb4-106">Voor JavaScript-toepassingen die zijn uitgevoerd in een browser, Azure AD levert Hallo Active Directory Authentication Library (ADAL) of adal.js.</span><span class="sxs-lookup"><span data-stu-id="67bb4-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="67bb4-107">Hallo enig doel adal.js toomake is het eenvoudig voor uw app tooget-toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="67bb4-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="67bb4-108">toodemonstrate hoe gemakkelijk het is, hier gaan we gaat verder met een AngularJS tooDo toepassing List die:</span><span class="sxs-lookup"><span data-stu-id="67bb4-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="67bb4-109">Tekenen Hallo gebruiker in toohello app met Azure AD als Hallo id-provider.</span><span class="sxs-lookup"><span data-stu-id="67bb4-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="67bb4-110">Sommige geeft informatie weer over Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="67bb4-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="67bb4-111">Veilig Hallo aanroepen van app-tooDo lijst API met behulp van Azure AD-bearer-tokens.</span><span class="sxs-lookup"><span data-stu-id="67bb4-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="67bb4-112">Tekenen Hallo gebruiker buiten het Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="67bb4-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="67bb4-113">toobuild hello voltooid werkende toepassing, moet u:</span><span class="sxs-lookup"><span data-stu-id="67bb4-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="67bb4-114">Uw app registreren bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67bb4-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="67bb4-115">ADAL installeren en configureren van Hallo één pagina app.</span><span class="sxs-lookup"><span data-stu-id="67bb4-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="67bb4-116">ADAL toohelp beveiligde pagina's in Hallo één pagina app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="67bb4-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="67bb4-117">tooget gestart, [Hallo app basisproject downloaden](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="67bb4-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="67bb4-118">U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="67bb4-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="67bb4-119">Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="67bb4-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="67bb4-120">Stap 1: Hallo DirectorySearcher toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="67bb4-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="67bb4-121">tooenable uw app tooauthenticate gebruikers en de get-tokens, moet u eerst tooregister in uw Azure AD-tenant:</span><span class="sxs-lookup"><span data-stu-id="67bb4-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="67bb4-122">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67bb4-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67bb4-123">Als u mappen toomultiple bent aangemeld, moet u mogelijk tooensure u bekijkt hello correcte directory.</span><span class="sxs-lookup"><span data-stu-id="67bb4-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="67bb4-124">toodo dus op de bovenste balk hello, klikt u op uw account.</span><span class="sxs-lookup"><span data-stu-id="67bb4-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="67bb4-125">Onder Hallo **Directory** Kies waar u tooregister hello Azure AD-tenant van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="67bb4-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="67bb4-126">Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="67bb4-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="67bb4-127">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="67bb4-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="67bb4-128">Volg de aanwijzingen Hallo en maak een nieuwe webtoepassing en/of web-API:</span><span class="sxs-lookup"><span data-stu-id="67bb4-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="67bb4-129">**Naam** beschrijft de toousers van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="67bb4-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="67bb4-130">**Omleidings-Uri** is Hallo locatie toowhich Azure AD tokens wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="67bb4-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="67bb4-131">Hallo-standaardlocatie voor dit voorbeeld is `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="67bb4-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="67bb4-132">Nadat u de registratie, wijst een unieke toepassingsnaam ID tooyour app in Azure AD toe.</span><span class="sxs-lookup"><span data-stu-id="67bb4-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="67bb4-133">U moet deze waarde in de volgende secties hello, dus kopieer het van Hallo toepassingstabblad.</span><span class="sxs-lookup"><span data-stu-id="67bb4-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="67bb4-134">Hallo OAuth impliciete stroom toocommunicate Adal.js gebruikt met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67bb4-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="67bb4-135">U moet Hallo impliciete stroom inschakelen voor uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="67bb4-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="67bb4-136">Klik op de toepassing hello en selecteer **Manifest** tooopen Hallo inline manifest editor.</span><span class="sxs-lookup"><span data-stu-id="67bb4-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="67bb4-137">Zoek Hallo `oauth2AllowImplicitFlow` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="67bb4-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="67bb4-138">Stel de waarde te`true`.</span><span class="sxs-lookup"><span data-stu-id="67bb4-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="67bb4-139">Klik op **opslaan** toosave Hallo manifest.</span><span class="sxs-lookup"><span data-stu-id="67bb4-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="67bb4-140">Machtigingen toekennen voor uw tenant voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="67bb4-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="67bb4-141">Ga te**instellingen** > **eigenschappen** > **Required Permissions**, en klik op Hallo **machtiging verlenen**knop op Hallo bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="67bb4-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="67bb4-142">Klik op **Ja** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="67bb4-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="67bb4-143">Stap 2: Installeer ADAL en Hallo één pagina app configureren</span><span class="sxs-lookup"><span data-stu-id="67bb4-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="67bb4-144">Nu dat u een toepassing in Azure AD hebt, kunt u adal.js installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="67bb4-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="67bb4-145">Hallo JavaScript-client configureren</span><span class="sxs-lookup"><span data-stu-id="67bb4-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="67bb4-146">Beginnen met het adal.js toohello TodoSPA project toe te voegen met behulp van Hallo Package Manager-Console:</span><span class="sxs-lookup"><span data-stu-id="67bb4-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="67bb4-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) en toe te voegen toohello `App/Scripts/` projectmap.</span><span class="sxs-lookup"><span data-stu-id="67bb4-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="67bb4-148">Download [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) en toe te voegen toohello `App/Scripts/` projectmap.</span><span class="sxs-lookup"><span data-stu-id="67bb4-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="67bb4-149">Laden van elk script voor einde Hallo Hallo `</body>` in `index.html`:</span><span class="sxs-lookup"><span data-stu-id="67bb4-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="67bb4-150">Hallo back-end-server configureren</span><span class="sxs-lookup"><span data-stu-id="67bb4-150">Configure hello back end server</span></span>
<span data-ttu-id="67bb4-151">Voor Hallo één pagina app back-end tooDo lijst API tooaccept tokens van Hallo browser moet Hallo back-end configuratie-informatie over het registreren van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="67bb4-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="67bb4-152">Open in Hallo TodoSPA project `web.config`.</span><span class="sxs-lookup"><span data-stu-id="67bb4-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="67bb4-153">Vervang de waarden Hallo Hallo-elementen in Hallo `<appSettings>` sectie tooreflect Hallo waarden die u gebruikt in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="67bb4-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="67bb4-154">Uw code zal naar deze waarden verwijzen wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="67bb4-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="67bb4-155">`ida:Tenant`Hallo-domein van uw Azure AD-tenant bijvoorbeeld: contoso.onmicrosoft.com is.</span><span class="sxs-lookup"><span data-stu-id="67bb4-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="67bb4-156">`ida:Audience`client-ID van uw toepassing die u hebt gekopieerd uit de portal Hallo Hallo is.</span><span class="sxs-lookup"><span data-stu-id="67bb4-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="67bb4-157">Stap 3: Gebruik ADAL toohelp beveiligde pagina's in Hallo single-page-app</span><span class="sxs-lookup"><span data-stu-id="67bb4-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="67bb4-158">Adal.js integreert met AngularJS route en HTTP-providers, zodat u beveiligde afzonderlijke weergaven in uw app met één pagina kunt.</span><span class="sxs-lookup"><span data-stu-id="67bb4-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="67bb4-159">In `App/Scripts/app.js`, breng in Hallo adal.js module:</span><span class="sxs-lookup"><span data-stu-id="67bb4-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="67bb4-160">Initialiseren `adalProvider` met behulp van Hallo configuratiewaarden die van de toepassingsregistratie van uw, ook in `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="67bb4-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="67bb4-161">Beveiligde Hallo Help `TodoList` weergave in de app met behulp van slechts één regel code Hallo: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="67bb4-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="67bb4-162">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="67bb4-162">Summary</span></span>
<span data-ttu-id="67bb4-163">U hebt nu een veilige één pagina app waarmee u kunt gebruikers aanmelden en uitgeven van bearer-token-beveiligde aanvragen tooits back-end-API.</span><span class="sxs-lookup"><span data-stu-id="67bb4-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="67bb4-164">Wanneer een gebruiker klikt op Hallo **TodoList** koppeling adal.js worden automatisch omgeleid tooAzure AD voor aanmelden indien nodig.</span><span class="sxs-lookup"><span data-stu-id="67bb4-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="67bb4-165">Bovendien koppelen adal.js automatisch een access token tooany Ajax-aanvragen die afkomstig zijn van de app toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="67bb4-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="67bb4-166">Hallo voorgaande stappen zijn Hallo bare minimaal benodigde toobuild een app met één pagina met behulp van adal.js.</span><span class="sxs-lookup"><span data-stu-id="67bb4-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="67bb4-167">Maar een aantal andere functies zijn handig in één pagina app:</span><span class="sxs-lookup"><span data-stu-id="67bb4-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="67bb4-168">tooexplicitly uitgeven aanmelden en afmeldingsaanvragen te verzenden, kunt u de functies in uw domeincontrollers die gebruikmaken van adal.js definiëren.</span><span class="sxs-lookup"><span data-stu-id="67bb4-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="67bb4-169">In `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="67bb4-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="67bb4-170">U kunt de gebruikersgegevens toopresent in de gebruikersinterface van de app Hallo.</span><span class="sxs-lookup"><span data-stu-id="67bb4-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="67bb4-171">Hallo ADAL-service is al toegevoegd toohello `userDataCtrl` -controller, zodat u toegang hebt tot Hallo `userInfo` -object in Hallo gekoppelde weergave, `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="67bb4-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="67bb4-172">Er zijn veel scenario's waarin moet u tooknow als Hallo gebruiker is aangemeld of niet.</span><span class="sxs-lookup"><span data-stu-id="67bb4-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="67bb4-173">U kunt ook Hallo `userInfo` object toogather deze informatie.</span><span class="sxs-lookup"><span data-stu-id="67bb4-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="67bb4-174">Bijvoorbeeld in `index.html`, kunt u beide Hallo weergeven **aanmelding** of **afmelding** knop op basis van de status van verificatie:</span><span class="sxs-lookup"><span data-stu-id="67bb4-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="67bb4-175">Uw Azure AD-geïntegreerde één pagina app kan verifiëren van gebruikers, veilig aanroepen van de back-end via OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="67bb4-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="67bb4-176">Als u nog niet gedaan hebt, is nu Hallo tijd toopopulate uw tenant waarbij sommige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="67bb4-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="67bb4-177">Uitvoeren van uw app tooDo lijst met één pagina en meld u aan met een van deze gebruikers.</span><span class="sxs-lookup"><span data-stu-id="67bb4-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="67bb4-178">Takenlijst taken toohello gebruiker toevoegen, meld u af en meld u opnieuw aan.</span><span class="sxs-lookup"><span data-stu-id="67bb4-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="67bb4-179">Adal.js maakt het eenvoudig tooincorporate veelvoorkomende identity-functies in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="67bb4-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="67bb4-180">Dit zorgt voor alle Hallo dirty werk voor u: cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmeldingspagina-gebruikersinterface vernieuwen van tokens verlopen en meer.</span><span class="sxs-lookup"><span data-stu-id="67bb4-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="67bb4-181">Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) is beschikbaar in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="67bb4-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67bb4-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67bb4-182">Next steps</span></span>
<span data-ttu-id="67bb4-183">U kunt nu verplaatsen op tooadditional scenario's.</span><span class="sxs-lookup"><span data-stu-id="67bb4-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="67bb4-184">U kunt tootry: [een CORS-web-API aanroepen vanuit een app met één pagina](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="67bb4-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
