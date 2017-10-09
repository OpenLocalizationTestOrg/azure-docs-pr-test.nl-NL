---
title: aaaHow tooUse Twilio voor spraak- en SMS (Python) | Microsoft Docs
description: Meer informatie over hoe toomake een telefonische oproep en verzend een SMS-met Hallo Twilio-API-service op Azure bericht. Codevoorbeelden geschreven in Python.
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a>Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden in Python
Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello Twilio-API-service op Azure. Hallo scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden. Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen Hallo [Vervolgstappen](#NextSteps) sectie.

## <a id="WhatIs"></a>Wat is Twilio?
Twilio is dat toekomstige Hallo zakelijke communicatie, ontwikkelaars tooembed spraak, VoIP, inschakelen en messaging in toepassingen. Ze virtualiseren alle infrastructuur die nodig is in een cloud-gebaseerde, globale-omgeving, beschikbaar te maken via Hallo Twilio communications API-platform. Toepassingen zijn eenvoudige toobuild en schaalbare. Profiteer van flexibiliteit met pay-as-you gaat prijzen en profiteren van de betrouwbaarheid van de cloud.

**Twilio stem** kunt u uw toepassingen toomake en gebeld.
**Twilio SMS** kunt u uw toepassing toosend tekstberichten en ontvangen.
**Twilio Client** kunt u toomake VoIP-aanroepen vanuit een telefoon, tablet of een browser en WebRTC ondersteunt.

## <a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen
Azure-klanten ontvangen een [speciale aanbieding] [ special_offer] $10 Twilio tegoed wanneer u een upgrade uitvoert van uw Twilio-Account. Deze Twilio-tegoed kan worden toegepast tooany Twilio-gebruik ($10 tegoed gelijkwaardige toosending maximaal 1000 SMS-berichten of ontvangst van too1000 inkomende stem minuten, afhankelijk van de locatie van uw telefoon en bericht- of aanroep bestemming Hallo). Dit inwisselen [Twilio tegoed] [ special_offer] en aan de slag.

Twilio is een betalen naar gebruik service. Er zijn geen kosten instellen en kunt u uw account op elk moment sluiten. U vindt meer informatie op [Twilio prijzen][twilio_pricing].

## <a id="Concepts"></a>Concepten
Hallo Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen. Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].

Belangrijke aspecten van Hallo Twilio-API zijn Twilio-termen en Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Twilio-termen
Hallo API wordt gebruikgemaakt van Twilio termen; bijvoorbeeld, Hallo  **&lt;zeg&gt;**  term Hiermee Twilio tooaudibly afleveren geeft een bericht op een aanroep.

Hallo Hieronder volgt een lijst met Twilio-bewerkingen. Meer informatie over Hallo andere termen en mogelijkheden via [Twilio Markup Language documentatie][twiml].

* **&lt;Externe&gt;**: Hallo aanroeper tooanother telefoon verbindt.
* **&lt;Verzamel&gt;**: cijfers ingevoerd op het telefoonnummer Hallo verzamelt.
* **&lt;Ophangen&gt;**: een aanroep wordt beëindigd.
* **&lt;Onderbreken&gt;**: achtergrond wacht op een opgegeven aantal seconden.
* **&lt;Afspelen&gt;**: een geluidsbestand afgespeeld.
* **&lt;Wachtrij&gt;**: Hallo tooa wachtrij van aanroepfuncties toevoegen.
* **&lt;Record&gt;**: registreert Hallo stem van de aanroepfunctie Hallo en retourneert een URL van een bestand dat Hallo opname bevat.
* **&lt;Omleiden&gt;**: draagt de controle van een telefoongesprek of SMS toohello TwiML op een andere URL.
* **&lt;Afwijzen&gt;**: geweigerd een binnenkomende tooyour Twilio nummer bellen zonder u facturering.
* **&lt;Zeg&gt;**: zet tekst toospeech die wordt gemaakt op een aanroep.
* **&lt;SMS&gt;**: een SMS-bericht verzonden.

### <a id="TwiML"></a>TwiML
TwiML is een reeks XML gebaseerde instructies op basis van Hallo Twilio-termen die Twilio van hoe u informeren over tooprocess een telefoongesprek of SMS.

