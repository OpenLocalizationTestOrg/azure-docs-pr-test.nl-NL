---
title: aaaAzure AD v2 JS SPA begeleide Setup - gebruik | Microsoft Docs
description: Hoe een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen in JavaScript SPA-toepassingen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="33dee-103">Hallo Microsoft Authentication Library (MSAL) toosign in Hallo gebruiker gebruiken</span><span class="sxs-lookup"><span data-stu-id="33dee-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="33dee-104">Maak een bestand met de naam `app.js`.</span><span class="sxs-lookup"><span data-stu-id="33dee-104">Create a file named `app.js`.</span></span> <span data-ttu-id="33dee-105">Als u Visual Studio, selecteer Hallo-project (project basismap), klik met de rechtermuisknop en selecteer: `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="33dee-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="33dee-106">Hallo na code tooyour toevoegen `app.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="33dee-106">Add hello following code tooyour `app.js` file:</span></span>

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="33dee-107">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="33dee-107">More Information</span></span>

<span data-ttu-id="33dee-108">Nadat een gebruiker op Hallo *'Microsoft Graph API aanroepen'* knop voor de eerste keer Hallo `callGraphApi` methodeaanroepen `loginRedirect` toosign in Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="33dee-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="33dee-109">Deze methode resulteert in het omleiden van Hallo gebruiker toohello *Microsoft Azure Active Directory-v2-eindpunt* tooprompt en Hallo gebruikersreferenties te valideren.</span><span class="sxs-lookup"><span data-stu-id="33dee-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="33dee-110">Als gevolg van een geslaagde aanmelden, Hallo gebruiker is omgeleid back toohello oorspronkelijke *index.html* pagina en een token wordt ontvangen, verwerkt door `msal.js` en Hallo gegevens in het Hallo-token in de cache wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="33dee-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="33dee-111">Dit token wordt ook wel Hallo *token ID* en algemene informatie over het Hallo-gebruiker, zoals de weergavenaam van de gebruiker Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="33dee-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="33dee-112">Als u van plan toouse bent is geen gegevens opgegeven door dit token voor andere doeleinden, moet u ervoor dat dit token is gevalideerd door uw back-end server tooguarantee die Hallo token toomake uitgegeven geldige gebruiker van de tooa voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="33dee-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="33dee-113">Hallo SPA die worden gegenereerd door deze handleiding maakt geen gebruik van Hallo ID token rechtstreeks – in plaats daarvan wordt aangeroepen `acquireTokenSilent` en/of `acquireTokenRedirect` tooacquire een *toegangstoken* tooquery Hallo Microsoft Graph API gebruikt.</span><span class="sxs-lookup"><span data-stu-id="33dee-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="33dee-114">Als u een steekproef die het Hallo-id-token valideert moet, Bekijk [dit](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 voorbeeld") voorbeeldtoepassing in GitHub – Hallo-voorbeeld gebruikt een ASP.NET-Web-API voor validatie van tokens.</span><span class="sxs-lookup"><span data-stu-id="33dee-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="33dee-115">Een gebruiker ophalen interactief token</span><span class="sxs-lookup"><span data-stu-id="33dee-115">Getting a user token interactively</span></span>

<span data-ttu-id="33dee-116">Initiële aanmelden na hello, u niet wilt dat Hallo vraag gebruikers tooreauthenticate telkens wanneer ze toorequest moeten een token tooaccess een resource: dus *acquireTokenSilent* moet de meeste Hallo tijd tooacquire tokens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="33dee-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="33dee-117">Er zijn echter situaties moet u gebruikers met Azure Active Directory v2 eindpunt werken – tooforce enkele voorbeelden zijn:</span><span class="sxs-lookup"><span data-stu-id="33dee-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="33dee-118">Gebruikers hebben mogelijk nodig tooreenter hun referenties omdat Hallo wachtwoord is verlopen</span><span class="sxs-lookup"><span data-stu-id="33dee-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="33dee-119">Uw toepassing vraagt toegang tooa resource die gebruiker moet tooconsent op Hallo</span><span class="sxs-lookup"><span data-stu-id="33dee-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="33dee-120">Tweeledige verificatie is vereist</span><span class="sxs-lookup"><span data-stu-id="33dee-120">Two factor authentication is required</span></span>

<span data-ttu-id="33dee-121">Aanroepen Hallo *acquireTokenRedirect(scope)* leiden tot het omleiden van gebruikers toohello Azure Active Directory-v2-eindpunt (of *acquireTokenPopup(scope)* resultaat op een pop-upvenster) waar gebruikers nodig hebben toointeract met door ofwel hun referenties geeft Hallo toestemming toohello vereiste resource of verificatie voltooien Hallo met twee factoren.</span><span class="sxs-lookup"><span data-stu-id="33dee-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="33dee-122">Een gebruiker ophalen achtergrond token</span><span class="sxs-lookup"><span data-stu-id="33dee-122">Getting a user token silently</span></span>
<span data-ttu-id="33dee-123">Hallo ` acquireTokenSilent` methode verwerkt token acquisities van organisaties en verlenging zonder tussenkomst van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="33dee-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="33dee-124">Na `loginRedirect` (of `loginPopup`) wordt uitgevoerd voor Hallo eerst `acquireTokenSilent` Hallo methode gebruikte tooobtain tokens die worden gebruikt tooaccess resources voor volgende aanroepen - beveiligd als aanroepen toorequest of vernieuwen van tokens achtergrond worden aangebracht.</span><span class="sxs-lookup"><span data-stu-id="33dee-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="33dee-125">`acquireTokenSilent`mislukken in sommige gevallen – bijvoorbeeld Hallo gebruikerswachtwoord kan is verlopen.</span><span class="sxs-lookup"><span data-stu-id="33dee-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="33dee-126">Uw toepassing kan verwerken van deze uitzondering op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="33dee-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="33dee-127">Te maken van een aanroep van`acquireTokenRedirect` onmiddellijk, waardoor het vragen Hallo toosign van de gebruiker in.</span><span class="sxs-lookup"><span data-stu-id="33dee-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="33dee-128">Dit patroon wordt meestal gebruikt in toepassingen met online wanneer er geen niet-geverifieerde inhoud in Hallo toepassingen toohello beschikbaar voor gebruikers is.</span><span class="sxs-lookup"><span data-stu-id="33dee-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="33dee-129">Hallo-voorbeeld gegenereerd met deze Begeleide installatie maakt gebruik van dit patroon.</span><span class="sxs-lookup"><span data-stu-id="33dee-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="33dee-130">Toepassingen kunnen ook een visuele indicatie toohello-gebruiker die een interactief aanmelden is vereist, zodat Hallo-gebruiker kunt selecteren Hallo juiste moment toosign in of toepassing hello opnieuw kunt maken `acquireTokenSilent` op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="33dee-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="33dee-131">Dit wordt meestal gebruikt wanneer Hallo gebruiker andere functionaliteit van de toepassing hello gebruiken kunt zonder wordt onderbroken: er bijvoorbeeld niet-geverifieerde inhoud beschikbaar zijn in de toepassing hello is.</span><span class="sxs-lookup"><span data-stu-id="33dee-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="33dee-132">Hallo-gebruiker kunt in dit geval bepalen wanneer hij of zij wil toosign in tooaccess Hallo beveiligde resource of toorefresh Hallo verouderde informatie.</span><span class="sxs-lookup"><span data-stu-id="33dee-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="33dee-133">Hallo Hallo-token die u zojuist hebt verkregen met Microsoft Graph-API niet aanroepen</span><span class="sxs-lookup"><span data-stu-id="33dee-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="33dee-134">Hallo na code tooyour toevoegen `app.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="33dee-134">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in hello page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in hello page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="33dee-135">Meer informatie over het maken van een REST-aanroep op basis van een beveiligde API</span><span class="sxs-lookup"><span data-stu-id="33dee-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="33dee-136">Hallo in Hallo voorbeeldtoepassing gemaakt door deze handleiding `callWebApiWithToken()` methode is gebruikte toomake een HTTP `GET` -aanvraag in voor een beveiligde bron die een token en ga daarna terug Hallo inhoud toohello aanroeper vereist.</span><span class="sxs-lookup"><span data-stu-id="33dee-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="33dee-137">Met deze methode wordt Hallo verkregen token in Hallo *HTTP-autorisatie-header*.</span><span class="sxs-lookup"><span data-stu-id="33dee-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="33dee-138">Voor Hallo voorbeeldtoepassing gemaakt door deze handleiding is Hallo resource Hallo Microsoft Graph API *mij* eindpunt – Hallo van gebruikersprofielgegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="33dee-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="33dee-139">Een methode toosign uit Hallo gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="33dee-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="33dee-140">Hallo na code tooyour toevoegen `app.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="33dee-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
