---
title: aaaGetting gestart met Azure AD aanmelden en afmelden met behulp van Node.js | Microsoft Docs
description: Meer informatie over hoe een Node.js Express MVC toobuild web-app die integreert met Azure AD voor aanmelden.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 26481899c74741743b947bd891b65ff24ffc43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a>Node.js-web-app aanmelden en afmelden met Azure AD
We gebruiken hier Passport:

* Meld u Hallo gebruiker in toohello app met Azure Active Directory (Azure AD).
* Informatie over Hallo gebruiker weergegeven.
* Meld u Hallo gebruiker buiten het Hallo-app.

Passport is verificatiemiddleware voor Node.js. Flexibel en modulair, Passport onopvallend in tooany kan worden verwijderd op basis van de Express of restify-webtoepassing. Een uitgebreide set strategieën ondersteunt verificatie met behulp van een gebruikersnaam en wachtwoord, Facebook, Twitter en meer. We hebben een strategie ontwikkeld voor Microsoft Azure Active Directory. We installeert deze module en voegt u Hallo Microsoft Azure Active Directory `passport-azure-ad` invoegtoepassing.

toodo deze, nemen Hallo stappen te volgen:

1. Een app te registreren.
2. Instellen van uw app toouse hello `passport-azure-ad` strategie.
3. Passport tooissue aanmelden en afmelden aanvragen tooAzure AD gebruiken.
4. Gegevens over Hallo gebruiker afdrukken.

Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).  toofollow langs, kunt u [basis van Hallo app downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) of kloon Hallo basisproject:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

toepassing Hello voltooid wordt op Hallo einde van deze zelfstudie ook aangeboden.

## <a name="step-1-register-an-app"></a>Stap 1: Een app registreren
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Selecteer in het menu bovenaan Hallo Hallo pagina Hallo uw account. Onder Hallo **Directory** Hallo Active Directory-tenant waar u tooregister Kies uw toepassing.

3. Selecteer **meer Services** in Hallo gelaten menu op Hallo van welkomstscherm clientzijde en selecteert u vervolgens **Azure Active Directory**.

4. Selecteer **App registraties**, en selecteer vervolgens **toevoegen**.

5. Ga als volgt Hallo prompts toocreate een **webtoepassing** en/of **WebAPI**.
  * Hallo **naam** Hallo toepassing beschrijft de toousers van uw toepassing.

  * Hallo **aanmeldings-URL** Hallo basis-URL van uw app is.  Hallo van een geraamte standaardwaarde is "http://localhost: 3000/auth/openid/return ''.

6. Nadat u hebt geregistreerd, wijst Azure AD van uw app een unieke toepassings-ID. U moet deze waarde in de volgende Hallo secties, dus kopieer het uit de pagina van de toepassing hello.
7. Van Hallo **instellingen** -> **eigenschappen** pagina voor uw toepassing, Hallo App ID URI bijwerken. Hallo **App ID URI** is de unieke id voor uw toepassing. Hallo conventies is toouse Hallo indeling `https://<tenant-domain>/<app-name>`, bijvoorbeeld: `https://contoso.onmicrosoft.com/my-first-aad-app`.

## <a name="step-2-add-prerequisites-tooyour-directory"></a>Stap 2: Vereisten tooyour map toevoegen
1. Vanaf de opdrachtregel Hallo mappen tooyour hoofdmap wijzigen als u niet al er, en vervolgens uitvoeren Hallo opdrachten:

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. U moet bovendien `passport-azure-ad`:
    * `npm install passport-azure-ad`

Hiermee installeert u Hallo bibliotheken die `passport-azure-ad` is afhankelijk van.

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>Stap 3: Uw app toouse Hallo passport-knooppunt-js strategie instellen
We configureren hier snelle toouse hello OpenID Connect-verificatieprotocol.  Passport is gebruikte toodo verschillende dingen, zoals het probleem aanmelden en afmeldingsaanvragen te verzenden, Hallo gebruikerssessie beheren en informatie over Hallo gebruiker ophalen.

