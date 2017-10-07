---
title: 'Azure AD B2C: Een web-API beveiligen met behulp van Node.js | Microsoft Docs'
description: Hoe toobuild een Node.js web-API accepteert die tokens van een B2C-tenant
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a>Azure AD B2C: Een web-API ontwikkelen met behulp van Node.js
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

Met Azure Active Directory (Azure AD) B2C kunt u een web-API beveiligen met OAuth 2.0-toegangstokens. Deze tokens kunnen client-apps die gebruikmaken van Azure AD B2C tooauthenticate toohello API. Dit artikel laat zien hoe een API 'takenlijst' toocreate waarmee gebruikers tooadd en de lijst met taken. Hallo-web-API is beveiligd met Azure AD B2C en alleen hun takenlijst kan toomanage geverifieerde gebruikers.

> [!NOTE]
> Dit voorbeeld is geschreven met het toobe verbonden tooby met onze [iOS B2C-voorbeeldtoepassing](active-directory-b2c-devquickstarts-ios.md). Hallo huidige procedure eerst doen en volg daarna dat voorbeeld.
>
>

**Passport** is verificatiemiddleware voor Node.js. Passport is flexibel en modulair, en kan onopvallend worden geïnstalleerd in een Express- of Restify-webtoepassing. Een uitgebreide set strategieën ondersteunt verificatie met een gebruikersnaam en wachtwoord, Facebook, Twitter en meer. We hebben een strategie ontwikkeld voor Azure Active Directory (Azure AD). U installeert deze module en voegt vervolgens hello Azure AD `passport-azure-ad` invoegtoepassing.

toodo dit voorbeeld moet u:

1. U registreert een toepassing met Azure AD.
2. Instellen van uw toepassing toouse Passport van `azure-ad-passport` invoegtoepassing.
3. Configureer een client toepassing toocall Hallo 'takenlijst'-web-API.

## <a name="get-an-azure-ad-b2c-directory"></a>Een Azure AD B2C-directory maken
Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.  Een directory is een container voor alle gebruikers, apps, groepen en meer.  Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u verdergaat.

## <a name="create-an-application"></a>Een app maken
Vervolgens moet u toocreate een app in uw B2C-directory die Azure AD bepaalde informatie geeft dat het toosecurely moet communiceren met uw app. In dit geval zowel Hallo client-app en web-API worden aangegeven met één **toepassings-ID**, omdat ze samen één logische app vormen. toocreate een app, volg [deze instructies](active-directory-b2c-app-registration.md). Zorg ervoor dat:

* Omvatten een **web-app of web api** in Hallo-toepassing
* U `http://localhost/TodoListService` invoert als **antwoord-URL**. Het is Hallo-standaard-URL voor dit codevoorbeeld.
* U een **toepassingsgeheim** maakt voor uw toepassing en dit kopieert. U hebt deze gegevens later nodig. Opmerking dat deze waarde toobe moet [XML escape-teken](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) voordat u deze kunt gebruiken.
* Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app. U hebt deze gegevens later nodig.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Het beleid maken
In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md). Deze app bevat twee identiteitservaringen: registreren en aanmelden. U moet één beleid toocreate van elk type, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).  Wanneer u uw drie beleidsregels maakt:

* Kies Hallo **weergavenaam** en andere registratiekenmerken in het registratiebeleid.
* Kies Hallo **weergavenaam** en **Object-ID** toepassingsclaims voor elk beleid.  U kunt ook andere claims kiezen.
* Noteer Hallo **naam** van elk beleid nadat u dit hebt gemaakt. Het voorvoegsel Hallo heeft `b2c_1_`.  U hebt deze beleidsnamen later nodig.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Wanneer u uw drie beleidsregels hebt gemaakt, bent u klaar toobuild uw app.

