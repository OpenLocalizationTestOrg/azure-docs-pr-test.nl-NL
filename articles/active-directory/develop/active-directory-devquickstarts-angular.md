---
title: Azure AD-AngularJS aan de slag | Microsoft Docs
description: "Hoe een AngularJS één pagina toepassing bouwt die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-beveiligde API aanroept met behulp van OAuth."
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
ms.openlocfilehash: 4153910bc03f112f84c26cda6f9c78f11028b934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="cb174-103">AngularJS één pagina apps beveiligen met Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb174-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="cb174-104">Azure Active Directory (Azure AD) maakt het eenvoudig en snel kunt aanmelden, afmelden en veilige OAuth-API toevoegen aan uw apps met één pagina aanroept.</span><span class="sxs-lookup"><span data-stu-id="cb174-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span></span>  <span data-ttu-id="cb174-105">Hiermee kunt uw apps voor het verifiëren van gebruikers met hun Windows Server Active Directory-accounts en een web-API die Azure AD beveiligen kunt, zoals de Office 365-API of de Azure-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cb174-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="cb174-106">Voor JavaScript-toepassingen die zijn uitgevoerd in een browser, levert Azure AD de Active Directory Authentication Library (ADAL) of adal.js.</span><span class="sxs-lookup"><span data-stu-id="cb174-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="cb174-107">Het enige doel van adal.js is gemakkelijker voor uw app toegangstokens ophalen.</span><span class="sxs-lookup"><span data-stu-id="cb174-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="cb174-108">Als u wilt laten zien hoe eenvoudig het is, hier we je een AngularJS To Do List toepassing bouwt die:</span><span class="sxs-lookup"><span data-stu-id="cb174-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span></span>

* <span data-ttu-id="cb174-109">De gebruiker zich aanmeldt bij de app met Azure AD als id-provider.</span><span class="sxs-lookup"><span data-stu-id="cb174-109">Signs the user in to the app by using Azure AD as the identity provider.</span></span>

* <span data-ttu-id="cb174-110">Sommige geeft informatie weer over de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cb174-110">Displays some information about the user.</span></span>
* <span data-ttu-id="cb174-111">Veilig van de app te doen lijst API aanroept met behulp van Azure AD-bearer-tokens.</span><span class="sxs-lookup"><span data-stu-id="cb174-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="cb174-112">De gebruiker buiten de app ondertekent.</span><span class="sxs-lookup"><span data-stu-id="cb174-112">Signs the user out of the app.</span></span>

<span data-ttu-id="cb174-113">De volledige, werkende toepassing bouwen, moet u:</span><span class="sxs-lookup"><span data-stu-id="cb174-113">To build the complete, working application, you need to:</span></span>

1. <span data-ttu-id="cb174-114">Uw app registreren bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb174-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="cb174-115">ADAL installeren en configureren van de app met één pagina.</span><span class="sxs-lookup"><span data-stu-id="cb174-115">Install ADAL and configure the single-page app.</span></span>
3. <span data-ttu-id="cb174-116">Gebruik ADAL voor het beveiligde pagina's in de app met één pagina.</span><span class="sxs-lookup"><span data-stu-id="cb174-116">Use ADAL to help secure pages in the single-page app.</span></span>