Als u bijvoorbeeld Hallo TwiML na Hallo tekst wilt converteren **Hallo wereld** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Bij het aanroepen van uw toepassing hello Twilio-API, is een van de API-parameters Hallo Hallo-URL die Hallo TwiML antwoord geretourneerd. U kunt voor ontwikkelingsdoeleinden Twilio geleverde URL's tooprovide hello TwiML antwoorden die wordt gebruikt door uw toepassingen. U ook uw eigen URL's tooproduce hello TwiML reacties kan hosten en een andere optie is toouse hello `TwiMLResponse` object.

Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml]. Zie voor meer informatie over Hallo Twilio-API, [Twilio-API][twilio_api].

## <a id="CreateAccount"></a>Een Twilio-Account maken
Wanneer u klaar tooget een Twilio-account bent, aanmelden op [probeer Twilio][try_twilio]. U kunt beginnen met een gratis account en upgrade van uw account later.

Wanneer u zich voor een Twilio-account aanmeldt, ontvangt u een account-SID en geen verificatietoken. Beide worden benodigde toomake Twilio-API-aanroepen. tooprevent onbevoegde toegang tot tooyour account, het verificatietoken te beveiligen. Uw account-SID en de verificatietoken worden weergegeven in Hallo [Twilio Console][twilio_console]in velden met het label Hallo **ACCOUNT-SID** en **AUTH TOKEN**respectievelijk.

## <a id="create_app"></a>Een Python-toepassing maken
Een Python-toepassing die gebruikmaakt van Hallo Twilio-service en wordt uitgevoerd in Azure gaat niet anders dan de andere Python-toepassing die gebruikmaakt van Hallo Twilio-service. Terwijl Twilio-services op basis van REST worden en op verschillende manieren kunnen worden aangeroepen vanuit Python, in dit artikel wordt de nadruk gelegd op hoe toouse Twilio services met [Twilio-bibliotheek voor Python vanuit GitHub][twilio_python]. Zie voor meer informatie over het gebruik van Hallo Twilio-bibliotheek voor Python [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].

Eerste, [installatie een nieuwe Azure Linux VM] [azure_vm_setup] tooact als host voor de nieuwe Python-webtoepassing. Zodra hello virtuele Machine wordt uitgevoerd, moet u tooexpose uw toepassing op een openbare poort zoals hieronder wordt beschreven.

### <a name="add-an-incoming-rule"></a>Een inkomende regel toevoegen
  1. Ga toohello [Netwerkbeveiligingsgroep] [azure_nsg] pagina.
  2. Selecteer Hallo Netwerkbeveiligingsgroep dat correspondeert met de virtuele Machine.
  3. Toevoegen en **uitgaande regel** voor **poort 80**. Ervoor tooallow binnenkomende van elk adres zijn.

### <a name="set-hello-dns-name-label"></a>Hallo Label DNS-naam instellen
  1. Ga toohello [Hallo openbare IP-mailadressen] [azure_ips] pagina.
  2. Selecteer Hallo openbare IP-adres dat correspends met uw virtuele Machine.
  3. Set Hallo **Label DNS-naam** in Hallo **configuratie** sectie. In geval van Hallo van dit voorbeeld is het wordt als volgt uitzien *your domain-label*. centralus.cloudapp.azure.com