toolearn over de werking van beleid in Azure AD B2C, beginnen met Hallo [zelfstudie .NET web app aan de slag](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="download-hello-code"></a>Hallo code downloaden
code voor deze zelfstudie Hallo [wordt bewaard in GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS). toobuild hello voorbeeld als u gaat, kunt u [een basisproject downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip). U kunt Hallo basisproject ook klonen:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

Hallo voltooid app is ook [beschikbaar als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) of op Hallo `complete` vertakking van Hallo dezelfde opslagplaats.

## <a name="download-nodejs-for-your-platform"></a>Node.js voor uw platform downloaden
toosuccessfully dit voorbeeld gebruiken, moet u een werkende implementatie van Node.js.

Installeer Node.js vanuit [nodejs.org](http://nodejs.org).

## <a name="install-mongodb-for-your-platform"></a>MongoDB installeren voor uw platform
toosuccessfully dit voorbeeld gebruiken, moet u een werkende implementatie van MongoDB. We gebruiken uw REST-API persistent MongoDB toomake in alle serverexemplaren.

Installeer MongoDB vanuit [mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Deze procedure wordt ervan uitgegaan dat u Hallo standaard en -servereindpunten voor MongoDB, namelijk op moment van schrijven van dit Hallo `mongodb://localhost`.
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a>Hallo Restify-modules installeren in uw web-API
We gebruiken uw REST API Restify toobuild. Restify is een minimaal en flexibel Node.js-toepassingsframework dat is afgeleid van Express. Het bevat een set krachtige functies voor het ontwikkelen van REST-API's op Connect.

### <a name="install-restify"></a>Restify installeren
Vanaf de opdrachtregel hello, wijzig de directory te`azuread`. Als hello `azuread` directory niet bestaat, maakt deze.

`cd azuread` of `mkdir azuread;`

Voer Hallo volgende opdracht:

`npm install restify`

Met deze opdracht wordt Restify geïnstalleerd.

#### <a name="did-you-get-an-error"></a>Krijgt u een foutmelding?
In sommige besturingssystemen wanneer u `npm`, foutbericht Hallo `Error: EPERM, chmod '/usr/local/bin/..'` en een aanvraag die u Hallo account uitvoeren als beheerder. Als dit probleem optreedt, gebruikt u Hallo `sudo` opdracht toorun `npm` op een hoger niveau van bevoegdheden.

#### <a name="did-you-get-a-dtrace-error"></a>Wordt er een DTrace-fout weergegeven?
Mogelijk wordt er iets in de trant van het volgende weergegeven wanneer u Restify installeert:

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

Restify biedt een krachtig mechanisme om REST-aanroepen te traceren met behulp van DTrace. Veel besturingssystemen beschikken echter niet over DTrace. U kunt deze fouten negeren.

Hallo-uitvoer van Hallo-opdracht moet worden weergegeven soortgelijke toothis tekst:

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

## <a name="install-passport-in-your-web-api"></a>Passport installeren in uw web-API
Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd.

Met behulp van de volgende opdracht Hallo Passport installeren:

`npm install passport`

Hallo-uitvoer van de opdracht Hallo moet soortgelijke toothis tekst:

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a>Passport-azuread tooyour web API toevoegen
Voeg vervolgens Hallo OAuth-strategie toe met behulp van `passport-azuread`, een reeks strategieën die Azure AD met Passport verbinden. Gebruik deze strategie voor bearer-tokens in Hallo REST-API-voorbeeld.

> [!NOTE]
> Hoewel OAuth2 een kader biedt waarin elk onbekend type token kan worden uitgegeven, worden alleen bepaalde typen tokens wijdverbreid gebruikt. Hallo-tokens voor het beveiligen van eindpunten zijn bearer-tokens. Deze typen tokens zijn Hallo meest wordt uitgegeven in OAuth2. Veel implementaties wordt ervan uitgegaan dat bearer-tokens Hallo enige type token dat is uitgegeven zijn.
>
>

Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd.

Hallo Passport installeren `passport-azure-ad` module met behulp van de volgende opdracht Hallo:

`npm install passport-azure-ad`

Hallo-uitvoer van de opdracht Hallo moet soortgelijke toothis tekst:

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a>MongoDB-modules tooyour web API toevoegen
In dit voorbeeld wordt MongoDB gebruikt als gegevensarchief. Installeer daarvoor Mongoose, een veel gebruikte invoegtoepassing voor het beheren van modellen en schema’s.

* `npm install mongoose`

## <a name="install-additional-modules"></a>Aanvullende modules installeren
Vervolgens installeert Hallo resterende vereiste modules.

Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:

`cd azuread`

Hallo-modules in installeren uw `node_modules` directory:

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a>Een bestand server.js met de afhankelijkheden maken
Hallo `server.js` bestand Hallo meerderheid van Hallo functionaliteit biedt voor uw Web-API-server.

Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:

`cd azuread`

Maak een bestand `server.js` in een teksteditor. Voeg Hallo volgende informatie:

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

Hallo-bestand opslaan. U terug tooit later.

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a>Maken van een bestand config.js toostore uw Azure AD-instellingen
Dit codebestand geeft de configuratieparameters Hallo van uw Azure AD-Portal toohello `Passport.js` bestand. U hebt deze configuratiewaarden gemaakt toen u in het eerste deel van de procedure Hallo HALLO hallo-API toohello webportal hebt toegevoegd. We uitleggen welke tooput Hallo waarden van deze parameters wanneer u Hallo code hebt gekopieerd.

Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:

`cd azuread`

Maak een bestand `config.js` in een teksteditor. Voeg Hallo volgende informatie:

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a>Vereiste waarden
`clientID`: Hallo van client-ID van uw Web-API-toepassing.

`IdentityMetadata`: Dit is de locatie `passport-azure-ad` zoekt naar de configuratiegegevens voor Hallo id-provider. Het lijkt erop ook voor Hallo sleutels toovalidate Hallo JSON webtokens.

`audience`: Hallo uniform resource identifier (URI) van Hallo portal die de aanroepende toepassing te identificeren.

`tenantName`: de tenantnaam, bijvoorbeeld **contoso.onmicrosoft.com**.

`policyName`: Hallo toovalidate Hallo tokens binnenkort in tooyour server het gewenste beleid. Dit beleid moet Hallo hetzelfde beleid die u voor de clienttoepassing Hallo voor aanmelden gebruikt.

> [!NOTE]
> Op dit moment Hallo gebruik dezelfde beleidsregels voor zowel client als server setup. Als u al een procedure hebt voltooid en deze beleidsregels hebt gemaakt, u geen toodo dus opnieuw hoeft. Omdat u Hallo procedure hebt voltooid, moet u mag niet tooset nieuw beleid voor clientprocedures op Hallo-site.
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a>Configuratiebestand tooyour server.js toevoegen
tooread hello waarden uit Hallo `config.js` bestand dat u hebt gemaakt, het toevoegen van Hallo `.config` bestand als een vereiste bron in uw toepassing en stel vervolgens Hallo globale variabelen toothose in Hallo `config.js` document.

Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:

`cd azuread`

Open Hallo `server.js` bestand in een teksteditor. Voeg Hallo volgende informatie:

```Javascript
var config = require('./config');
```
Voeg een nieuwe sectie te`server.js` die Hallo volgende code bevat:

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

Vervolgens laten we de tijdelijke aanduidingen voor Hallo gebruikers we van onze aanroepen toepassingen ontvangen toevoegen.

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

U gaat ook een logger maken.

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Hallo MongoDB-model en schema-informatie toevoegen met behulp van Mongoose
Hallo handig eerdere voorbereiding wanneer u deze drie bestanden samenbrengt in een REST-API-service.

Voor deze procedure gebruikt u MongoDB toostore uw taken, zoals eerder besproken.

In Hallo `config.js` -bestand dat u uw database aangeroepen **tasklist**. Die naam is ook wat u achter Hallo Hallo opnemen `mongoose_auth_local` verbindings-URL. U hoeft niet toocreate deze vooraf in MongoDB-database. Het Hallo-database voor u gemaakt op de eerste uitvoering van de servertoepassing Hallo.

Nadat u welke MongoDB-database toouse Hallo-server zien, moet u toowrite enkele aanvullende code toocreate Hallo model en het schema voor de servertaken.

### <a name="expand-hello-model"></a>Hallo model uitbreiden
Dit schemamodel is eenvoudig. U kunt het naar behoefte uitbreiden.

`owner`: De persoon toohello taak is toegewezen. Dit object is een **tekenreeks**.  

`Text`: Hallo taak zelf. Dit object is een **tekenreeks**.

`date`: Hallo datum die taak Hallo vervalt. Dit object is een **datum/tijd**.

`completed`: Als het Hallo-taak is voltooid. Dit object is een **Booleaanse waarde**.

### <a name="create-hello-schema-in-hello-code"></a>Hallo-schema in Hallo code maken
Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:

`cd azuread`

Open Hallo `server.js` bestand in een teksteditor. Hallo volgende informatie hieronder Hallo configuratie-item toevoegen:

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
Hallo-schema voor het eerst wordt gemaakt en maakt u een modelobject dat u uw gegevens in de gehele Hallo code bij het definiëren van toostore uw **routes**.

## <a name="add-routes-for-your-rest-api-task-server"></a>Routes toevoegen voor de REST-API-taakserver
Nu u een database model toowork met hebt, toevoegen Hallo routes die u voor de REST-API-server gebruikt.

### <a name="about-routes-in-restify"></a>Routes in Restify
Routes werken in Restify op Hallo dezelfde manier als wanneer ze de Express-stack hello gebruiken. U definieert routes met behulp van Hallo URI dat u Hallo client toepassingen toocall verwacht.

Een doorsnee patroon voor een Restify-route is:

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

U kunt Restify en Express gebruiken voor een veel diepere functionaliteit, zoals voor het definiëren van toepassingstypen en de uitvoering van complexe routering tussen verschillende eindpunten. Voor Hallo doel van deze zelfstudie Houd we deze routes eenvoudig.

#### <a name="add-default-routes-tooyour-server"></a>Standaard routes tooyour server toevoegen
U nu Hallo eenvoudige CRUD-routes voor toevoegen **maken** en **lijst** voor onze REST-API. Andere deze routes kunnen worden gevonden in Hallo `complete` vertakking van Hallo-voorbeeld.

Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:

`cd azuread`

Open Hallo `server.js` bestand in een teksteditor. Onder de databasevermeldingen Hallo aangebrachte hoger toevoegen Hallo volgende informatie:

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err)
            return next(err);

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a>Foutafhandeling voor Hallo routes toevoegen
Sommige foutafhandeling toevoegen zodat u eventuele problemen die kunnen optreden back toohello-client op een manier die kunt kan communiceren.

Hallo na code toevoegen:

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a>De server maken
U hebt nu een database gedefinieerd en de routes geconfigureerd. Hallo laatste wat voor u toodo is tooadd Hallo server-exemplaar waarmee uw aanroepen worden beheerd.

Restify en Express kunt u mate aanpassen voor een REST-API-server, maar we de meest eenvoudige configuratie Hallo hier gebruiken.

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a>Hallo routes toohello server (zonder verificatie) toevoegen
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a>Authentication tooyour REST-API-server toevoegen
Nu u een actieve REST-API-server hebt, kunt u deze gaan gebruiken met Azure AD.

Vanaf de opdrachtregel hello, wijzig de directory te`azuread`, als deze nog niet is gebeurd:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Hallo OIDCBearerStrategy die is opgenomen in passport-azure-ad gebruiken
> [!TIP]
> Wanneer u API's schrijft, u moet altijd koppelen Hallo gegevens toosomething uniek in vergelijking met het Hallo-token dat Hallo gebruiker niet kunnen vervalsen. Wanneer Hallo server ToDo-items opslaat, gebeurt dit op basis van Hallo **oid** van Hallo-gebruiker in Hallo-token (aangeroepen via token.oid), die in het veld Hallo 'eigenaar' gaat. Met deze waarde zorgt u ervoor dat alleen die gebruiker toegang heeft tot zijn/haar eigen ToDo-items. Er is geen blootstelling in Hallo API van de 'eigenaar' zodat een externe gebruiker anderen ToDo-items aanvragen kan, zelfs als ze zijn geverifieerd.
>
>

Gebruik vervolgens Hallo bearer-strategie die wordt geleverd met `passport-azure-ad`.

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

Hallo hetzelfde patroon wordt gebruikt voor alle strategieën Passport. U geeft hieraan een `function()` door die `token` en `done` als parameters heeft. Hallo-strategie komt weer tooyou nadat deze zijn werk heeft gedaan. U moet vervolgens Hallo gebruiker opslaat en Hallo token opslaan zodat u niet tooask voor het opnieuw hoeft.

> [!IMPORTANT]
> Hallo bovenstaande code wordt elke gebruiker die zich tooauthenticate tooyour server. Dit proces wordt automatische registratie genoemd. In productieservers laat niet in alle gebruikers toegang Hallo API zonder dat zij een registratieproces doorlopen eerst. Dit proces is meestal Hallo patroon dat u in consumenten-apps die tooregister toestaan ziet via Facebook, maar vervolgens vraagt u toofill aanvullende informatie. Als dit programma is niet een opdrachtregelprogramma, kan hebben we Hallo e opgehaald uit Hallo Tokenobject dat wordt geretourneerd en vervolgens gebruikers toofill aanvullende informatie gevraagd. Omdat dit een voorbeeld is, we ze tooan in-memory database toevoegen.
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a>Dat het weigert uitvoeren van uw toepassing server tooverify u
U kunt `curl` toosee hebt u nu OAuth2-bescherming voor uw eindpunten. Hallo geretourneerde headers moeten voldoende tootell u dat u op het juiste pad Hallo.

Controleer of het MongoDB-exemplaar is geactiveerd:

    $sudo mongodb

Toohello directory en Voer Hallo-server wijzigen:

    $ cd azuread
    $ node server.js

Voer `curl` uit in een nieuw terminalvenster

Probeer een basic POST:

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

Een 401-fout is Hallo-reactie die u wilt. Hiermee wordt aangegeven dat Hallo Passport-laag probeert tooredirect toohello autoriseren eindpunt.

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a>U hebt nu een REST-API-service die gebruikmaakt van OAuth2
U hebt een REST-API geïmplementeerd met behulp van Restify en OAuth! U hebt nu voldoende code zodat u kunt doorgaan toodevelop uw service en op dit voorbeeld bouwen. U bent nu met deze server zo ver mogelijk gegaan zonder gebruik te maken van een OAuth2-compatibele client. Voor die stap gebruikt u een extra procedure zoals onze [tooa web-API verbinden met behulp van iOS met B2C](active-directory-b2c-devquickstarts-ios.md) scenario.

## <a name="next-steps"></a>Volgende stappen
U kunt nu toomore geavanceerde onderwerpen, zoals verplaatsen:

[Verbinding maken met tooa web-API met behulp van iOS met B2C](active-directory-b2c-devquickstarts-ios.md)