1. toobegin, open Hallo `config.js` bestand in de hoofdmap Hallo van Hallo-project en voer vervolgens de configuratiewaarden van uw app in Hallo `exports.creds` sectie.

  * Hallo `clientID` Hallo is **toepassings-Id** die is toegewezen tooyour-app in Hallo-portal voor wachtwoordregistratie.

  * Hallo `returnURL` Hallo is **omleidings-Uri** die u hebt ingevoerd in Hallo-portal.

  * Hallo `clientSecret` Hallo geheim dat u hebt gegenereerd in de portal Hallo is.

2. Open vervolgens Hallo `app.js` bestand in de hoofdmap Hallo van Hallo-project. Voeg vervolgens na de aanroep tooinvoke Hallo Hallo `OIDCStrategy` strategie die wordt geleverd met `passport-azure-ad`.

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. Gebruik daarna Hallo strategie die we zojuist waarnaar wordt verwezen toohandle onze aanvragen aanmelden.

    ```JavaScript
    // Use hello OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
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
Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort) die alle schrijvers van strategieën voor. Hallo-strategie bekijkt, ziet u dat we geven deze een functie die een token en een gereed heeft als Hallo-parameters. Hallo-strategie komt weer toous nadat deze zijn werk doet. We willen vervolgens toostore Hallo gebruiker en stash Hallo token dus we er geen tooask voor het opnieuw moeten.

> [!IMPORTANT]
Hallo vorige code wordt elke gebruiker die tooauthenticate tooour server plaatsvindt. Dit wordt automatische registratie genoemd. Het is raadzaam dat u niet toestaan dat iedereen tooa productieserver zonder dat zij worden geregistreerd via een proces dat u kiest eerst worden geverifieerd. Dit is meestal Hallo patroon dat u ziet in consumenten-apps, die vervolgens vraagt u tooprovide aanvullende informatie, maar kunnen u tooregister met Facebook. Als dit niet een voorbeeldtoepassing, kan hebben we e-mailadres van de gebruiker Hallo opgehaald uit Hallo Tokenobject dat wordt geretourneerd en wordt vervolgens gevraagd Hallo gebruiker toofill aanvullende informatie. Omdat dit een testserver, we ze toohello in-memory database toevoegen.


4. Vervolgens laten we Hallo-methoden die ons in staat tootrack Hallo aangemelde gebruikers zoals vereist door Passport stellen toevoegen. Deze methoden omvatten serialiseren en deserialiseren van Hallo gebruikersgegevens.

    ```JavaScript

            // Passport session setup. (Section 2)

            //   toosupport persistent sign-in sessions, Passport needs toobe able to
            //   serialize users into hello session and deserialize them out of hello session. Typically,
            //   this is done simply by storing hello user ID when serializing and finding
            //   hello user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array toohold signed-in users
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

