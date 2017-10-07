---
title: Active Directory-v2.0 aaaAzure Node.js web-app aanmelden | Microsoft Docs
description: Meer informatie over hoe toobuild een Node.js web-app die een gebruiker zich aanmeldt met behulp van zowel een persoonlijk Microsoft-account en een account voor werk of school.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="9800b-103">Aanmelden tooa Node.js-web-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="9800b-103">Add sign-in tooa Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="9800b-104">Niet alle Azure Active Directory-scenario's en onderdelen werken met Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="9800b-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="9800b-105">toodetermine of moet u Hallo v2.0-eindpunt of Hallo v1.0 eindpunt, gelezen over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="9800b-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="9800b-106">In deze zelfstudie gebruiken we Passport toodo Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="9800b-106">In this tutorial, we use Passport toodo hello following tasks:</span></span>

* <span data-ttu-id="9800b-107">Hallo-gebruiker aanmelden via Azure Active Directory (Azure AD) in een web-app en Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="9800b-107">In a web app, sign in hello user by using Azure Active Directory (Azure AD) and hello v2.0 endpoint.</span></span>
* <span data-ttu-id="9800b-108">Informatie over Hallo gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9800b-108">Display information about hello user.</span></span>
* <span data-ttu-id="9800b-109">Meld u Hallo gebruiker buiten het Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="9800b-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="9800b-110">**Passport** is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="9800b-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="9800b-111">Flexibel en modulair, Passport kan onopvallend worden verwijderd in een snelle gebaseerde of restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="9800b-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="9800b-112">In Passport, een uitgebreide set strategieën ondersteuning voor verificatie met behulp van een gebruikersnaam en wachtwoord, Facebook, Twitter of andere opties.</span><span class="sxs-lookup"><span data-stu-id="9800b-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="9800b-113">We hebben een strategie ontwikkeld voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9800b-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="9800b-114">In dit artikel we u zien hoe tooinstall Hallo module en voeg vervolgens hello Azure AD `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="9800b-114">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="9800b-115">Downloaden</span><span class="sxs-lookup"><span data-stu-id="9800b-115">Download</span></span>
<span data-ttu-id="9800b-116">Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="9800b-116">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="9800b-117">toofollow hello zelfstudie, kunt u [basis van Hallo app downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) of kloon Hallo basisproject:</span><span class="sxs-lookup"><span data-stu-id="9800b-117">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="9800b-118">U kunt ook de toepassing hello voltooid op Hallo einde van deze zelfstudie ophalen.</span><span class="sxs-lookup"><span data-stu-id="9800b-118">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="9800b-119">1: een app registreren</span><span class="sxs-lookup"><span data-stu-id="9800b-119">1: Register an app</span></span>
<span data-ttu-id="9800b-120">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of voert u [deze gedetailleerde stappen](active-directory-v2-app-registration.md) tooregister een app.</span><span class="sxs-lookup"><span data-stu-id="9800b-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="9800b-121">Zorg ervoor dat u:</span><span class="sxs-lookup"><span data-stu-id="9800b-121">Make sure you:</span></span>

* <span data-ttu-id="9800b-122">Kopiëren Hallo **toepassings-Id** tooyour app toegewezen.</span><span class="sxs-lookup"><span data-stu-id="9800b-122">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="9800b-123">U moet voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="9800b-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="9800b-124">Hallo toevoegen **Web** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="9800b-124">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="9800b-125">Kopiëren Hallo **omleidings-URI** van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="9800b-125">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="9800b-126">Moet u Hallo standaardwaarde URI van `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="9800b-126">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-tooyour-directory"></a><span data-ttu-id="9800b-127">2: prerequisities tooyour map toevoegen</span><span class="sxs-lookup"><span data-stu-id="9800b-127">2: Add prerequisities tooyour directory</span></span>
<span data-ttu-id="9800b-128">Bij een opdrachtprompt mappen toogo tooyour hoofdmap niet wijzigen als u nog geen er.</span><span class="sxs-lookup"><span data-stu-id="9800b-128">At a command prompt, change directories toogo tooyour root folder, if you are not already there.</span></span> <span data-ttu-id="9800b-129">Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="9800b-129">Run hello following commands:</span></span>

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

