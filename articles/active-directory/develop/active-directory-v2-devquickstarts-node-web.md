---
title: Azure Active Directory-v2.0 Node.js web-app aanmelden | Microsoft Docs
description: Informatie over het bouwen van een Node.js-web-app die een gebruiker zich aanmeldt met behulp van zowel een persoonlijk Microsoft-account en een account voor werk of school.
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
ms.openlocfilehash: 6d49c742f72440e22830915c90de009d9188db2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="d6cfc-103">Aanmelden toevoegen aan een Node.js-web-app</span><span class="sxs-lookup"><span data-stu-id="d6cfc-103">Add sign-in to a Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="d6cfc-104">Niet alle Azure Active Directory-scenario's en onderdelen werken met het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="d6cfc-105">Meer informatie over om te bepalen of u het v2.0-eindpunt of het eindpunt v1.0 moet gebruiken, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d6cfc-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="d6cfc-106">In deze zelfstudie gebruiken we Passport naar de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-106">In this tutorial, we use Passport to do the following tasks:</span></span>

* <span data-ttu-id="d6cfc-107">Meld u de gebruiker met behulp van Azure Active Directory (Azure AD) en het v2.0-eindpunt in een web-app.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-107">In a web app, sign in the user by using Azure Active Directory (Azure AD) and the v2.0 endpoint.</span></span>
* <span data-ttu-id="d6cfc-108">Informatie over de gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-108">Display information about the user.</span></span>
* <span data-ttu-id="d6cfc-109">Meld u aan de gebruiker buiten de app.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-109">Sign the user out of the app.</span></span>

<span data-ttu-id="d6cfc-110">**Passport** is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="d6cfc-111">Flexibel en modulair, Passport kan onopvallend worden verwijderd in een snelle gebaseerde of restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="d6cfc-112">In Passport, een uitgebreide set strategieën ondersteuning voor verificatie met behulp van een gebruikersnaam en wachtwoord, Facebook, Twitter of andere opties.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="d6cfc-113">We hebben een strategie ontwikkeld voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="d6cfc-114">In dit artikel wordt beschreven hoe u installeert de module en voegt u de Azure AD `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-114">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="d6cfc-115">Downloaden</span><span class="sxs-lookup"><span data-stu-id="d6cfc-115">Download</span></span>
<span data-ttu-id="d6cfc-116">De code voor deze zelfstudie wordt onderhouden in [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="d6cfc-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="d6cfc-117">Wilt u de zelfstudie, kunt u [basis van de app downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) of het geraamte:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-117">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="d6cfc-118">U kunt ook de voltooide toepassing aan het einde van deze zelfstudie ophalen.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-118">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="d6cfc-119">1: een app registreren</span><span class="sxs-lookup"><span data-stu-id="d6cfc-119">1: Register an app</span></span>
<span data-ttu-id="d6cfc-120">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of voert u [deze gedetailleerde stappen](active-directory-v2-app-registration.md) om een app te registreren.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="d6cfc-121">Zorg ervoor dat u:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-121">Make sure you:</span></span>

* <span data-ttu-id="d6cfc-122">Kopieer de **toepassings-Id** toegewezen aan uw app.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-122">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="d6cfc-123">U moet voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="d6cfc-124">Voeg de **Web** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-124">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="d6cfc-125">Kopieer de **omleidings-URI** vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-125">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="d6cfc-126">Moet u de standaardwaarde van de URI van `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-126">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-to-your-directory"></a><span data-ttu-id="d6cfc-127">2: prerequisities toevoegen aan uw directory</span><span class="sxs-lookup"><span data-stu-id="d6cfc-127">2: Add prerequisities to your directory</span></span>
<span data-ttu-id="d6cfc-128">Bij een opdrachtprompt, wijzig de mappen naar de hoofdmap, als u niet al er.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-128">At a command prompt, change directories to go to your root folder, if you are not already there.</span></span> <span data-ttu-id="d6cfc-129">Voer de volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-129">Run the following commands:</span></span>

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

<span data-ttu-id="d6cfc-130">Daarnaast gebruiken wij `passport-azure-ad` in de basis van de Snelstartgids:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-130">In addition, we use `passport-azure-ad` in the skeleton of the quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="d6cfc-131">Hiermee installeert u de bibliotheken die `passport-azure-ad` gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-131">This installs the libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="d6cfc-132">3: uw app instellen voor gebruik van de strategie passport-knooppunt-js</span><span class="sxs-lookup"><span data-stu-id="d6cfc-132">3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="d6cfc-133">De Express-middleware instellen voor gebruik van het OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-133">Set up the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="d6cfc-134">U kunt Passport aan- en afmeldingsaanvragen te verzenden en informatie ophalen over de gebruiker, onder andere de gebruikerssessie te beheren.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-134">You use Passport to issue sign-in and sign-out requests, manage the user's session, and get information about the user, among other things.</span></span>

