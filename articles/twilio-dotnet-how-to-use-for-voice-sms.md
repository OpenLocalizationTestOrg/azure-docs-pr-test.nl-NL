---
title: aaaHow tooUse Twilio voor spraak- en SMS (.NET) | Microsoft Docs
description: Meer informatie over hoe toomake een telefonische oproep en verzend een SMS-met Hallo Twilio-API-service op Azure bericht. Codevoorbeelden geschreven in .NET.
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a>Hoe toouse Twilio voor spraak- en SMS-mogelijkheden van Azure
Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello Twilio-API-service op Azure. Hallo scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden. Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen Hallo [Vervolgstappen](#NextSteps) sectie.

## <a id="WhatIs"></a>Wat is Twilio?
Twilio is dat toekomstige Hallo zakelijke communicatie, ontwikkelaars tooembed spraak, VoIP, inschakelen en messaging in toepassingen. Ze virtualiseren alle infrastructuur die nodig is in een cloud-gebaseerde, globale-omgeving, beschikbaar te maken via Hallo Twilio communications API-platform. Toepassingen zijn eenvoudige toobuild en schaalbare. Profiteer van flexibiliteit met betalen naar gebruik prijzen en profiteren van de betrouwbaarheid van de cloud.

**Twilio stem** kunt u uw toepassingen toomake en gebeld. **Twilio SMS** kunt u uw toepassingen toosend en SMS-berichten ontvangen. **Twilio Client** kunt u toomake VoIP-aanroepen vanuit een telefoon, tablet of een browser en WebRTC ondersteunt.

## <a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen
Azure-klanten ontvangen een [speciale aanbieding](http://www.twilio.com/azure): gratis $10 Twilio tegoed wanneer u een upgrade uitvoert van uw Twilio-Account. Deze Twilio-tegoed kan worden toegepast tooany Twilio-gebruik ($10 tegoed gelijkwaardige toosending maximaal 1000 SMS-berichten of ontvangst van too1000 inkomende stem minuten, afhankelijk van de locatie van uw telefoon en bericht- of aanroep bestemming Hallo). Deze Twilio-tegoed inwisselen en aan de slag op [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio is een betalen naar gebruik service. Er zijn geen kosten instellen en kunt u uw account op elk moment sluiten. U vindt meer informatie op [Twilio prijzen](http://www.twilio.com/voice/pricing).

## <a id="Concepts"></a>Concepten
Hallo Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen. Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].

Belangrijke aspecten van Hallo Twilio-API zijn Twilio-termen en Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Twilio-termen
Hallo API wordt gebruikgemaakt van Twilio termen; bijvoorbeeld, Hallo  **&lt;zeg&gt;**  term Hiermee Twilio tooaudibly afleveren geeft een bericht op een aanroep.

Hallo Hieronder volgt een lijst met Twilio-bewerkingen.  Meer informatie over Hallo andere termen en mogelijkheden via [Twilio Markup Language documentatie](http://www.twilio.com/docs/api/twiml).

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

## <a id="create_app"></a>Een Azure-toepassing maken
Een Azure-toepassing die als host fungeert voor een toepassing Twilio ingeschakeld is niet anders als elke andere Azure-toepassing. U Hallo Twilio .NET-bibliotheek toevoegen en configureren van Hallo rol toouse hello Twilio .NET-bibliotheken.
Zie voor meer informatie over het maken van een eerste Azure-project [een Azure-project maken met Visual Studio][vs_project].

## <a id="configure_app"></a>Configureren van uw toepassing toouse Twilio-bibliotheken
Twilio biedt een reeks .NET helper-bibliotheken die verschillende aspecten van Twilio tooprovide eenvoudig en gemakkelijk manieren toointeract met Hallo Twilio REST-API en Twilio Client teruglopen toogenerate TwiML reacties.

Twilio bevat vijf bibliotheken voor .NET-ontwikkelaars:
Bibliotheek|Beschrijving
---|---
Twilio.API|Hallo core Twilio-bibliotheek die Hallo Twilio REST-API in een beschrijvende .NET-bibliotheek terugloopt. Deze bibliotheek is beschikbaar voor .NET, Silverlight en Windows Phone 7.
Twilio.TwiML|Biedt een .NET gebruiksvriendelijke manier toogenerate TwiML aantekeningen.
Twilio.MVC|Voor ontwikkelaars met ASP.NET MVC, bevat deze bibliotheek een TwilioController, TwiML ActionResult en aanvraag validatiekenmerk.
Twilio.WebMatrix|Deze bibliotheek bevat voor ontwikkelaars met ontwikkelsysteem van Microsoft gratis WebMatrix, Razor syntaxis van de hulpprogramma's voor verschillende Twilio-acties.
Twilio.Client.Capability|Hallo mogelijkheid token generator voor gebruik met Hallo Twilio Client JavaScript SDK bevat.

Houd er rekening mee dat alle bibliotheken .NET 3.5, Silverlight 4 of Windows Phone 7 of hoger vereist.

Hallo voorbeelden in deze handleiding Hallo Twilio.API bibliotheek gebruiken.

Hallo-bibliotheken mag [geïnstalleerd met behulp van Hallo NuGet package manager extensie](http://www.twilio.com/docs/csharp/install) beschikbaar is voor Visual Studio 2010 up too2015.  Hallo broncode op wordt gehost [GitHub][twilio_github_repo], waaronder een Wiki met volledige documentatie voor het gebruik van Hallo-bibliotheken.

Microsoft Visual Studio 2010 installeert standaard versie 1.2 van NuGet. Hallo Twilio-bibliotheken installeren vereist versie 1.6 van NuGet of hoger. Zie voor meer informatie over het installeren of bijwerken van NuGet [http://nuget.org/][nuget].

> [!NOTE]
> tooinstall hello meest recente versie van NuGet, moet u eerst Hallo geladen versie met behulp van Visual Studio-extensie Manager Hallo verwijderen. toodo geval is, moet u Visual Studio uitvoeren als administrator. Anders wordt is de knop verwijderen Hallo uitgeschakeld.
>
>

### <a id="use_nuget"></a>tooadd hello Twilio-bibliotheken tooyour Visual Studio-project:
1. Open uw oplossing in Visual Studio.
2. Met de rechtermuisknop op **verwijzingen**.
3. Klik op **NuGet-pakketten beheren...**
4. Klik op **Online**.
5. Typ in de online zoekvak hello, *twilio*.
6. Klik op **installeren** op Hallo Twilio-pakket.

## <a id="howto_make_call"></a>Procedure: een uitgaande aanroep
Hallo hieronder ziet u hoe een uitgaande toomake-gesprek Hallo **CallResource** klasse. Deze code wordt een Twilio-voorwaarde site tooreturn hello Twilio Markup Language (TwiML) antwoord. Vervang uw waarden voor Hallo **naar** en **van** telefoonnummers, en zorg ervoor dat u controleert of Hallo **van** telefoonnummer voor uw Twilio-account voordat Hallo code wordt uitgevoerd.

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

Voor meer informatie over Hallo parameters doorgegeven toohello **CallResource.Create** methode, Zie [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Zoals gezegd, gebruikt deze code een Twilio-voorwaarde site tooreturn hello TwiML antwoord. U kunt in plaats hiervan uw eigen site tooprovide hello TwiML antwoord. Zie voor meer informatie [hoe: bieden TwiML reacties van uw eigen website](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Procedure: een SMS-bericht verzenden
Hallo volgende schermafbeelding ziet u hoe een SMS-bericht met toosend Hallo **MessageResource** klasse. Hallo **van** nummer wordt geleverd door Twilio voor proefversie accounts toosend SMS-berichten. Hallo **naar** nummer voor uw Twilio-account moet worden geverifieerd voordat u Hallo code uitvoeren.

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <a id="howto_provide_twiml_responses"></a>Hoe: TwiML reacties van uw eigen website opgeven
Wanneer uw toepassing initieert een aanroep van toohello Twilio-API - bijvoorbeeld via Hallo **CallResource.Create** methode - Twilio stuurt de aanvraag-URL voor tooan die verwachte tooreturn is een antwoord TwiML. Hallo-voorbeeld in [hoe: geen uitgaande aanroep doen](#howto_make_call) gebruikt Hallo Twilio-geleverde URL [http://twimlets.com/message] [ twimlet_message_url] tooreturn Hallo antwoord.

> [!NOTE]
> Hoewel TwiML is ontworpen voor gebruik door webservices, kunt u Hallo TwiML kunt weergeven in uw browser. Bijvoorbeeld, klik op [http://twimlets.com/message] [ twimlet_message_url] toosee een lege &lt;antwoord&gt; element; Klik bijvoorbeeld op [http://twimlets.com/message ? Bericht % 5B0 %5, D = Hallo % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee een &lt;antwoord&gt; element met een &lt;zeg&gt; element.
>
>

In plaats van te vertrouwen op Hallo geleverde Twilio-URL, kunt u uw eigen website URL waarmee HTTP-antwoorden worden geretourneerd. U kunt Hallo site maken in een andere taal waarmee HTTP-antwoorden worden geretourneerd. In dit onderwerp wordt ervan uitgegaan dat u Hallo-URL van een algemene ASP.NET-handler moet worden gehost.

Hallo na ASP.NET-Handler een antwoord TwiML waarin staat dat crafts **Hallo wereld** op Hallo-aanroep.

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
Zoals u in de bovenstaande Hallo voorbeeld zien kunt, is het Hallo TwiML antwoord gewoon een XML-document. Hallo Twilio.TwiML bibliotheek bevat de klassen die voor u TwiML genereren. Hallo onderstaand voorbeeld gelijkwaardige antwoord Hallo produceert, zoals hierboven beschreven, maar gebruikt Hallo **VoiceResponse** klasse.

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

Zie voor meer informatie over TwiML [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).

Nadat u een manier tooprovide TwiML antwoorden hebt ingesteld, kunt u die URL toohello doorgeven **CallResource.Create** methode. Bijvoorbeeld, als u een webtoepassing met de naam MyTwiML geïmplementeerd tooan Azure-cloudservice hebt en Hallo-naam van uw ASP.NET-Handler mytwiml.ashx is, Hallo-URL kan worden doorgegeven te**CallResource.Create** zoals weergegeven in de volgende code Hallo Voorbeeld:

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

Zie voor meer informatie over het gebruik van Twilio in Azure met ASP.NET [hoe toomake een telefoon aanroepen in een Webrol in Azure met behulp van Twilio][howto_phonecall_dotnet].

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
