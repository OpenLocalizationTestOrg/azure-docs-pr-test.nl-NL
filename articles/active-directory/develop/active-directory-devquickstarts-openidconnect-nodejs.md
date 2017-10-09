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
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="5d642-103">Node.js-web-app aanmelden en afmelden met Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d642-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="5d642-104">We gebruiken hier Passport:</span><span class="sxs-lookup"><span data-stu-id="5d642-104">Here we use Passport to:</span></span>

* <span data-ttu-id="5d642-105">Meld u Hallo gebruiker in toohello app met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d642-105">Sign hello user in toohello app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="5d642-106">Informatie over Hallo gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5d642-106">Display information about hello user.</span></span>
* <span data-ttu-id="5d642-107">Meld u Hallo gebruiker buiten het Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="5d642-107">Sign hello user out of hello app.</span></span>

<span data-ttu-id="5d642-108">Passport is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="5d642-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="5d642-109">Flexibel en modulair, Passport onopvallend in tooany kan worden verwijderd op basis van de Express of restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="5d642-109">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or restify web application.</span></span> <span data-ttu-id="5d642-110">Een uitgebreide set strategieën ondersteunt verificatie met behulp van een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.</span><span class="sxs-lookup"><span data-stu-id="5d642-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="5d642-111">We hebben een strategie ontwikkeld voor Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d642-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="5d642-112">We installeert deze module en voegt u Hallo Microsoft Azure Active Directory `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="5d642-112">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="5d642-113">toodo deze, nemen Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5d642-113">toodo this, take hello following steps:</span></span>

1. <span data-ttu-id="5d642-114">Een app te registreren.</span><span class="sxs-lookup"><span data-stu-id="5d642-114">Register an app.</span></span>
2. <span data-ttu-id="5d642-115">Instellen van uw app toouse hello `passport-azure-ad` strategie.</span><span class="sxs-lookup"><span data-stu-id="5d642-115">Set up your app toouse hello `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="5d642-116">Passport tooissue aanmelden en afmelden aanvragen tooAzure AD gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5d642-116">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="5d642-117">Gegevens over Hallo gebruiker afdrukken.</span><span class="sxs-lookup"><span data-stu-id="5d642-117">Print data about hello user.</span></span>

<span data-ttu-id="5d642-118">Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="5d642-118">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="5d642-119">toofollow langs, kunt u [basis van Hallo app downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) of kloon Hallo basisproject:</span><span class="sxs-lookup"><span data-stu-id="5d642-119">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="5d642-120">toepassing Hello voltooid wordt op Hallo einde van deze zelfstudie ook aangeboden.</span><span class="sxs-lookup"><span data-stu-id="5d642-120">hello completed application is provided at hello end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="5d642-121">Stap 1: Een app registreren</span><span class="sxs-lookup"><span data-stu-id="5d642-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="5d642-122">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5d642-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="5d642-123">Selecteer in het menu bovenaan Hallo Hallo pagina Hallo uw account.</span><span class="sxs-lookup"><span data-stu-id="5d642-123">In hello menu at hello top of hello page, select your account.</span></span> <span data-ttu-id="5d642-124">Onder Hallo **Directory** Hallo Active Directory-tenant waar u tooregister Kies uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5d642-124">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="5d642-125">Selecteer **meer Services** in Hallo gelaten menu op Hallo van welkomstscherm clientzijde en selecteert u vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5d642-125">Select **More Services** in hello menu on hello left side of hello screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="5d642-126">Selecteer **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5d642-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="5d642-127">Ga als volgt Hallo prompts toocreate een **webtoepassing** en/of **WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="5d642-127">Follow hello prompts toocreate a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="5d642-128">Hallo **naam** Hallo toepassing beschrijft de toousers van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5d642-128">hello **name** of hello application describes your application toousers.</span></span>

  * <span data-ttu-id="5d642-129">Hallo **aanmeldings-URL** Hallo basis-URL van uw app is.</span><span class="sxs-lookup"><span data-stu-id="5d642-129">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="5d642-130">Hallo van een geraamte standaardwaarde is "http://localhost: 3000/auth/openid/return ''.</span><span class="sxs-lookup"><span data-stu-id="5d642-130">hello skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="5d642-131">Nadat u hebt geregistreerd, wijst Azure AD van uw app een unieke toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="5d642-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="5d642-132">U moet deze waarde in de volgende Hallo secties, dus kopieer het uit de pagina van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="5d642-132">You need this value in hello following sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="5d642-133">Van Hallo **instellingen** -> **eigenschappen** pagina voor uw toepassing, Hallo App ID URI bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5d642-133">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="5d642-134">Hallo **App ID URI** is de unieke id voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5d642-134">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="5d642-135">Hallo conventies is toouse Hallo indeling `https://<tenant-domain>/<app-name>`, bijvoorbeeld: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="5d642-135">hello convention is toouse hello format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-tooyour-directory"></a><span data-ttu-id="5d642-136">Stap 2: Vereisten tooyour map toevoegen</span><span class="sxs-lookup"><span data-stu-id="5d642-136">Step 2: Add prerequisites tooyour directory</span></span>
