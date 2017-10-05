---
title: Azure AD-Node.js aan de slag | Microsoft Docs
description: "Het bouwen van een REST Node.js-web-API die kan worden geïntegreerd met Azure AD voor verificatie."
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
ms.openlocfilehash: 4f58177f540c14172d7ece8b4bc8c8a2b9787f8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="76a6b-103">Aan de slag met web-API's voor Node.js</span><span class="sxs-lookup"><span data-stu-id="76a6b-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="76a6b-104">*Passport* is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="76a6b-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="76a6b-105">Flexibel en modulair, Passport kan worden onopvallend verwijderd voor een Express- of Restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="76a6b-105">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="76a6b-106">Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.</span><span class="sxs-lookup"><span data-stu-id="76a6b-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="76a6b-107">We hebben een strategie ontwikkeld voor Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76a6b-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="76a6b-108">We installeert deze module en voegt u de Microsoft Azure Active Directory `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="76a6b-108">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="76a6b-109">Hiervoor doet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="76a6b-109">To do this, you need to:</span></span>

1. <span data-ttu-id="76a6b-110">U registreert een toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76a6b-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="76a6b-111">Uw app instellen voor het gebruik van de Passport `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="76a6b-111">Set up your app to use Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="76a6b-112">Configureer een clienttoepassing de takenlijst-web-API niet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-112">Configure a client application to call the To Do List web API.</span></span>

<span data-ttu-id="76a6b-113">De code voor deze zelfstudie wordt onderhouden in [GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="76a6b-113">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="76a6b-114">In dit artikel dekt niet het implementeren van aanmelding, registratie en Profielbeheer met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="76a6b-114">This article doesn't cover how to implement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="76a6b-115">Dit artikel gaat over het aanroepen van web API's nadat de gebruiker al is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="76a6b-115">It focuses on calling web APIs after the user is already authenticated.</span></span>  <span data-ttu-id="76a6b-116">Het is raadzaam dat u met begint [integreren met Azure Active Directory-document](active-directory-how-to-integrate.md) voor meer informatie over de basisprincipes van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="76a6b-116">We recommend that you start with [How to integrate with Azure Active Directory document](active-directory-how-to-integrate.md) to learn about the basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="76a6b-117">We de broncode bijvoorbeeld uitgevoerd in GitHub onder een MIT-licentie hebt gepubliceerd, dus kloon (of zelfs beter fork) gerust en feedback geven en pull-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-117">We've released all the source code for this running example in GitHub under an MIT license, so feel free to clone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="76a6b-118">Over Node.js-modules</span><span class="sxs-lookup"><span data-stu-id="76a6b-118">About Node.js modules</span></span>
<span data-ttu-id="76a6b-119">We Node.js-modules gebruiken in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="76a6b-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="76a6b-120">Modules zijn geladen JavaScript-pakketten die specifieke functionaliteit voor uw toepassing bieden.</span><span class="sxs-lookup"><span data-stu-id="76a6b-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="76a6b-121">U kunt gewoonlijk modules installeren met behulp van de Node.js een opdrachtregelprogramma NPM in de NPM-installatiemap.</span><span class="sxs-lookup"><span data-stu-id="76a6b-121">You usually install modules by using the Node.js an NPM command-line tool in the NPM installation directory.</span></span> <span data-ttu-id="76a6b-122">Sommige modules, zoals de HTTP-module worden echter opgenomen in het core Node.js-pakket.</span><span class="sxs-lookup"><span data-stu-id="76a6b-122">However, some modules, such as the HTTP module, are included in the core Node.js package.</span></span>

<span data-ttu-id="76a6b-123">Geïnstalleerde modules worden opgeslagen in de **node_modules** map in de hoofdmap van uw Node.js-installatiemap.</span><span class="sxs-lookup"><span data-stu-id="76a6b-123">Installed modules are saved in the **node_modules** directory at the root of your Node.js installation directory.</span></span> <span data-ttu-id="76a6b-124">Elke module in de **node_modules** directory onderhoudt een eigen **node_modules** map waarin zich geen modules die afhankelijk zijn van.</span><span class="sxs-lookup"><span data-stu-id="76a6b-124">Each module in the **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="76a6b-125">Ook elke vereiste module heeft een **node_modules** directory.</span><span class="sxs-lookup"><span data-stu-id="76a6b-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="76a6b-126">Deze directory recursieve structuur vertegenwoordigt de afhankelijkheidsketen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-126">This recursive directory structure represents the dependency chain.</span></span>

<span data-ttu-id="76a6b-127">Deze structuur van de keten afhankelijkheid resulteert in een grotere toepassing footprint.</span><span class="sxs-lookup"><span data-stu-id="76a6b-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="76a6b-128">Maar ook wordt hiermee gegarandeerd dat alle afhankelijkheden is voldaan en de versie van de modules die wordt gebruikt in ontwikkeling wordt ook gebruikt in productie.</span><span class="sxs-lookup"><span data-stu-id="76a6b-128">But it also guarantees that all dependencies are met and that the version of the modules that's used in development is also used in production.</span></span> <span data-ttu-id="76a6b-129">Hierdoor wordt het gedrag van de app productie beter voorspelbaar en voorkomt dat versioning problemen die gevolgen voor gebruikers hebben mogelijk.</span><span class="sxs-lookup"><span data-stu-id="76a6b-129">This makes the production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="76a6b-130">Stap 1: Een Azure AD-tenant registreren</span><span class="sxs-lookup"><span data-stu-id="76a6b-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="76a6b-131">Dit voorbeeld gebruiken, moet u een Azure Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="76a6b-131">To use this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="76a6b-132">Als u niet zeker weet welke tenant krijgen, raadpleegt u [een Azure AD-tenant verkrijgen](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="76a6b-132">If you're not sure what a tenant is or how to get one, see [How to get an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="76a6b-133">Stap 2: Een toepassing maken</span><span class="sxs-lookup"><span data-stu-id="76a6b-133">Step 2: Create an application</span></span>
<span data-ttu-id="76a6b-134">Vervolgens maakt u een app in uw directory waarmee informatie over het Azure AD die nodig zijn voor het veilig te communiceren met uw app.</span><span class="sxs-lookup"><span data-stu-id="76a6b-134">Next you create an app in your directory that gives Azure AD information that it needs to securely communicate with your app.</span></span>  <span data-ttu-id="76a6b-135">De client-app en de web-API worden aangegeven met één **toepassings-ID** in dit geval omdat ze samen één logische app vormen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-135">Both the client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="76a6b-136">Volg [deze instructies](active-directory-how-applications-are-added.md) om een app te maken.</span><span class="sxs-lookup"><span data-stu-id="76a6b-136">To create an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="76a6b-137">Als u een line-of-business-app bouwt [deze aanvullende instructies nuttig kunnen zijn](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="76a6b-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="76a6b-138">Een toepassing maken:</span><span class="sxs-lookup"><span data-stu-id="76a6b-138">To create an application:</span></span>

1. <span data-ttu-id="76a6b-139">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="76a6b-139">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="76a6b-140">Selecteer in het bovenste menu uw account.</span><span class="sxs-lookup"><span data-stu-id="76a6b-140">On the top menu, select your account.</span></span> <span data-ttu-id="76a6b-141">Klik vervolgens onder de **Directory** kiest u de Active Directory-tenant waar u uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="76a6b-141">Then, under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="76a6b-142">Selecteer in het menu aan de linkerkant **meer Services**, en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="76a6b-142">In the menu on the left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="76a6b-143">Selecteer **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="76a6b-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="76a6b-144">Volg de aanwijzingen voor het maken van een **webtoepassing en/of WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="76a6b-144">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="76a6b-145">De **naam** beschrijving van de toepassing van uw toepassing aan eindgebruikers.</span><span class="sxs-lookup"><span data-stu-id="76a6b-145">The **name** of the application describes your application to end users.</span></span>

      * <span data-ttu-id="76a6b-146">De **aanmeldings-URL** is de basis-URL van uw app.</span><span class="sxs-lookup"><span data-stu-id="76a6b-146">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="76a6b-147">Is de standaard-URL van de voorbeeldcode `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="76a6b-147">The default URL of the sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="76a6b-148">Nadat u hebt geregistreerd, wijst Azure AD uw app een unieke id</span><span class="sxs-lookup"><span data-stu-id="76a6b-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="76a6b-149">U moet deze waarde in de volgende secties, dus kopiëren van de toepassingspagina.</span><span class="sxs-lookup"><span data-stu-id="76a6b-149">You need this value in the next sections, so copy it from the application page.</span></span>