<span data-ttu-id="9800b-130">Daarnaast gebruiken wij `passport-azure-ad` in Hallo geraamte van Hallo Quick Start:</span><span class="sxs-lookup"><span data-stu-id="9800b-130">In addition, we use `passport-azure-ad` in hello skeleton of hello quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="9800b-131">Hiermee installeert u Hallo bibliotheken die `passport-azure-ad` gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9800b-131">This installs hello libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="9800b-132">3: uw app toouse Hallo passport-knooppunt-js strategie instellen</span><span class="sxs-lookup"><span data-stu-id="9800b-132">3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="9800b-133">Hallo Express-middleware toouse hello OpenID Connect-verificatieprotocol instellen.</span><span class="sxs-lookup"><span data-stu-id="9800b-133">Set up hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="9800b-134">U gebruikt Passport tooissue aanmelden en afmeldingsaanvragen te verzenden, Hallo gebruikerssessie beheren en informatie ophalen over de gebruiker hello, onder andere.</span><span class="sxs-lookup"><span data-stu-id="9800b-134">You use Passport tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, among other things.</span></span>

1.  <span data-ttu-id="9800b-135">Open in de hoofdmap van de Hallo van Hallo-project, Hallo bestand Config.js file.</span><span class="sxs-lookup"><span data-stu-id="9800b-135">In hello root of hello project, open hello Config.js file.</span></span> <span data-ttu-id="9800b-136">In Hallo `exports.creds` sectie, voert u de configuratiewaarden van uw app.</span><span class="sxs-lookup"><span data-stu-id="9800b-136">In hello `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="9800b-137">`clientID`: Hallo **toepassings-Id** die is toegewezen tooyour-app in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9800b-137">`clientID`: hello **Application Id** that's assigned tooyour app in hello Azure portal.</span></span>
  * <span data-ttu-id="9800b-138">`returnURL`: Hallo **omleidings-URI** die u hebt ingevoerd in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="9800b-138">`returnURL`: hello **Redirect URI** that you entered in hello portal.</span></span>
  * <span data-ttu-id="9800b-139">`clientSecret`: Hallo geheim dat u hebt gegenereerd in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="9800b-139">`clientSecret`: hello secret that you generated in hello portal.</span></span>

2.  <span data-ttu-id="9800b-140">In de hoofdmap van de Hallo van Hallo-project, Hallo App.js bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="9800b-140">In hello root of hello project, open hello App.js file.</span></span> <span data-ttu-id="9800b-141">tooinvoke hello OIDCStrategy stratey, wordt geleverd met `passport-azure-ad`, Hallo aanroep volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="9800b-141">tooinvoke hello OIDCStrategy stratey, which comes with `passport-azure-ad`, add hello following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="9800b-142">toohandle uw aanvragen aanmelden gebruik Hallo strategie die u zojuist hebt waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="9800b-142">toohandle your sign-in requests, use hello strategy you just referenced:</span></span>

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
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

<span data-ttu-id="9800b-143">Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="9800b-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="9800b-144">Alle schrijvers van strategieën toohello patroon.</span><span class="sxs-lookup"><span data-stu-id="9800b-144">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="9800b-145">Hallo-strategie doorgeven een `function()` die gebruikmaakt van een token en `done` als parameters.</span><span class="sxs-lookup"><span data-stu-id="9800b-145">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="9800b-146">Hallo-strategie terug nadat al het werk wordt.</span><span class="sxs-lookup"><span data-stu-id="9800b-146">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="9800b-147">Hallo-gebruiker en stash Hallo token opslaan zodat u niet tooask voor het opnieuw hoeft.</span><span class="sxs-lookup"><span data-stu-id="9800b-147">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9800b-148">Hallo voorafgaande code geldt voor elke gebruiker die tooyour server kan worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="9800b-148">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="9800b-149">Dit wordt automatische registratie genoemd.</span><span class="sxs-lookup"><span data-stu-id="9800b-149">This is known as auto-registration.</span></span> <span data-ttu-id="9800b-150">Op een productieserver je wilt niet dat toolet iedereen zonder dat zij een registratieproces die u kiest doorlopen eerst.</span><span class="sxs-lookup"><span data-stu-id="9800b-150">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="9800b-151">Dit is meestal Hallo patroon die u in consumenten-apps ziet.</span><span class="sxs-lookup"><span data-stu-id="9800b-151">This is usually hello pattern that you see in consumer apps.</span></span> <span data-ttu-id="9800b-152">Hallo-app kunt u mogelijk tooregister met Facebook, maar vervolgens wordt u gevraagd een tooenter aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="9800b-152">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="9800b-153">Als u een opdrachtregelprogramma zijn niet voor deze zelfstudie gebruikt, kan u Hallo e extraheren uit Hallo Tokenobject dat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9800b-153">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="9800b-154">Vervolgens vraagt u mogelijk Hallo gebruiker tooenter aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="9800b-154">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="9800b-155">Omdat dit een testserver is, u Hallo gebruiker toevoegen rechtstreeks toohello de database in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="9800b-155">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="9800b-156">Voeg Hallo methoden tookeep bijhouden van gebruikers die zijn ondertekend, te gebruiken zoals wordt vereist door Passport.</span><span class="sxs-lookup"><span data-stu-id="9800b-156">Add hello methods that you use tookeep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="9800b-157">Dit omvat het serialiseren en deserialiseren van Hallo gebruikersgegevens:</span><span class="sxs-lookup"><span data-stu-id="9800b-157">This includes serializing and deserializing hello user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
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

5.  <span data-ttu-id="9800b-158">Voeg code Hallo Hallo Express-engine wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="9800b-158">Add hello code that loads hello Express engine.</span></span> <span data-ttu-id="9800b-159">Gebruik van Hallo standaard /views en /routes patroon dat Express:</span><span class="sxs-lookup"><span data-stu-id="9800b-159">You use hello default /views and /routes pattern that Express provides:</span></span>

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="9800b-160">Hallo POST routes die lever Hallo werkelijke aanmelden aanvragen toohello toevoegen `passport-azure-ad` engine:</span><span class="sxs-lookup"><span data-stu-id="9800b-160">Add hello POST routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="9800b-161">4: gebruik Passport tooissue aan- en afmeldingsaanvragen tooAzure AD-aanvragen</span><span class="sxs-lookup"><span data-stu-id="9800b-161">4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="9800b-162">Uw app is nu ingesteld toocommunicate met Hallo v2.0-eindpunt met behulp van Hallo OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="9800b-162">Your app is now set up toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="9800b-163">Hallo `passport-azure-ad` strategie zorgt voor alle Hallo details van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van Hallo gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="9800b-163">hello `passport-azure-ad` strategy takes care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining hello user session.</span></span> <span data-ttu-id="9800b-164">Alle die altijd is ingeschakeld toodo toogive is uw gebruikers een manier toosign in en meld u out en toogather meer informatie over het Hallo-gebruiker die is aangemeld.</span><span class="sxs-lookup"><span data-stu-id="9800b-164">All that is left toodo is toogive your users a way toosign in and sign out, and toogather more information about hello user who is signed in.</span></span>

1.  <span data-ttu-id="9800b-165">Hallo toevoegen **standaard**, **aanmelding**, **account**, en **afmelding** methoden tooyour App.js bestand:</span><span class="sxs-lookup"><span data-stu-id="9800b-165">Add hello **default**, **login**, **account**, and **logout** methods tooyour App.js file:</span></span>

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="9800b-166">Dit zijn Hallo details:</span><span class="sxs-lookup"><span data-stu-id="9800b-166">Here are hello details:</span></span>
    
    * <span data-ttu-id="9800b-167">Hallo `/` route toohello index.ejs weergave wordt omgeleid.</span><span class="sxs-lookup"><span data-stu-id="9800b-167">hello `/` route redirects toohello index.ejs view.</span></span> <span data-ttu-id="9800b-168">Dit wordt Hallo gebruiker doorgegeven in Hallo-aanvraag (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="9800b-168">It passes hello user in hello request (if it exists).</span></span>
    * <span data-ttu-id="9800b-169">Hallo `/account` eerst routeren *zorgt ervoor dat u bent geverifieerd* (u implementeert die in de volgende code Hallo).</span><span class="sxs-lookup"><span data-stu-id="9800b-169">hello `/account` route first *ensures that you are authenticated* (you implement that in hello following code).</span></span> <span data-ttu-id="9800b-170">Hallo-gebruiker wordt vervolgens doorgegeven in Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="9800b-170">Then, it passes hello user in hello request.</span></span> <span data-ttu-id="9800b-171">Dit is zodat u meer informatie over gebruikers Hallo krijgt.</span><span class="sxs-lookup"><span data-stu-id="9800b-171">This is so you can get more information about hello user.</span></span>
    * <span data-ttu-id="9800b-172">Hallo `/login` gesprekken rondsturen uw `azuread-openidconnect` verificator van `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="9800b-172">hello `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="9800b-173">Als dat niet lukt, wordt hij omgeleid Hallo gebruiker terug te`/login`.</span><span class="sxs-lookup"><span data-stu-id="9800b-173">If that doesn't succeed, it redirects hello user back too`/login`.</span></span>
    * <span data-ttu-id="9800b-174">Hallo `/logout` route roept Hallo logout.ejs weergeven (en route).</span><span class="sxs-lookup"><span data-stu-id="9800b-174">hello `/logout` route calls hello logout.ejs view (and route).</span></span> <span data-ttu-id="9800b-175">Hiermee worden cookies en vervolgens retourneert Hallo back tooindex.ejs gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9800b-175">This clears cookies, and then returns hello user back tooindex.ejs.</span></span>

2.  <span data-ttu-id="9800b-176">Hallo toevoegen **EnsureAuthenticated** methode die u eerder in gebruikt `/account`:</span><span class="sxs-lookup"><span data-stu-id="9800b-176">Add hello **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="9800b-177">Maak in App.js, Hallo-server:</span><span class="sxs-lookup"><span data-stu-id="9800b-177">In App.js, create hello server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a><span data-ttu-id="9800b-178">5: Hallo weergaven en routes in Express dat u uw gebruikers worden weergegeven op Hallo website maken</span><span class="sxs-lookup"><span data-stu-id="9800b-178">5: Create hello views and routes in Express that you show your user on hello website</span></span>
<span data-ttu-id="9800b-179">Hallo routes en weergaven waarin informatie toohello gebruiker toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9800b-179">Add hello routes and views that show information toohello user.</span></span> <span data-ttu-id="9800b-180">Hallo routes en weergaven ook Hallo afhandelen `/logout` en `/login` routes die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9800b-180">hello routes and views also handle hello `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="9800b-181">Maken in de hoofdmap hello, Hallo `/routes/index.js` route.</span><span class="sxs-lookup"><span data-stu-id="9800b-181">In hello root directory, create hello `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="9800b-182">Maken in de hoofdmap hello, Hallo `/routes/user.js` route.</span><span class="sxs-lookup"><span data-stu-id="9800b-182">In hello root directory, create hello `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="9800b-183">`/routes/index.js`en `/routes/user.js` zijn eenvoudige routes die Hallo aanvraag tooyour weergaven doorgegeven, met inbegrip van Hallo gebruiker, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="9800b-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along hello request tooyour views, including hello user, if present.</span></span>

