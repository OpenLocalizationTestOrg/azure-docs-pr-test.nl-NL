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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="ff8c8-104">Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden in Java</span><span class="sxs-lookup"><span data-stu-id="ff8c8-104">How tooUse Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="ff8c8-105">Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello Twilio-API-service op Azure.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="ff8c8-106">Hallo scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="ff8c8-107">Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen Hallo [Vervolgstappen](#NextSteps) sectie.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="ff8c8-108"><a id="WhatIs"></a>Wat is Twilio?</span><span class="sxs-lookup"><span data-stu-id="ff8c8-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="ff8c8-109">Twilio is een telephony-webservice-API waarmee u uw bestaande web talen en de vaardigheden toobuild stem en de SMS-toepassingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="ff8c8-110">Twilio is een service van derden (niet een functie van Azure en niet in een Microsoft-product).</span><span class="sxs-lookup"><span data-stu-id="ff8c8-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="ff8c8-111">**Twilio stem** kunt u uw toepassingen toomake en gebeld.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="ff8c8-112">**Twilio SMS** kunt u uw toepassingen toomake en SMS-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="ff8c8-113">**Twilio Client** zorgt ervoor dat uw toepassingen tooenable gesproken communicatie met bestaande Internet-verbindingen, inclusief mobiele verbindingen.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="ff8c8-114"><a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="ff8c8-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="ff8c8-115">Informatie over prijzen voor Twilio is beschikbaar op [Twilio prijzen][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="ff8c8-116">Azure-klanten ontvangen een [speciale aanbieding][special_offer]: een gratis tegoed van 1000 teksten of 1000 inkomende minuten.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="ff8c8-117">toosign voor dit bieden of meer informatie, gaat u naar [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="ff8c8-118"><a id="Concepts"></a>Concepten</span><span class="sxs-lookup"><span data-stu-id="ff8c8-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="ff8c8-119">Hallo Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="ff8c8-120">Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="ff8c8-121">Belangrijke aspecten van Hallo Twilio-API zijn Twilio-termen en Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="ff8c8-121">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="ff8c8-122"><a id="Verbs"></a>Twilio-termen</span><span class="sxs-lookup"><span data-stu-id="ff8c8-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="ff8c8-123">Hallo API wordt gebruikgemaakt van Twilio termen; bijvoorbeeld, Hallo  **&lt;zeg&gt;**  term Hiermee Twilio tooaudibly afleveren geeft een bericht op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-123">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="ff8c8-124">Hallo Hieronder volgt een lijst met Twilio-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-124">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="ff8c8-125">**&lt;Externe&gt;**: Hallo aanroeper tooanother telefoon verbindt.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-125">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="ff8c8-126">**&lt;Verzamel&gt;**: cijfers ingevoerd op het telefoonnummer Hallo verzamelt.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-126">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="ff8c8-127">**&lt;Ophangen&gt;**: een aanroep wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="ff8c8-128">**&lt;Afspelen&gt;**: een geluidsbestand afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="ff8c8-129">**&lt;Wachtrij&gt;**: Hallo tooa wachtrij van aanroepfuncties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-129">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="ff8c8-130">**&lt;Onderbreken&gt;**: achtergrond wacht op een opgegeven aantal seconden.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="ff8c8-131">**&lt;Record&gt;**: Hallo aanroeper stem registreert en retourneert een URL van een bestand dat Hallo opname bevat.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-131">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="ff8c8-132">**&lt;Omleiden&gt;**: draagt de controle van een telefoongesprek of SMS toohello TwiML op een andere URL.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="ff8c8-133">**&lt;Afwijzen&gt;**: geweigerd een binnenkomende tooyour Twilio nummer bellen zonder u facturering.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-133">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="ff8c8-134">**&lt;Zeg&gt;**: zet tekst toospeech die wordt gemaakt op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-134">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="ff8c8-135">**&lt;SMS&gt;**: een SMS-bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="ff8c8-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="ff8c8-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="ff8c8-137">TwiML is een reeks XML gebaseerde instructies op basis van Hallo Twilio-termen die Twilio van hoe u informeren over tooprocess een telefoongesprek of SMS.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-137">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="ff8c8-138">Als u bijvoorbeeld Hallo TwiML na Hallo tekst wilt converteren **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="ff8c8-138">As an example, hello following TwiML would convert hello text **Hello World!**</span></span> <span data-ttu-id="ff8c8-139">toospeech.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-139">toospeech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="ff8c8-140">Bij het aanroepen van uw toepassing hello Twilio-API, is een van de API-parameters Hallo Hallo-URL die Hallo TwiML antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-140">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="ff8c8-141">U kunt voor ontwikkelingsdoeleinden Twilio geleverde URL's tooprovide hello TwiML antwoorden die wordt gebruikt door uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-141">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="ff8c8-142">U ook uw eigen URL's tooproduce hello TwiML reacties kan hosten en een andere optie is toouse hello **TwiMLResponse** object.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-142">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="ff8c8-143">Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="ff8c8-144">Zie voor meer informatie over Hallo Twilio-API, [Twilio-API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-144">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="ff8c8-145"><a id="CreateAccount"></a>Een Twilio-Account maken</span><span class="sxs-lookup"><span data-stu-id="ff8c8-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="ff8c8-146">Wanneer u klaar tooget een Twilio-account bent, aanmelden op [probeer Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-146">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="ff8c8-147">U kunt beginnen met een gratis account en upgrade van uw account later.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="ff8c8-148">Wanneer u zich voor een Twilio-account aanmeldt, ontvangt u een account-ID en geen verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="ff8c8-149">Beide worden benodigde toomake Twilio-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-149">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="ff8c8-150">tooprevent onbevoegde toegang tot tooyour account, het verificatietoken te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-150">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="ff8c8-151">Uw account-ID en verificatie token kunnen worden bekeken op Hallo [Twilio Console][twilio_console]in velden met het label Hallo **ACCOUNT-SID** en **AUTH TOKEN**respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-151">Your account ID and authentication token are viewable at hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="ff8c8-152"><a id="create_app"></a>Een Java-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="ff8c8-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="ff8c8-153">Hallo Twilio JAR verkrijgen en voeg deze tooyour Java build pad en de WAR implementatie-assembly.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-153">Obtain hello Twilio JAR and add it tooyour Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="ff8c8-154">Op [https://github.com/twilio/twilio-java][twilio_java], kunt u bronnen voor Hallo GitHub downloaden en uw eigen JAR maken of een vooraf samengestelde JAR (met of zonder afhankelijkheden) downloaden.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="ff8c8-155">Zorg ervoor dat uw JDK **cacerts** keystore Hallo Equifax beveiligde CA-certificaat bevat met MD5 vingerafdruk 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Hallo serienummer is 35:DE:F4:CF en Hallo SHA1 vingerafdruk is D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="ff8c8-155">Ensure your JDK's **cacerts** keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="ff8c8-156">Dit is Hallo-certificaat (certificeringsinstantie)-certificaat voor Hallo [https://api.twilio.com] [ twilio_api_service] -service, die wordt aangeroepen wanneer u Twilio APIs gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-156">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="ff8c8-157">Voor informatie over uw JDK gezorgd **cacerts** keystore bevat Hallo juiste CA-certificaat, Zie [toevoegen van een certificaat toohello Java CA-certificaatarchief][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-157">For information about ensuring your JDK's **cacerts** keystore contains hello correct CA certificate, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="ff8c8-158">Gedetailleerde instructies voor het gebruik van Hallo Twilio-clientbibliotheek voor Java zijn beschikbaar op [hoe tooMake een telefonische oproep met behulp van Twilio in een Java-toepassing in Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-158">Detailed instructions for using hello Twilio client library for Java are available at [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="ff8c8-159"><a id="configure_app"></a>Configureren van uw toepassing tooUse Twilio-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="ff8c8-159"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="ff8c8-160">U kunt binnen uw code toevoegen **importeren** instructies Hallo boven aan de bronbestanden voor Hallo Twilio-pakketten of u klassen wilt toouse in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-160">Within your code, you can add **import** statements at hello top of your source files for hello Twilio packages or classes you want toouse in your application.</span></span>

<span data-ttu-id="ff8c8-161">Voor Java-bronbestanden:</span><span class="sxs-lookup"><span data-stu-id="ff8c8-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="ff8c8-162">Voor de bronbestanden van de pagina voor Java-Server (JSP):</span><span class="sxs-lookup"><span data-stu-id="ff8c8-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="ff8c8-163">Afhankelijk van welke Twilio-pakketten of klassen die u wilt toouse, uw **importeren** instructies kunnen afwijken.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-163">Depending on which Twilio packages or classes you want toouse, your **import** statements may be different.</span></span>

## <span data-ttu-id="ff8c8-164"><a id="howto_make_call"></a>Procedure: een uitgaande aanroep</span><span class="sxs-lookup"><span data-stu-id="ff8c8-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="ff8c8-165">Hallo hieronder ziet u hoe een uitgaande toomake-gesprek Hallo **aanroepen** klasse.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-165">hello following shows how toomake an outgoing call using hello **Call** class.</span></span> <span data-ttu-id="ff8c8-166">Deze code wordt een Twilio-voorwaarde site tooreturn hello Twilio Markup Language (TwiML) antwoord.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-166">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="ff8c8-167">Vervang uw waarden voor Hallo **van** en **naar** telefoonnummers, en zorg ervoor dat u controleert of Hallo **van** telefoonnummer voor uw Twilio-account voorafgaande toorunning Hallo code.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-167">Substitute your values for hello **from** and **to** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="ff8c8-168">Voor meer informatie over Hallo parameters doorgegeven toohello **Call.creator** methode, Zie [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-168">For more information about hello parameters passed in toohello **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="ff8c8-169">Zoals gezegd, gebruikt deze code een Twilio-voorwaarde site tooreturn hello TwiML antwoord.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-169">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="ff8c8-170">U kunt in plaats hiervan uw eigen site tooprovide hello TwiML antwoord; Zie voor meer informatie [hoe tooProvide TwiML antwoorden in een Java-toepassing in Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="ff8c8-170">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="ff8c8-171"><a id="howto_send_sms"></a>Procedure: een SMS-bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="ff8c8-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="ff8c8-172">Hallo hieronder ziet u hoe een SMS-bericht met toosend Hallo **bericht** klasse.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-172">hello following shows how toosend an SMS message using hello **Message** class.</span></span> <span data-ttu-id="ff8c8-173">Hallo **van** getal, **4155992671**, wordt geleverd door Twilio voor proefversie accounts toosend SMS-berichten.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-173">hello **from** number, **4155992671**, is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="ff8c8-174">Hallo **naar** nummer om uw Twilio-account voorafgaande toorunning Hallo-code moet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-174">hello **to** number must be verified for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="ff8c8-175">Voor meer informatie over Hallo parameters doorgegeven toohello **Message.creator** methode, Zie [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-175">For more information about hello parameters passed in toohello **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="ff8c8-176"><a id="howto_provide_twiml_responses"></a>Hoe: TwiML reacties van uw eigen Website opgeven</span><span class="sxs-lookup"><span data-stu-id="ff8c8-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="ff8c8-177">Wanneer uw toepassing een aanroep van toohello Twilio-API, bijvoorbeeld via Hallo initieert **CallCreator.create** methode Twilio verzendt uw aanvraag tooa-URL is de verwachte tooreturn een TwiML antwoord.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-177">When your application initiates a call toohello Twilio API, for example via hello **CallCreator.create** method, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="ff8c8-178">Hallo in bovenstaand voorbeeld gebruikt Hallo Twilio-geleverde URL [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-178">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="ff8c8-179">(Hoewel TwiML is ontworpen voor gebruik door webservices, u kunt weergeven Hallo TwiML in uw browser.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-179">(While TwiML is designed for use by Web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="ff8c8-180">Bijvoorbeeld, klik op [http://twimlets.com/message] [ twimlet_message_url] toosee een lege  **&lt;antwoord&gt;**  element; klik op alseenandervoorbeeld:[http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee een  **&lt;antwoord&gt;**  element met een  **&lt;Zeg &gt;**  element.)</span><span class="sxs-lookup"><span data-stu-id="ff8c8-180">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] toosee a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="ff8c8-181">In plaats van te vertrouwen op Hallo geleverde Twilio-URL, kunt u uw eigen website URL waarmee HTTP-antwoorden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-181">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="ff8c8-182">U kunt Hallo-site maken in een andere taal waarmee HTTP-antwoorden; in dit onderwerp wordt ervan uitgegaan dat u gaat hosten Hallo-URL in een JSP-pagina.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-182">You can create hello site in any language that returns HTTP responses; this topic assumes you'll be hosting hello URL in a JSP page.</span></span>

<span data-ttu-id="ff8c8-183">Hallo JSP pagina resultaten in een antwoord TwiML waarin staat dat na **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="ff8c8-183">hello following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="ff8c8-184">op het Hallo-aanroep.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-184">on hello call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="ff8c8-185">Hallo volgende JSP pagina resulteert in een TwiML-antwoord dat wat tekst vertelt heeft verschillende gepauzeerd en staat informatie over Hallo Twilio-API-versie en hello Azure role-naam.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-185">hello following JSP page results in a TwiML response that says some text, has several pauses, and says information about hello Twilio API version and hello Azure role name.</span></span>

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

<span data-ttu-id="ff8c8-186">Hallo **ApiVersion** parameter is beschikbaar in Twilio voice-aanvragen (geen SMS-aanvragen).</span><span class="sxs-lookup"><span data-stu-id="ff8c8-186">hello **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="ff8c8-187">toosee hello beschikbaar aanvraagparameters voor spraak Twilio- en SMS-aanvragen, Zie <https://www.twilio.com/docs/api/twiml/twilio_request> en <https://www.twilio.com/docs/api/twiml/sms/twilio_request >respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-187">toosee hello available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="ff8c8-188">Hallo **RoleName** omgevingsvariabele is beschikbaar als onderdeel van een Azure-implementatie.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-188">hello **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="ff8c8-189">(Als u wilt dat de aangepaste omgevingsvariabelen tooadd zodat deze kunnen worden opgehaald uit **System.getenv**, Zie Hallo omgeving variabelen sectie op [configuratie-instellingen van diverse rol] [misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="ff8c8-189">(If you want tooadd custom environment variables so they could be picked up from **System.getenv**, see hello environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="ff8c8-190">Zodra u uw JSP-pagina tooprovide TwiML antwoorden instellen hebt, Hallo-URL van Hallo JSP-pagina gebruiken als de URL die wordt doorgegeven in Hallo Hallo **Call.creator** methode.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-190">Once you have your JSP page set up tooprovide TwiML responses, use hello URL of hello JSP page as hello URL passed into hello **Call.creator** method.</span></span> <span data-ttu-id="ff8c8-191">Bijvoorbeeld, als u een webtoepassing hebt met de naam MyTwiML geïmplementeerd tooan Azure gehoste service, en Hallo-naam van Hallo JSP pagina mytwiml.jsp, Hallo-URL te kan worden doorgegeven**Call.creator** zoals weergegeven in de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="ff8c8-191">For example, if you have a Web application named MyTwiML deployed tooan Azure hosted service, and hello name of hello JSP page is mytwiml.jsp, hello URL can be passed too**Call.creator** as shown in hello following:</span></span>

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="ff8c8-192">Er is een andere optie voor het beantwoorden van TwiML via Hallo **VoiceResponse** klasse, die beschikbaar in Hallo is **com.twilio.twiml** pakket.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-192">Another option for responding with TwiML is via hello **VoiceResponse** class, which is available in hello **com.twilio.twiml** package.</span></span>

<span data-ttu-id="ff8c8-193">Zie voor meer informatie over het gebruik van Twilio in Azure met Java [hoe tooMake een telefonische oproep met behulp van Twilio in een Java-toepassing in Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-193">For additional information about using Twilio in Azure with Java, see [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="ff8c8-194"><a id="AdditionalServices"></a>How to: extra Twilio-Services gebruiken</span><span class="sxs-lookup"><span data-stu-id="ff8c8-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="ff8c8-195">Bovendien kunt toohello voorbeelden die hier worden weergegeven, dat twilio biedt op basis van een web-API's u tooleverage aanvullende Twilio-functionaliteit van uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ff8c8-195">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="ff8c8-196">Zie voor meer details Hallo [Twilio-API-documentatie][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="ff8c8-196">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="ff8c8-197"><a id="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff8c8-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="ff8c8-198">Nu u basisprincipes Hallo Hallo Twilio-service hebt geleerd, volgt u deze koppelingen toolearn meer:</span><span class="sxs-lookup"><span data-stu-id="ff8c8-198">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="ff8c8-199">[Richtlijnen voor Twilio-beveiliging][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="ff8c8-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="ff8c8-200">[Van de procedure Twilio en voorbeeldcode][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="ff8c8-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="ff8c8-201">[Twilio Quick Start-zelfstudie][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="ff8c8-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="ff8c8-202">[Twilio op GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="ff8c8-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="ff8c8-203">[Neem contact tooTwilio ondersteuning][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="ff8c8-203">[Talk tooTwilio Support][twilio_support]</span></span>

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
