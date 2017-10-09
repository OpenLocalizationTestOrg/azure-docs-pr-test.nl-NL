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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>Hallo Microsoft Authentication Library (MSAL) toosign in Hallo gebruiker gebruiken

1.  Maak een bestand met de naam `app.js`. Als u Visual Studio, selecteer Hallo-project (project basismap), klik met de rechtermuisknop en selecteer: `Add`  >  `New Item`  >  `JavaScript File`:
2.  Hallo na code tooyour toevoegen `app.js` bestand:

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
### <a name="more-information"></a>Meer informatie

Nadat een gebruiker op Hallo *'Microsoft Graph API aanroepen'* knop voor de eerste keer Hallo `callGraphApi` methodeaanroepen `loginRedirect` toosign in Hallo-gebruiker. Deze methode resulteert in het omleiden van Hallo gebruiker toohello *Microsoft Azure Active Directory-v2-eindpunt* tooprompt en Hallo gebruikersreferenties te valideren. Als gevolg van een geslaagde aanmelden, Hallo gebruiker is omgeleid back toohello oorspronkelijke *index.html* pagina en een token wordt ontvangen, verwerkt door `msal.js` en Hallo gegevens in het Hallo-token in de cache wordt opgeslagen. Dit token wordt ook wel Hallo *token ID* en algemene informatie over het Hallo-gebruiker, zoals de weergavenaam van de gebruiker Hallo bevat. Als u van plan toouse bent is geen gegevens opgegeven door dit token voor andere doeleinden, moet u ervoor dat dit token is gevalideerd door uw back-end server tooguarantee die Hallo token toomake uitgegeven geldige gebruiker van de tooa voor uw toepassing.

Hallo SPA die worden gegenereerd door deze handleiding maakt geen gebruik van Hallo ID token rechtstreeks – in plaats daarvan wordt aangeroepen `acquireTokenSilent` en/of `acquireTokenRedirect` tooacquire een *toegangstoken* tooquery Hallo Microsoft Graph API gebruikt. Als u een steekproef die het Hallo-id-token valideert moet, Bekijk [dit](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 voorbeeld") voorbeeldtoepassing in GitHub – Hallo-voorbeeld gebruikt een ASP.NET-Web-API voor validatie van tokens.

#### <a name="getting-a-user-token-interactively"></a>Een gebruiker ophalen interactief token

Initiële aanmelden na hello, u niet wilt dat Hallo vraag gebruikers tooreauthenticate telkens wanneer ze toorequest moeten een token tooaccess een resource: dus *acquireTokenSilent* moet de meeste Hallo tijd tooacquire tokens gebruikt. Er zijn echter situaties moet u gebruikers met Azure Active Directory v2 eindpunt werken – tooforce enkele voorbeelden zijn:
-   Gebruikers hebben mogelijk nodig tooreenter hun referenties omdat Hallo wachtwoord is verlopen
-   Uw toepassing vraagt toegang tooa resource die gebruiker moet tooconsent op Hallo
-   Tweeledige verificatie is vereist

Aanroepen Hallo *acquireTokenRedirect(scope)* leiden tot het omleiden van gebruikers toohello Azure Active Directory-v2-eindpunt (of *acquireTokenPopup(scope)* resultaat op een pop-upvenster) waar gebruikers nodig hebben toointeract met door ofwel hun referenties geeft Hallo toestemming toohello vereiste resource of verificatie voltooien Hallo met twee factoren.

#### <a name="getting-a-user-token-silently"></a>Een gebruiker ophalen achtergrond token
Hallo ` acquireTokenSilent` methode verwerkt token acquisities van organisaties en verlenging zonder tussenkomst van de gebruiker. Na `loginRedirect` (of `loginPopup`) wordt uitgevoerd voor Hallo eerst `acquireTokenSilent` Hallo methode gebruikte tooobtain tokens die worden gebruikt tooaccess resources voor volgende aanroepen - beveiligd als aanroepen toorequest of vernieuwen van tokens achtergrond worden aangebracht.
`acquireTokenSilent`mislukken in sommige gevallen – bijvoorbeeld Hallo gebruikerswachtwoord kan is verlopen. Uw toepassing kan verwerken van deze uitzondering op twee manieren:

1.  Te maken van een aanroep van`acquireTokenRedirect` onmiddellijk, waardoor het vragen Hallo toosign van de gebruiker in. Dit patroon wordt meestal gebruikt in toepassingen met online wanneer er geen niet-geverifieerde inhoud in Hallo toepassingen toohello beschikbaar voor gebruikers is. Hallo-voorbeeld gegenereerd met deze Begeleide installatie maakt gebruik van dit patroon.

2. Toepassingen kunnen ook een visuele indicatie toohello-gebruiker die een interactief aanmelden is vereist, zodat Hallo-gebruiker kunt selecteren Hallo juiste moment toosign in of toepassing hello opnieuw kunt maken `acquireTokenSilent` op een later tijdstip. Dit wordt meestal gebruikt wanneer Hallo gebruiker andere functionaliteit van de toepassing hello gebruiken kunt zonder wordt onderbroken: er bijvoorbeeld niet-geverifieerde inhoud beschikbaar zijn in de toepassing hello is. Hallo-gebruiker kunt in dit geval bepalen wanneer hij of zij wil toosign in tooaccess Hallo beveiligde resource of toorefresh Hallo verouderde informatie.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Hallo Hallo-token die u zojuist hebt verkregen met Microsoft Graph-API niet aanroepen

Hallo na code tooyour toevoegen `app.js` bestand:

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Meer informatie over het maken van een REST-aanroep op basis van een beveiligde API

Hallo in Hallo voorbeeldtoepassing gemaakt door deze handleiding `callWebApiWithToken()` methode is gebruikte toomake een HTTP `GET` -aanvraag in voor een beveiligde bron die een token en ga daarna terug Hallo inhoud toohello aanroeper vereist. Met deze methode wordt Hallo verkregen token in Hallo *HTTP-autorisatie-header*. Voor Hallo voorbeeldtoepassing gemaakt door deze handleiding is Hallo resource Hallo Microsoft Graph API *mij* eindpunt – Hallo van gebruikersprofielgegevens worden weergegeven.

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Een methode toosign uit Hallo gebruiker toevoegen

Hallo na code tooyour toevoegen `app.js` bestand:

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