1. <span data-ttu-id="5d642-137">Vanaf de opdrachtregel Hallo mappen tooyour hoofdmap wijzigen als u niet al er, en vervolgens uitvoeren Hallo opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5d642-137">From hello command line, change directories tooyour root folder if you're not already there, and then run hello following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="5d642-138">U moet bovendien `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="5d642-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="5d642-139">Hiermee installeert u Hallo bibliotheken die `passport-azure-ad` is afhankelijk van.</span><span class="sxs-lookup"><span data-stu-id="5d642-139">This installs hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="5d642-140">Stap 3: Uw app toouse Hallo passport-knooppunt-js strategie instellen</span><span class="sxs-lookup"><span data-stu-id="5d642-140">Step 3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="5d642-141">We configureren hier snelle toouse hello OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="5d642-141">Here, we configure Express toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="5d642-142">Passport is gebruikte toodo verschillende dingen, zoals het probleem aanmelden en afmeldingsaanvragen te verzenden, Hallo gebruikerssessie beheren en informatie over Hallo gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="5d642-142">Passport is used toodo various things, including issue sign-in and sign-out requests, manage hello user's session, and get information about hello user.</span></span>

1. <span data-ttu-id="5d642-143">toobegin, open Hallo `config.js` bestand in de hoofdmap Hallo van Hallo-project en voer vervolgens de configuratiewaarden van uw app in Hallo `exports.creds` sectie.</span><span class="sxs-lookup"><span data-stu-id="5d642-143">toobegin, open hello `config.js` file at hello root of hello project, and then enter your app's configuration values in hello `exports.creds` section.</span></span>

  * <span data-ttu-id="5d642-144">Hallo `clientID` Hallo is **toepassings-Id** die is toegewezen tooyour-app in Hallo-portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="5d642-144">hello `clientID` is hello **Application Id** that's assigned tooyour app in hello registration portal.</span></span>

  * <span data-ttu-id="5d642-145">Hallo `returnURL` Hallo is **omleidings-Uri** die u hebt ingevoerd in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="5d642-145">hello `returnURL` is hello **Redirect Uri** that you entered in hello portal.</span></span>

  * <span data-ttu-id="5d642-146">Hallo `clientSecret` Hallo geheim dat u hebt gegenereerd in de portal Hallo is.</span><span class="sxs-lookup"><span data-stu-id="5d642-146">hello `clientSecret` is hello secret that you generated in hello portal.</span></span>

