---
title: Aan de slag met Azure AD aanmelden en afmelden met behulp van Node.js | Microsoft Docs
description: Informatie over het bouwen van een Node.js Express MVC-web-app die met Azure AD voor aanmelden integreert.
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
ms.openlocfilehash: 13317b016f9ff3955f376b858645c42668b0de42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="6cf6b-103">Node.js-web-app aanmelden en afmelden met Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cf6b-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="6cf6b-104">We gebruiken hier Passport:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-104">Here we use Passport to:</span></span>

* <span data-ttu-id="6cf6b-105">De gebruiker zich aanmeldt bij de app met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6cf6b-105">Sign the user in to the app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="6cf6b-106">Informatie over de gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-106">Display information about the user.</span></span>
* <span data-ttu-id="6cf6b-107">Meld u aan de gebruiker buiten de app.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-107">Sign the user out of the app.</span></span>

<span data-ttu-id="6cf6b-108">Passport is verificatiemiddleware voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="6cf6b-109">Flexibel en modulair, Passport kan worden onopvallend verwijderd voor een Express- of restify-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-109">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or restify web application.</span></span> <span data-ttu-id="6cf6b-110">Een uitgebreide set strategieën ondersteunt verificatie met behulp van een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="6cf6b-111">We hebben een strategie ontwikkeld voor Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="6cf6b-112">We installeert deze module en voegt u de Microsoft Azure Active Directory `passport-azure-ad` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-112">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="6cf6b-113">U doet dit door de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-113">To do this, take the following steps:</span></span>

1. <span data-ttu-id="6cf6b-114">Een app te registreren.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-114">Register an app.</span></span>
2. <span data-ttu-id="6cf6b-115">Uw app instellen om te gebruiken de `passport-azure-ad` strategie.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-115">Set up your app to use the `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="6cf6b-116">U gebruikt Passport om aan- en afmeldingsaanvragen te verzenden naar Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-116">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="6cf6b-117">Gegevens over de gebruiker afdrukken.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-117">Print data about the user.</span></span>