1.  <span data-ttu-id="d6cfc-135">Open het bestand Config.js file in de hoofdmap van het project.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-135">In the root of the project, open the Config.js file.</span></span> <span data-ttu-id="d6cfc-136">In de `exports.creds` sectie, voert u de configuratiewaarden van uw app.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-136">In the `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="d6cfc-137">`clientID`: De **toepassings-Id** die toegewezen aan uw app in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-137">`clientID`: The **Application Id** that's assigned to your app in the Azure portal.</span></span>
  * <span data-ttu-id="d6cfc-138">`returnURL`: De **omleidings-URI** die u hebt ingevoerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-138">`returnURL`: The **Redirect URI** that you entered in the portal.</span></span>
  * <span data-ttu-id="d6cfc-139">`clientSecret`: Het geheim dat u hebt gegenereerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-139">`clientSecret`: The secret that you generated in the portal.</span></span>

2.  <span data-ttu-id="d6cfc-140">Open het bestand App.js in de hoofdmap van het project.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-140">In the root of the project, open the App.js file.</span></span> <span data-ttu-id="d6cfc-141">Om aan te roepen de stratey OIDCStrategy, wordt geleverd met `passport-azure-ad`, voeg de volgende oproep verzenden:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-141">To invoke the OIDCStrategy stratey, which comes with `passport-azure-ad`, add the following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="d6cfc-142">Gebruik de strategie die u zojuist hebt om uw aanmelding verzoeken afhandelen waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-142">To handle your sign-in requests, use the strategy you just referenced:</span></span>

  ```JavaScript
  // Use the OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. The function accepts
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

<span data-ttu-id="d6cfc-143">Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="d6cfc-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="d6cfc-144">Alle schrijvers van strategieën voor het patroon.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-144">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="d6cfc-145">Geeft de strategie voor een `function()` die gebruikmaakt van een token en `done` als parameters.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-145">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="d6cfc-146">De strategie terug nadat al het werk wordt.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-146">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="d6cfc-147">Sla de gebruiker en het token niet initialiseren zodat u niet hoeft te vragen voor het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-147">Store the user and stash the token so you don’t need to ask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d6cfc-148">De voorafgaande code geldt voor elke gebruiker die kan worden geverifieerd met de server.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-148">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="d6cfc-149">Dit wordt automatische registratie genoemd.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-149">This is known as auto-registration.</span></span> <span data-ttu-id="d6cfc-150">Op een productieserver wilt u niet dat iedereen, kunnen zonder dat zij een registratieproces die u kiest doorlopen eerst.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-150">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="d6cfc-151">Dit is doorgaans het patroon die u in consumenten-apps ziet.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-151">This is usually the pattern that you see in consumer apps.</span></span> <span data-ttu-id="d6cfc-152">De app kunt u mogelijk registreren met Facebook, maar vervolgens wordt u gevraagd om in te voeren als u meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-152">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="d6cfc-153">Als u een opdrachtregelprogramma zijn niet voor deze zelfstudie gebruikt, kunt u het e-mailbericht kan extraheren uit het Tokenobject dat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-153">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="d6cfc-154">Vervolgens vraagt u mogelijk de gebruiker in te voeren als u meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-154">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="d6cfc-155">Omdat dit een testserver is, moet u de gebruiker rechtstreeks naar de database in het geheugen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-155">Because this is a test server, you add the user directly to the in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="d6cfc-156">Voeg de methoden die u gebruikt voor het bijhouden van gebruikers die zijn aangemeld, zoals wordt vereist door Passport.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-156">Add the methods that you use to keep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="d6cfc-157">Dit omvat het serialiseren en deserialiseren van gegevens van de gebruiker:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-157">This includes serializing and deserializing the user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   To support persistent login sessions, Passport needs to be able to
  //   serialize users into, and deserialize users out of, the session. Typically,
  //   this is as simple as storing the user ID when serializing, and finding
  //   the user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array to hold signed-in users
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