Zodra u zich kunt tooconnect via SSH toohello virtuele Machine die u kunt installeren Webframework van uw keuze Hallo (Hallo twee meest bekende in Python wordt [Flask](http://flask.pocoo.org/) en [Django](https://www.djangoproject.com)). U kunt een van beide installeren alleen door Hallo `pip install` opdracht.

Houd er rekening mee dat we Hallo virtueel machineverkeer tooallow alleen geconfigureerd op poort 80. Dus zorg ervoor dat tooconfigure Hallo toepassing toouse deze poort.

## <a id="configure_app"></a>Configureren van uw toepassing tooUse Twilio-bibliotheken
U kunt uw toepassing toouse hello Twilio-bibliotheek voor Python configureren op twee manieren:

* Hallo Twilio-bibliotheek voor Python installeren als een Pip-pakket. Het kan worden geïnstalleerd met Hallo volgende opdrachten:
   
        $ pip install twilio

    OF

* Hallo Twilio-bibliotheek voor Python vanuit GitHub downloaden ([https://github.com/twilio/twilio-python][twilio_python]) en installeer deze als volgt:

        $ python setup.py install

Wanneer u Hallo Twilio-bibliotheek voor Python hebt geïnstalleerd, kunt u vervolgens `import` in uw Python-bestanden:

        import twilio

Zie voor meer informatie [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Procedure: een uitgaande aanroep
Hallo volgende ziet u hoe een uitgaande toomake aanroepen. Deze code wordt een Twilio-voorwaarde site tooreturn hello Twilio Markup Language (TwiML) antwoord. Vervang uw waarden voor Hallo **from_number** en **to_number** telefoonnummers, en zorg ervoor dat u hebt geverifieerd dat Hallo **from_number** telefoonnummer voor uw Twilio-account voordat u de code van de Hallo is uitgevoerd.

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

Zoals gezegd, gebruikt deze code een Twilio-voorwaarde site tooreturn hello TwiML antwoord. U kunt in plaats hiervan uw eigen site tooprovide hello TwiML antwoord; Zie voor meer informatie [hoe tooProvide TwiML antwoorden vanaf uw eigen website](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Procedure: een SMS-bericht verzenden
Hallo hieronder ziet u hoe een SMS-bericht met toosend Hallo `TwilioRestClient` klasse. Hallo **from_number** nummer wordt geleverd door Twilio voor proefversie accounts toosend SMS-berichten. Hallo **to_number** nummer voor uw Twilio-account moet worden gecontroleerd voordat Hallo code wordt uitgevoerd.

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <a id="howto_provide_twiml_responses"></a>Hoe: TwiML reacties van uw eigen Website opgeven
Wanneer uw toepassing een aanroep van toohello Twilio-API initieert, stuurt Twilio uw aanvraag tooa-URL die wordt verwacht tooreturn TwiML antwoord. Hallo in bovenstaand voorbeeld gebruikt Hallo Twilio-geleverde URL [http://twimlets.com/message][twimlet_message_url]. (Hoewel TwiML is ontworpen voor gebruik door Twilio, kunt u deze bekijken in uw browser. Bijvoorbeeld, klik op [http://twimlets.com/message] [ twimlet_message_url] toosee een lege `<Response>` element; Klik bijvoorbeeld op [http://twimlets.com/message? Bericht % 5B0 %5, D = Hallo % 20World] [ twimlet_message_url_hello_world] toosee een `<Response>` element met een `<Say>` element.)

In plaats van te vertrouwen op Hallo geleverde Twilio-URL, kunt u uw eigen website waarmee HTTP-antwoorden worden geretourneerd. U kunt Hallo-site maken in een andere taal die als resultaat geeft de XML-reacties; in dit onderwerp wordt ervan uitgegaan dat u Python toocreate hello TwiML gaat gebruiken.

Hallo volgende voorbeelden wordt de uitvoer een TwiML-antwoord dat **Hallo wereld** op Hallo-aanroep.

Met Flask:

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

Met Django:

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

Zoals u in de bovenstaande Hallo voorbeeld zien kunt, is het Hallo TwiML antwoord gewoon een XML-document. Hallo Twilio-bibliotheek voor Python bevat klassen die voor u TwiML genereren. Hallo onderstaand voorbeeld gelijkwaardige antwoord Hallo produceert, zoals hierboven beschreven, maar gebruikt Hallo `twiml` module in Hallo Twilio-bibliotheek voor Python:

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

Zie voor meer informatie over TwiML [https://www.twilio.com/docs/api/twiml][twiml_reference].

Zodra u uw Python-toepassing instellen tooprovide TwiML antwoorden hebt, Hallo-URL van de toepassing hello gebruiken als de URL die wordt doorgegeven in Hallo Hallo `client.calls.create` methode. Bijvoorbeeld, als u een webtoepassing met de naam hebt **MyTwiML** geïmplementeerde tooan Azure gehoste service, kunt u de url als webhook gebruiken zoals wordt weergegeven in Hallo voorbeeld te volgen:

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <a id="AdditionalServices"></a>How to: extra Twilio-Services gebruiken
Bovendien kunt toohello voorbeelden die hier worden weergegeven, dat twilio biedt op basis van een web-API's u tooleverage aanvullende Twilio-functionaliteit van uw Azure-toepassing. Zie voor meer details Hallo [Twilio-API-documentatie][twilio_api].

## <a id="NextSteps"></a>Volgende stappen
Nu u basisprincipes Hallo Hallo Twilio-service hebt geleerd, volgt u deze koppelingen toolearn meer:

* [Richtlijnen voor Twilio-beveiliging][twilio_security_guidelines]
* [Twilio-procedure hulplijnen en voorbeeldcode][twilio_howtos]
* [Twilio Quick Start-zelfstudie][twilio_quickstarts]
* [Twilio op GitHub][twilio_on_github]
* [Neem contact tooTwilio ondersteuning][twilio_support]

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
