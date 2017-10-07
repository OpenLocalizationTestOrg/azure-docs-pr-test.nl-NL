---
title: aaaAzure AD Node.js aan de slag | Microsoft Docs
description: "Hoe toobuild een REST Node.js-web-API die kan worden geïntegreerd met Azure AD voor verificatie."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a>Aan de slag met web-API's voor Node.js
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

*Passport* is verificatiemiddleware voor Node.js. Flexibel en modulair, Passport onopvallend in tooany kan worden verwijderd op basis van de Express of Restify-webtoepassing. Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer. We hebben een strategie ontwikkeld voor Microsoft Azure Active Directory (Azure AD). We installeert deze module en voegt u Hallo Microsoft Azure Active Directory `passport-azure-ad` invoegtoepassing.

toodo, moet u:

1. U registreert een toepassing met Azure AD.
2. Instellen van uw app toouse Passport van `passport-azure-ad` invoegtoepassing.
3. Configureer een client toepassing toocall hello tooDo lijst web-API.

Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).

> [!NOTE]
> In dit artikel wordt niet beschreven hoe tooimplement aanmelden, registreren, of profiel management met Azure AD B2C. Dit artikel gaat over het aanroepen van web API's nadat Hallo gebruiker al is geverifieerd.  Het is raadzaam dat u met begint [hoe toointegrate met Azure Active Directory-document](active-directory-how-to-integrate.md) toolearn over Hallo basisprincipes van Azure Active Directory.
>
>

We alle Hallo broncode bijvoorbeeld uitgevoerd in GitHub onder een MIT-licentie hebt uitgebracht dus gratis tooclone (of zelfs beter fork) en feedback geven en pull-aanvragen.

## <a name="about-nodejs-modules"></a>Over Node.js-modules
We Node.js-modules gebruiken in dit scenario. Modules zijn geladen JavaScript-pakketten die specifieke functionaliteit voor uw toepassing bieden. U installeren meestal modules met behulp van Node.js een opdrachtregelprogramma NPM Hallo in Hallo NPM-installatiemap. Sommige modules, zoals Hallo HTTP-module, zijn echter opgenomen in Hallo core Node.js-pakket.

Geïnstalleerde modules worden opgeslagen in Hallo **node_modules** map in de hoofdmap Hallo van uw Node.js-installatiemap. Elke module Hallo **node_modules** directory onderhoudt een eigen **node_modules** map waarin zich geen modules die afhankelijk zijn van. Ook elke vereiste module heeft een **node_modules** directory. Deze directory recursieve structuur vertegenwoordigt Hallo afhankelijkheidsketen.

Deze structuur van de keten afhankelijkheid resulteert in een grotere toepassing footprint. Maar ook wordt hiermee gegarandeerd dat alle afhankelijkheden wordt voldaan en die Hallo-versie van het Hallo-modules die wordt gebruikt in ontwikkeling ook in productie gebruikt wordt. Dit gedrag Hallo productie-app beter voorspelbaar maakt en voorkomt dat versioning problemen die gevolgen voor gebruikers hebben mogelijk.

## <a name="step-1-register-an-azure-ad-tenant"></a>Stap 1: Een Azure AD-tenant registreren
toouse dit steekproef, moet u een Azure Active Directory-tenant. Als u niet zeker weet welke tenant of hoe tooget, Zie [hoe tooget een Azure AD-tenant](active-directory-howto-tenant.md).

## <a name="step-2-create-an-application"></a>Stap 2: Een toepassing maken
Vervolgens maakt u een app in uw directory dat biedt Azure AD-informatie dat het toosecurely moet met uw app communiceren.  Zowel Hallo client-app en web-API worden aangegeven met één **toepassings-ID** in dit geval omdat ze samen één logische app vormen.  toocreate een app, volg [deze instructies](active-directory-how-applications-are-added.md). Als u een line-of-business-app bouwt [deze aanvullende instructies nuttig kunnen zijn](../active-directory-applications-guiding-developers-for-lob-applications.md).

