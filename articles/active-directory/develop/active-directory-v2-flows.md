---
title: App-typen voor de Azure Active Directory v2.0-eindpunt | Microsoft Docs
description: De typen apps en scenario's ondersteund door het Azure Active Directory v2.0-eindpunt.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 9d59e7f0e8f326c40be86e199d7712f6c565cc13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="app-types-for-the-azure-active-directory-v20-endpoint"></a><span data-ttu-id="b4ebd-103">App-typen voor de Azure Active Directory v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="b4ebd-103">App types for the Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="b4ebd-104">Het Azure Active Directory (Azure AD) v2.0-eindpunt ondersteunt verificatie voor diverse moderne app-architecturen allemaal op basis van industriestandaard-protocollen [OAuth 2.0- of OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-104">The Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="b4ebd-105">Dit artikel wordt beschreven welke typen apps die u maken kunt met behulp van Azure AD v2.0, ongeacht uw voorkeurstaal of platform.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-105">This article describes the types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="b4ebd-106">De informatie in dit artikel is bedoeld om te begrijpen geavanceerde scenario's voordat u [beginnen met werken met de code](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-106">The information in this article is designed to help you understand high-level scenarios before you [start working with the code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="b4ebd-107">Het v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="b4ebd-108">Meer informatie over om te bepalen of het v2.0-eindpunt moet worden gebruikt, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="the-basics"></a><span data-ttu-id="b4ebd-109">De basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="b4ebd-109">The basics</span></span>
<span data-ttu-id="b4ebd-110">U moet registreren elke app die gebruikmaakt van het v2.0-eindpunt in de [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-110">You must register each app that uses the v2.0 endpoint in the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="b4ebd-111">Het registratieproces app verzamelt en wijst deze waarden voor uw app:</span><span class="sxs-lookup"><span data-stu-id="b4ebd-111">The app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="b4ebd-112">Een **toepassings-ID** die wordt aangeduid uw app</span><span class="sxs-lookup"><span data-stu-id="b4ebd-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="b4ebd-113">Een **omleidings-URI** die u kunt gebruiken om te leiden antwoorden terug naar uw app</span><span class="sxs-lookup"><span data-stu-id="b4ebd-113">A **Redirect URI** that you can use to direct responses back to your app</span></span>
* <span data-ttu-id="b4ebd-114">Enkele andere scenariospecifieke waarden</span><span class="sxs-lookup"><span data-stu-id="b4ebd-114">A few other scenario-specific values</span></span>

<span data-ttu-id="b4ebd-115">Informatie voor meer informatie over hoe [een app registreren](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-115">For details, learn how to [register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="b4ebd-116">Nadat de app is geregistreerd, communiceert de app met Azure AD door verzoeken te sturen naar de Azure AD v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-116">After the app is registered, the app communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="b4ebd-117">We bieden open source frameworks en bibliotheken waarmee de details van deze aanvragen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-117">We provide open-source frameworks and libraries that handle the details of these requests.</span></span> <span data-ttu-id="b4ebd-118">U hebt ook de optie voor het implementeren van de verificatielogica zelf aanvragen voor deze eindpunten te maken:</span><span class="sxs-lookup"><span data-stu-id="b4ebd-118">You also have the option to implement the authentication logic yourself by creating requests to these endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries to link to -->

## <a name="web-apps"></a><span data-ttu-id="b4ebd-119">Web-apps</span><span class="sxs-lookup"><span data-stu-id="b4ebd-119">Web apps</span></span>
<span data-ttu-id="b4ebd-120">Voor web-apps (.NET, PHP, Java, Ruby, Python, knooppunt) dat de gebruiker via een browser gebruikt, kunt u [OpenID Connect](active-directory-v2-protocols.md) voor gebruikersaanmelding.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that the user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="b4ebd-121">In het OpenID Connect ontvangt de web-app een token ID.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-121">In OpenID Connect, the web app receives an ID token.</span></span> <span data-ttu-id="b4ebd-122">Een token ID is een beveiligingstoken dat de identiteit van de gebruiker wordt geverifieerd en bevat informatie over de gebruiker in de vorm van claims:</span><span class="sxs-lookup"><span data-stu-id="b4ebd-122">An ID token is a security token that verifies the user's identity and provides information about the user in the form of claims:</span></span>

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

<span data-ttu-id="b4ebd-123">U kunt meer informatie over de typen tokens en claims die beschikbaar zijn voor een app in de [v2.0 tokens verwijzing](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-123">You can learn about all the types of tokens and claims that are available to an app in the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="b4ebd-124">In de web server-apps duurt de authenticatiestroom-in deze stappen op hoog niveau:</span><span class="sxs-lookup"><span data-stu-id="b4ebd-124">In web server apps, the sign-in authentication flow takes these high-level steps:</span></span>

![Authenticatiestroom voor web-app](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="b4ebd-126">U kunt controleren of de identiteit van de gebruiker door het valideren van het token ID met een openbare ondertekeningssleutel die is ontvangen van het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-126">You can ensure the user's identity by validating the ID token with a public signing key that is received from the v2.0 endpoint.</span></span> <span data-ttu-id="b4ebd-127">Een sessiecookie is ingesteld, die kan worden gebruikt om de gebruiker op de volgende pagina-aanvragen te identificeren.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-127">A session cookie is set, which can be used to identify the user on subsequent page requests.</span></span>

<span data-ttu-id="b4ebd-128">Overzicht van dit scenario werkt, probeer een van de web-app aanmelden codevoorbeelden die in onze v2.0 [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-128">To see this scenario in action, try one of the web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="b4ebd-129">Naast eenvoudige aanmelden moet een webserver-app mogelijk toegang tot een andere webservice, zoals een REST-API.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-129">In addition to simple sign-in, a web server app might need to access another web service, such as a REST API.</span></span> <span data-ttu-id="b4ebd-130">In dit geval de app web server alleen mogelijk in een gecombineerde OpenID Connect en OAuth 2.0-stroom met behulp van de [OAuth 2.0-autorisatiecodestroom](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-130">In this case, the web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="b4ebd-131">Lees voor meer informatie over dit scenario over [aan de slag met web-apps en Web-API's](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="b4ebd-132">Web-API's</span><span class="sxs-lookup"><span data-stu-id="b4ebd-132">Web APIs</span></span>
<span data-ttu-id="b4ebd-133">U kunt het v2.0-eindpunt om webservices, zoals de RESTful Web-API van uw app te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-133">You can use the v2.0 endpoint to secure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="b4ebd-134">Een Web-API gebruikt een toegangstoken OAuth 2.0 in plaats van de ID-tokens en sessiecookies om de gegevens te beveiligen en om inkomende aanvragen te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token to secure its data and to authenticate incoming requests.</span></span> <span data-ttu-id="b4ebd-135">De aanroeper van een Web-API voegt een toegangstoken in de autorisatie-header van een HTTP-verzoek als volgt:</span><span class="sxs-lookup"><span data-stu-id="b4ebd-135">The caller of a Web API appends an access token in the authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="b4ebd-136">De Web-API gebruikt het toegangstoken om de identiteit van de API-aanroeper te verifiëren en informatie over de aanroeper van claims die zijn gecodeerd in het toegangstoken niet uitpakken.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-136">The Web API uses the access token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the access token.</span></span> <span data-ttu-id="b4ebd-137">Zie voor meer informatie over de typen tokens en claims die beschikbaar voor een app zijn, de [v2.0 tokens verwijzing](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-137">To learn about all the types of tokens and claims that are available to an app, see the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="b4ebd-138">Een Web-API gebruikers kunt geven de macht opt-in-of specifieke functionaliteit of gegevens afmelden bij het blootstellen van machtigingen, ook wel bekend als [scopes](active-directory-v2-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-138">A Web API can give users the power to opt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="b4ebd-139">Voor een app aanroepen te verkrijgen van de machtiging voor een scope, de gebruiker moet toestemming geven aan het bereik tijdens een stroom.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-139">For a calling app to acquire permission to a scope, the user must consent to the scope during a flow.</span></span> <span data-ttu-id="b4ebd-140">Het v2.0-eindpunt wordt de gebruiker om toestemming wordt gevraagd en vervolgens registreert machtigingen in alle toegangstokens die ontvangt van de Web-API.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-140">The v2.0 endpoint asks the user for permission, and then records permissions in all access tokens that the Web API receives.</span></span> <span data-ttu-id="b4ebd-141">De Web-API valideert de toegangstokens dit op elke aanroep ontvangt en autorisatie controles uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-141">The Web API validates the access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="b4ebd-142">Een Web-API kan toegangstokens ontvangen van alle typen apps, met inbegrip van server-web-apps, bureaublad en mobiele apps, apps van één pagina, daemons aan serverzijde en zelfs andere Web-API's.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="b4ebd-143">De stroom op hoog niveau voor een Web-API ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="b4ebd-143">The high-level flow for a Web API looks like this:</span></span>

![Web-API-authenticatiestroom](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="b4ebd-145">Bekijk voor meer informatie over hoe u een Web-API beveiligen met behulp van OAuth2-toegangstokens, de codevoorbeelden van Web-API in onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-145">To learn how to secure a Web API by using OAuth2 access tokens, check out the Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="b4ebd-146">In veel gevallen moet de web-API's ook uitgaande aanvragen in andere downstream web-API's die zijn beveiligd door Azure Active Directory aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-146">In many cases, web APIs also need to make outbound requests to other downstream web APIs secured by Azure Active Directory.</span></span>  <span data-ttu-id="b4ebd-147">Om dit te doen, web-API's kan profiteren van Azure AD **op namens** stroom, waardoor de web-API voor het uitwisselen van een binnenkomende toegangstoken voor een andere toegangstoken moet worden gebruikt in uitgaande aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-147">To do so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows the web API to exchange an incoming access token for another access token to be used in outbound requests.</span></span>  <span data-ttu-id="b4ebd-148">Het v2.0-eindpunt van namens stroom wordt beschreven in [details hier](active-directory-v2-protocols-oauth-on-behalf-of.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-148">The v2.0 endpoint's On Behalf Of flow is described in [detail here](active-directory-v2-protocols-oauth-on-behalf-of.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="b4ebd-149">Mobiele en systeemeigen apps</span><span class="sxs-lookup"><span data-stu-id="b4ebd-149">Mobile and native apps</span></span>
<span data-ttu-id="b4ebd-150">Apparaat geïnstalleerd apps, zoals mobiele en bureaublad-apps, nodig vaak toegang tot back-endservices of Web-API's die gegevens opslaan en uitvoeren van functies namens een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-150">Device-installed apps, such as mobile and desktop apps, often need to access back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="b4ebd-151">Deze apps kunnen toevoegen aan- en autorisatie aan back-end-services met behulp van de [OAuth 2.0-autorisatiecodestroom](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-151">These apps can add sign-in and authorization to back-end services by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="b4ebd-152">In deze stroom ontvangt de app een autorisatiecode van het v2.0-eindpunt wanneer de gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-152">In this flow, the app receives an authorization code from the v2.0 endpoint when the user signs in.</span></span> <span data-ttu-id="b4ebd-153">De autorisatiecode vertegenwoordigt de machtiging van de app aan te roepen back-end-services namens de gebruiker die is aangemeld.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-153">The authorization code represents the app's permission to call back-end services on behalf of the user who is signed in.</span></span> <span data-ttu-id="b4ebd-154">De app kan de autorisatiecode op de achtergrond voor een toegangstoken OAuth 2.0 en een vernieuwingstoken uitwisselen.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-154">The app can exchange the authorization code in the background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="b4ebd-155">De app kunt gebruiken van het toegangstoken voor verificatie bij de Web-API's in HTTP-aanvragen en het vernieuwingstoken gebruiken om nieuwe toegangstokens oudere toegangstokens verloopt.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-155">The app can use the access token to authenticate to Web APIs in HTTP requests, and use the refresh token to get new access tokens when older access tokens expire.</span></span>

![Systeemeigen app verificatiestroom](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="b4ebd-157">Apps met één pagina (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="b4ebd-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="b4ebd-158">Veel moderne apps hebben een front-end app met één pagina die voornamelijk in JavaScript is geschreven.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="b4ebd-159">Vaak wordt geschreven met behulp van een framework zoals AngularJS, Ember.js of Durandal.js.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="b4ebd-160">Het Azure AD v2.0-eindpunt ondersteunt deze apps met behulp van de [impliciete OAuth 2.0-stroom](active-directory-v2-protocols-implicit.md).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-160">The Azure AD v2.0 endpoint supports these apps by using the [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="b4ebd-161">In deze stroom voert de app-tokens ontvangen rechtstreeks vanuit de v2.0 eindpunt, zonder eventuele uitwisselingen server-naar-server te autoriseren.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-161">In this flow, the app receives tokens directly from the v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="b4ebd-162">Alle verificatielogica en sessie afhandeling van vindt volledig in de JavaScript-client, zonder extra paginaomleidingen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-162">All authentication logic and session handling takes place entirely in the JavaScript client, without extra page redirects.</span></span>

![Impliciete verificatiestroom](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="b4ebd-164">Overzicht van dit scenario werkt, probeer een van de codevoorbeelden van één pagina app onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-164">To see this scenario in action, try one of the single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="b4ebd-165">Daemons en serverzijde apps</span><span class="sxs-lookup"><span data-stu-id="b4ebd-165">Daemons and server-side apps</span></span>
<span data-ttu-id="b4ebd-166">Apps die langlopende processen hebben of die werken zonder interactie met een gebruiker moeten ook een manier om toegang te krijgen tot beveiligde bronnen, zoals Web-API's.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-166">Apps that have long-running processes or that operate without interaction with a user also need a way to access secured resources, such as Web APIs.</span></span> <span data-ttu-id="b4ebd-167">Deze apps kunnen verifiëren en tokens verkrijgen met behulp van de identiteit van de app in plaats van een gebruiker identiteit met het OAuth 2.0-clientreferentiestroom overgedragen.</span><span class="sxs-lookup"><span data-stu-id="b4ebd-167">These apps can authenticate and get tokens by using the app's identity, rather than a user's delegated identity, with the OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="b4ebd-168">In deze stroom voert de app communiceert rechtstreeks met de `/token` eindpunt eindpunten verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="b4ebd-168">In this flow, the app interacts directly with the `/token` endpoint to obtain endpoints:</span></span>

![Verificatiestroom daemon-app](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="b4ebd-170">Een daemon-app bouwen, Zie de documentatie van de client-referenties in onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie of probeer een [voorbeeld-app voor .NET](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span><span class="sxs-lookup"><span data-stu-id="b4ebd-170">To build a daemon app, see the client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>
