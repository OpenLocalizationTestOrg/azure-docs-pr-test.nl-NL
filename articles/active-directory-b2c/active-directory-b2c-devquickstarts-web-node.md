---
title: Aanmelding toevoegen aan een Node.js-web-app voor Azure B2C | Microsoft Docs
description: Een Node.js-web-app maken waarmee gebruikers worden aangemeld via een B2C-tenant.
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: c85b8f8434d1e837ac96ac63b9b37f990677ed6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="91f67-103">Azure AD B2C: aanmelding toevoegen aan een Node.js-web-app</span><span class="sxs-lookup"><span data-stu-id="91f67-103">Azure AD B2C: Add sign-in to a Node.js web app</span></span>

<span data-ttu-id="91f67-104">**Passport** is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="91f67-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="91f67-105">Passport is zeer flexibel en modulair, en kan onopvallend worden geïnstalleerd in een Express- of Restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="91f67-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="91f67-106">Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.</span><span class="sxs-lookup"><span data-stu-id="91f67-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="91f67-107">We hebben een strategie ontwikkeld voor Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91f67-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="91f67-108">U installeert deze module en voegt de vervolgens de `passport-azure-ad`-invoegtoepassing van Azure AD toe.</span><span class="sxs-lookup"><span data-stu-id="91f67-108">You will install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="91f67-109">Hiervoor doet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="91f67-109">To do this, you need to:</span></span>

1. <span data-ttu-id="91f67-110">U registreert een toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91f67-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="91f67-111">U stelt de app in op het gebruik van de `passport-azure-ad`-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="91f67-111">Set up your app to use the `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="91f67-112">U gebruikt Passport om aan- en afmeldingsaanvragen te verzenden naar Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91f67-112">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="91f67-113">U drukt de gebruikersgegevens af.</span><span class="sxs-lookup"><span data-stu-id="91f67-113">Print user data.</span></span>

<span data-ttu-id="91f67-114">De code voor deze zelfstudie [wordt bewaard in GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="91f67-114">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="91f67-115">Als u het voorbeeld wilt uitvoeren, kunt u [de basis van de app downloaden als zip-bestand](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="91f67-115">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="91f67-116">U kunt het basisproject ook klonen:</span><span class="sxs-lookup"><span data-stu-id="91f67-116">You can also clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="91f67-117">De voltooide toepassing wordt verstrekt aan het einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="91f67-117">The completed application is provided at the end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="91f67-118">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="91f67-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="91f67-119">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="91f67-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="91f67-120">Een directory is een container voor alle gebruikers, apps, groepen en meer.</span><span class="sxs-lookup"><span data-stu-id="91f67-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="91f67-121">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u doorgaat in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="91f67-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="91f67-122">Een app maken</span><span class="sxs-lookup"><span data-stu-id="91f67-122">Create an application</span></span>

<span data-ttu-id="91f67-123">Vervolgens maakt u een app in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="91f67-123">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="91f67-124">Hiermee geeft u informatie door aan Azure AD die nodig is om veilig te communiceren met uw app.</span><span class="sxs-lookup"><span data-stu-id="91f67-124">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="91f67-125">De client-app en web-API worden aangegeven met één **toepassings-id** omdat deze beide één logische app vormen.</span><span class="sxs-lookup"><span data-stu-id="91f67-125">Both the client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="91f67-126">Volg [deze instructies](active-directory-b2c-app-registration.md) om een app te maken.</span><span class="sxs-lookup"><span data-stu-id="91f67-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="91f67-127">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="91f67-127">Be sure to:</span></span>

- <span data-ttu-id="91f67-128">U een **web-app**/**web-API** in de toepassing opneemt.</span><span class="sxs-lookup"><span data-stu-id="91f67-128">Include a **web app**/**web API** in the application.</span></span>
- <span data-ttu-id="91f67-129">U `http://localhost:3000/auth/openid/return` invoert als **antwoord-URL**.</span><span class="sxs-lookup"><span data-stu-id="91f67-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="91f67-130">Dit is de standaard-URL voor dit codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="91f67-130">It is the default URL for this code sample.</span></span>
- <span data-ttu-id="91f67-131">U een **toepassingsgeheim** maakt voor uw toepassing en dit kopieert.</span><span class="sxs-lookup"><span data-stu-id="91f67-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="91f67-132">U hebt dit later nodig.</span><span class="sxs-lookup"><span data-stu-id="91f67-132">You will need it later.</span></span> <span data-ttu-id="91f67-133">Merk op dat deze waarde [een escape-teken voor XML](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) moet bevatten voordat u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="91f67-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="91f67-134">U de **toepassings-id** kopieert die is toegewezen aan uw app.</span><span class="sxs-lookup"><span data-stu-id="91f67-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="91f67-135">Deze hebt u ook later nodig.</span><span class="sxs-lookup"><span data-stu-id="91f67-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="91f67-136">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="91f67-136">Create your policies</span></span>

