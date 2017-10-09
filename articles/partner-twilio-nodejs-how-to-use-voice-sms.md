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
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="a5c39-104">Met behulp van Twilio voor spraak-, VoIP- en SMS-berichten in Azure</span><span class="sxs-lookup"><span data-stu-id="a5c39-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="a5c39-105">Deze handleiding wordt uitgelegd hoe toobuild apps die communiceren met Twilio en node.js in Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c39-105">This guide demonstrates how toobuild apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="a5c39-106">Wat is Twilio?</span><span class="sxs-lookup"><span data-stu-id="a5c39-106">What is Twilio?</span></span>
<span data-ttu-id="a5c39-107">Twilio is een API-platform die maakt het eenvoudig voor ontwikkelaars toomake telefoongesprekken binnenkrijgt, verzenden en ontvangen van tekstberichten en insluiten VoIP-aanroepen in de browser en systeemeigen mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a5c39-107">Twilio is an API platform that makes it easy for developers toomake and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="a5c39-108">Laten we kort gaat over hoe dit werkt vooraleer.</span><span class="sxs-lookup"><span data-stu-id="a5c39-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="a5c39-109">Aanroepen en SMS-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="a5c39-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="a5c39-110">Twilio kan ontwikkelaars te[kopen programmeerbare telefoonnummers] [ purchase_phone] die kunnen worden gebruikt tooboth verzenden en ontvangen oproepen en berichten.</span><span class="sxs-lookup"><span data-stu-id="a5c39-110">Twilio allows developers too[purchase programmable phone numbers][purchase_phone] which can be used tooboth send and receive calls and text messages.</span></span> <span data-ttu-id="a5c39-111">Wanneer een getal Twilio een inkomend telefoongesprek of tekstbericht ontvangt, stuurt Twilio uw webtoepassing een HTTP POST of GET-aanvraag, waarin u wordt gevraagd voor instructies over hoe toohandle Hallo telefoongesprek of tekstbericht.</span><span class="sxs-lookup"><span data-stu-id="a5c39-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how toohandle hello call or text.</span></span> <span data-ttu-id="a5c39-112">De server reageert tooTwilio van HTTP-aanvraag met [TwiML][twiml], een eenvoudige reeks XML-labels die instructies voor het bevatten toohandle een telefoongesprek of tekstbericht.</span><span class="sxs-lookup"><span data-stu-id="a5c39-112">Your server will respond tooTwilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how toohandle a call or text.</span></span> <span data-ttu-id="a5c39-113">Voorbeelden van TwiML ziet er in even.</span><span class="sxs-lookup"><span data-stu-id="a5c39-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="a5c39-114">Het aanroepen en het verzenden van berichten</span><span class="sxs-lookup"><span data-stu-id="a5c39-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="a5c39-115">Door het maken van HTTP-aanvragen toohello API Twilio-webservice kunnen ontwikkelaars SMS-berichten verzenden of uitgaande telefoongesprekken starten.</span><span class="sxs-lookup"><span data-stu-id="a5c39-115">By making HTTP requests toohello Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="a5c39-116">Voor uitgaande oproepen Hallo developer moet ook een URL opgeven die als resultaat TwiML instructies gegeven voor hoe toohandle Hallo uitgaande aanroepen nadat deze is verbonden.</span><span class="sxs-lookup"><span data-stu-id="a5c39-116">For outbound calls, hello developer must also specify a URL that returns TwiML instructions for how toohandle hello outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="a5c39-117">VoIP-mogelijkheden insluiten in UI-code (JavaScript, iOS of Android)</span><span class="sxs-lookup"><span data-stu-id="a5c39-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="a5c39-118">Twilio biedt een client-side '-SDK die alle desktop-webbrowser, iOS-app of Android-app in een VoIP-telefoon omzetten kunt.</span><span class="sxs-lookup"><span data-stu-id="a5c39-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="a5c39-119">In dit artikel gaan we in op het toouse VoIP aanroepen in de browser Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5c39-119">In this article, we will focus on how toouse VoIP calling in hello browser.</span></span> <span data-ttu-id="a5c39-120">In aanvulling toohello *Twilio JavaScript SDK* uitgevoerd in de browser hello, een servertoepassing (onze node.js-toepassing) moet gebruikte tooissue een 'mogelijkheid token' toohello JavaScript-client.</span><span class="sxs-lookup"><span data-stu-id="a5c39-120">In addition toohello *Twilio JavaScript SDK* running in hello browser, a server-side application (our node.js application) must be used tooissue a "capability token" toohello JavaScript client.</span></span> <span data-ttu-id="a5c39-121">Meer informatie over het gebruik van VoIP met behulp van node.js [op Hallo Twilio dev blog][voipnode].</span><span class="sxs-lookup"><span data-stu-id="a5c39-121">You can read more about using VoIP with node.js [on hello Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="a5c39-122">Aanmelden voor Twilio (Microsoft korting)</span><span class="sxs-lookup"><span data-stu-id="a5c39-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="a5c39-123">Voordat u Twilio-services gebruikt, moet u eerst [aanmelden voor een account][signup].</span><span class="sxs-lookup"><span data-stu-id="a5c39-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="a5c39-124">Microsoft Azure-klanten krijgt u een speciale korting - [ervoor toosign hier worden][signup]!</span><span class="sxs-lookup"><span data-stu-id="a5c39-124">Microsoft Azure customers receive a special discount - [be sure toosign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="a5c39-125">Maken en implementeren van een Azure-Website voor node.js</span><span class="sxs-lookup"><span data-stu-id="a5c39-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="a5c39-126">Vervolgens moet u toocreate een node.js website worden uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c39-126">Next, you will need toocreate a node.js website running on Azure.</span></span> <span data-ttu-id="a5c39-127">[Hallo officiële documentatie om dit te doen zich hier bevindt][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="a5c39-127">[hello official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="a5c39-128">Op hoog niveau, gaat u Hallo volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a5c39-128">At a high level, you will be doing hello following:</span></span>

