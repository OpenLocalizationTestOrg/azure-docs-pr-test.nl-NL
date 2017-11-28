---
title: aaaChanges toohello Azure AD v2.0-eindpunt | Microsoft Docs
description: Een beschrijving van wijzigingen die toohello app model v2.0 openbare preview-protocollen worden uitgevoerd.
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
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a><span data-ttu-id="c46b5-103">Belangrijke Updates toohello v2.0 verificatieprotocollen</span><span class="sxs-lookup"><span data-stu-id="c46b5-103">Important Updates toohello v2.0 Authentication Protocols</span></span>
<span data-ttu-id="c46b5-104">Ontwikkelaars aandacht!</span><span class="sxs-lookup"><span data-stu-id="c46b5-104">Attention developers!</span></span> <span data-ttu-id="c46b5-105">Via Hallo brengen volgende twee weken, we een aantal updates tooour v2.0-verificatieprotocollen die u kunnen betekenen dat de wijzigingen voor alle apps die u hebt geschreven in onze preview-periode op te splitsen.</span><span class="sxs-lookup"><span data-stu-id="c46b5-105">Over hello next two weeks, we will be making a few updates tooour v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="c46b5-106">Wie heeft dit invloed op?</span><span class="sxs-lookup"><span data-stu-id="c46b5-106">Who does this affect?</span></span>
<span data-ttu-id="c46b5-107">Alle apps die zijn geschreven toouse Hallo v2.0 geconvergeerde eindpunt voor authenticatie</span><span class="sxs-lookup"><span data-stu-id="c46b5-107">Any apps that have been written toouse hello v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="c46b5-108">Meer informatie over het v2.0-eindpunt Hallo vindt [hier](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c46b5-108">More information on hello v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="c46b5-109">Als u een app met Hallo v2.0-eindpunt door rechtstreeks toohello v2.0 protocol coderen hebt gebouwd met een van onze middlewares OpenID Connect of OAuth web of andere 3e partij bibliotheken tooperform verificatie gebruikt, u moet voorbereid tootest projecten en maken wijzigingen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c46b5-109">If you have built an app using hello v2.0 endpoint by coding directly toohello v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries tooperform authentication, you should be prepared tootest your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="c46b5-110">Wie heeft niet dit invloed op?</span><span class="sxs-lookup"><span data-stu-id="c46b5-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="c46b5-111">Alle apps die zijn geschreven voor Hallo productie Azure AD authentication eindpunt</span><span class="sxs-lookup"><span data-stu-id="c46b5-111">Any apps that have been written against hello production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="c46b5-112">Dit protocol is ingesteld in steen en worden geen wijzigingen in de problemen.</span><span class="sxs-lookup"><span data-stu-id="c46b5-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="c46b5-113">Bovendien als uw app **alleen** onze ADAL-bibliotheek tooperform verificatie, gebruikt u hebt geen toochange alles.</span><span class="sxs-lookup"><span data-stu-id="c46b5-113">Furthermore, if your app **only** uses our ADAL library tooperform authentication, you won\`t have toochange anything.</span></span>  <span data-ttu-id="c46b5-114">ADAL, is uw app uit Hallo wijzigingen afgeschermd.</span><span class="sxs-lookup"><span data-stu-id="c46b5-114">ADAL has shielded your app from hello changes.</span></span>  

## <a name="what-are-hello-changes"></a><span data-ttu-id="c46b5-115">Wat zijn Hallo wijzigingen?</span><span class="sxs-lookup"><span data-stu-id="c46b5-115">What are hello changes?</span></span>
### <a name="removing-hello-x5t-value-from-jwt-headers"></a><span data-ttu-id="c46b5-116">Hallo x5t waarde verwijderen uit een JWT-headers</span><span class="sxs-lookup"><span data-stu-id="c46b5-116">Removing hello x5t value from JWT headers</span></span>
<span data-ttu-id="c46b5-117">Hallo v2.0-eindpunt maakt gebruik van JWT-tokens uitgebreid, die een gedeelte van de parameters header met relevante metagegevens over Hallo token bevatten.</span><span class="sxs-lookup"><span data-stu-id="c46b5-117">hello v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about hello token.</span></span>  <span data-ttu-id="c46b5-118">Als u Hallo-header van een van onze huidige JWTs decoderen, zou u ongeveer vinden:</span><span class="sxs-lookup"><span data-stu-id="c46b5-118">If you decode hello header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="c46b5-119">Waar de eigenschappen van beide Hallo 'x5t' en 'kind' hello openbare sleutel identificeren die moet gebruikte toovalidate Hallo token handtekening, zoals het ophalen van metagegevens-eindpunt met OpenID Connect Hallo.</span><span class="sxs-lookup"><span data-stu-id="c46b5-119">Where both hello "x5t" and "kid" properties identify hello public key that should be used toovalidate hello token\`s signature, as retrieved from hello OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="c46b5-120">Hallo wijziging we hier maken is tooremove Hallo 'x5t'-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c46b5-120">hello change we are making here is tooremove hello "x5t" property.</span></span>  <span data-ttu-id="c46b5-121">U kunt doorgaan toouse Hallo dezelfde mechanismen toovalidate tokens, maar verstandig alleen op Hallo 'kind' eigenschap tooretrieve Hallo juiste openbare sleutel, als de opgegeven in de Hallo OpenID Connect-protocol.</span><span class="sxs-lookup"><span data-stu-id="c46b5-121">You may continue toouse hello same mechanisms toovalidate tokens, but should rely only on hello "kid" property tooretrieve hello correct public key, as specified in hello OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c46b5-122">**Uw job: Zorg ervoor dat uw app is niet afhankelijk van Hallo Hallo x5t waarde bestaan.**</span><span class="sxs-lookup"><span data-stu-id="c46b5-122">**Your job: Make sure your app does not depend on hello existence of hello x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="c46b5-123">Profile_info verwijderen</span><span class="sxs-lookup"><span data-stu-id="c46b5-123">Removing profile_info</span></span>
<span data-ttu-id="c46b5-124">Voorheen Hallo v2.0-eindpunt is is een base64-gecodeerd JSON-object in retourneren token antwoorden aangeroepen `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="c46b5-124">Previously, hello v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="c46b5-125">Bij het aanvragen van een toegangstoken van Hallo v2.0-eindpunt met het verzenden van een aanvraag naar:</span><span class="sxs-lookup"><span data-stu-id="c46b5-125">When requesting an access token from hello v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="c46b5-126">antwoord Hallo eruit als Hallo JSON-object te volgen:</span><span class="sxs-lookup"><span data-stu-id="c46b5-126">hello response would look like hello following JSON object:</span></span>

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

<span data-ttu-id="c46b5-127">Hallo `profile_info` waarde bevat informatie over Hallo-gebruiker die zich aangemeld op Hallo app - hun weergavenaam, de voornaam, achternaam, e-mailadres, id, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c46b5-127">hello `profile_info` value contained information about hello user who signed into hello app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="c46b5-128">Hallo voornamelijk om `profile_info` is gebruikt voor het opslaan van token en op het scherm.</span><span class="sxs-lookup"><span data-stu-id="c46b5-128">Primarily, hello `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="c46b5-129">Hallo worden nu verwijderd `profile_info` waarde – maar maak je geen zorgen, bieden we nog steeds deze toodevelopers informatie op een iets andere plaats.</span><span class="sxs-lookup"><span data-stu-id="c46b5-129">We are now removing hello `profile_info` value – but don't worry, we are still providing this information toodevelopers in a slightly different place.</span></span>  <span data-ttu-id="c46b5-130">In plaats van `profile_info`, Hallo v2.0-eindpunt resulteert nu een `id_token` in elk token antwoord:</span><span class="sxs-lookup"><span data-stu-id="c46b5-130">Instead of `profile_info`, hello v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="c46b5-131">U kunt decoderen en parseren Hallo id_token tooretrieve Hallo dezelfde informatie die u hebt ontvangen van profile_info.</span><span class="sxs-lookup"><span data-stu-id="c46b5-131">You may decode and parse hello id_token tooretrieve hello same information that you received from profile_info.</span></span>  <span data-ttu-id="c46b5-132">Hallo id_token is een JSON Web Token (JWT), met inhoud zoals opgegeven door het OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="c46b5-132">hello id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="c46b5-133">Hallo code Hiertoe moet vergelijkbaar: u hoeft alleen tooextract Hallo midden segment (tekst hello) van Hallo id_token en base64 dit tooaccess Hallo JSON-object binnen decoderen.</span><span class="sxs-lookup"><span data-stu-id="c46b5-133">hello code for doing so should be very similar – you simply need tooextract hello middle segment (hello body) of hello id_token and base64 decode it tooaccess hello JSON object within.</span></span>

<span data-ttu-id="c46b5-134">Via Hallo volgende twee weken, u moet de code van uw app tooretrieve Hallo gebruikersgegevens uit beide Hallo `id_token` of `profile_info`; afhankelijk van wat aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="c46b5-134">Over hello next two weeks, you should code your app tooretrieve hello user information from either hello `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="c46b5-135">Op die manier wanneer Hallo wijziging wordt aangebracht uw app aankan naadloos Hallo overgang van `profile_info` te`id_token` zonder onderbreking.</span><span class="sxs-lookup"><span data-stu-id="c46b5-135">That way when hello change is made, your app can seamlessly handle hello transition from `profile_info` too`id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c46b5-136">**Uw job: Zorg ervoor dat uw app is niet afhankelijk van Hallo bestaan Hallo `profile_info` waarde.**</span><span class="sxs-lookup"><span data-stu-id="c46b5-136">**Your job: Make sure your app does not depend on hello existence of hello `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="c46b5-137">Id_token_expires_in verwijderen</span><span class="sxs-lookup"><span data-stu-id="c46b5-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="c46b5-138">Vergelijkbare te`profile_info`, worden ook verwijderd Hallo `id_token_expires_in` parameter van antwoorden.</span><span class="sxs-lookup"><span data-stu-id="c46b5-138">Similar too`profile_info`, we are also removing hello `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="c46b5-139">Voorheen Hallo v2.0-eindpunt zou waarde retourneren voor `id_token_expires_in` samen met elke id_token antwoord, bijvoorbeeld in een antwoord autoriseren:</span><span class="sxs-lookup"><span data-stu-id="c46b5-139">Previously, hello v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="c46b5-140">Of in een token antwoord:</span><span class="sxs-lookup"><span data-stu-id="c46b5-140">Or in a token response:</span></span>

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

<span data-ttu-id="c46b5-141">Hallo `id_token_expires_in` waarde duidt dit op het aantal seconden Hallo id_token blijft geldig voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="c46b5-141">hello `id_token_expires_in` value would indicate hello number of seconds hello id_token would remain valid for.</span></span>  <span data-ttu-id="c46b5-142">Nu we Hallo verwijdert `id_token_expires_in` volledig waarde.</span><span class="sxs-lookup"><span data-stu-id="c46b5-142">Now, we are removing hello `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="c46b5-143">In plaats daarvan kunt u Hallo OpenID Connect standaard `nbf` en `exp` tooexamine Hallo geldigheid van een id_token claims.</span><span class="sxs-lookup"><span data-stu-id="c46b5-143">Instead, you may use hello OpenID Connect standard `nbf` and `exp` claims tooexamine hello validity of an id_token.</span></span>  <span data-ttu-id="c46b5-144">Zie Hallo [v2.0 tokenverwijzing](active-directory-v2-tokens.md) voor meer informatie over deze claims.</span><span class="sxs-lookup"><span data-stu-id="c46b5-144">See hello [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c46b5-145">**Uw job: Zorg ervoor dat uw app is niet afhankelijk van Hallo bestaan Hallo `id_token_expires_in` waarde.**</span><span class="sxs-lookup"><span data-stu-id="c46b5-145">**Your job: Make sure your app does not depend on hello existence of hello `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a><span data-ttu-id="c46b5-146">Hallo claims geretourneerd door een bereik wijzigen openid =</span><span class="sxs-lookup"><span data-stu-id="c46b5-146">Changing hello claims returned by scope=openid</span></span>
<span data-ttu-id="c46b5-147">Deze wijziging wordt de meest significante – Hallo in feite, heeft dit gevolgen voor vrijwel elke app die gebruikmaakt van Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="c46b5-147">This change will be hello most significant – in fact, it will affect almost every app that uses hello v2.0 endpoint.</span></span>  <span data-ttu-id="c46b5-148">Veel toepassingen verzenden aanvragen toohello v2.0-eindpunt met Hallo `openid` bereik, zoals:</span><span class="sxs-lookup"><span data-stu-id="c46b5-148">Many applications send requests toohello v2.0 endpoint using hello `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="c46b5-149">Vandaag, wanneer Hallo gebruiker toestemming voor Hallo verleent `openid` bereik, uw app ontvangt een schat aan informatie over Hallo gebruiker in de resulterende id_token Hallo.</span><span class="sxs-lookup"><span data-stu-id="c46b5-149">Today, when hello user grants consent for hello `openid` scope, your app receives a wealth of information about hello user in hello resulting id_token.</span></span>  <span data-ttu-id="c46b5-150">Deze claims kunnen opnemen hun naam, voorkeur gebruikersnaam, e-mailadres, object-ID en meer.</span><span class="sxs-lookup"><span data-stu-id="c46b5-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="c46b5-151">In deze update we wijzigt Hallo informatie die Hallo `openid` bereik kan uw apptoegang tot, toobetter comform Hello OpenID Connect-specificatie.</span><span class="sxs-lookup"><span data-stu-id="c46b5-151">In this update, we are changing hello information that hello `openid` scope affords your app access to, toobetter comform with hello OpenID Connect specification.</span></span>  <span data-ttu-id="c46b5-152">Hallo `openid` bereik wordt alleen toestaan van uw app toosign Hallo gebruiker in en ontvangt een app-specifiek-id voor de gebruiker Hallo in Hallo `sub` van Hallo id_token claim.</span><span class="sxs-lookup"><span data-stu-id="c46b5-152">hello `openid` scope will only allow your app toosign hello user in, and receive an app-specific identifier for hello user in hello `sub` claim of hello id_token.</span></span>  <span data-ttu-id="c46b5-153">claims in een id_token Hallo alleen hello `openid` bereik verleend worden persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="c46b5-153">hello claims in an id_token with only hello `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="c46b5-154">Voorbeeld id_token claims zijn:</span><span class="sxs-lookup"><span data-stu-id="c46b5-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="c46b5-155">Als u tooobtain persoonsgegevens (PII) over Hallo gebruiker in uw app wilt, moet uw app toorequest extra machtigingen van Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c46b5-155">If you want tooobtain personally identifiable information (PII) about hello user in your app, your app will need toorequest additional permissions from hello user.</span></span>  <span data-ttu-id="c46b5-156">We introduceert ondersteuning voor twee nieuwe scopes uit Hallo OpenID Connect spec – hello `email` en `profile` scopes – waarmee u toodo dus.</span><span class="sxs-lookup"><span data-stu-id="c46b5-156">We are introducing support for two new scopes from hello OpenID Connect spec – hello `email` and `profile` scopes – which allow you toodo so.</span></span>

* <span data-ttu-id="c46b5-157">Hallo `email` bereik is zeer eenvoudig: het primaire e-mailadres van uw app toegang toohello gebruiker via Hallo kunt `email` in Hallo id_token claim.</span><span class="sxs-lookup"><span data-stu-id="c46b5-157">hello `email` scope is very straightforward – it allows your app access toohello user's primary email address via hello `email` claim in hello id_token.</span></span>  <span data-ttu-id="c46b5-158">Houd er rekening mee dat Hallo `email` claim altijd worden niet aanwezig in id_tokens – het alleen worden opgenomen als beschikbaar in Hallo gebruikersprofiel.</span><span class="sxs-lookup"><span data-stu-id="c46b5-158">Note that hello `email` claim will not always be present in id_tokens – it will only be included if available in hello user's profile.</span></span>
* <span data-ttu-id="c46b5-159">Hallo `profile` bereik kan uw app toegang tooall andere basisinformatie over Hallo gebruiker – de naam, de voorkeur username, object-ID, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c46b5-159">hello `profile` scope affords your app access tooall other basic information about hello user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="c46b5-160">Hiermee kunt u toocode uw app op een wijze minimale openbaarmaking – vraagt u Hallo gebruiker voor NET Hallo reeks gegevens dat uw app toodo de taak vereist.</span><span class="sxs-lookup"><span data-stu-id="c46b5-160">This allows you toocode your app in a minimal-disclosure fashion – you can ask hello user for just hello set of information that your app requires toodo its job.</span></span>  <span data-ttu-id="c46b5-161">Als u ophalen van de volledige set Hallo gebruikersgegevens die uw app momenteel ontvangt toocontinue wilt, moet u alle drie bereiken opnemen in uw autorisatieaanvragen:</span><span class="sxs-lookup"><span data-stu-id="c46b5-161">If you want toocontinue getting hello full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="c46b5-162">Uw app kunt beginnen met het verzenden van Hallo `email` en `profile` onmiddellijk bereiken en Hallo v2.0-eindpunt accepteert deze twee scopes en beginnen met het aanvragen van de machtigingen van gebruikers indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c46b5-162">Your app can begin sending hello `email` and `profile` scopes immediately, and hello v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="c46b5-163">Echter Hallo wijzigen in Hallo interpretatie van Hallo `openid` bereik wordt pas van kracht een paar weken.</span><span class="sxs-lookup"><span data-stu-id="c46b5-163">However, hello change in hello interpretation of hello `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c46b5-164">**Uw job: Hallo toevoegen `profile` en `email` scopes als uw app informatie over Hallo gebruiker vereist.**</span><span class="sxs-lookup"><span data-stu-id="c46b5-164">**Your job: Add hello `profile` and `email` scopes if your app requires information about hello user.**</span></span>  <span data-ttu-id="c46b5-165">Houd er rekening mee dat ADAL beide machtigingen in aanvragen standaard bevatten zal.</span><span class="sxs-lookup"><span data-stu-id="c46b5-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a><span data-ttu-id="c46b5-166">Hallo verlener afsluitende slash te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c46b5-166">Removing hello issuer trailing slash.</span></span>
<span data-ttu-id="c46b5-167">Voorheen duurde Hallo verlener waarde die wordt weergegeven in de tokens van Hallo v2.0-eindpunt Hallo formulier</span><span class="sxs-lookup"><span data-stu-id="c46b5-167">Previously, hello issuer value that appears in tokens from hello v2.0 endpoint took hello form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="c46b5-168">Hallo-guid is waar Hallo tenantId van hello Azure AD-tenant die Hallo token heeft afgegeven.</span><span class="sxs-lookup"><span data-stu-id="c46b5-168">Where hello guid was hello tenantId of hello Azure AD tenant which issued hello token.</span></span>  <span data-ttu-id="c46b5-169">Met deze wijzigingen wordt Hallo verlener waarde</span><span class="sxs-lookup"><span data-stu-id="c46b5-169">With these changes, hello issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="c46b5-170">in beide tokens en Hallo OpenID Connect discovery-document.</span><span class="sxs-lookup"><span data-stu-id="c46b5-170">in both tokens and in hello OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c46b5-171">**Uw job: Zorg ervoor dat uw app Hallo verlener waarde zowel met als zonder een afsluitende slash tijdens het valideren van certificaatverlener accepteert.**</span><span class="sxs-lookup"><span data-stu-id="c46b5-171">**Your job: Make sure your app accepts hello issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="c46b5-172">Waarom wijzigen?</span><span class="sxs-lookup"><span data-stu-id="c46b5-172">Why change?</span></span>
<span data-ttu-id="c46b5-173">Hallo primaire reden voor het introduceren van deze wijzigingen is toobe compatibel zijn met de Hallo standaard specificatie OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="c46b5-173">hello primary motivation for introducing these changes is toobe compliant with hello OpenID Connect standard specification.</span></span>  <span data-ttu-id="c46b5-174">We hopen toominimize verschillen tussen integreren met Microsoft identity services en met andere services identiteit in de industrie Hallo door OpenID Connect compatibel.</span><span class="sxs-lookup"><span data-stu-id="c46b5-174">By being OpenID Connect compliant, we hope toominimize differences between integrating with Microsoft identity services and with other identity services in hello industry.</span></span>  <span data-ttu-id="c46b5-175">We willen hun favoriete open-source-verificatiebibliotheken tooenable ontwikkelaars toouse zonder tooalter Hallo bibliotheken tooaccommodate Microsoft verschillen.</span><span class="sxs-lookup"><span data-stu-id="c46b5-175">We want tooenable developers toouse their favorite open source authentication libraries without having tooalter hello libraries tooaccommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="c46b5-176">Wat kunt u doen?</span><span class="sxs-lookup"><span data-stu-id="c46b5-176">What can you do?</span></span>
<span data-ttu-id="c46b5-177">Vanaf vandaag, kunt u beginnen met het maken van alle Hallo wijzigingen die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="c46b5-177">As of today, you can begin making all of hello changes described above.</span></span>  <span data-ttu-id="c46b5-178">U moet onmiddellijk het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c46b5-178">You should immediately:</span></span>

1. <span data-ttu-id="c46b5-179">**Verwijder de afhankelijkheden van Hallo `x5t` headerparameter.**</span><span class="sxs-lookup"><span data-stu-id="c46b5-179">**Remove any dependencies on hello `x5t` header parameter.**</span></span>
2. <span data-ttu-id="c46b5-180">**Hallo overgang van de juiste manier verwerken `profile_info` te`id_token` in antwoorden van een token.**</span><span class="sxs-lookup"><span data-stu-id="c46b5-180">**Gracefully handle hello transition from `profile_info` too`id_token` in token responses.**</span></span>
3. <span data-ttu-id="c46b5-181">**Verwijder de afhankelijkheden van Hallo `id_token_expires_in` antwoord-parameter.**</span><span class="sxs-lookup"><span data-stu-id="c46b5-181">**Remove any dependencies on hello `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="c46b5-182">**Hallo toevoegen `profile` en `email` scopes tooyour app als uw app basisgebruiker informatie nodig heeft.**</span><span class="sxs-lookup"><span data-stu-id="c46b5-182">**Add hello `profile` and `email` scopes tooyour app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="c46b5-183">**Waarden van de verlener in tokens zowel met als zonder een afsluitende slash accepteren.**</span><span class="sxs-lookup"><span data-stu-id="c46b5-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="c46b5-184">Onze [protocoldocumentatie v2.0](active-directory-v2-protocols.md) is al bijgewerkt tooreflect deze wijzigingen, zodat u deze als referentie gebruiken kunt bij het bijwerken van uw code.</span><span class="sxs-lookup"><span data-stu-id="c46b5-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated tooreflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="c46b5-185">Als u meer vragen op Hallo bereik van Hallo wijzigingen hebt, kunt u gratis tooreach out toous op Twitter op @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="c46b5-185">If you have any further questions on hello scope of hello changes, please feel free tooreach out toous on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="c46b5-186">Hoe vaak wijzigingen protocol plaatsvindt?</span><span class="sxs-lookup"><span data-stu-id="c46b5-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="c46b5-187">We voorziet niet alle verder op te splitsen verificatieprotocollen toohello wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c46b5-187">We do not foresee any further breaking changes toohello authentication protocols.</span></span>  <span data-ttu-id="c46b5-188">We bundelt deze wijzigingen in een versie die u geen toogo via dit soort updateproces snel opnieuw elk gewenst moment hebt opzettelijk.</span><span class="sxs-lookup"><span data-stu-id="c46b5-188">We are intentionally bundling these changes into one release so that you won\`t have toogo through this type of update process again any time soon.</span></span>  <span data-ttu-id="c46b5-189">Natuurlijk, zullen wij tooadd functies toohello geconvergeerde v2.0 authentication-service die u van profiteren kunt, maar deze wijzigingen moet additief zijn en niet-bestaande code einde.</span><span class="sxs-lookup"><span data-stu-id="c46b5-189">Of course, we will continue tooadd features toohello converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="c46b5-190">Willen we graag ten slotte toosay Hartelijk dank voor dingen tijdens de evaluatieperiode Hallo uitprobeert.</span><span class="sxs-lookup"><span data-stu-id="c46b5-190">Lastly, we would like toosay thank you for trying things out during hello preview period.</span></span>  <span data-ttu-id="c46b5-191">Hallo insights en ervaringen van onze vroege gebruikers zijn waardevol zijn tot nu toe, en we hopen dat u hebt tooshare uw mening en ideeën.</span><span class="sxs-lookup"><span data-stu-id="c46b5-191">hello insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue tooshare your opinions and ideas.</span></span>

<span data-ttu-id="c46b5-192">Gelukkig coderen!</span><span class="sxs-lookup"><span data-stu-id="c46b5-192">Happy coding!</span></span>

<span data-ttu-id="c46b5-193">Hallo Microsoft Identity deling</span><span class="sxs-lookup"><span data-stu-id="c46b5-193">hello Microsoft Identity Division</span></span>

