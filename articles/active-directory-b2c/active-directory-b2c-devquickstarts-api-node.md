---
title: 'Azure AD B2C: Een web-API beveiligen met behulp van Node.js | Microsoft Docs'
description: Een Node.js web-API ontwikkelen die tokens accepteert van een B2C-tenant
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
ms.openlocfilehash: 6480be75c314ede1b786e959a79c0385dd2edea8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="95f42-103">Azure AD B2C: Een web-API ontwikkelen met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="95f42-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="95f42-104">Met Azure Active Directory (Azure AD) B2C kunt u een web-API beveiligen met OAuth 2.0-toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="95f42-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="95f42-105">Met deze tokens kunnen client-apps die gebruikmaken van Azure AD B2C, worden geverifieerd bij de API.</span><span class="sxs-lookup"><span data-stu-id="95f42-105">These tokens allow your client apps that use Azure AD B2C to authenticate to the API.</span></span> <span data-ttu-id="95f42-106">In dit artikel wordt uitgelegd hoe u een takenlijst-API maakt, waarmee gebruikers taken kunnen toevoegen en vermelden.</span><span class="sxs-lookup"><span data-stu-id="95f42-106">This article shows you how to create a "to-do list" API that allows users to add and list tasks.</span></span> <span data-ttu-id="95f42-107">De web-API is beveiligd met Azure AD B2C en biedt geverifieerde gebruikers alleen de mogelijkheid om hun takenlijst te beheren.</span><span class="sxs-lookup"><span data-stu-id="95f42-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="95f42-108">Dit voorbeeld is bedoeld voor gebruik met de [iOS B2C-voorbeeldtoepassing](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="95f42-108">This sample was written to be connected to by using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="95f42-109">Voer eerst deze procedure uit en volg daarna dat voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="95f42-109">Do the current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="95f42-110">**Passport** is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="95f42-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="95f42-111">Passport is flexibel en modulair, en kan onopvallend worden geïnstalleerd in een Express- of Restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="95f42-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="95f42-112">Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.</span><span class="sxs-lookup"><span data-stu-id="95f42-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="95f42-113">We hebben een strategie ontwikkeld voor Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="95f42-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="95f42-114">U installeert deze module en voegt vervolgens de `passport-azure-ad`-invoegtoepassing van Azure AD toe.</span><span class="sxs-lookup"><span data-stu-id="95f42-114">You install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="95f42-115">Hiervoor doet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="95f42-115">To do this sample, you need to:</span></span>

1. <span data-ttu-id="95f42-116">U registreert een toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95f42-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="95f42-117">U stelt de toepassing in voor het gebruik van de Passport-invoegtoepassing van `azure-ad-passport`.</span><span class="sxs-lookup"><span data-stu-id="95f42-117">Set up your application to use Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="95f42-118">U configureert een client om de web-API 'takenlijst' aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="95f42-118">Configure a client application to call the "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="95f42-119">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="95f42-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="95f42-120">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="95f42-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="95f42-121">Een directory is een container voor alle gebruikers, apps, groepen en meer.</span><span class="sxs-lookup"><span data-stu-id="95f42-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="95f42-122">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u verdergaat.</span><span class="sxs-lookup"><span data-stu-id="95f42-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="95f42-123">Een app maken</span><span class="sxs-lookup"><span data-stu-id="95f42-123">Create an application</span></span>
<span data-ttu-id="95f42-124">Vervolgens moet u in de B2C-directory een app maken die Azure AD de informatie geeft die nodig is om veilig te communiceren met uw app.</span><span class="sxs-lookup"><span data-stu-id="95f42-124">Next, you need to create an app in your B2C directory that gives Azure AD some information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="95f42-125">In dit geval worden zowel de client-app als de web-API vertegenwoordigd door één **toepassings-id** omdat ze samen één logische app vormen.</span><span class="sxs-lookup"><span data-stu-id="95f42-125">In this case, both the client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="95f42-126">Volg [deze instructies](active-directory-b2c-app-registration.md) om een app te maken.</span><span class="sxs-lookup"><span data-stu-id="95f42-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="95f42-127">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="95f42-127">Be sure to:</span></span>

