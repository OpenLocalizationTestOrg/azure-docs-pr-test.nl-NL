---
title: aaaUsing Twilio voor spraak-, VoIP- en SMS-berichten in Azure
description: Meer informatie over hoe toomake een telefonische oproep en verzend een SMS-met Hallo Twilio-API-service op Azure bericht. Codevoorbeelden geschreven in Node.js.
services: 
documentationcenter: nodejs
author: devinrader
manager: wpickett
editor: 
ms.assetid: f558cbbd-13d2-416f-b9b1-33a99c426af9
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/25/2014
ms.author: wpickett
ms.openlocfilehash: 6c44d60e217fcdf51e69fd2a8197f979afbb507a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a>Met behulp van Twilio voor spraak-, VoIP- en SMS-berichten in Azure
Deze handleiding wordt uitgelegd hoe toobuild apps die communiceren met Twilio en node.js in Azure.

<a id="whatis"/>

## <a name="what-is-twilio"></a>Wat is Twilio?
Twilio is een API-platform die maakt het eenvoudig voor ontwikkelaars toomake telefoongesprekken binnenkrijgt, verzenden en ontvangen van tekstberichten en insluiten VoIP-aanroepen in de browser en systeemeigen mobiele toepassingen. Laten we kort gaat over hoe dit werkt vooraleer.

### <a name="receiving-calls-and-text-messages"></a>Aanroepen en SMS-berichten ontvangen
Twilio kan ontwikkelaars te[kopen programmeerbare telefoonnummers] [ purchase_phone] die kunnen worden gebruikt tooboth verzenden en ontvangen oproepen en berichten. Wanneer een getal Twilio een inkomend telefoongesprek of tekstbericht ontvangt, stuurt Twilio uw webtoepassing een HTTP POST of GET-aanvraag, waarin u wordt gevraagd voor instructies over hoe toohandle Hallo telefoongesprek of tekstbericht. De server reageert tooTwilio van HTTP-aanvraag met [TwiML][twiml], een eenvoudige reeks XML-labels die instructies voor het bevatten toohandle een telefoongesprek of tekstbericht. Voorbeelden van TwiML ziet er in even.

### <a name="making-calls-and-sending-text-messages"></a>Het aanroepen en het verzenden van berichten
Door het maken van HTTP-aanvragen toohello API Twilio-webservice kunnen ontwikkelaars SMS-berichten verzenden of uitgaande telefoongesprekken starten. Voor uitgaande oproepen Hallo developer moet ook een URL opgeven die als resultaat TwiML instructies gegeven voor hoe toohandle Hallo uitgaande aanroepen nadat deze is verbonden.

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a>VoIP-mogelijkheden insluiten in UI-code (JavaScript, iOS of Android)
Twilio biedt een client-side '-SDK die alle desktop-webbrowser, iOS-app of Android-app in een VoIP-telefoon omzetten kunt. In dit artikel gaan we in op het toouse VoIP aanroepen in de browser Hallo. In aanvulling toohello *Twilio JavaScript SDK* uitgevoerd in de browser hello, een servertoepassing (onze node.js-toepassing) moet gebruikte tooissue een 'mogelijkheid token' toohello JavaScript-client. Meer informatie over het gebruik van VoIP met behulp van node.js [op Hallo Twilio dev blog][voipnode].

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a>Aanmelden voor Twilio (Microsoft korting)
Voordat u Twilio-services gebruikt, moet u eerst [aanmelden voor een account][signup]. Microsoft Azure-klanten krijgt u een speciale korting - [ervoor toosign hier worden][signup]!

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a>Maken en implementeren van een Azure-Website voor node.js
Vervolgens moet u toocreate een node.js website worden uitgevoerd op Azure. [Hallo officiële documentatie om dit te doen zich hier bevindt][azure_new_site]. Op hoog niveau, gaat u Hallo volgende doen:

* Aanmelden voor een Azure-account als u nog niet hebt
* Met behulp van hello Azure admin console toocreate een nieuwe website
* Source control-ondersteuning (wordt ervan uitgegaan gebruikt van git) toe te voegen
* Maken van een bestand `server.js` met een eenvoudige node.js-webtoepassing
* Deze eenvoudige toepassing tooAzure implementeren

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a>Hallo Twilio-Module configureren
We begint vervolgens toowrite een eenvoudige node.js-toepassing, waardoor het gebruik van Hallo Twilio-API. Voordat we beginnen, moeten we tooconfigure onze Twilio-accountreferenties.

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a>Twilio-referenties in systeemomgevingsvariabelen configureren
In de volgorde toomake geverifieerde aanvragen op basis van Hallo Twilio-back-end moeten we onze account-SID en auth-token, die dienen als Hallo-gebruikersnaam en wachtwoord voor onze Twilio-account ingesteld. de veiligste manier tooconfigure Hallo voor gebruik met Hallo knooppunt module in Azure is via systeemomgevingsvariabelen, die u rechtstreeks in Azure Hallo-beheerconsole kunt instellen.

