---
title: Met behulp van Twilio voor spraak-, VoIP- en SMS-berichten in Azure
description: Informatie over het maken van een telefonische oproep en verzenden van een SMS-bericht met de Twilio-API-service op Azure. Codevoorbeelden geschreven in Node.js.
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
ms.openlocfilehash: 44ec97812130d41d75be98fc8e2d846b7cb5c913
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="e11f9-104">Met behulp van Twilio voor spraak-, VoIP- en SMS-berichten in Azure</span><span class="sxs-lookup"><span data-stu-id="e11f9-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="e11f9-105">Deze handleiding wordt uitgelegd hoe u apps bouwen die met Twilio en node.js in Azure communiceren.</span><span class="sxs-lookup"><span data-stu-id="e11f9-105">This guide demonstrates how to build apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="e11f9-106">Wat is Twilio?</span><span class="sxs-lookup"><span data-stu-id="e11f9-106">What is Twilio?</span></span>
<span data-ttu-id="e11f9-107">Twilio is een API-platform waarmee u gemakkelijk voor ontwikkelaars en telefoongesprekken binnenkrijgt, verzenden en ontvangen berichten, en insluiten VoIP-aanroepen in de browser en systeemeigen mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e11f9-107">Twilio is an API platform that makes it easy for developers to make and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="e11f9-108">Laten we kort gaat over hoe dit werkt vooraleer.</span><span class="sxs-lookup"><span data-stu-id="e11f9-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="e11f9-109">Aanroepen en SMS-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="e11f9-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="e11f9-110">Twilio kan ontwikkelaars [kopen programmeerbare telefoonnummers] [ purchase_phone] die zowel verzenden en ontvangen oproepen en berichten kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e11f9-110">Twilio allows developers to [purchase programmable phone numbers][purchase_phone] which can be used to both send and receive calls and text messages.</span></span> <span data-ttu-id="e11f9-111">Wanneer een getal Twilio een inkomend telefoongesprek of tekstbericht ontvangt, stuurt Twilio uw webtoepassing een HTTP POST of GET-aanvraag, waarin u wordt gevraagd voor instructies over het afhandelen van telefoongesprek of tekstbericht.</span><span class="sxs-lookup"><span data-stu-id="e11f9-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how to handle the call or text.</span></span> <span data-ttu-id="e11f9-112">De server reageert op HTTP-aanvraag met Twilio van [TwiML][twiml], een eenvoudige reeks XML-labels die bevatten instructies voor het verwerken van een telefoongesprek of tekstbericht.</span><span class="sxs-lookup"><span data-stu-id="e11f9-112">Your server will respond to Twilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how to handle a call or text.</span></span> <span data-ttu-id="e11f9-113">Voorbeelden van TwiML ziet er in even.</span><span class="sxs-lookup"><span data-stu-id="e11f9-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="e11f9-114">Het aanroepen en het verzenden van berichten</span><span class="sxs-lookup"><span data-stu-id="e11f9-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="e11f9-115">Doordat de HTTP-aanvragen naar de API van Twilio-webservice kunnen ontwikkelaars SMS-berichten verzenden of uitgaande telefoongesprekken starten.</span><span class="sxs-lookup"><span data-stu-id="e11f9-115">By making HTTP requests to the Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="e11f9-116">Voor uitgaande oproepen de ontwikkelaar moet ook een URL opgeven die als resultaat TwiML instructies voor het verwerken van de uitgaande aanroep gegeven zodra deze is verbonden.</span><span class="sxs-lookup"><span data-stu-id="e11f9-116">For outbound calls, the developer must also specify a URL that returns TwiML instructions for how to handle the outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="e11f9-117">VoIP-mogelijkheden insluiten in UI-code (JavaScript, iOS of Android)</span><span class="sxs-lookup"><span data-stu-id="e11f9-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="e11f9-118">Twilio biedt een client-side '-SDK die alle desktop-webbrowser, iOS-app of Android-app in een VoIP-telefoon omzetten kunt.</span><span class="sxs-lookup"><span data-stu-id="e11f9-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="e11f9-119">In dit artikel gaan we in op het gebruik van VoIP aanroepen in de browser.</span><span class="sxs-lookup"><span data-stu-id="e11f9-119">In this article, we will focus on how to use VoIP calling in the browser.</span></span> <span data-ttu-id="e11f9-120">Naast de *Twilio JavaScript SDK* wordt uitgevoerd in de browser, een servertoepassing (onze node.js-toepassing) worden gebruikt voor het uitgeven van een 'mogelijkheid token' aan de JavaScript-client.</span><span class="sxs-lookup"><span data-stu-id="e11f9-120">In addition to the *Twilio JavaScript SDK* running in the browser, a server-side application (our node.js application) must be used to issue a "capability token" to the JavaScript client.</span></span> <span data-ttu-id="e11f9-121">Meer informatie over het gebruik van VoIP met behulp van node.js [op de blog van de dev Twilio][voipnode].</span><span class="sxs-lookup"><span data-stu-id="e11f9-121">You can read more about using VoIP with node.js [on the Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="e11f9-122">Aanmelden voor Twilio (Microsoft korting)</span><span class="sxs-lookup"><span data-stu-id="e11f9-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="e11f9-123">Voordat u Twilio-services gebruikt, moet u eerst [aanmelden voor een account][signup].</span><span class="sxs-lookup"><span data-stu-id="e11f9-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="e11f9-124">Microsoft Azure-klanten krijgt u een speciale korting - [moet hier aanmelden][signup]!</span><span class="sxs-lookup"><span data-stu-id="e11f9-124">Microsoft Azure customers receive a special discount - [be sure to sign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="e11f9-125">Maken en implementeren van een Azure-Website voor node.js</span><span class="sxs-lookup"><span data-stu-id="e11f9-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="e11f9-126">Vervolgens moet u een node.js-website uitgevoerd op Azure te maken.</span><span class="sxs-lookup"><span data-stu-id="e11f9-126">Next, you will need to create a node.js website running on Azure.</span></span> <span data-ttu-id="e11f9-127">[De officiële documentatie om dit te doen zich hier bevindt][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="e11f9-127">[The official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="e11f9-128">Op een hoog niveau zal u worden als volgt:</span><span class="sxs-lookup"><span data-stu-id="e11f9-128">At a high level, you will be doing the following:</span></span>