een toepassing toocreate:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. In het bovenste menu hello, selecteert u uw account. Klik vervolgens onder Hallo **Directory** Hallo Active Directory-tenant waar u tooregister Kies uw toepassing.

3. Selecteer in het menu aan de linkerkant Hallo Hallo **meer Services**, en selecteer vervolgens **Azure Active Directory**.

4. Selecteer **App registraties**, en selecteer vervolgens **toevoegen**.

5. Ga als volgt Hallo prompts toocreate een **webtoepassing en/of WebAPI**.

      * Hallo **naam** Hallo toepassing beschrijving van uw toepassing tooend gebruikers.

      * Hallo **aanmeldings-URL** Hallo basis-URL van uw app is.  standaard-URL van de voorbeeldcode Hallo is Hallo `https://localhost:8080`.

6. Nadat u hebt geregistreerd, wijst Azure AD uw app een unieke id U moet deze waarde in de volgende secties hello, dus kopiëren van de pagina van de toepassing hello.

7. Van Hallo **instellingen** -> **eigenschappen** pagina voor uw toepassing, Hallo App ID URI bijwerken. Hallo **App ID URI** is de unieke id voor uw toepassing. Hallo-conventie is toouse `https://<tenant-domain>/<app-name>`, bijvoorbeeld: `https://contoso.onmicrosoft.com/my-first-aad-app`.

8. Maak een **sleutel** voor uw toepassing uit Hallo **instellingen** pagina en kopieer het ergens. U moet deze binnenkort.

## <a name="step-3-download-nodejs-for-your-platform"></a>Stap 3: Node.js voor uw platform downloaden
toosuccessfully dit voorbeeld gebruiken, moet u een werkende implementatie van Node.js hebben.