5.  <span data-ttu-id="d6cfc-158">Voeg de code die de Express-engine wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-158">Add the code that loads the Express engine.</span></span> <span data-ttu-id="d6cfc-159">Gebruik van de standaard /views en /routes patroon dat Express:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-159">You use the default /views and /routes pattern that Express provides:</span></span>

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
    // Initialize Passport!  Also use passport.session() middleware, to support
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="d6cfc-160">Toevoegen van het bericht van routes die lever de werkelijke aanmelden aanvragen voor de `passport-azure-ad` engine:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-160">Add the POST routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. The first step in OpenID authentication involves redirecting
  //   the user to the user's OpenID provider. After authenticating, the OpenID
  //   provider redirects the user back to this application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in the sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called.
  //   In this example, it redirects the user to the home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called. 
  //   In this example, it redirects the user to the home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="d6cfc-161">4: gebruik Passport om aan- en afmeldingsaanvragen te verzenden naar Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6cfc-161">4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="d6cfc-162">Uw app is nu ingesteld om te communiceren met het v2.0-eindpunt met behulp van het OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-162">Your app is now set up to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="d6cfc-163">De `passport-azure-ad` strategie zorgt voor de details van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van de gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-163">The `passport-azure-ad` strategy takes care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining the user session.</span></span> <span data-ttu-id="d6cfc-164">Alle die nog moet doen om uw gebruikers aanmelden en afmelden en meer informatie over de gebruiker die is aangemeld verzamelen is.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-164">All that is left to do is to give your users a way to sign in and sign out, and to gather more information about the user who is signed in.</span></span>

