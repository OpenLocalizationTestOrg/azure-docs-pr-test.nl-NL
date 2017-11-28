---
title: aaaApp typen voor hello Azure Active Directory v2.0-eindpunt | Microsoft Docs
description: Hallo typen apps en scenario's ondersteund door hello Azure Active Directory v2.0-eindpunt.
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
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a><span data-ttu-id="3c1d6-103">App-typen voor hello Azure Active Directory v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="3c1d6-103">App types for hello Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="3c1d6-104">Hello Azure Active Directory (Azure AD) v2.0-eindpunt ondersteunt verificatie voor diverse moderne app-architecturen allemaal op basis van industriestandaard-protocollen [OAuth 2.0- of OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-104">hello Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="3c1d6-105">Dit artikel wordt beschreven Hallo typen apps die u maken kunt met behulp van Azure AD v2.0, ongeacht uw voorkeurstaal of platform.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-105">This article describes hello types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="3c1d6-106">Hallo informatie in dit artikel is ontworpen toohelp u inzicht in geavanceerde scenario's voordat u [beginnen met werken met Hallo code](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-106">hello information in this article is designed toohelp you understand high-level scenarios before you [start working with hello code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="3c1d6-107">Hallo v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-107">hello v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="3c1d6-108">toodetermine of Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-108">toodetermine whether you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="hello-basics"></a><span data-ttu-id="3c1d6-109">Hallo-basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="3c1d6-109">hello basics</span></span>
<span data-ttu-id="3c1d6-110">U moet elke app die gebruikmaakt van Hallo v2.0-eindpunt in Hallo registreren [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-110">You must register each app that uses hello v2.0 endpoint in hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="3c1d6-111">Hallo app registratieproces verzamelt en wijst deze waarden voor uw app:</span><span class="sxs-lookup"><span data-stu-id="3c1d6-111">hello app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="3c1d6-112">Een **toepassings-ID** die wordt aangeduid uw app</span><span class="sxs-lookup"><span data-stu-id="3c1d6-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="3c1d6-113">Een **omleidings-URI** waarmee u toodirect antwoorden back tooyour app kunt</span><span class="sxs-lookup"><span data-stu-id="3c1d6-113">A **Redirect URI** that you can use toodirect responses back tooyour app</span></span>
* <span data-ttu-id="3c1d6-114">Enkele andere scenariospecifieke waarden</span><span class="sxs-lookup"><span data-stu-id="3c1d6-114">A few other scenario-specific values</span></span>

<span data-ttu-id="3c1d6-115">Voor meer informatie, meer informatie over hoe te[een app registreren](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-115">For details, learn how too[register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="3c1d6-116">Nadat het Hallo-app is geregistreerd, communiceert de Hallo-app met Azure AD door te verzenden aanvragen toohello Azure AD v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-116">After hello app is registered, hello app communicates with Azure AD by sending requests toohello Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="3c1d6-117">We bieden open source frameworks en bibliotheken waarmee Hallo details van deze aanvragen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-117">We provide open-source frameworks and libraries that handle hello details of these requests.</span></span> <span data-ttu-id="3c1d6-118">U hebt ook Hallo optie tooimplement Hallo verificatielogica zelf aanvragen toothese eindpunten maken:</span><span class="sxs-lookup"><span data-stu-id="3c1d6-118">You also have hello option tooimplement hello authentication logic yourself by creating requests toothese endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a><span data-ttu-id="3c1d6-119">Web-apps</span><span class="sxs-lookup"><span data-stu-id="3c1d6-119">Web apps</span></span>
<span data-ttu-id="3c1d6-120">Voor web-apps (.NET, PHP, Java, Ruby, Python, knooppunt) die gebruiker toegang krijgt via een browser hello, kunt u [OpenID Connect](active-directory-v2-protocols.md) voor gebruikersaanmelding.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that hello user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="3c1d6-121">In het OpenID Connect ontvangt Hallo web-app een token ID.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-121">In OpenID Connect, hello web app receives an ID token.</span></span> <span data-ttu-id="3c1d6-122">Een token ID is een beveiligingstoken dat Hallo gebruikersidentiteit controleert en bevat informatie over het Hallo-gebruiker in de vorm van claims Hallo:</span><span class="sxs-lookup"><span data-stu-id="3c1d6-122">An ID token is a security token that verifies hello user's identity and provides information about hello user in hello form of claims:</span></span>

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

<span data-ttu-id="3c1d6-123">U kunt meer informatie over alle Hallo typen tokens en claims die beschikbaar tooan-app in Hallo [v2.0 tokens verwijzing](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-123">You can learn about all hello types of tokens and claims that are available tooan app in hello [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="3c1d6-124">In de web server-apps duurt het Hallo-in authenticatiestroom deze stappen op hoog niveau:</span><span class="sxs-lookup"><span data-stu-id="3c1d6-124">In web server apps, hello sign-in authentication flow takes these high-level steps:</span></span>

![Authenticatiestroom voor web-app](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="3c1d6-126">U kunt controleren of Hallo gebruikersidentiteit door het Hallo-id-token te valideren met een openbare ondertekeningssleutel die is ontvangen van Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-126">You can ensure hello user's identity by validating hello ID token with a public signing key that is received from hello v2.0 endpoint.</span></span> <span data-ttu-id="3c1d6-127">Een sessiecookie is ingesteld, wat kan gebruikte tooidentify Hallo gebruiker op de volgende pagina-aanvragen zijn.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-127">A session cookie is set, which can be used tooidentify hello user on subsequent page requests.</span></span>

<span data-ttu-id="3c1d6-128">toosee dit scenario werkt, probeer een van de Hallo web-app aanmelden code-voorbeelden in onze v2.0 [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-128">toosee this scenario in action, try one of hello web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="3c1d6-129">Bovendien toosimple aanmelden moet een webserver-app mogelijk tooaccess een andere webservice, zoals een REST-API.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-129">In addition toosimple sign-in, a web server app might need tooaccess another web service, such as a REST API.</span></span> <span data-ttu-id="3c1d6-130">In dit geval Hallo webserver-app alleen mogelijk in een gecombineerde OpenID Connect en OAuth 2.0-stroom met behulp van Hallo [OAuth 2.0-autorisatiecodestroom](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-130">In this case, hello web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using hello [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="3c1d6-131">Lees voor meer informatie over dit scenario over [aan de slag met web-apps en Web-API's](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="3c1d6-132">Web-API's</span><span class="sxs-lookup"><span data-stu-id="3c1d6-132">Web APIs</span></span>
<span data-ttu-id="3c1d6-133">U kunt Hallo v2.0-eindpunt toosecure webservices, zoals de RESTful Web-API van uw app kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-133">You can use hello v2.0 endpoint toosecure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="3c1d6-134">In plaats van de ID-tokens en sessiecookies een Web-API maakt gebruik van een token toosecure voor OAuth 2.0-toegang tot de gegevens en tooauthenticate binnenkomende aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token toosecure its data and tooauthenticate incoming requests.</span></span> <span data-ttu-id="3c1d6-135">Hallo aanroeper van een Web-API voegt een toegangstoken in Hallo autorisatie-header van een HTTP-verzoek als volgt:</span><span class="sxs-lookup"><span data-stu-id="3c1d6-135">hello caller of a Web API appends an access token in hello authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="3c1d6-136">Hallo-Web-API gebruikt Hallo access token tooverify Hallo API aanroeper identiteits- en tooextract informatie over de aanroeper van claims die zijn gecodeerd in toegangstoken Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-136">hello Web API uses hello access token tooverify hello API caller's identity and tooextract information about hello caller from claims that are encoded in hello access token.</span></span> <span data-ttu-id="3c1d6-137">toolearn over alle Hallo typen tokens en claims die beschikbaar tooan app, Zie Hallo [v2.0 tokens verwijzing](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-137">toolearn about all hello types of tokens and claims that are available tooan app, see hello [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="3c1d6-138">Een Web-API kunt geeft gebruikers Hallo power tooopt in of specifieke functionaliteit of gegevens afmelden bij het blootstellen van machtigingen, ook wel bekend als [scopes](active-directory-v2-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-138">A Web API can give users hello power tooopt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="3c1d6-139">Voor een aanroepen app tooacquire machtiging tooa scope, Hallo gebruiker toestemming moet geven toohello bereik tijdens een stroom.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-139">For a calling app tooacquire permission tooa scope, hello user must consent toohello scope during a flow.</span></span> <span data-ttu-id="3c1d6-140">Hallo v2.0-eindpunt Hallo-gebruiker om toestemming wordt gevraagd en vervolgens registreert machtigingen in alle toegangstokens die Hallo die web API ontvangt.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-140">hello v2.0 endpoint asks hello user for permission, and then records permissions in all access tokens that hello Web API receives.</span></span> <span data-ttu-id="3c1d6-141">Hallo-Web-API valideert Hallo toegangstokens dit op elke aanroep ontvangt en autorisatie controles uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-141">hello Web API validates hello access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="3c1d6-142">Een Web-API kan toegangstokens ontvangen van alle typen apps, met inbegrip van server-web-apps, bureaublad en mobiele apps, apps van één pagina, daemons aan serverzijde en zelfs andere Web-API's.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="3c1d6-143">Hallo op hoog niveau stroom voor een Web-API ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="3c1d6-143">hello high-level flow for a Web API looks like this:</span></span>

![Web-API-authenticatiestroom](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="3c1d6-145">toolearn hoe toosecure een Web-API met OAuth2-toegangstokens, uitchecken Hallo Web API-code-voorbeelden in onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-145">toolearn how toosecure a Web API by using OAuth2 access tokens, check out hello Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="3c1d6-146">Web-API's in veel gevallen moet ook toomake uitgaande aanvragen tooother downstream web-API's die zijn beveiligd door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-146">In many cases, web APIs also need toomake outbound requests tooother downstream web APIs secured by Azure Active Directory.</span></span>  <span data-ttu-id="3c1d6-147">toodo dus web-API's kan profiteren van Azure AD **op namens** stroom, waardoor Hallo web-API tooexchange een binnenkomende toegangstoken voor een andere access token toobe gebruikt in uitgaande aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-147">toodo so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows hello web API tooexchange an incoming access token for another access token toobe used in outbound requests.</span></span>  <span data-ttu-id="3c1d6-148">Hallo v2.0-eindpunt namens stroom wordt beschreven in [details hier](active-directory-v2-protocols-oauth-on-behalf-of.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-148">hello v2.0 endpoint's On Behalf Of flow is described in [detail here](active-directory-v2-protocols-oauth-on-behalf-of.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="3c1d6-149">Mobiele en systeemeigen apps</span><span class="sxs-lookup"><span data-stu-id="3c1d6-149">Mobile and native apps</span></span>
<span data-ttu-id="3c1d6-150">Apparaat geïnstalleerd apps, zoals mobiele en bureaublad-apps, moeten vaak tooaccess back-endservices of Web-API's die gegevens opslaan en uitvoeren van functies namens een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-150">Device-installed apps, such as mobile and desktop apps, often need tooaccess back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="3c1d6-151">Deze apps aanmelden en autorisatie tooback-end-services kunnen toevoegen met behulp van Hallo [OAuth 2.0-autorisatiecodestroom](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-151">These apps can add sign-in and authorization tooback-end services by using hello [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="3c1d6-152">In deze stroom ontvangt Hallo app een autorisatiecode Hallo v2.0-eindpunt wanneer Hallo gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-152">In this flow, hello app receives an authorization code from hello v2.0 endpoint when hello user signs in.</span></span> <span data-ttu-id="3c1d6-153">Hallo autorisatie code vertegenwoordigt Hallo van app machtiging toocall back-end-services namens Hallo-gebruiker die is aangemeld.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-153">hello authorization code represents hello app's permission toocall back-end services on behalf of hello user who is signed in.</span></span> <span data-ttu-id="3c1d6-154">Hallo-app kan de autorisatiecode Hallo op de achtergrond Hallo voor een toegangstoken OAuth 2.0 en een vernieuwingstoken uitwisselen.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-154">hello app can exchange hello authorization code in hello background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="3c1d6-155">Hallo-app kunt gebruiken Hallo access token tooauthenticate tooWeb API's in HTTP-aanvragen en Hallo vernieuwen token tooget nieuwe toegangstokens gebruiken wanneer oudere toegangstokens verlopen.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-155">hello app can use hello access token tooauthenticate tooWeb APIs in HTTP requests, and use hello refresh token tooget new access tokens when older access tokens expire.</span></span>

![Systeemeigen app verificatiestroom](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="3c1d6-157">Apps met één pagina (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="3c1d6-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="3c1d6-158">Veel moderne apps hebben een front-end app met één pagina die voornamelijk in JavaScript is geschreven.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="3c1d6-159">Vaak wordt geschreven met behulp van een framework zoals AngularJS, Ember.js of Durandal.js.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="3c1d6-160">Hello Azure AD v2.0-eindpunt ondersteunt deze apps via Hallo [impliciete OAuth 2.0-stroom](active-directory-v2-protocols-implicit.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-160">hello Azure AD v2.0 endpoint supports these apps by using hello [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="3c1d6-161">In deze stroom Hallo app-tokens rechtstreeks van ontvangen Hallo v2.0 autoriseren eindpunt, zonder eventuele uitwisselingen server-naar-server.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-161">In this flow, hello app receives tokens directly from hello v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="3c1d6-162">Alle verificatielogica en sessie afhandeling van vindt volledig in Hallo JavaScript-client, zonder extra paginaomleidingen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-162">All authentication logic and session handling takes place entirely in hello JavaScript client, without extra page redirects.</span></span>

![Impliciete verificatiestroom](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="3c1d6-164">toosee dit scenario werkt, probeer een van de Hallo één pagina app-codevoorbeelden in onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-164">toosee this scenario in action, try one of hello single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="3c1d6-165">Daemons en serverzijde apps</span><span class="sxs-lookup"><span data-stu-id="3c1d6-165">Daemons and server-side apps</span></span>
<span data-ttu-id="3c1d6-166">Apps die langlopende processen hebben of die werken zonder interactie met een gebruiker moeten ook een manier tooaccess bronnen, zoals Web-API's beveiligde.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-166">Apps that have long-running processes or that operate without interaction with a user also need a way tooaccess secured resources, such as Web APIs.</span></span> <span data-ttu-id="3c1d6-167">Deze apps kunnen verifiëren en tokens verkrijgen met de identiteit van de app Hallo in plaats van een gebruiker overgedragen identiteit met clientreferentiestroom Hallo OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-167">These apps can authenticate and get tokens by using hello app's identity, rather than a user's delegated identity, with hello OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="3c1d6-168">In deze stroom Hallo app communiceert rechtstreeks met de Hallo `/token` eindpunt tooobtain eindpunten:</span><span class="sxs-lookup"><span data-stu-id="3c1d6-168">In this flow, hello app interacts directly with hello `/token` endpoint tooobtain endpoints:</span></span>

![Verificatiestroom daemon-app](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="3c1d6-170">een app daemon toobuild Zie Hallo client referenties documentatie in onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie of probeer een [voorbeeld-app voor .NET](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-170">toobuild a daemon app, see hello client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>
