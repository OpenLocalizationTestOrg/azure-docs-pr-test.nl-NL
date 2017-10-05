---
title: Wijzigingen in de Azure AD v2.0-eindpunt | Microsoft Docs
description: Een beschrijving van wijzigingen die worden uitgevoerd in de app model v2.0 openbare preview-protocollen.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae73833a68db14804dc40eaf07ff7d3effaa9052
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="49a29-103">Belangrijke Updates voor de verificatieprotocollen v2.0</span><span class="sxs-lookup"><span data-stu-id="49a29-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="49a29-104">Ontwikkelaars aandacht!</span><span class="sxs-lookup"><span data-stu-id="49a29-104">Attention developers!</span></span> <span data-ttu-id="49a29-105">De volgende twee weken brengen we enkele updates voor onze v2.0-verificatieprotocollen die u kunnen betekenen dat de wijzigingen voor alle apps die u hebt geschreven in onze preview-periode op te splitsen.</span><span class="sxs-lookup"><span data-stu-id="49a29-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="49a29-106">Wie heeft dit invloed op?</span><span class="sxs-lookup"><span data-stu-id="49a29-106">Who does this affect?</span></span>
<span data-ttu-id="49a29-107">Alle apps die zijn geschreven voor het gebruik van het v2.0 geconvergeerde eindpunt voor authenticatie</span><span class="sxs-lookup"><span data-stu-id="49a29-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="49a29-108">Meer informatie over het v2.0-eindpunt vindt [hier](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49a29-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="49a29-109">Als u een app met het v2.0-eindpunt met de codering rechtstreeks aan het protocol v2.0 hebt gebouwd, moet met behulp van een van onze middlewares OpenID Connect of OAuth web of met andere 3e partij bibliotheken voor het uitvoeren van verificatie, u worden voorbereid voor het testen van uw projecten en wijzigingen aanbrengen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="49a29-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="49a29-110">Wie heeft niet dit invloed op?</span><span class="sxs-lookup"><span data-stu-id="49a29-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="49a29-111">Alle apps die zijn geschreven voor het eindpunt productie Azure AD-verificatie</span><span class="sxs-lookup"><span data-stu-id="49a29-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="49a29-112">Dit protocol is ingesteld in steen en worden geen wijzigingen in de problemen.</span><span class="sxs-lookup"><span data-stu-id="49a29-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="49a29-113">Bovendien, als uw app **alleen** onze ADAL-bibliotheek gebruikt voor het uitvoeren van verificatie, u hebt geen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="49a29-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="49a29-114">ADAL heeft uw app uit de wijzigingen worden afgeschermd.</span><span class="sxs-lookup"><span data-stu-id="49a29-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="49a29-115">Wat zijn de wijzigingen?</span><span class="sxs-lookup"><span data-stu-id="49a29-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="49a29-116">De waarde x5t verwijderen van JWT-headers</span><span class="sxs-lookup"><span data-stu-id="49a29-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="49a29-117">Het v2.0-eindpunt maakt gebruik van JWT-tokens uitgebreid, die een gedeelte van de parameters header met relevante metagegevens over het token bevatten.</span><span class="sxs-lookup"><span data-stu-id="49a29-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="49a29-118">Als u de koptekst van een van onze huidige JWTs decoderen, zou u ongeveer vinden:</span><span class="sxs-lookup"><span data-stu-id="49a29-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="49a29-119">Eigenschappen van de 'x5t' en 'kid' identificeren waar de openbare sleutel die moet worden gebruikt voor het valideren van de handtekening van het token, opgehaald uit het eindpunt van de metagegevens OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="49a29-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="49a29-120">De wijziging we hier maken is het verwijderen van de eigenschap 'x5t'.</span><span class="sxs-lookup"><span data-stu-id="49a29-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="49a29-121">U kunt doorgaan met het gebruik van dezelfde mechanismen om tokens te valideren, maar verstandig alleen op de eigenschap 'kid' voor het ophalen van de juiste openbare sleutel, zoals opgegeven in het OpenID Connect-protocol.</span><span class="sxs-lookup"><span data-stu-id="49a29-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="49a29-122">**Uw job: Zorg ervoor dat uw app is niet afhankelijk van de aanwezigheid van de x5t-waarde.**</span><span class="sxs-lookup"><span data-stu-id="49a29-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="49a29-123">Profile_info verwijderen</span><span class="sxs-lookup"><span data-stu-id="49a29-123">Removing profile_info</span></span>
<span data-ttu-id="49a29-124">Voorheen het v2.0-eindpunt is is een base64-gecodeerd JSON-object in retourneren token antwoorden aangeroepen `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="49a29-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="49a29-125">Bij het aanvragen van een toegangstoken van het v2.0-eindpunt met een verzoek om te verzenden:</span><span class="sxs-lookup"><span data-stu-id="49a29-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="49a29-126">Het antwoord eruit als de volgende JSON-object:</span><span class="sxs-lookup"><span data-stu-id="49a29-126">The response would look like the following JSON object:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="49a29-127">De `profile_info` waarde bevat informatie over de gebruiker die heeft aangemeld bij de app - hun weergavenaam, de voornaam, achternaam, e-mailadres, id, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="49a29-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="49a29-128">Voornamelijk om de `profile_info` is gebruikt voor het opslaan van token en op het scherm.</span><span class="sxs-lookup"><span data-stu-id="49a29-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="49a29-129">Nu worden verwijderd de `profile_info` waarde – maar maak je geen zorgen, bieden we nog steeds deze informatie voor ontwikkelaars op een iets andere plaats.</span><span class="sxs-lookup"><span data-stu-id="49a29-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="49a29-130">In plaats van `profile_info`, het v2.0-eindpunt resulteert nu een `id_token` in elk token antwoord:</span><span class="sxs-lookup"><span data-stu-id="49a29-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="49a29-131">U kunt decoderen en parseren van de id_token om op te halen van de dezelfde informatie die u hebt ontvangen van profile_info.</span><span class="sxs-lookup"><span data-stu-id="49a29-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="49a29-132">De id_token is een JSON Web Token (JWT), met inhoud zoals opgegeven door het OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="49a29-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="49a29-133">De code hiervoor dus moet vergelijkbaar: u hoeft alleen het middelste segment (de tekst) van de id_token uitpakken en decoderen van base64 deze toegang krijgt tot het JSON-object.</span><span class="sxs-lookup"><span data-stu-id="49a29-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="49a29-134">De volgende twee weken moet u de code uw app om de gebruikersgegevens van de opgehaald uit de `id_token` of `profile_info`; afhankelijk van wat aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="49a29-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="49a29-135">Op die manier wanneer de wijziging wordt aangebracht uw app kan de overgang van naadloos verwerken `profile_info` naar `id_token` zonder onderbreking.</span><span class="sxs-lookup"><span data-stu-id="49a29-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49a29-136">**Uw job: Zorg ervoor dat uw app is niet afhankelijk van de aanwezigheid van de `profile_info` waarde.**</span><span class="sxs-lookup"><span data-stu-id="49a29-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="49a29-137">Id_token_expires_in verwijderen</span><span class="sxs-lookup"><span data-stu-id="49a29-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="49a29-138">Net als bij `profile_info`, worden ook verwijderd de `id_token_expires_in` parameter van antwoorden.</span><span class="sxs-lookup"><span data-stu-id="49a29-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="49a29-139">Voorheen het v2.0-eindpunt zou waarde retourneren voor `id_token_expires_in` samen met elke id_token antwoord, bijvoorbeeld in een antwoord autoriseren:</span><span class="sxs-lookup"><span data-stu-id="49a29-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="49a29-140">Of in een token antwoord:</span><span class="sxs-lookup"><span data-stu-id="49a29-140">Or in a token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="49a29-141">De `id_token_expires_in` waarde duidt dit op het aantal seconden dat de id_token blijft geldig voor.</span><span class="sxs-lookup"><span data-stu-id="49a29-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="49a29-142">Nu we verwijdert de `id_token_expires_in` volledig waarde.</span><span class="sxs-lookup"><span data-stu-id="49a29-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="49a29-143">In plaats daarvan kunt u de standaard OpenID Connect `nbf` en `exp` controleren de geldigheid van een id_token-claims.</span><span class="sxs-lookup"><span data-stu-id="49a29-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="49a29-144">Zie de [v2.0 tokenverwijzing](active-directory-v2-tokens.md) voor meer informatie over deze claims.</span><span class="sxs-lookup"><span data-stu-id="49a29-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49a29-145">**Uw job: Zorg ervoor dat uw app is niet afhankelijk van de aanwezigheid van de `id_token_expires_in` waarde.**</span><span class="sxs-lookup"><span data-stu-id="49a29-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="49a29-146">Het wijzigen van de claims geretourneerd door een bereik openid =</span><span class="sxs-lookup"><span data-stu-id="49a29-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="49a29-147">Deze wijziging wordt de belangrijkste – in feite, heeft dit gevolgen voor vrijwel elke app die gebruikmaakt van het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="49a29-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="49a29-148">Veel toepassingen aanvragen verzenden naar het v2.0-eindpunt met behulp de `openid` bereik, zoals:</span><span class="sxs-lookup"><span data-stu-id="49a29-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="49a29-149">Vandaag, wanneer de gebruiker toestemming voor verleent de `openid` bereik, uw app een schat aan informatie over de gebruiker in de resulterende id_token ontvangt.</span><span class="sxs-lookup"><span data-stu-id="49a29-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="49a29-150">Deze claims kunnen opnemen hun naam, voorkeur gebruikersnaam, e-mailadres, object-ID en meer.</span><span class="sxs-lookup"><span data-stu-id="49a29-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="49a29-151">In deze update wordt de informatie wijzigt die de `openid` bereik kan uw apptoegang tot, voor betere comform met de specificatie van het OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="49a29-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="49a29-152">De `openid` bereik wordt alleen toe zodat uw app voor het ondertekenen van de gebruiker in en ontvangen van een app-specifiek-id voor de gebruiker in de `sub` claimen van de id_token.</span><span class="sxs-lookup"><span data-stu-id="49a29-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="49a29-153">De claims in een id_token met alleen de `openid` bereik verleend worden persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="49a29-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="49a29-154">Voorbeeld id_token claims zijn:</span><span class="sxs-lookup"><span data-stu-id="49a29-154">Example id_token claims are:</span></span>

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

<span data-ttu-id="49a29-155">Als u ophalen van persoonsgegevens (PII) over de gebruiker in uw app wilt, moet uw app om aanvullende machtigingen van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="49a29-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="49a29-156">Ondersteuning voor twee nieuwe scopes worden geïntroduceerd van het OpenID Connect-specificatie – de `email` en `profile` scopes – waarmee u kunt doen.</span><span class="sxs-lookup"><span data-stu-id="49a29-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="49a29-157">De `email` bereik is zeer eenvoudig: uw app-toegang tot het primaire e-mailadres van de gebruiker via de `email` claim in de id_token.</span><span class="sxs-lookup"><span data-stu-id="49a29-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="49a29-158">Houd er rekening mee dat de `email` claim altijd worden niet aanwezig in id_tokens – het alleen worden opgenomen als beschikbaar in het gebruikersprofiel.</span><span class="sxs-lookup"><span data-stu-id="49a29-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="49a29-159">De `profile` bereik kan uw apptoegang tot alle andere basisinformatie over de gebruiker – de naam, de voorkeur username, object-ID, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="49a29-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="49a29-160">Hiermee kunt u uw app op een wijze minimale openbaarmaking code – vraagt u de gebruiker voor de set gegevens die uw app vereist zijn ingesteld met de taak uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="49a29-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="49a29-161">Als u doorgaan met het ophalen van de volledige set van gebruikersgegevens die uw app ontvangt momenteel wilt, moet u alle drie bereiken opnemen in uw autorisatieaanvragen:</span><span class="sxs-lookup"><span data-stu-id="49a29-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="49a29-162">Uw app kunt beginnen met het verzenden van de `email` en `profile` onmiddellijk bereiken en het v2.0-eindpunt accepteert deze twee scopes en beginnen met het aanvragen van de machtigingen van gebruikers indien nodig.</span><span class="sxs-lookup"><span data-stu-id="49a29-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="49a29-163">Echter, de wijziging in de interpretatie van de `openid` bereik wordt pas van kracht een paar weken.</span><span class="sxs-lookup"><span data-stu-id="49a29-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49a29-164">**Uw job: Voeg de `profile` en `email` scopes als uw app informatie over de gebruiker vereist.**</span><span class="sxs-lookup"><span data-stu-id="49a29-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="49a29-165">Houd er rekening mee dat ADAL beide machtigingen in aanvragen standaard bevatten zal.</span><span class="sxs-lookup"><span data-stu-id="49a29-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="49a29-166">Verwijderen van de verlener afsluitende slash.</span><span class="sxs-lookup"><span data-stu-id="49a29-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="49a29-167">Voorheen werd door duurde de waarde van de certificaatverlener die wordt weergegeven in de tokens van het v2.0-eindpunt het formulier</span><span class="sxs-lookup"><span data-stu-id="49a29-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="49a29-168">De guid is waar de tenantId van de Azure AD-tenant die het token heeft afgegeven.</span><span class="sxs-lookup"><span data-stu-id="49a29-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="49a29-169">Met deze wijzigingen, wordt de waarde van de verlener pas</span><span class="sxs-lookup"><span data-stu-id="49a29-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="49a29-170">in beide tokens en in het OpenID Connect discovery-document.</span><span class="sxs-lookup"><span data-stu-id="49a29-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49a29-171">**Uw job: Zorg ervoor dat uw app in de waarde van de verlener zowel met als zonder een afsluitende slash accepteert tijdens de validatie van de verlener.**</span><span class="sxs-lookup"><span data-stu-id="49a29-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="49a29-172">Waarom wijzigen?</span><span class="sxs-lookup"><span data-stu-id="49a29-172">Why change?</span></span>
<span data-ttu-id="49a29-173">Er is de primaire reden voor de introductie van deze wijzigingen te voldoen aan de standaard OpenID Connect-specificatie.</span><span class="sxs-lookup"><span data-stu-id="49a29-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="49a29-174">We hopen verschillen tussen integreren met Microsoft identity services en andere services identiteit in de branche te beperken door OpenID Connect compatibel, dat.</span><span class="sxs-lookup"><span data-stu-id="49a29-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="49a29-175">We willen kunnen ontwikkelaars hun favoriete open-source-verificatiebibliotheken gebruiken zonder dat voor het wijzigen van de bibliotheken om Microsoft verschillen te ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="49a29-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="49a29-176">Wat kunt u doen?</span><span class="sxs-lookup"><span data-stu-id="49a29-176">What can you do?</span></span>
<span data-ttu-id="49a29-177">Vanaf vandaag, kunt u beginnen met het maken van alle wijzigingen die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="49a29-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="49a29-178">U moet onmiddellijk het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="49a29-178">You should immediately:</span></span>

1. <span data-ttu-id="49a29-179">**Verwijder eventuele afhankelijkheden op de `x5t` headerparameter.**</span><span class="sxs-lookup"><span data-stu-id="49a29-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="49a29-180">**De overgang van de juiste manier verwerken `profile_info` naar `id_token` in antwoorden van een token.**</span><span class="sxs-lookup"><span data-stu-id="49a29-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="49a29-181">**Verwijder eventuele afhankelijkheden op de `id_token_expires_in` antwoord-parameter.**</span><span class="sxs-lookup"><span data-stu-id="49a29-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="49a29-182">**Voeg de `profile` en `email` scopes aan uw app als uw app basisgebruiker informatie nodig heeft.**</span><span class="sxs-lookup"><span data-stu-id="49a29-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="49a29-183">**Waarden van de verlener in tokens zowel met als zonder een afsluitende slash accepteren.**</span><span class="sxs-lookup"><span data-stu-id="49a29-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="49a29-184">Onze [v2.0 protocoldocumentatie](active-directory-v2-protocols.md) al is bijgewerkt met deze wijzigingen, zodat u deze als referentie gebruiken kunt bij het bijwerken van uw code.</span><span class="sxs-lookup"><span data-stu-id="49a29-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="49a29-185">Als u meer vragen over het bereik van de wijzigingen hebt, aarzel niet om te bereiken ons op Twitter op @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="49a29-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="49a29-186">Hoe vaak wijzigingen protocol plaatsvindt?</span><span class="sxs-lookup"><span data-stu-id="49a29-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="49a29-187">We voorziet niet alle verder op te splitsen wijzigingen in de verificatieprotocollen.</span><span class="sxs-lookup"><span data-stu-id="49a29-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="49a29-188">We bundelt deze wijzigingen in een versie die u hebt geen te gaan via dit soort updateproces snel opnieuw elk gewenst moment opzettelijk.</span><span class="sxs-lookup"><span data-stu-id="49a29-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="49a29-189">Natuurlijk, zullen wij functies toevoegen aan de geconvergeerde v2.0 authentication-service die u van profiteren kunt, maar deze wijzigingen moet additief zijn en niet-bestaande code einde.</span><span class="sxs-lookup"><span data-stu-id="49a29-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="49a29-190">Tot slot willen we spreken Hartelijk dank voor dingen uitprobeert tijdens de preview-periode.</span><span class="sxs-lookup"><span data-stu-id="49a29-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="49a29-191">Inzicht en ervaringen van onze vroege gebruikers zijn waardevol zijn tot nu toe, en we hopen dat u hebt uw mening en ideeën delen.</span><span class="sxs-lookup"><span data-stu-id="49a29-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="49a29-192">Gelukkig coderen!</span><span class="sxs-lookup"><span data-stu-id="49a29-192">Happy coding!</span></span>

<span data-ttu-id="49a29-193">De deling van de Microsoft-identiteitsbeheer</span><span class="sxs-lookup"><span data-stu-id="49a29-193">The Microsoft Identity Division</span></span>

