---
title: aaaHow tooUse Twilio voor spraak- en SMS (Ruby) | Microsoft Docs
description: Meer informatie over hoe toomake een telefonische oproep en verzend een SMS-met Hallo Twilio-API-service op Azure bericht. Codevoorbeelden geschreven in Ruby.
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a>Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden in Ruby
Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello Twilio-API-service op Azure. Hallo scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden. Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen Hallo [Vervolgstappen](#NextSteps) sectie.

## <a id="WhatIs"></a>Wat is Twilio?
Twilio is een telephony-webservice-API waarmee u uw bestaande web talen en de vaardigheden toobuild stem en de SMS-toepassingen gebruiken. Twilio is een service van derden (niet een functie van Azure en niet in een Microsoft-product).

**Twilio stem** kunt u uw toepassingen toomake en gebeld. **Twilio SMS** kunt u uw toepassingen toomake en SMS-berichten ontvangen. **Twilio Client** zorgt ervoor dat uw toepassingen tooenable gesproken communicatie met bestaande Internet-verbindingen, inclusief mobiele verbindingen.

## <a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen
Informatie over prijzen voor Twilio is beschikbaar op [Twilio prijzen][twilio_pricing]. Azure-klanten ontvangen een [speciale aanbieding][special_offer]: een gratis tegoed van 1000 teksten of 1000 inkomende minuten. toosign voor dit bieden of meer informatie, gaat u naar [http://ahoy.twilio.com/azure][special_offer].  

## <a id="Concepts"></a>Concepten
Hallo Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen. Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].

### <a id="TwiML"></a>TwiML
TwiML is een reeks XML-instructies die Twilio van hoe u informeren tooprocess een telefoongesprek of SMS.

Als u bijvoorbeeld Hallo TwiML na Hallo tekst wilt converteren **Hallo wereld** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Alle TwiML documenten hebben `<Response>` als hun hoofdelement. Van daaruit u Twilio-termen toodefine Hallo gedrag van uw toepassing.

### <a id="Verbs"></a>TwiML termen
Twilio-bewerkingen zijn XML-labels die Twilio wat te vertellen**doen**. Bijvoorbeeld, Hallo  **&lt;zeg&gt;**  term Hiermee Twilio tooaudibly afleveren geeft een bericht op een aanroep. 

Hallo Hieronder volgt een lijst met Twilio-bewerkingen.

* **&lt;Externe&gt;**: Hallo aanroeper tooanother telefoon verbindt.
* **&lt;Verzamel&gt;**: cijfers ingevoerd op het telefoonnummer Hallo verzamelt.
* **&lt;Ophangen&gt;**: een aanroep wordt beëindigd.
* **&lt;Afspelen&gt;**: een geluidsbestand afgespeeld.
* **&lt;Onderbreken&gt;**: achtergrond wacht op een opgegeven aantal seconden.
* **&lt;Record&gt;**: Hallo aanroeper stem registreert en retourneert een URL van een bestand dat Hallo opname bevat.
* **&lt;Omleiden&gt;**: draagt de controle van een telefoongesprek of SMS toohello TwiML op een andere URL.
* **&lt;Afwijzen&gt;**: geweigerd een binnenkomende tooyour Twilio nummer bellen zonder u facturering
* **&lt;Zeg&gt;**: zet tekst toospeech die wordt gemaakt op een aanroep.
* **&lt;SMS&gt;**: een SMS-bericht verzonden.

Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml]. Zie voor meer informatie over Hallo Twilio-API, [Twilio-API][twilio_api].

## <a id="CreateAccount"></a>Een Twilio-Account maken
Wanneer u klaar tooget een Twilio-account bent, aanmelden op [probeer Twilio][try_twilio]. U kunt beginnen met een gratis account en upgrade van uw account later.

Wanneer u zich voor een Twilio-account aanmeldt, krijgt u een gratis telefoonnummer voor uw toepassing. U ontvangt ook een SID-account en een auth-token. Beide worden benodigde toomake Twilio-API-aanroepen. tooprevent onbevoegde toegang tot tooyour account, het verificatietoken te beveiligen. Uw account-SID en auth token kunnen worden bekeken op Hallo [Twilio-accountpagina][twilio_account]in velden met het label Hallo **ACCOUNT-SID** en **AUTH TOKEN** , respectievelijk.

### <a id="VerifyPhoneNumbers"></a>Controleer of de telefoonnummers
Toevoeging toohello aantal u door Twilio krijgt, kunt u ook cijfers (dat wil zeggen uw mobiele telefoon of home telefoonnummer) te beheren voor gebruik in uw toepassingen controleren. 

Voor meer informatie over een telefoonnummer tooverify Zie [beheren cijfers][verify_phone].

## <a id="create_app"></a>Een Ruby-toepassing maken
Een Ruby-toepassing die gebruikmaakt van Hallo Twilio-service en wordt uitgevoerd in Azure gaat niet anders dan andere Ruby toepassing die gebruikmaakt van Hallo Twilio-service. Terwijl Twilio-services RESTful worden en op verschillende manieren kunnen worden aangeroepen vanuit Ruby, in dit artikel wordt de nadruk gelegd op hoe toouse Twilio services met [Twilio hulpbibliotheek voor Ruby][twilio_ruby].

Eerst [installatie een nieuwe Azure Linux VM] [ azure_vm_setup] tooact als host voor de nieuwe Ruby-webtoepassing. Hallo stappen met betrekking tot Hallo maken van een app Rails, net set-up Hallo VM overslaan. Zorg ervoor dat u maakt een eindpunt met een externe poort 80 en een interne 5000-poort.

