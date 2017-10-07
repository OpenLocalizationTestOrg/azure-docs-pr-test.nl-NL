---
title: aaaHow tooUse Twilio voor spraak- en SMS (PHP) | Microsoft Docs
description: Meer informatie over hoe toomake een telefonische oproep en verzend een SMS-met Hallo Twilio-API-service op Azure bericht. Codevoorbeelden geschreven in PHP.
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden van PHP
Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello Twilio-API-service op Azure. Hallo scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden. Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen Hallo [Vervolgstappen](#NextSteps) sectie.

## <a id="WhatIs"></a>Wat is Twilio?
Twilio is dat toekomstige Hallo zakelijke communicatie, ontwikkelaars tooembed spraak, VoIP, inschakelen en messaging in toepassingen. Ze virtualiseren alle infrastructuur die nodig is in een cloud-gebaseerde, globale-omgeving, beschikbaar te maken via Hallo Twilio communications API-platform. Toepassingen zijn eenvoudige toobuild en schaalbare. Profiteer van flexibiliteit met pay-as-you gaat prijzen en profiteren van de betrouwbaarheid van de cloud.

**Twilio stem** kunt u uw toepassingen toomake en gebeld. **Twilio SMS** kunt u uw toepassing toosend tekstberichten en ontvangen. **Twilio Client** kunt u toomake VoIP-aanroepen vanuit een telefoon, tablet of een browser en WebRTC ondersteunt.

## <a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen
Azure-klanten ontvangen een [speciale aanbieding](http://www.twilio.com/azure): gratis $10 Twilio tegoed wanneer u een upgrade uitvoert van uw Twilio-Account. Deze Twilio-tegoed kan worden toegepast tooany Twilio-gebruik ($10 tegoed gelijkwaardige toosending maximaal 1000 SMS-berichten of ontvangst van too1000 inkomende stem minuten, afhankelijk van de locatie van uw telefoon en bericht- of aanroep bestemming Hallo). Deze Twilio-tegoed inwisselen en aan de slag op: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio is een betalen naar gebruik service. Er zijn geen kosten instellen en kunt u uw account op elk moment sluiten. U vindt meer informatie op [Twilio prijzen][twilio_pricing].

## <a id="Concepts"></a>Concepten
Hallo Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen. Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].

Belangrijke aspecten van Hallo Twilio-API zijn Twilio-termen en Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Twilio-termen
Hallo API wordt gebruikgemaakt van Twilio termen; bijvoorbeeld, Hallo  **&lt;zeg&gt;**  term Hiermee Twilio tooaudibly afleveren geeft een bericht op een aanroep.

Hallo Hieronder volgt een lijst met Twilio-bewerkingen. Meer informatie over Hallo andere termen en mogelijkheden via [Twilio Markup Language documentatie](http://www.twilio.com/docs/api/twiml).

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

### <a id="TwiML"></a>TwiML
TwiML is een reeks XML gebaseerde instructies op basis van Hallo Twilio-termen die Twilio van hoe u informeren over tooprocess een telefoongesprek of SMS.

Als u bijvoorbeeld Hallo TwiML na Hallo tekst wilt converteren **Hallo wereld** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Bij het aanroepen van uw toepassing hello Twilio-API, is een van de API-parameters Hallo Hallo-URL die Hallo TwiML antwoord geretourneerd. U kunt voor ontwikkelingsdoeleinden Twilio geleverde URL's tooprovide hello TwiML antwoorden die wordt gebruikt door uw toepassingen. U ook uw eigen URL's tooproduce hello TwiML reacties kan hosten en een andere optie is toouse hello **TwiMLResponse** object.

Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml]. Zie voor meer informatie over Hallo Twilio-API, [Twilio-API][twilio_api].

## <a id="CreateAccount"></a>Een Twilio-Account maken
Wanneer u klaar tooget een Twilio-account bent, aanmelden op [probeer Twilio][try_twilio]. U kunt beginnen met een gratis account en upgrade van uw account later.

Wanneer u zich voor een Twilio-account aanmeldt, ontvangt u een account-ID en geen verificatietoken. Beide worden benodigde toomake Twilio-API-aanroepen. tooprevent onbevoegde toegang tot tooyour account, het verificatietoken te beveiligen. Uw account-ID en verificatie token kunnen worden bekeken op Hallo [Twilio-accountpagina][twilio_account]in velden met het label Hallo **ACCOUNT-SID** en **AUTH TOKEN**respectievelijk.

## <a id="create_app"></a>Een PHP-toepassing maken
Een PHP-toepassing die gebruikmaakt van Hallo Twilio-service en wordt uitgevoerd in Azure gaat niet anders dan de andere PHP-toepassing die gebruikmaakt van Hallo Twilio-service. Terwijl Twilio-services op basis van REST worden en op verschillende manieren kunnen worden aangeroepen vanuit PHP, in dit artikel wordt de nadruk gelegd op hoe toouse Twilio services met [Twilio-bibliotheek voor PHP vanuit GitHub][twilio_php]. Zie voor meer informatie over het gebruik van Hallo Twilio-bibliotheek voor PHP [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].

Gedetailleerde instructies voor het bouwen en implementeren van een toepassing Twilio/PHP tooAzure zijn beschikbaar op [hoe tooMake een telefonische oproep met behulp van Twilio in een PHP-toepassing in Azure][howto_phonecall_php].

## <a id="configure_app"></a>Configureren van uw toepassing tooUse Twilio-bibliotheken
U kunt uw toepassing toouse hello Twilio-bibliotheek configureren voor PHP op twee manieren:

1. Hallo Twilio-bibliotheek voor PHP vanuit GitHub downloaden ([https://github.com/twilio/twilio-php][twilio_php]) en voeg Hallo **Services** directory tooyour-toepassing.
   
    OF
2. Hallo Twilio-bibliotheek voor PHP installeren als een PEER-pakket. Het kan worden geïnstalleerd met Hallo volgende opdrachten:
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

Zodra u Hallo Twilio-bibliotheek voor PHP hebt geïnstalleerd, kunt u vervolgens toevoegen een **require_once** instructie Hallo boven aan uw PHP-bestanden tooreference Hallo bibliotheek:

        require_once 'Services/Twilio.php';

Zie voor meer informatie [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Procedure: een uitgaande aanroep
Hallo hieronder ziet u hoe een uitgaande toomake-gesprek Hallo **Services_Twilio** klasse. Deze code wordt een Twilio-voorwaarde site tooreturn hello Twilio Markup Language (TwiML) antwoord. Vervang uw waarden voor Hallo **van** en **naar** telefoonnummers, en zorg ervoor dat u controleert of Hallo **van** telefoonnummer voor uw Twilio-account voorafgaande toorunning Hallo code.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Zoals gezegd, gebruikt deze code een Twilio-voorwaarde site tooreturn hello TwiML antwoord. U kunt in plaats hiervan uw eigen site tooprovide hello TwiML antwoord; Zie voor meer informatie [hoe tooProvide TwiML antwoorden vanaf uw eigen website](#howto_provide_twiml_responses).

* **Opmerking**: validatiefouten voor tootroubleshoot SSL-certificaat, Zie [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>Procedure: een SMS-bericht verzenden
Hallo hieronder ziet u hoe een SMS-bericht met toosend Hallo **Services_Twilio** klasse. Hallo **van** nummer wordt geleverd door Twilio voor proefversie accounts toosend SMS-berichten. Hallo **naar** nummer om uw Twilio-account voorafgaande toorunning Hallo-code moet worden geverifieerd.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a>Hoe: TwiML reacties van uw eigen Website opgeven
Wanneer uw toepassing een aanroep van toohello Twilio-API initieert, stuurt Twilio uw aanvraag tooa-URL die wordt verwacht tooreturn TwiML antwoord. Hallo in bovenstaand voorbeeld gebruikt Hallo Twilio-geleverde URL [http://twimlets.com/message][twimlet_message_url]. (Hoewel TwiML is ontworpen voor gebruik door Twilio, vindt u het Hallo in uw browser. Bijvoorbeeld, klik op [http://twimlets.com/message] [ twimlet_message_url] toosee een lege `<Response>` element; Klik bijvoorbeeld op [http://twimlets.com/message? Bericht % 5B0 %5, D = Hallo % 20World] [ twimlet_message_url_hello_world] toosee een `<Response>` element met een `<Say>` element.)

In plaats van te vertrouwen op Hallo geleverde Twilio-URL, kunt u uw eigen website waarmee HTTP-antwoorden worden geretourneerd. U kunt Hallo-site maken in een andere taal die als resultaat geeft de XML-reacties; in dit onderwerp wordt ervan uitgegaan dat u PHP toocreate hello TwiML wilt gebruiken.

Hallo PHP pagina resultaten in een antwoord TwiML waarin staat dat na **Hallo wereld** op Hallo-aanroep.

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

Zoals u in de bovenstaande Hallo voorbeeld zien kunt, is het Hallo TwiML antwoord gewoon een XML-document. Hallo Twilio-bibliotheek voor PHP bevat klassen die voor u TwiML genereren. Hallo onderstaand voorbeeld gelijkwaardige antwoord Hallo produceert, zoals hierboven, maar gebruikt Hallo **Services\_Twilio\_Twiml** klasse in Hallo Twilio-bibliotheek voor PHP:

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

Zie voor meer informatie over TwiML [https://www.twilio.com/docs/api/twiml][twiml_reference]. 

Zodra u uw PHP-pagina tooprovide TwiML antwoorden instellen hebt, Hallo-URL van Hallo PHP-pagina gebruiken als de URL die wordt doorgegeven in Hallo Hallo `Services_Twilio->account->calls->create` methode. Bijvoorbeeld, als u een webtoepassing met de naam hebt **MyTwiML** geïmplementeerde tooan Azure gehoste service en het Hallo-naam van de PHP-pagina Hallo is **mytwiml.php**, Hallo URL te kan worden doorgegeven **Services_ Twilio-account > -> aanroepen -> maken** zoals weergegeven in Hallo voorbeeld te volgen:

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Zie voor meer informatie over het gebruik van Twilio in Azure met PHP [hoe tooMake een telefonische oproep met behulp van Twilio in een PHP-toepassing in Azure][howto_phonecall_php].

## <a id="AdditionalServices"></a>How to: extra Twilio-Services gebruiken
Bovendien kunt toohello voorbeelden die hier worden weergegeven, dat twilio biedt op basis van een web-API's u tooleverage aanvullende Twilio-functionaliteit van uw Azure-toepassing. Zie voor meer details Hallo [Twilio-API-documentatie][twilio_api_documentation].

## <a id="NextSteps"></a>Volgende stappen
Nu u basisprincipes Hallo Hallo Twilio-service hebt geleerd, volgt u deze koppelingen toolearn meer:

* [Richtlijnen voor Twilio-beveiliging][twilio_security_guidelines]
* [Van de procedure Twilio en voorbeeldcode][twilio_howtos]
* [Twilio Quick Start-zelfstudie][twilio_quickstarts] 
* [Twilio op GitHub][twilio_on_github]
* [Neem contact tooTwilio ondersteuning][twilio_support]

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
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