2. <span data-ttu-id="5d642-147">Open vervolgens Hallo `app.js` bestand in de hoofdmap Hallo van Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="5d642-147">Next, open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="5d642-148">Voeg vervolgens na de aanroep tooinvoke Hallo Hallo `OIDCStrategy` strategie die wordt geleverd met `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="5d642-148">Then add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="5d642-149">Gebruik daarna Hallo strategie die we zojuist waarnaar wordt verwezen toohandle onze aanvragen aanmelden.</span><span class="sxs-lookup"><span data-stu-id="5d642-149">After that, use hello strategy we just referenced toohandle our sign-in requests.</span></span>

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
<span data-ttu-id="5d642-150">Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort) die alle schrijvers van strategieën voor.</span><span class="sxs-lookup"><span data-stu-id="5d642-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="5d642-151">Hallo-strategie bekijkt, ziet u dat we geven deze een functie die een token en een gereed heeft als Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="5d642-151">Looking at hello strategy, you see that we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="5d642-152">Hallo-strategie komt weer toous nadat deze zijn werk doet.</span><span class="sxs-lookup"><span data-stu-id="5d642-152">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="5d642-153">We willen vervolgens toostore Hallo gebruiker en stash Hallo token dus we er geen tooask voor het opnieuw moeten.</span><span class="sxs-lookup"><span data-stu-id="5d642-153">Then we want toostore hello user and stash hello token so we don't need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="5d642-154">Hallo vorige code wordt elke gebruiker die tooauthenticate tooour server plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="5d642-154">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="5d642-155">Dit wordt automatische registratie genoemd.</span><span class="sxs-lookup"><span data-stu-id="5d642-155">This is known as auto-registration.</span></span> <span data-ttu-id="5d642-156">Het is raadzaam dat u niet toestaan dat iedereen tooa productieserver zonder dat zij worden geregistreerd via een proces dat u kiest eerst worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="5d642-156">We    recommend that you don't let anyone authenticate tooa production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="5d642-157">Dit is meestal Hallo patroon dat u ziet in consumenten-apps, die vervolgens vraagt u tooprovide aanvullende informatie, maar kunnen u tooregister met Facebook.</span><span class="sxs-lookup"><span data-stu-id="5d642-157">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you tooprovide additional information.</span></span> <span data-ttu-id="5d642-158">Als dit niet een voorbeeldtoepassing, kan hebben we e-mailadres van de gebruiker Hallo opgehaald uit Hallo Tokenobject dat wordt geretourneerd en wordt vervolgens gevraagd Hallo gebruiker toofill aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="5d642-158">If this weren't a sample application, we could have extracted hello user's email address from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="5d642-159">Omdat dit een testserver, we ze toohello in-memory database toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5d642-159">Because this is a test server, we add them toohello in-memory database.</span></span>


4. <span data-ttu-id="5d642-160">Vervolgens laten we Hallo-methoden die ons in staat tootrack Hallo aangemelde gebruikers zoals vereist door Passport stellen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5d642-160">Next, let's add hello methods that enable us tootrack hello signed-in users as required by Passport.</span></span> <span data-ttu-id="5d642-161">Deze methoden omvatten serialiseren en deserialiseren van Hallo gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="5d642-161">These methods include serializing and deserializing hello user's information.</span></span>

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

5.  <span data-ttu-id="5d642-162">Vervolgens voegen we Hallo code tooload Hallo Express-engine.</span><span class="sxs-lookup"><span data-stu-id="5d642-162">Next, let's add hello code tooload hello Express engine.</span></span> <span data-ttu-id="5d642-163">Hier gebruiken we Hallo standaard /views en /routes patroon dat Express biedt.</span><span class="sxs-lookup"><span data-stu-id="5d642-163">Here we use hello default /views and /routes pattern that Express provides.</span></span>

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

6. <span data-ttu-id="5d642-164">Tot slot gaan we toevoegen Hallo routes die lever Hallo werkelijke aanmelden aanvragen toohello `passport-azure-ad` engine:</span><span class="sxs-lookup"><span data-stu-id="5d642-164">Finally, let's add hello routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>


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


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="5d642-165">Stap 4: Gebruik Passport tooissue aanmelden en afmelden aanvragen tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="5d642-165">Step 4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="5d642-166">Uw app is nu correct geconfigureerde toocommunicate met Hallo-eindpunt met behulp van Hallo OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="5d642-166">Your app is now properly configured toocommunicate with hello endpoint by using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="5d642-167">`passport-azure-ad`heeft gezorgd voor alle Hallo details van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van gebruikerssessies.</span><span class="sxs-lookup"><span data-stu-id="5d642-167">`passport-azure-ad` has taken care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="5d642-168">Alles wat blijft is zodat u uw gebruikers een manier toosign in en meld u af en verzamelen van aanvullende gegevens over Hallo aangemelde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5d642-168">All that remains is giving your users a way toosign in and sign out, and gathering additional information about hello signed-in users.</span></span>

1. <span data-ttu-id="5d642-169">Eerst laten we toevoegen Hallo standaard, aanmelden, account en afmeldingsmethoden toe tooour `app.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="5d642-169">First, let's add hello default, sign-in, account, and sign-out methods tooour `app.js` file:</span></span>

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

2.  <span data-ttu-id="5d642-170">Laten we controleert deze onderdelen:</span><span class="sxs-lookup"><span data-stu-id="5d642-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="5d642-171">Hallo `/`route leidt toohello index.ejs weergave Hallo gebruiker doorgeven in Hallo-aanvraag (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="5d642-171">hello `/`route redirects toohello index.ejs view, passing hello user in hello request (if it exists).</span></span>
  * <span data-ttu-id="5d642-172">Hallo `/account` eerst routeren *zorgt ervoor dat we worden geverifieerd* (we implementeren die in het volgende voorbeeld Hallo), en vervolgens geeft de gebruiker in de aanvraag Hallo Hallo zodat we extra informatie over Hallo-gebruiker kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="5d642-172">hello `/account` route first *ensures we are authenticated* (we implement that in hello following example), and then passes hello user in hello request so that we can get additional information about hello user.</span></span>
  * <span data-ttu-id="5d642-173">Hallo `/login` route roept onze verificator azuread openidconnect van `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="5d642-173">hello `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="5d642-174">Als dat niet lukt, wordt hij omgeleid Hallo terug te/gebruikersaanmelding.</span><span class="sxs-lookup"><span data-stu-id="5d642-174">If that doesn't succeed, it redirects hello user back too/login.</span></span>
  * <span data-ttu-id="5d642-175">Hallo `/logout` route roept Hallo logout.ejs (en route), welke cookies wist en retourneert Hallo back tooindex.ejs gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5d642-175">hello `/logout` route simply calls hello logout.ejs (and route), which clears cookies and then returns hello user back tooindex.ejs.</span></span>