Installeer Node.js vanuit [http://nodejs.org](http://nodejs.org).

## <a name="step-4-install-mongodb-on-your-platform"></a>Stap 4: Installatie MongoDB op uw platform
toosuccessfully dit voorbeeld gebruiken, moet u een werkende implementatie van MongoDB hebben. U MongoDB toomake Hallo REST-API persistent gebruiken in alle serverexemplaren.

Installeer MongoDB vanuit [http://mongodb.org](http://www.mongodb.org).

> [!NOTE]
> In dit scenario wordt ervan uitgegaan dat u Hallo standaard en -servereindpunten voor MongoDB, die op moment van schrijven van dit Hallo mongodb://localhost is.
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a>Stap 5: Hallo Restify-modules installeren in uw web-API
We gebruiken Restify toobuild onze REST-API. Restify is een minimaal en flexibel Node.js-toepassingsframework dat afgeleid van Express. Het bevat een set krachtige functies voor het ontwikkelen van REST-API's op Connect.

### <a name="install-restify"></a>Restify installeren
1. Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** directory. Als hello **azuread** directory niet bestaat, maakt.

        `cd azuread - or- mkdir azuread; cd azuread`

2. Type Hallo volgende opdracht:

    `npm install restify`

    Met deze opdracht wordt Restify geïnstalleerd.

#### <a name="did-you-get-an-error"></a>Krijgt u een foutmelding?
Wanneer u NPM op sommige besturingssystemen gebruikt, wordt u er een foutmelding waarin wordt gemeld **fout: EPERM, type chmod ' / usr/lokale/bin /...'** en een suggestie dat u actieve Hallo-account als beheerder probeert. Als dit het geval is, gebruik van Hallo sudo-opdracht toorun NPM op een hoger niveau van bevoegdheden.

#### <a name="did-you-get-an-error-regarding-dtrace"></a>Krijgt u een fout met betrekking tot DTRACE?
U ziet een fout als volgt wanneer u Restify installeert:

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
Restify biedt een krachtig mechanisme om REST-aanroepen te traceren met behulp van DTrace. Veel besturingssystemen hoeft echter geen DTrace. U kunt deze fouten negeren.

Hallo-uitvoer van deze opdracht ziet er vergelijkbare toohello volgende uitvoer:

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


## <a name="step-6-install-passportjs-in-your-web-api"></a>Stap 6: Installatie Passport.js in uw web-API
[Passport](http://passportjs.org/) is verificatiemiddleware voor Node.js. Flexibel en modulair, Passport onopvallend in tooany kan worden verwijderd op basis van de Express of Restify-webtoepassing. Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer.

We hebben een strategie ontwikkeld voor Azure Active Directory. We installeert deze module en voeg vervolgens hello Azure Active Directory strategie-invoegtoepassing.

1. Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** directory.

2. tooinstall passport.js, Voer Hallo volgende opdracht:

    `npm install passport`

    Hallo-uitvoer van Hallo opdracht ziet er vergelijkbare toohello volgende:

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a>Stap 7: Passport-Azure-AD tooyour web API toevoegen
Naast we Hallo OAuth-strategie toevoegen met behulp van `passport-azure-ad`, een reeks strategieën die verbinding maken met Azure Active Directory-tooPassport. We gebruiken deze strategie voor bearer-tokens in dit voorbeeld REST-API.

> [!NOTE]
> Hoewel OAuth2 een kader waarin elk onbekend type token kan worden uitgegeven, worden alleen bepaalde typen worden vaak gebruikt. Bearer-tokens zijn de meest gebruikte Hallo tokens voor het beveiligen van eindpunten. Type Hallo meest wordt uitgegeven in OAuth2-token zijn. Veel implementaties wordt ervan uitgegaan dat bearer-tokens zijn alleen type Hallo van tokens die zijn uitgegeven.
>
>

Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** directory.

Type Hallo volgende opdracht tooinstall hello Passport.js `passport-azure-ad module`:

`npm install passport-azure-ad`

Hallo-uitvoer van Hallo opdracht ziet er vergelijkbare toohello volgende uitvoer:


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a>Stap 8: MongoDB-modules tooyour web API toevoegen
We gebruikt MongoDB als onze gegevensarchief. Daarom moeten we tooinstall Hallo veelgebruikte invoegtoepassing aangeroepen Mongoose toomanage modellen en schema's. Er moet ook tooinstall Hallo databasestuurprogramma voor MongoDB (dit wordt ook MongoDB genoemd).

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a>Stap 9: Aanvullende modules installeren
Naast er Hallo resterende vereiste modules worden geïnstalleerd.

1. Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.

    `cd azuread`

2. Voer Hallo opdrachten tooinstall na deze modules in uw **node_modules** directory:

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a>Stap 10: Een server.js met de afhankelijkheden maken
Hallo server.js-bestand bevat de meeste Hallo-functionaliteit voor onze web API-server. We toevoegen onze toothis codebestand de meeste. Voor productiedoeleinden, is het raadzaam dat u Hallo-functionaliteit in kleinere bestanden, zoals afzonderlijke routes en controllers opsplitsen. In deze demonstratie gebruiken we server.js voor deze functionaliteit.

1. Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.

    `cd azuread`

2. Maak een `server.js` bestand in uw favoriete editor en voeg vervolgens Hallo volgende informatie:

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. Hallo-bestand opslaan. Er wordt kort tooit geretourneerd.

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a>Stap 11: Maak een bestand config toostore uw Azure AD-instellingen
Dit codebestand geeft de configuratieparameters Hallo van uw Azure Active Directory-portal tooPassport.js. U hebt deze configuratiewaarden gemaakt wanneer u API Hallo-toohello webportal toegevoegd in de eerste deel Hallo Hallo stapsgewijze kennismaking. We uitleggen welke tooput Hallo waarden van deze parameters wanneer u Hallo code hebt gekopieerd.

1. Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.

    `cd azuread`

2. Maak een `config.js` bestand in uw favoriete editor en voeg vervolgens Hallo volgende informatie:

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. Hallo-bestand opslaan.

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a>Stap 12: Waarden tooyour server.js configuratiebestand toevoegen
We moeten deze waarden van Hallo .config-bestand dat u hebt gemaakt tooread via onze toepassing. toodo, we Hallo .config-bestand als een vereiste bron in onze toepassing toevoegen. We Stel Hallo globale variabelen toomatch Hallo variabelen in Hallo config.js document.

1. Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.

    `cd azuread`

2. Open uw `server.js` bestand in uw favoriete editor en voeg vervolgens Hallo volgende informatie:

    ```Javascript
    var config = require('./config');
    ```
3. Voeg een nieuwe sectie te`server.js` Hello code te volgen:

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. Hallo-bestand opslaan.

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Stap 13: Hallo MongoDB-Model en de schemagegevens toevoegen met behulp van Mongoose
Alle deze voorbereiding gaat nu toostart betaalt uitschakelen als we deze drie bestanden in een REST-API-service combineren.

Voor dit scenario we gebruiken MongoDB toostore onze taken, zoals beschreven in stap 4.

In Hallo `config.js` bestand dat wordt gemaakt in stap 11, we onze database aangeroepen `tasklist`, omdat die was we plaatsen aan Hallo einde van onze **mogoose_auth_local** verbindings-URL. U hoeft niet toocreate deze vooraf in MongoDB-database. In plaats daarvan maakt MongoDB dit voor ons op Hallo eerst het uitvoeren van de servertoepassing (ervan uitgaande dat Hallo de database nog niet bestaat).

Nu we hebben Hallo server u welke MongoDB-database verteld willen we graag toouse, moeten we toowrite enkele aanvullende code toocreate Hallo model en het schema voor onze server taken.

### <a name="discussion-of-hello-model"></a>Beschrijving van de Hallo-model
Onze schemamodel is eenvoudig. U uitbreiden het naar behoefte.

NAAM: naam van Hallo van Hallo persoon die toohello taak is toegewezen. Een **tekenreeks**.

TAAK: Hallo taak zelf. Een **tekenreeks**.

DATUM: Hallo datum die taak Hallo vervalt. EEN **DATETIME**.

VOLTOOID: Als Hallo-taak is voltooid of niet. EEN **BOOLEAANSE**.

### <a name="creating-hello-schema-in-hello-code"></a>Hallo-schema maken in Hallo code
1. Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.

    `cd azuread`

2. Open uw `server.js` bestand in uw favoriete editor en voeg vervolgens de volgende informatie hieronder configuratievermelding Hallo Hallo:

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
    var TaskSchema = new Schema({
        owner: String,
        task: String,
        completed: Boolean,
        date: Date
    });

    // Use hello schema tooregister a model.
    mongoose.model('Task', TaskSchema);
    var Task = mongoose.model('Task');
    ```
Zoals u vanuit Hallo code ziet, maken we onze schema eerst. Vervolgens we een modelobject dat we toostore onze gegevens in de gehele Hallo code maken wanneer we definiëren gebruiken onze **Routes**.

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a>Step 14: Onze routes toevoegen voor onze REST-API-taakserver
Nu we hebben een database model toowork met, gaan we toevoegen Hallo routes we gaan gebruiken voor onze REST-API-server zijn.

### <a name="about-routes-in-restify"></a>Routes in Restify
Routes werken in Restify Hallo dezelfde manier ze in Hallo Express stack. U definieert routes met behulp van Hallo URI dat u Hallo client toepassingen toocall verwacht. Meestal kunt definiëren u uw routes in een afzonderlijk bestand. Wij gebruiken we onze routes in Hallo server.js-bestand geplaatst. Het is raadzaam dat u rekening te houden deze routes in een eigen bestand voor gebruik in productieomgevingen.

Een doorsnee patroon voor een Restify-route is als volgt:

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


Dit is Hallo patroon op het meest eenvoudige niveau. Restify (en Express) bieden veel diepere functionaliteit, zoals het definiëren van toepassingstypen en het geven van complexe routering tussen verschillende eindpunten. Voor onze toepassing, zijn we deze routes eenvoudig houden.

### <a name="add-default-routes-tooour-server"></a>Standaard routes tooour server toevoegen
We nu toevoegen Hallo eenvoudige CRUD-routes voor het maken, ophalen, bijwerken en verwijderen.

1. Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er:

    `cd azuread`

2. Open Hallo `server.js` bestand in uw favoriete editor en voeg vervolgens Hallo informatie hieronder Hallo vorige items in de database die u hebt aangebracht na:

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}


// Delete a task by name.

function removeTask(req, res, next) {

    Task.remove({
        task: req.params.task,
        owner: owner
    }, function(err) {
        if (err) {
            req.log.warn(err,
                'removeTask: unable toodelete %s',
                req.params.task);
            next(err);
        } else {
            log.info('Deleted task:', req.params.task);
            res.send(204);
            next();
        }
    });
}

// Delete all tasks.

function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
}


// Get a specific task based on name.

function getTask(req, res, next) {

    log.info('getTask was called for: ', owner);
    Task.find({
        owner: owner
    }, function(err, data) {
        if (err) {
            req.log.warn(err, 'get: unable tooread %s', owner);
            next(err);
            return;
        }

        res.json(data);
    });

    return next();
}

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a>Fout tijdens verwerken van in onze API's toevoegen
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a>Stap 15: De server maken
We hebben onze database gedefinieerd en onze routes aanwezig zijn. het laatste wat toodo Hallo is Hallo server-exemplaar dat onze aanroepen beheert toevoegen.

In Restify (en Express) kunt u een groot aantal aanpassing voor een REST-API-server uitvoeren, maar opnieuw gaan we toouse Hallo meest eenvoudige configuratie voor onze toepassing.

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a>Stap 16: Hallo routes toohello server (zonder verificatie nu) toevoegen
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler.
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a>Stap 17: Voer Hallo-server (voordat het OAuth-ondersteuning toe te voegen)
Testen van uw server voordat we verificatie toe te voegen.

de eenvoudigste manier tootest Hallo uw server is curl gebruikt in een opdrachtregel. Voordat we dat doen, moeten we een hulpprogramma waarmee we tooparse uitvoer als JSON.

1. Hallo volgende JSON-hulpprogramma (alle Hallo volgen voorbeelden Gebruik dit hulpprogramma) installeren:

    `$npm install -g jsontool`

    Hiermee installeert globaal Hallo JSON-hulpprogramma. Nu dat we dat hebt gedaan, gaat spelen met Hallo-server:

2. Controleer eerst of dat het mongoDB-exemplaar wordt uitgevoerd:

    `$sudo mongod`

3. Vervolgens wijzigen toohello directory en start curling:

    `$ cd azuread` `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4. Vervolgens kunt we toevoegen een taak op deze manier:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    Hallo-antwoord moet zijn:

        ```Shell
        HTTP/1.1 201 Created
        Connection: close
        Access-Control-Allow-Origin: *
        Access-Control-Allow-Headers: X-Requested-With
        Content-Type: application/x-www-form-urlencoded
        Content-Length: 5
        Date: Tue, 04 Feb 2014 01:02:26 GMT
        Hello
        ```
    En we kunnen een lijst met taken voor Brandon op deze manier:

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Als alle dit werkt, we klaar tooadd OAuth toohello REST-API-server.

U hebt een REST-API-server met MongoDB!

## <a name="step-18-add-authentication-tooour-rest-api-server"></a>Stap 18: Authentication tooour REST-API-server toevoegen
Nu dat we een actieve REST-API hebben, begint het van groot belang met Azure AD.

Vanaf de opdrachtregel Hallo wijzigen mappen toohello **azuread** map als u niet al er.

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Hallo OIDCBearerStrategy die is opgenomen in passport-azure-ad gebruiken
Tot nu toe hebben we een typische REST-TODO-server zonder enige vorm van autorisatie gebouwd. Dit is waar u begint het samenstellen.

1. We moeten eerst tooindicate willen we toouse Passport. Dit recht na de andere serverconfiguratie genomen:

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > Wanneer u schrijft API's, het is raadzaam dat u altijd Hallo gegevens toosomething uniek in vergelijking met het Hallo-token dat Hallo gebruiker koppelt niet kunnen vervalsen. Wanneer deze server TODO-items opslaat, slaat deze op basis van Hallo object-ID van gebruiker in de Hallo in Hallo-token (aangeroepen via token.oid), die we in Hallo 'eigenaar' veld plaatsen. Dit zorgt ervoor dat alleen die gebruiker toegang heeft tot hun TODOs. Er is geen blootstelling in Hallo API van de 'eigenaar' zodat een externe gebruiker Hallo TODOs van anderen aanvragen kan, zelfs als ze zijn geverifieerd.                    

2. Volgende we gebruiken Hallo bearer-strategie die wordt geleverd met `passport-azure-ad`. Bekijkt hello code nu en wordt uitgelegd Hallo rest binnenkort. Plaats deze achter u hebt geplakt hierboven:

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
    **/

    var findById = function(id, fn) {
        for (var i = 0, len = users.length; i < len; i++) {
            var user = users[i];
            if (user.sub === id) {
                log.info('Found user: ', user);
                return fn(null, user);
            }
        }
        return fn(null, null);
    };


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

Passport wordt een vergelijkbaar patroon gebruikt voor alle strategieën (Twitter, Facebook, enzovoort) die alle schrijvers van strategieën voor. Hallo-strategie bekijkt, ziet u geven we een functie die een token en een gereed heeft als Hallo-parameters. Hallo-strategie komt weer toous nadat deze zijn werk doet. Nadat het geval is, Hallo gebruiker en opgeslagen stash Hallo token zodat we niet opnieuw tooask voor het opnieuw hoeft.

> [!IMPORTANT]
> Hallo vorige code wordt elke gebruiker die tooauthenticate tooour server plaatsvindt. Dit wordt automatische registratie genoemd. In productieservers doorlopen u die wordt aangeraden dat u niet toestaan dat iedereen zonder dat zij eerst een registratieproces die u kiest. Dit is meestal Hallo patroon dat u ziet in consumenten-apps, die vervolgens vraagt u toofill aanvullende informatie, maar kunnen u tooregister met Facebook. Als dit niet een opdrachtregelprogramma, kan hebben we Hallo e opgehaald uit Hallo Tokenobject dat wordt geretourneerd en wordt vervolgens gevraagd Hallo gebruiker toofill aanvullende informatie. Omdat dit een testserver, we gewoon ze toohello in-memory database toevoegen.
>
>

### <a name="protect-some-endpoints"></a>Sommige eindpunten beveiligen
U beveiligt de eindpunten door te geven Hallo `passport.authenticate()` aanroep met het Hallo-protocol dat u wilt dat toouse.

onze servercode doen iets meer interessante toomake Hallo route Hiermee kunt bewerken.

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a>Stap 19: De servertoepassing opnieuw uitvoeren en zorg ervoor dat u wordt geweigerd
We gebruiken `curl` opnieuw toosee als we nu OAuth2-bescherming tegen onze eindpunten. We doen deze test voordat u een van onze client-SDK's met dit eindpunt uitvoert. Hallo headers die worden geretourneerd moeten voldoende tootell ons als gaan we omlaag rechts Hallo-pad.

1. Controleer eerst of dat het mongoDB-exemplaar wordt uitgevoerd:

    `$sudo mongod`

2. Vervolgens wijzigen toohello directory en start curling.

      `$ cd azuread` `$ node server.js`

3. Probeer een basic POST.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

Een 401 is Hallo-reactie die u hier zoekt. Dit antwoord geeft aan dat Hallo Passport-laag probeert tooredirect toohello geautoriseerd eindpunt, is precies wat u wilt.

## <a name="next-steps"></a>Volgende stappen
U bent gegaan zo ver mogelijk kunt u met deze server zonder met behulp van een OAuth2-compatibele client. U moet toogo via een extra scenario.

U hebt nu geleerd hoe tooimplement een REST-API met behulp van Restify en OAuth2. Hebt u ook meer dan voldoende code tookeep uw service ontwikkelen en te leren hoe toobuild op dit voorbeeld.

Als u geïnteresseerd in de volgende stappen Hallo in uw ADAL reis bent, vindt hier u enkele ondersteunde ADAL clients het is raadzaam dat u met blijven werken.

Omlaag tooyour developer machine klonen en configureren zoals beschreven in het Hallo-scenario.

[ADAL voor iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[ADAL voor Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
