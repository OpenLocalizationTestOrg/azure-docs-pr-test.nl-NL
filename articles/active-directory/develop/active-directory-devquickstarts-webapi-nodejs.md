---
title: aaaAzure AD Node.js aan de slag | Microsoft Docs
description: "Hoe toobuild een REST Node.js-web-API die kan worden geïntegreerd met Azure AD voor verificatie."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="039e4-103">Aan de slag met web-API's voor Node.js</span><span class="sxs-lookup"><span data-stu-id="039e4-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="039e4-104">*Passport* is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="039e4-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="039e4-105">Flexibel en modulair, Passport onopvallend in tooany kan worden verwijderd op basis van de Express of Restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="039e4-105">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="039e4-106">Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.</span><span class="sxs-lookup"><span data-stu-id="039e4-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="039e4-107">We hebben een strategie ontwikkeld voor Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="039e4-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="039e4-108">We installeert deze module en voegt u Hallo Microsoft Azure Active Directory `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="039e4-108">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="039e4-109">toodo, moet u:</span><span class="sxs-lookup"><span data-stu-id="039e4-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="039e4-110">U registreert een toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="039e4-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="039e4-111">Instellen van uw app toouse Passport van `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="039e4-111">Set up your app toouse Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="039e4-112">Configureer een client toepassing toocall hello tooDo lijst web-API.</span><span class="sxs-lookup"><span data-stu-id="039e4-112">Configure a client application toocall hello tooDo List web API.</span></span>

<span data-ttu-id="039e4-113">Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="039e4-113">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="039e4-114">In dit artikel wordt niet beschreven hoe tooimplement aanmelden, registreren, of profiel management met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="039e4-114">This article doesn't cover how tooimplement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="039e4-115">Dit artikel gaat over het aanroepen van web API's nadat Hallo gebruiker al is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="039e4-115">It focuses on calling web APIs after hello user is already authenticated.</span></span>  <span data-ttu-id="039e4-116">Het is raadzaam dat u met begint [hoe toointegrate met Azure Active Directory-document](active-directory-how-to-integrate.md) toolearn over Hallo basisprincipes van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="039e4-116">We recommend that you start with [How toointegrate with Azure Active Directory document](active-directory-how-to-integrate.md) toolearn about hello basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="039e4-117">We alle Hallo broncode bijvoorbeeld uitgevoerd in GitHub onder een MIT-licentie hebt uitgebracht dus gratis tooclone (of zelfs beter fork) en feedback geven en pull-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="039e4-117">We've released all hello source code for this running example in GitHub under an MIT license, so feel free tooclone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="039e4-118">Over Node.js-modules</span><span class="sxs-lookup"><span data-stu-id="039e4-118">About Node.js modules</span></span>
<span data-ttu-id="039e4-119">We Node.js-modules gebruiken in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="039e4-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="039e4-120">Modules zijn geladen JavaScript-pakketten die specifieke functionaliteit voor uw toepassing bieden.</span><span class="sxs-lookup"><span data-stu-id="039e4-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="039e4-121">U installeren meestal modules met behulp van Node.js een opdrachtregelprogramma NPM Hallo in Hallo NPM-installatiemap.</span><span class="sxs-lookup"><span data-stu-id="039e4-121">You usually install modules by using hello Node.js an NPM command-line tool in hello NPM installation directory.</span></span> <span data-ttu-id="039e4-122">Sommige modules, zoals Hallo HTTP-module, zijn echter opgenomen in Hallo core Node.js-pakket.</span><span class="sxs-lookup"><span data-stu-id="039e4-122">However, some modules, such as hello HTTP module, are included in hello core Node.js package.</span></span>

<span data-ttu-id="039e4-123">Geïnstalleerde modules worden opgeslagen in Hallo **node_modules** map in de hoofdmap Hallo van uw Node.js-installatiemap.</span><span class="sxs-lookup"><span data-stu-id="039e4-123">Installed modules are saved in hello **node_modules** directory at hello root of your Node.js installation directory.</span></span> <span data-ttu-id="039e4-124">Elke module Hallo **node_modules** directory onderhoudt een eigen **node_modules** map waarin zich geen modules die afhankelijk zijn van.</span><span class="sxs-lookup"><span data-stu-id="039e4-124">Each module in hello **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="039e4-125">Ook elke vereiste module heeft een **node_modules** directory.</span><span class="sxs-lookup"><span data-stu-id="039e4-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="039e4-126">Deze directory recursieve structuur vertegenwoordigt Hallo afhankelijkheidsketen.</span><span class="sxs-lookup"><span data-stu-id="039e4-126">This recursive directory structure represents hello dependency chain.</span></span>