<span data-ttu-id="91f67-137">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="91f67-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="91f67-138">Deze app bevat drie identiteitservaringen: registreren, aanmelden en aanmelden via Facebook.</span><span class="sxs-lookup"><span data-stu-id="91f67-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="91f67-139">U moet deze beleidsregel maken voor elk type, zoals wordt beschreven in het [naslagartikel voor beleid](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="91f67-139">You need to create this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="91f67-140">Wanneer u uw drie beleidsregels maakt:</span><span class="sxs-lookup"><span data-stu-id="91f67-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="91f67-141">Kiest u **Weergavenaam** en andere registratiekenmerken in het registratiebeleid.</span><span class="sxs-lookup"><span data-stu-id="91f67-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="91f67-142">Kiest u **Weergavenaam**- en **Object-id**-toepassingsclaims voor elk beleid.</span><span class="sxs-lookup"><span data-stu-id="91f67-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="91f67-143">U kunt ook andere claims kiezen.</span><span class="sxs-lookup"><span data-stu-id="91f67-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="91f67-144">Kopieert u de **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="91f67-144">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="91f67-145">Deze moet het voorvoegsel `b2c_1_` bevatten.</span><span class="sxs-lookup"><span data-stu-id="91f67-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="91f67-146">U hebt deze beleidsnamen later nodig.</span><span class="sxs-lookup"><span data-stu-id="91f67-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="91f67-147">Nadat u de drie beleidsregels hebt gemaakt, kunt u uw app maken.</span><span class="sxs-lookup"><span data-stu-id="91f67-147">After you create your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="91f67-148">In dit artikel wordt niet beschreven hoe u de gemaakte beleidsregels gebruikt.</span><span class="sxs-lookup"><span data-stu-id="91f67-148">Note that this article does not cover how to use the policies you just created.</span></span> <span data-ttu-id="91f67-149">Voor meer informatie over de werking van beleid in Azure AD B2C, leest u eerst de [zelfstudie Aan de slag met .NET-web-app](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="91f67-149">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-to-your-directory"></a><span data-ttu-id="91f67-150">Vereisten aan de directory toevoegen</span><span class="sxs-lookup"><span data-stu-id="91f67-150">Add prerequisites to your directory</span></span>

<span data-ttu-id="91f67-151">Wijzig vanaf de opdrachtregel de directory's in de hoofdmap, als u hier nog niet bent.</span><span class="sxs-lookup"><span data-stu-id="91f67-151">From the command line, change directories to your root folder, if you're not already there.</span></span> <span data-ttu-id="91f67-152">Voer de volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="91f67-152">Run the following commands:</span></span>

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

<span data-ttu-id="91f67-153">Daarnaast hebben we `passport-azure-ad` gebruikt voor het voorbeeld in de basis van de snelstartgids.</span><span class="sxs-lookup"><span data-stu-id="91f67-153">In addition, we used `passport-azure-ad` for our preview in the skeleton of the Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="91f67-154">Hiermee worden de bibliotheken geïnstalleerd waarvan `passport-azure-ad` afhankelijk is.</span><span class="sxs-lookup"><span data-stu-id="91f67-154">This will install the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-to-use-the-passport-nodejs-strategy"></a><span data-ttu-id="91f67-155">Uw app instellen voor gebruik van de strategie Passport-Node.js</span><span class="sxs-lookup"><span data-stu-id="91f67-155">Set up your app to use the Passport-Node.js strategy</span></span>
<span data-ttu-id="91f67-156">Configureer de Express-middleware voor gebruik van het OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="91f67-156">Configure the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="91f67-157">Passport wordt onder andere gebruikt om aan- en afmeldingsaanvragen te verzenden, gebruikerssessies te beheren en informatie over gebruikers op te halen.</span><span class="sxs-lookup"><span data-stu-id="91f67-157">Passport will be used to issue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="91f67-158">Open het bestand `config.js` in de hoofdmap van het project en geef de configuratiewaarden van de app op in de sectie `exports.creds`.</span><span class="sxs-lookup"><span data-stu-id="91f67-158">Open the `config.js` file in the root of the project and enter your app's configuration values in the `exports.creds` section.</span></span>
- <span data-ttu-id="91f67-159">`clientID`: de **toepassings-id** die is toegewezen aan uw app in de registratieportal.</span><span class="sxs-lookup"><span data-stu-id="91f67-159">`clientID`: The **Application ID** assigned to your app in the registration portal.</span></span>
- <span data-ttu-id="91f67-160">`returnURL`: de **omleidings-URI** die u hebt ingevoerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="91f67-160">`returnURL`: The **Redirect URI** you entered in the portal.</span></span>
- <span data-ttu-id="91f67-161">`tenantName`: de tenantnaam van de app, bijvoorbeeld **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="91f67-161">`tenantName`: The tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="91f67-162">Open het bestand `app.js` in de hoofdmap van het project.</span><span class="sxs-lookup"><span data-stu-id="91f67-162">Open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="91f67-163">Voeg de volgende aanroep toe om de `OIDCStrategy`-strategie aan te roepen die beschikbaar is in `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="91f67-163">Add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="91f67-164">Gebruik de strategie waarnaar u net hebt verwezen om aanmeldingsaanvragen te verwerken.</span><span class="sxs-lookup"><span data-stu-id="91f67-164">Use the strategy you just referenced to handle sign-in requests.</span></span>

```JavaScript
// Use the OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
    process.nextTick(function () {
      findByEmail(profile.email, function(err, user) {
        if (err) {
          return done(err);
        }
        if (!user) {
          // "Auto-registration"
          users.push(profile);
          return done(null, profile);
        }
        return done(null, user);
      });
    });
  }
));
```
<span data-ttu-id="91f67-165">In Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (inclusief Twitter en Facebook).</span><span class="sxs-lookup"><span data-stu-id="91f67-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="91f67-166">Alle schrijvers van strategieën gebruiken dit patroon.</span><span class="sxs-lookup"><span data-stu-id="91f67-166">All strategy writers adhere to this pattern.</span></span> <span data-ttu-id="91f67-167">Wanneer u de strategie bekijkt, ziet u dat u een `function()` met een token hieraan doorgeeft en `done` doorgeeft als parameters.</span><span class="sxs-lookup"><span data-stu-id="91f67-167">When you look at the strategy, you can see that you pass it a `function()` that has a token and a `done` as the parameters.</span></span> <span data-ttu-id="91f67-168">De strategie komt weer naar u terug nadat al het werk is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="91f67-168">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="91f67-169">Sla de gebruiker en het token op, zodat u hier niet opnieuw naar hoeft te vragen.</span><span class="sxs-lookup"><span data-stu-id="91f67-169">Store the user and stash the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="91f67-170">De voorafgaande code geldt voor alle gebruikers die worden geverifieerd door de server.</span><span class="sxs-lookup"><span data-stu-id="91f67-170">The preceding code takes all users whom the server authenticates.</span></span> <span data-ttu-id="91f67-171">Dit is automatische registratie.</span><span class="sxs-lookup"><span data-stu-id="91f67-171">This is autoregistration.</span></span> <span data-ttu-id="91f67-172">Wanneer u productieservers gebruikt, wilt u gebruikers alleen toelaten als ze een registratieproces hebben doorlopen dat u hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="91f67-172">When you use production servers, you don’t want to let in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="91f67-173">U ziet dit patroon vaak in consumenten-apps.</span><span class="sxs-lookup"><span data-stu-id="91f67-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="91f67-174">U kunt u hiermee registreren met Facebook, maar vervolgens wordt u om aanvullende informatie gevraagd.</span><span class="sxs-lookup"><span data-stu-id="91f67-174">These allow you to register by using Facebook, but then they ask you to fill out additional information.</span></span> <span data-ttu-id="91f67-175">Als de toepassing geen voorbeeld zou zijn, zouden we een e-mailadres kunnen extraheren uit het tokenobject dat wordt geretourneerd en vervolgens de gebruiker vragen om aanvullende informatie in te vullen.</span><span class="sxs-lookup"><span data-stu-id="91f67-175">If our application wasn’t a sample, we could extract an email address from the token object that is returned, and then ask the user to fill out additional information.</span></span> <span data-ttu-id="91f67-176">Omdat dit een testserver is, voegen we gebruikers toe aan de database in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="91f67-176">Because this is a test server, we simply add users to the in-memory database.</span></span>

<span data-ttu-id="91f67-177">Voeg de methoden toe waarmee u gebruikers kunt bijhouden die zich hebben aangemeld, zoals wordt vereist door Passport.</span><span class="sxs-lookup"><span data-stu-id="91f67-177">Add the methods that allow you to keep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="91f67-178">Dit omvat het serialiseren en deserialiseren van gebruikersgegevens:</span><span class="sxs-lookup"><span data-stu-id="91f67-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   To support persistent sign-in sessions, Passport needs to be able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing the user ID when Passport serializes a user
//   and finding the user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array to hold users who have signed in
var users = [];

var findByEmail = function(email, fn) {
  for (var i = 0, len = users.length; i < len; i++) {
    var user = users[i];
    log.info('we are using user: ', user);
    if (user.email === email) {
      return fn(null, user);
    }
  }
  return fn(null, null);
};

```