* <span data-ttu-id="a5c39-129">Aanmelden voor een Azure-account als u nog niet hebt</span><span class="sxs-lookup"><span data-stu-id="a5c39-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="a5c39-130">Met behulp van hello Azure admin console toocreate een nieuwe website</span><span class="sxs-lookup"><span data-stu-id="a5c39-130">Using hello Azure admin console toocreate a new website</span></span>
* <span data-ttu-id="a5c39-131">Source control-ondersteuning (wordt ervan uitgegaan gebruikt van git) toe te voegen</span><span class="sxs-lookup"><span data-stu-id="a5c39-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="a5c39-132">Maken van een bestand `server.js` met een eenvoudige node.js-webtoepassing</span><span class="sxs-lookup"><span data-stu-id="a5c39-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="a5c39-133">Deze eenvoudige toepassing tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="a5c39-133">Deploying this simple application tooAzure</span></span>

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a><span data-ttu-id="a5c39-134">Hallo Twilio-Module configureren</span><span class="sxs-lookup"><span data-stu-id="a5c39-134">Configure hello Twilio Module</span></span>
<span data-ttu-id="a5c39-135">We begint vervolgens toowrite een eenvoudige node.js-toepassing, waardoor het gebruik van Hallo Twilio-API.</span><span class="sxs-lookup"><span data-stu-id="a5c39-135">Next, we will begin toowrite a simple node.js application which makes use of hello Twilio API.</span></span> <span data-ttu-id="a5c39-136">Voordat we beginnen, moeten we tooconfigure onze Twilio-accountreferenties.</span><span class="sxs-lookup"><span data-stu-id="a5c39-136">Before we begin, we need tooconfigure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="a5c39-137">Twilio-referenties in systeemomgevingsvariabelen configureren</span><span class="sxs-lookup"><span data-stu-id="a5c39-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="a5c39-138">In de volgorde toomake geverifieerde aanvragen op basis van Hallo Twilio-back-end moeten we onze account-SID en auth-token, die dienen als Hallo-gebruikersnaam en wachtwoord voor onze Twilio-account ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a5c39-138">In order toomake authenticated requests against hello Twilio back end, we need our account SID and auth token, which function as hello username and password set for our Twilio account.</span></span> <span data-ttu-id="a5c39-139">de veiligste manier tooconfigure Hallo voor gebruik met Hallo knooppunt module in Azure is via systeemomgevingsvariabelen, die u rechtstreeks in Azure Hallo-beheerconsole kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="a5c39-139">hello most secure way tooconfigure these for use with hello node module in Azure is via system environment variables, which you can set directly in hello Azure admin console.</span></span>