<span data-ttu-id="039e4-127">Deze structuur van de keten afhankelijkheid resulteert in een grotere toepassing footprint.</span><span class="sxs-lookup"><span data-stu-id="039e4-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="039e4-128">Maar ook wordt hiermee gegarandeerd dat alle afhankelijkheden wordt voldaan en die Hallo-versie van het Hallo-modules die wordt gebruikt in ontwikkeling ook in productie gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="039e4-128">But it also guarantees that all dependencies are met and that hello version of hello modules that's used in development is also used in production.</span></span> <span data-ttu-id="039e4-129">Dit gedrag Hallo productie-app beter voorspelbaar maakt en voorkomt dat versioning problemen die gevolgen voor gebruikers hebben mogelijk.</span><span class="sxs-lookup"><span data-stu-id="039e4-129">This makes hello production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="039e4-130">Stap 1: Een Azure AD-tenant registreren</span><span class="sxs-lookup"><span data-stu-id="039e4-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="039e4-131">toouse dit steekproef, moet u een Azure Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="039e4-131">toouse this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="039e4-132">Als u niet zeker weet welke tenant of hoe tooget, Zie [hoe tooget een Azure AD-tenant](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="039e4-132">If you're not sure what a tenant is or how tooget one, see [How tooget an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="039e4-133">Stap 2: Een toepassing maken</span><span class="sxs-lookup"><span data-stu-id="039e4-133">Step 2: Create an application</span></span>
<span data-ttu-id="039e4-134">Vervolgens maakt u een app in uw directory dat biedt Azure AD-informatie dat het toosecurely moet met uw app communiceren.</span><span class="sxs-lookup"><span data-stu-id="039e4-134">Next you create an app in your directory that gives Azure AD information that it needs toosecurely communicate with your app.</span></span>  <span data-ttu-id="039e4-135">Zowel Hallo client-app en web-API worden aangegeven met één **toepassings-ID** in dit geval omdat ze samen één logische app vormen.</span><span class="sxs-lookup"><span data-stu-id="039e4-135">Both hello client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="039e4-136">toocreate een app, volg [deze instructies](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="039e4-136">toocreate an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="039e4-137">Als u een line-of-business-app bouwt [deze aanvullende instructies nuttig kunnen zijn](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="039e4-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="039e4-138">een toepassing toocreate:</span><span class="sxs-lookup"><span data-stu-id="039e4-138">toocreate an application:</span></span>

1. <span data-ttu-id="039e4-139">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="039e4-139">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="039e4-140">In het bovenste menu hello, selecteert u uw account.</span><span class="sxs-lookup"><span data-stu-id="039e4-140">On hello top menu, select your account.</span></span> <span data-ttu-id="039e4-141">Klik vervolgens onder Hallo **Directory** Hallo Active Directory-tenant waar u tooregister Kies uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="039e4-141">Then, under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="039e4-142">Selecteer in het menu aan de linkerkant Hallo Hallo **meer Services**, en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="039e4-142">In hello menu on hello left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="039e4-143">Selecteer **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="039e4-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="039e4-144">Ga als volgt Hallo prompts toocreate een **webtoepassing en/of WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="039e4-144">Follow hello prompts toocreate a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="039e4-145">Hallo **naam** Hallo toepassing beschrijving van uw toepassing tooend gebruikers.</span><span class="sxs-lookup"><span data-stu-id="039e4-145">hello **name** of hello application describes your application tooend users.</span></span>

      * <span data-ttu-id="039e4-146">Hallo **aanmeldings-URL** Hallo basis-URL van uw app is.</span><span class="sxs-lookup"><span data-stu-id="039e4-146">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="039e4-147">standaard-URL van de voorbeeldcode Hallo is Hallo `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="039e4-147">hello default URL of hello sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="039e4-148">Nadat u hebt geregistreerd, wijst Azure AD uw app een unieke id</span><span class="sxs-lookup"><span data-stu-id="039e4-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="039e4-149">U moet deze waarde in de volgende secties hello, dus kopiëren van de pagina van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="039e4-149">You need this value in hello next sections, so copy it from hello application page.</span></span>

7. <span data-ttu-id="039e4-150">Van Hallo **instellingen** -> **eigenschappen** pagina voor uw toepassing, Hallo App ID URI bijwerken.</span><span class="sxs-lookup"><span data-stu-id="039e4-150">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="039e4-151">Hallo **App ID URI** is de unieke id voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="039e4-151">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="039e4-152">Hallo-conventie is toouse `https://<tenant-domain>/<app-name>`, bijvoorbeeld: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="039e4-152">hello convention is toouse `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="039e4-153">Maak een **sleutel** voor uw toepassing uit Hallo **instellingen** pagina en kopieer het ergens.</span><span class="sxs-lookup"><span data-stu-id="039e4-153">Create a **Key** for your application from hello **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="039e4-154">U moet deze binnenkort.</span><span class="sxs-lookup"><span data-stu-id="039e4-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="039e4-155">Stap 3: Node.js voor uw platform downloaden</span><span class="sxs-lookup"><span data-stu-id="039e4-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="039e4-156">toosuccessfully dit voorbeeld gebruiken, moet u een werkende implementatie van Node.js hebben.</span><span class="sxs-lookup"><span data-stu-id="039e4-156">toosuccessfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="039e4-157">Installeer Node.js vanuit [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="039e4-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="039e4-158">Stap 4: Installatie MongoDB op uw platform</span><span class="sxs-lookup"><span data-stu-id="039e4-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="039e4-159">toosuccessfully dit voorbeeld gebruiken, moet u een werkende implementatie van MongoDB hebben.</span><span class="sxs-lookup"><span data-stu-id="039e4-159">toosuccessfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="039e4-160">U MongoDB toomake Hallo REST-API persistent gebruiken in alle serverexemplaren.</span><span class="sxs-lookup"><span data-stu-id="039e4-160">You use MongoDB toomake hello REST API persistent across server instances.</span></span>

<span data-ttu-id="039e4-161">Installeer MongoDB vanuit [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="039e4-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="039e4-162">In dit scenario wordt ervan uitgegaan dat u Hallo standaard en -servereindpunten voor MongoDB, die op moment van schrijven van dit Hallo mongodb://localhost is.</span><span class="sxs-lookup"><span data-stu-id="039e4-162">This walkthrough assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="039e4-163">Stap 5: Hallo Restify-modules installeren in uw web-API</span><span class="sxs-lookup"><span data-stu-id="039e4-163">Step 5: Install hello Restify modules in your web API</span></span>
<span data-ttu-id="039e4-164">We gebruiken Restify toobuild onze REST-API.</span><span class="sxs-lookup"><span data-stu-id="039e4-164">We are using Restify toobuild our REST API.</span></span> <span data-ttu-id="039e4-165">Restify is een minimaal en flexibel Node.js-toepassingsframework dat afgeleid van Express.</span><span class="sxs-lookup"><span data-stu-id="039e4-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="039e4-166">Het bevat een set krachtige functies voor het ontwikkelen van REST-API's op Connect.</span><span class="sxs-lookup"><span data-stu-id="039e4-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="039e4-167">Restify installeren</span><span class="sxs-lookup"><span data-stu-id="039e4-167">Install Restify</span></span>
1. <span data-ttu-id="039e4-168">Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** directory.</span><span class="sxs-lookup"><span data-stu-id="039e4-168">From hello command line, change directories toohello **azuread** directory.</span></span> <span data-ttu-id="039e4-169">Als hello **azuread** directory niet bestaat, maakt.</span><span class="sxs-lookup"><span data-stu-id="039e4-169">If hello **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="039e4-170">Type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="039e4-170">Type hello following command:</span></span>

    `npm install restify`

    <span data-ttu-id="039e4-171">Met deze opdracht wordt Restify geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="039e4-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="039e4-172">Krijgt u een foutmelding?</span><span class="sxs-lookup"><span data-stu-id="039e4-172">Did you get an error?</span></span>
<span data-ttu-id="039e4-173">Wanneer u NPM op sommige besturingssystemen gebruikt, wordt u er een foutmelding waarin wordt gemeld **fout: EPERM, type chmod ' / usr/lokale/bin /...'**</span><span class="sxs-lookup"><span data-stu-id="039e4-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="039e4-174">en een suggestie dat u actieve Hallo-account als beheerder probeert.</span><span class="sxs-lookup"><span data-stu-id="039e4-174">and a suggestion that you try running hello account as an administrator.</span></span> <span data-ttu-id="039e4-175">Als dit het geval is, gebruik van Hallo sudo-opdracht toorun NPM op een hoger niveau van bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="039e4-175">If this occurs, use hello sudo command toorun NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="039e4-176">Krijgt u een fout met betrekking tot DTRACE?</span><span class="sxs-lookup"><span data-stu-id="039e4-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="039e4-177">U ziet een fout als volgt wanneer u Restify installeert:</span><span class="sxs-lookup"><span data-stu-id="039e4-177">You might see an error like this when installing Restify:</span></span>

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
<span data-ttu-id="039e4-178">Restify biedt een krachtig mechanisme om REST-aanroepen te traceren met behulp van DTrace.</span><span class="sxs-lookup"><span data-stu-id="039e4-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="039e4-179">Veel besturingssystemen hoeft echter geen DTrace.</span><span class="sxs-lookup"><span data-stu-id="039e4-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="039e4-180">U kunt deze fouten negeren.</span><span class="sxs-lookup"><span data-stu-id="039e4-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="039e4-181">Hallo-uitvoer van deze opdracht ziet er vergelijkbare toohello volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="039e4-181">hello output of this command should look similar toohello following output:</span></span>

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


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="039e4-182">Stap 6: Installatie Passport.js in uw web-API</span><span class="sxs-lookup"><span data-stu-id="039e4-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="039e4-183">[Passport](http://passportjs.org/) is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="039e4-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="039e4-184">Flexibel en modulair, Passport onopvallend in tooany kan worden verwijderd op basis van de Express of Restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="039e4-184">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="039e4-185">Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.</span><span class="sxs-lookup"><span data-stu-id="039e4-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="039e4-186">We hebben een strategie ontwikkeld voor Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="039e4-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="039e4-187">We installeert deze module en voeg vervolgens hello Azure Active Directory strategie-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="039e4-187">We install this module and then add hello Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="039e4-188">Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** directory.</span><span class="sxs-lookup"><span data-stu-id="039e4-188">From hello command line, change directories toohello **azuread** directory.</span></span>

2. <span data-ttu-id="039e4-189">tooinstall passport.js, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="039e4-189">tooinstall passport.js, enter hello following command :</span></span>

    `npm install passport`

    <span data-ttu-id="039e4-190">Hallo-uitvoer van Hallo opdracht ziet er vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="039e4-190">hello output of hello command should look similar toohello following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="039e4-191">Stap 7: Passport-Azure-AD tooyour web API toevoegen</span><span class="sxs-lookup"><span data-stu-id="039e4-191">Step 7: Add Passport-Azure-AD tooyour web API</span></span>
<span data-ttu-id="039e4-192">Naast we Hallo OAuth-strategie toevoegen met behulp van `passport-azure-ad`, een reeks strategieën die verbinding maken met Azure Active Directory-tooPassport.</span><span class="sxs-lookup"><span data-stu-id="039e4-192">Next we add hello OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory tooPassport.</span></span> <span data-ttu-id="039e4-193">We gebruiken deze strategie voor bearer-tokens in dit voorbeeld REST-API.</span><span class="sxs-lookup"><span data-stu-id="039e4-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="039e4-194">Hoewel OAuth2 een kader waarin elk onbekend type token kan worden uitgegeven, worden alleen bepaalde typen worden vaak gebruikt.</span><span class="sxs-lookup"><span data-stu-id="039e4-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="039e4-195">Bearer-tokens zijn de meest gebruikte Hallo tokens voor het beveiligen van eindpunten.</span><span class="sxs-lookup"><span data-stu-id="039e4-195">Bearer tokens are hello most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="039e4-196">Type Hallo meest wordt uitgegeven in OAuth2-token zijn.</span><span class="sxs-lookup"><span data-stu-id="039e4-196">They are hello most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="039e4-197">Veel implementaties wordt ervan uitgegaan dat bearer-tokens zijn alleen type Hallo van tokens die zijn uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="039e4-197">Many implementations assume that bearer tokens are hello only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="039e4-198">Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** directory.</span><span class="sxs-lookup"><span data-stu-id="039e4-198">From hello command line, change directories toohello **azuread** directory.</span></span>

<span data-ttu-id="039e4-199">Type Hallo volgende opdracht tooinstall hello Passport.js `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="039e4-199">Type hello following command tooinstall hello Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="039e4-200">Hallo-uitvoer van Hallo opdracht ziet er vergelijkbare toohello volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="039e4-200">hello output of hello command should look similar toohello following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="039e4-201">Stap 8: MongoDB-modules tooyour web API toevoegen</span><span class="sxs-lookup"><span data-stu-id="039e4-201">Step 8: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="039e4-202">We gebruikt MongoDB als onze gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="039e4-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="039e4-203">Daarom moeten we tooinstall Hallo veelgebruikte invoegtoepassing aangeroepen Mongoose toomanage modellen en schema's.</span><span class="sxs-lookup"><span data-stu-id="039e4-203">For that reason, we need tooinstall hello widely used plug-in called Mongoose toomanage models and schemas.</span></span> <span data-ttu-id="039e4-204">Er moet ook tooinstall Hallo databasestuurprogramma voor MongoDB (dit wordt ook MongoDB genoemd).</span><span class="sxs-lookup"><span data-stu-id="039e4-204">We also need tooinstall hello database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="039e4-205">Stap 9: Aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="039e4-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="039e4-206">Naast er Hallo resterende vereiste modules worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="039e4-206">Next we install hello remaining required modules.</span></span>

1. <span data-ttu-id="039e4-207">Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="039e4-207">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="039e4-208">Voer Hallo opdrachten tooinstall na deze modules in uw **node_modules** directory:</span><span class="sxs-lookup"><span data-stu-id="039e4-208">Enter hello following commands tooinstall these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="039e4-209">Stap 10: Een server.js met de afhankelijkheden maken</span><span class="sxs-lookup"><span data-stu-id="039e4-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="039e4-210">Hallo server.js-bestand bevat de meeste Hallo-functionaliteit voor onze web API-server.</span><span class="sxs-lookup"><span data-stu-id="039e4-210">hello server.js file provides most of hello functionality for our web API server.</span></span> <span data-ttu-id="039e4-211">We toevoegen onze toothis codebestand de meeste.</span><span class="sxs-lookup"><span data-stu-id="039e4-211">We add most of our code toothis file.</span></span> <span data-ttu-id="039e4-212">Voor productiedoeleinden, is het raadzaam dat u Hallo-functionaliteit in kleinere bestanden, zoals afzonderlijke routes en controllers opsplitsen.</span><span class="sxs-lookup"><span data-stu-id="039e4-212">For production purposes, we recommend that you refactor hello functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="039e4-213">In deze demonstratie gebruiken we server.js voor deze functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="039e4-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="039e4-214">Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="039e4-214">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="039e4-215">Maak een `server.js` bestand in uw favoriete editor en voeg vervolgens Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="039e4-215">Create a `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. <span data-ttu-id="039e4-216">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="039e4-216">Save hello file.</span></span> <span data-ttu-id="039e4-217">Er wordt kort tooit geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="039e4-217">We'll return tooit shortly.</span></span>

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="039e4-218">Stap 11: Maak een bestand config toostore uw Azure AD-instellingen</span><span class="sxs-lookup"><span data-stu-id="039e4-218">Step 11: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="039e4-219">Dit codebestand geeft de configuratieparameters Hallo van uw Azure Active Directory-portal tooPassport.js.</span><span class="sxs-lookup"><span data-stu-id="039e4-219">This code file passes hello configuration parameters from your Azure Active Directory portal tooPassport.js.</span></span> <span data-ttu-id="039e4-220">U hebt deze configuratiewaarden gemaakt wanneer u API Hallo-toohello webportal toegevoegd in de eerste deel Hallo Hallo stapsgewijze kennismaking.</span><span class="sxs-lookup"><span data-stu-id="039e4-220">You created these configuration values when you added hello web API toohello portal in hello first part of hello walkthrough.</span></span> <span data-ttu-id="039e4-221">We uitleggen welke tooput Hallo waarden van deze parameters wanneer u Hallo code hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="039e4-221">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

1. <span data-ttu-id="039e4-222">Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="039e4-222">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="039e4-223">Maak een `config.js` bestand in uw favoriete editor en voeg vervolgens Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="039e4-223">Create a `config.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. <span data-ttu-id="039e4-224">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="039e4-224">Save hello file.</span></span>

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a><span data-ttu-id="039e4-225">Stap 12: Waarden tooyour server.js configuratiebestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="039e4-225">Step 12: Add configuration values tooyour server.js file</span></span>
<span data-ttu-id="039e4-226">We moeten deze waarden van Hallo .config-bestand dat u hebt gemaakt tooread via onze toepassing.</span><span class="sxs-lookup"><span data-stu-id="039e4-226">We need tooread these values from hello .config file that you created across our application.</span></span> <span data-ttu-id="039e4-227">toodo, we Hallo .config-bestand als een vereiste bron in onze toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="039e4-227">toodo this, we add hello .config file as a required resource in our application.</span></span> <span data-ttu-id="039e4-228">We Stel Hallo globale variabelen toomatch Hallo variabelen in Hallo config.js document.</span><span class="sxs-lookup"><span data-stu-id="039e4-228">Then we set hello global variables toomatch hello variables in hello config.js document.</span></span>

1. <span data-ttu-id="039e4-229">Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="039e4-229">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="039e4-230">Open uw `server.js` bestand in uw favoriete editor en voeg vervolgens Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="039e4-230">Open your `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="039e4-231">Voeg een nieuwe sectie te`server.js` Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="039e4-231">Then add a new section too`server.js` with hello following code:</span></span>

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="039e4-232">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="039e4-232">Save hello file.</span></span>

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="039e4-233">Stap 13: Hallo MongoDB-Model en de schemagegevens toevoegen met behulp van Mongoose</span><span class="sxs-lookup"><span data-stu-id="039e4-233">Step 13: Add hello MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="039e4-234">Alle deze voorbereiding gaat nu toostart betaalt uitschakelen als we deze drie bestanden in een REST-API-service combineren.</span><span class="sxs-lookup"><span data-stu-id="039e4-234">Now all this preparation is going toostart paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="039e4-235">Voor dit scenario we gebruiken MongoDB toostore onze taken, zoals beschreven in stap 4.</span><span class="sxs-lookup"><span data-stu-id="039e4-235">For this walkthrough, we use MongoDB toostore our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="039e4-236">In Hallo `config.js` bestand dat wordt gemaakt in stap 11, we onze database aangeroepen `tasklist`, omdat die was we plaatsen aan Hallo einde van onze **mogoose_auth_local** verbindings-URL.</span><span class="sxs-lookup"><span data-stu-id="039e4-236">In hello `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at hello end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="039e4-237">U hoeft niet toocreate deze vooraf in MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="039e4-237">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="039e4-238">In plaats daarvan maakt MongoDB dit voor ons op Hallo eerst het uitvoeren van de servertoepassing (ervan uitgaande dat Hallo de database nog niet bestaat).</span><span class="sxs-lookup"><span data-stu-id="039e4-238">Instead, MongoDB creates this for us on hello first run of our server application (assuming that hello database doesn't already exist).</span></span>

<span data-ttu-id="039e4-239">Nu we hebben Hallo server u welke MongoDB-database verteld willen we graag toouse, moeten we toowrite enkele aanvullende code toocreate Hallo model en het schema voor onze server taken.</span><span class="sxs-lookup"><span data-stu-id="039e4-239">Now that we've told hello server which MongoDB database we'd like toouse, we need toowrite some additional code toocreate hello model and schema for our server's tasks.</span></span>

### <a name="discussion-of-hello-model"></a><span data-ttu-id="039e4-240">Beschrijving van de Hallo-model</span><span class="sxs-lookup"><span data-stu-id="039e4-240">Discussion of hello model</span></span>
<span data-ttu-id="039e4-241">Onze schemamodel is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="039e4-241">Our schema model is simple.</span></span> <span data-ttu-id="039e4-242">U uitbreiden het naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="039e4-242">You expand it as required.</span></span>

<span data-ttu-id="039e4-243">NAAM: naam van Hallo van Hallo persoon die toohello taak is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="039e4-243">NAME: hello name of hello person who is assigned toohello task.</span></span> <span data-ttu-id="039e4-244">Een **tekenreeks**.</span><span class="sxs-lookup"><span data-stu-id="039e4-244">A **String**.</span></span>

<span data-ttu-id="039e4-245">TAAK: Hallo taak zelf.</span><span class="sxs-lookup"><span data-stu-id="039e4-245">TASK: hello task itself.</span></span> <span data-ttu-id="039e4-246">Een **tekenreeks**.</span><span class="sxs-lookup"><span data-stu-id="039e4-246">A **String**.</span></span>

<span data-ttu-id="039e4-247">DATUM: Hallo datum die taak Hallo vervalt.</span><span class="sxs-lookup"><span data-stu-id="039e4-247">DATE: hello date that hello task is due.</span></span> <span data-ttu-id="039e4-248">EEN **DATETIME**.</span><span class="sxs-lookup"><span data-stu-id="039e4-248">A **DATETIME**.</span></span>

<span data-ttu-id="039e4-249">VOLTOOID: Als Hallo-taak is voltooid of niet.</span><span class="sxs-lookup"><span data-stu-id="039e4-249">COMPLETED: If hello task has been completed or not.</span></span> <span data-ttu-id="039e4-250">EEN **BOOLEAANSE**.</span><span class="sxs-lookup"><span data-stu-id="039e4-250">A **BOOLEAN**.</span></span>

### <a name="creating-hello-schema-in-hello-code"></a><span data-ttu-id="039e4-251">Hallo-schema maken in Hallo code</span><span class="sxs-lookup"><span data-stu-id="039e4-251">Creating hello schema in hello code</span></span>
1. <span data-ttu-id="039e4-252">Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="039e4-252">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="039e4-253">Open uw `server.js` bestand in uw favoriete editor en voeg vervolgens de volgende informatie hieronder configuratievermelding Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="039e4-253">Open your `server.js` file in your favorite editor, and then add hello following information below hello configuration entry:</span></span>

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="039e4-254">Zoals u vanuit Hallo code ziet, maken we onze schema eerst.</span><span class="sxs-lookup"><span data-stu-id="039e4-254">As you can tell from hello code, we create our schema first.</span></span> <span data-ttu-id="039e4-255">Vervolgens we een modelobject dat we toostore onze gegevens in de gehele Hallo code maken wanneer we definiëren gebruiken onze **Routes**.</span><span class="sxs-lookup"><span data-stu-id="039e4-255">Then we create a model object that we use toostore our data throughout hello code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="039e4-256">Step 14: Onze routes toevoegen voor onze REST-API-taakserver</span><span class="sxs-lookup"><span data-stu-id="039e4-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="039e4-257">Nu we hebben een database model toowork met, gaan we toevoegen Hallo routes we gaan gebruiken voor onze REST-API-server zijn.</span><span class="sxs-lookup"><span data-stu-id="039e4-257">Now that we have a database model toowork with, let's add hello routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="039e4-258">Routes in Restify</span><span class="sxs-lookup"><span data-stu-id="039e4-258">About routes in Restify</span></span>
<span data-ttu-id="039e4-259">Routes werken in Restify Hallo dezelfde manier ze in Hallo Express stack.</span><span class="sxs-lookup"><span data-stu-id="039e4-259">Routes work in Restify hello same way they do in hello Express stack.</span></span> <span data-ttu-id="039e4-260">U definieert routes met behulp van Hallo URI dat u Hallo client toepassingen toocall verwacht.</span><span class="sxs-lookup"><span data-stu-id="039e4-260">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="039e4-261">Meestal kunt definiëren u uw routes in een afzonderlijk bestand.</span><span class="sxs-lookup"><span data-stu-id="039e4-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="039e4-262">Wij gebruiken we onze routes in Hallo server.js-bestand geplaatst.</span><span class="sxs-lookup"><span data-stu-id="039e4-262">For our purposes, we put our routes in hello server.js file.</span></span> <span data-ttu-id="039e4-263">Het is raadzaam dat u rekening te houden deze routes in een eigen bestand voor gebruik in productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="039e4-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="039e4-264">Een doorsnee patroon voor een Restify-route is als volgt:</span><span class="sxs-lookup"><span data-stu-id="039e4-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="039e4-265">Dit is Hallo patroon op het meest eenvoudige niveau.</span><span class="sxs-lookup"><span data-stu-id="039e4-265">This is hello pattern at its most basic level.</span></span> <span data-ttu-id="039e4-266">Restify (en Express) bieden veel diepere functionaliteit, zoals het definiëren van toepassingstypen en het geven van complexe routering tussen verschillende eindpunten.</span><span class="sxs-lookup"><span data-stu-id="039e4-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="039e4-267">Voor onze toepassing, zijn we deze routes eenvoudig houden.</span><span class="sxs-lookup"><span data-stu-id="039e4-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-tooour-server"></a><span data-ttu-id="039e4-268">Standaard routes tooour server toevoegen</span><span class="sxs-lookup"><span data-stu-id="039e4-268">Add default routes tooour server</span></span>
<span data-ttu-id="039e4-269">We nu toevoegen Hallo eenvoudige CRUD-routes voor het maken, ophalen, bijwerken en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="039e4-269">We now add hello basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="039e4-270">Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er:</span><span class="sxs-lookup"><span data-stu-id="039e4-270">From hello command line, change directories toohello **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="039e4-271">Open Hallo `server.js` bestand in uw favoriete editor en voeg vervolgens Hallo informatie hieronder Hallo vorige items in de database die u hebt aangebracht na:</span><span class="sxs-lookup"><span data-stu-id="039e4-271">Open hello `server.js` file in your favorite editor, and then add hello following information below hello previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="039e4-272">Fout tijdens verwerken van in onze API's toevoegen</span><span class="sxs-lookup"><span data-stu-id="039e4-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="039e4-273">Stap 15: De server maken</span><span class="sxs-lookup"><span data-stu-id="039e4-273">Step 15: Create your server</span></span>
<span data-ttu-id="039e4-274">We hebben onze database gedefinieerd en onze routes aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="039e4-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="039e4-275">het laatste wat toodo Hallo is Hallo server-exemplaar dat onze aanroepen beheert toevoegen.</span><span class="sxs-lookup"><span data-stu-id="039e4-275">hello last thing toodo is add hello server instance that manages our calls.</span></span>

<span data-ttu-id="039e4-276">In Restify (en Express) kunt u een groot aantal aanpassing voor een REST-API-server uitvoeren, maar opnieuw gaan we toouse Hallo meest eenvoudige configuratie voor onze toepassing.</span><span class="sxs-lookup"><span data-stu-id="039e4-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going toouse hello most basic setup for our purposes.</span></span>

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a><span data-ttu-id="039e4-277">Stap 16: Hallo routes toohello server (zonder verificatie nu) toevoegen</span><span class="sxs-lookup"><span data-stu-id="039e4-277">Step 16: Add hello routes toohello server (without authentication for now)</span></span>
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a><span data-ttu-id="039e4-278">Stap 17: Voer Hallo-server (voordat het OAuth-ondersteuning toe te voegen)</span><span class="sxs-lookup"><span data-stu-id="039e4-278">Step 17: Run hello server (before adding OAuth support)</span></span>
<span data-ttu-id="039e4-279">Testen van uw server voordat we verificatie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="039e4-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="039e4-280">de eenvoudigste manier tootest Hallo uw server is curl gebruikt in een opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="039e4-280">hello easiest way tootest your server is by using curl in a command line.</span></span> <span data-ttu-id="039e4-281">Voordat we dat doen, moeten we een hulpprogramma waarmee we tooparse uitvoer als JSON.</span><span class="sxs-lookup"><span data-stu-id="039e4-281">Before we do that, we need a utility that allows us tooparse output as JSON.</span></span>

1. <span data-ttu-id="039e4-282">Hallo volgende JSON-hulpprogramma (alle Hallo volgen voorbeelden Gebruik dit hulpprogramma) installeren:</span><span class="sxs-lookup"><span data-stu-id="039e4-282">Install hello following JSON tool (all hello following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="039e4-283">Hiermee installeert globaal Hallo JSON-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="039e4-283">This installs hello JSON tool globally.</span></span> <span data-ttu-id="039e4-284">Nu dat we dat hebt gedaan, gaat spelen met Hallo-server:</span><span class="sxs-lookup"><span data-stu-id="039e4-284">Now that we’ve accomplished that, let’s play with hello server:</span></span>

2. <span data-ttu-id="039e4-285">Controleer eerst of dat het mongoDB-exemplaar wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="039e4-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="039e4-286">Vervolgens wijzigen toohello directory en start curling:</span><span class="sxs-lookup"><span data-stu-id="039e4-286">Then, change toohello directory and start curling:</span></span>

    <span data-ttu-id="039e4-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="039e4-287">`$ cd azuread` `$ node server.js`</span></span>

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. <span data-ttu-id="039e4-288">Vervolgens kunt we toevoegen een taak op deze manier:</span><span class="sxs-lookup"><span data-stu-id="039e4-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="039e4-289">Hallo-antwoord moet zijn:</span><span class="sxs-lookup"><span data-stu-id="039e4-289">hello response should be:</span></span>

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
    <span data-ttu-id="039e4-290">En we kunnen een lijst met taken voor Brandon op deze manier:</span><span class="sxs-lookup"><span data-stu-id="039e4-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="039e4-291">Als alle dit werkt, we klaar tooadd OAuth toohello REST-API-server.</span><span class="sxs-lookup"><span data-stu-id="039e4-291">If all this works, we're ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="039e4-292">U hebt een REST-API-server met MongoDB!</span><span class="sxs-lookup"><span data-stu-id="039e4-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-tooour-rest-api-server"></a><span data-ttu-id="039e4-293">Stap 18: Authentication tooour REST-API-server toevoegen</span><span class="sxs-lookup"><span data-stu-id="039e4-293">Step 18: Add authentication tooour REST API server</span></span>
<span data-ttu-id="039e4-294">Nu dat we een actieve REST-API hebben, begint het van groot belang met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="039e4-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="039e4-295">Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="039e4-295">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="039e4-296">Hallo OIDCBearerStrategy die is opgenomen in passport-azure-ad gebruiken</span><span class="sxs-lookup"><span data-stu-id="039e4-296">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="039e4-297">Tot nu toe hebben we een typische REST-TODO-server zonder enige vorm van autorisatie gebouwd.</span><span class="sxs-lookup"><span data-stu-id="039e4-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="039e4-298">Dit is waar u begint het samenstellen.</span><span class="sxs-lookup"><span data-stu-id="039e4-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="039e4-299">We moeten eerst tooindicate willen we toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="039e4-299">First, we need tooindicate that we want toouse Passport.</span></span> <span data-ttu-id="039e4-300">Dit recht na de andere serverconfiguratie genomen:</span><span class="sxs-lookup"><span data-stu-id="039e4-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="039e4-301">Wanneer u schrijft API's, het is raadzaam dat u altijd Hallo gegevens toosomething uniek in vergelijking met het Hallo-token dat Hallo gebruiker koppelt niet kunnen vervalsen.</span><span class="sxs-lookup"><span data-stu-id="039e4-301">When you write APIs, we recommend that you always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="039e4-302">Wanneer deze server TODO-items opslaat, slaat deze op basis van Hallo object-ID van gebruiker in de Hallo in Hallo-token (aangeroepen via token.oid), die we in Hallo 'eigenaar' veld plaatsen.</span><span class="sxs-lookup"><span data-stu-id="039e4-302">When this server stores TODO items, it stores them based on hello object ID of hello user in hello token (called through token.oid), which we put in hello “owner” field.</span></span> <span data-ttu-id="039e4-303">Dit zorgt ervoor dat alleen die gebruiker toegang heeft tot hun TODOs.</span><span class="sxs-lookup"><span data-stu-id="039e4-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="039e4-304">Er is geen blootstelling in Hallo API van de 'eigenaar' zodat een externe gebruiker Hallo TODOs van anderen aanvragen kan, zelfs als ze zijn geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="039e4-304">There is no exposure in hello API of “owner,” so an external user can request hello TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="039e4-305">Volgende we gebruiken Hallo bearer-strategie die wordt geleverd met `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="039e4-305">Next let’s use hello bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="039e4-306">Bekijkt hello code nu en wordt uitgelegd Hallo rest binnenkort.</span><span class="sxs-lookup"><span data-stu-id="039e4-306">Look at hello code for now and we'll explain hello rest shortly.</span></span> <span data-ttu-id="039e4-307">Plaats deze achter u hebt geplakt hierboven:</span><span class="sxs-lookup"><span data-stu-id="039e4-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

<span data-ttu-id="039e4-308">Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort) die alle schrijvers van strategieën voor.</span><span class="sxs-lookup"><span data-stu-id="039e4-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="039e4-309">Hallo-strategie bekijkt, ziet u geven we een functie die een token en een gereed heeft als Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="039e4-309">Looking at hello strategy, you see we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="039e4-310">Hallo-strategie komt weer toous nadat deze zijn werk doet.</span><span class="sxs-lookup"><span data-stu-id="039e4-310">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="039e4-311">Nadat het geval is, Hallo gebruiker en opgeslagen stash Hallo token zodat we niet opnieuw tooask voor het opnieuw hoeft.</span><span class="sxs-lookup"><span data-stu-id="039e4-311">After it does, we store hello user and stash hello token so we won’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="039e4-312">Hallo vorige code wordt elke gebruiker die tooauthenticate tooour server plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="039e4-312">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="039e4-313">Dit wordt automatische registratie genoemd.</span><span class="sxs-lookup"><span data-stu-id="039e4-313">This is known as auto-registration.</span></span> <span data-ttu-id="039e4-314">In productieservers doorlopen u die wordt aangeraden dat u niet toestaan dat iedereen zonder dat zij eerst een registratieproces die u kiest.</span><span class="sxs-lookup"><span data-stu-id="039e4-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="039e4-315">Dit is meestal Hallo patroon dat u ziet in consumenten-apps, die vervolgens vraagt u toofill aanvullende informatie, maar kunnen u tooregister met Facebook.</span><span class="sxs-lookup"><span data-stu-id="039e4-315">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="039e4-316">Als dit niet een opdrachtregelprogramma, kan hebben we Hallo e opgehaald uit Hallo Tokenobject dat wordt geretourneerd en wordt vervolgens gevraagd Hallo gebruiker toofill aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="039e4-316">If this wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="039e4-317">Omdat dit een testserver, we gewoon ze toohello in-memory database toevoegen.</span><span class="sxs-lookup"><span data-stu-id="039e4-317">Because this is a test server, we simply add them toohello in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="039e4-318">Sommige eindpunten beveiligen</span><span class="sxs-lookup"><span data-stu-id="039e4-318">Protect some endpoints</span></span>
<span data-ttu-id="039e4-319">U beveiligt de eindpunten door te geven Hallo `passport.authenticate()` aanroep met het Hallo-protocol dat u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="039e4-319">You protect endpoints by specifying hello `passport.authenticate()` call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="039e4-320">onze servercode doen iets meer interessante toomake Hallo route Hiermee kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="039e4-320">toomake our server code do something more interesting, let’s edit hello route.</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="039e4-321">Stap 19: De servertoepassing opnieuw uitvoeren en zorg ervoor dat u wordt geweigerd</span><span class="sxs-lookup"><span data-stu-id="039e4-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="039e4-322">We gebruiken `curl` opnieuw toosee als we nu OAuth2-bescherming tegen onze eindpunten.</span><span class="sxs-lookup"><span data-stu-id="039e4-322">Let's use `curl` again toosee if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="039e4-323">We doen deze test voordat u een van onze client-SDK's met dit eindpunt uitvoert.</span><span class="sxs-lookup"><span data-stu-id="039e4-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="039e4-324">Hallo headers die worden geretourneerd moeten voldoende tootell ons als gaan we omlaag rechts Hallo-pad.</span><span class="sxs-lookup"><span data-stu-id="039e4-324">hello headers that are returned should be enough tootell us if we're going down hello right path.</span></span>

1. <span data-ttu-id="039e4-325">Controleer eerst of dat het mongoDB-exemplaar wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="039e4-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="039e4-326">Vervolgens wijzigen toohello directory en start curling.</span><span class="sxs-lookup"><span data-stu-id="039e4-326">Then, change toohello directory and start curling.</span></span>

      <span data-ttu-id="039e4-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="039e4-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="039e4-328">Probeer een basic POST.</span><span class="sxs-lookup"><span data-stu-id="039e4-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="039e4-329">Een 401 is Hallo-reactie die u hier zoekt.</span><span class="sxs-lookup"><span data-stu-id="039e4-329">A 401 is hello response you are looking for here.</span></span> <span data-ttu-id="039e4-330">Dit antwoord geeft aan dat Hallo Passport-laag probeert tooredirect toohello geautoriseerd eindpunt, is precies wat u wilt.</span><span class="sxs-lookup"><span data-stu-id="039e4-330">This response indicates that hello Passport layer is trying tooredirect toohello authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="039e4-331">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="039e4-331">Next steps</span></span>
<span data-ttu-id="039e4-332">U bent gegaan zo ver mogelijk kunt u met deze server zonder met behulp van een OAuth2-compatibele client.</span><span class="sxs-lookup"><span data-stu-id="039e4-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="039e4-333">U moet toogo via een extra scenario.</span><span class="sxs-lookup"><span data-stu-id="039e4-333">You will need toogo through an additional walkthrough.</span></span>

<span data-ttu-id="039e4-334">U hebt nu geleerd hoe tooimplement een REST-API met behulp van Restify en OAuth2.</span><span class="sxs-lookup"><span data-stu-id="039e4-334">You've now learned how tooimplement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="039e4-335">Hebt u ook meer dan voldoende code tookeep uw service ontwikkelen en te leren hoe toobuild op dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="039e4-335">You also have more than enough code tookeep developing your service and learning how toobuild on this example.</span></span>

<span data-ttu-id="039e4-336">Als u geïnteresseerd in de volgende stappen Hallo in uw ADAL reis bent, vindt hier u enkele ondersteunde ADAL clients het is raadzaam dat u met blijven werken.</span><span class="sxs-lookup"><span data-stu-id="039e4-336">If you are interested in hello next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="039e4-337">Omlaag tooyour developer machine klonen en configureren zoals beschreven in het Hallo-scenario.</span><span class="sxs-lookup"><span data-stu-id="039e4-337">Clone down tooyour developer machine and configure as described in hello walkthrough.</span></span>

[<span data-ttu-id="039e4-338">ADAL voor iOS</span><span class="sxs-lookup"><span data-stu-id="039e4-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="039e4-339">ADAL voor Android</span><span class="sxs-lookup"><span data-stu-id="039e4-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
