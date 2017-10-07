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
# <a name="add-sign-in-tooa-nodejs-web-app"></a>Aanmelden tooa Node.js-web-app toevoegen

> [!NOTE]
> Niet alle Azure Active Directory-scenario's en onderdelen werken met Hallo v2.0-eindpunt. toodetermine of moet u Hallo v2.0-eindpunt of Hallo v1.0 eindpunt, gelezen over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 

In deze zelfstudie gebruiken we Passport toodo Hallo taken te volgen:

* Hallo-gebruiker aanmelden via Azure Active Directory (Azure AD) in een web-app en Hallo v2.0-eindpunt.
* Informatie over Hallo gebruiker weergegeven.
* Meld u Hallo gebruiker buiten het Hallo-app.

**Passport** is verificatiemiddleware voor Node.js. Flexibel en modulair, Passport kan onopvallend worden verwijderd in een snelle gebaseerde of restify-webtoepassing. In Passport, een uitgebreide set strategieën ondersteuning voor verificatie met behulp van een gebruikersnaam en wachtwoord, Facebook, Twitter of andere opties. We hebben een strategie ontwikkeld voor Azure AD. In dit artikel we u zien hoe tooinstall Hallo module en voeg vervolgens hello Azure AD `passport-azure-ad` invoegtoepassing.

## <a name="download"></a>Downloaden
Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs). toofollow hello zelfstudie, kunt u [basis van Hallo app downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) of kloon Hallo basisproject:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

U kunt ook de toepassing hello voltooid op Hallo einde van deze zelfstudie ophalen.

## <a name="1-register-an-app"></a>1: een app registreren
Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of voert u [deze gedetailleerde stappen](active-directory-v2-app-registration.md) tooregister een app. Zorg ervoor dat u:

* Kopiëren Hallo **toepassings-Id** tooyour app toegewezen. U moet voor deze zelfstudie.
* Hallo toevoegen **Web** platform voor uw app.
* Kopiëren Hallo **omleidings-URI** van Hallo-portal. Moet u Hallo standaardwaarde URI van `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-add-prerequisities-tooyour-directory"></a>2: prerequisities tooyour map toevoegen
Bij een opdrachtprompt mappen toogo tooyour hoofdmap niet wijzigen als u nog geen er. Voer Hallo volgende opdrachten:

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

Daarnaast gebruiken wij `passport-azure-ad` in Hallo geraamte van Hallo Quick Start:

* `npm install passport-azure-ad`

Hiermee installeert u Hallo bibliotheken die `passport-azure-ad` gebruikt.

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3: uw app toouse Hallo passport-knooppunt-js strategie instellen
Hallo Express-middleware toouse hello OpenID Connect-verificatieprotocol instellen. U gebruikt Passport tooissue aanmelden en afmeldingsaanvragen te verzenden, Hallo gebruikerssessie beheren en informatie ophalen over de gebruiker hello, onder andere.

1.  Open in de hoofdmap van de Hallo van Hallo-project, Hallo bestand Config.js file. In Hallo `exports.creds` sectie, voert u de configuratiewaarden van uw app.
  
  * `clientID`: Hallo **toepassings-Id** die is toegewezen tooyour-app in hello Azure-portal.
  * `returnURL`: Hallo **omleidings-URI** die u hebt ingevoerd in Hallo-portal.
  * `clientSecret`: Hallo geheim dat u hebt gegenereerd in Hallo-portal.

2.  In de hoofdmap van de Hallo van Hallo-project, Hallo App.js bestand te openen. tooinvoke hello OIDCStrategy stratey, wordt geleverd met `passport-azure-ad`, Hallo aanroep volgende toevoegen:

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle uw aanvragen aanmelden gebruik Hallo strategie die u zojuist hebt waarnaar wordt verwezen:

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

Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort). Alle schrijvers van strategieën toohello patroon. Hallo-strategie doorgeven een `function()` die gebruikmaakt van een token en `done` als parameters. Hallo-strategie terug nadat al het werk wordt. Hallo-gebruiker en stash Hallo token opslaan zodat u niet tooask voor het opnieuw hoeft.

  > [!IMPORTANT]
  > Hallo voorafgaande code geldt voor elke gebruiker die tooyour server kan worden geverifieerd. Dit wordt automatische registratie genoemd. Op een productieserver je wilt niet dat toolet iedereen zonder dat zij een registratieproces die u kiest doorlopen eerst. Dit is meestal Hallo patroon die u in consumenten-apps ziet. Hallo-app kunt u mogelijk tooregister met Facebook, maar vervolgens wordt u gevraagd een tooenter aanvullende informatie. Als u een opdrachtregelprogramma zijn niet voor deze zelfstudie gebruikt, kan u Hallo e extraheren uit Hallo Tokenobject dat wordt geretourneerd. Vervolgens vraagt u mogelijk Hallo gebruiker tooenter aanvullende informatie. Omdat dit een testserver is, u Hallo gebruiker toevoegen rechtstreeks toohello de database in het geheugen.
  > 
  > 

4.  Voeg Hallo methoden tookeep bijhouden van gebruikers die zijn ondertekend, te gebruiken zoals wordt vereist door Passport. Dit omvat het serialiseren en deserialiseren van Hallo gebruikersgegevens:

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

5.  Voeg code Hallo Hallo Express-engine wordt geladen. Gebruik van Hallo standaard /views en /routes patroon dat Express:

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

6.  Hallo POST routes die lever Hallo werkelijke aanmelden aanvragen toohello toevoegen `passport-azure-ad` engine:

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

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4: gebruik Passport tooissue aan- en afmeldingsaanvragen tooAzure AD-aanvragen
Uw app is nu ingesteld toocommunicate met Hallo v2.0-eindpunt met behulp van Hallo OpenID Connect-verificatieprotocol. Hallo `passport-azure-ad` strategie zorgt voor alle Hallo details van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van Hallo gebruikerssessie. Alle die altijd is ingeschakeld toodo toogive is uw gebruikers een manier toosign in en meld u out en toogather meer informatie over het Hallo-gebruiker die is aangemeld.

1.  Hallo toevoegen **standaard**, **aanmelding**, **account**, en **afmelding** methoden tooyour App.js bestand:

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

  Dit zijn Hallo details:
    
    * Hallo `/` route toohello index.ejs weergave wordt omgeleid. Dit wordt Hallo gebruiker doorgegeven in Hallo-aanvraag (indien aanwezig).
    * Hallo `/account` eerst routeren *zorgt ervoor dat u bent geverifieerd* (u implementeert die in de volgende code Hallo). Hallo-gebruiker wordt vervolgens doorgegeven in Hallo-aanvraag. Dit is zodat u meer informatie over gebruikers Hallo krijgt.
    * Hallo `/login` gesprekken rondsturen uw `azuread-openidconnect` verificator van `passport-azuread`. Als dat niet lukt, wordt hij omgeleid Hallo gebruiker terug te`/login`.
    * Hallo `/logout` route roept Hallo logout.ejs weergeven (en route). Hiermee worden cookies en vervolgens retourneert Hallo back tooindex.ejs gebruiker.

2.  Hallo toevoegen **EnsureAuthenticated** methode die u eerder in gebruikt `/account`:

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

3.  Maak in App.js, Hallo-server:

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5: Hallo weergaven en routes in Express dat u uw gebruikers worden weergegeven op Hallo website maken
Hallo routes en weergaven waarin informatie toohello gebruiker toevoegen. Hallo routes en weergaven ook Hallo afhandelen `/logout` en `/login` routes die u hebt gemaakt.

1. Maken in de hoofdmap hello, Hallo `/routes/index.js` route.

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  Maken in de hoofdmap hello, Hallo `/routes/user.js` route.

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`en `/routes/user.js` zijn eenvoudige routes die Hallo aanvraag tooyour weergaven doorgegeven, met inbegrip van Hallo gebruiker, indien aanwezig.

