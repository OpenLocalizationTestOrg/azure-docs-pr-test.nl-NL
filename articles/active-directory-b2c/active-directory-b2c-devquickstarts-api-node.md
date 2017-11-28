---
title: 'Azure AD B2C: Een web-API beveiligen met behulp van Node.js | Microsoft Docs'
description: Hoe toobuild een Node.js web-API accepteert die tokens van een B2C-tenant
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="939d7-103">Azure AD B2C: Een web-API ontwikkelen met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="939d7-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="939d7-104">Met Azure Active Directory (Azure AD) B2C kunt u een web-API beveiligen met OAuth 2.0-toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="939d7-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="939d7-105">Deze tokens kunnen client-apps die gebruikmaken van Azure AD B2C tooauthenticate toohello API.</span><span class="sxs-lookup"><span data-stu-id="939d7-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="939d7-106">Dit artikel laat zien hoe een API 'takenlijst' toocreate waarmee gebruikers tooadd en de lijst met taken.</span><span class="sxs-lookup"><span data-stu-id="939d7-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="939d7-107">Hallo-web-API is beveiligd met Azure AD B2C en alleen hun takenlijst kan toomanage geverifieerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="939d7-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="939d7-108">Dit voorbeeld is geschreven met het toobe verbonden tooby met onze [iOS B2C-voorbeeldtoepassing](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="939d7-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="939d7-109">Hallo huidige procedure eerst doen en volg daarna dat voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="939d7-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="939d7-110">**Passport** is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="939d7-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="939d7-111">Passport is flexibel en modulair, en kan onopvallend worden geïnstalleerd in een Express- of Restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="939d7-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="939d7-112">Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.</span><span class="sxs-lookup"><span data-stu-id="939d7-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="939d7-113">We hebben een strategie ontwikkeld voor Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="939d7-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="939d7-114">U installeert deze module en voegt vervolgens hello Azure AD `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="939d7-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="939d7-115">toodo dit voorbeeld moet u:</span><span class="sxs-lookup"><span data-stu-id="939d7-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="939d7-116">U registreert een toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="939d7-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="939d7-117">Instellen van uw toepassing toouse Passport van `azure-ad-passport` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="939d7-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="939d7-118">Configureer een client toepassing toocall Hallo 'takenlijst'-web-API.</span><span class="sxs-lookup"><span data-stu-id="939d7-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="939d7-119">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="939d7-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="939d7-120">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="939d7-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="939d7-121">Een directory is een container voor alle gebruikers, apps, groepen en meer.</span><span class="sxs-lookup"><span data-stu-id="939d7-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="939d7-122">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u verdergaat.</span><span class="sxs-lookup"><span data-stu-id="939d7-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="939d7-123">Een app maken</span><span class="sxs-lookup"><span data-stu-id="939d7-123">Create an application</span></span>
<span data-ttu-id="939d7-124">Vervolgens moet u toocreate een app in uw B2C-directory die Azure AD bepaalde informatie geeft dat het toosecurely moet communiceren met uw app.</span><span class="sxs-lookup"><span data-stu-id="939d7-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="939d7-125">In dit geval zowel Hallo client-app en web-API worden aangegeven met één **toepassings-ID**, omdat ze samen één logische app vormen.</span><span class="sxs-lookup"><span data-stu-id="939d7-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="939d7-126">toocreate een app, volg [deze instructies](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="939d7-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="939d7-127">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="939d7-127">Be sure to:</span></span>

* <span data-ttu-id="939d7-128">Omvatten een **web-app of web api** in Hallo-toepassing</span><span class="sxs-lookup"><span data-stu-id="939d7-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="939d7-129">U `http://localhost/TodoListService` invoert als **antwoord-URL**.</span><span class="sxs-lookup"><span data-stu-id="939d7-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="939d7-130">Het is Hallo-standaard-URL voor dit codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="939d7-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="939d7-131">U een **toepassingsgeheim** maakt voor uw toepassing en dit kopieert.</span><span class="sxs-lookup"><span data-stu-id="939d7-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="939d7-132">U hebt deze gegevens later nodig.</span><span class="sxs-lookup"><span data-stu-id="939d7-132">You need this data later.</span></span> <span data-ttu-id="939d7-133">Opmerking dat deze waarde toobe moet [XML escape-teken](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) voordat u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="939d7-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="939d7-134">Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app.</span><span class="sxs-lookup"><span data-stu-id="939d7-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="939d7-135">U hebt deze gegevens later nodig.</span><span class="sxs-lookup"><span data-stu-id="939d7-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="939d7-136">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="939d7-136">Create your policies</span></span>
<span data-ttu-id="939d7-137">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="939d7-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="939d7-138">Deze app bevat twee identiteitservaringen: registreren en aanmelden.</span><span class="sxs-lookup"><span data-stu-id="939d7-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="939d7-139">U moet één beleid toocreate van elk type, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="939d7-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="939d7-140">Wanneer u uw drie beleidsregels maakt:</span><span class="sxs-lookup"><span data-stu-id="939d7-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="939d7-141">Kies Hallo **weergavenaam** en andere registratiekenmerken in het registratiebeleid.</span><span class="sxs-lookup"><span data-stu-id="939d7-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="939d7-142">Kies Hallo **weergavenaam** en **Object-ID** toepassingsclaims voor elk beleid.</span><span class="sxs-lookup"><span data-stu-id="939d7-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="939d7-143">U kunt ook andere claims kiezen.</span><span class="sxs-lookup"><span data-stu-id="939d7-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="939d7-144">Noteer Hallo **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="939d7-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="939d7-145">Het voorvoegsel Hallo heeft `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="939d7-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="939d7-146">U hebt deze beleidsnamen later nodig.</span><span class="sxs-lookup"><span data-stu-id="939d7-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="939d7-147">Wanneer u uw drie beleidsregels hebt gemaakt, bent u klaar toobuild uw app.</span><span class="sxs-lookup"><span data-stu-id="939d7-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="939d7-148">toolearn over de werking van beleid in Azure AD B2C, beginnen met Hallo [zelfstudie .NET web app aan de slag](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="939d7-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="939d7-149">Hallo code downloaden</span><span class="sxs-lookup"><span data-stu-id="939d7-149">Download hello code</span></span>
<span data-ttu-id="939d7-150">code voor deze zelfstudie Hallo [wordt bewaard in GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="939d7-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="939d7-151">toobuild hello voorbeeld als u gaat, kunt u [een basisproject downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="939d7-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="939d7-152">U kunt Hallo basisproject ook klonen:</span><span class="sxs-lookup"><span data-stu-id="939d7-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="939d7-153">Hallo voltooid app is ook [beschikbaar als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) of op Hallo `complete` vertakking van Hallo dezelfde opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="939d7-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="939d7-154">Node.js voor uw platform downloaden</span><span class="sxs-lookup"><span data-stu-id="939d7-154">Download Node.js for your platform</span></span>
<span data-ttu-id="939d7-155">toosuccessfully dit voorbeeld gebruiken, moet u een werkende implementatie van Node.js.</span><span class="sxs-lookup"><span data-stu-id="939d7-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="939d7-156">Installeer Node.js vanuit [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="939d7-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="939d7-157">MongoDB installeren voor uw platform</span><span class="sxs-lookup"><span data-stu-id="939d7-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="939d7-158">toosuccessfully dit voorbeeld gebruiken, moet u een werkende implementatie van MongoDB.</span><span class="sxs-lookup"><span data-stu-id="939d7-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="939d7-159">We gebruiken uw REST-API persistent MongoDB toomake in alle serverexemplaren.</span><span class="sxs-lookup"><span data-stu-id="939d7-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="939d7-160">Installeer MongoDB vanuit [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="939d7-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="939d7-161">Deze procedure wordt ervan uitgegaan dat u Hallo standaard en -servereindpunten voor MongoDB, namelijk op moment van schrijven van dit Hallo `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="939d7-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="939d7-162">Hallo Restify-modules installeren in uw web-API</span><span class="sxs-lookup"><span data-stu-id="939d7-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="939d7-163">We gebruiken uw REST API Restify toobuild.</span><span class="sxs-lookup"><span data-stu-id="939d7-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="939d7-164">Restify is een minimaal en flexibel Node.js-toepassingsframework dat is afgeleid van Express.</span><span class="sxs-lookup"><span data-stu-id="939d7-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="939d7-165">Het bevat een set krachtige functies voor het ontwikkelen van REST-API's op Connect.</span><span class="sxs-lookup"><span data-stu-id="939d7-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="939d7-166">Restify installeren</span><span class="sxs-lookup"><span data-stu-id="939d7-166">Install Restify</span></span>
<span data-ttu-id="939d7-167">Vanaf de opdrachtregel hello, wijzig de directory te`azuread`.</span><span class="sxs-lookup"><span data-stu-id="939d7-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="939d7-168">Als hello `azuread` directory niet bestaat, maakt deze.</span><span class="sxs-lookup"><span data-stu-id="939d7-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="939d7-169">`cd azuread` of `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="939d7-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="939d7-170">Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="939d7-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="939d7-171">Met deze opdracht wordt Restify geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="939d7-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="939d7-172">Krijgt u een foutmelding?</span><span class="sxs-lookup"><span data-stu-id="939d7-172">Did you get an error?</span></span>
<span data-ttu-id="939d7-173">In sommige besturingssystemen wanneer u `npm`, foutbericht Hallo `Error: EPERM, chmod '/usr/local/bin/..'` en een aanvraag die u Hallo account uitvoeren als beheerder.</span><span class="sxs-lookup"><span data-stu-id="939d7-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="939d7-174">Als dit probleem optreedt, gebruikt u Hallo `sudo` opdracht toorun `npm` op een hoger niveau van bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="939d7-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="939d7-175">Wordt er een DTrace-fout weergegeven?</span><span class="sxs-lookup"><span data-stu-id="939d7-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="939d7-176">Mogelijk wordt er iets in de trant van het volgende weergegeven wanneer u Restify installeert:</span><span class="sxs-lookup"><span data-stu-id="939d7-176">You may see something like this text when you install Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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

<span data-ttu-id="939d7-177">Restify biedt een krachtig mechanisme om REST-aanroepen te traceren met behulp van DTrace.</span><span class="sxs-lookup"><span data-stu-id="939d7-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="939d7-178">Veel besturingssystemen beschikken echter niet over DTrace.</span><span class="sxs-lookup"><span data-stu-id="939d7-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="939d7-179">U kunt deze fouten negeren.</span><span class="sxs-lookup"><span data-stu-id="939d7-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="939d7-180">Hallo-uitvoer van Hallo-opdracht moet worden weergegeven soortgelijke toothis tekst:</span><span class="sxs-lookup"><span data-stu-id="939d7-180">hello output of hello command should appear similar toothis text:</span></span>

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
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="939d7-181">Passport installeren in uw web-API</span><span class="sxs-lookup"><span data-stu-id="939d7-181">Install Passport in your web API</span></span>
<span data-ttu-id="939d7-182">Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd.</span><span class="sxs-lookup"><span data-stu-id="939d7-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="939d7-183">Met behulp van de volgende opdracht Hallo Passport installeren:</span><span class="sxs-lookup"><span data-stu-id="939d7-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="939d7-184">Hallo-uitvoer van de opdracht Hallo moet soortgelijke toothis tekst:</span><span class="sxs-lookup"><span data-stu-id="939d7-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="939d7-185">Passport-azuread tooyour web API toevoegen</span><span class="sxs-lookup"><span data-stu-id="939d7-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="939d7-186">Voeg vervolgens Hallo OAuth-strategie toe met behulp van `passport-azuread`, een reeks strategieën die Azure AD met Passport verbinden.</span><span class="sxs-lookup"><span data-stu-id="939d7-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="939d7-187">Gebruik deze strategie voor bearer-tokens in Hallo REST-API-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="939d7-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="939d7-188">Hoewel OAuth2 een kader biedt waarin elk onbekend type token kan worden uitgegeven, worden alleen bepaalde typen tokens wijdverbreid gebruikt.</span><span class="sxs-lookup"><span data-stu-id="939d7-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="939d7-189">Hallo-tokens voor het beveiligen van eindpunten zijn bearer-tokens.</span><span class="sxs-lookup"><span data-stu-id="939d7-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="939d7-190">Deze typen tokens zijn Hallo meest wordt uitgegeven in OAuth2.</span><span class="sxs-lookup"><span data-stu-id="939d7-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="939d7-191">Veel implementaties wordt ervan uitgegaan dat bearer-tokens Hallo enige type token dat is uitgegeven zijn.</span><span class="sxs-lookup"><span data-stu-id="939d7-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="939d7-192">Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd.</span><span class="sxs-lookup"><span data-stu-id="939d7-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="939d7-193">Hallo Passport installeren `passport-azure-ad` module met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="939d7-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="939d7-194">Hallo-uitvoer van de opdracht Hallo moet soortgelijke toothis tekst:</span><span class="sxs-lookup"><span data-stu-id="939d7-194">hello output of hello command should be similar toothis text:</span></span>

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="939d7-195">MongoDB-modules tooyour web API toevoegen</span><span class="sxs-lookup"><span data-stu-id="939d7-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="939d7-196">In dit voorbeeld wordt MongoDB gebruikt als gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="939d7-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="939d7-197">Installeer daarvoor Mongoose, een veel gebruikte invoegtoepassing voor het beheren van modellen en schema’s.</span><span class="sxs-lookup"><span data-stu-id="939d7-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="939d7-198">Aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="939d7-198">Install additional modules</span></span>
<span data-ttu-id="939d7-199">Vervolgens installeert Hallo resterende vereiste modules.</span><span class="sxs-lookup"><span data-stu-id="939d7-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="939d7-200">Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="939d7-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="939d7-201">Hallo-modules in installeren uw `node_modules` directory:</span><span class="sxs-lookup"><span data-stu-id="939d7-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="939d7-202">Een bestand server.js met de afhankelijkheden maken</span><span class="sxs-lookup"><span data-stu-id="939d7-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="939d7-203">Hallo `server.js` bestand Hallo meerderheid van Hallo functionaliteit biedt voor uw Web-API-server.</span><span class="sxs-lookup"><span data-stu-id="939d7-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="939d7-204">Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="939d7-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="939d7-205">Maak een bestand `server.js` in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="939d7-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="939d7-206">Voeg Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="939d7-206">Add hello following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="939d7-207">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="939d7-207">Save hello file.</span></span> <span data-ttu-id="939d7-208">U terug tooit later.</span><span class="sxs-lookup"><span data-stu-id="939d7-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="939d7-209">Maken van een bestand config.js toostore uw Azure AD-instellingen</span><span class="sxs-lookup"><span data-stu-id="939d7-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="939d7-210">Dit codebestand geeft de configuratieparameters Hallo van uw Azure AD-Portal toohello `Passport.js` bestand.</span><span class="sxs-lookup"><span data-stu-id="939d7-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="939d7-211">U hebt deze configuratiewaarden gemaakt toen u in het eerste deel van de procedure Hallo HALLO hallo-API toohello webportal hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="939d7-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="939d7-212">We uitleggen welke tooput Hallo waarden van deze parameters wanneer u Hallo code hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="939d7-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="939d7-213">Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="939d7-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="939d7-214">Maak een bestand `config.js` in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="939d7-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="939d7-215">Voeg Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="939d7-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="939d7-216">Vereiste waarden</span><span class="sxs-lookup"><span data-stu-id="939d7-216">Required values</span></span>
<span data-ttu-id="939d7-217">`clientID`: Hallo van client-ID van uw Web-API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="939d7-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="939d7-218">`IdentityMetadata`: Dit is de locatie `passport-azure-ad` zoekt naar de configuratiegegevens voor Hallo id-provider.</span><span class="sxs-lookup"><span data-stu-id="939d7-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="939d7-219">Het lijkt erop ook voor Hallo sleutels toovalidate Hallo JSON webtokens.</span><span class="sxs-lookup"><span data-stu-id="939d7-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="939d7-220">`audience`: Hallo uniform resource identifier (URI) van Hallo portal die de aanroepende toepassing te identificeren.</span><span class="sxs-lookup"><span data-stu-id="939d7-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="939d7-221">`tenantName`: de tenantnaam, bijvoorbeeld **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="939d7-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="939d7-222">`policyName`: Hallo toovalidate Hallo tokens binnenkort in tooyour server het gewenste beleid.</span><span class="sxs-lookup"><span data-stu-id="939d7-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="939d7-223">Dit beleid moet Hallo hetzelfde beleid die u voor de clienttoepassing Hallo voor aanmelden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="939d7-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="939d7-224">Op dit moment Hallo gebruik dezelfde beleidsregels voor zowel client als server setup.</span><span class="sxs-lookup"><span data-stu-id="939d7-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="939d7-225">Als u al een procedure hebt voltooid en deze beleidsregels hebt gemaakt, u geen toodo dus opnieuw hoeft.</span><span class="sxs-lookup"><span data-stu-id="939d7-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="939d7-226">Omdat u Hallo procedure hebt voltooid, moet u mag niet tooset nieuw beleid voor clientprocedures op Hallo-site.</span><span class="sxs-lookup"><span data-stu-id="939d7-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="939d7-227">Configuratiebestand tooyour server.js toevoegen</span><span class="sxs-lookup"><span data-stu-id="939d7-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="939d7-228">tooread hello waarden uit Hallo `config.js` bestand dat u hebt gemaakt, het toevoegen van Hallo `.config` bestand als een vereiste bron in uw toepassing en stel vervolgens Hallo globale variabelen toothose in Hallo `config.js` document.</span><span class="sxs-lookup"><span data-stu-id="939d7-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="939d7-229">Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="939d7-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="939d7-230">Open Hallo `server.js` bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="939d7-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="939d7-231">Voeg Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="939d7-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="939d7-232">Voeg een nieuwe sectie te`server.js` die Hallo volgende code bevat:</span><span class="sxs-lookup"><span data-stu-id="939d7-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="939d7-233">Vervolgens laten we de tijdelijke aanduidingen voor Hallo gebruikers we van onze aanroepen toepassingen ontvangen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="939d7-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="939d7-234">U gaat ook een logger maken.</span><span class="sxs-lookup"><span data-stu-id="939d7-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="939d7-235">Hallo MongoDB-model en schema-informatie toevoegen met behulp van Mongoose</span><span class="sxs-lookup"><span data-stu-id="939d7-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="939d7-236">Hallo handig eerdere voorbereiding wanneer u deze drie bestanden samenbrengt in een REST-API-service.</span><span class="sxs-lookup"><span data-stu-id="939d7-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="939d7-237">Voor deze procedure gebruikt u MongoDB toostore uw taken, zoals eerder besproken.</span><span class="sxs-lookup"><span data-stu-id="939d7-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="939d7-238">In Hallo `config.js` -bestand dat u uw database aangeroepen **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="939d7-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="939d7-239">Die naam is ook wat u achter Hallo Hallo opnemen `mongoose_auth_local` verbindings-URL.</span><span class="sxs-lookup"><span data-stu-id="939d7-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="939d7-240">U hoeft niet toocreate deze vooraf in MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="939d7-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="939d7-241">Het Hallo-database voor u gemaakt op de eerste uitvoering van de servertoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="939d7-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="939d7-242">Nadat u welke MongoDB-database toouse Hallo-server zien, moet u toowrite enkele aanvullende code toocreate Hallo model en het schema voor de servertaken.</span><span class="sxs-lookup"><span data-stu-id="939d7-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="939d7-243">Hallo model uitbreiden</span><span class="sxs-lookup"><span data-stu-id="939d7-243">Expand hello model</span></span>
<span data-ttu-id="939d7-244">Dit schemamodel is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="939d7-244">This schema model is simple.</span></span> <span data-ttu-id="939d7-245">U kunt het naar behoefte uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="939d7-245">You can expand it as required.</span></span>

<span data-ttu-id="939d7-246">`owner`: De persoon toohello taak is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="939d7-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="939d7-247">Dit object is een **tekenreeks**.</span><span class="sxs-lookup"><span data-stu-id="939d7-247">This object is a **string**.</span></span>  

<span data-ttu-id="939d7-248">`Text`: Hallo taak zelf.</span><span class="sxs-lookup"><span data-stu-id="939d7-248">`Text`: hello task itself.</span></span> <span data-ttu-id="939d7-249">Dit object is een **tekenreeks**.</span><span class="sxs-lookup"><span data-stu-id="939d7-249">This object is a **string**.</span></span>

<span data-ttu-id="939d7-250">`date`: Hallo datum die taak Hallo vervalt.</span><span class="sxs-lookup"><span data-stu-id="939d7-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="939d7-251">Dit object is een **datum/tijd**.</span><span class="sxs-lookup"><span data-stu-id="939d7-251">This object is a **datetime**.</span></span>

<span data-ttu-id="939d7-252">`completed`: Als het Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="939d7-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="939d7-253">Dit object is een **Booleaanse waarde**.</span><span class="sxs-lookup"><span data-stu-id="939d7-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="939d7-254">Hallo-schema in Hallo code maken</span><span class="sxs-lookup"><span data-stu-id="939d7-254">Create hello schema in hello code</span></span>
<span data-ttu-id="939d7-255">Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="939d7-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="939d7-256">Open Hallo `server.js` bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="939d7-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="939d7-257">Hallo volgende informatie hieronder Hallo configuratie-item toevoegen:</span><span class="sxs-lookup"><span data-stu-id="939d7-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="939d7-258">Hallo-schema voor het eerst wordt gemaakt en maakt u een modelobject dat u uw gegevens in de gehele Hallo code bij het definiëren van toostore uw **routes**.</span><span class="sxs-lookup"><span data-stu-id="939d7-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="939d7-259">Routes toevoegen voor de REST-API-taakserver</span><span class="sxs-lookup"><span data-stu-id="939d7-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="939d7-260">Nu u een database model toowork met hebt, toevoegen Hallo routes die u voor de REST-API-server gebruikt.</span><span class="sxs-lookup"><span data-stu-id="939d7-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="939d7-261">Routes in Restify</span><span class="sxs-lookup"><span data-stu-id="939d7-261">About routes in Restify</span></span>
<span data-ttu-id="939d7-262">Routes werken in Restify op Hallo dezelfde manier als wanneer ze de Express-stack hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="939d7-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="939d7-263">U definieert routes met behulp van Hallo URI dat u Hallo client toepassingen toocall verwacht.</span><span class="sxs-lookup"><span data-stu-id="939d7-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="939d7-264">Een doorsnee patroon voor een Restify-route is:</span><span class="sxs-lookup"><span data-stu-id="939d7-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="939d7-265">U kunt Restify en Express gebruiken voor een veel diepere functionaliteit, zoals voor het definiëren van toepassingstypen en de uitvoering van complexe routering tussen verschillende eindpunten.</span><span class="sxs-lookup"><span data-stu-id="939d7-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="939d7-266">Voor Hallo doel van deze zelfstudie Houd we deze routes eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="939d7-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="939d7-267">Standaard routes tooyour server toevoegen</span><span class="sxs-lookup"><span data-stu-id="939d7-267">Add default routes tooyour server</span></span>
<span data-ttu-id="939d7-268">U nu Hallo eenvoudige CRUD-routes voor toevoegen **maken** en **lijst** voor onze REST-API.</span><span class="sxs-lookup"><span data-stu-id="939d7-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="939d7-269">Andere deze routes kunnen worden gevonden in Hallo `complete` vertakking van Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="939d7-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="939d7-270">Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="939d7-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="939d7-271">Open Hallo `server.js` bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="939d7-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="939d7-272">Onder de databasevermeldingen Hallo aangebrachte hoger toevoegen Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="939d7-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="939d7-273">Foutafhandeling voor Hallo routes toevoegen</span><span class="sxs-lookup"><span data-stu-id="939d7-273">Add error handling for hello routes</span></span>
<span data-ttu-id="939d7-274">Sommige foutafhandeling toevoegen zodat u eventuele problemen die kunnen optreden back toohello-client op een manier die kunt kan communiceren.</span><span class="sxs-lookup"><span data-stu-id="939d7-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="939d7-275">Hallo na code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="939d7-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a><span data-ttu-id="939d7-276">De server maken</span><span class="sxs-lookup"><span data-stu-id="939d7-276">Create your server</span></span>
<span data-ttu-id="939d7-277">U hebt nu een database gedefinieerd en de routes geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="939d7-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="939d7-278">Hallo laatste wat voor u toodo is tooadd Hallo server-exemplaar waarmee uw aanroepen worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="939d7-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="939d7-279">Restify en Express kunt u mate aanpassen voor een REST-API-server, maar we de meest eenvoudige configuratie Hallo hier gebruiken.</span><span class="sxs-lookup"><span data-stu-id="939d7-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="939d7-280">Hallo routes toohello server (zonder verificatie) toevoegen</span><span class="sxs-lookup"><span data-stu-id="939d7-280">Add hello routes toohello server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="939d7-281">Authentication tooyour REST-API-server toevoegen</span><span class="sxs-lookup"><span data-stu-id="939d7-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="939d7-282">Nu u een actieve REST-API-server hebt, kunt u deze gaan gebruiken met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="939d7-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="939d7-283">Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="939d7-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="939d7-284">Hallo OIDCBearerStrategy die is opgenomen in passport-azure-ad gebruiken</span><span class="sxs-lookup"><span data-stu-id="939d7-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="939d7-285">Wanneer u API's schrijft, u moet altijd koppelen Hallo gegevens toosomething uniek in vergelijking met het Hallo-token dat Hallo gebruiker niet kunnen vervalsen.</span><span class="sxs-lookup"><span data-stu-id="939d7-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="939d7-286">Wanneer Hallo server ToDo-items opslaat, gebeurt dit op basis van Hallo **oid** van Hallo-gebruiker in Hallo-token (aangeroepen via token.oid), die in het veld Hallo 'eigenaar' gaat.</span><span class="sxs-lookup"><span data-stu-id="939d7-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="939d7-287">Met deze waarde zorgt u ervoor dat alleen die gebruiker toegang heeft tot zijn/haar eigen ToDo-items.</span><span class="sxs-lookup"><span data-stu-id="939d7-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="939d7-288">Er is geen blootstelling in Hallo API van de 'eigenaar' zodat een externe gebruiker anderen ToDo-items aanvragen kan, zelfs als ze zijn geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="939d7-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="939d7-289">Gebruik vervolgens Hallo bearer-strategie die wordt geleverd met `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="939d7-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="939d7-290">Hallo hetzelfde patroon wordt gebruikt voor alle strategieën Passport.</span><span class="sxs-lookup"><span data-stu-id="939d7-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="939d7-291">U geeft hieraan een `function()` door die `token` en `done` als parameters heeft.</span><span class="sxs-lookup"><span data-stu-id="939d7-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="939d7-292">Hallo-strategie komt weer tooyou nadat deze zijn werk heeft gedaan.</span><span class="sxs-lookup"><span data-stu-id="939d7-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="939d7-293">U moet vervolgens Hallo gebruiker opslaat en Hallo token opslaan zodat u niet tooask voor het opnieuw hoeft.</span><span class="sxs-lookup"><span data-stu-id="939d7-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="939d7-294">Hallo bovenstaande code wordt elke gebruiker die zich tooauthenticate tooyour server.</span><span class="sxs-lookup"><span data-stu-id="939d7-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="939d7-295">Dit proces wordt automatische registratie genoemd.</span><span class="sxs-lookup"><span data-stu-id="939d7-295">This process is known as autoregistration.</span></span> <span data-ttu-id="939d7-296">In productieservers laat niet in alle gebruikers toegang Hallo API zonder dat zij een registratieproces doorlopen eerst.</span><span class="sxs-lookup"><span data-stu-id="939d7-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="939d7-297">Dit proces is meestal Hallo patroon dat u in consumenten-apps die tooregister toestaan ziet via Facebook, maar vervolgens vraagt u toofill aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="939d7-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="939d7-298">Als dit programma is niet een opdrachtregelprogramma, kan hebben we Hallo e opgehaald uit Hallo Tokenobject dat wordt geretourneerd en vervolgens gebruikers toofill aanvullende informatie gevraagd.</span><span class="sxs-lookup"><span data-stu-id="939d7-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="939d7-299">Omdat dit een voorbeeld is, we ze tooan in-memory database toevoegen.</span><span class="sxs-lookup"><span data-stu-id="939d7-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="939d7-300">Dat het weigert uitvoeren van uw toepassing server tooverify u</span><span class="sxs-lookup"><span data-stu-id="939d7-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="939d7-301">U kunt `curl` toosee hebt u nu OAuth2-bescherming voor uw eindpunten.</span><span class="sxs-lookup"><span data-stu-id="939d7-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="939d7-302">Hallo geretourneerde headers moeten voldoende tootell u dat u op het juiste pad Hallo.</span><span class="sxs-lookup"><span data-stu-id="939d7-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="939d7-303">Controleer of het MongoDB-exemplaar is geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="939d7-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="939d7-304">Toohello directory en Voer Hallo-server wijzigen:</span><span class="sxs-lookup"><span data-stu-id="939d7-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="939d7-305">Voer `curl` uit in een nieuw terminalvenster</span><span class="sxs-lookup"><span data-stu-id="939d7-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="939d7-306">Probeer een basic POST:</span><span class="sxs-lookup"><span data-stu-id="939d7-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="939d7-307">Een 401-fout is Hallo-reactie die u wilt.</span><span class="sxs-lookup"><span data-stu-id="939d7-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="939d7-308">Hiermee wordt aangegeven dat Hallo Passport-laag probeert tooredirect toohello autoriseren eindpunt.</span><span class="sxs-lookup"><span data-stu-id="939d7-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="939d7-309">U hebt nu een REST-API-service die gebruikmaakt van OAuth2</span><span class="sxs-lookup"><span data-stu-id="939d7-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="939d7-310">U hebt een REST-API geïmplementeerd met behulp van Restify en OAuth!</span><span class="sxs-lookup"><span data-stu-id="939d7-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="939d7-311">U hebt nu voldoende code zodat u kunt doorgaan toodevelop uw service en op dit voorbeeld bouwen.</span><span class="sxs-lookup"><span data-stu-id="939d7-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="939d7-312">U bent nu met deze server zo ver mogelijk gegaan zonder gebruik te maken van een OAuth2-compatibele client.</span><span class="sxs-lookup"><span data-stu-id="939d7-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="939d7-313">Voor die stap gebruikt u een extra procedure zoals onze [tooa web-API verbinden met behulp van iOS met B2C](active-directory-b2c-devquickstarts-ios.md) scenario.</span><span class="sxs-lookup"><span data-stu-id="939d7-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="939d7-314">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="939d7-314">Next steps</span></span>
<span data-ttu-id="939d7-315">U kunt nu toomore geavanceerde onderwerpen, zoals verplaatsen:</span><span class="sxs-lookup"><span data-stu-id="939d7-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="939d7-316">Verbinding maken met tooa web-API met behulp van iOS met B2C</span><span class="sxs-lookup"><span data-stu-id="939d7-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
