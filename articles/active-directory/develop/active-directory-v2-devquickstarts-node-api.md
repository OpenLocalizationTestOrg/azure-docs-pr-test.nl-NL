---
title: Een Azure Active Directory v2.0-web-API beveiligen met behulp van Node.js | Microsoft Docs
description: Informatie over het bouwen van een Node.js-web-API die tokens van een persoonlijk Microsoft-account en van werk accepteert of school accounts.
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
ms.openlocfilehash: 94e945a52b9df7c495de1611baa08083357670c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="4bdf7-103">Een web-API beveiligen met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="4bdf7-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="4bdf7-104">Niet alle Azure Active Directory-scenario's en onderdelen werken met het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="4bdf7-105">Meer informatie over om te bepalen of u het v2.0-eindpunt of het eindpunt v1.0 moet gebruiken, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="4bdf7-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="4bdf7-106">Wanneer u het v2.0-eindpunt voor Azure Active Directory (Azure AD) gebruikt, kunt u [OAuth 2.0](active-directory-v2-protocols.md) toegang tot tokens, voor het beveiligen van uw web-API.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-106">When you use the Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens to protect your web API.</span></span> <span data-ttu-id="4bdf7-107">Met OAuth 2.0 toegang tokens, gebruikers die beschikken over een persoonlijk Microsoft-account en werk of schoolaccounts kunnen veilig toegang krijgen tot uw web-API.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="4bdf7-108">*Passport* is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="4bdf7-109">Flexibel en modulair, Passport kan onopvallend worden verwijderd in een snelle gebaseerde of restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="4bdf7-110">In Passport, een uitgebreide set strategieën ondersteuning voor verificatie met behulp van een gebruikersnaam en wachtwoord, Facebook, Twitter of andere opties.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="4bdf7-111">We hebben een strategie ontwikkeld voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="4bdf7-112">In dit artikel wordt beschreven hoe u installeert de module en voegt u de Azure AD `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-112">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="4bdf7-113">Downloaden</span><span class="sxs-lookup"><span data-stu-id="4bdf7-113">Download</span></span>
<span data-ttu-id="4bdf7-114">De code voor deze zelfstudie wordt onderhouden in [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="4bdf7-114">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="4bdf7-115">Wilt u de zelfstudie, kunt u [basis van de app downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), of het geraamte:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-115">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="4bdf7-116">U kunt ook de voltooide toepassing aan het einde van deze zelfstudie ophalen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-116">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="4bdf7-117">1: een app registreren</span><span class="sxs-lookup"><span data-stu-id="4bdf7-117">1: Register an app</span></span>
<span data-ttu-id="4bdf7-118">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of voert u [deze gedetailleerde stappen](active-directory-v2-app-registration.md) om een app te registreren.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="4bdf7-119">Zorg ervoor dat u:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-119">Make sure you:</span></span>

* <span data-ttu-id="4bdf7-120">Kopieer de **toepassings-Id** toegewezen aan uw app.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-120">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="4bdf7-121">U hebt deze nodig voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="4bdf7-122">Voeg de **Mobile** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="4bdf7-123">Kopieer de **omleidings-URI** vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="4bdf7-124">Moet u de standaardwaarde van de URI van `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-124">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="4bdf7-125">2: Installeer Node.js</span><span class="sxs-lookup"><span data-stu-id="4bdf7-125">2: Install Node.js</span></span>
<span data-ttu-id="4bdf7-126">Voor het gebruik van het voorbeeld voor deze zelfstudie, moet u [Installeer Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="4bdf7-126">To use the sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="4bdf7-127">3: Installeer MongoDB</span><span class="sxs-lookup"><span data-stu-id="4bdf7-127">3: Install MongoDB</span></span>
<span data-ttu-id="4bdf7-128">Om te kunnen gebruiken in dit voorbeeld, moet u [MongoDB installeren](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="4bdf7-128">To successfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="4bdf7-129">In dit voorbeeld gebruikt u MongoDB om uw REST-API persistent ervoor in alle serverexemplaren.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-129">In this sample, you use MongoDB to make your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="4bdf7-130">In dit artikel gaan we ervan uit dat u de standaard- en -servereindpunten voor MongoDB: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-130">In this article, we assume that you use the default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="4bdf7-131">4: de restify-modules installeren in uw web-API</span><span class="sxs-lookup"><span data-stu-id="4bdf7-131">4: Install the restify modules in your web API</span></span>
<span data-ttu-id="4bdf7-132">We Resitfy gebruiken voor het bouwen van de REST-API.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-132">We use Resitfy to build our REST API.</span></span> <span data-ttu-id="4bdf7-133">Restify is een minimaal en flexibel Node.js-toepassingsframework dat afgeleid van Express.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="4bdf7-134">Restify is een set krachtige functies die u gebruiken kunt voor het bouwen van de REST-API's op Connect.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-134">Restify has a robust set of features that you can use to build REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="4bdf7-135">Restify installeren</span><span class="sxs-lookup"><span data-stu-id="4bdf7-135">Install restify</span></span>
1.  <span data-ttu-id="4bdf7-136">Wijzig bij een opdrachtprompt de map in **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-136">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="4bdf7-137">Als de **azuread** directory niet bestaat, deze maken:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-137">If the **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="4bdf7-138">Restify installeren:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="4bdf7-139">De uitvoer van deze opdracht moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-139">The output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="4bdf7-140">Krijgt u een foutmelding?</span><span class="sxs-lookup"><span data-stu-id="4bdf7-140">Did you get an error?</span></span>
<span data-ttu-id="4bdf7-141">In sommige besturingssystemen wanneer u de `npm` uitvoert, en u dit bericht ziet: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-141">On some operating systems, when you use the `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="4bdf7-142">De fout wordt gevolgd door een aanvraag die u probeert het account uitvoeren als beheerder.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-142">The error is followed by a request that you try running the account as an administrator.</span></span> <span data-ttu-id="4bdf7-143">Als dit het geval is, gebruikt u de opdracht `sudo` om uit te voeren `npm` op een hoger niveau van bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-143">If this occurs, use the command `sudo` to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-to-dtrace"></a><span data-ttu-id="4bdf7-144">Krijgt u een fout met betrekking tot DTrace?</span><span class="sxs-lookup"><span data-stu-id="4bdf7-144">Did you get an error related to DTrace?</span></span>
<span data-ttu-id="4bdf7-145">Wanneer u installeert restify, ziet u dit bericht:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="4bdf7-146">Restify is een krachtig mechanisme te traceren REST aanroept met behulp van DTrace.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-146">Restify has a powerful mechanism to trace REST calls by using DTrace.</span></span> <span data-ttu-id="4bdf7-147">DTrace is echter niet beschikbaar is op veel besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="4bdf7-148">U kunt dit foutbericht negeren.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="4bdf7-149">5: installatie Passport.js in uw web-API</span><span class="sxs-lookup"><span data-stu-id="4bdf7-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="4bdf7-150">Wijzig bij de opdrachtprompt de map in **azuread**.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-150">At the command prompt, change the directory to **azuread**.</span></span>

2.  <span data-ttu-id="4bdf7-151">Passport.js installeren:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="4bdf7-152">De uitvoer van de opdracht er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-152">The output of the command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="4bdf7-153">6: passport-azure-ad toevoegen aan uw web-API</span><span class="sxs-lookup"><span data-stu-id="4bdf7-153">6: Add passport-azure-ad to your web API</span></span>
<span data-ttu-id="4bdf7-154">Voeg vervolgens de OAuth-strategie toe met behulp van de passport-azuread.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-154">Next, add the OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="4bdf7-155">`passport-azuread`is een reeks strategieën die Azure AD met Passport verbinden.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="4bdf7-156">We gebruiken deze strategie voor bearer-tokens in dit voorbeeld REST-API.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="4bdf7-157">Hoewel OAuth 2.0 een kader waarin elk onbekend type token kan worden uitgegeven biedt, worden bepaalde typen worden vaak gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="4bdf7-158">Bearer-tokens worden vaak gebruikt voor het beveiligen van eindpunten.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-158">Bearer tokens are commonly used to protect endpoints.</span></span> <span data-ttu-id="4bdf7-159">Bearer-tokens zijn het meest wordt uitgegeven token in OAuth 2.0-type.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-159">Bearer tokens are the most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="4bdf7-160">Veel OAuth 2.0-implementaties wordt ervan uitgegaan dat bearer-tokens het enige type token dat is uitgegeven zijn.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-160">Many OAuth 2.0 implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="4bdf7-161">Wijzig bij een opdrachtprompt de map in **azuread**.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-161">At a command prompt, change the directory to **azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="4bdf7-162">Installeer de Passport.js `passport-azure-ad` module:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-162">Install the Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="4bdf7-163">De uitvoer van de opdracht er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-163">The output of the command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="4bdf7-164">7: MongoDB-modules toevoegen aan uw web-API</span><span class="sxs-lookup"><span data-stu-id="4bdf7-164">7: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="4bdf7-165">In dit voorbeeld gebruiken we MongoDB als onze gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="4bdf7-166">Installeren van Mongoose, een veelgebruikte invoegtoepassing voor het beheren van modellen en schema's:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-166">Install Mongoose, a widely used plug-in, to manage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="4bdf7-167">Installeer het databasestuurprogramma voor MongoDB, ook wel MongoDB genoemd:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-167">Install the database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="4bdf7-168">8: aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="4bdf7-168">8: Install additional modules</span></span>
<span data-ttu-id="4bdf7-169">Installeer de overige vereiste modules.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-169">Install the remaining required modules.</span></span>

1.  <span data-ttu-id="4bdf7-170">Wijzig bij een opdrachtprompt de map in **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-170">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4bdf7-171">Voer de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-171">Enter the following commands.</span></span> <span data-ttu-id="4bdf7-172">De opdrachten installeren de volgende modules in de map node_modules:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-172">The commands install the following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="4bdf7-173">9: een bestand Server.js voor afhankelijkheden maken</span><span class="sxs-lookup"><span data-stu-id="4bdf7-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="4bdf7-174">Een bestand Server.js bevat het merendeel van de functies voor uw web-API-server.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-174">A Server.js file holds the majority of the functionality for your web API server.</span></span> <span data-ttu-id="4bdf7-175">De meeste van uw code toevoegen aan dit bestand.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-175">Add most of your code to this file.</span></span> <span data-ttu-id="4bdf7-176">Voor productiedoeleinden, kunt u de functionaliteit in kleinere bestanden opsplitsen zoals voor afzonderlijke routes en controllers.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-176">For production purposes, you can refactor the functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="4bdf7-177">In dit artikel gebruiken we Server.js voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="4bdf7-178">Wijzig bij een opdrachtprompt de map in **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-178">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4bdf7-179">Met een editor naar keuze, maak een Server.js-bestand.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="4bdf7-180">De volgende informatie toevoegen aan het bestand:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-180">Add the following information to the file:</span></span>

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

3.  <span data-ttu-id="4bdf7-181">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-181">Save the file.</span></span> <span data-ttu-id="4bdf7-182">U gaat terug naar deze binnenkort.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-182">You will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="4bdf7-183">10: maken van een configuratiebestand voor het opslaan van uw Azure AD-instellingen</span><span class="sxs-lookup"><span data-stu-id="4bdf7-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="4bdf7-184">Dit codebestand geeft de configuratieparameters van uw Azure AD-portal aan Passport.js.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-184">This code file passes the configuration parameters from your Azure AD portal to Passport.js.</span></span> <span data-ttu-id="4bdf7-185">U hebt deze configuratiewaarden gemaakt toen u de web-API toegevoegd aan de portal aan het begin van het artikel.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-185">You created these configuration values when you added the web API to the portal at the beginning of the article.</span></span> <span data-ttu-id="4bdf7-186">Nadat u de code hebt gekopieerd, wordt uitgelegd wat er in de waarden van deze parameters.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-186">After you copy the code, we'll explain what to put in the values of these parameters.</span></span>

1.  <span data-ttu-id="4bdf7-187">Wijzig bij een opdrachtprompt de map in **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-187">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4bdf7-188">Maak een bestand Config.js in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="4bdf7-189">Voeg de volgende informatie toe:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-189">Add the following information:</span></span>

    ```Javascript
    // Don't commit this file to your public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need to change this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="4bdf7-190">Vereiste waarden</span><span class="sxs-lookup"><span data-stu-id="4bdf7-190">Required values</span></span>

*   <span data-ttu-id="4bdf7-191">**IdentityMetadata**: dit is wanneer `passport-azure-ad` wordt gezocht naar de configuratiegegevens voor de identiteitsprovider (IDP) en de sleutels voor het valideren van de JSON Web Tokens (JWTs).</span><span class="sxs-lookup"><span data-stu-id="4bdf7-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for the identity provider (IDP) and the keys to validate the JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="4bdf7-192">Als u Azure AD gebruikt, wilt u waarschijnlijk niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-192">If you are using Azure AD, you probably don't want to change this.</span></span>

*   <span data-ttu-id="4bdf7-193">**doelgroep**: uw omleidings-URI van de portal.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-193">**audience**: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4bdf7-194">Uw sleutels rouleert met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="4bdf7-195">Zorg ervoor dat u altijd via de URL 'openid_keys' pull en of de app toegang hebt tot het Internet.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-195">Be sure that you always pull from the "openid_keys" URL, and that the app can access the Internet.</span></span>
> 
> 

## <a name="11-add-the-configuration-to-your-serverjs-file"></a><span data-ttu-id="4bdf7-196">11: de configuratie toevoegen aan het bestand Server.js</span><span class="sxs-lookup"><span data-stu-id="4bdf7-196">11: Add the configuration to your Server.js file</span></span>
<span data-ttu-id="4bdf7-197">Uw toepassing moet lezen van de waarden uit het configuratiebestand dat u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-197">Your application needs to read the values from the config file you just created.</span></span> <span data-ttu-id="4bdf7-198">Voeg het .config-bestand als een vereiste bron in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-198">Add the .config file as a required resource in your application.</span></span> <span data-ttu-id="4bdf7-199">De globale variabelen ingesteld op apparaten die in Config.js.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-199">Set the global variables to those that are in Config.js.</span></span>

1.  <span data-ttu-id="4bdf7-200">Wijzig bij de opdrachtprompt de map in **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-200">At the command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4bdf7-201">Open Server.js in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-201">In an editor, open Server.js.</span></span> <span data-ttu-id="4bdf7-202">Voeg de volgende informatie toe:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-202">Add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="4bdf7-203">Een nieuwe sectie aan Server.js toevoegen:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-203">Add a new section to Server.js:</span></span>

    ```Javascript
    // Pass these options in to the ODICBearerStrategy.
    var options = {
    // The URL of the metadata document for your app. Put the keys for token validation from the URL found in the jwks_uri tag in the metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array to hold signed-in users and the current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="4bdf7-204">12: de MongoDB-model en het schema-informatie toevoegen met behulp van Mongoose</span><span class="sxs-lookup"><span data-stu-id="4bdf7-204">12: Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="4bdf7-205">Sluit deze drie bestanden in een REST-API-service.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="4bdf7-206">In dit artikel gebruiken we MongoDB voor het opslaan van onze taken.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-206">In this article, we use MongoDB to store our tasks.</span></span> <span data-ttu-id="4bdf7-207">Bespreken we dit op *stap 4*.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="4bdf7-208">In het bestand Config.js file u hebt gemaakt in stap 11, uw database heet *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-208">In the Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="4bdf7-209">Dat is wat u aan het einde van uw mongoose_auth_local verbindings-URL opnemen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-209">That was what you put at the end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="4bdf7-210">U hoeft deze database niet vooraf in MongoDB te maken.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-210">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="4bdf7-211">De database wordt gemaakt op de eerste uitvoering van de servertoepassing (ervan uitgaande dat de database nog niet bestaat).</span><span class="sxs-lookup"><span data-stu-id="4bdf7-211">The database is created on the first run of your server application (assuming the database does not already exist).</span></span>

<span data-ttu-id="4bdf7-212">U hebt de-server opgegeven welke MongoDB-database moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-212">You've told the server what MongoDB database to use.</span></span> <span data-ttu-id="4bdf7-213">Vervolgens moet u aanvullende code schrijven om het model en het schema voor de taken van de server maken.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-213">Next, you need to write some additional code to create the model and schema for your server's tasks.</span></span>

### <a name="the-model"></a><span data-ttu-id="4bdf7-214">Het model</span><span class="sxs-lookup"><span data-stu-id="4bdf7-214">The model</span></span>
<span data-ttu-id="4bdf7-215">De schemamodel is zeer eenvoudige.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-215">The schema model is very basic.</span></span> <span data-ttu-id="4bdf7-216">U kunt deze als u wilt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="4bdf7-217">Het schemamodel heeft de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-217">The schema model has these values:</span></span>

*   <span data-ttu-id="4bdf7-218">**NAAM**.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-218">**NAME**.</span></span> <span data-ttu-id="4bdf7-219">De persoon die is toegewezen aan de taak.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-219">The person assigned to the task.</span></span> <span data-ttu-id="4bdf7-220">Dit is een **tekenreeks** waarde.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-220">This is a **string** value.</span></span>
*   <span data-ttu-id="4bdf7-221">**TAAK**.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-221">**TASK**.</span></span> <span data-ttu-id="4bdf7-222">De naam van de taak.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-222">The name of the task.</span></span> <span data-ttu-id="4bdf7-223">Dit is een **tekenreeks** waarde.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-223">This is a **string** value.</span></span>
*   <span data-ttu-id="4bdf7-224">**DATUM**.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-224">**DATE**.</span></span> <span data-ttu-id="4bdf7-225">De datum waarop de taak moet voltooid zijn.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-225">The date that the task is due.</span></span> <span data-ttu-id="4bdf7-226">Dit is een **datetime** waarde.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="4bdf7-227">**VOLTOOID**.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-227">**COMPLETED**.</span></span> <span data-ttu-id="4bdf7-228">Hiermee wordt aangegeven of de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-228">Whether the task is completed.</span></span> <span data-ttu-id="4bdf7-229">Dit is een **Booleaanse** waarde.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-229">This is a **Boolean** value.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="4bdf7-230">Het schema in de code maken</span><span class="sxs-lookup"><span data-stu-id="4bdf7-230">Create the schema in the code</span></span>
1.  <span data-ttu-id="4bdf7-231">Wijzig bij een opdrachtprompt de map in **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-231">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4bdf7-232">Open in uw editor Server.js.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-232">In your editor, open Server.js.</span></span> <span data-ttu-id="4bdf7-233">Onder het configuratie-item toevoegen de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-233">Below the configuration entry, add the following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="4bdf7-234">Deze code maakt verbinding met de MongoDB-server.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-234">This code connects to the MongoDB server.</span></span> <span data-ttu-id="4bdf7-235">Ook wordt een schemaobject.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-235">It also returns a schema object.</span></span>

#### <a name="using-the-schema-create-your-model-in-the-code"></a><span data-ttu-id="4bdf7-236">Met het schema, het model in de code maken</span><span class="sxs-lookup"><span data-stu-id="4bdf7-236">Using the schema, create your model in the code</span></span>
<span data-ttu-id="4bdf7-237">Voeg onder de vorige code de volgende code:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-237">Below the preceding code, add the following code:</span></span>

```Javascript
// Create a basic schema to store your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="4bdf7-238">Zoals u van de code ziet, maakt u eerst uw schema.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-238">As you can tell from the code, first you create your schema.</span></span> <span data-ttu-id="4bdf7-239">Vervolgens maakt u een modelobject.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-239">Next, you create a model object.</span></span> <span data-ttu-id="4bdf7-240">Gebruik van het modelobject voor het opslaan van uw gegevens in de code bij het definiëren van uw **routes**.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-240">You use the model object to store your data throughout the code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="4bdf7-241">13: uw routes toevoegen voor de REST-API-taakserver</span><span class="sxs-lookup"><span data-stu-id="4bdf7-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="4bdf7-242">Nu u een databasemodel werken met hebt, toevoegen de routes die u voor de REST-API-server gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-242">Now that you have a database model to work with, add the routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="4bdf7-243">Routes in restify</span><span class="sxs-lookup"><span data-stu-id="4bdf7-243">About routes in restify</span></span>
<span data-ttu-id="4bdf7-244">Routes in restify werk precies dezelfde manier wanneer u de Express-stack gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-244">Routes in restify work exactly the same way they do when you use the Express stack.</span></span> <span data-ttu-id="4bdf7-245">U definieert routes met behulp van de URI die de clienttoepassingen aanroepen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-245">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="4bdf7-246">Meestal kunt definiëren u uw routes in een afzonderlijk bestand.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="4bdf7-247">In deze zelfstudie we onze routes in Server.js geplaatst.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="4bdf7-248">Voor gebruik in productieomgevingen, is het raadzaam dat u rekening te houden routes in een eigen bestand.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="4bdf7-249">Een doorsnee patroon voor een restify-route is:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep the server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="4bdf7-250">Dit is het patroon op de meest eenvoudige niveau.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-250">This is the pattern at the most basic level.</span></span> <span data-ttu-id="4bdf7-251">Restify (en Express) bieden veel diepere functionaliteit, zoals de mogelijkheid voor het definiëren van toepassingstypen en complexe routering tussen verschillende eindpunten.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-251">Restify (and Express) provide much deeper functionality, like the ability to define application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="4bdf7-252">Standaardroutes toevoegen aan een server</span><span class="sxs-lookup"><span data-stu-id="4bdf7-252">Add default routes to your server</span></span>
<span data-ttu-id="4bdf7-253">De eenvoudige CRUD-routes toevoegen: **maken**, **ophalen**, **bijwerken**, en **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-253">Add the basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="4bdf7-254">Wijzig bij een opdrachtprompt de map in **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-254">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4bdf7-255">Open Server.js in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-255">In an editor, open Server.js.</span></span> <span data-ttu-id="4bdf7-256">De databasevermeldingen die u eerder hebt aangebracht toevoegen hieronder de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-256">Below the database entries you made earlier, add the following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow you to use MongoDB Server as your response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it to MongoDB.
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
    req.log.warn(err, 'createTask: unable to save');
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
    'removeTask: unable to delete %s',
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
    req.log.warn(err, 'get: unable to read %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns the list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow us to use MongoDB Server as our response to any origin.
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
    log.warn(err, "There are no tasks in the database. Add one!");
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

### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="4bdf7-257">Foutafhandeling voor de routes toevoegen</span><span class="sxs-lookup"><span data-stu-id="4bdf7-257">Add error handling for the routes</span></span>
<span data-ttu-id="4bdf7-258">Foutafhandeling toevoegen zodat u terug naar de client over het opgetreden probleem kan communiceren.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-258">Add some error handling so you can communicate back to the client about the problem you encountered.</span></span>

<span data-ttu-id="4bdf7-259">Voeg de volgende code hieronder de code die u al hebt geschreven:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-259">Add the following code below the code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back to the client.
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


## <a name="14-create-your-server"></a><span data-ttu-id="4bdf7-260">14: de server maken</span><span class="sxs-lookup"><span data-stu-id="4bdf7-260">14: Create your server</span></span>
<span data-ttu-id="4bdf7-261">Het laatste wat te doen is het toevoegen van uw server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-261">The last thing to do is to add your server instance.</span></span> <span data-ttu-id="4bdf7-262">Het serverexemplaar beheert uw aanroepen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-262">The server instance manages your calls.</span></span>

<span data-ttu-id="4bdf7-263">Restify (en Express) mate aanpassen die u met een REST-API-server gebruiken kunt hebben.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="4bdf7-264">In deze zelfstudie gebruiken we de meest eenvoudige configuratie.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-264">In this tutorial, we use the most basic setup.</span></span>

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
// Allow 5 requests/second by IP address, and burst to 10.
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
## <a name="15-add-the-routes-without-authentication-for-now"></a><span data-ttu-id="4bdf7-265">15: de routes (zonder verificatie nu) toevoegen</span><span class="sxs-lookup"><span data-stu-id="4bdf7-265">15: Add the routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD to add the real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in the pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need to maintain session state. You can experiment with removing API protection.
/* To do this, remove the passport.authenticate() method:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-the-server"></a><span data-ttu-id="4bdf7-266">16: de server wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="4bdf7-266">16: Run the server</span></span>
<span data-ttu-id="4bdf7-267">Het is een goed idee om uw server te testen voordat u verificatie toevoegt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-267">It's a good idea to test your server before you add authentication.</span></span>

<span data-ttu-id="4bdf7-268">Er is de eenvoudigste manier om uw server testen met behulp van curl bij een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-268">The easiest way to test your server is by using curl at a command prompt.</span></span> <span data-ttu-id="4bdf7-269">Om dit te doen, moet u een eenvoudig hulpprogramma waarmee u kunt uitvoer kunt parseren als JSON.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-269">To do this, you need a simple utility that you can use to parse output as JSON.</span></span> 

1.  <span data-ttu-id="4bdf7-270">Installeer het JSON-hulpprogramma we gebruiken in de volgende voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-270">Install the JSON tool that we use in the following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="4bdf7-271">Hiermee wordt het JSON-hulpprogramma op alle vereiste locaties geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-271">This installs the JSON tool globally.</span></span>

2.  <span data-ttu-id="4bdf7-272">Controleer of het MongoDB-exemplaar is geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="4bdf7-273">Wijzig de map in **azuread**, en voer vervolgens curl:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-273">Change the directory to **azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="4bdf7-274">Een taak wilt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-274">To add a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="4bdf7-275">Het antwoord moet zijn:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-275">The response should be:</span></span>

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

5.  <span data-ttu-id="4bdf7-276">Lijst met taken voor Brandon:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="4bdf7-277">Als alle deze opdrachten worden uitgevoerd zonder fouten, bent u OAuth toevoegen aan de REST-API-server.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-277">If all these commands run without errors, you are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="4bdf7-278">*U hebt nu een REST-API-server met MongoDB.*</span><span class="sxs-lookup"><span data-stu-id="4bdf7-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-to-your-rest-api-server"></a><span data-ttu-id="4bdf7-279">17: verificatie toevoegen aan de REST-API-server</span><span class="sxs-lookup"><span data-stu-id="4bdf7-279">17: Add authentication to your REST API server</span></span>
<span data-ttu-id="4bdf7-280">Nu dat u een actieve REST-API hebt, instellen voor gebruik met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-280">Now that you have a running REST API, set it up to use it with Azure AD.</span></span>

<span data-ttu-id="4bdf7-281">Wijzig bij een opdrachtprompt de map in **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-281">At a command prompt, change the directory to **azuread**:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="4bdf7-282">De oidcbearerstrategy gebruiken die is opgenomen in passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="4bdf7-282">Use the oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="4bdf7-283">U kunt een typische REST-TODO-server zonder enige vorm van autorisatie tot nu toe hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="4bdf7-284">Voeg nu verificatie.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-284">Now, add authentication.</span></span>

<span data-ttu-id="4bdf7-285">Ten eerste kunt u aangeven dat u Passport wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-285">First,  indicate that you want to use Passport.</span></span> <span data-ttu-id="4bdf7-286">Dit recht na de configuratie van uw eerdere server genomen:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="4bdf7-287">Wanneer u API's schrijft, is het een goed idee om de gegevens altijd koppelen aan een unieke van het token dat de gebruiker niet kan vervalsen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-287">When you write APIs, it's a good idea to always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="4bdf7-288">Wanneer deze server TODO-items opslaat, slaat deze op basis van de abonnements-ID van de gebruiker in het token (aangeroepen via token.sub).</span><span class="sxs-lookup"><span data-stu-id="4bdf7-288">When this server stores TODO items, it stores them based on the user subscription ID in the token (called through token.sub).</span></span> <span data-ttu-id="4bdf7-289">U kunt de token.sub plaatsen in het veld 'eigenaar'.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-289">You put the token.sub in the “owner” field.</span></span> <span data-ttu-id="4bdf7-290">Dit zorgt ervoor dat alleen die gebruiker toegang heeft tot de gebruiker TODOs.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-290">This ensures that only that user can access the user's TODOs.</span></span> <span data-ttu-id="4bdf7-291">Niemand anders toegang tot de TODOs die zijn ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-291">No one else can access the TODOs that were entered.</span></span> <span data-ttu-id="4bdf7-292">Er is geen blootstelling in de API voor de 'eigenaar'.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-292">There is no exposure in the API for “owner.”</span></span> <span data-ttu-id="4bdf7-293">Een externe gebruiker kan andere gebruikers TODOs, aanvragen, zelfs als ze zijn geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="4bdf7-294">Gebruik vervolgens de Open ID Connect Bearer-strategie die wordt geleverd met `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-294">Next, use the Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="4bdf7-295">Plaats deze achter eerder geplakt:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users.
/*
/* Because of the Passport pattern, you need to manage users and info tokens
/* with a FindorCreate() method. The method must be provided by the implementor.
/* In the following code, you autoregister any user and implement a FindById().
/* It's a good idea to do something more advanced.
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
log.info('verifying the user');
log.info(token, 'was the token retrieved');
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

<span data-ttu-id="4bdf7-296">Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="4bdf7-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="4bdf7-297">Alle schrijvers van strategieën voor het patroon.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-297">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="4bdf7-298">Geeft de strategie voor een `function()` die gebruikmaakt van een token en `done` als parameters.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-298">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="4bdf7-299">De strategie terug nadat al het werk wordt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-299">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="4bdf7-300">Sla de gebruiker en het token niet initialiseren zodat u niet hoeft te vragen voor het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-300">Store the user and stash the token so you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4bdf7-301">De voorafgaande code geldt voor elke gebruiker die kan worden geverifieerd met de server.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-301">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="4bdf7-302">Dit wordt automatische registratie genoemd.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-302">This is known as auto-registration.</span></span> <span data-ttu-id="4bdf7-303">Op een productieserver wilt u niet dat iedereen, kunnen zonder dat zij een registratieproces die u kiest doorlopen eerst.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-303">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="4bdf7-304">Dit is doorgaans het patroon die u in consumenten-apps ziet.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-304">This is usually the pattern you see in consumer apps.</span></span> <span data-ttu-id="4bdf7-305">De app kunt u mogelijk registreren met Facebook, maar vervolgens wordt u gevraagd om in te voeren als u meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-305">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="4bdf7-306">Als u een opdrachtregelprogramma zijn niet voor deze zelfstudie gebruikt, kunt u het e-mailbericht kan extraheren uit het Tokenobject dat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-306">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="4bdf7-307">Vervolgens vraagt u mogelijk de gebruiker in te voeren als u meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-307">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="4bdf7-308">Omdat dit een testserver is, moet u de gebruiker rechtstreeks naar de database in het geheugen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-308">Because this is a test server, you add the user directly to the in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="4bdf7-309">Eindpunten beveiligen</span><span class="sxs-lookup"><span data-stu-id="4bdf7-309">Protect endpoints</span></span>
<span data-ttu-id="4bdf7-310">Eindpunten beveiligen door te geven de **passport.authenticate()** aanroepen met het protocol dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-310">Protect endpoints by specifying the **passport.authenticate()** call with the protocol that you want to use.</span></span>

<span data-ttu-id="4bdf7-311">U kunt uw route in uw servercode voor een meer geavanceerde optie bewerken:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="4bdf7-312">18: de servertoepassing opnieuw uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4bdf7-312">18: Run your server application again</span></span>
<span data-ttu-id="4bdf7-313">Curl opnieuw gebruiken om te zien als u OAuth 2.0-beveiliging voor uw eindpunten hebt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-313">Use curl again to see if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="4bdf7-314">Doe dit voordat u een van uw client-SDK's uitvoeren met dit eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="4bdf7-315">De geretourneerde headers moeten vertellen als de verificatie van uw correct werkt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-315">The headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="4bdf7-316">Zorg ervoor dat uw isntance MongoDB wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="4bdf7-317">Wijzig in de **azuread** directory en gebruik curl:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-317">Change to the **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="4bdf7-318">Probeer een basic POST:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="4bdf7-319">Een 401-respons geeft aan dat de Passport-laag probeert om te leiden naar het geautoriseerde eindpunt, is precies wat u wilt.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-319">A 401 response indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="4bdf7-320">*U hebt nu een REST-API-service die gebruikmaakt van OAuth 2.0.*</span><span class="sxs-lookup"><span data-stu-id="4bdf7-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="4bdf7-321">U bent gegaan zo ver mogelijk kunt u met deze server zonder met behulp van een OAuth 2.0-compatibele client.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="4bdf7-322">Daarvoor moet u een extra zelfstudie bekijken.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-322">For that, you will need to review an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bdf7-323">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4bdf7-323">Next steps</span></span>
<span data-ttu-id="4bdf7-324">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) wordt geleverd als [een ZIP-bestand](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4bdf7-324">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="4bdf7-325">U kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="4bdf7-326">Nu kunt u op verplaatsen met geavanceerdere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-326">Now, you can move on to more advanced topics.</span></span> <span data-ttu-id="4bdf7-327">U wilt proberen [beveiligen van een Node.js-web-app met behulp van het v2.0-eindpunt](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="4bdf7-327">You might want to try [Secure a Node.js web app using the v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="4bdf7-328">Hier volgen enkele aanvullende resources:</span><span class="sxs-lookup"><span data-stu-id="4bdf7-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="4bdf7-329">Handleiding voor Azure AD v2.0-ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="4bdf7-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="4bdf7-330">Stack-overloop 'azure active directory' tag</span><span class="sxs-lookup"><span data-stu-id="4bdf7-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="4bdf7-331">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="4bdf7-331">Get security updates for our products</span></span>
<span data-ttu-id="4bdf7-332">We raden u aan te melden om te worden geïnformeerd wanneer er beveiligingsincidenten optreden.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-332">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="4bdf7-333">Op de [Microsoft technische beveiligingsmeldingen](https://technet.microsoft.com/security/dd252948) pagina moet u zich abonneren op beveiligingswaarschuwingen aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="4bdf7-333">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

