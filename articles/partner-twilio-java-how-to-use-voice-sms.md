---
title: aaaHow tooUse Twilio voor spraak- en SMS (Java) | Microsoft Docs
description: Meer informatie over hoe toomake een telefonische oproep en verzend een SMS-met Hallo Twilio-API-service op Azure bericht. Codevoorbeelden geschreven in Java.
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a>Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden in Java
Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello Twilio-API-service op Azure. Hallo scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden. Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen Hallo [Vervolgstappen](#NextSteps) sectie.

## <a id="WhatIs"></a>Wat is Twilio?
Twilio is een telephony-webservice-API waarmee u uw bestaande web talen en de vaardigheden toobuild stem en de SMS-toepassingen gebruiken. Twilio is een service van derden (niet een functie van Azure en niet in een Microsoft-product).

**Twilio stem** kunt u uw toepassingen toomake en gebeld. **Twilio SMS** kunt u uw toepassingen toomake en SMS-berichten ontvangen. **Twilio Client** zorgt ervoor dat uw toepassingen tooenable gesproken communicatie met bestaande Internet-verbindingen, inclusief mobiele verbindingen.

## <a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen
Informatie over prijzen voor Twilio is beschikbaar op [Twilio prijzen][twilio_pricing]. Azure-klanten ontvangen een [speciale aanbieding][special_offer]: een gratis tegoed van 1000 teksten of 1000 inkomende minuten. toosign voor dit bieden of meer informatie, gaat u naar [http://ahoy.twilio.com/azure][special_offer].

## <a id="Concepts"></a>Concepten
Hallo Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen. Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].

Belangrijke aspecten van Hallo Twilio-API zijn Twilio-termen en Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Twilio-termen
Hallo API wordt gebruikgemaakt van Twilio termen; bijvoorbeeld, Hallo  **&lt;zeg&gt;**  term Hiermee Twilio tooaudibly afleveren geeft een bericht op een aanroep.

Hallo Hieronder volgt een lijst met Twilio-bewerkingen.

* **&lt;Externe&gt;**: Hallo aanroeper tooanother telefoon verbindt.
* **&lt;Verzamel&gt;**: cijfers ingevoerd op het telefoonnummer Hallo verzamelt.
* **&lt;Ophangen&gt;**: een aanroep wordt beëindigd.
* **&lt;Afspelen&gt;**: een geluidsbestand afgespeeld.
* **&lt;Wachtrij&gt;**: Hallo tooa wachtrij van aanroepfuncties toevoegen.
* **&lt;Onderbreken&gt;**: achtergrond wacht op een opgegeven aantal seconden.
* **&lt;Record&gt;**: Hallo aanroeper stem registreert en retourneert een URL van een bestand dat Hallo opname bevat.
* **&lt;Omleiden&gt;**: draagt de controle van een telefoongesprek of SMS toohello TwiML op een andere URL.
* **&lt;Afwijzen&gt;**: geweigerd een binnenkomende tooyour Twilio nummer bellen zonder u facturering.
* **&lt;Zeg&gt;**: zet tekst toospeech die wordt gemaakt op een aanroep.
* **&lt;SMS&gt;**: een SMS-bericht verzonden.

### <a id="TwiML"></a>TwiML
TwiML is een reeks XML gebaseerde instructies op basis van Hallo Twilio-termen die Twilio van hoe u informeren over tooprocess een telefoongesprek of SMS.

Als u bijvoorbeeld Hallo TwiML na Hallo tekst wilt converteren **Hello World!** toospeech.

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

Bij het aanroepen van uw toepassing hello Twilio-API, is een van de API-parameters Hallo Hallo-URL die Hallo TwiML antwoord geretourneerd. U kunt voor ontwikkelingsdoeleinden Twilio geleverde URL's tooprovide hello TwiML antwoorden die wordt gebruikt door uw toepassingen. U ook uw eigen URL's tooproduce hello TwiML reacties kan hosten en een andere optie is toouse hello **TwiMLResponse** object.

Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml]. Zie voor meer informatie over Hallo Twilio-API, [Twilio-API][twilio_api].