In onderstaande Hallo voorbeelden, we gebruiken [Sinatra][sinatra], een zeer eenvoudige web-framework voor Ruby. Maar u kunt gewoon Hallo Twilio-hulpbibliotheek voor Ruby gebruiken met een andere webframework, met inbegrip van Ruby op Rails.

SSH in uw nieuwe virtuele machine en maak een map voor uw nieuwe app. Maak een bestand met de naam Gemfile en kopieer Hallo code in het volgende in die map:

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

Op Hallo opdrachtregel uitvoeren `bundle install`. Hiermee installeert u bovenstaande Hallo-afhankelijkheden. Maak vervolgens een bestand met de naam `web.rb`. Dit is waar Hallo-code voor uw web-app woont. Plak Hallo code in het volgende:

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

Op dit moment moet u kunnen Hallo uitvoeren Hallo opdracht `ruby web.rb -p 5000`. Dit wordt spin-up een kleine webserver op poort 5000. U moet kunnen toobrowse toothis app in uw browser via Hallo URL instellen voor uw Azure VM. Nadat u uw web-app in de browser Hallo bereiken kunt, bent u klaar toostart bouwen van een Twilio-app.

## <a id="configure_app"></a>Uw toepassing tooUse Twilio configureren
U kunt uw web-app toouse hello Twilio-bibliotheek configureren met het bijwerken van uw `Gemfile` tooinclude deze regel:

    gem 'twilio-ruby'

Voer op de opdrachtregel hello, `bundle install`. Open nu `web.rb` en deze regel boven hello, inclusief:

    require 'twilio-ruby'

U bent nu klaar voor toouse hello Twilio-hulpbibliotheek voor Ruby in uw web-app.

## <a id="howto_make_call"></a>Procedure: een uitgaande aanroep
Hallo volgende ziet u hoe een uitgaande toomake aanroepen. Belangrijkste concepten bevatten voor Ruby toomake die rest-API aanroept met behulp van Hallo Twilio-hulpbibliotheek en TwiML rendering. Vervang uw waarden voor Hallo **van** en **naar** telefoonnummers, en zorg ervoor dat u controleert of Hallo **van** telefoonnummer voor uw Twilio-account voorafgaande toorunning Hallo code.

Deze functie te toevoegen`web.md`:

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

Als de open-up `http://yourdomain.cloudapp.net/make_call` in een browser die Hallo aanroep toohello Twilio-API toomake Hallo telefonische oproep wordt geactiveerd. Hallo eerst twee parameters in `client.account.calls.create` redelijk spreken voor zich: Hallo nummer Hallo-aanroep is `from` en Hallo nummer Hallo-aanroep is `to`. 

Hallo derde parameter (`url`) Hallo URL dat Twilio tooget instructies over welke toodo aanvragen zodra het Hallo-aanroep is verbonden. In dit geval wordt de installatie een URL (`http://yourdomain.cloudapp.net`) die een eenvoudig TwiML document retourneert en maakt gebruik van Hallo `<Say>` term toodo sommige spraak en spreek 'Hello Monkey' toohello ontvanger Hallo aanroepen.

## <a id="howto_recieve_sms"></a>Procedure: een SMS-bericht ontvangen
In het vorige voorbeeld Hallo geïnitieerd we een **uitgaande** telefoongesprek. Deze tijd, Hallo telefoonnummer op dat Twilio doorgegeven tijdens registratie tooprocess hebt we gebruiken een **binnenkomende** SMS-bericht.

Eerste, aanmelden tooyour [Twilio-dashboard][twilio_account]. Klik op 'Cijfers' in de bovenste nav Hallo en klik vervolgens op Hallo Twilio-nummer die u zijn opgegeven. Hier ziet u twee URL's die u kunt configureren. Een stem aanvraag-URL en een SMS-bericht aanvraag-URL. Dit zijn Hallo-URL's die is gemaakt met Twilio-aanroepen wanneer een telefonische oproep of een SMS-bericht tooyour nummer wordt verzonden. Hallo-URL's worden ook wel bekend als 'web hooks'.

Willen we graag tooprocess binnenkomende SMS-berichten, dus we Hallo URL bijwerken`http://yourdomain.cloudapp.net/sms_url`. Opwekken en klikt u op wijzigingen opslaan onder Hallo van Hallo pagina. Nu weer `web.rb` onze toepassing toohandle we programma dit:

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

Hallo nadat wijziging hebt aangebracht, moet u ervoor dat toore-begin uw web-app. Nu uw telefoon Elimineer en verzenden van een SMS-tooyour Twilio-nummer. U krijgt onmiddellijk een SMS-antwoord met de tekst "artikel van Hey, Hartelijk dank voor het Hallo-ping! Twilio en Azure steen! '.

## <a id="additional_services"></a>How to: extra Twilio-Services gebruiken
Bovendien kunt toohello voorbeelden die hier worden weergegeven, dat twilio biedt op basis van een web-API's u tooleverage aanvullende Twilio-functionaliteit van uw Azure-toepassing. Zie voor meer details Hallo [Twilio-API-documentatie][twilio_api_documentation].

### <a id="NextSteps"></a>Volgende stappen
Nu u basisprincipes Hallo Hallo Twilio-service hebt geleerd, volgt u deze koppelingen toolearn meer:

* [Richtlijnen voor Twilio-beveiliging][twilio_security_guidelines]
* [Twilio HowTos en voorbeeldcode][twilio_howtos]
* [Twilio Quick Start-zelfstudie][twilio_quickstarts] 
* [Twilio op GitHub][twilio_on_github]
* [Neem contact tooTwilio ondersteuning][twilio_support]

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