<span data-ttu-id="6cf6b-118">De code voor deze zelfstudie wordt onderhouden in [GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="6cf6b-118">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="6cf6b-119">Als u wilt volgen, kunt u [basis van de app downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) of het geraamte:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-119">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="6cf6b-120">De voltooide toepassing wordt verstrekt aan het einde van deze zelfstudie ook.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-120">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="6cf6b-121">Stap 1: Een app registreren</span><span class="sxs-lookup"><span data-stu-id="6cf6b-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="6cf6b-122">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6cf6b-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="6cf6b-123">Selecteer in het menu aan de bovenkant van de pagina uw account.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-123">In the menu at the top of the page, select your account.</span></span> <span data-ttu-id="6cf6b-124">Onder de **Directory** kiest u de Active Directory-tenant waar u uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-124">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="6cf6b-125">Selecteer **meer Services** in het menu aan de linkerkant van het scherm en selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-125">Select **More Services** in the menu on the left side of the screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="6cf6b-126">Selecteer **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="6cf6b-127">Volg de aanwijzingen voor het maken van een **webtoepassing** en/of **WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-127">Follow the prompts to create a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="6cf6b-128">De **naam** beschrijft uw toepassing voor gebruikers van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-128">The **name** of the application describes your application to users.</span></span>

  * <span data-ttu-id="6cf6b-129">De **aanmeldings-URL** is de basis-URL van uw app.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-129">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="6cf6b-130">Het basisproject standaardwaarde is "http://localhost: 3000/auth/openid/return ''.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-130">The skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="6cf6b-131">Nadat u hebt geregistreerd, wijst Azure AD van uw app een unieke toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="6cf6b-132">U moet deze waarde in de volgende secties, dus kopiëren van de toepassingspagina.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-132">You need this value in the following sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="6cf6b-133">Van de **instellingen** -> **eigenschappen** pagina voor uw toepassing, het bijwerken van de App ID URI.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-133">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="6cf6b-134">De **App ID URI** is de unieke id voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-134">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="6cf6b-135">De overeenkomst is met de indeling `https://<tenant-domain>/<app-name>`, bijvoorbeeld: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-135">The convention is to use the format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-to-your-directory"></a><span data-ttu-id="6cf6b-136">Stap 2: Vereisten voor uw directory toevoegen</span><span class="sxs-lookup"><span data-stu-id="6cf6b-136">Step 2: Add prerequisites to your directory</span></span>
1. <span data-ttu-id="6cf6b-137">Vanaf de opdrachtregel, wijzig de mappen in de hoofdmap bent u niet al er, en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-137">From the command line, change directories to your root folder if you're not already there, and then run the following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="6cf6b-138">U moet bovendien `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="6cf6b-139">Hiermee installeert u de bibliotheken die `passport-azure-ad` is afhankelijk van.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-139">This installs the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="6cf6b-140">Stap 3: Uw app instellen voor het gebruik van de strategie passport-knooppunt-js</span><span class="sxs-lookup"><span data-stu-id="6cf6b-140">Step 3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="6cf6b-141">We configureren hier snelle voor het gebruik van het OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-141">Here, we configure Express to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="6cf6b-142">Passport wordt gebruikt om verschillende dingen, met inbegrip van probleem aanmelden en afmeldingsaanvragen te verzenden, sessie van de gebruiker beheren en informatie ophalen over de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-142">Passport is used to do various things, including issue sign-in and sign-out requests, manage the user's session, and get information about the user.</span></span>

1. <span data-ttu-id="6cf6b-143">Om te beginnen, opent u de `config.js` bestand in de hoofdmap van het project en voer vervolgens de configuratiewaarden van uw app in de `exports.creds` sectie.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-143">To begin, open the `config.js` file at the root of the project, and then enter your app's configuration values in the `exports.creds` section.</span></span>

  * <span data-ttu-id="6cf6b-144">De `clientID` is de **toepassings-Id** die toegewezen aan uw app in de portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-144">The `clientID` is the **Application Id** that's assigned to your app in the registration portal.</span></span>

  * <span data-ttu-id="6cf6b-145">De `returnURL` is de **omleidings-Uri** die u hebt ingevoerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-145">The `returnURL` is the **Redirect Uri** that you entered in the portal.</span></span>

  * <span data-ttu-id="6cf6b-146">De `clientSecret` is het geheim die u hebt gegenereerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-146">The `clientSecret` is the secret that you generated in the portal.</span></span>

2. <span data-ttu-id="6cf6b-147">Open vervolgens de `app.js` bestand in de hoofdmap van het project.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-147">Next, open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="6cf6b-148">Voeg de volgende oproep verzenden om aan te roepen de `OIDCStrategy` strategie die wordt geleverd met `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-148">Then add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="6cf6b-149">Gebruik daarna de strategie die we zojuist waarnaar wordt verwezen voor het afhandelen van onze aanvragen aanmelden.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-149">After that, use the strategy we just referenced to handle our sign-in requests.</span></span>

    ```JavaScript
    // Use the OIDCStrategy within Passport. (Section 2)
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
<span data-ttu-id="6cf6b-150">Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort) die alle schrijvers van strategieën voor.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="6cf6b-151">De strategie bekijkt, ziet u dat geven we een functie die een token en een gereed als parameters heeft.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-151">Looking at the strategy, you see that we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="6cf6b-152">De strategie komt weer naar ons nadat deze zijn werk doet.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-152">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="6cf6b-153">We willen vervolgens om de gebruiker op te slaan en het token niet initialiseren zodat we niet hoeven te vragen voor het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-153">Then we want to store the user and stash the token so we don't need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="6cf6b-154">De vorige code wordt elke gebruiker die plaatsvindt om te verifiëren met onze server.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-154">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="6cf6b-155">Dit wordt automatische registratie genoemd.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-155">This is known as auto-registration.</span></span> <span data-ttu-id="6cf6b-156">Het is raadzaam dat u niet toestaan dat iedereen bij een productieserver zonder dat zij worden geregistreerd via een proces dat u kiest eerst geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-156">We    recommend that you don't let anyone authenticate to a production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="6cf6b-157">Dit is doorgaans het patroon die u ziet in consumenten-apps, waarmee u kunt registreren met Facebook, maar vervolgens vraagt u om aanvullende informatie te geven.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-157">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to provide additional information.</span></span> <span data-ttu-id="6cf6b-158">Als dit niet een voorbeeldtoepassing, kan hebben we e-mailadres van de gebruiker opgehaald uit het Tokenobject dat wordt geretourneerd en wordt vervolgens gevraagd de gebruiker om aanvullende informatie in te vullen.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-158">If this weren't a sample application, we could have extracted the user's email address from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="6cf6b-159">Omdat dit een testserver is, wordt deze toevoegen aan de database in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-159">Because this is a test server, we add them to the in-memory database.</span></span>


4. <span data-ttu-id="6cf6b-160">Vervolgens laten we de methoden waarmee we voor het bijhouden van de aangemelde gebruikers zoals vereist door Passport toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-160">Next, let's add the methods that enable us to track the signed-in users as required by Passport.</span></span> <span data-ttu-id="6cf6b-161">Deze methoden omvatten serialiseren en deserialiseren van gegevens van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-161">These methods include serializing and deserializing the user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   To support persistent sign-in sessions, Passport needs to be able to
            //   serialize users into the session and deserialize them out of the session. Typically,
            //   this is done simply by storing the user ID when serializing and finding
            //   the user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array to hold signed-in users
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

5.  <span data-ttu-id="6cf6b-162">Vervolgens voegen we de code voor het laden van de Express-engine.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-162">Next, let's add the code to load the Express engine.</span></span> <span data-ttu-id="6cf6b-163">Hier gebruiken we de standaard /views en /routes patroon dat Express biedt.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-163">Here we use the default /views and /routes pattern that Express provides.</span></span>

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
          // Initialize Passport!  Also use passport.session() middleware, to support
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. <span data-ttu-id="6cf6b-164">Laten we Voeg de routes die aanlevert de werkelijke aanmelden aanvragen voor de `passport-azure-ad` engine:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-164">Finally, let's add the routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware to authenticate the
        //   request. The first step in OpenID authentication involves redirecting
        //   the user to their OpenID provider. After authenticating, the OpenID
        //   provider redirects the user back to this application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in the Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="6cf6b-165">Stap 4: Gebruik Passport om aan- en afmeldingsaanvragen te verzenden naar Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cf6b-165">Step 4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="6cf6b-166">Uw app is nu geconfigureerd om te communiceren met het eindpunt met behulp van het OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-166">Your app is now properly configured to communicate with the endpoint by using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="6cf6b-167">`passport-azure-ad`heeft gezorgd voor de details van verificatieberichten, het valideren van tokens van Azure AD en het onderhoud van gebruikerssessies.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-167">`passport-azure-ad` has taken care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="6cf6b-168">Alle resterende is door uw gebruikers te kunnen aanmelden en afmelden en verzamelen van aanvullende informatie over de aangemelde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-168">All that remains is giving your users a way to sign in and sign out, and gathering additional information about the signed-in users.</span></span>

1. <span data-ttu-id="6cf6b-169">Eerst gaan we de standaard, aanmelden, account en toevoegen afmeldingsmethoden toe aan onze `app.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-169">First, let's add the default, sign-in, account, and sign-out methods to our `app.js` file:</span></span>

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
            log.info('Login was called in the Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="6cf6b-170">Laten we controleert deze onderdelen:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="6cf6b-171">De `/`route wordt omgeleid naar de weergave index.ejs doorgeven van de gebruiker in de aanvraag (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="6cf6b-171">The `/`route redirects to the index.ejs view, passing the user in the request (if it exists).</span></span>
  * <span data-ttu-id="6cf6b-172">De `/account` eerst routeren *zorgt ervoor dat we worden geverifieerd* (we implementeren die in het volgende voorbeeld), en wordt de gebruiker doorgegeven in de aanvraag zodat we extra informatie over de gebruiker kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-172">The `/account` route first *ensures we are authenticated* (we implement that in the following example), and then passes the user in the request so that we can get additional information about the user.</span></span>
  * <span data-ttu-id="6cf6b-173">De `/login` route roept onze verificator azuread openidconnect van `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-173">The `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="6cf6b-174">Als dat niet lukt, wordt de gebruiker omgeleid naar /login.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-174">If that doesn't succeed, it redirects the user back to /login.</span></span>
  * <span data-ttu-id="6cf6b-175">De `/logout` gewoon aanroepen de logout.ejs (en route) die worden cookies gewist en retourneert vervolgens de gebruiker terug naar index.ejs routeren.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-175">The `/logout` route simply calls the logout.ejs (and route), which clears cookies and then returns the user back to index.ejs.</span></span>

3. <span data-ttu-id="6cf6b-176">Voor het laatste deel van `app.js`, voegen we de **EnsureAuthenticated** methode die wordt gebruikt in `/account`, zoals eerder is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-176">For the last part of `app.js`, let's add the **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware to ensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs to be protected. If
        //   the request is authenticated (typically via a persistent sign-in session),
        //   the request proceeds. Otherwise, the user is redirected to the
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="6cf6b-177">Maak ten slotte de server zelf laten we in `app.js`:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-177">Finally, let's create the server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-to-display-our-user-in-the-website-create-the-views-and-routes-in-express"></a><span data-ttu-id="6cf6b-178">Stap 5: Zodat de gebruiker in de website maken de weergaven en routes in Express</span><span class="sxs-lookup"><span data-stu-id="6cf6b-178">Step 5: To display our user in the website, create the views and routes in Express</span></span>
<span data-ttu-id="6cf6b-179">Nu `app.js` is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-179">Now `app.js` is complete.</span></span> <span data-ttu-id="6cf6b-180">Moet u de routes en weergaven waarin de informatie die we u aan de gebruiker, evenals verwerken toevoegen de `/logout` en `/login` routes die we hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-180">We simply need to add the routes and views that show the information we get to the user, as well as handle the `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="6cf6b-181">Maak de route `/routes/index.js` onder de hoofddirectory.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-181">Create the `/routes/index.js` route under the root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="6cf6b-182">Maak de route `/routes/user.js` onder de hoofddirectory.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-182">Create the `/routes/user.js` route under the root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="6cf6b-183">Deze doorgegeven de aanvraag aan onze weergaven, met inbegrip van de gebruiker, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-183">These pass along the request to our views, including the user if present.</span></span>

3. <span data-ttu-id="6cf6b-184">Maak de weergave `/views/index.ejs` onder de hoofddirectory.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-184">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="6cf6b-185">Dit is een eenvoudige pagina waarmee onze aanmelding en afmelding methoden aangeroepen en kan we accountgegevens halen.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-185">This is a simple page that calls our login and logout methods and enables us to grab account information.</span></span> <span data-ttu-id="6cf6b-186">U ziet dat we de voorwaardelijke kunnen gebruiken `if (!user)` als de gebruiker wordt doorgegeven in de aanvraag is bewijs hebben we een aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-186">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="6cf6b-187">Maak de `/views/account.ejs` weergeven onder de hoofddirectory, zodat we extra informatie kunt bekijken die `passport-azuread` in de gebruikersaanvraag heeft geplaatst.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-187">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azuread` has put in the user request.</span></span>

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

5. <span data-ttu-id="6cf6b-188">We maken dit goed door het toevoegen van een lay-out.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="6cf6b-189">Maak de ' / views/layout.ejs' weergave onder de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-189">Create the '/views/layout.ejs' view under the root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="6cf6b-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6cf6b-190">Next steps</span></span>
<span data-ttu-id="6cf6b-191">Ten slotte bouwen en uitvoeren van uw app.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-191">Finally, build and run your app.</span></span> <span data-ttu-id="6cf6b-192">Voer `node app.js`, en ga vervolgens naar `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-192">Run `node app.js`, and then go to `http://localhost:3000`.</span></span>

<span data-ttu-id="6cf6b-193">Meld u aan met een persoonlijk Microsoft-account of een account voor werk of school en zien hoe de identiteit van de gebruiker wordt weergegeven in de lijst /account.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-193">Sign in with either a personal Microsoft account or a work or school account, and notice how the user's identity is reflected in the /account list.</span></span> <span data-ttu-id="6cf6b-194">U hebt nu een web-app die beveiligd met standaardprotocollen die gebruikers met hun persoonlijke en zakelijke/school accounts kunnen worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="6cf6b-195">Voor naslag is het voltooide voorbeeld (zonder uw configuratiewaarden) [geleverd als zip-bestand](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="6cf6b-195">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="6cf6b-196">U kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="6cf6b-197">U kunt nu verplaatsen naar geavanceerdere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="6cf6b-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="6cf6b-198">Het is raadzaam om te proberen:</span><span class="sxs-lookup"><span data-stu-id="6cf6b-198">You might want to try:</span></span>

[<span data-ttu-id="6cf6b-199">Een Web-API met Azure AD beveiligen</span><span class="sxs-lookup"><span data-stu-id="6cf6b-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