7. <span data-ttu-id="76a6b-150">Van de **instellingen** -> **eigenschappen** pagina voor uw toepassing, het bijwerken van de App ID URI.</span><span class="sxs-lookup"><span data-stu-id="76a6b-150">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="76a6b-151">De **App ID URI** is de unieke id voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="76a6b-151">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="76a6b-152">De overeenkomst is met `https://<tenant-domain>/<app-name>`, bijvoorbeeld: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="76a6b-152">The convention is to use `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="76a6b-153">Maak een **sleutel** voor uw toepassing uit de **instellingen** pagina en kopieer het ergens.</span><span class="sxs-lookup"><span data-stu-id="76a6b-153">Create a **Key** for your application from the **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="76a6b-154">U moet deze binnenkort.</span><span class="sxs-lookup"><span data-stu-id="76a6b-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="76a6b-155">Stap 3: Node.js voor uw platform downloaden</span><span class="sxs-lookup"><span data-stu-id="76a6b-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="76a6b-156">U moet een werkende implementatie van Node.js hebben om dit voorbeeld te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76a6b-156">To successfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="76a6b-157">Installeer Node.js vanuit [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="76a6b-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="76a6b-158">Stap 4: Installatie MongoDB op uw platform</span><span class="sxs-lookup"><span data-stu-id="76a6b-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="76a6b-159">Om te kunnen gebruiken in dit voorbeeld, moet u een werkende implementatie van MongoDB hebben.</span><span class="sxs-lookup"><span data-stu-id="76a6b-159">To successfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="76a6b-160">U gebruikt MongoDB om de REST-API persistent ervoor in alle serverexemplaren.</span><span class="sxs-lookup"><span data-stu-id="76a6b-160">You use MongoDB to make the REST API persistent across server instances.</span></span>

<span data-ttu-id="76a6b-161">Installeer MongoDB vanuit [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="76a6b-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="76a6b-162">In dit scenario wordt ervan uitgegaan dat u de standaard- en -servereindpunten voor MongoDB, die op het moment van schrijven van dit mongodb://localhost is.</span><span class="sxs-lookup"><span data-stu-id="76a6b-162">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="76a6b-163">Stap 5: De Restify-modules installeren in uw web-API</span><span class="sxs-lookup"><span data-stu-id="76a6b-163">Step 5: Install the Restify modules in your web API</span></span>
<span data-ttu-id="76a6b-164">We Restify gebruiken voor het bouwen van de REST-API.</span><span class="sxs-lookup"><span data-stu-id="76a6b-164">We are using Restify to build our REST API.</span></span> <span data-ttu-id="76a6b-165">Restify is een minimaal en flexibel Node.js-toepassingsframework dat afgeleid van Express.</span><span class="sxs-lookup"><span data-stu-id="76a6b-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="76a6b-166">Het bevat een set krachtige functies voor het ontwikkelen van REST-API's op Connect.</span><span class="sxs-lookup"><span data-stu-id="76a6b-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="76a6b-167">Restify installeren</span><span class="sxs-lookup"><span data-stu-id="76a6b-167">Install Restify</span></span>
1. <span data-ttu-id="76a6b-168">Vanaf de opdrachtregel, wijzig de mappen op de **azuread** directory.</span><span class="sxs-lookup"><span data-stu-id="76a6b-168">From the command line, change directories to the **azuread** directory.</span></span> <span data-ttu-id="76a6b-169">Als de **azuread** directory niet bestaat, maakt.</span><span class="sxs-lookup"><span data-stu-id="76a6b-169">If the **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="76a6b-170">Typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="76a6b-170">Type the following command:</span></span>

    `npm install restify`

    <span data-ttu-id="76a6b-171">Met deze opdracht wordt Restify geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="76a6b-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="76a6b-172">Krijgt u een foutmelding?</span><span class="sxs-lookup"><span data-stu-id="76a6b-172">Did you get an error?</span></span>
<span data-ttu-id="76a6b-173">Wanneer u NPM op sommige besturingssystemen gebruikt, wordt u er een foutmelding waarin wordt gemeld **fout: EPERM, type chmod ' / usr/lokale/bin /...'**</span><span class="sxs-lookup"><span data-stu-id="76a6b-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="76a6b-174">en een suggestie die u probeert het account uitvoeren als beheerder.</span><span class="sxs-lookup"><span data-stu-id="76a6b-174">and a suggestion that you try running the account as an administrator.</span></span> <span data-ttu-id="76a6b-175">Als dit het geval is, moet u de sudo-opdracht gebruiken NPM op een hoger niveau van bevoegdheden wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="76a6b-175">If this occurs, use the sudo command to run NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="76a6b-176">Krijgt u een fout met betrekking tot DTRACE?</span><span class="sxs-lookup"><span data-stu-id="76a6b-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="76a6b-177">U ziet een fout als volgt wanneer u Restify installeert:</span><span class="sxs-lookup"><span data-stu-id="76a6b-177">You might see an error like this when installing Restify:</span></span>

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
<span data-ttu-id="76a6b-178">Restify biedt een krachtig mechanisme om REST-aanroepen te traceren met behulp van DTrace.</span><span class="sxs-lookup"><span data-stu-id="76a6b-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="76a6b-179">Veel besturingssystemen hoeft echter geen DTrace.</span><span class="sxs-lookup"><span data-stu-id="76a6b-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="76a6b-180">U kunt deze fouten negeren.</span><span class="sxs-lookup"><span data-stu-id="76a6b-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="76a6b-181">De uitvoer van deze opdracht moet er ongeveer als de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="76a6b-181">The output of this command should look similar to the following output:</span></span>

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


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="76a6b-182">Stap 6: Installatie Passport.js in uw web-API</span><span class="sxs-lookup"><span data-stu-id="76a6b-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="76a6b-183">[Passport](http://passportjs.org/) is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="76a6b-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="76a6b-184">Flexibel en modulair, Passport kan worden onopvallend verwijderd voor een Express- of Restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="76a6b-184">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="76a6b-185">Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.</span><span class="sxs-lookup"><span data-stu-id="76a6b-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="76a6b-186">We hebben een strategie ontwikkeld voor Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="76a6b-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="76a6b-187">We installeert deze module en voeg vervolgens de invoegtoepassing van de strategie voor Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="76a6b-187">We install this module and then add the Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="76a6b-188">Vanaf de opdrachtregel, wijzig de mappen op de **azuread** directory.</span><span class="sxs-lookup"><span data-stu-id="76a6b-188">From the command line, change directories to the **azuread** directory.</span></span>

2. <span data-ttu-id="76a6b-189">Als u wilt installeren passport.js, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="76a6b-189">To install passport.js, enter the following command :</span></span>

    `npm install passport`

    <span data-ttu-id="76a6b-190">De uitvoer van de opdracht moet er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="76a6b-190">The output of the command should look similar to the following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="76a6b-191">Stap 7: Passport-Azure-AD toevoegen aan uw web-API</span><span class="sxs-lookup"><span data-stu-id="76a6b-191">Step 7: Add Passport-Azure-AD to your web API</span></span>
<span data-ttu-id="76a6b-192">Vervolgens wordt de OAuth-strategie toevoegen met behulp van `passport-azure-ad`, een reeks strategieën die Azure Active Directory met Passport verbinden.</span><span class="sxs-lookup"><span data-stu-id="76a6b-192">Next we add the OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory to Passport.</span></span> <span data-ttu-id="76a6b-193">We gebruiken deze strategie voor bearer-tokens in dit voorbeeld REST-API.</span><span class="sxs-lookup"><span data-stu-id="76a6b-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="76a6b-194">Hoewel OAuth2 een kader waarin elk onbekend type token kan worden uitgegeven, worden alleen bepaalde typen worden vaak gebruikt.</span><span class="sxs-lookup"><span data-stu-id="76a6b-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="76a6b-195">Bearer-tokens zijn de meest gebruikte tokens voor het beveiligen van eindpunten.</span><span class="sxs-lookup"><span data-stu-id="76a6b-195">Bearer tokens are the most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="76a6b-196">Ze zijn het meest wordt uitgegeven token in OAuth2-type.</span><span class="sxs-lookup"><span data-stu-id="76a6b-196">They are the most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="76a6b-197">Veel implementaties wordt ervan uitgegaan dat bearer-tokens het enige type tokens die zijn uitgegeven zijn.</span><span class="sxs-lookup"><span data-stu-id="76a6b-197">Many implementations assume that bearer tokens are the only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="76a6b-198">Vanaf de opdrachtregel, wijzig de mappen op de **azuread** directory.</span><span class="sxs-lookup"><span data-stu-id="76a6b-198">From the command line, change directories to the **azuread** directory.</span></span>

<span data-ttu-id="76a6b-199">Typ de volgende opdracht voor het installeren van de Passport.js `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="76a6b-199">Type the following command to install the Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="76a6b-200">De uitvoer van de opdracht moet er ongeveer als de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="76a6b-200">The output of the command should look similar to the following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="76a6b-201">Stap 8: MongoDB-modules toevoegen aan uw web-API</span><span class="sxs-lookup"><span data-stu-id="76a6b-201">Step 8: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="76a6b-202">We gebruikt MongoDB als onze gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="76a6b-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="76a6b-203">Daarom moeten we de veelgebruikte invoegtoepassing aangeroepen Mongoose voor het beheren van modellen en schema's te installeren.</span><span class="sxs-lookup"><span data-stu-id="76a6b-203">For that reason, we need to install the widely used plug-in called Mongoose to manage models and schemas.</span></span> <span data-ttu-id="76a6b-204">Ook moet het databasestuurprogramma voor MongoDB (dit wordt ook MongoDB genoemd) te installeren.</span><span class="sxs-lookup"><span data-stu-id="76a6b-204">We also need to install the database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="76a6b-205">Stap 9: Aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="76a6b-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="76a6b-206">Vervolgens wordt de overige vereiste modules installeren.</span><span class="sxs-lookup"><span data-stu-id="76a6b-206">Next we install the remaining required modules.</span></span>

