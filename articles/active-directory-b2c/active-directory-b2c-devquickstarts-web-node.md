---
title: aaaAdd aanmelden tooa Node.js web-app voor Azure B2C | Microsoft Docs
description: Hoe toobuild een Node.js-web-app die gebruikers worden aangemeld met behulp van een B2C-tenant.
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
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="46d1b-103">Azure AD B2C: Aanmelden tooa Node.js-webtoepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="46d1b-103">Azure AD B2C: Add sign-in tooa Node.js web app</span></span>

<span data-ttu-id="46d1b-104">**Passport** is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="46d1b-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="46d1b-105">Passport is zeer flexibel en modulair, en kan onopvallend worden geïnstalleerd in een Express- of Restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="46d1b-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="46d1b-106">Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.</span><span class="sxs-lookup"><span data-stu-id="46d1b-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="46d1b-107">We hebben een strategie ontwikkeld voor Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46d1b-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="46d1b-108">U installeert deze module en voegt u hello Azure AD `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="46d1b-108">You will install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="46d1b-109">toodo, moet u:</span><span class="sxs-lookup"><span data-stu-id="46d1b-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="46d1b-110">U registreert een toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46d1b-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="46d1b-111">Instellen van uw app toouse hello `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="46d1b-111">Set up your app toouse hello `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="46d1b-112">Passport tooissue aanmelden en afmelden aanvragen tooAzure AD gebruiken.</span><span class="sxs-lookup"><span data-stu-id="46d1b-112">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="46d1b-113">U drukt de gebruikersgegevens af.</span><span class="sxs-lookup"><span data-stu-id="46d1b-113">Print user data.</span></span>