* <span data-ttu-id="e11f9-129">Aanmelden voor een Azure-account als u nog niet hebt</span><span class="sxs-lookup"><span data-stu-id="e11f9-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="e11f9-130">Een nieuwe website maken via de Azure-beheerconsole</span><span class="sxs-lookup"><span data-stu-id="e11f9-130">Using the Azure admin console to create a new website</span></span>
* <span data-ttu-id="e11f9-131">Source control-ondersteuning (wordt ervan uitgegaan gebruikt van git) toe te voegen</span><span class="sxs-lookup"><span data-stu-id="e11f9-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="e11f9-132">Maken van een bestand `server.js` met een eenvoudige node.js-webtoepassing</span><span class="sxs-lookup"><span data-stu-id="e11f9-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="e11f9-133">Deze eenvoudige toepassing in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="e11f9-133">Deploying this simple application to Azure</span></span>

<a id="twiliomodule"/>

## <a name="configure-the-twilio-module"></a><span data-ttu-id="e11f9-134">De Module Twilio configureren</span><span class="sxs-lookup"><span data-stu-id="e11f9-134">Configure the Twilio Module</span></span>
<span data-ttu-id="e11f9-135">We begint vervolgens een eenvoudige node.js-toepassing die gebruik maakt van de API Twilio schrijven.</span><span class="sxs-lookup"><span data-stu-id="e11f9-135">Next, we will begin to write a simple node.js application which makes use of the Twilio API.</span></span> <span data-ttu-id="e11f9-136">Voordat we beginnen, moeten we onze Twilio-referenties voor account configureren.</span><span class="sxs-lookup"><span data-stu-id="e11f9-136">Before we begin, we need to configure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="e11f9-137">Twilio-referenties in systeemomgevingsvariabelen configureren</span><span class="sxs-lookup"><span data-stu-id="e11f9-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="e11f9-138">Om te kunnen maken van geverifieerde aanvragen op basis van de back-end van Twilio, moeten we onze account-SID en auth-token, die dienen als de gebruikersnaam en het wachtwoord voor onze Twilio-account ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e11f9-138">In order to make authenticated requests against the Twilio back end, we need our account SID and auth token, which function as the username and password set for our Twilio account.</span></span> <span data-ttu-id="e11f9-139">De veiligste manier om te configureren voor gebruik met de module knooppunt in Azure is via systeemomgevingsvariabelen, die u rechtstreeks in de Azure-beheerconsole kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="e11f9-139">The most secure way to configure these for use with the node module in Azure is via system environment variables, which you can set directly in the Azure admin console.</span></span>