3.  <span data-ttu-id="9800b-184">Maken in de hoofdmap hello, Hallo `/views/index.ejs` weergeven.</span><span class="sxs-lookup"><span data-stu-id="9800b-184">In hello root directory, create hello `/views/index.ejs` view.</span></span> <span data-ttu-id="9800b-185">Deze pagina roept de **aanmelding** en **afmelding** methoden.</span><span class="sxs-lookup"><span data-stu-id="9800b-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="9800b-186">U ook hello gebruiken `/views/index.ejs` toocapture accountgegevens te bekijken.</span><span class="sxs-lookup"><span data-stu-id="9800b-186">You also use hello `/views/index.ejs` view toocapture account information.</span></span> <span data-ttu-id="9800b-187">U kunt voorwaardelijke Hallo `if (!user)` als Hallo-gebruiker in Hallo-aanvraag wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="9800b-187">You can use hello conditional `if (!user)` as hello user being passed through in hello request.</span></span> <span data-ttu-id="9800b-188">Het is bewijs dat u een gebruiker aangemeld hebt.</span><span class="sxs-lookup"><span data-stu-id="9800b-188">It is evidence that you have a user signed in.</span></span>

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  <span data-ttu-id="9800b-189">Maken in de hoofdmap hello, Hallo `/views/account.ejs` weergeven.</span><span class="sxs-lookup"><span data-stu-id="9800b-189">In hello root directory, create hello `/views/account.ejs` view.</span></span> <span data-ttu-id="9800b-190">Hallo `/views/account.ejs` weergave kunt u aanvullende informatie tooview die `passport-azuread` worden geplaatst in de gebruikersaanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="9800b-190">hello `/views/account.ejs` view allows you tooview additional information that `passport-azuread` puts in hello user request.</span></span>

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
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  <span data-ttu-id="9800b-191">Toevoegen van een lay-out.</span><span class="sxs-lookup"><span data-stu-id="9800b-191">Add a layout.</span></span> <span data-ttu-id="9800b-192">Maken in de hoofdmap hello, Hallo `/views/layout.ejs` weergeven.</span><span class="sxs-lookup"><span data-stu-id="9800b-192">In hello root directory, create hello `/views/layout.ejs` view.</span></span>

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  <span data-ttu-id="9800b-193">toobuild en uitvoeren van uw app uitvoeren `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="9800b-193">toobuild and run your app, run `node app.js`.</span></span> <span data-ttu-id="9800b-194">Ga vervolgens te`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="9800b-194">Then, go too`http://localhost:3000`.</span></span>