<span data-ttu-id="91f67-179">Voeg de code voor het laden van de Express-engine toe.</span><span class="sxs-lookup"><span data-stu-id="91f67-179">Add the code to load the Express engine.</span></span> <span data-ttu-id="91f67-180">Hierna kunt u zien dat we het standaardpatroon voor `/views` en `/routes` van Express gebruiken.</span><span class="sxs-lookup"><span data-stu-id="91f67-180">In the following, you can see that we use the default `/views` and `/routes` pattern that Express provides.</span></span>

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware to support
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="91f67-181">Voeg de `POST`-routes toe waarmee de daadwerkelijke aanmeldingsaanvragen worden afgeleverd bij de `passport-azure-ad`-engine:</span><span class="sxs-lookup"><span data-stu-id="91f67-181">Add the `POST` routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware to authenticate the
//   request. The first step in OpenID authentication involves redirecting
//   the user to an OpenID provider. After the user is authenticated,
//   the OpenID provider redirects the user back to this application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in the Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it redirects the user to the home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it will redirect the user to the home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="91f67-182">Passport gebruiken om aan- en afmeldingsaanvragen te verzenden naar Azure AD</span><span class="sxs-lookup"><span data-stu-id="91f67-182">Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>

<span data-ttu-id="91f67-183">Uw app is nu geconfigureerd voor communicatie met het v2.0-eindpunt met behulp van het OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="91f67-183">Your app is now properly configured to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="91f67-184">`passport-azure-ad` heeft gezorgd voor de details van het samenstellen van verificatieberichten, het valideren van tokens van Azure AD en het beheren van gebruikerssessies.</span><span class="sxs-lookup"><span data-stu-id="91f67-184">`passport-azure-ad` has taken care of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="91f67-185">U hoeft alleen nog ervoor te zorgen dat uw gebruikers zich kunnen aan- en afmelden en aanvullende informatie te verzamelen over gebruikers die zich hebben aangemeld.</span><span class="sxs-lookup"><span data-stu-id="91f67-185">All that remains is to give your users a way to sign in and sign out, and to gather additional information on users who have signed in.</span></span>