3.  Maken in de hoofdmap hello, Hallo `/views/index.ejs` weergeven. Deze pagina roept de **aanmelding** en **afmelding** methoden. U ook hello gebruiken `/views/index.ejs` toocapture accountgegevens te bekijken. U kunt voorwaardelijke Hallo `if (!user)` als Hallo-gebruiker in Hallo-aanvraag wordt doorgegeven. Het is bewijs dat u een gebruiker aangemeld hebt.

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

4.  Maken in de hoofdmap hello, Hallo `/views/account.ejs` weergeven. Hallo `/views/account.ejs` weergave kunt u aanvullende informatie tooview die `passport-azuread` worden geplaatst in de gebruikersaanvraag Hallo.

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

5.  Toevoegen van een lay-out. Maken in de hoofdmap hello, Hallo `/views/layout.ejs` weergeven.

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

6.  toobuild en uitvoeren van uw app uitvoeren `node app.js`. Ga vervolgens te`http://localhost:3000`.

7.  Aanmelden met een persoonlijk Microsoft-account of een account voor werk of school. Houd er rekening mee dat de identiteit van de gebruiker Hallo worden weerspiegeld in Hallo /account lijst. 

U hebt nu een web-app die is beveiligd met behulp van protocollen volgens de industrienorm. U kunt gebruikers in uw app verifiëren met behulp van hun persoonlijke en werk of school-account.

## <a name="next-steps"></a>Volgende stappen
Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) wordt geleverd als [een ZIP-bestand](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip). U kunt dit ook klonen vanuit GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Vervolgens kunt u op toomore geavanceerde onderwerpen. U kunt tootry:

[Een Node.js-web-API beveiligen met behulp van Hallo v2.0-eindpunt](active-directory-v2-devquickstarts-node-api.md)

Hier volgen enkele aanvullende resources:

* [Handleiding voor Azure AD v2.0-ontwikkelaars](active-directory-appmodel-v2-overview.md)
* [Stack-overloop 'azure active directory' tag](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Beveiligingsupdates voor onze producten downloaden
We raden u toosign up toobe een melding wanneer er beveiligingsincidenten optreden. Op Hallo [Microsoft technische beveiligingsmeldingen](https://technet.microsoft.com/security/dd252948) pagina moet u zich abonneren tooSecurity adviezen waarschuwingen.