7.  <span data-ttu-id="9800b-195">Aanmelden met een persoonlijk Microsoft-account of een account voor werk of school.</span><span class="sxs-lookup"><span data-stu-id="9800b-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="9800b-196">Houd er rekening mee dat de identiteit van de gebruiker Hallo worden weerspiegeld in Hallo /account lijst.</span><span class="sxs-lookup"><span data-stu-id="9800b-196">Note that hello user's identity is reflected in hello /account list.</span></span> 

<span data-ttu-id="9800b-197">U hebt nu een web-app die is beveiligd met behulp van protocollen volgens de industrienorm.</span><span class="sxs-lookup"><span data-stu-id="9800b-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="9800b-198">U kunt gebruikers in uw app verifiëren met behulp van hun persoonlijke en werk of school-account.</span><span class="sxs-lookup"><span data-stu-id="9800b-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9800b-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9800b-199">Next steps</span></span>
<span data-ttu-id="9800b-200">Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) wordt geleverd als [een ZIP-bestand](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="9800b-200">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="9800b-201">U kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="9800b-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="9800b-202">Vervolgens kunt u op toomore geavanceerde onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="9800b-202">Next, you can move on toomore advanced topics.</span></span> <span data-ttu-id="9800b-203">U kunt tootry:</span><span class="sxs-lookup"><span data-stu-id="9800b-203">You might want tootry:</span></span>

[<span data-ttu-id="9800b-204">Een Node.js-web-API beveiligen met behulp van Hallo v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="9800b-204">Secure a Node.js web API by using hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="9800b-205">Hier volgen enkele aanvullende resources:</span><span class="sxs-lookup"><span data-stu-id="9800b-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="9800b-206">Handleiding voor Azure AD v2.0-ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="9800b-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="9800b-207">Stack-overloop 'azure active directory' tag</span><span class="sxs-lookup"><span data-stu-id="9800b-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="9800b-208">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="9800b-208">Get security updates for our products</span></span>
<span data-ttu-id="9800b-209">We raden u toosign up toobe een melding wanneer er beveiligingsincidenten optreden.</span><span class="sxs-lookup"><span data-stu-id="9800b-209">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="9800b-210">Op Hallo [Microsoft technische beveiligingsmeldingen](https://technet.microsoft.com/security/dd252948) pagina moet u zich abonneren tooSecurity adviezen waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="9800b-210">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