<span data-ttu-id="e11f9-140">Selecteer uw node.js-website en klik op de koppeling 'Configureren'.</span><span class="sxs-lookup"><span data-stu-id="e11f9-140">Select your node.js website, and click the "CONFIGURE" link.</span></span>  <span data-ttu-id="e11f9-141">Als u Schuif naar beneden een bits, ziet u een gebied waarin u configuratie-eigenschappen voor uw toepassing instellen kunt.</span><span class="sxs-lookup"><span data-stu-id="e11f9-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="e11f9-142">Voer de referenties van uw Twilio-account ([gevonden op uw Twilio-Console][twilio_console]) zoals - Zorg ervoor dat deze de naam `TWILIO_ACCOUNT_SID` en `TWILIO_AUTH_TOKEN`respectievelijk:</span><span class="sxs-lookup"><span data-stu-id="e11f9-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure to name them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Azure-beheerconsole][azure-admin-console]

<span data-ttu-id="e11f9-144">Wanneer u deze variabelen hebt geconfigureerd, start u uw toepassing in de Azure-console.</span><span class="sxs-lookup"><span data-stu-id="e11f9-144">Once you have configured these variables, restart your application in the Azure console.</span></span>

### <a name="declaring-the-twilio-module-in-packagejson"></a><span data-ttu-id="e11f9-145">De module Twilio in package.json declareren</span><span class="sxs-lookup"><span data-stu-id="e11f9-145">Declaring the Twilio module in package.json</span></span>
<span data-ttu-id="e11f9-146">Vervolgens moet u een package.json voor het beheren van onze afhankelijkheden van de module knooppunt via [npm].</span><span class="sxs-lookup"><span data-stu-id="e11f9-146">Next, we need to create a package.json to manage our node module dependencies via [npm].</span></span> <span data-ttu-id="e11f9-147">Op hetzelfde niveau als het `server.js` bestand dat u hebt gemaakt in de *Azure/node.js* zelfstudie, maakt u een bestand met de naam `package.json`.</span><span class="sxs-lookup"><span data-stu-id="e11f9-147">At the same level as the `server.js` file you created in the *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="e11f9-148">In dit bestand, plaatst u het volgende:</span><span class="sxs-lookup"><span data-stu-id="e11f9-148">Inside this file, place the following:</span></span>

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

<span data-ttu-id="e11f9-149">Dit verklaart de twilio-module als een afhankelijkheid, evenals de populaire [Express-webframework] [ express] en de sjabloon EJS engine.</span><span class="sxs-lookup"><span data-stu-id="e11f9-149">This declares the twilio module as a dependency, as well as the popular [Express web framework][express] and the EJS template engine.</span></span>  <span data-ttu-id="e11f9-150">Goed, nu er klaar voor bent - gaan we de code schrijven!</span><span class="sxs-lookup"><span data-stu-id="e11f9-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="e11f9-151">Een uitgaande aanroep</span><span class="sxs-lookup"><span data-stu-id="e11f9-151">Make an Outbound Call</span></span>
<span data-ttu-id="e11f9-152">We maken een eenvoudig formulier dat een aanroep naar een getal kiest te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="e11f9-152">Let's create a simple form that will place a call to a number we choose.</span></span> <span data-ttu-id="e11f9-153">Open `server.js`, en voer de volgende code.</span><span class="sxs-lookup"><span data-stu-id="e11f9-153">Open up `server.js`, and enter the following code.</span></span> <span data-ttu-id="e11f9-154">Houd er rekening mee aanduiding 'CHANGE_ME' - er plaatst u de naam van uw azure-website:</span><span class="sxs-lookup"><span data-stu-id="e11f9-154">Note where it says "CHANGE_ME" - put the name of your azure website there:</span></span>

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

// Render an HTML user interface for the application's home page
app.get('/', (request, response) => response.render('index'));