## <a id="CreateAccount"></a>Een Twilio-Account maken
Wanneer u klaar tooget een Twilio-account bent, aanmelden op [probeer Twilio][try_twilio]. U kunt beginnen met een gratis account en upgrade van uw account later.

Wanneer u zich voor een Twilio-account aanmeldt, ontvangt u een account-ID en geen verificatietoken. Beide worden benodigde toomake Twilio-API-aanroepen. tooprevent onbevoegde toegang tot tooyour account, het verificatietoken te beveiligen. Uw account-ID en verificatie token kunnen worden bekeken op Hallo [Twilio Console][twilio_console]in velden met het label Hallo **ACCOUNT-SID** en **AUTH TOKEN**respectievelijk.

## <a id="create_app"></a>Een Java-toepassing maken
1. Hallo Twilio JAR verkrijgen en voeg deze tooyour Java build pad en de WAR implementatie-assembly. Op [https://github.com/twilio/twilio-java][twilio_java], kunt u bronnen voor Hallo GitHub downloaden en uw eigen JAR maken of een vooraf samengestelde JAR (met of zonder afhankelijkheden) downloaden.
2. Zorg ervoor dat uw JDK **cacerts** keystore Hallo Equifax beveiligde CA-certificaat bevat met MD5 vingerafdruk 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Hallo serienummer is 35:DE:F4:CF en Hallo SHA1 vingerafdruk is D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Dit is Hallo-certificaat (certificeringsinstantie)-certificaat voor Hallo [https://api.twilio.com] [ twilio_api_service] -service, die wordt aangeroepen wanneer u Twilio APIs gebruiken. Voor informatie over uw JDK gezorgd **cacerts** keystore bevat Hallo juiste CA-certificaat, Zie [toevoegen van een certificaat toohello Java CA-certificaatarchief][add_ca_cert].

Gedetailleerde instructies voor het gebruik van Hallo Twilio-clientbibliotheek voor Java zijn beschikbaar op [hoe tooMake een telefonische oproep met behulp van Twilio in een Java-toepassing in Azure][howto_phonecall_java].

## <a id="configure_app"></a>Configureren van uw toepassing tooUse Twilio-bibliotheken
U kunt binnen uw code toevoegen **importeren** instructies Hallo boven aan de bronbestanden voor Hallo Twilio-pakketten of u klassen wilt toouse in uw toepassing.

Voor Java-bronbestanden:

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

Voor de bronbestanden van de pagina voor Java-Server (JSP):

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
Afhankelijk van welke Twilio-pakketten of klassen die u wilt toouse, uw **importeren** instructies kunnen afwijken.

## <a id="howto_make_call"></a>Procedure: een uitgaande aanroep
Hallo hieronder ziet u hoe een uitgaande toomake-gesprek Hallo **aanroepen** klasse. Deze code wordt een Twilio-voorwaarde site tooreturn hello Twilio Markup Language (TwiML) antwoord. Vervang uw waarden voor Hallo **van** en **naar** telefoonnummers, en zorg ervoor dat u controleert of Hallo **van** telefoonnummer voor uw Twilio-account voorafgaande toorunning Hallo code.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Voor meer informatie over Hallo parameters doorgegeven toohello **Call.creator** methode, Zie [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Zoals gezegd, gebruikt deze code een Twilio-voorwaarde site tooreturn hello TwiML antwoord. U kunt in plaats hiervan uw eigen site tooprovide hello TwiML antwoord; Zie voor meer informatie [hoe tooProvide TwiML antwoorden in een Java-toepassing in Azure](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Procedure: een SMS-bericht verzenden
Hallo hieronder ziet u hoe een SMS-bericht met toosend Hallo **bericht** klasse. Hallo **van** getal, **4155992671**, wordt geleverd door Twilio voor proefversie accounts toosend SMS-berichten. Hallo **naar** nummer om uw Twilio-account voorafgaande toorunning Hallo-code moet worden geverifieerd.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

Voor meer informatie over Hallo parameters doorgegeven toohello **Message.creator** methode, Zie [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].

## <a id="howto_provide_twiml_responses"></a>Hoe: TwiML reacties van uw eigen Website opgeven
Wanneer uw toepassing een aanroep van toohello Twilio-API, bijvoorbeeld via Hallo initieert **CallCreator.create** methode Twilio verzendt uw aanvraag tooa-URL is de verwachte tooreturn een TwiML antwoord. Hallo in bovenstaand voorbeeld gebruikt Hallo Twilio-geleverde URL [http://twimlets.com/message][twimlet_message_url]. (Hoewel TwiML is ontworpen voor gebruik door webservices, u kunt weergeven Hallo TwiML in uw browser. Bijvoorbeeld, klik op [http://twimlets.com/message] [ twimlet_message_url] toosee een lege  **&lt;antwoord&gt;**  element; klik op alseenandervoorbeeld:[http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee een  **&lt;antwoord&gt;**  element met een  **&lt;Zeg &gt;**  element.)

In plaats van te vertrouwen op Hallo geleverde Twilio-URL, kunt u uw eigen website URL waarmee HTTP-antwoorden worden geretourneerd. U kunt Hallo-site maken in een andere taal waarmee HTTP-antwoorden; in dit onderwerp wordt ervan uitgegaan dat u gaat hosten Hallo-URL in een JSP-pagina.

Hallo JSP pagina resultaten in een antwoord TwiML waarin staat dat na **Hello World!** op het Hallo-aanroep.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

Hallo volgende JSP pagina resulteert in een TwiML-antwoord dat wat tekst vertelt heeft verschillende gepauzeerd en staat informatie over Hallo Twilio-API-versie en hello Azure role-naam.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

Hallo **ApiVersion** parameter is beschikbaar in Twilio voice-aanvragen (geen SMS-aanvragen). toosee hello beschikbaar aanvraagparameters voor spraak Twilio- en SMS-aanvragen, Zie <https://www.twilio.com/docs/api/twiml/twilio_request> en <https://www.twilio.com/docs/api/twiml/sms/twilio_request >respectievelijk. Hallo **RoleName** omgevingsvariabele is beschikbaar als onderdeel van een Azure-implementatie. (Als u wilt dat de aangepaste omgevingsvariabelen tooadd zodat deze kunnen worden opgehaald uit **System.getenv**, Zie Hallo omgeving variabelen sectie op [configuratie-instellingen van diverse rol] [misc_role_config_settings].)

Zodra u uw JSP-pagina tooprovide TwiML antwoorden instellen hebt, Hallo-URL van Hallo JSP-pagina gebruiken als de URL die wordt doorgegeven in Hallo Hallo **Call.creator** methode. Bijvoorbeeld, als u een webtoepassing hebt met de naam MyTwiML geïmplementeerd tooan Azure gehoste service, en Hallo-naam van Hallo JSP pagina mytwiml.jsp, Hallo-URL te kan worden doorgegeven**Call.creator** zoals weergegeven in de volgende Hallo:

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Er is een andere optie voor het beantwoorden van TwiML via Hallo **VoiceResponse** klasse, die beschikbaar in Hallo is **com.twilio.twiml** pakket.

Zie voor meer informatie over het gebruik van Twilio in Azure met Java [hoe tooMake een telefonische oproep met behulp van Twilio in een Java-toepassing in Azure][howto_phonecall_java].

## <a id="AdditionalServices"></a>How to: extra Twilio-Services gebruiken
Bovendien kunt toohello voorbeelden die hier worden weergegeven, dat twilio biedt op basis van een web-API's u tooleverage aanvullende Twilio-functionaliteit van uw Azure-toepassing. Zie voor meer details Hallo [Twilio-API-documentatie][twilio_api_documentation].

## <a id="NextSteps"></a>Volgende stappen
Nu u basisprincipes Hallo Hallo Twilio-service hebt geleerd, volgt u deze koppelingen toolearn meer:

* [Richtlijnen voor Twilio-beveiliging][twilio_security_guidelines]
* [Van de procedure Twilio en voorbeeldcode][twilio_howtos]
* [Twilio Quick Start-zelfstudie][twilio_quickstarts]
* [Twilio op GitHub][twilio_on_github]
* [Neem contact tooTwilio ondersteuning][twilio_support]

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