<span data-ttu-id="a5c39-140">Selecteer uw node.js-website en klik op de koppeling 'Configureren' Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5c39-140">Select your node.js website, and click hello "CONFIGURE" link.</span></span>  <span data-ttu-id="a5c39-141">Als u Schuif naar beneden een bits, ziet u een gebied waarin u configuratie-eigenschappen voor uw toepassing instellen kunt.</span><span class="sxs-lookup"><span data-stu-id="a5c39-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="a5c39-142">Voer de referenties van uw Twilio-account ([gevonden op uw Twilio-Console][twilio_console]) zoals - Zorg ervoor dat tooname ze `TWILIO_ACCOUNT_SID` en `TWILIO_AUTH_TOKEN`respectievelijk:</span><span class="sxs-lookup"><span data-stu-id="a5c39-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure tooname them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Azure-beheerconsole][azure-admin-console]

<span data-ttu-id="a5c39-144">Wanneer u deze variabelen hebt geconfigureerd, start u uw toepassing in hello Azure-console.</span><span class="sxs-lookup"><span data-stu-id="a5c39-144">Once you have configured these variables, restart your application in hello Azure console.</span></span>

### <a name="declaring-hello-twilio-module-in-packagejson"></a><span data-ttu-id="a5c39-145">Hallo Twilio-module in package.json declareren</span><span class="sxs-lookup"><span data-stu-id="a5c39-145">Declaring hello Twilio module in package.json</span></span>
<span data-ttu-id="a5c39-146">Vervolgens moet een package.json toomanage toocreate onze afhankelijkheden van de module knooppunt via [npm].</span><span class="sxs-lookup"><span data-stu-id="a5c39-146">Next, we need toocreate a package.json toomanage our node module dependencies via [npm].</span></span> <span data-ttu-id="a5c39-147">Op Hallo van hetzelfde niveau als Hallo `server.js` bestand dat u hebt gemaakt in Hallo *Azure/node.js* zelfstudie, maakt u een bestand met de naam `package.json`.</span><span class="sxs-lookup"><span data-stu-id="a5c39-147">At hello same level as hello `server.js` file you created in hello *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="a5c39-148">In dit bestand plaatsen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="a5c39-148">Inside this file, place hello following:</span></span>

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

<span data-ttu-id="a5c39-149">Dit verklaart Hallo twilio module als een afhankelijkheid, evenals de Hallo populaire [Express-webframework] [ express] en Hallo EJS sjabloon engine.</span><span class="sxs-lookup"><span data-stu-id="a5c39-149">This declares hello twilio module as a dependency, as well as hello popular [Express web framework][express] and hello EJS template engine.</span></span>  <span data-ttu-id="a5c39-150">Goed, nu er klaar voor bent - gaan we de code schrijven!</span><span class="sxs-lookup"><span data-stu-id="a5c39-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="a5c39-151">Een uitgaande aanroep</span><span class="sxs-lookup"><span data-stu-id="a5c39-151">Make an Outbound Call</span></span>
<span data-ttu-id="a5c39-152">We maken een eenvoudig formulier dat een aanroep tooa getal kiest te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="a5c39-152">Let's create a simple form that will place a call tooa number we choose.</span></span> <span data-ttu-id="a5c39-153">Open `server.js`, en voer de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5c39-153">Open up `server.js`, and enter hello following code.</span></span> <span data-ttu-id="a5c39-154">Houd er rekening mee aanduiding 'CHANGE_ME' - Hallo-naam van uw azure-website er plaatsen:</span><span class="sxs-lookup"><span data-stu-id="a5c39-154">Note where it says "CHANGE_ME" - put hello name of your azure website there:</span></span>

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

