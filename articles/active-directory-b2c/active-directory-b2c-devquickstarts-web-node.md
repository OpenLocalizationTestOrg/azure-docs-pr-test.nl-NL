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
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>Azure AD B2C: Aanmelden tooa Node.js-webtoepassing toevoegen

**Passport** is verificatiemiddleware voor Node.js. Passport is zeer flexibel en modulair, en kan onopvallend worden geïnstalleerd in een Express- of Restify-webtoepassing. Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.

We hebben een strategie ontwikkeld voor Azure Active Directory (Azure AD). U installeert deze module en voegt u hello Azure AD `passport-azure-ad` invoegtoepassing.

toodo, moet u:

1. U registreert een toepassing met Azure AD.
2. Instellen van uw app toouse hello `passport-azure-ad` invoegtoepassing.
3. Passport tooissue aanmelden en afmelden aanvragen tooAzure AD gebruiken.
4. U drukt de gebruikersgegevens af.

code voor deze zelfstudie Hallo [wordt bewaard in GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS). toofollow langs, kunt u [basis van Hallo app downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip). U kunt Hallo basisproject ook klonen:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

toepassing Hello voltooid wordt op Hallo einde van deze zelfstudie aangeboden.

## <a name="get-an-azure-ad-b2c-directory"></a>Een Azure AD B2C-directory maken

Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.  Een directory is een container voor alle gebruikers, apps, groepen en meer. Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u doorgaat in deze handleiding.

## <a name="create-an-application"></a>Een app maken

Vervolgens moet u een app toocreate in uw B2C-directory. Hiermee geeft u Azure AD-informatie dat het moet toocommunicate veilig met uw app. Beide Hallo van client-app en web-API worden aangegeven met één **toepassings-ID**, omdat ze samen één logische app vormen. toocreate een app, volg [deze instructies](active-directory-b2c-app-registration.md). Zorg ervoor dat:

- Omvatten een **web-app**/**web-API** in Hallo-toepassing.
- U `http://localhost:3000/auth/openid/return` invoert als **antwoord-URL**. Het is Hallo-standaard-URL voor dit codevoorbeeld.
- U een **toepassingsgeheim** maakt voor uw toepassing en dit kopieert. U hebt dit later nodig. Opmerking dat deze waarde toobe moet [XML escape-teken](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) voordat u deze kunt gebruiken.
- Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app. Deze hebt u ook later nodig.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Het beleid maken

In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md). Deze app bevat drie identiteitservaringen: registreren, aanmelden en aanmelden via Facebook. U moet toocreate dit beleid voor elk type, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Wanneer u uw drie beleidsregels maakt:

- Kies Hallo **weergavenaam** en andere registratiekenmerken in het registratiebeleid.
- Kies Hallo **weergavenaam** en **Object-ID** toepassingsclaims voor elk beleid. U kunt ook andere claims kiezen.
- Kopiëren Hallo **naam** van elk beleid nadat u dit hebt gemaakt. Het voorvoegsel Hallo heeft `b2c_1_`.  U hebt deze beleidsnamen later nodig.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Wanneer u uw drie beleidsregels maakt, bent u klaar toobuild uw app.

Houd er rekening mee dat dit artikel wordt niet beschreven hoe toouse Hallo beleidsregels u zojuist hebt gemaakt. toolearn over de werking van beleid in Azure AD B2C, beginnen met Hallo [zelfstudie .NET web app aan de slag](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="add-prerequisites-tooyour-directory"></a>Vereisten tooyour map toevoegen

Vanaf de opdrachtregel Hallo tooyour hoofdmap mappen te wijzigen als u niet al er. Voer Hallo volgende opdrachten:

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

Daarnaast hebben we gebruikt `passport-azure-ad` voor het voorbeeld in Hallo basisproject Hallo Quick Start.

- `npm install passport-azure-ad`

Hiermee installeert u Hallo bibliotheken die `passport-azure-ad` is afhankelijk van.

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>Instellen van uw app toouse Hallo strategie Passport-Node.js
Configureer Hallo Express-middleware toouse hello OpenID Connect-verificatieprotocol. Passport gaat gebruikte tooissue aanmelden en afmeldingsaanvragen te verzenden, gebruikerssessies te beheren en informatie over gebruikers, onder andere acties.

Open Hallo `config.js` bestand in de hoofdmap Hallo van Hallo-project en voer de configuratiewaarden van uw app in Hallo `exports.creds` sectie.
- `clientID`: Hallo **toepassings-ID** tooyour-app in de portal voor registratie van Hallo toegewezen.
- `returnURL`: Hallo **omleidings-URI** u hebt ingevoerd in het Hallo-portal.
- `tenantName`: de tenantnaam Hallo van uw app, bijvoorbeeld **contoso.onmicrosoft.com**.

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Open Hallo `app.js` bestand in de hoofdmap Hallo van Hallo-project. Toevoegen van de volgende aanroep tooinvoke Hallo Hallo `OIDCStrategy` strategie die wordt geleverd met `passport-azure-ad`.


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

Gebruik Hallo-strategie die u zojuist hebt waarnaar wordt verwezen toohandle aanmelden aanvragen.

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
In Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (inclusief Twitter en Facebook). Alle schrijvers van strategieën toothis patroon. Wanneer u Hallo strategie bekijkt, ziet u dat u gebruikmaakt van een `function()` die een token heeft en een `done` als Hallo-parameters. Hallo-strategie komt weer tooyou nadat deze zijn werk heeft gedaan. Sla Hallo gebruiker en Hallo token niet initialiseren zodat u niet tooask voor het opnieuw hoeft.

> [!IMPORTANT]
Hallo voorafgaande code geldt voor alle gebruikers die Hallo-server verifieert. Dit is automatische registratie. Wanneer u productieservers gebruikt, kunt u toolet gebruikers niet wilt, tenzij ze een registratieproces die u hebt ingesteld hebben doorlopen. U ziet dit patroon vaak in consumenten-apps. Hiermee kunt u tooregister via Facebook, maar vervolgens zij vraagt u toofill aanvullende informatie. Als de toepassing geen voorbeeld, kunnen we een e-mailadres extraheren uit Hallo Tokenobject dat wordt geretourneerd en vervolgens vraagt u Hallo gebruiker toofill aanvullende informatie. Omdat dit een testserver, toevoegen we gewoon gebruikers toohello in-memory database.

Voeg Hallo methoden waarmee u tookeep bijhouden van gebruikers die zijn aangemeld, zoals wordt vereist door Passport. Dit omvat het serialiseren en deserialiseren van gebruikersgegevens:

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

Hallo code tooload Hallo Express-engine toevoegen. In de volgende hello, ziet u dat we de standaard Hallo gebruiken `/views` en `/routes` patroon dat Express biedt.

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

Hallo toevoegen `POST` routes die aanlevert Hallo werkelijke aanmelden aanvragen toohello `passport-azure-ad` engine:

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

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Passport tooissue aanmelden en afmelden aanvragen tooAzure AD gebruiken

Uw app is nu correct geconfigureerde toocommunicate met Hallo v2.0-eindpunt met behulp van Hallo OpenID Connect-verificatieprotocol. `passport-azure-ad`heeft gezorgd voor Hallo details van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van de gebruikerssessie. Alles wat blijft toogive is uw gebruikers een manier toosign in en meld u out en toogather aanvullende informatie over gebruikers die zich hebben aangemeld.

Voeg eerst Hallo standaard, aanmelden, account en afmeldingsmethoden toe tooyour `app.js` bestand:

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

tooreview informatie over deze methoden:
- Hallo `/` route leidt toohello `index.ejs` weergeven per gebruiker Hallo doorgeven in Hallo-aanvraag (indien aanwezig).
- Hallo `/account` route wordt eerst gecontroleerd of u bent geverifieerd (Hallo implementatie voor deze bewerking hieronder is). Deze worden vervolgens doorgegeven Hallo gebruiker in de aanvraag Hallo zodat u aanvullende informatie over het Hallo-gebruiker kunt ophalen.
- Hallo `/login` route aanroepen Hallo `azuread-openidconnect` verificator van `passport-azure-ad`. Als dit niet lukt, leidt Hallo route Hallo gebruiker terug te`/login`.
- `/logout` roept `logout.ejs` aan (en de bijbehorende route). Hiermee worden cookies en vervolgens retourneert gebruiker terug te Hallo`index.ejs`.


Voor het laatste deel van Hallo `app.js`, Hallo toevoegen `EnsureAuthenticated` methode die wordt gebruikt in Hallo `/account` route.

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

Maak ten slotte Hallo-server zelf in `app.js`.

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>Hallo weergaven maken en het beleid van routes in Express toocall

Uw `app.js` is nu voltooid. U hoeft alleen maar tooadd Hallo routes en weergaven waarmee u toocall Hallo beleid voor aanmelden en registreren. Deze ook Hallo afhandelen `/logout` en `/login` routes die u hebt gemaakt.

Hallo maken `/routes/index.js` route onder Hallo-hoofdmap.

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

Hallo maken `/routes/user.js` route onder Hallo-hoofdmap.

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

Deze eenvoudige routes doorgegeven aanvragen tooyour weergaven. Ze bevatten Hallo gebruiker, indien aanwezig.

Hallo maken `/views/index.ejs` weergave onder Hallo-hoofdmap. Dit is een eenvoudige pagina waarmee beleid voor aanmelden en afmelden wordt aangeroepen. U kunt ook gebruiken deze toograb accountgegevens. Opmerking waarmee u voorwaardelijke Hallo kunt `if (!user)` zoals Hallo gebruiker wordt doorgegeven in Hallo aanvraag tooprovide bewijsmateriaal die Hallo-gebruiker is aangemeld.

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

Hallo maken `/views/account.ejs` weergeven onder de hoofdmap hello, zodat u kunt aanvullende informatie weergeven die `passport-azure-ad` plaatsen in de gebruikersaanvraag Hallo.

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

U kunt nu uw app bouwen en uitvoeren.

Voer `node app.js` en te navigeren`http://localhost:3000`


Registreren of aanmelden toohello app via e-mail of Facebook. Meld u af en meld u weer aan als een andere gebruiker.

##<a name="next-steps"></a>Volgende stappen

Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [wordt geleverd als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip). U kunt dit ook klonen van GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

U kunt nu op toomore geavanceerde onderwerpen verplaatsen. U kunt het volgende proberen:

[Een web-API beveiligen met behulp van Hallo B2C-model in Node.js](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