1. <span data-ttu-id="76a6b-207">Vanaf de opdrachtregel, wijzig de mappen op de **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="76a6b-207">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="76a6b-208">Voer de volgende opdrachten voor het installeren van deze modules in uw **node_modules** directory:</span><span class="sxs-lookup"><span data-stu-id="76a6b-208">Enter the following commands to install these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="76a6b-209">Stap 10: Een server.js met de afhankelijkheden maken</span><span class="sxs-lookup"><span data-stu-id="76a6b-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="76a6b-210">Het bestand server.js bevat de meeste van de functionaliteit voor onze web API-server.</span><span class="sxs-lookup"><span data-stu-id="76a6b-210">The server.js file provides most of the functionality for our web API server.</span></span> <span data-ttu-id="76a6b-211">We de meeste code toevoegen aan dit bestand.</span><span class="sxs-lookup"><span data-stu-id="76a6b-211">We add most of our code to this file.</span></span> <span data-ttu-id="76a6b-212">Voor productiedoeleinden, is het raadzaam dat u de functionaliteit in kleinere bestanden, zoals afzonderlijke routes en controllers opsplitsen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-212">For production purposes, we recommend that you refactor the functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="76a6b-213">In deze demonstratie gebruiken we server.js voor deze functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="76a6b-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="76a6b-214">Vanaf de opdrachtregel, wijzig de mappen op de **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="76a6b-214">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="76a6b-215">Maak een `server.js` bestand in uw favoriete editor en voeg vervolgens de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="76a6b-215">Create a `server.js` file in your favorite editor, and then add the following information:</span></span>

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