// Handle the form POST to place a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call to this number
    to:request.body.number,

    // Change to a Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" to your app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});

// Generate TwiML to handle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message to the call's receiver
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

<span data-ttu-id="e11f9-155">Maak vervolgens een map met de naam `views` - binnen deze map staan, maakt u een bestand met de naam `index.ejs` met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="e11f9-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with the following contents:</span></span>

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
      <input type="submit" value="Call the number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="e11f9-156">Nu u uw website in Azure implementeert en open uw startpagina.</span><span class="sxs-lookup"><span data-stu-id="e11f9-156">Now, deploy your website to Azure and open your home.</span></span> <span data-ttu-id="e11f9-157">U moet mogelijk uw telefoonnummer invoeren in het tekstveld en ontvangen van een aanroep van het nummer van uw Twilio!</span><span class="sxs-lookup"><span data-stu-id="e11f9-157">You should be able to enter your phone number in the text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="e11f9-158">SMS-bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="e11f9-158">Send an SMS Message</span></span>
<span data-ttu-id="e11f9-159">Nu gaan we instellen van een gebruikersinterface en een formulier afhandeling van logica voor het verzenden van een SMS-bericht.</span><span class="sxs-lookup"><span data-stu-id="e11f9-159">Now, let's set up a user interface and form handling logic to send a text message.</span></span> <span data-ttu-id="e11f9-160">Open `server.js`, en voeg de volgende code toe na de laatste aanroep `app.post`:</span><span class="sxs-lookup"><span data-stu-id="e11f9-160">Open up `server.js`, and add the following code after the last call to `app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text to this number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // The body of the text message
      body: request.body.message

  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="e11f9-161">In `views/index.ejs`, toevoegen van een andere vorm onder de eerste is een getal en een SMS-bericht verzenden:</span><span class="sxs-lookup"><span data-stu-id="e11f9-161">In `views/index.ejs`, add another form under the first one to submit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message to send" name="message"/>
  <br/>
  <input type="submit" value="Send text to the number above"/>
</form>
```

<span data-ttu-id="e11f9-162">Uw toepassing in Azure opnieuw implementeren en u moet nu verzenden die vormen en zelf (of een van je vrienden dichtstbijzijnde) een SMS-bericht verzenden!</span><span class="sxs-lookup"><span data-stu-id="e11f9-162">Re-deploy your application to Azure, and you should now be able to submit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="e11f9-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e11f9-163">Next Steps</span></span>
<span data-ttu-id="e11f9-164">U hebt nu de basisprincipes van het bouwen van apps die communiceren met behulp van node.js en Twilio geleerd.</span><span class="sxs-lookup"><span data-stu-id="e11f9-164">You have now learned the basics of using node.js and Twilio to build apps that communicate.</span></span> <span data-ttu-id="e11f9-165">Maar deze voorbeelden scratchruimte nauwelijks het oppervlak van wat is er mogelijk met Twilio en node.js.</span><span class="sxs-lookup"><span data-stu-id="e11f9-165">But these examples barely scratch the surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="e11f9-166">Bekijk de volgende bronnen voor meer informatie Twilio gebruiken met node.js:</span><span class="sxs-lookup"><span data-stu-id="e11f9-166">For more information using Twilio with node.js, check out the following resources:</span></span>

* <span data-ttu-id="e11f9-167">[Officiële module docs][docs]</span><span class="sxs-lookup"><span data-stu-id="e11f9-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="e11f9-168">[Zelfstudie over VoIP met node.js-toepassingen][voipnode]</span><span class="sxs-lookup"><span data-stu-id="e11f9-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="e11f9-169">[Votr - een realtime SMS stemmen-toepassing met node.js en CouchDB (drie onderdelen)][votr]</span><span class="sxs-lookup"><span data-stu-id="e11f9-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="e11f9-170">[Paar programmering in de browser met behulp van node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="e11f9-170">[Pair programming in the browser with node.js][pair]</span></span>

<span data-ttu-id="e11f9-171">We hopen dat u graag node.js en Twilio hacken op Azure.</span><span class="sxs-lookup"><span data-stu-id="e11f9-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
<span data-ttu-id="e11f9-172">[npm]: http://npmjs.org</span><span class="sxs-lookup"><span data-stu-id="e11f9-172">[npm]: http://npmjs.org</span></span>
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