Selecteer uw node.js-website en klik op de koppeling 'Configureren' Hallo.  Als u Schuif naar beneden een bits, ziet u een gebied waarin u configuratie-eigenschappen voor uw toepassing instellen kunt.  Voer de referenties van uw Twilio-account ([gevonden op uw Twilio-Console][twilio_console]) zoals - Zorg ervoor dat tooname ze `TWILIO_ACCOUNT_SID` en `TWILIO_AUTH_TOKEN`respectievelijk:

![Azure-beheerconsole][azure-admin-console]

Wanneer u deze variabelen hebt geconfigureerd, start u uw toepassing in hello Azure-console.

### <a name="declaring-hello-twilio-module-in-packagejson"></a>Hallo Twilio-module in package.json declareren
Vervolgens moet een package.json toomanage toocreate onze afhankelijkheden van de module knooppunt via [npm]. Op Hallo van hetzelfde niveau als Hallo `server.js` bestand dat u hebt gemaakt in Hallo *Azure/node.js* zelfstudie, maakt u een bestand met de naam `package.json`.  In dit bestand plaatsen Hallo volgende:

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node server"
  },
  "dependencies": {
    "body-parser": "^1.16.1",
    "ejs": "^2.5.5",
    "errorhandler": "^1.5.0",
    "express": "^4.14.1",
    "morgan": "^1.8.1",
    "twilio": "^2.11.1"
  }
}
```

Dit verklaart Hallo twilio module als een afhankelijkheid, evenals de Hallo populaire [Express-webframework] [ express] en Hallo EJS sjabloon engine.  Goed, nu er klaar voor bent - gaan we de code schrijven!

<a id="makecall"/>

## <a name="make-an-outbound-call"></a>Een uitgaande aanroep
We maken een eenvoudig formulier dat een aanroep tooa getal kiest te plaatsen. Open `server.js`, en voer de volgende code Hallo. Houd er rekening mee aanduiding 'CHANGE_ME' - Hallo-naam van uw azure-website er plaatsen:

```javascript
// Module dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const twilio = require('twilio');
const logger = require('morgan');
const bodyParser = require('body-parser');
const errorHandler = require('errorhandler');
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
// Create Express web application
const app = express();

// Express configuration
app.set('port', process.env.PORT || 3000);
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.use(logger('tiny'));
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(express.static(path.join(__dirname, 'public')));

if (app.get('env') !== 'production') {
  app.use(errorHandler());
}

// Render an HTML user interface for hello application's home page
app.get('/', (request, response) => response.render('index'));

// Handle hello form POST tooplace a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call toothis number
    to:request.body.number,

    // Change tooa Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" tooyour app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});

// Generate TwiML toohandle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message toohello call's receiver
  twiml.say('hello - thanks for checking out Twilio and Azure', {
      voice:'woman'
  });

  response.set('Content-Type', 'text/xml');
  response.send(twiml.toString());
});

// Start server
app.listen(app.get('port'), function(){
  console.log(`Express server listening on port ${app.get('port')}`);
});
```

Maak vervolgens een map met de naam `views` - binnen deze map staan, maakt u een bestand met de naam `index.ejs` Hello volgende inhoud:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Twilio Test</title>
  <style>
    input { height:20px; width:300px; font-size:18px; margin:5px; padding:5px; }
  </style>
</head>
<body>
  <h1>Twilio Test</h1>
  <form action="/call" method="POST">
      <input placeholder="Enter a phone number" name="number"/>
      <br/>
      <input type="submit" value="Call hello number above"/>
  </form>
</body>
</html>
```

Nu uw website tooAzure implementeren en open uw startpagina. U moet kunnen tooenter worden uw telefoonnummer in veld van de tekst hello en ontvangen van een aanroep van het nummer van uw Twilio!

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a>SMS-bericht verzenden
Nu gaan we een gebruikersinterface en instellen formulier afhandeling van logica toosend een SMS-bericht. Open `server.js`, en voeg de code te volgen na de laatste aanroep Hallo Hallo`app.post`:

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text toothis number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // hello body of hello text message
      body: request.body.message

  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});
```

In `views/index.ejs`, een ander formulier onder Hallo eerst een toosubmit een getal en een SMS-bericht toevoegen:

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

Implementeer de tooAzure van uw toepassing opnieuw en nu moet u kunnen toosubmit waarmee wordt gevormd en zelf (of een van je vrienden dichtstbijzijnde) een SMS-bericht verzenden!

<a id="nextsteps"/>

## <a name="next-steps"></a>Volgende stappen
U hebt nu basisbeginselen Hallo van het gebruik van node.js en Twilio toobuild apps die communiceren. Maar deze voorbeelden scratchruimte nauwelijks Hallo voor aanvallen van de mogelijkheden met Twilio en node.js. Bekijk voor meer informatie Twilio gebruiken met node.js Hallo resources te volgen:

* [Officiële module docs][docs]
* [Zelfstudie over VoIP met node.js-toepassingen][voipnode]
* [Votr - een realtime SMS stemmen-toepassing met node.js en CouchDB (drie onderdelen)][votr]
* [Paar programmering in de browser Hallo met behulp van node.js][pair]

We hopen dat u graag node.js en Twilio hacken op Azure.

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
[npm]: http://npmjs.org
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