5.  Vervolgens voegen we Hallo code tooload Hallo Express-engine. Hier gebruiken we Hallo standaard /views en /routes patroon dat Express biedt.

    ```JavaScript

        // configure Express (section 2)

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

6. Tot slot gaan we toevoegen Hallo routes die lever Hallo werkelijke aanmelden aanvragen toohello `passport-azure-ad` engine:


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware tooauthenticate the
        //   request. hello first step in OpenID authentication involves redirecting
        //   hello user tootheir OpenID provider. After authenticating, hello OpenID
        //   provider redirects hello user back toothis application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in hello Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Stap 4: Gebruik Passport tooissue aanmelden en afmelden aanvragen tooAzure AD
Uw app is nu correct geconfigureerde toocommunicate met Hallo-eindpunt met behulp van Hallo OpenID Connect-verificatieprotocol.  `passport-azure-ad`heeft gezorgd voor alle Hallo details van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van gebruikerssessies. Alles wat blijft is zodat u uw gebruikers een manier toosign in en meld u af en verzamelen van aanvullende gegevens over Hallo aangemelde gebruikers.

1. Eerst laten we toevoegen Hallo standaard, aanmelden, account en afmeldingsmethoden toe tooour `app.js` bestand:

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
            log.info('Login was called in hello Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  Laten we controleert deze onderdelen:

  * Hallo `/`route leidt toohello index.ejs weergave Hallo gebruiker doorgeven in Hallo-aanvraag (indien aanwezig).
  * Hallo `/account` eerst routeren *zorgt ervoor dat we worden geverifieerd* (we implementeren die in het volgende voorbeeld Hallo), en vervolgens geeft de gebruiker in de aanvraag Hallo Hallo zodat we extra informatie over Hallo-gebruiker kunt ophalen.
  * Hallo `/login` route roept onze verificator azuread openidconnect van `passport-azuread`. Als dat niet lukt, wordt hij omgeleid Hallo terug te/gebruikersaanmelding.
  * Hallo `/logout` route roept Hallo logout.ejs (en route), welke cookies wist en retourneert Hallo back tooindex.ejs gebruiker.

3. Voor het laatste deel van Hallo `app.js`, gaan we voegen Hallo **EnsureAuthenticated** methode die wordt gebruikt in `/account`, zoals eerder is weergegeven.

    ```JavaScript

        // Simple route middleware tooensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs toobe protected. If
        //   hello request is authenticated (typically via a persistent sign-in session),
        //   hello request proceeds. Otherwise, hello user is redirected toothe
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. Maak ten slotte Hallo-server zelf laten we in `app.js`:

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a>Stap 5: toodisplay onze gebruiker op Hallo website maken Hallo weergaven en routes in Express
Nu `app.js` is voltooid. We gewoon moet tooadd Hallo routes en weergaven die informatie weergeven Hallo we toohello gebruiker ophalen, evenals verwerken Hallo `/logout` en `/login` routes die we hebben gemaakt.

1. Hallo maken `/routes/index.js` route onder Hallo-hoofdmap.

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. Hallo maken `/routes/user.js` route onder Hallo-hoofdmap.

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 Deze doorgegeven Hallo aanvraag tooour weergaven, met inbegrip van Hallo gebruiker, indien aanwezig.

3. Hallo maken `/views/index.ejs` weergave onder Hallo-hoofdmap. Dit is een eenvoudige pagina die onze aanmelding en afmelding methoden aanroept en kunnen we toograb accountgegevens. U ziet dat we kunnen gebruiken Hallo voorwaardelijke `if (!user)` omdat Hallo gebruiker wordt doorgegeven in de aanvraag Hallo bewijs hebben we een aangemelde gebruiker.

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. Hallo maken `/views/account.ejs` weergeven onder de hoofdmap hello, zodat we extra informatie kunt bekijken die `passport-azuread` in Hallo gebruikersaanvraag heeft geplaatst.

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. We maken dit goed door het toevoegen van een lay-out. Hallo maken ' / views/layout.ejs' weergave onder Hallo root directory.

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
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

##<a name="next-steps"></a>Volgende stappen
Ten slotte bouwen en uitvoeren van uw app. Voer `node app.js`, en ga te`http://localhost:3000`.

Meld u aan met een persoonlijk Microsoft-account of een account voor werk of school en u ziet hoe Hallo gebruikersidentiteit in Hallo /account lijst wordt weergegeven. U hebt nu een web-app die beveiligd met standaardprotocollen die gebruikers met hun persoonlijke en zakelijke/school accounts kunnen worden geverifieerd.

Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [wordt geleverd als ZIP-bestand](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip). U kunt dit ook klonen vanuit GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

U kunt nu verplaatsen naar geavanceerdere onderwerpen. U kunt tootry:

[Een Web-API met Azure AD beveiligen](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