<span data-ttu-id="cb174-117">Aan de slag [de basis van de app downloaden](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) of [het voltooide voorbeeld downloaden](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="cb174-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="cb174-118">U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="cb174-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="cb174-119">Als u niet al een tenant [Lees hoe u een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="cb174-119">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-the-directorysearcher-application"></a><span data-ttu-id="cb174-120">Stap 1: De DirectorySearcher-toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="cb174-120">Step 1: Register the DirectorySearcher application</span></span>
<span data-ttu-id="cb174-121">Als u wilt inschakelen voor de app voor het verifiëren van gebruikers en tokens krijgen, moet u eerst registreren in uw Azure AD-tenant:</span><span class="sxs-lookup"><span data-stu-id="cb174-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="cb174-122">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cb174-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cb174-123">Als u bent aangemeld bij meerdere mappen, moet u mogelijk om te controleren of dat u de juiste map bekijkt.</span><span class="sxs-lookup"><span data-stu-id="cb174-123">If you are signed in to multiple directories, you may need to ensure you are viewing the correct directory.</span></span> <span data-ttu-id="cb174-124">Klik op uw account om dit te doen op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="cb174-124">To do so, on the top bar, click your account.</span></span> <span data-ttu-id="cb174-125">Onder de **Directory** kiest u de Azure AD-tenant waar u uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="cb174-125">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="cb174-126">Klik op **meer Services** in het linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb174-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="cb174-127">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cb174-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="cb174-128">Volg de aanwijzingen en maak een nieuwe webtoepassing en/of web-API:</span><span class="sxs-lookup"><span data-stu-id="cb174-128">Follow the prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="cb174-129">**Naam** beschrijving van uw toepassing voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="cb174-129">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="cb174-130">**Omleidings-Uri** is de locatie waarop Azure AD tokens wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="cb174-130">**Redirect Uri** is the location to which Azure AD will return tokens.</span></span> <span data-ttu-id="cb174-131">De standaardlocatie voor dit voorbeeld is `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="cb174-131">The default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="cb174-132">Nadat u de registratie, wijst Azure AD een unieke toepassings-ID toe aan uw app.</span><span class="sxs-lookup"><span data-stu-id="cb174-132">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span>  <span data-ttu-id="cb174-133">U moet deze waarde in de volgende secties, dus kopiëren vanaf het toepassingstabblad.</span><span class="sxs-lookup"><span data-stu-id="cb174-133">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="cb174-134">De impliciete OAuth-stroom Adal.js gebruikt om te communiceren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb174-134">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span></span> <span data-ttu-id="cb174-135">U moet de impliciete stroom inschakelen voor uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="cb174-135">You must enable the implicit flow for your application:</span></span>
  1. <span data-ttu-id="cb174-136">Klik op de toepassing en selecteer **Manifest** om het manifest inline-editor te openen.</span><span class="sxs-lookup"><span data-stu-id="cb174-136">Click the application and select **Manifest** to open the inline manifest editor.</span></span>
  2. <span data-ttu-id="cb174-137">Zoek de `oauth2AllowImplicitFlow` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cb174-137">Locate the `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="cb174-138">Stel de waarde op `true`.</span><span class="sxs-lookup"><span data-stu-id="cb174-138">Set its value to `true`.</span></span>
  3. <span data-ttu-id="cb174-139">Klik op **opslaan** om op te slaan van het manifest.</span><span class="sxs-lookup"><span data-stu-id="cb174-139">Click **Save** to save the manifest.</span></span>
8. <span data-ttu-id="cb174-140">Machtigingen toekennen voor uw tenant voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="cb174-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="cb174-141">Ga naar **instellingen** > **eigenschappen** > **Required Permissions**, en klik op de **machtiging verlenen** knop op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="cb174-141">Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span></span> <span data-ttu-id="cb174-142">Klik op **Ja** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="cb174-142">Click **Yes** to confirm.</span></span>

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a><span data-ttu-id="cb174-143">Stap 2: Installeer ADAL en configureren van de app met één pagina</span><span class="sxs-lookup"><span data-stu-id="cb174-143">Step 2: Install ADAL and configure the single-page app</span></span>
<span data-ttu-id="cb174-144">Nu dat u een toepassing in Azure AD hebt, kunt u adal.js installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="cb174-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-the-javascript-client"></a><span data-ttu-id="cb174-145">De JavaScript-client configureren</span><span class="sxs-lookup"><span data-stu-id="cb174-145">Configure the JavaScript client</span></span>
<span data-ttu-id="cb174-146">Beginnen met het adal.js toevoegen aan het project TodoSPA met behulp van de Package Manager-Console:</span><span class="sxs-lookup"><span data-stu-id="cb174-146">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span></span>
  1. <span data-ttu-id="cb174-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) en toe te voegen aan de `App/Scripts/` projectmap.</span><span class="sxs-lookup"><span data-stu-id="cb174-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="cb174-148">Download [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) en toe te voegen aan de `App/Scripts/` projectmap.</span><span class="sxs-lookup"><span data-stu-id="cb174-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="cb174-149">Laden van elk script vóór het einde van de `</body>` in `index.html`:</span><span class="sxs-lookup"><span data-stu-id="cb174-149">Load each script before the end of the `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-the-back-end-server"></a><span data-ttu-id="cb174-150">De back-end-server configureren</span><span class="sxs-lookup"><span data-stu-id="cb174-150">Configure the back end server</span></span>
<span data-ttu-id="cb174-151">Voor de single-page-app back-end te doen lijst API tokens van de browser accepteert, moet de back-end configuratie-informatie over de registratie van de app.</span><span class="sxs-lookup"><span data-stu-id="cb174-151">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span></span> <span data-ttu-id="cb174-152">Open in het project TodoSPA `web.config`.</span><span class="sxs-lookup"><span data-stu-id="cb174-152">In the TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="cb174-153">Vervang de waarden van de elementen in de `<appSettings>` sectie in overeenstemming met de waarden die u in de Azure portal gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cb174-153">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="cb174-154">Uw code zal naar deze waarden verwijzen wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="cb174-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="cb174-155">`ida:Tenant`is het domein van uw Azure AD-tenant bijvoorbeeld: contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="cb174-155">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="cb174-156">`ida:Audience`is de client-ID van uw toepassing die u hebt gekopieerd uit de portal.</span><span class="sxs-lookup"><span data-stu-id="cb174-156">`ida:Audience` is the client ID of your application that you copied from the portal.</span></span>

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a><span data-ttu-id="cb174-157">Stap 3: Gebruik ADAL om u te helpen, beveiligde pagina's in de app met één pagina</span><span class="sxs-lookup"><span data-stu-id="cb174-157">Step 3: Use ADAL to help secure pages in the single-page app</span></span>
<span data-ttu-id="cb174-158">Adal.js integreert met AngularJS route en HTTP-providers, zodat u beveiligde afzonderlijke weergaven in uw app met één pagina kunt.</span><span class="sxs-lookup"><span data-stu-id="cb174-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="cb174-159">In `App/Scripts/app.js`, brengen in de module adal.js:</span><span class="sxs-lookup"><span data-stu-id="cb174-159">In `App/Scripts/app.js`, bring in the adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="cb174-160">Initialiseren `adalProvider` met behulp van de configuratiewaarden van de toepassingsregistratie van uw, ook in `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="cb174-160">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="cb174-161">Beveiligen van de `TodoList` weergave in de app met behulp van slechts één regel code: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="cb174-161">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="cb174-162">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="cb174-162">Summary</span></span>
<span data-ttu-id="cb174-163">U hebt nu een veilige één pagina app waarmee u kunt gebruikers aanmelden en bearer-token-beveiligde aanvragen te verlenen aan de back-end-API.</span><span class="sxs-lookup"><span data-stu-id="cb174-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span></span> <span data-ttu-id="cb174-164">Wanneer een gebruiker klikt op de **TodoList** koppeling adal.js worden automatisch omgeleid naar Azure AD voor aanmelden indien nodig.</span><span class="sxs-lookup"><span data-stu-id="cb174-164">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span> <span data-ttu-id="cb174-165">Adal.js wordt bovendien automatisch een toegangstoken koppelen aan een Ajax-aanvragen die worden verzonden naar de back-end van de app.</span><span class="sxs-lookup"><span data-stu-id="cb174-165">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span></span>  

<span data-ttu-id="cb174-166">De voorgaande stappen zijn bare minimale nodig voor het bouwen van een app met één pagina met behulp van adal.js.</span><span class="sxs-lookup"><span data-stu-id="cb174-166">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span></span> <span data-ttu-id="cb174-167">Maar een aantal andere functies zijn handig in één pagina app:</span><span class="sxs-lookup"><span data-stu-id="cb174-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="cb174-168">Expliciet uitgeven aanmelden en afmeldingsaanvragen te verzenden, kunt u functies definiëren in uw domeincontrollers die adal.js aanroepen.</span><span class="sxs-lookup"><span data-stu-id="cb174-168">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="cb174-169">In `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="cb174-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="cb174-170">Het is raadzaam om gebruikersgegevens in de gebruikersinterface van de app.</span><span class="sxs-lookup"><span data-stu-id="cb174-170">You might want to present user information in the app's UI.</span></span> <span data-ttu-id="cb174-171">De ADAL-service is al toegevoegd aan de `userDataCtrl` -controller, zodat u toegang hebt tot de `userInfo` object in de bijbehorende weergave `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="cb174-171">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="cb174-172">Er zijn veel scenario's waarin u weten wilt of de gebruiker is aangemeld of niet.</span><span class="sxs-lookup"><span data-stu-id="cb174-172">There are many scenarios in which you'll want to know if the user is signed in or not.</span></span> <span data-ttu-id="cb174-173">U kunt ook de `userInfo` object informatie te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="cb174-173">You can also use the `userInfo` object to gather this information.</span></span>  <span data-ttu-id="cb174-174">Bijvoorbeeld in `index.html`, kunt u weergeven ofwel de **aanmelding** of **afmelding** knop op basis van de status van verificatie:</span><span class="sxs-lookup"><span data-stu-id="cb174-174">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="cb174-175">Uw Azure AD-geïntegreerde één pagina app kan verifiëren van gebruikers, veilig aanroepen van de back-end via OAuth 2.0 en algemene informatie over de gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="cb174-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="cb174-176">Als u nog niet gedaan hebt, is nu de tijd voor het vullen van uw tenant waarbij sommige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="cb174-176">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="cb174-177">Uitvoeren van uw To Do List single-page-app en meld u aan met een van deze gebruikers.</span><span class="sxs-lookup"><span data-stu-id="cb174-177">Run your To Do List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="cb174-178">Taken toevoegen aan de takenlijst van de gebruiker, meldt u zich af en meld u opnieuw aan.</span><span class="sxs-lookup"><span data-stu-id="cb174-178">Add tasks to the user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="cb174-179">Adal.js kunt gemakkelijk veelvoorkomende identiteit functies opnemen in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="cb174-179">Adal.js makes it easy to incorporate common identity features into your application.</span></span> <span data-ttu-id="cb174-180">Dit zorgt voor al het dirty werk voor u: cachebeheer, OAuth-protocolondersteuning, dat de gebruiker een aanmeldingspagina-gebruikersinterface vernieuwen van tokens verlopen en meer.</span><span class="sxs-lookup"><span data-stu-id="cb174-180">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="cb174-181">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) is beschikbaar in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="cb174-181">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb174-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cb174-182">Next steps</span></span>
<span data-ttu-id="cb174-183">U kunt nu verder met aanvullende scenario's.</span><span class="sxs-lookup"><span data-stu-id="cb174-183">You can now move on to additional scenarios.</span></span> <span data-ttu-id="cb174-184">U wilt proberen: [een CORS-web-API aanroepen vanuit een app met één pagina](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="cb174-184">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
