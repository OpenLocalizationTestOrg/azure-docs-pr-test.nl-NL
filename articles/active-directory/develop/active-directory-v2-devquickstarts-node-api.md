---
title: een web-API van Azure Active Directory v2.0 aaaSecure met behulp van Node.js | Microsoft Docs
description: Meer informatie over hoe toobuild een Node.js web-API die tokens van een persoonlijk Microsoft-account en van werk-of schoolaccounts accepteert.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="75c7b-103">Een web-API beveiligen met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="75c7b-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="75c7b-104">Niet alle Azure Active Directory-scenario's en onderdelen werken met Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="75c7b-105">toodetermine of moet u Hallo v2.0-eindpunt of Hallo v1.0 eindpunt, gelezen over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="75c7b-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="75c7b-106">Wanneer u v2.0-eindpunt voor hello Azure Active Directory (Azure AD) gebruikt, kunt u [OAuth 2.0](active-directory-v2-protocols.md) toegang tokens tooprotect uw web-API.</span><span class="sxs-lookup"><span data-stu-id="75c7b-106">When you use hello Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens tooprotect your web API.</span></span> <span data-ttu-id="75c7b-107">Met OAuth 2.0 toegang tokens, gebruikers die beschikken over een persoonlijk Microsoft-account en werk of schoolaccounts kunnen veilig toegang krijgen tot uw web-API.</span><span class="sxs-lookup"><span data-stu-id="75c7b-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="75c7b-108">*Passport* is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="75c7b-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="75c7b-109">Flexibel en modulair, Passport kan onopvallend worden verwijderd in een snelle gebaseerde of restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="75c7b-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="75c7b-110">In Passport, een uitgebreide set strategieën ondersteuning voor verificatie met behulp van een gebruikersnaam en wachtwoord, Facebook, Twitter of andere opties.</span><span class="sxs-lookup"><span data-stu-id="75c7b-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="75c7b-111">We hebben een strategie ontwikkeld voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75c7b-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="75c7b-112">In dit artikel we u zien hoe tooinstall Hallo module en voeg vervolgens hello Azure AD `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="75c7b-112">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="75c7b-113">Downloaden</span><span class="sxs-lookup"><span data-stu-id="75c7b-113">Download</span></span>
<span data-ttu-id="75c7b-114">Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="75c7b-114">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="75c7b-115">toofollow hello zelfstudie, kunt u [basis van Hallo app downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), of kloon Hallo basisproject:</span><span class="sxs-lookup"><span data-stu-id="75c7b-115">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="75c7b-116">U kunt ook de toepassing hello voltooid op Hallo einde van deze zelfstudie ophalen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-116">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="75c7b-117">1: een app registreren</span><span class="sxs-lookup"><span data-stu-id="75c7b-117">1: Register an app</span></span>
<span data-ttu-id="75c7b-118">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of voert u [deze gedetailleerde stappen](active-directory-v2-app-registration.md) tooregister een app.</span><span class="sxs-lookup"><span data-stu-id="75c7b-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="75c7b-119">Zorg ervoor dat u:</span><span class="sxs-lookup"><span data-stu-id="75c7b-119">Make sure you:</span></span>

* <span data-ttu-id="75c7b-120">Kopiëren Hallo **toepassings-Id** tooyour app toegewezen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-120">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="75c7b-121">U hebt deze nodig voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="75c7b-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="75c7b-122">Hallo toevoegen **Mobile** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="75c7b-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="75c7b-123">Kopiëren Hallo **omleidings-URI** van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="75c7b-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="75c7b-124">Moet u Hallo standaardwaarde URI van `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="75c7b-124">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="75c7b-125">2: Installeer Node.js</span><span class="sxs-lookup"><span data-stu-id="75c7b-125">2: Install Node.js</span></span>
<span data-ttu-id="75c7b-126">Voorbeeld van toouse Hallo voor deze zelfstudie, moet u [Installeer Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="75c7b-126">toouse hello sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="75c7b-127">3: Installeer MongoDB</span><span class="sxs-lookup"><span data-stu-id="75c7b-127">3: Install MongoDB</span></span>
<span data-ttu-id="75c7b-128">toosuccessfully dit voorbeeld gebruiken, moet u [MongoDB installeren](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="75c7b-128">toosuccessfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="75c7b-129">In dit voorbeeld gebruikt u MongoDB toomake uw REST-API persistent in alle serverexemplaren.</span><span class="sxs-lookup"><span data-stu-id="75c7b-129">In this sample, you use MongoDB toomake your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="75c7b-130">In dit artikel gaan we ervan uit dat u Hallo standaard en -servereindpunten voor MongoDB: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="75c7b-130">In this article, we assume that you use hello default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="75c7b-131">4: installatie Hallo restify-modules in uw web-API</span><span class="sxs-lookup"><span data-stu-id="75c7b-131">4: Install hello restify modules in your web API</span></span>
<span data-ttu-id="75c7b-132">We gebruiken onze REST API Resitfy toobuild.</span><span class="sxs-lookup"><span data-stu-id="75c7b-132">We use Resitfy toobuild our REST API.</span></span> <span data-ttu-id="75c7b-133">Restify is een minimaal en flexibel Node.js-toepassingsframework dat afgeleid van Express.</span><span class="sxs-lookup"><span data-stu-id="75c7b-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="75c7b-134">Restify is een set krachtige functies waarmee u toobuild REST-API's op Connect kunt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-134">Restify has a robust set of features that you can use toobuild REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="75c7b-135">Restify installeren</span><span class="sxs-lookup"><span data-stu-id="75c7b-135">Install restify</span></span>
1.  <span data-ttu-id="75c7b-136">Wijzig bij een opdrachtprompt Hallo directory te**azuread**:</span><span class="sxs-lookup"><span data-stu-id="75c7b-136">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="75c7b-137">Als hello **azuread** directory niet bestaat, deze maken:</span><span class="sxs-lookup"><span data-stu-id="75c7b-137">If hello **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="75c7b-138">Restify installeren:</span><span class="sxs-lookup"><span data-stu-id="75c7b-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="75c7b-139">Hallo-uitvoer van deze opdracht moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="75c7b-139">hello output of this command should look like this:</span></span>

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a><span data-ttu-id="75c7b-140">Krijgt u een foutmelding?</span><span class="sxs-lookup"><span data-stu-id="75c7b-140">Did you get an error?</span></span>
<span data-ttu-id="75c7b-141">In sommige besturingssystemen wanneer u Hallo `npm` uitvoert, en u dit bericht ziet: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="75c7b-141">On some operating systems, when you use hello `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="75c7b-142">Hallo-fout wordt gevolgd door een aanvraag voor dat u actieve Hallo-account als beheerder probeert.</span><span class="sxs-lookup"><span data-stu-id="75c7b-142">hello error is followed by a request that you try running hello account as an administrator.</span></span> <span data-ttu-id="75c7b-143">Als dit het geval is, gebruikt u Hallo opdracht `sudo` toorun `npm` op een hoger niveau van bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="75c7b-143">If this occurs, use hello command `sudo` toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-toodtrace"></a><span data-ttu-id="75c7b-144">Krijgt u een fout opgetreden tooDTrace?</span><span class="sxs-lookup"><span data-stu-id="75c7b-144">Did you get an error related tooDTrace?</span></span>
<span data-ttu-id="75c7b-145">Wanneer u installeert restify, ziet u dit bericht:</span><span class="sxs-lookup"><span data-stu-id="75c7b-145">When you install restify, you might see this message:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="75c7b-146">Restify is een krachtig mechanisme tootrace REST aanroept met behulp van DTrace.</span><span class="sxs-lookup"><span data-stu-id="75c7b-146">Restify has a powerful mechanism tootrace REST calls by using DTrace.</span></span> <span data-ttu-id="75c7b-147">DTrace is echter niet beschikbaar is op veel besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="75c7b-148">U kunt dit foutbericht negeren.</span><span class="sxs-lookup"><span data-stu-id="75c7b-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="75c7b-149">5: installatie Passport.js in uw web-API</span><span class="sxs-lookup"><span data-stu-id="75c7b-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="75c7b-150">Wijzig bij de opdrachtprompt Hallo Hallo directory te**azuread**.</span><span class="sxs-lookup"><span data-stu-id="75c7b-150">At hello command prompt, change hello directory too**azuread**.</span></span>

2.  <span data-ttu-id="75c7b-151">Passport.js installeren:</span><span class="sxs-lookup"><span data-stu-id="75c7b-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="75c7b-152">Hallo-uitvoer van Hallo opdracht er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="75c7b-152">hello output of hello command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="75c7b-153">6: passport-azure-ad tooyour web API toevoegen</span><span class="sxs-lookup"><span data-stu-id="75c7b-153">6: Add passport-azure-ad tooyour web API</span></span>
<span data-ttu-id="75c7b-154">Vervolgens met passport-azuread toevoegen Hallo-OAuth-strategie.</span><span class="sxs-lookup"><span data-stu-id="75c7b-154">Next, add hello OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="75c7b-155">`passport-azuread`is een reeks strategieën die Azure AD met Passport verbinden.</span><span class="sxs-lookup"><span data-stu-id="75c7b-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="75c7b-156">We gebruiken deze strategie voor bearer-tokens in dit voorbeeld REST-API.</span><span class="sxs-lookup"><span data-stu-id="75c7b-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="75c7b-157">Hoewel OAuth 2.0 een kader waarin elk onbekend type token kan worden uitgegeven biedt, worden bepaalde typen worden vaak gebruikt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="75c7b-158">Bearer-tokens zijn vaak gebruikte tooprotect eindpunten.</span><span class="sxs-lookup"><span data-stu-id="75c7b-158">Bearer tokens are commonly used tooprotect endpoints.</span></span> <span data-ttu-id="75c7b-159">Bearer-tokens zijn Hallo meest wordt uitgegeven type token in OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="75c7b-159">Bearer tokens are hello most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="75c7b-160">Veel OAuth 2.0-implementaties wordt ervan uitgegaan dat bearer-tokens Hallo enige type token dat is uitgegeven zijn.</span><span class="sxs-lookup"><span data-stu-id="75c7b-160">Many OAuth 2.0 implementations assume that bearer tokens are hello only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="75c7b-161">Wijzig bij een opdrachtprompt Hallo directory te**azuread**.</span><span class="sxs-lookup"><span data-stu-id="75c7b-161">At a command prompt, change hello directory too**azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="75c7b-162">Hallo Passport.js installeren `passport-azure-ad` module:</span><span class="sxs-lookup"><span data-stu-id="75c7b-162">Install hello Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="75c7b-163">Hallo-uitvoer van Hallo opdracht er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="75c7b-163">hello output of hello command should look like this:</span></span>

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="75c7b-164">7: MongoDB-modules tooyour web API toevoegen</span><span class="sxs-lookup"><span data-stu-id="75c7b-164">7: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="75c7b-165">In dit voorbeeld gebruiken we MongoDB als onze gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="75c7b-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="75c7b-166">Installeren van Mongoose, een veelgebruikte invoegtoepassing toomanage modellen en schema's:</span><span class="sxs-lookup"><span data-stu-id="75c7b-166">Install Mongoose, a widely used plug-in, toomanage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="75c7b-167">Hallo databasestuurprogramma voor MongoDB, ook wel MongoDB genoemd installeren:</span><span class="sxs-lookup"><span data-stu-id="75c7b-167">Install hello database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="75c7b-168">8: aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="75c7b-168">8: Install additional modules</span></span>
<span data-ttu-id="75c7b-169">Hallo resterende vereiste modules installeren.</span><span class="sxs-lookup"><span data-stu-id="75c7b-169">Install hello remaining required modules.</span></span>

1.  <span data-ttu-id="75c7b-170">Wijzig bij een opdrachtprompt Hallo directory te**azuread**:</span><span class="sxs-lookup"><span data-stu-id="75c7b-170">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="75c7b-171">Voer Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-171">Enter hello following commands.</span></span> <span data-ttu-id="75c7b-172">Hallo opdrachten installeren Hallo modules in de map node_modules te volgen:</span><span class="sxs-lookup"><span data-stu-id="75c7b-172">hello commands install hello following modules in your node_modules directory:</span></span>

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="75c7b-173">9: een bestand Server.js voor afhankelijkheden maken</span><span class="sxs-lookup"><span data-stu-id="75c7b-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="75c7b-174">Een bestand Server.js bevat Hallo meerderheid van Hallo-functionaliteit voor uw web-API-server.</span><span class="sxs-lookup"><span data-stu-id="75c7b-174">A Server.js file holds hello majority of hello functionality for your web API server.</span></span> <span data-ttu-id="75c7b-175">De meeste van uw code toothis bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-175">Add most of your code toothis file.</span></span> <span data-ttu-id="75c7b-176">Voor productiedoeleinden, kunt u Hallo-functionaliteit in kleinere bestanden opsplitsen zoals voor afzonderlijke routes en controllers.</span><span class="sxs-lookup"><span data-stu-id="75c7b-176">For production purposes, you can refactor hello functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="75c7b-177">In dit artikel gebruiken we Server.js voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="75c7b-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="75c7b-178">Wijzig bij een opdrachtprompt Hallo directory te**azuread**:</span><span class="sxs-lookup"><span data-stu-id="75c7b-178">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="75c7b-179">Met een editor naar keuze, maak een Server.js-bestand.</span><span class="sxs-lookup"><span data-stu-id="75c7b-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="75c7b-180">Hallo toohello informatiebestand volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="75c7b-180">Add hello following information toohello file:</span></span>

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  <span data-ttu-id="75c7b-181">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="75c7b-181">Save hello file.</span></span> <span data-ttu-id="75c7b-182">U wordt spoedig tooit geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="75c7b-182">You will return tooit shortly.</span></span>

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="75c7b-183">10: uw Azure AD-instellingen voor een toostore config-bestand maken</span><span class="sxs-lookup"><span data-stu-id="75c7b-183">10: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="75c7b-184">Dit codebestand geeft de configuratieparameters Hallo van uw Azure AD portal tooPassport.js.</span><span class="sxs-lookup"><span data-stu-id="75c7b-184">This code file passes hello configuration parameters from your Azure AD portal tooPassport.js.</span></span> <span data-ttu-id="75c7b-185">U hebt deze configuratiewaarden gemaakt toen u API Hallo-toohello webportal aan Hallo begin van Hallo artikel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="75c7b-185">You created these configuration values when you added hello web API toohello portal at hello beginning of hello article.</span></span> <span data-ttu-id="75c7b-186">Na het kopiëren van Hallo code wordt uitgelegd welke tooput Hallo waarden van deze parameters.</span><span class="sxs-lookup"><span data-stu-id="75c7b-186">After you copy hello code, we'll explain what tooput in hello values of these parameters.</span></span>

1.  <span data-ttu-id="75c7b-187">Wijzig bij een opdrachtprompt Hallo directory te**azuread**:</span><span class="sxs-lookup"><span data-stu-id="75c7b-187">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="75c7b-188">Maak een bestand Config.js in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="75c7b-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="75c7b-189">Voeg Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="75c7b-189">Add hello following information:</span></span>

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="75c7b-190">Vereiste waarden</span><span class="sxs-lookup"><span data-stu-id="75c7b-190">Required values</span></span>

*   <span data-ttu-id="75c7b-191">**IdentityMetadata**: dit is wanneer `passport-azure-ad` zoekt de configuratiegegevens voor het Hallo-identiteitsprovider (IDP) en Hallo sleutels toovalidate Hallo JSON Web Tokens (JWTs).</span><span class="sxs-lookup"><span data-stu-id="75c7b-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for hello identity provider (IDP) and hello keys toovalidate hello JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="75c7b-192">Als u Azure AD gebruikt, wilt u waarschijnlijk niet toochange dit.</span><span class="sxs-lookup"><span data-stu-id="75c7b-192">If you are using Azure AD, you probably don't want toochange this.</span></span>

*   <span data-ttu-id="75c7b-193">**doelgroep**: uw omleidings-URI van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="75c7b-193">**audience**: Your redirect URI from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="75c7b-194">Uw sleutels rouleert met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="75c7b-195">Zorg ervoor dat u altijd pull van Hallo 'openid_keys' URL en die Hallo app toegang heeft tot Internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="75c7b-195">Be sure that you always pull from hello "openid_keys" URL, and that hello app can access hello Internet.</span></span>
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a><span data-ttu-id="75c7b-196">11: tooyour Hallo-Server.js configuratiebestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="75c7b-196">11: Add hello configuration tooyour Server.js file</span></span>
<span data-ttu-id="75c7b-197">Uw toepassing moet tooread Hallo waarden uit Hallo-configuratiebestand die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-197">Your application needs tooread hello values from hello config file you just created.</span></span> <span data-ttu-id="75c7b-198">Hallo .config-bestand als een vereiste bron in uw toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-198">Add hello .config file as a required resource in your application.</span></span> <span data-ttu-id="75c7b-199">Hallo globale variabelen toothose in Config.js ingesteld.</span><span class="sxs-lookup"><span data-stu-id="75c7b-199">Set hello global variables toothose that are in Config.js.</span></span>

1.  <span data-ttu-id="75c7b-200">Wijzig bij de opdrachtprompt Hallo Hallo directory te**azuread**:</span><span class="sxs-lookup"><span data-stu-id="75c7b-200">At hello command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="75c7b-201">Open Server.js in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="75c7b-201">In an editor, open Server.js.</span></span> <span data-ttu-id="75c7b-202">Voeg Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="75c7b-202">Add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="75c7b-203">Een nieuwe sectie tooServer.js toevoegen:</span><span class="sxs-lookup"><span data-stu-id="75c7b-203">Add a new section tooServer.js:</span></span>

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="75c7b-204">12: Hallo MongoDB-model en schema-informatie toevoegen met behulp van Mongoose</span><span class="sxs-lookup"><span data-stu-id="75c7b-204">12: Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="75c7b-205">Sluit deze drie bestanden in een REST-API-service.</span><span class="sxs-lookup"><span data-stu-id="75c7b-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="75c7b-206">In dit artikel gebruiken we MongoDB toostore onze taken.</span><span class="sxs-lookup"><span data-stu-id="75c7b-206">In this article, we use MongoDB toostore our tasks.</span></span> <span data-ttu-id="75c7b-207">Bespreken we dit op *stap 4*.</span><span class="sxs-lookup"><span data-stu-id="75c7b-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="75c7b-208">In Hallo Config.js bestand dat u hebt gemaakt in stap 11, uw database heet *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="75c7b-208">In hello Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="75c7b-209">Dat was u plaatsen aan Hallo einde van uw mongoose_auth_local verbindings-URL.</span><span class="sxs-lookup"><span data-stu-id="75c7b-209">That was what you put at hello end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="75c7b-210">U hoeft niet toocreate deze vooraf in MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="75c7b-210">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="75c7b-211">Hallo-database wordt gemaakt op Hallo eerst het uitvoeren van de servertoepassing (ervan uitgaande dat Hallo database nog niet bestaat).</span><span class="sxs-lookup"><span data-stu-id="75c7b-211">hello database is created on hello first run of your server application (assuming hello database does not already exist).</span></span>

<span data-ttu-id="75c7b-212">U hebt Hallo-server opgegeven welke toouse MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="75c7b-212">You've told hello server what MongoDB database toouse.</span></span> <span data-ttu-id="75c7b-213">Vervolgens moet u toowrite enkele aanvullende code toocreate Hallo model en het schema voor de taken van uw server.</span><span class="sxs-lookup"><span data-stu-id="75c7b-213">Next, you need toowrite some additional code toocreate hello model and schema for your server's tasks.</span></span>

### <a name="hello-model"></a><span data-ttu-id="75c7b-214">Hallo-model</span><span class="sxs-lookup"><span data-stu-id="75c7b-214">hello model</span></span>
<span data-ttu-id="75c7b-215">Hallo-schemamodel is zeer eenvoudige.</span><span class="sxs-lookup"><span data-stu-id="75c7b-215">hello schema model is very basic.</span></span> <span data-ttu-id="75c7b-216">U kunt deze als u wilt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="75c7b-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="75c7b-217">Hallo-schemamodel heeft de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="75c7b-217">hello schema model has these values:</span></span>

*   <span data-ttu-id="75c7b-218">**NAAM**.</span><span class="sxs-lookup"><span data-stu-id="75c7b-218">**NAME**.</span></span> <span data-ttu-id="75c7b-219">Hallo persoon toegewezen toohello taak.</span><span class="sxs-lookup"><span data-stu-id="75c7b-219">hello person assigned toohello task.</span></span> <span data-ttu-id="75c7b-220">Dit is een **tekenreeks** waarde.</span><span class="sxs-lookup"><span data-stu-id="75c7b-220">This is a **string** value.</span></span>
*   <span data-ttu-id="75c7b-221">**TAAK**.</span><span class="sxs-lookup"><span data-stu-id="75c7b-221">**TASK**.</span></span> <span data-ttu-id="75c7b-222">Hallo-naam van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="75c7b-222">hello name of hello task.</span></span> <span data-ttu-id="75c7b-223">Dit is een **tekenreeks** waarde.</span><span class="sxs-lookup"><span data-stu-id="75c7b-223">This is a **string** value.</span></span>
*   <span data-ttu-id="75c7b-224">**DATUM**.</span><span class="sxs-lookup"><span data-stu-id="75c7b-224">**DATE**.</span></span> <span data-ttu-id="75c7b-225">Hallo datum die taak Hallo vervalt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-225">hello date that hello task is due.</span></span> <span data-ttu-id="75c7b-226">Dit is een **datetime** waarde.</span><span class="sxs-lookup"><span data-stu-id="75c7b-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="75c7b-227">**VOLTOOID**.</span><span class="sxs-lookup"><span data-stu-id="75c7b-227">**COMPLETED**.</span></span> <span data-ttu-id="75c7b-228">Hiermee wordt aangegeven of Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="75c7b-228">Whether hello task is completed.</span></span> <span data-ttu-id="75c7b-229">Dit is een **Booleaanse** waarde.</span><span class="sxs-lookup"><span data-stu-id="75c7b-229">This is a **Boolean** value.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="75c7b-230">Hallo-schema in Hallo code maken</span><span class="sxs-lookup"><span data-stu-id="75c7b-230">Create hello schema in hello code</span></span>
1.  <span data-ttu-id="75c7b-231">Wijzig bij een opdrachtprompt Hallo directory te**azuread**:</span><span class="sxs-lookup"><span data-stu-id="75c7b-231">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="75c7b-232">Open in uw editor Server.js.</span><span class="sxs-lookup"><span data-stu-id="75c7b-232">In your editor, open Server.js.</span></span> <span data-ttu-id="75c7b-233">Hieronder Hallo-configuratie-item toevoegen Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="75c7b-233">Below hello configuration entry, add hello following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="75c7b-234">Deze code maakt verbinding toohello MongoDB-server.</span><span class="sxs-lookup"><span data-stu-id="75c7b-234">This code connects toohello MongoDB server.</span></span> <span data-ttu-id="75c7b-235">Ook wordt een schemaobject.</span><span class="sxs-lookup"><span data-stu-id="75c7b-235">It also returns a schema object.</span></span>

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a><span data-ttu-id="75c7b-236">Het model in Hallo-code Hallo schema gebruikt, maken</span><span class="sxs-lookup"><span data-stu-id="75c7b-236">Using hello schema, create your model in hello code</span></span>
<span data-ttu-id="75c7b-237">Toevoegen onder Hallo voorafgaand aan code, Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="75c7b-237">Below hello preceding code, add hello following code:</span></span>

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="75c7b-238">Zoals u vanuit Hallo code ziet, maakt u eerst uw schema.</span><span class="sxs-lookup"><span data-stu-id="75c7b-238">As you can tell from hello code, first you create your schema.</span></span> <span data-ttu-id="75c7b-239">Vervolgens maakt u een modelobject.</span><span class="sxs-lookup"><span data-stu-id="75c7b-239">Next, you create a model object.</span></span> <span data-ttu-id="75c7b-240">Gebruik van Hallo model object toostore uw gegevens in de gehele Hallo code bij het definiëren van uw **routes**.</span><span class="sxs-lookup"><span data-stu-id="75c7b-240">You use hello model object toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="75c7b-241">13: uw routes toevoegen voor de REST-API-taakserver</span><span class="sxs-lookup"><span data-stu-id="75c7b-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="75c7b-242">Nu u een database model toowork met hebt, toevoegen Hallo routes die u voor de REST-API-server gebruikt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-242">Now that you have a database model toowork with, add hello routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="75c7b-243">Routes in restify</span><span class="sxs-lookup"><span data-stu-id="75c7b-243">About routes in restify</span></span>
<span data-ttu-id="75c7b-244">Routes in restify werk exact hello dezelfde manier als ze doen wanneer u Hallo Express-stack.</span><span class="sxs-lookup"><span data-stu-id="75c7b-244">Routes in restify work exactly hello same way they do when you use hello Express stack.</span></span> <span data-ttu-id="75c7b-245">U definieert routes met behulp van Hallo URI dat u Hallo client toepassingen toocall verwacht.</span><span class="sxs-lookup"><span data-stu-id="75c7b-245">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="75c7b-246">Meestal kunt definiëren u uw routes in een afzonderlijk bestand.</span><span class="sxs-lookup"><span data-stu-id="75c7b-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="75c7b-247">In deze zelfstudie we onze routes in Server.js geplaatst.</span><span class="sxs-lookup"><span data-stu-id="75c7b-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="75c7b-248">Voor gebruik in productieomgevingen, is het raadzaam dat u rekening te houden routes in een eigen bestand.</span><span class="sxs-lookup"><span data-stu-id="75c7b-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="75c7b-249">Een doorsnee patroon voor een restify-route is:</span><span class="sxs-lookup"><span data-stu-id="75c7b-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="75c7b-250">Dit is Hallo patroon op Hallo meest eenvoudige niveau.</span><span class="sxs-lookup"><span data-stu-id="75c7b-250">This is hello pattern at hello most basic level.</span></span> <span data-ttu-id="75c7b-251">Restify (en Express) bieden veel diepere functionaliteit, zoals Hallo mogelijkheid toodefine toepassingstypen en complexe routering tussen verschillende eindpunten.</span><span class="sxs-lookup"><span data-stu-id="75c7b-251">Restify (and Express) provide much deeper functionality, like hello ability toodefine application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="75c7b-252">Standaard routes tooyour server toevoegen</span><span class="sxs-lookup"><span data-stu-id="75c7b-252">Add default routes tooyour server</span></span>
<span data-ttu-id="75c7b-253">Hallo eenvoudige CRUD-routes toevoegen: **maken**, **ophalen**, **bijwerken**, en **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="75c7b-253">Add hello basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="75c7b-254">Wijzig bij een opdrachtprompt Hallo directory te**azuread**:</span><span class="sxs-lookup"><span data-stu-id="75c7b-254">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="75c7b-255">Open Server.js in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="75c7b-255">In an editor, open Server.js.</span></span> <span data-ttu-id="75c7b-256">Hieronder Hallo databasevermeldingen die u eerder hebt gemaakt, het toevoegen van Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="75c7b-256">Below hello database entries you made earlier, add hello following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable toosave');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable toodelete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="75c7b-257">Foutafhandeling voor Hallo routes toevoegen</span><span class="sxs-lookup"><span data-stu-id="75c7b-257">Add error handling for hello routes</span></span>
<span data-ttu-id="75c7b-258">Foutafhandeling toevoegen zodat u de client terug toohello over opgetreden Hallo probleem kan communiceren.</span><span class="sxs-lookup"><span data-stu-id="75c7b-258">Add some error handling so you can communicate back toohello client about hello problem you encountered.</span></span>

<span data-ttu-id="75c7b-259">Na de code hieronder Hallo code, die u al hebt geschreven Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="75c7b-259">Add hello following code below hello code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back toohello client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a><span data-ttu-id="75c7b-260">14: de server maken</span><span class="sxs-lookup"><span data-stu-id="75c7b-260">14: Create your server</span></span>
<span data-ttu-id="75c7b-261">laatste ding toodo Hallo tooadd uw server-exemplaar is.</span><span class="sxs-lookup"><span data-stu-id="75c7b-261">hello last thing toodo is tooadd your server instance.</span></span> <span data-ttu-id="75c7b-262">Hallo-serverexemplaar beheert uw aanroepen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-262">hello server instance manages your calls.</span></span>

<span data-ttu-id="75c7b-263">Restify (en Express) mate aanpassen die u met een REST-API-server gebruiken kunt hebben.</span><span class="sxs-lookup"><span data-stu-id="75c7b-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="75c7b-264">In deze zelfstudie gebruiken we de meest eenvoudige configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="75c7b-264">In this tutorial, we use hello most basic setup.</span></span>

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a><span data-ttu-id="75c7b-265">15: Hallo routes (zonder verificatie nu) toevoegen</span><span class="sxs-lookup"><span data-stu-id="75c7b-265">15: Add hello routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a><span data-ttu-id="75c7b-266">16: Hallo-server wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="75c7b-266">16: Run hello server</span></span>
<span data-ttu-id="75c7b-267">Het is een goed idee tootest uw server voordat u verificatie toevoegt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-267">It's a good idea tootest your server before you add authentication.</span></span>

<span data-ttu-id="75c7b-268">de eenvoudigste manier tootest Hallo uw server is met behulp van curl bij een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-268">hello easiest way tootest your server is by using curl at a command prompt.</span></span> <span data-ttu-id="75c7b-269">toodo, moet u een eenvoudig hulpprogramma dat u tooparse uitvoer als JSON gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-269">toodo this, you need a simple utility that you can use tooparse output as JSON.</span></span> 

1.  <span data-ttu-id="75c7b-270">Hallo JSON-hulpprogramma dat we gebruiken op Hallo volgen voorbeelden installeren:</span><span class="sxs-lookup"><span data-stu-id="75c7b-270">Install hello JSON tool that we use in hello following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="75c7b-271">Hiermee installeert globaal Hallo JSON-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="75c7b-271">This installs hello JSON tool globally.</span></span>

2.  <span data-ttu-id="75c7b-272">Controleer of het MongoDB-exemplaar is geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="75c7b-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="75c7b-273">Hallo directory ook wijzigen**azuread**, en voer vervolgens curl:</span><span class="sxs-lookup"><span data-stu-id="75c7b-273">Change hello directory too**azuread**, and then run curl:</span></span>

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  <span data-ttu-id="75c7b-274">een taak tooadd:</span><span class="sxs-lookup"><span data-stu-id="75c7b-274">tooadd a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="75c7b-275">Hallo-antwoord moet zijn:</span><span class="sxs-lookup"><span data-stu-id="75c7b-275">hello response should be:</span></span>

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  <span data-ttu-id="75c7b-276">Lijst met taken voor Brandon:</span><span class="sxs-lookup"><span data-stu-id="75c7b-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="75c7b-277">Als alle deze opdrachten worden uitgevoerd zonder fouten, bent u klaar tooadd OAuth toohello REST-API-server.</span><span class="sxs-lookup"><span data-stu-id="75c7b-277">If all these commands run without errors, you are ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="75c7b-278">*U hebt nu een REST-API-server met MongoDB.*</span><span class="sxs-lookup"><span data-stu-id="75c7b-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="75c7b-279">17: authentication tooyour REST-API-server toevoegen</span><span class="sxs-lookup"><span data-stu-id="75c7b-279">17: Add authentication tooyour REST API server</span></span>
<span data-ttu-id="75c7b-280">Nu dat u een actieve REST-API hebt, moet u deze instellen in toouse met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75c7b-280">Now that you have a running REST API, set it up toouse it with Azure AD.</span></span>

<span data-ttu-id="75c7b-281">Wijzig bij een opdrachtprompt Hallo directory te**azuread**:</span><span class="sxs-lookup"><span data-stu-id="75c7b-281">At a command prompt, change hello directory too**azuread**:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="75c7b-282">Gebruik Hallo oidcbearerstrategy die is opgenomen in passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="75c7b-282">Use hello oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="75c7b-283">U kunt een typische REST-TODO-server zonder enige vorm van autorisatie tot nu toe hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="75c7b-284">Voeg nu verificatie.</span><span class="sxs-lookup"><span data-stu-id="75c7b-284">Now, add authentication.</span></span>

<span data-ttu-id="75c7b-285">Ten eerste kunt u aangeven dat u wilt dat toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="75c7b-285">First,  indicate that you want toouse Passport.</span></span> <span data-ttu-id="75c7b-286">Dit recht na de configuratie van uw eerdere server genomen:</span><span class="sxs-lookup"><span data-stu-id="75c7b-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="75c7b-287">Wanneer u API's schrijft, is het een goed idee tooalways koppeling Hallo gegevens toosomething uniek in vergelijking met het Hallo-token dat Hallo gebruiker niet kan vervalsen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-287">When you write APIs, it's a good idea tooalways link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="75c7b-288">Wanneer deze server TODO-items opslaat, slaat deze op basis van Hallo gebruiker abonnements-ID in het Hallo-token (aangeroepen via token.sub).</span><span class="sxs-lookup"><span data-stu-id="75c7b-288">When this server stores TODO items, it stores them based on hello user subscription ID in hello token (called through token.sub).</span></span> <span data-ttu-id="75c7b-289">U plaatsen Hallo token.sub in Hallo 'eigenaar'-veld.</span><span class="sxs-lookup"><span data-stu-id="75c7b-289">You put hello token.sub in hello “owner” field.</span></span> <span data-ttu-id="75c7b-290">Dit zorgt ervoor dat alleen die gebruiker toegang heeft tot TODOs Hallo van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="75c7b-290">This ensures that only that user can access hello user's TODOs.</span></span> <span data-ttu-id="75c7b-291">Niemand anders toegang tot Hallo TODOs die zijn ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="75c7b-291">No one else can access hello TODOs that were entered.</span></span> <span data-ttu-id="75c7b-292">Er is geen blootstelling in Hallo API voor de 'eigenaar'.</span><span class="sxs-lookup"><span data-stu-id="75c7b-292">There is no exposure in hello API for “owner.”</span></span> <span data-ttu-id="75c7b-293">Een externe gebruiker kan andere gebruikers TODOs, aanvragen, zelfs als ze zijn geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="75c7b-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="75c7b-294">Gebruik vervolgens Hallo Open ID Connect Bearer-strategie die wordt geleverd met `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="75c7b-294">Next, use hello Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="75c7b-295">Plaats deze achter eerder geplakt:</span><span class="sxs-lookup"><span data-stu-id="75c7b-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

<span data-ttu-id="75c7b-296">Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="75c7b-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="75c7b-297">Alle schrijvers van strategieën toohello patroon.</span><span class="sxs-lookup"><span data-stu-id="75c7b-297">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="75c7b-298">Hallo-strategie doorgeven een `function()` die gebruikmaakt van een token en `done` als parameters.</span><span class="sxs-lookup"><span data-stu-id="75c7b-298">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="75c7b-299">Hallo-strategie terug nadat al het werk wordt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-299">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="75c7b-300">Hallo-gebruiker en stash Hallo token opslaan zodat u niet tooask voor het opnieuw hoeft.</span><span class="sxs-lookup"><span data-stu-id="75c7b-300">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75c7b-301">Hallo voorafgaande code geldt voor elke gebruiker die tooyour server kan worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="75c7b-301">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="75c7b-302">Dit wordt automatische registratie genoemd.</span><span class="sxs-lookup"><span data-stu-id="75c7b-302">This is known as auto-registration.</span></span> <span data-ttu-id="75c7b-303">Op een productieserver je wilt niet dat toolet iedereen zonder dat zij een registratieproces die u kiest doorlopen eerst.</span><span class="sxs-lookup"><span data-stu-id="75c7b-303">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="75c7b-304">Dit is meestal Hallo patroon dat u in consumenten-apps ziet.</span><span class="sxs-lookup"><span data-stu-id="75c7b-304">This is usually hello pattern you see in consumer apps.</span></span> <span data-ttu-id="75c7b-305">Hallo-app kunt u mogelijk tooregister met Facebook, maar vervolgens wordt u gevraagd een tooenter aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="75c7b-305">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="75c7b-306">Als u een opdrachtregelprogramma zijn niet voor deze zelfstudie gebruikt, kan u Hallo e extraheren uit Hallo Tokenobject dat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="75c7b-306">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="75c7b-307">Vervolgens vraagt u mogelijk Hallo gebruiker tooenter aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="75c7b-307">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="75c7b-308">Omdat dit een testserver is, u Hallo gebruiker toevoegen rechtstreeks toohello de database in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-308">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="75c7b-309">Eindpunten beveiligen</span><span class="sxs-lookup"><span data-stu-id="75c7b-309">Protect endpoints</span></span>
<span data-ttu-id="75c7b-310">Eindpunten beveiligen door te geven Hallo **passport.authenticate()** aanroep met het Hallo-protocol dat u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="75c7b-310">Protect endpoints by specifying hello **passport.authenticate()** call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="75c7b-311">U kunt uw route in uw servercode voor een meer geavanceerde optie bewerken:</span><span class="sxs-lookup"><span data-stu-id="75c7b-311">You can edit your route in your server code for a more advanced option:</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="75c7b-312">18: de servertoepassing opnieuw uitvoeren</span><span class="sxs-lookup"><span data-stu-id="75c7b-312">18: Run your server application again</span></span>
<span data-ttu-id="75c7b-313">Gebruik curl opnieuw toosee als u OAuth 2.0-beveiliging voor uw eindpunten hebt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-313">Use curl again toosee if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="75c7b-314">Doe dit voordat u een van uw client-SDK's uitvoeren met dit eindpunt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="75c7b-315">Hallo-headers geretourneerd moeten vertellen als de verificatie van uw correct werkt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-315">hello headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="75c7b-316">Zorg ervoor dat uw isntance MongoDB wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="75c7b-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="75c7b-317">Wijzigen van toohello **azuread** directory en gebruik curl:</span><span class="sxs-lookup"><span data-stu-id="75c7b-317">Change toohello **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="75c7b-318">Probeer een basic POST:</span><span class="sxs-lookup"><span data-stu-id="75c7b-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="75c7b-319">Een 401-respons geeft aan dat Hallo Passport-laag probeert tooredirect toohello autoriseren eindpunt, is precies wat u wilt.</span><span class="sxs-lookup"><span data-stu-id="75c7b-319">A 401 response indicates that hello Passport layer is trying tooredirect toohello authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="75c7b-320">*U hebt nu een REST-API-service die gebruikmaakt van OAuth 2.0.*</span><span class="sxs-lookup"><span data-stu-id="75c7b-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="75c7b-321">U bent gegaan zo ver mogelijk kunt u met deze server zonder met behulp van een OAuth 2.0-compatibele client.</span><span class="sxs-lookup"><span data-stu-id="75c7b-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="75c7b-322">Daarvoor moet u een extra zelfstudie tooreview.</span><span class="sxs-lookup"><span data-stu-id="75c7b-322">For that, you will need tooreview an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75c7b-323">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="75c7b-323">Next steps</span></span>
<span data-ttu-id="75c7b-324">Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) wordt geleverd als [een ZIP-bestand](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="75c7b-324">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="75c7b-325">U kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="75c7b-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="75c7b-326">U kunt nu op toomore geavanceerde onderwerpen verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-326">Now, you can move on toomore advanced topics.</span></span> <span data-ttu-id="75c7b-327">U kunt tootry [een Node.js-web-app Hallo v2.0-eindpunt met Secure](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="75c7b-327">You might want tootry [Secure a Node.js web app using hello v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="75c7b-328">Hier volgen enkele aanvullende resources:</span><span class="sxs-lookup"><span data-stu-id="75c7b-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="75c7b-329">Handleiding voor Azure AD v2.0-ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="75c7b-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="75c7b-330">Stack-overloop 'azure active directory' tag</span><span class="sxs-lookup"><span data-stu-id="75c7b-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="75c7b-331">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="75c7b-331">Get security updates for our products</span></span>
<span data-ttu-id="75c7b-332">We raden u toosign up toobe een melding wanneer er beveiligingsincidenten optreden.</span><span class="sxs-lookup"><span data-stu-id="75c7b-332">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="75c7b-333">Op Hallo [Microsoft technische beveiligingsmeldingen](https://technet.microsoft.com/security/dd252948) pagina moet u zich abonneren tooSecurity adviezen waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="75c7b-333">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