3. <span data-ttu-id="5d642-176">Voor het laatste deel van Hallo `app.js`, gaan we voegen Hallo **EnsureAuthenticated** methode die wordt gebruikt in `/account`, zoals eerder is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5d642-176">For hello last part of `app.js`, let's add hello **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

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

4. <span data-ttu-id="5d642-177">Maak ten slotte Hallo-server zelf laten we in `app.js`:</span><span class="sxs-lookup"><span data-stu-id="5d642-177">Finally, let's create hello server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a><span data-ttu-id="5d642-178">Stap 5: toodisplay onze gebruiker op Hallo website maken Hallo weergaven en routes in Express</span><span class="sxs-lookup"><span data-stu-id="5d642-178">Step 5: toodisplay our user in hello website, create hello views and routes in Express</span></span>
<span data-ttu-id="5d642-179">Nu `app.js` is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5d642-179">Now `app.js` is complete.</span></span> <span data-ttu-id="5d642-180">We gewoon moet tooadd Hallo routes en weergaven die informatie weergeven Hallo we toohello gebruiker ophalen, evenals verwerken Hallo `/logout` en `/login` routes die we hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d642-180">We simply need tooadd hello routes and views that show hello information we get toohello user, as well as handle hello `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="5d642-181">Hallo maken `/routes/index.js` route onder Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="5d642-181">Create hello `/routes/index.js` route under hello root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="5d642-182">Hallo maken `/routes/user.js` route onder Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="5d642-182">Create hello `/routes/user.js` route under hello root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="5d642-183">Deze doorgegeven Hallo aanvraag tooour weergaven, met inbegrip van Hallo gebruiker, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="5d642-183">These pass along hello request tooour views, including hello user if present.</span></span>

3. <span data-ttu-id="5d642-184">Hallo maken `/views/index.ejs` weergave onder Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="5d642-184">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="5d642-185">Dit is een eenvoudige pagina die onze aanmelding en afmelding methoden aanroept en kunnen we toograb accountgegevens.</span><span class="sxs-lookup"><span data-stu-id="5d642-185">This is a simple page that calls our login and logout methods and enables us toograb account information.</span></span> <span data-ttu-id="5d642-186">U ziet dat we kunnen gebruiken Hallo voorwaardelijke `if (!user)` omdat Hallo gebruiker wordt doorgegeven in de aanvraag Hallo bewijs hebben we een aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5d642-186">Notice that we can use hello conditional `if (!user)` as hello user being passed through in hello request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="5d642-187">Hallo maken `/views/account.ejs` weergeven onder de hoofdmap hello, zodat we extra informatie kunt bekijken die `passport-azuread` in Hallo gebruikersaanvraag heeft geplaatst.</span><span class="sxs-lookup"><span data-stu-id="5d642-187">Create hello `/views/account.ejs` view under hello root directory so that we can view additional information that `passport-azuread` has put in hello user request.</span></span>

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

5. <span data-ttu-id="5d642-188">We maken dit goed door het toevoegen van een lay-out.</span><span class="sxs-lookup"><span data-stu-id="5d642-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="5d642-189">Hallo maken ' / views/layout.ejs' weergave onder Hallo root directory.</span><span class="sxs-lookup"><span data-stu-id="5d642-189">Create hello '/views/layout.ejs' view under hello root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="5d642-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d642-190">Next steps</span></span>
<span data-ttu-id="5d642-191">Ten slotte bouwen en uitvoeren van uw app.</span><span class="sxs-lookup"><span data-stu-id="5d642-191">Finally, build and run your app.</span></span> <span data-ttu-id="5d642-192">Voer `node app.js`, en ga te`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="5d642-192">Run `node app.js`, and then go too`http://localhost:3000`.</span></span>

<span data-ttu-id="5d642-193">Meld u aan met een persoonlijk Microsoft-account of een account voor werk of school en u ziet hoe Hallo gebruikersidentiteit in Hallo /account lijst wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5d642-193">Sign in with either a personal Microsoft account or a work or school account, and notice how hello user's identity is reflected in hello /account list.</span></span> <span data-ttu-id="5d642-194">U hebt nu een web-app die beveiligd met standaardprotocollen die gebruikers met hun persoonlijke en zakelijke/school accounts kunnen worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="5d642-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="5d642-195">Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [wordt geleverd als ZIP-bestand](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5d642-195">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="5d642-196">U kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="5d642-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="5d642-197">U kunt nu verplaatsen naar geavanceerdere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="5d642-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="5d642-198">U kunt tootry:</span><span class="sxs-lookup"><span data-stu-id="5d642-198">You might want tootry:</span></span>

[<span data-ttu-id="5d642-199">Een Web-API met Azure AD beveiligen</span><span class="sxs-lookup"><span data-stu-id="5d642-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