<span data-ttu-id="91f67-186">Voeg eerst de standaardmethode en de aanmeldings-, account- en afmeldingsmethoden toe aan uw `app.js`-bestand:</span><span class="sxs-lookup"><span data-stu-id="91f67-186">First, add the default, sign-in, account, and sign-out methods to your `app.js` file:</span></span>

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in the Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="91f67-187">Meer informatie over deze methoden:</span><span class="sxs-lookup"><span data-stu-id="91f67-187">To review these methods in detail:</span></span>
- <span data-ttu-id="91f67-188">Met de route `/` wordt u omgeleid naar de weergave `index.ejs` door de gebruiker in de aanvraag door te geven (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="91f67-188">The `/` route redirects to the `index.ejs` view by passing the user in the request (if it exists).</span></span>
- <span data-ttu-id="91f67-189">Met de route `/account` wordt eerst gecontroleerd of u bent geverifieerd (de implementatie hiervoor vindt u hieronder).</span><span class="sxs-lookup"><span data-stu-id="91f67-189">The `/account` route first verifies that you are authenticated (the implementation for this is below).</span></span> <span data-ttu-id="91f67-190">Vervolgens wordt de gebruiker in de aanvraag doorgegeven, zodat u aanvullende informatie over de gebruiker kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="91f67-190">It then passes the user in the request so that you can get additional information about the user.</span></span>
- <span data-ttu-id="91f67-191">Met de route `/login` wordt de `azuread-openidconnect`-verificator aangeroepen vanuit `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="91f67-191">The `/login` route calls the `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="91f67-192">Als dit niet lukt, wordt de gebruiker omgeleid naar `/login`.</span><span class="sxs-lookup"><span data-stu-id="91f67-192">If it doesn't succeed, the route redirects the user back to `/login`.</span></span>
- <span data-ttu-id="91f67-193">`/logout` roept `logout.ejs` aan (en de bijbehorende route).</span><span class="sxs-lookup"><span data-stu-id="91f67-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="91f67-194">Hiermee worden cookies gewist en keert de gebruiker terug naar `index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="91f67-194">This clears cookies and then returns the user back to `index.ejs`.</span></span>


<span data-ttu-id="91f67-195">Voor het laatste deel van `app.js` voegt u de `EnsureAuthenticated`-methode toe die wordt gebruikt in de route `/account`.</span><span class="sxs-lookup"><span data-stu-id="91f67-195">For the last part of `app.js`, add the `EnsureAuthenticated` method that is used in the `/account` route.</span></span>

```JavaScript

// Simple route middleware to ensure that the user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs to be protected. If
//   the request is authenticated (typically via a persistent sign-in session),
//   then the request will proceed. Otherwise, the user will be redirected to the
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="91f67-196">Maak ten slotte de server zelf in `app.js`.</span><span class="sxs-lookup"><span data-stu-id="91f67-196">Finally, create the server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-the-views-and-routes-in-express-to-call-your-policies"></a><span data-ttu-id="91f67-197">De weergaven en routes in Express maken om uw beleid aan te roepen</span><span class="sxs-lookup"><span data-stu-id="91f67-197">Create the views and routes in Express to call your policies</span></span>

<span data-ttu-id="91f67-198">Uw `app.js` is nu voltooid.</span><span class="sxs-lookup"><span data-stu-id="91f67-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="91f67-199">U hoeft alleen nog de routes en weergaven toe te voegen waarmee u het aanmeldings- en registratiebeleid kunt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="91f67-199">You just need to add the routes and views that allow you to call the sign-in and sign-up policies.</span></span> <span data-ttu-id="91f67-200">Hiermee worden ook de routes voor `/logout` en `/login` verwerkt die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="91f67-200">These also handle the `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="91f67-201">Maak de route `/routes/index.js` onder de hoofddirectory.</span><span class="sxs-lookup"><span data-stu-id="91f67-201">Create the `/routes/index.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="91f67-202">Maak de route `/routes/user.js` onder de hoofddirectory.</span><span class="sxs-lookup"><span data-stu-id="91f67-202">Create the `/routes/user.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="91f67-203">Met deze eenvoudige routes worden aanvragen doorgegeven aan uw weergaven.</span><span class="sxs-lookup"><span data-stu-id="91f67-203">These simple routes pass along requests to your views.</span></span> <span data-ttu-id="91f67-204">Deze omvatten de gebruiker, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="91f67-204">They include the user, if one is present.</span></span>

<span data-ttu-id="91f67-205">Maak de weergave `/views/index.ejs` onder de hoofddirectory.</span><span class="sxs-lookup"><span data-stu-id="91f67-205">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="91f67-206">Dit is een eenvoudige pagina waarmee beleid voor aanmelden en afmelden wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="91f67-206">This is a simple page that calls policies for sign-in and sign-out.</span></span> <span data-ttu-id="91f67-207">U kunt dit ook gebruiken om accountgegevens op te halen.</span><span class="sxs-lookup"><span data-stu-id="91f67-207">You can also use it to grab account information.</span></span> <span data-ttu-id="91f67-208">U kunt de voorwaardelijke `if (!user)` gebruiken als de gebruiker wordt doorgegeven in de aanvraag om te bewijzen dat deze is aangemeld.</span><span class="sxs-lookup"><span data-stu-id="91f67-208">Note that you can use the conditional `if (!user)` as the user is passed through in the request to provide evidence that the user is signed in.</span></span>

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

<span data-ttu-id="91f67-209">Maak de weergave `/views/account.ejs` onder de hoofddirectory, zodat u aanvullende informatie kunt weergeven die `passport-azure-ad` in de gebruikersaanvraag heeft geplaatst.</span><span class="sxs-lookup"><span data-stu-id="91f67-209">Create the `/views/account.ejs` view under the root directory so that you can view additional information that `passport-azure-ad` put in the user request.</span></span>

```Javascript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login">Sign in</a>
<% } else { %>
<p>displayName: <%= user.displayName %></p>
<p>givenName: <%= user.name.givenName %></p>
<p>familyName: <%= user.name.familyName %></p>
<p>UPN: <%= user._json.upn %></p>
<p>Profile ID: <%= user.id %></p>
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

<span data-ttu-id="91f67-210">U kunt nu uw app bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="91f67-210">You can now build and run your app.</span></span>

<span data-ttu-id="91f67-211">`node app.js` uitvoeren en naar `http://localhost:3000` navigeren</span><span class="sxs-lookup"><span data-stu-id="91f67-211">Run `node app.js` and navigate to `http://localhost:3000`</span></span>


<span data-ttu-id="91f67-212">Registreer u of meld u aan bij de app via e-mail of Facebook.</span><span class="sxs-lookup"><span data-stu-id="91f67-212">Sign up or sign in to the app by using email or Facebook.</span></span> <span data-ttu-id="91f67-213">Meld u af en meld u weer aan als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="91f67-213">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="91f67-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91f67-214">Next steps</span></span>

<span data-ttu-id="91f67-215">Voor naslag is het voltooide voorbeeld (zonder uw configuratiewaarden) [geleverd als zip-bestand](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="91f67-215">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="91f67-216">U kunt dit ook klonen van GitHub:</span><span class="sxs-lookup"><span data-stu-id="91f67-216">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="91f67-217">U kunt nu verder met geavanceerdere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="91f67-217">You can now move on to more advanced topics.</span></span> <span data-ttu-id="91f67-218">U kunt het volgende proberen:</span><span class="sxs-lookup"><span data-stu-id="91f67-218">You might try:</span></span>

[<span data-ttu-id="91f67-219">Een web-API beveiligen met het B2C-model in Node.js</span><span class="sxs-lookup"><span data-stu-id="91f67-219">Secure a web API by using the B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on to more advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing the your B2C App's UX >>]()

-->