<span data-ttu-id="a5c39-155">Maak vervolgens een map met de naam `views` - binnen deze map staan, maakt u een bestand met de naam `index.ejs` Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="a5c39-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with hello following contents:</span></span>

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

<span data-ttu-id="a5c39-156">Nu uw website tooAzure implementeren en open uw startpagina.</span><span class="sxs-lookup"><span data-stu-id="a5c39-156">Now, deploy your website tooAzure and open your home.</span></span> <span data-ttu-id="a5c39-157">U moet kunnen tooenter worden uw telefoonnummer in veld van de tekst hello en ontvangen van een aanroep van het nummer van uw Twilio!</span><span class="sxs-lookup"><span data-stu-id="a5c39-157">You should be able tooenter your phone number in hello text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="a5c39-158">SMS-bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="a5c39-158">Send an SMS Message</span></span>
<span data-ttu-id="a5c39-159">Nu gaan we een gebruikersinterface en instellen formulier afhandeling van logica toosend een SMS-bericht.</span><span class="sxs-lookup"><span data-stu-id="a5c39-159">Now, let's set up a user interface and form handling logic toosend a text message.</span></span> <span data-ttu-id="a5c39-160">Open `server.js`, en voeg de code te volgen na de laatste aanroep Hallo Hallo`app.post`:</span><span class="sxs-lookup"><span data-stu-id="a5c39-160">Open up `server.js`, and add hello following code after hello last call too`app.post`:</span></span>

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

<span data-ttu-id="a5c39-161">In `views/index.ejs`, een ander formulier onder Hallo eerst een toosubmit een getal en een SMS-bericht toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a5c39-161">In `views/index.ejs`, add another form under hello first one toosubmit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

<span data-ttu-id="a5c39-162">Implementeer de tooAzure van uw toepassing opnieuw en nu moet u kunnen toosubmit waarmee wordt gevormd en zelf (of een van je vrienden dichtstbijzijnde) een SMS-bericht verzenden!</span><span class="sxs-lookup"><span data-stu-id="a5c39-162">Re-deploy your application tooAzure, and you should now be able toosubmit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="a5c39-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a5c39-163">Next Steps</span></span>
<span data-ttu-id="a5c39-164">U hebt nu basisbeginselen Hallo van het gebruik van node.js en Twilio toobuild apps die communiceren.</span><span class="sxs-lookup"><span data-stu-id="a5c39-164">You have now learned hello basics of using node.js and Twilio toobuild apps that communicate.</span></span> <span data-ttu-id="a5c39-165">Maar deze voorbeelden scratchruimte nauwelijks Hallo voor aanvallen van de mogelijkheden met Twilio en node.js.</span><span class="sxs-lookup"><span data-stu-id="a5c39-165">But these examples barely scratch hello surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="a5c39-166">Bekijk voor meer informatie Twilio gebruiken met node.js Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5c39-166">For more information using Twilio with node.js, check out hello following resources:</span></span>

* <span data-ttu-id="a5c39-167">[Officiële module docs][docs]</span><span class="sxs-lookup"><span data-stu-id="a5c39-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="a5c39-168">[Zelfstudie over VoIP met node.js-toepassingen][voipnode]</span><span class="sxs-lookup"><span data-stu-id="a5c39-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="a5c39-169">[Votr - een realtime SMS stemmen-toepassing met node.js en CouchDB (drie onderdelen)][votr]</span><span class="sxs-lookup"><span data-stu-id="a5c39-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="a5c39-170">[Paar programmering in de browser Hallo met behulp van node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="a5c39-170">[Pair programming in hello browser with node.js][pair]</span></span>

<span data-ttu-id="a5c39-171">We hopen dat u graag node.js en Twilio hacken op Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c39-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

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