<span data-ttu-id="46d1b-114">code voor deze zelfstudie Hallo [wordt bewaard in GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="46d1b-114">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="46d1b-115">toofollow langs, kunt u [basis van Hallo app downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="46d1b-115">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="46d1b-116">U kunt Hallo basisproject ook klonen:</span><span class="sxs-lookup"><span data-stu-id="46d1b-116">You can also clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="46d1b-117">toepassing Hello voltooid wordt op Hallo einde van deze zelfstudie aangeboden.</span><span class="sxs-lookup"><span data-stu-id="46d1b-117">hello completed application is provided at hello end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="46d1b-118">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="46d1b-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="46d1b-119">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="46d1b-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="46d1b-120">Een directory is een container voor alle gebruikers, apps, groepen en meer.</span><span class="sxs-lookup"><span data-stu-id="46d1b-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="46d1b-121">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u doorgaat in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="46d1b-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="46d1b-122">Een app maken</span><span class="sxs-lookup"><span data-stu-id="46d1b-122">Create an application</span></span>

<span data-ttu-id="46d1b-123">Vervolgens moet u een app toocreate in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="46d1b-123">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="46d1b-124">Hiermee geeft u Azure AD-informatie dat het moet toocommunicate veilig met uw app.</span><span class="sxs-lookup"><span data-stu-id="46d1b-124">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="46d1b-125">Beide Hallo van client-app en web-API worden aangegeven met één **toepassings-ID**, omdat ze samen één logische app vormen.</span><span class="sxs-lookup"><span data-stu-id="46d1b-125">Both hello client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="46d1b-126">toocreate een app, volg [deze instructies](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="46d1b-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="46d1b-127">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="46d1b-127">Be sure to:</span></span>

- <span data-ttu-id="46d1b-128">Omvatten een **web-app**/**web-API** in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="46d1b-128">Include a **web app**/**web API** in hello application.</span></span>
- <span data-ttu-id="46d1b-129">U `http://localhost:3000/auth/openid/return` invoert als **antwoord-URL**.</span><span class="sxs-lookup"><span data-stu-id="46d1b-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="46d1b-130">Het is Hallo-standaard-URL voor dit codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="46d1b-130">It is hello default URL for this code sample.</span></span>
- <span data-ttu-id="46d1b-131">U een **toepassingsgeheim** maakt voor uw toepassing en dit kopieert.</span><span class="sxs-lookup"><span data-stu-id="46d1b-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="46d1b-132">U hebt dit later nodig.</span><span class="sxs-lookup"><span data-stu-id="46d1b-132">You will need it later.</span></span> <span data-ttu-id="46d1b-133">Opmerking dat deze waarde toobe moet [XML escape-teken](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) voordat u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="46d1b-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="46d1b-134">Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app.</span><span class="sxs-lookup"><span data-stu-id="46d1b-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="46d1b-135">Deze hebt u ook later nodig.</span><span class="sxs-lookup"><span data-stu-id="46d1b-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="46d1b-136">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="46d1b-136">Create your policies</span></span>

<span data-ttu-id="46d1b-137">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="46d1b-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="46d1b-138">Deze app bevat drie identiteitservaringen: registreren, aanmelden en aanmelden via Facebook.</span><span class="sxs-lookup"><span data-stu-id="46d1b-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="46d1b-139">U moet toocreate dit beleid voor elk type, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="46d1b-139">You need toocreate this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="46d1b-140">Wanneer u uw drie beleidsregels maakt:</span><span class="sxs-lookup"><span data-stu-id="46d1b-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="46d1b-141">Kies Hallo **weergavenaam** en andere registratiekenmerken in het registratiebeleid.</span><span class="sxs-lookup"><span data-stu-id="46d1b-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="46d1b-142">Kies Hallo **weergavenaam** en **Object-ID** toepassingsclaims voor elk beleid.</span><span class="sxs-lookup"><span data-stu-id="46d1b-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="46d1b-143">U kunt ook andere claims kiezen.</span><span class="sxs-lookup"><span data-stu-id="46d1b-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="46d1b-144">Kopiëren Hallo **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46d1b-144">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="46d1b-145">Het voorvoegsel Hallo heeft `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="46d1b-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="46d1b-146">U hebt deze beleidsnamen later nodig.</span><span class="sxs-lookup"><span data-stu-id="46d1b-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="46d1b-147">Wanneer u uw drie beleidsregels maakt, bent u klaar toobuild uw app.</span><span class="sxs-lookup"><span data-stu-id="46d1b-147">After you create your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="46d1b-148">Houd er rekening mee dat dit artikel wordt niet beschreven hoe toouse Hallo beleidsregels u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46d1b-148">Note that this article does not cover how toouse hello policies you just created.</span></span> <span data-ttu-id="46d1b-149">toolearn over de werking van beleid in Azure AD B2C, beginnen met Hallo [zelfstudie .NET web app aan de slag](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="46d1b-149">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-tooyour-directory"></a><span data-ttu-id="46d1b-150">Vereisten tooyour map toevoegen</span><span class="sxs-lookup"><span data-stu-id="46d1b-150">Add prerequisites tooyour directory</span></span>

<span data-ttu-id="46d1b-151">Vanaf de opdrachtregel Hallo tooyour hoofdmap mappen te wijzigen als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="46d1b-151">From hello command line, change directories tooyour root folder, if you're not already there.</span></span> <span data-ttu-id="46d1b-152">Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="46d1b-152">Run hello following commands:</span></span>

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

<span data-ttu-id="46d1b-153">Daarnaast hebben we gebruikt `passport-azure-ad` voor het voorbeeld in Hallo basisproject Hallo Quick Start.</span><span class="sxs-lookup"><span data-stu-id="46d1b-153">In addition, we used `passport-azure-ad` for our preview in hello skeleton of hello Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="46d1b-154">Hiermee installeert u Hallo bibliotheken die `passport-azure-ad` is afhankelijk van.</span><span class="sxs-lookup"><span data-stu-id="46d1b-154">This will install hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a><span data-ttu-id="46d1b-155">Instellen van uw app toouse Hallo strategie Passport-Node.js</span><span class="sxs-lookup"><span data-stu-id="46d1b-155">Set up your app toouse hello Passport-Node.js strategy</span></span>
<span data-ttu-id="46d1b-156">Configureer Hallo Express-middleware toouse hello OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="46d1b-156">Configure hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="46d1b-157">Passport gaat gebruikte tooissue aanmelden en afmeldingsaanvragen te verzenden, gebruikerssessies te beheren en informatie over gebruikers, onder andere acties.</span><span class="sxs-lookup"><span data-stu-id="46d1b-157">Passport will be used tooissue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="46d1b-158">Open Hallo `config.js` bestand in de hoofdmap Hallo van Hallo-project en voer de configuratiewaarden van uw app in Hallo `exports.creds` sectie.</span><span class="sxs-lookup"><span data-stu-id="46d1b-158">Open hello `config.js` file in hello root of hello project and enter your app's configuration values in hello `exports.creds` section.</span></span>
- <span data-ttu-id="46d1b-159">`clientID`: Hallo **toepassings-ID** tooyour-app in de portal voor registratie van Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="46d1b-159">`clientID`: hello **Application ID** assigned tooyour app in hello registration portal.</span></span>
- <span data-ttu-id="46d1b-160">`returnURL`: Hallo **omleidings-URI** u hebt ingevoerd in het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="46d1b-160">`returnURL`: hello **Redirect URI** you entered in hello portal.</span></span>
- <span data-ttu-id="46d1b-161">`tenantName`: de tenantnaam Hallo van uw app, bijvoorbeeld **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="46d1b-161">`tenantName`: hello tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="46d1b-162">Open Hallo `app.js` bestand in de hoofdmap Hallo van Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="46d1b-162">Open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="46d1b-163">Toevoegen van de volgende aanroep tooinvoke Hallo Hallo `OIDCStrategy` strategie die wordt geleverd met `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="46d1b-163">Add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="46d1b-164">Gebruik Hallo-strategie die u zojuist hebt waarnaar wordt verwezen toohandle aanmelden aanvragen.</span><span class="sxs-lookup"><span data-stu-id="46d1b-164">Use hello strategy you just referenced toohandle sign-in requests.</span></span>

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
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
<span data-ttu-id="46d1b-165">In Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (inclusief Twitter en Facebook).</span><span class="sxs-lookup"><span data-stu-id="46d1b-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="46d1b-166">Alle schrijvers van strategieën toothis patroon.</span><span class="sxs-lookup"><span data-stu-id="46d1b-166">All strategy writers adhere toothis pattern.</span></span> <span data-ttu-id="46d1b-167">Wanneer u Hallo strategie bekijkt, ziet u dat u gebruikmaakt van een `function()` die een token heeft en een `done` als Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="46d1b-167">When you look at hello strategy, you can see that you pass it a `function()` that has a token and a `done` as hello parameters.</span></span> <span data-ttu-id="46d1b-168">Hallo-strategie komt weer tooyou nadat deze zijn werk heeft gedaan.</span><span class="sxs-lookup"><span data-stu-id="46d1b-168">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="46d1b-169">Sla Hallo gebruiker en Hallo token niet initialiseren zodat u niet tooask voor het opnieuw hoeft.</span><span class="sxs-lookup"><span data-stu-id="46d1b-169">Store hello user and stash hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="46d1b-170">Hallo voorafgaande code geldt voor alle gebruikers die Hallo-server verifieert.</span><span class="sxs-lookup"><span data-stu-id="46d1b-170">hello preceding code takes all users whom hello server authenticates.</span></span> <span data-ttu-id="46d1b-171">Dit is automatische registratie.</span><span class="sxs-lookup"><span data-stu-id="46d1b-171">This is autoregistration.</span></span> <span data-ttu-id="46d1b-172">Wanneer u productieservers gebruikt, kunt u toolet gebruikers niet wilt, tenzij ze een registratieproces die u hebt ingesteld hebben doorlopen.</span><span class="sxs-lookup"><span data-stu-id="46d1b-172">When you use production servers, you don’t want toolet in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="46d1b-173">U ziet dit patroon vaak in consumenten-apps.</span><span class="sxs-lookup"><span data-stu-id="46d1b-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="46d1b-174">Hiermee kunt u tooregister via Facebook, maar vervolgens zij vraagt u toofill aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="46d1b-174">These allow you tooregister by using Facebook, but then they ask you toofill out additional information.</span></span> <span data-ttu-id="46d1b-175">Als de toepassing geen voorbeeld, kunnen we een e-mailadres extraheren uit Hallo Tokenobject dat wordt geretourneerd en vervolgens vraagt u Hallo gebruiker toofill aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="46d1b-175">If our application wasn’t a sample, we could extract an email address from hello token object that is returned, and then ask hello user toofill out additional information.</span></span> <span data-ttu-id="46d1b-176">Omdat dit een testserver, toevoegen we gewoon gebruikers toohello in-memory database.</span><span class="sxs-lookup"><span data-stu-id="46d1b-176">Because this is a test server, we simply add users toohello in-memory database.</span></span>

<span data-ttu-id="46d1b-177">Voeg Hallo methoden waarmee u tookeep bijhouden van gebruikers die zijn aangemeld, zoals wordt vereist door Passport.</span><span class="sxs-lookup"><span data-stu-id="46d1b-177">Add hello methods that allow you tookeep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="46d1b-178">Dit omvat het serialiseren en deserialiseren van gebruikersgegevens:</span><span class="sxs-lookup"><span data-stu-id="46d1b-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
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

<span data-ttu-id="46d1b-179">Hallo code tooload Hallo Express-engine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="46d1b-179">Add hello code tooload hello Express engine.</span></span> <span data-ttu-id="46d1b-180">In de volgende hello, ziet u dat we de standaard Hallo gebruiken `/views` en `/routes` patroon dat Express biedt.</span><span class="sxs-lookup"><span data-stu-id="46d1b-180">In hello following, you can see that we use hello default `/views` and `/routes` pattern that Express provides.</span></span>

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
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="46d1b-181">Hallo toevoegen `POST` routes die aanlevert Hallo werkelijke aanmelden aanvragen toohello `passport-azure-ad` engine:</span><span class="sxs-lookup"><span data-stu-id="46d1b-181">Add hello `POST` routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="46d1b-182">Passport tooissue aanmelden en afmelden aanvragen tooAzure AD gebruiken</span><span class="sxs-lookup"><span data-stu-id="46d1b-182">Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>

<span data-ttu-id="46d1b-183">Uw app is nu correct geconfigureerde toocommunicate met Hallo v2.0-eindpunt met behulp van Hallo OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="46d1b-183">Your app is now properly configured toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="46d1b-184">`passport-azure-ad`heeft gezorgd voor Hallo details van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van de gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="46d1b-184">`passport-azure-ad` has taken care of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="46d1b-185">Alles wat blijft toogive is uw gebruikers een manier toosign in en meld u out en toogather aanvullende informatie over gebruikers die zich hebben aangemeld.</span><span class="sxs-lookup"><span data-stu-id="46d1b-185">All that remains is toogive your users a way toosign in and sign out, and toogather additional information on users who have signed in.</span></span>

<span data-ttu-id="46d1b-186">Voeg eerst Hallo standaard, aanmelden, account en afmeldingsmethoden toe tooyour `app.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="46d1b-186">First, add hello default, sign-in, account, and sign-out methods tooyour `app.js` file:</span></span>

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
    log.info('Login was called in hello Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="46d1b-187">tooreview informatie over deze methoden:</span><span class="sxs-lookup"><span data-stu-id="46d1b-187">tooreview these methods in detail:</span></span>
- <span data-ttu-id="46d1b-188">Hallo `/` route leidt toohello `index.ejs` weergeven per gebruiker Hallo doorgeven in Hallo-aanvraag (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="46d1b-188">hello `/` route redirects toohello `index.ejs` view by passing hello user in hello request (if it exists).</span></span>
- <span data-ttu-id="46d1b-189">Hallo `/account` route wordt eerst gecontroleerd of u bent geverifieerd (Hallo implementatie voor deze bewerking hieronder is).</span><span class="sxs-lookup"><span data-stu-id="46d1b-189">hello `/account` route first verifies that you are authenticated (hello implementation for this is below).</span></span> <span data-ttu-id="46d1b-190">Deze worden vervolgens doorgegeven Hallo gebruiker in de aanvraag Hallo zodat u aanvullende informatie over het Hallo-gebruiker kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="46d1b-190">It then passes hello user in hello request so that you can get additional information about hello user.</span></span>
- <span data-ttu-id="46d1b-191">Hallo `/login` route aanroepen Hallo `azuread-openidconnect` verificator van `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="46d1b-191">hello `/login` route calls hello `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="46d1b-192">Als dit niet lukt, leidt Hallo route Hallo gebruiker terug te`/login`.</span><span class="sxs-lookup"><span data-stu-id="46d1b-192">If it doesn't succeed, hello route redirects hello user back too`/login`.</span></span>
- <span data-ttu-id="46d1b-193">`/logout` roept `logout.ejs` aan (en de bijbehorende route).</span><span class="sxs-lookup"><span data-stu-id="46d1b-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="46d1b-194">Hiermee worden cookies en vervolgens retourneert gebruiker terug te Hallo`index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="46d1b-194">This clears cookies and then returns hello user back too`index.ejs`.</span></span>


<span data-ttu-id="46d1b-195">Voor het laatste deel van Hallo `app.js`, Hallo toevoegen `EnsureAuthenticated` methode die wordt gebruikt in Hallo `/account` route.</span><span class="sxs-lookup"><span data-stu-id="46d1b-195">For hello last part of `app.js`, add hello `EnsureAuthenticated` method that is used in hello `/account` route.</span></span>

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="46d1b-196">Maak ten slotte Hallo-server zelf in `app.js`.</span><span class="sxs-lookup"><span data-stu-id="46d1b-196">Finally, create hello server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a><span data-ttu-id="46d1b-197">Hallo weergaven maken en het beleid van routes in Express toocall</span><span class="sxs-lookup"><span data-stu-id="46d1b-197">Create hello views and routes in Express toocall your policies</span></span>

<span data-ttu-id="46d1b-198">Uw `app.js` is nu voltooid.</span><span class="sxs-lookup"><span data-stu-id="46d1b-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="46d1b-199">U hoeft alleen maar tooadd Hallo routes en weergaven waarmee u toocall Hallo beleid voor aanmelden en registreren.</span><span class="sxs-lookup"><span data-stu-id="46d1b-199">You just need tooadd hello routes and views that allow you toocall hello sign-in and sign-up policies.</span></span> <span data-ttu-id="46d1b-200">Deze ook Hallo afhandelen `/logout` en `/login` routes die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46d1b-200">These also handle hello `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="46d1b-201">Hallo maken `/routes/index.js` route onder Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="46d1b-201">Create hello `/routes/index.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="46d1b-202">Hallo maken `/routes/user.js` route onder Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="46d1b-202">Create hello `/routes/user.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="46d1b-203">Deze eenvoudige routes doorgegeven aanvragen tooyour weergaven.</span><span class="sxs-lookup"><span data-stu-id="46d1b-203">These simple routes pass along requests tooyour views.</span></span> <span data-ttu-id="46d1b-204">Ze bevatten Hallo gebruiker, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="46d1b-204">They include hello user, if one is present.</span></span>

<span data-ttu-id="46d1b-205">Hallo maken `/views/index.ejs` weergave onder Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="46d1b-205">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="46d1b-206">Dit is een eenvoudige pagina waarmee beleid voor aanmelden en afmelden wordt aangeroepen. U kunt ook gebruiken deze toograb accountgegevens.</span><span class="sxs-lookup"><span data-stu-id="46d1b-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it toograb account information.</span></span> <span data-ttu-id="46d1b-207">Opmerking waarmee u voorwaardelijke Hallo kunt `if (!user)` zoals Hallo gebruiker wordt doorgegeven in Hallo aanvraag tooprovide bewijsmateriaal die Hallo-gebruiker is aangemeld.</span><span class="sxs-lookup"><span data-stu-id="46d1b-207">Note that you can use hello conditional `if (!user)` as hello user is passed through in hello request tooprovide evidence that hello user is signed in.</span></span>

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

<span data-ttu-id="46d1b-208">Hallo maken `/views/account.ejs` weergeven onder de hoofdmap hello, zodat u kunt aanvullende informatie weergeven die `passport-azure-ad` plaatsen in de gebruikersaanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="46d1b-208">Create hello `/views/account.ejs` view under hello root directory so that you can view additional information that `passport-azure-ad` put in hello user request.</span></span>

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

<span data-ttu-id="46d1b-209">U kunt nu uw app bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="46d1b-209">You can now build and run your app.</span></span>

<span data-ttu-id="46d1b-210">Voer `node app.js` en te navigeren`http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="46d1b-210">Run `node app.js` and navigate too`http://localhost:3000`</span></span>


<span data-ttu-id="46d1b-211">Registreren of aanmelden toohello app via e-mail of Facebook.</span><span class="sxs-lookup"><span data-stu-id="46d1b-211">Sign up or sign in toohello app by using email or Facebook.</span></span> <span data-ttu-id="46d1b-212">Meld u af en meld u weer aan als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="46d1b-212">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="46d1b-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46d1b-213">Next steps</span></span>

<span data-ttu-id="46d1b-214">Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [wordt geleverd als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="46d1b-214">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="46d1b-215">U kunt dit ook klonen van GitHub:</span><span class="sxs-lookup"><span data-stu-id="46d1b-215">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="46d1b-216">U kunt nu op toomore geavanceerde onderwerpen verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="46d1b-216">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="46d1b-217">U kunt het volgende proberen:</span><span class="sxs-lookup"><span data-stu-id="46d1b-217">You might try:</span></span>

[<span data-ttu-id="46d1b-218">Een web-API beveiligen met behulp van Hallo B2C-model in Node.js</span><span class="sxs-lookup"><span data-stu-id="46d1b-218">Secure a web API by using hello B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