1.  <span data-ttu-id="d6cfc-165">Voeg de **standaard**, **aanmelding**, **account**, en **afmelding** methoden voor het bestand App.js:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-165">Add the **default**, **login**, **account**, and **logout** methods to your App.js file:</span></span>

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
      log.info('Login was called in the sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="d6cfc-166">Hier volgen de details:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-166">Here are the details:</span></span>
    
    * <span data-ttu-id="d6cfc-167">De `/` route wordt omgeleid naar de weergave index.ejs.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-167">The `/` route redirects to the index.ejs view.</span></span> <span data-ttu-id="d6cfc-168">Dit wordt de gebruiker doorgegeven in de aanvraag (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="d6cfc-168">It passes the user in the request (if it exists).</span></span>
    * <span data-ttu-id="d6cfc-169">De `/account` eerst routeren *zorgt ervoor dat u bent geverifieerd* (u implementeert die in de volgende code).</span><span class="sxs-lookup"><span data-stu-id="d6cfc-169">The `/account` route first *ensures that you are authenticated* (you implement that in the following code).</span></span> <span data-ttu-id="d6cfc-170">Vervolgens wordt de gebruiker in de aanvraag doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-170">Then, it passes the user in the request.</span></span> <span data-ttu-id="d6cfc-171">Dit is zodat u meer informatie over de gebruiker krijgt.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-171">This is so you can get more information about the user.</span></span>
    * <span data-ttu-id="d6cfc-172">De `/login` gesprekken rondsturen uw `azuread-openidconnect` verificator van `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-172">The `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="d6cfc-173">Als dat niet lukt, wordt de gebruiker wordt omgeleid naar `/login`.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-173">If that doesn't succeed, it redirects the user back to `/login`.</span></span>
    * <span data-ttu-id="d6cfc-174">De `/logout` route roept de logout.ejs weergeven (en route).</span><span class="sxs-lookup"><span data-stu-id="d6cfc-174">The `/logout` route calls the logout.ejs view (and route).</span></span> <span data-ttu-id="d6cfc-175">Hiermee worden cookies gewist en retourneert vervolgens de gebruiker terug naar index.ejs.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-175">This clears cookies, and then returns the user back to index.ejs.</span></span>

2.  <span data-ttu-id="d6cfc-176">Voeg de **EnsureAuthenticated** methode die u eerder in gebruikt `/account`:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-176">Add the **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware to ensure the user is authenticated (section 4)

  //   Use this route middleware on any resource that needs to be protected. If
  //   the request is authenticated (typically via a persistent login session),
  //   the request proceeds. Otherwise, the user is redirected to the
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="d6cfc-177">Maak in App.js, de server:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-177">In App.js, create the server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-the-views-and-routes-in-express-that-you-show-your-user-on-the-website"></a><span data-ttu-id="d6cfc-178">5: Maak de weergaven en routes in Express dat u uw gebruikers worden weergegeven op de website</span><span class="sxs-lookup"><span data-stu-id="d6cfc-178">5: Create the views and routes in Express that you show your user on the website</span></span>
<span data-ttu-id="d6cfc-179">Voeg de routes en weergaven die aan de gebruiker alleen informatie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-179">Add the routes and views that show information to the user.</span></span> <span data-ttu-id="d6cfc-180">De routes en weergaven verwerken ook de `/logout` en `/login` routes die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-180">The routes and views also handle the `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="d6cfc-181">In de hoofdmap, maken de `/routes/index.js` route.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-181">In the root directory, create the `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="d6cfc-182">In de hoofdmap, maken de `/routes/user.js` route.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-182">In the root directory, create the `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="d6cfc-183">`/routes/index.js`en `/routes/user.js` zijn eenvoudige routes die de aanvraag aan uw weergaven doorgegeven, met inbegrip van de gebruiker, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along the request to your views, including the user, if present.</span></span>

3.  <span data-ttu-id="d6cfc-184">In de hoofdmap, maken de `/views/index.ejs` weergeven.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-184">In the root directory, create the `/views/index.ejs` view.</span></span> <span data-ttu-id="d6cfc-185">Deze pagina roept de **aanmelding** en **afmelding** methoden.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="d6cfc-186">Ook gebruiken de `/views/index.ejs` weergave voor het vastleggen van gegevens van het account.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-186">You also use the `/views/index.ejs` view to capture account information.</span></span> <span data-ttu-id="d6cfc-187">U kunt de voorwaardelijke `if (!user)` als de gebruiker in de aanvraag wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-187">You can use the conditional `if (!user)` as the user being passed through in the request.</span></span> <span data-ttu-id="d6cfc-188">Het is bewijs dat u een gebruiker aangemeld hebt.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="d6cfc-189">In de hoofdmap, maken de `/views/account.ejs` weergeven.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-189">In the root directory, create the `/views/account.ejs` view.</span></span> <span data-ttu-id="d6cfc-190">De `/views/account.ejs` weergave kunt u aanvullende informatie weergeven die `passport-azuread` op aanvraag van de gebruiker worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-190">The `/views/account.ejs` view allows you to view additional information that `passport-azuread` puts in the user request.</span></span>

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

5.  <span data-ttu-id="d6cfc-191">Toevoegen van een lay-out.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-191">Add a layout.</span></span> <span data-ttu-id="d6cfc-192">In de hoofdmap, maken de `/views/layout.ejs` weergeven.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-192">In the root directory, create the `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="d6cfc-193">Voor het bouwen en uitvoeren van uw app, voer `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-193">To build and run your app, run `node app.js`.</span></span> <span data-ttu-id="d6cfc-194">Ga vervolgens naar `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-194">Then, go to `http://localhost:3000`.</span></span>

7.  <span data-ttu-id="d6cfc-195">Aanmelden met een persoonlijk Microsoft-account of een account voor werk of school.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="d6cfc-196">Houd er rekening mee dat de identiteit van de gebruiker wordt weergegeven in de lijst /account.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-196">Note that the user's identity is reflected in the /account list.</span></span> 

<span data-ttu-id="d6cfc-197">U hebt nu een web-app die is beveiligd met behulp van protocollen volgens de industrienorm.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="d6cfc-198">U kunt gebruikers in uw app verifiëren met behulp van hun persoonlijke en werk of school-account.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6cfc-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6cfc-199">Next steps</span></span>
<span data-ttu-id="d6cfc-200">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) wordt geleverd als [een ZIP-bestand](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d6cfc-200">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="d6cfc-201">U kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="d6cfc-202">Vervolgens kunt u op verplaatsen met geavanceerdere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-202">Next, you can move on to more advanced topics.</span></span> <span data-ttu-id="d6cfc-203">Het is raadzaam om te proberen:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-203">You might want to try:</span></span>

[<span data-ttu-id="d6cfc-204">Een Node.js-web-API beveiligen met behulp van het v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="d6cfc-204">Secure a Node.js web API by using the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="d6cfc-205">Hier volgen enkele aanvullende resources:</span><span class="sxs-lookup"><span data-stu-id="d6cfc-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="d6cfc-206">Handleiding voor Azure AD v2.0-ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="d6cfc-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="d6cfc-207">Stack-overloop 'azure active directory' tag</span><span class="sxs-lookup"><span data-stu-id="d6cfc-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="d6cfc-208">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="d6cfc-208">Get security updates for our products</span></span>
<span data-ttu-id="d6cfc-209">We raden u aan te melden om te worden geïnformeerd wanneer er beveiligingsincidenten optreden.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-209">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="d6cfc-210">Op de [Microsoft technische beveiligingsmeldingen](https://technet.microsoft.com/security/dd252948) pagina moet u zich abonneren op beveiligingswaarschuwingen aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="d6cfc-210">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