3. <span data-ttu-id="76a6b-216">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="76a6b-216">Save the file.</span></span> <span data-ttu-id="76a6b-217">We keert kort terug naar deze.</span><span class="sxs-lookup"><span data-stu-id="76a6b-217">We'll return to it shortly.</span></span>

## <a name="step-11-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="76a6b-218">Stap 11: Maak een configuratiebestand voor het opslaan van uw Azure AD-instellingen</span><span class="sxs-lookup"><span data-stu-id="76a6b-218">Step 11: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="76a6b-219">Dit codebestand geeft de configuratieparameters van uw Azure Active Directory-portal aan Passport.js.</span><span class="sxs-lookup"><span data-stu-id="76a6b-219">This code file passes the configuration parameters from your Azure Active Directory portal to Passport.js.</span></span> <span data-ttu-id="76a6b-220">U hebt deze configuratiewaarden gemaakt toen u de web-API toegevoegd aan de portal in het eerste deel van de procedure.</span><span class="sxs-lookup"><span data-stu-id="76a6b-220">You created these configuration values when you added the web API to the portal in the first part of the walkthrough.</span></span> <span data-ttu-id="76a6b-221">Wanneer u de code hebt gekopieerd, wordt uitgelegd wat u in de waarden van deze parameters moet zetten.</span><span class="sxs-lookup"><span data-stu-id="76a6b-221">We explain what to put in the values of these parameters after you copy the code.</span></span>

1. <span data-ttu-id="76a6b-222">Vanaf de opdrachtregel, wijzig de mappen op de **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="76a6b-222">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="76a6b-223">Maak een `config.js` bestand in uw favoriete editor en voeg vervolgens de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="76a6b-223">Create a `config.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in to your server unless you use the common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in to your server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes to stderr in Unix.

         };
    ```
3. <span data-ttu-id="76a6b-224">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="76a6b-224">Save the file.</span></span>

## <a name="step-12-add-configuration-values-to-your-serverjs-file"></a><span data-ttu-id="76a6b-225">Stap 12: Configuratiewaarden toevoegen aan het bestand server.js</span><span class="sxs-lookup"><span data-stu-id="76a6b-225">Step 12: Add configuration values to your server.js file</span></span>
<span data-ttu-id="76a6b-226">We moeten deze waarden lezen uit het .config-bestand dat u hebt gemaakt in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="76a6b-226">We need to read these values from the .config file that you created across our application.</span></span> <span data-ttu-id="76a6b-227">U doet dit door toevoegen we het .config-bestand als een vereiste bron in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="76a6b-227">To do this, we add the .config file as a required resource in our application.</span></span> <span data-ttu-id="76a6b-228">Vervolgens stelt u de globale variabelen moeten overeenkomen met de variabelen in het bestand config.js-document.</span><span class="sxs-lookup"><span data-stu-id="76a6b-228">Then we set the global variables to match the variables in the config.js document.</span></span>