* <span data-ttu-id="95f42-128">U een **web-app of web-API** in de toepassing opneemt.</span><span class="sxs-lookup"><span data-stu-id="95f42-128">Include a **web app/web api** in the application</span></span>
* <span data-ttu-id="95f42-129">U `http://localhost/TodoListService` invoert als **antwoord-URL**.</span><span class="sxs-lookup"><span data-stu-id="95f42-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="95f42-130">Dit is de standaard-URL voor dit codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="95f42-130">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="95f42-131">U een **toepassingsgeheim** maakt voor uw toepassing en dit kopieert.</span><span class="sxs-lookup"><span data-stu-id="95f42-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="95f42-132">U hebt deze gegevens later nodig.</span><span class="sxs-lookup"><span data-stu-id="95f42-132">You need this data later.</span></span> <span data-ttu-id="95f42-133">Deze waarde moet [een escape-teken voor XML](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) bevatten voordat u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="95f42-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="95f42-134">U de **toepassings-id** kopieert die is toegewezen aan uw app.</span><span class="sxs-lookup"><span data-stu-id="95f42-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="95f42-135">U hebt deze gegevens later nodig.</span><span class="sxs-lookup"><span data-stu-id="95f42-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="95f42-136">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="95f42-136">Create your policies</span></span>
<span data-ttu-id="95f42-137">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="95f42-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="95f42-138">Deze app bevat twee identiteitservaringen: registreren en aanmelden.</span><span class="sxs-lookup"><span data-stu-id="95f42-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="95f42-139">U moet één beleidsregel maken voor elk type, zoals wordt beschreven in het [naslagartikel voor beleid](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="95f42-139">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="95f42-140">Wanneer u uw drie beleidsregels maakt:</span><span class="sxs-lookup"><span data-stu-id="95f42-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="95f42-141">Kiest u **Weergavenaam** en andere registratiekenmerken in het registratiebeleid.</span><span class="sxs-lookup"><span data-stu-id="95f42-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="95f42-142">Kiest u **Weergavenaam**- en **Object-id**-toepassingsclaims voor elk beleid.</span><span class="sxs-lookup"><span data-stu-id="95f42-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="95f42-143">U kunt ook andere claims kiezen.</span><span class="sxs-lookup"><span data-stu-id="95f42-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="95f42-144">Noteert u de **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="95f42-144">Copy down the **Name** of each policy after you create it.</span></span> <span data-ttu-id="95f42-145">Deze moet het voorvoegsel `b2c_1_` bevatten.</span><span class="sxs-lookup"><span data-stu-id="95f42-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="95f42-146">U hebt deze beleidsnamen later nodig.</span><span class="sxs-lookup"><span data-stu-id="95f42-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="95f42-147">Nadat u de drie beleidsregels hebt gemaakt, kunt u uw app maken.</span><span class="sxs-lookup"><span data-stu-id="95f42-147">After you have created your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="95f42-148">Voor meer informatie over de werking van beleid in Azure AD B2C, leest u eerst de [zelfstudie Aan de slag met .NET-web-app](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="95f42-148">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-the-code"></a><span data-ttu-id="95f42-149">De code downloaden</span><span class="sxs-lookup"><span data-stu-id="95f42-149">Download the code</span></span>
<span data-ttu-id="95f42-150">De code voor deze zelfstudie [wordt bewaard in GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="95f42-150">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="95f42-151">Als u het voorbeeld wilt maken terwijl u aan het werk bent, kunt u [een basisproject downloaden als zip-bestand](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="95f42-151">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="95f42-152">U kunt het basisproject ook klonen:</span><span class="sxs-lookup"><span data-stu-id="95f42-152">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="95f42-153">De voltooide app is ook [beschikbaar als zip-bestand](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) of in de `complete`-vertakking van dezelfde opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="95f42-153">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="95f42-154">Node.js voor uw platform downloaden</span><span class="sxs-lookup"><span data-stu-id="95f42-154">Download Node.js for your platform</span></span>
<span data-ttu-id="95f42-155">U moet een werkende installatie van Node.js hebben om dit voorbeeld te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="95f42-155">To successfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="95f42-156">Installeer Node.js vanuit [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="95f42-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="95f42-157">MongoDB installeren voor uw platform</span><span class="sxs-lookup"><span data-stu-id="95f42-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="95f42-158">U moet een werkende installatie van MongoDB hebben om dit voorbeeld te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="95f42-158">To successfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="95f42-159">U gebruikt MongoDB om uw REST-API permanent te maken in alle serverexemplaren.</span><span class="sxs-lookup"><span data-stu-id="95f42-159">We use MongoDB to make your REST API persistent across server instances.</span></span>

<span data-ttu-id="95f42-160">Installeer MongoDB vanuit [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="95f42-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="95f42-161">In deze procedure wordt ervan uitgegaan dat u gebruikmaakt van de standaardinstallatie- en -servereindpunten voor MongoDB. Op het moment waarop dit artikel is geschreven, zijn dat `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="95f42-161">This walk-through assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="95f42-162">De Restify-modules installeren in uw web-API</span><span class="sxs-lookup"><span data-stu-id="95f42-162">Install the Restify modules in your web API</span></span>
<span data-ttu-id="95f42-163">U gebruikt Restify om de REST-API te ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="95f42-163">We use Restify to build your REST API.</span></span> <span data-ttu-id="95f42-164">Restify is een minimaal en flexibel Node.js-toepassingsframework dat is afgeleid van Express.</span><span class="sxs-lookup"><span data-stu-id="95f42-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="95f42-165">Het bevat een set krachtige functies voor het ontwikkelen van REST-API's op Connect.</span><span class="sxs-lookup"><span data-stu-id="95f42-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="95f42-166">Restify installeren</span><span class="sxs-lookup"><span data-stu-id="95f42-166">Install Restify</span></span>
<span data-ttu-id="95f42-167">Wijzig de directory vanaf de opdrachtregel in `azuread`.</span><span class="sxs-lookup"><span data-stu-id="95f42-167">From the command line, change your directory to `azuread`.</span></span> <span data-ttu-id="95f42-168">Als de directory `azuread` niet bestaat, maakt u deze.</span><span class="sxs-lookup"><span data-stu-id="95f42-168">If the `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="95f42-169">`cd azuread` of `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="95f42-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="95f42-170">Voer de volgende opdracht in:</span><span class="sxs-lookup"><span data-stu-id="95f42-170">Enter the following command:</span></span>

`npm install restify`

<span data-ttu-id="95f42-171">Met deze opdracht wordt Restify geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="95f42-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="95f42-172">Krijgt u een foutmelding?</span><span class="sxs-lookup"><span data-stu-id="95f42-172">Did you get an error?</span></span>
<span data-ttu-id="95f42-173">Wanneer u `npm` in sommige besturingssystemen gebruikt, wordt het foutbericht `Error: EPERM, chmod '/usr/local/bin/..'` weergegeven, plus het verzoek om het account uit te voeren als beheerder.</span><span class="sxs-lookup"><span data-stu-id="95f42-173">In some operating systems, when you use `npm`, you may receive the error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run the account as an administrator.</span></span> <span data-ttu-id="95f42-174">In dat geval gebruikt u de opdracht `sudo` om `npm` uit te voeren op een hoger niveau van bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="95f42-174">If this problem occurs, use the `sudo` command to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="95f42-175">Wordt er een DTrace-fout weergegeven?</span><span class="sxs-lookup"><span data-stu-id="95f42-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="95f42-176">Mogelijk wordt er iets in de trant van het volgende weergegeven wanneer u Restify installeert:</span><span class="sxs-lookup"><span data-stu-id="95f42-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="95f42-177">Restify biedt een krachtig mechanisme om REST-aanroepen te traceren met behulp van DTrace.</span><span class="sxs-lookup"><span data-stu-id="95f42-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="95f42-178">Veel besturingssystemen beschikken echter niet over DTrace.</span><span class="sxs-lookup"><span data-stu-id="95f42-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="95f42-179">U kunt deze fouten negeren.</span><span class="sxs-lookup"><span data-stu-id="95f42-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="95f42-180">De uitvoer van de opdracht ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="95f42-180">The output of the command should appear similar to this text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="95f42-181">Passport installeren in uw web-API</span><span class="sxs-lookup"><span data-stu-id="95f42-181">Install Passport in your web API</span></span>
<span data-ttu-id="95f42-182">Wijzig de directory vanaf de opdrachtregel in `azuread`, als dat nog niet is gebeurd.</span><span class="sxs-lookup"><span data-stu-id="95f42-182">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="95f42-183">Installeer Passport met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="95f42-183">Install Passport using the following command:</span></span>

`npm install passport`

<span data-ttu-id="95f42-184">De uitvoer van de opdracht ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="95f42-184">The output of the command should be similar to this text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-to-your-web-api"></a><span data-ttu-id="95f42-185">Passport-azuread toevoegen aan uw web-API</span><span class="sxs-lookup"><span data-stu-id="95f42-185">Add passport-azuread to your web API</span></span>
<span data-ttu-id="95f42-186">Voeg vervolgens de OAuth-strategie toe met behulp van `passport-azuread`. Dit is een reeks strategieën die Azure AD verbinden met Passport.</span><span class="sxs-lookup"><span data-stu-id="95f42-186">Next, add the OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="95f42-187">Gebruik deze strategie voor bearer-tokens in het REST-API-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="95f42-187">Use this strategy for bearer tokens in the REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="95f42-188">Hoewel OAuth2 een kader biedt waarin elk onbekend type token kan worden uitgegeven, worden alleen bepaalde typen tokens wijdverbreid gebruikt.</span><span class="sxs-lookup"><span data-stu-id="95f42-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="95f42-189">De tokens voor het beveiligen van eindpunten zijn bearer-tokens.</span><span class="sxs-lookup"><span data-stu-id="95f42-189">The tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="95f42-190">Dit is het type token dat het meest wordt uitgegeven in OAuth2.</span><span class="sxs-lookup"><span data-stu-id="95f42-190">These types of tokens are the most widely issued in OAuth2.</span></span> <span data-ttu-id="95f42-191">In veel implementaties wordt ervan uitgegaan dat bearer-tokens het enige type token zijn dat wordt uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="95f42-191">Many implementations assume that bearer tokens are the only type of token issued.</span></span>
>
>

<span data-ttu-id="95f42-192">Wijzig de directory vanaf de opdrachtregel in `azuread`, als dat nog niet is gebeurd.</span><span class="sxs-lookup"><span data-stu-id="95f42-192">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="95f42-193">Voer de volgende opdracht in om de Passport-module `passport-azure-ad` te installeren:</span><span class="sxs-lookup"><span data-stu-id="95f42-193">Install the Passport `passport-azure-ad` module using the following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="95f42-194">De uitvoer van de opdracht ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="95f42-194">The output of the command should be similar to this text:</span></span>

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

## <a name="add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="95f42-195">MongoDB-modules toevoegen aan uw web-API</span><span class="sxs-lookup"><span data-stu-id="95f42-195">Add MongoDB modules to your web API</span></span>
<span data-ttu-id="95f42-196">In dit voorbeeld wordt MongoDB gebruikt als gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="95f42-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="95f42-197">Installeer daarvoor Mongoose, een veel gebruikte invoegtoepassing voor het beheren van modellen en schema’s.</span><span class="sxs-lookup"><span data-stu-id="95f42-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="95f42-198">Aanvullende modules installeren</span><span class="sxs-lookup"><span data-stu-id="95f42-198">Install additional modules</span></span>
<span data-ttu-id="95f42-199">Vervolgens installeert u de overige vereiste modules.</span><span class="sxs-lookup"><span data-stu-id="95f42-199">Next, install the remaining required modules.</span></span>

<span data-ttu-id="95f42-200">Wijzig de directory vanaf de opdrachtregel in `azuread`, als dat nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="95f42-200">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="95f42-201">Installeer de modules in uw `node_modules`-directory:</span><span class="sxs-lookup"><span data-stu-id="95f42-201">Install the modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="95f42-202">Een bestand server.js met de afhankelijkheden maken</span><span class="sxs-lookup"><span data-stu-id="95f42-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="95f42-203">Het bestand `server.js` verstrekt het merendeel van de functionaliteit voor uw web-API-server.</span><span class="sxs-lookup"><span data-stu-id="95f42-203">The `server.js` file provides the majority of the functionality for your Web API server.</span></span>

<span data-ttu-id="95f42-204">Wijzig de directory vanaf de opdrachtregel in `azuread`, als dat nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="95f42-204">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="95f42-205">Maak een bestand `server.js` in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="95f42-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="95f42-206">Voeg de volgende informatie toe:</span><span class="sxs-lookup"><span data-stu-id="95f42-206">Add the following information:</span></span>

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

<span data-ttu-id="95f42-207">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="95f42-207">Save the file.</span></span> <span data-ttu-id="95f42-208">U hebt dit bestand later nodig.</span><span class="sxs-lookup"><span data-stu-id="95f42-208">You return to it later.</span></span>

## <a name="create-a-configjs-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="95f42-209">Een bestand config.js maken om de Azure AD-instellingen op te slaan</span><span class="sxs-lookup"><span data-stu-id="95f42-209">Create a config.js file to store your Azure AD settings</span></span>
<span data-ttu-id="95f42-210">Dit codebestand geeft de configuratieparameters van de Azure AD Portal door aan het bestand `Passport.js`.</span><span class="sxs-lookup"><span data-stu-id="95f42-210">This code file passes the configuration parameters from your Azure AD Portal to the `Passport.js` file.</span></span> <span data-ttu-id="95f42-211">U hebt deze configuratiewaarden gemaakt toen u de web-API aan de portal toevoegde in het eerste deel van de procedure.</span><span class="sxs-lookup"><span data-stu-id="95f42-211">You created these configuration values when you added the web API to the portal in the first part of the walk-through.</span></span> <span data-ttu-id="95f42-212">Wanneer u de code hebt gekopieerd, wordt uitgelegd wat u in de waarden van deze parameters moet zetten.</span><span class="sxs-lookup"><span data-stu-id="95f42-212">We explain what to put in the values of these parameters after you copy the code.</span></span>

<span data-ttu-id="95f42-213">Wijzig de directory vanaf de opdrachtregel in `azuread`, als dat nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="95f42-213">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="95f42-214">Maak een bestand `config.js` in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="95f42-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="95f42-215">Voeg de volgende informatie toe:</span><span class="sxs-lookup"><span data-stu-id="95f42-215">Add the following information:</span></span>

```Javascript
// Don't commit this file to your public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in the portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // the Client ID of the application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add the B2C tenant name in the <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is the policy you'll want to validate against in B2C. Usually this is your Sign-in policy (as users sign in to this API)
passReqToCallback: false // This is a node.js construct that lets you pass the req all the way back to any upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="95f42-216">Vereiste waarden</span><span class="sxs-lookup"><span data-stu-id="95f42-216">Required values</span></span>
<span data-ttu-id="95f42-217">`clientID` : de client-id van uw web-API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="95f42-217">`clientID`: The client ID of your Web API application.</span></span>

<span data-ttu-id="95f42-218">`IdentityMetadata` : dit is de locatie waar `passport-azure-ad` de configuratiegegevens voor de id-provider zoekt.</span><span class="sxs-lookup"><span data-stu-id="95f42-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for the identity provider.</span></span> <span data-ttu-id="95f42-219">Er wordt ook gezocht naar de sleutels om de JSON-webtokens te valideren.</span><span class="sxs-lookup"><span data-stu-id="95f42-219">It also looks for the keys to validate the JSON web tokens.</span></span>

<span data-ttu-id="95f42-220">`audience`: de uniform resource identifier (URI) van de portal die de aanroepende toepassing identificeert.</span><span class="sxs-lookup"><span data-stu-id="95f42-220">`audience`: The uniform resource identifier (URI) from the portal that identifies your calling application.</span></span>

<span data-ttu-id="95f42-221">`tenantName`: de tenantnaam, bijvoorbeeld **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="95f42-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="95f42-222">`policyName`: het beleid waarmee u de tokens wilt valideren die bij de server binnenkomen.</span><span class="sxs-lookup"><span data-stu-id="95f42-222">`policyName`: The policy that you want to validate the tokens coming in to your server.</span></span> <span data-ttu-id="95f42-223">Dit beleid moet hetzelfde zijn als het beleid dat u op de clienttoepassing gebruikt om u aan te melden.</span><span class="sxs-lookup"><span data-stu-id="95f42-223">This policy should be the same policy that you use on the client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="95f42-224">Gebruik nu hetzelfde beleid in de client- en serverconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="95f42-224">For now, use the same policies across both client and server setup.</span></span> <span data-ttu-id="95f42-225">Als u al een procedure hebt doorlopen waarin u deze beleidsregels hebt gemaakt, hoeft u dit niet opnieuw te doen.</span><span class="sxs-lookup"><span data-stu-id="95f42-225">If you have already completed a walk-through and created these policies, you don't need to do so again.</span></span> <span data-ttu-id="95f42-226">Omdat u de procedure hebt voltooid, hoeft u op de site geen nieuw beleid voor clientprocedures te maken.</span><span class="sxs-lookup"><span data-stu-id="95f42-226">Because you completed the walk-through, you shouldn't need to set up new policies for client walk-throughs on the site.</span></span>
>
>

## <a name="add-configuration-to-your-serverjs-file"></a><span data-ttu-id="95f42-227">Configuratie toevoegen aan het bestand server.js</span><span class="sxs-lookup"><span data-stu-id="95f42-227">Add configuration to your server.js file</span></span>
<span data-ttu-id="95f42-228">Als u de waarden wilt lezen van het `config.js`-bestand dat u hebt gemaakt, voegt u het `.config`-bestand als een vereiste resource toe in uw toepassing en stelt u de globale variabelen in op de variabelen in het `config.js`-document.</span><span class="sxs-lookup"><span data-stu-id="95f42-228">To read the values from the `config.js` file you created, add the `.config` file as a required resource in your application, and then set the global variables to those in the `config.js` document.</span></span>

<span data-ttu-id="95f42-229">Wijzig de directory vanaf de opdrachtregel in `azuread`, als dat nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="95f42-229">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="95f42-230">Open het bestand `server.js` in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="95f42-230">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="95f42-231">Voeg de volgende informatie toe:</span><span class="sxs-lookup"><span data-stu-id="95f42-231">Add the following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="95f42-232">Voeg een nieuwe sectie aan `server.js` toe die de volgende code bevat:</span><span class="sxs-lookup"><span data-stu-id="95f42-232">Add a new section to `server.js` that includes the following code:</span></span>

```Javascript
// We pass these options in to the ODICBearerStrategy.

var options = {
    // The URL of the metadata document for your app. We put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="95f42-233">Daarna voegt u tijdelijke aanduidingen toe voor de gebruikers die van de aanroepende toepassingen worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="95f42-233">Next, let's add some placeholders for the users we receive from our calling applications.</span></span>

```Javascript
// array to hold logged in users and the current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="95f42-234">U gaat ook een logger maken.</span><span class="sxs-lookup"><span data-stu-id="95f42-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="95f42-235">Het MongoDB-model en de schemagegevens toevoegen met behulp van Mongoose</span><span class="sxs-lookup"><span data-stu-id="95f42-235">Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="95f42-236">De eerdere voorbereiding loont de moeite wanneer u deze drie bestanden samenbrengt in een REST-API-service.</span><span class="sxs-lookup"><span data-stu-id="95f42-236">The earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="95f42-237">Voor deze procedure gebruikt u MongoDB om uw taken op te slaan, zoals eerder is besproken.</span><span class="sxs-lookup"><span data-stu-id="95f42-237">For this walk-through, use MongoDB to store your tasks, as discussed earlier.</span></span>

<span data-ttu-id="95f42-238">In het bestand `config.js` hebt u de **takenlijst** van uw database aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="95f42-238">In the `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="95f42-239">De naam van de takenlijst is aan het einde van de verbindings-URL van `mongoose_auth_local` geplaatst.</span><span class="sxs-lookup"><span data-stu-id="95f42-239">That name was also what you put at the end of the `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="95f42-240">U hoeft deze database niet vooraf in MongoDB te maken.</span><span class="sxs-lookup"><span data-stu-id="95f42-240">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="95f42-241">De database wordt voor u gemaakt wanneer u de servertoepassing voor de eerste keer uitvoert.</span><span class="sxs-lookup"><span data-stu-id="95f42-241">It creates the database for you on the first run of your server application.</span></span>

<span data-ttu-id="95f42-242">Nadat u de server hebt laten weten welke MongoDB-database u wilt gebruiken, moet u aanvullende code schrijven om het model en het schema voor de servertaken te maken.</span><span class="sxs-lookup"><span data-stu-id="95f42-242">After you tell the server which MongoDB database to use, you need to write some additional code to create the model and schema for your server tasks.</span></span>

### <a name="expand-the-model"></a><span data-ttu-id="95f42-243">Het model uitbreiden</span><span class="sxs-lookup"><span data-stu-id="95f42-243">Expand the model</span></span>
<span data-ttu-id="95f42-244">Dit schemamodel is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="95f42-244">This schema model is simple.</span></span> <span data-ttu-id="95f42-245">U kunt het naar behoefte uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="95f42-245">You can expand it as required.</span></span>

<span data-ttu-id="95f42-246">`owner`: de persoon die aan de taak is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="95f42-246">`owner`: Who is assigned to the task.</span></span> <span data-ttu-id="95f42-247">Dit object is een **tekenreeks**.</span><span class="sxs-lookup"><span data-stu-id="95f42-247">This object is a **string**.</span></span>  

<span data-ttu-id="95f42-248">`Text`: de taak zelf.</span><span class="sxs-lookup"><span data-stu-id="95f42-248">`Text`: The task itself.</span></span> <span data-ttu-id="95f42-249">Dit object is een **tekenreeks**.</span><span class="sxs-lookup"><span data-stu-id="95f42-249">This object is a **string**.</span></span>

<span data-ttu-id="95f42-250">`date`: de datum waarop de taak moet zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="95f42-250">`date`: The date that the task is due.</span></span> <span data-ttu-id="95f42-251">Dit object is een **datum/tijd**.</span><span class="sxs-lookup"><span data-stu-id="95f42-251">This object is a **datetime**.</span></span>

<span data-ttu-id="95f42-252">`completed`: of de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="95f42-252">`completed`: If the task is complete.</span></span> <span data-ttu-id="95f42-253">Dit object is een **Booleaanse waarde**.</span><span class="sxs-lookup"><span data-stu-id="95f42-253">This object is a **Boolean**.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="95f42-254">Het schema in de code maken</span><span class="sxs-lookup"><span data-stu-id="95f42-254">Create the schema in the code</span></span>
<span data-ttu-id="95f42-255">Wijzig de directory vanaf de opdrachtregel in `azuread`, als dat nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="95f42-255">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="95f42-256">Open het bestand `server.js` in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="95f42-256">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="95f42-257">Voeg de volgende informatie toe onder het configuratie-item:</span><span class="sxs-lookup"><span data-stu-id="95f42-257">Add the following information below the configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect to MongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema to store our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use the schema to register a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="95f42-258">Eerst maakt u het schema en vervolgens maakt u een modelobject dat u gebruikt om uw gegevens in de code op te slaan wanneer u de **routes** definieert.</span><span class="sxs-lookup"><span data-stu-id="95f42-258">You first create the schema, and then you create a model object that you use to store your data throughout the code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="95f42-259">Routes toevoegen voor de REST-API-taakserver</span><span class="sxs-lookup"><span data-stu-id="95f42-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="95f42-260">Nu u een databasemodel hebt om mee te werken, voegt u de routes toe die u voor de REST-API-server wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="95f42-260">Now that you have a database model to work with, add the routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="95f42-261">Routes in Restify</span><span class="sxs-lookup"><span data-stu-id="95f42-261">About routes in Restify</span></span>
<span data-ttu-id="95f42-262">Routes werken in Restify op precies dezelfde manier als wanneer ze de Express-stack gebruiken.</span><span class="sxs-lookup"><span data-stu-id="95f42-262">Routes work in Restify in the same way that they work when they use the Express stack.</span></span> <span data-ttu-id="95f42-263">U definieert routes met behulp van de URI die de clienttoepassingen aanroepen.</span><span class="sxs-lookup"><span data-stu-id="95f42-263">You define routes by using the URI that you expect the client applications to call.</span></span>

<span data-ttu-id="95f42-264">Een doorsnee patroon voor een Restify-route is:</span><span class="sxs-lookup"><span data-stu-id="95f42-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep the server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="95f42-265">U kunt Restify en Express gebruiken voor een veel diepere functionaliteit, zoals voor het definiëren van toepassingstypen en de uitvoering van complexe routering tussen verschillende eindpunten.</span><span class="sxs-lookup"><span data-stu-id="95f42-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="95f42-266">Voor deze zelfstudie houden we de routes eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="95f42-266">For the purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="95f42-267">Standaardroutes toevoegen aan een server</span><span class="sxs-lookup"><span data-stu-id="95f42-267">Add default routes to your server</span></span>
<span data-ttu-id="95f42-268">U voegt nu de CRUD-basisroutes voor **maken** en **vermelden** toe aan de REST-API.</span><span class="sxs-lookup"><span data-stu-id="95f42-268">You now add the basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="95f42-269">Andere routes vindt u in het gedeelte `complete` van het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="95f42-269">Other routes can be found in the `complete` branch of the sample.</span></span>

<span data-ttu-id="95f42-270">Wijzig de directory vanaf de opdrachtregel in `azuread`, als dat nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="95f42-270">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="95f42-271">Open het bestand `server.js` in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="95f42-271">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="95f42-272">Voeg de volgende informatie toe onder de databasevermeldingen die u hierboven hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="95f42-272">Below the database entries you made above add the following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it to Mongodb
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
            req.log.warn(err, 'createTask: unable to save');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

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
            log.warn(err, "There is no tasks in the database. Add one!");
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


#### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="95f42-273">Foutafhandeling voor de routes toevoegen</span><span class="sxs-lookup"><span data-stu-id="95f42-273">Add error handling for the routes</span></span>
<span data-ttu-id="95f42-274">Voeg een vorm van foutafhandeling toe, zodat u eventuele problemen op een begrijpelijke manier kunt terugkoppelen naar de client.</span><span class="sxs-lookup"><span data-stu-id="95f42-274">Add some error handling so that you can communicate any problems you encounter back to the client in a way that it can understand.</span></span>

<span data-ttu-id="95f42-275">Voeg de volgende code toe:</span><span class="sxs-lookup"><span data-stu-id="95f42-275">Add the following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back to the client
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


## <a name="create-your-server"></a><span data-ttu-id="95f42-276">De server maken</span><span class="sxs-lookup"><span data-stu-id="95f42-276">Create your server</span></span>
<span data-ttu-id="95f42-277">U hebt nu een database gedefinieerd en de routes geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="95f42-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="95f42-278">Nu hoeft u alleen nog het serverexemplaar toe te voegen waarmee uw aanroepen worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="95f42-278">The last thing for you to do is to add the server instance that manages your calls.</span></span>

<span data-ttu-id="95f42-279">Met Restify en Express kunt u de REST-API-server in grote mate aanpassen, maar hier gebruikt u de meest eenvoudige configuratie.</span><span class="sxs-lookup"><span data-stu-id="95f42-279">Restify and Express provide deep customization for a REST API server, but we use the most basic setup here.</span></span>

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

// Allow 5 requests/second by IP, and burst to 10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping to REST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-the-routes-to-the-server-without-authentication"></a><span data-ttu-id="95f42-280">De routes toevoegen aan de server (zonder verificatie)</span><span class="sxs-lookup"><span data-stu-id="95f42-280">Add the routes to the server (without authentication)</span></span>
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
    consoleMessage += '\n Open your browser to %s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-to-your-rest-api-server"></a><span data-ttu-id="95f42-281">Verificatie toevoegen aan een REST-API-app</span><span class="sxs-lookup"><span data-stu-id="95f42-281">Add authentication to your REST API server</span></span>
<span data-ttu-id="95f42-282">Nu u een actieve REST-API-server hebt, kunt u deze gaan gebruiken met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95f42-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="95f42-283">Wijzig de directory vanaf de opdrachtregel in `azuread`, als dat nog niet is gebeurd:</span><span class="sxs-lookup"><span data-stu-id="95f42-283">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="95f42-284">De OIDCBearerStrategy gebruiken die is opgenomen in passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="95f42-284">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="95f42-285">Wanneer u API's schrijft, moet u de gegevens altijd koppelen aan iets unieks in het token, iets dat de gebruiker niet kan vervalsen.</span><span class="sxs-lookup"><span data-stu-id="95f42-285">When you write APIs, you should always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="95f42-286">Wanneer de server ToDo-items opslaat, gebeurt dit op basis van de **oid** van de gebruiker in het token (aangeroepen via token.oid); deze komt in het eigenaarsveld te staan.</span><span class="sxs-lookup"><span data-stu-id="95f42-286">When the server stores ToDo items, it does so based on the **oid** of the user in the token (called through token.oid), which goes in the “owner” field.</span></span> <span data-ttu-id="95f42-287">Met deze waarde zorgt u ervoor dat alleen die gebruiker toegang heeft tot zijn/haar eigen ToDo-items.</span><span class="sxs-lookup"><span data-stu-id="95f42-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="95f42-288">In de API wordt de 'eigenaar' niet weergegeven. Dat betekent dat een externe gebruiker ToDo-items van anderen kan aanvragen, ook al zijn ze geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="95f42-288">There is no exposure in the API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="95f42-289">Vervolgens gebruikt u de bearer-strategie die bij `passport-azure-ad` is geleverd.</span><span class="sxs-lookup"><span data-stu-id="95f42-289">Next, use the bearer strategy that comes with `passport-azure-ad`.</span></span>

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
        log.info('verifying the user');
        log.info(token, 'was the token retreived');
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

<span data-ttu-id="95f42-290">Passport maakt gebruik van hetzelfde patroon voor alle strategieën.</span><span class="sxs-lookup"><span data-stu-id="95f42-290">Passport uses the same pattern for all its strategies.</span></span> <span data-ttu-id="95f42-291">U geeft hieraan een `function()` door die `token` en `done` als parameters heeft.</span><span class="sxs-lookup"><span data-stu-id="95f42-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="95f42-292">De strategie komt weer naar u terug nadat al het werk is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="95f42-292">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="95f42-293">Sla de gebruiker op en sla ook het token op, zodat u het niet opnieuw hoeft op te vragen.</span><span class="sxs-lookup"><span data-stu-id="95f42-293">You should then store the user and save the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95f42-294">In bovenstaande code wordt elke gebruiker gebruikt die zich bij de server kan verifiëren.</span><span class="sxs-lookup"><span data-stu-id="95f42-294">The code above takes any user who happens to authenticate to your server.</span></span> <span data-ttu-id="95f42-295">Dit proces wordt automatische registratie genoemd.</span><span class="sxs-lookup"><span data-stu-id="95f42-295">This process is known as autoregistration.</span></span> <span data-ttu-id="95f42-296">In productieservers geeft u gebruikers geen toegang tot de API zonder ze een registratieproces te laten doorlopen.</span><span class="sxs-lookup"><span data-stu-id="95f42-296">In production servers, don't let in any users access the API without first having them go through a registration process.</span></span> <span data-ttu-id="95f42-297">Dit proces is doorgaans het patroon dat u ziet in consumentenapps, waarbij u zich kunt registreren via Facebook, maar waarvoor u vervolgens aanvullende informatie moet invullen.</span><span class="sxs-lookup"><span data-stu-id="95f42-297">This process is usually the pattern you see in consumer apps that allow you to register by using Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="95f42-298">Als dit geen opdrachtregelprogramma was, had u het e-mailadres kunnen verkrijgen uit het tokenobject dat wordt geretourneerd en had u gebruikers daarna niet kunnen vragen aanvullende gegevens in te vullen.</span><span class="sxs-lookup"><span data-stu-id="95f42-298">If this program wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked users to fill out additional information.</span></span> <span data-ttu-id="95f42-299">Omdat dit een voorbeeld is, voegt u ze toe aan een database in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="95f42-299">Because this is a sample, we add them to an in-memory database.</span></span>
>
>

## <a name="run-your-server-application-to-verify-that-it-rejects-you"></a><span data-ttu-id="95f42-300">De servertoepassing uitvoeren om te verifiëren dat u wordt geweigerd</span><span class="sxs-lookup"><span data-stu-id="95f42-300">Run your server application to verify that it rejects you</span></span>
<span data-ttu-id="95f42-301">U kunt `curl` gebruiken om na te gaan of u nu OAuth2-bescherming voor uw eindpunten hebt.</span><span class="sxs-lookup"><span data-stu-id="95f42-301">You can use `curl` to see if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="95f42-302">De geretourneerde headers moeten voldoende zijn om aan te geven dat u op de juiste weg bent.</span><span class="sxs-lookup"><span data-stu-id="95f42-302">The headers returned should be enough to tell you that you are on the right path.</span></span>

<span data-ttu-id="95f42-303">Controleer of het MongoDB-exemplaar is geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="95f42-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="95f42-304">Schakel naar de directory en voer de server uit:</span><span class="sxs-lookup"><span data-stu-id="95f42-304">Change to the directory and run the server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="95f42-305">Voer `curl` uit in een nieuw terminalvenster</span><span class="sxs-lookup"><span data-stu-id="95f42-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="95f42-306">Probeer een basic POST:</span><span class="sxs-lookup"><span data-stu-id="95f42-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="95f42-307">Een 401-fout is het gewenste antwoord.</span><span class="sxs-lookup"><span data-stu-id="95f42-307">A 401 error is the response you want.</span></span> <span data-ttu-id="95f42-308">Hiermee wordt aangegeven dat de Passport-laag probeert om te leiden naar het geautoriseerde eindpunt.</span><span class="sxs-lookup"><span data-stu-id="95f42-308">It indicates that the Passport layer is trying to redirect to the authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="95f42-309">U hebt nu een REST-API-service die gebruikmaakt van OAuth2</span><span class="sxs-lookup"><span data-stu-id="95f42-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="95f42-310">U hebt een REST-API geïmplementeerd met behulp van Restify en OAuth!</span><span class="sxs-lookup"><span data-stu-id="95f42-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="95f42-311">U hebt nu voldoende code om door te gaan met het ontwikkelen van uw service. U kunt voortbouwen op dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="95f42-311">You now have sufficient code so that you can continue to develop your service and build on this example.</span></span> <span data-ttu-id="95f42-312">U bent nu met deze server zo ver mogelijk gegaan zonder gebruik te maken van een OAuth2-compatibele client.</span><span class="sxs-lookup"><span data-stu-id="95f42-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="95f42-313">Gebruik voor de volgende stap een aanvullende walkthrough, zoals [Een web-API verbinden met behulp van iOS met B2C](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="95f42-313">For that next step use an additional walk-through like our [Connect to a web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95f42-314">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="95f42-314">Next steps</span></span>
<span data-ttu-id="95f42-315">U kunt nu verdergaan met geavanceerdere onderwerpen, te weten:</span><span class="sxs-lookup"><span data-stu-id="95f42-315">You can now move to more advanced topics, such as:</span></span>

[<span data-ttu-id="95f42-316">Een web-API verbinden met behulp van iOS met B2C</span><span class="sxs-lookup"><span data-stu-id="95f42-316">Connect to a web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