1. <span data-ttu-id="76a6b-229">Vanaf de opdrachtregel, wijzig de mappen op de **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="76a6b-229">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="76a6b-230">Open uw `server.js` bestand in uw favoriete editor en voeg vervolgens de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="76a6b-230">Open your `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="76a6b-231">Voeg een nieuwe rubriek voor `server.js` met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="76a6b-231">Then add a new section to `server.js` with the following code:</span></span>

    ```Javascript
    var options = {
        // The URL of the metadata document for your app. We will put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array to hold logged in users and the current logged in user (owner).
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

      // If the logging level is specified, switch to it.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="76a6b-232">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="76a6b-232">Save the file.</span></span>

## <a name="step-13-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="76a6b-233">Stap 13: De MongoDB-Model en de schemagegevens toevoegen met behulp van Mongoose</span><span class="sxs-lookup"><span data-stu-id="76a6b-233">Step 13: Add The MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="76a6b-234">Alle deze voorbereiding gaat nu gaan betalen uitschakelen als we deze drie bestanden in een REST-API-service combineren.</span><span class="sxs-lookup"><span data-stu-id="76a6b-234">Now all this preparation is going to start paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="76a6b-235">Voor dit scenario we MongoDB gebruiken voor het opslaan van onze taken, zoals beschreven in stap 4.</span><span class="sxs-lookup"><span data-stu-id="76a6b-235">For this walkthrough, we use MongoDB to store our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="76a6b-236">In de `config.js` bestand dat wordt gemaakt in stap 11, we onze database aangeroepen `tasklist`, omdat die was we plaatsen aan het einde van onze **mogoose_auth_local** verbindings-URL.</span><span class="sxs-lookup"><span data-stu-id="76a6b-236">In the `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at the end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="76a6b-237">U hoeft deze database niet vooraf in MongoDB te maken.</span><span class="sxs-lookup"><span data-stu-id="76a6b-237">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="76a6b-238">In plaats daarvan maakt MongoDB dit voor ons op de eerste uitvoering van onze servertoepassing (ervan uitgaande dat de database nog niet bestaat).</span><span class="sxs-lookup"><span data-stu-id="76a6b-238">Instead, MongoDB creates this for us on the first run of our server application (assuming that the database doesn't already exist).</span></span>

<span data-ttu-id="76a6b-239">Nu we hebben u de server verteld welke MongoDB-database die we wilt gebruiken, moet er aanvullende code schrijven om het model en het schema voor onze server taken maken.</span><span class="sxs-lookup"><span data-stu-id="76a6b-239">Now that we've told the server which MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's tasks.</span></span>

### <a name="discussion-of-the-model"></a><span data-ttu-id="76a6b-240">Beschrijving van het model</span><span class="sxs-lookup"><span data-stu-id="76a6b-240">Discussion of the model</span></span>
<span data-ttu-id="76a6b-241">Onze schemamodel is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="76a6b-241">Our schema model is simple.</span></span> <span data-ttu-id="76a6b-242">U uitbreiden het naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="76a6b-242">You expand it as required.</span></span>

<span data-ttu-id="76a6b-243">NAAM: De naam van de persoon die is toegewezen aan de taak.</span><span class="sxs-lookup"><span data-stu-id="76a6b-243">NAME: The name of the person who is assigned to the task.</span></span> <span data-ttu-id="76a6b-244">Een **tekenreeks**.</span><span class="sxs-lookup"><span data-stu-id="76a6b-244">A **String**.</span></span>

<span data-ttu-id="76a6b-245">TAAK: De taak zelf.</span><span class="sxs-lookup"><span data-stu-id="76a6b-245">TASK: The task itself.</span></span> <span data-ttu-id="76a6b-246">Een **tekenreeks**.</span><span class="sxs-lookup"><span data-stu-id="76a6b-246">A **String**.</span></span>

<span data-ttu-id="76a6b-247">DATUM: De datum waarop de taak moet voltooid zijn.</span><span class="sxs-lookup"><span data-stu-id="76a6b-247">DATE: The date that the task is due.</span></span> <span data-ttu-id="76a6b-248">EEN **DATETIME**.</span><span class="sxs-lookup"><span data-stu-id="76a6b-248">A **DATETIME**.</span></span>

<span data-ttu-id="76a6b-249">VOLTOOID: Als de taak is voltooid of niet.</span><span class="sxs-lookup"><span data-stu-id="76a6b-249">COMPLETED: If the task has been completed or not.</span></span> <span data-ttu-id="76a6b-250">EEN **BOOLEAANSE**.</span><span class="sxs-lookup"><span data-stu-id="76a6b-250">A **BOOLEAN**.</span></span>

### <a name="creating-the-schema-in-the-code"></a><span data-ttu-id="76a6b-251">Het schema maken in de code</span><span class="sxs-lookup"><span data-stu-id="76a6b-251">Creating the schema in the code</span></span>
1. <span data-ttu-id="76a6b-252">Vanaf de opdrachtregel, wijzig de mappen op de **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="76a6b-252">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="76a6b-253">Open uw `server.js` bestand in uw favoriete editor en voeg vervolgens de volgende informatie onder het configuratie-item:</span><span class="sxs-lookup"><span data-stu-id="76a6b-253">Open your `server.js` file in your favorite editor, and then add the following information below the configuration entry:</span></span>

    ```Javascript
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema to store our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="76a6b-254">Zoals u van de code ziet, maken we onze schema eerst.</span><span class="sxs-lookup"><span data-stu-id="76a6b-254">As you can tell from the code, we create our schema first.</span></span> <span data-ttu-id="76a6b-255">Vervolgens we een modelobject dat we gebruiken maken voor het opslaan van onze gegevens in de code bij we definiëren onze **Routes**.</span><span class="sxs-lookup"><span data-stu-id="76a6b-255">Then we create a model object that we use to store our data throughout the code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="76a6b-256">Step 14: Onze routes toevoegen voor onze REST-API-taakserver</span><span class="sxs-lookup"><span data-stu-id="76a6b-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="76a6b-257">Nu we hebben een databasemodel werken met, gaan we toevoegen de routes die we gaan gebruiken voor onze REST-API-server.</span><span class="sxs-lookup"><span data-stu-id="76a6b-257">Now that we have a database model to work with, let's add the routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="76a6b-258">Routes in Restify</span><span class="sxs-lookup"><span data-stu-id="76a6b-258">About routes in Restify</span></span>
<span data-ttu-id="76a6b-259">Routes werken in Restify op dezelfde manier als ze doen in de Express-stack.</span><span class="sxs-lookup"><span data-stu-id="76a6b-259">Routes work in Restify the same way they do in the Express stack.</span></span> <span data-ttu-id="76a6b-260">U definieert routes met behulp van de URI die de clienttoepassingen aanroepen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-260">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="76a6b-261">Meestal kunt definiëren u uw routes in een afzonderlijk bestand.</span><span class="sxs-lookup"><span data-stu-id="76a6b-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="76a6b-262">Wij gebruiken we onze routes in het server.js-bestand geplaatst.</span><span class="sxs-lookup"><span data-stu-id="76a6b-262">For our purposes, we put our routes in the server.js file.</span></span> <span data-ttu-id="76a6b-263">Het is raadzaam dat u rekening te houden deze routes in een eigen bestand voor gebruik in productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="76a6b-264">Een doorsnee patroon voor een Restify-route is als volgt:</span><span class="sxs-lookup"><span data-stu-id="76a6b-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep the server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="76a6b-265">Dit is het patroon op het meest eenvoudige niveau.</span><span class="sxs-lookup"><span data-stu-id="76a6b-265">This is the pattern at its most basic level.</span></span> <span data-ttu-id="76a6b-266">Restify (en Express) bieden veel diepere functionaliteit, zoals het definiëren van toepassingstypen en het geven van complexe routering tussen verschillende eindpunten.</span><span class="sxs-lookup"><span data-stu-id="76a6b-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="76a6b-267">Voor onze toepassing, zijn we deze routes eenvoudig houden.</span><span class="sxs-lookup"><span data-stu-id="76a6b-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-to-our-server"></a><span data-ttu-id="76a6b-268">Standaardroutes toevoegen aan onze server</span><span class="sxs-lookup"><span data-stu-id="76a6b-268">Add default routes to our server</span></span>
<span data-ttu-id="76a6b-269">We nu toevoegen de eenvoudige CRUD-routes van maken, ophalen, bijwerken en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-269">We now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="76a6b-270">Vanaf de opdrachtregel, wijzig de mappen op de **azuread** map als u niet al er:</span><span class="sxs-lookup"><span data-stu-id="76a6b-270">From the command line, change directories to the **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="76a6b-271">Open de `server.js` bestand in uw favoriete editor en voeg vervolgens de volgende informatie onder de vorige databasevermeldingen die u hebt aangebracht:</span><span class="sxs-lookup"><span data-stu-id="76a6b-271">Open the `server.js` file in your favorite editor, and then add the following information below the previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it to Mongodb.
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

/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

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
            log.warn(err, "There is no tasks in the database. Did you initialize the database as stated in the README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="76a6b-272">Fout tijdens verwerken van in onze API's toevoegen</span><span class="sxs-lookup"><span data-stu-id="76a6b-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back to the client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="76a6b-273">Stap 15: De server maken</span><span class="sxs-lookup"><span data-stu-id="76a6b-273">Step 15: Create your server</span></span>
<span data-ttu-id="76a6b-274">We hebben onze database gedefinieerd en onze routes aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="76a6b-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="76a6b-275">Het laatste wat te doen is het toevoegen van het serverexemplaar waarmee onze aanroepen worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="76a6b-275">The last thing to do is add the server instance that manages our calls.</span></span>

<span data-ttu-id="76a6b-276">In Restify (en Express) kunt u een groot aantal aanpassing voor een REST-API-server uitvoeren, maar we gaan opnieuw de meest eenvoudige configuratie gebruiken voor onze doeleinden.</span><span class="sxs-lookup"><span data-stu-id="76a6b-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going to use the most basic setup for our purposes.</span></span>

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

// Allow five requests per second by IP, and burst to 10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping to REST.
```

## <a name="step-16-add-the-routes-to-the-server-without-authentication-for-now"></a><span data-ttu-id="76a6b-277">Stap 16: De routes toevoegen aan de server (zonder verificatie nu)</span><span class="sxs-lookup"><span data-stu-id="76a6b-277">Step 16: Add the routes to the server (without authentication for now)</span></span>
```Javascript
/// Now the real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In the pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need to maintain session state. You can experiment with removing API protection
/* by removing the passport.authenticate() method as follows:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-the-server-before-adding-oauth-support"></a><span data-ttu-id="76a6b-278">Stap 17: Uitvoering van de server (vóór het OAuth-ondersteuning toe te voegen)</span><span class="sxs-lookup"><span data-stu-id="76a6b-278">Step 17: Run the server (before adding OAuth support)</span></span>
<span data-ttu-id="76a6b-279">Testen van uw server voordat we verificatie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="76a6b-280">Er is de eenvoudigste manier om uw server testen met behulp van curl in een opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="76a6b-280">The easiest way to test your server is by using curl in a command line.</span></span> <span data-ttu-id="76a6b-281">Voordat we dat doen, moeten we een hulpprogramma waarmee we uitvoer kunt parseren als JSON.</span><span class="sxs-lookup"><span data-stu-id="76a6b-281">Before we do that, we need a utility that allows us to parse output as JSON.</span></span>

1. <span data-ttu-id="76a6b-282">Installeer de volgende JSON-hulpprogramma (dit hulpprogramma gebruiken in de volgende voorbeelden):</span><span class="sxs-lookup"><span data-stu-id="76a6b-282">Install the following JSON tool (all the following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="76a6b-283">Hiermee wordt het JSON-hulpprogramma op alle vereiste locaties geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="76a6b-283">This installs the JSON tool globally.</span></span> <span data-ttu-id="76a6b-284">Nu dat we dat hebt gedaan, gaan we afspelen met de server:</span><span class="sxs-lookup"><span data-stu-id="76a6b-284">Now that we’ve accomplished that, let’s play with the server:</span></span>

2. <span data-ttu-id="76a6b-285">Controleer eerst of dat het mongoDB-exemplaar wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="76a6b-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="76a6b-286">Vervolgens wijzigen naar de map en start curling:</span><span class="sxs-lookup"><span data-stu-id="76a6b-286">Then, change to the directory and start curling:</span></span>

    <span data-ttu-id="76a6b-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="76a6b-287">`$ cd azuread` `$ node server.js`</span></span>

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

4. <span data-ttu-id="76a6b-288">Vervolgens kunt we toevoegen een taak op deze manier:</span><span class="sxs-lookup"><span data-stu-id="76a6b-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="76a6b-289">Het antwoord moet zijn:</span><span class="sxs-lookup"><span data-stu-id="76a6b-289">The response should be:</span></span>

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
    <span data-ttu-id="76a6b-290">En we kunnen een lijst met taken voor Brandon op deze manier:</span><span class="sxs-lookup"><span data-stu-id="76a6b-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="76a6b-291">Als alle dit werkt, kunt u OAuth toevoegen aan de REST-API-server.</span><span class="sxs-lookup"><span data-stu-id="76a6b-291">If all this works, we're ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="76a6b-292">U hebt een REST-API-server met MongoDB!</span><span class="sxs-lookup"><span data-stu-id="76a6b-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-to-our-rest-api-server"></a><span data-ttu-id="76a6b-293">Stap 18: Verificatie toevoegen aan onze REST-API-server</span><span class="sxs-lookup"><span data-stu-id="76a6b-293">Step 18: Add authentication to our REST API server</span></span>
<span data-ttu-id="76a6b-294">Nu dat we een actieve REST-API hebben, begint het van groot belang met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76a6b-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="76a6b-295">Vanaf de opdrachtregel, wijzig de mappen op de **azuread** map als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="76a6b-295">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="76a6b-296">De OIDCBearerStrategy gebruiken die is opgenomen in passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="76a6b-296">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="76a6b-297">Tot nu toe hebben we een typische REST-TODO-server zonder enige vorm van autorisatie gebouwd.</span><span class="sxs-lookup"><span data-stu-id="76a6b-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="76a6b-298">Dit is waar u begint het samenstellen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="76a6b-299">Eerst moet aangeven dat we Passport wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76a6b-299">First, we need to indicate that we want to use Passport.</span></span> <span data-ttu-id="76a6b-300">Dit recht na de andere serverconfiguratie genomen:</span><span class="sxs-lookup"><span data-stu-id="76a6b-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="76a6b-301">Wanneer u API's schrijft, wordt u aangeraden altijd de gegevens koppelen aan een unieke van het token dat de gebruiker niet kan vervalsen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-301">When you write APIs, we recommend that you always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="76a6b-302">Wanneer deze server TODO-items opslaat, slaat deze op basis van de object-ID van de gebruiker in het token (aangeroepen via token.oid), die we in het veld 'eigenaar' plaatsen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-302">When this server stores TODO items, it stores them based on the object ID of the user in the token (called through token.oid), which we put in the “owner” field.</span></span> <span data-ttu-id="76a6b-303">Dit zorgt ervoor dat alleen die gebruiker toegang heeft tot hun TODOs.</span><span class="sxs-lookup"><span data-stu-id="76a6b-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="76a6b-304">Er is geen blootstelling in de 'eigenaar'-API zodat een externe gebruiker de TODOs van anderen aanvragen kan, zelfs als ze zijn geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="76a6b-304">There is no exposure in the API of “owner,” so an external user can request the TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="76a6b-305">Volgende we gebruiken de bearer-strategie die wordt geleverd met `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="76a6b-305">Next let’s use the bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="76a6b-306">Bekijk de code nu en wordt de rest kort uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="76a6b-306">Look at the code for now and we'll explain the rest shortly.</span></span> <span data-ttu-id="76a6b-307">Plaats deze achter u hebt geplakt hierboven:</span><span class="sxs-lookup"><span data-stu-id="76a6b-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling the OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides the need to manage users and info tokens
    /* with a FindorCreate() method that must be provided by the implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want to do something smarter.
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
            log.info('verifying the user');
            log.info(token, 'was the token retreived');
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

<span data-ttu-id="76a6b-308">Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort) die alle schrijvers van strategieën voor.</span><span class="sxs-lookup"><span data-stu-id="76a6b-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="76a6b-309">De strategie bekijkt, ziet u geven we een functie die een token en een gereed als parameters heeft.</span><span class="sxs-lookup"><span data-stu-id="76a6b-309">Looking at the strategy, you see we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="76a6b-310">De strategie komt weer naar ons nadat deze zijn werk doet.</span><span class="sxs-lookup"><span data-stu-id="76a6b-310">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="76a6b-311">Nadat het geval is, we opslaan van de gebruiker en het token niet initialiseren zodat we niet opnieuw hoeft te vragen voor het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="76a6b-311">After it does, we store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76a6b-312">De vorige code wordt elke gebruiker die plaatsvindt om te verifiëren met onze server.</span><span class="sxs-lookup"><span data-stu-id="76a6b-312">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="76a6b-313">Dit wordt automatische registratie genoemd.</span><span class="sxs-lookup"><span data-stu-id="76a6b-313">This is known as auto-registration.</span></span> <span data-ttu-id="76a6b-314">In productieservers doorlopen u die wordt aangeraden dat u niet toestaan dat iedereen zonder dat zij eerst een registratieproces die u kiest.</span><span class="sxs-lookup"><span data-stu-id="76a6b-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="76a6b-315">Dit is doorgaans het patroon die u ziet in consumenten-apps, waarmee u kunt registreren met Facebook, maar vervolgens vraagt u om aanvullende informatie in te vullen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-315">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="76a6b-316">Als dit niet een opdrachtregelprogramma, kan hebben we het e-mailbericht opgehaald uit het Tokenobject dat wordt geretourneerd en wordt vervolgens gevraagd de gebruiker om aanvullende informatie in te vullen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-316">If this wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="76a6b-317">Omdat dit een testserver is, voegen we deze gewoon toe aan de database in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-317">Because this is a test server, we simply add them to the in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="76a6b-318">Sommige eindpunten beveiligen</span><span class="sxs-lookup"><span data-stu-id="76a6b-318">Protect some endpoints</span></span>
<span data-ttu-id="76a6b-319">U beveiligt de eindpunten door te geven de `passport.authenticate()` aanroepen met het protocol dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76a6b-319">You protect endpoints by specifying the `passport.authenticate()` call with the protocol that you want to use.</span></span>

<span data-ttu-id="76a6b-320">Als u ons servercode iets interessanters te doen, gaan we de route voor bewerken.</span><span class="sxs-lookup"><span data-stu-id="76a6b-320">To make our server code do something more interesting, let’s edit the route.</span></span>

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

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="76a6b-321">Stap 19: De servertoepassing opnieuw uitvoeren en zorg ervoor dat u wordt geweigerd</span><span class="sxs-lookup"><span data-stu-id="76a6b-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="76a6b-322">We gebruiken `curl` opnieuw uit om te controleren of we nu OAuth2-bescherming tegen onze eindpunten.</span><span class="sxs-lookup"><span data-stu-id="76a6b-322">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="76a6b-323">We doen deze test voordat u een van onze client-SDK's met dit eindpunt uitvoert.</span><span class="sxs-lookup"><span data-stu-id="76a6b-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="76a6b-324">De geretourneerde headers moeten voldoende om ons te laten als gaan we u het juiste pad.</span><span class="sxs-lookup"><span data-stu-id="76a6b-324">The headers that are returned should be enough to tell us if we're going down the right path.</span></span>

1. <span data-ttu-id="76a6b-325">Controleer eerst of dat het mongoDB-exemplaar wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="76a6b-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="76a6b-326">Vervolgens wijzigen naar de map en start curling.</span><span class="sxs-lookup"><span data-stu-id="76a6b-326">Then, change to the directory and start curling.</span></span>

      <span data-ttu-id="76a6b-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="76a6b-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="76a6b-328">Probeer een basic POST.</span><span class="sxs-lookup"><span data-stu-id="76a6b-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="76a6b-329">Een 401 is de reactie die u hier zoekt.</span><span class="sxs-lookup"><span data-stu-id="76a6b-329">A 401 is the response you are looking for here.</span></span> <span data-ttu-id="76a6b-330">Dit antwoord geeft aan dat de Passport-laag probeert omleiden naar het geautoriseerde eindpunt, is precies wat u wilt.</span><span class="sxs-lookup"><span data-stu-id="76a6b-330">This response indicates that the Passport layer is trying to redirect to the authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76a6b-331">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76a6b-331">Next steps</span></span>
<span data-ttu-id="76a6b-332">U bent gegaan zo ver mogelijk kunt u met deze server zonder met behulp van een OAuth2-compatibele client.</span><span class="sxs-lookup"><span data-stu-id="76a6b-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="76a6b-333">U moet een extra scenario doorlopen.</span><span class="sxs-lookup"><span data-stu-id="76a6b-333">You will need to go through an additional walkthrough.</span></span>

<span data-ttu-id="76a6b-334">U hebt nu geleerd hoe u een REST-API implementeert met Restify en OAuth2.</span><span class="sxs-lookup"><span data-stu-id="76a6b-334">You've now learned how to implement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="76a6b-335">Hebt u ook meer dan voldoende code te houden voor het ontwikkelen van uw service en leren hoe u kunt in dit voorbeeld is opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="76a6b-335">You also have more than enough code to keep developing your service and learning how to build on this example.</span></span>

<span data-ttu-id="76a6b-336">Als u geïnteresseerd in de volgende stappen in de ADAL reis bent, vindt hier u enkele ondersteunde ADAL clients het is raadzaam dat u met blijven werken.</span><span class="sxs-lookup"><span data-stu-id="76a6b-336">If you are interested in the next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="76a6b-337">Klonen naar beneden op uw machine ontwikkelaars en configureren zoals beschreven in deze stapsgewijze kennismaking.</span><span class="sxs-lookup"><span data-stu-id="76a6b-337">Clone down to your developer machine and configure as described in the walkthrough.</span></span>

[<span data-ttu-id="76a6b-338">ADAL voor iOS</span><span class="sxs-lookup"><span data-stu-id="76a6b-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="76a6b-339">ADAL voor Android</span><span class="sxs-lookup"><span data-stu-id="76a6b-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
