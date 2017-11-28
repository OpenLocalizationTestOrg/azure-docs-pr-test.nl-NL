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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="e9643-104">Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden van PHP</span><span class="sxs-lookup"><span data-stu-id="e9643-104">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="e9643-105">Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello Twilio-API-service op Azure.</span><span class="sxs-lookup"><span data-stu-id="e9643-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="e9643-106">Hallo scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden.</span><span class="sxs-lookup"><span data-stu-id="e9643-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="e9643-107">Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen Hallo [Vervolgstappen](#NextSteps) sectie.</span><span class="sxs-lookup"><span data-stu-id="e9643-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="e9643-108"><a id="WhatIs"></a>Wat is Twilio?</span><span class="sxs-lookup"><span data-stu-id="e9643-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="e9643-109">Twilio is dat toekomstige Hallo zakelijke communicatie, ontwikkelaars tooembed spraak, VoIP, inschakelen en messaging in toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e9643-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="e9643-110">Ze virtualiseren alle infrastructuur die nodig is in een cloud-gebaseerde, globale-omgeving, beschikbaar te maken via Hallo Twilio communications API-platform.</span><span class="sxs-lookup"><span data-stu-id="e9643-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="e9643-111">Toepassingen zijn eenvoudige toobuild en schaalbare.</span><span class="sxs-lookup"><span data-stu-id="e9643-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="e9643-112">Profiteer van flexibiliteit met pay-as-you gaat prijzen en profiteren van de betrouwbaarheid van de cloud.</span><span class="sxs-lookup"><span data-stu-id="e9643-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="e9643-113">**Twilio stem** kunt u uw toepassingen toomake en gebeld.</span><span class="sxs-lookup"><span data-stu-id="e9643-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="e9643-114">**Twilio SMS** kunt u uw toepassing toosend tekstberichten en ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e9643-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span> <span data-ttu-id="e9643-115">**Twilio Client** kunt u toomake VoIP-aanroepen vanuit een telefoon, tablet of een browser en WebRTC ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="e9643-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="e9643-116"><a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="e9643-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="e9643-117">Azure-klanten ontvangen een [speciale aanbieding](http://www.twilio.com/azure): gratis $10 Twilio tegoed wanneer u een upgrade uitvoert van uw Twilio-Account.</span><span class="sxs-lookup"><span data-stu-id="e9643-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="e9643-118">Deze Twilio-tegoed kan worden toegepast tooany Twilio-gebruik ($10 tegoed gelijkwaardige toosending maximaal 1000 SMS-berichten of ontvangst van too1000 inkomende stem minuten, afhankelijk van de locatie van uw telefoon en bericht- of aanroep bestemming Hallo).</span><span class="sxs-lookup"><span data-stu-id="e9643-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="e9643-119">Deze Twilio-tegoed inwisselen en aan de slag op: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="e9643-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="e9643-120">Twilio is een betalen naar gebruik service.</span><span class="sxs-lookup"><span data-stu-id="e9643-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="e9643-121">Er zijn geen kosten instellen en kunt u uw account op elk moment sluiten.</span><span class="sxs-lookup"><span data-stu-id="e9643-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="e9643-122">U vindt meer informatie op [Twilio prijzen][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="e9643-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="e9643-123"><a id="Concepts"></a>Concepten</span><span class="sxs-lookup"><span data-stu-id="e9643-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="e9643-124">Hallo Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e9643-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="e9643-125">Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="e9643-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="e9643-126">Belangrijke aspecten van Hallo Twilio-API zijn Twilio-termen en Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="e9643-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="e9643-127"><a id="Verbs"></a>Twilio-termen</span><span class="sxs-lookup"><span data-stu-id="e9643-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="e9643-128">Hallo API wordt gebruikgemaakt van Twilio termen; bijvoorbeeld, Hallo  **&lt;zeg&gt;**  term Hiermee Twilio tooaudibly afleveren geeft een bericht op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="e9643-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="e9643-129">Hallo Hieronder volgt een lijst met Twilio-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="e9643-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="e9643-130">Meer informatie over Hallo andere termen en mogelijkheden via [Twilio Markup Language documentatie](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="e9643-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="e9643-131">**&lt;Externe&gt;**: Hallo aanroeper tooanother telefoon verbindt.</span><span class="sxs-lookup"><span data-stu-id="e9643-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="e9643-132">**&lt;Verzamel&gt;**: cijfers ingevoerd op het telefoonnummer Hallo verzamelt.</span><span class="sxs-lookup"><span data-stu-id="e9643-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="e9643-133">**&lt;Ophangen&gt;**: een aanroep wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="e9643-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="e9643-134">**&lt;Afspelen&gt;**: een geluidsbestand afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="e9643-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="e9643-135">**&lt;Onderbreken&gt;**: achtergrond wacht op een opgegeven aantal seconden.</span><span class="sxs-lookup"><span data-stu-id="e9643-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="e9643-136">**&lt;Record&gt;**: Hallo aanroeper stem registreert en retourneert een URL van een bestand dat Hallo opname bevat.</span><span class="sxs-lookup"><span data-stu-id="e9643-136">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="e9643-137">**&lt;Omleiden&gt;**: draagt de controle van een telefoongesprek of SMS toohello TwiML op een andere URL.</span><span class="sxs-lookup"><span data-stu-id="e9643-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="e9643-138">**&lt;Afwijzen&gt;**: geweigerd een binnenkomende tooyour Twilio nummer bellen zonder u facturering</span><span class="sxs-lookup"><span data-stu-id="e9643-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="e9643-139">**&lt;Zeg&gt;**: zet tekst toospeech die wordt gemaakt op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="e9643-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="e9643-140">**&lt;SMS&gt;**: een SMS-bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="e9643-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="e9643-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="e9643-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="e9643-142">TwiML is een reeks XML gebaseerde instructies op basis van Hallo Twilio-termen die Twilio van hoe u informeren over tooprocess een telefoongesprek of SMS.</span><span class="sxs-lookup"><span data-stu-id="e9643-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="e9643-143">Als u bijvoorbeeld Hallo TwiML na Hallo tekst wilt converteren **Hallo wereld** toospeech.</span><span class="sxs-lookup"><span data-stu-id="e9643-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="e9643-144">Bij het aanroepen van uw toepassing hello Twilio-API, is een van de API-parameters Hallo Hallo-URL die Hallo TwiML antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e9643-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="e9643-145">U kunt voor ontwikkelingsdoeleinden Twilio geleverde URL's tooprovide hello TwiML antwoorden die wordt gebruikt door uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e9643-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="e9643-146">U ook uw eigen URL's tooproduce hello TwiML reacties kan hosten en een andere optie is toouse hello **TwiMLResponse** object.</span><span class="sxs-lookup"><span data-stu-id="e9643-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="e9643-147">Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="e9643-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="e9643-148">Zie voor meer informatie over Hallo Twilio-API, [Twilio-API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="e9643-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="e9643-149"><a id="CreateAccount"></a>Een Twilio-Account maken</span><span class="sxs-lookup"><span data-stu-id="e9643-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="e9643-150">Wanneer u klaar tooget een Twilio-account bent, aanmelden op [probeer Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="e9643-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="e9643-151">U kunt beginnen met een gratis account en upgrade van uw account later.</span><span class="sxs-lookup"><span data-stu-id="e9643-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="e9643-152">Wanneer u zich voor een Twilio-account aanmeldt, ontvangt u een account-ID en geen verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="e9643-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="e9643-153">Beide worden benodigde toomake Twilio-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e9643-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="e9643-154">tooprevent onbevoegde toegang tot tooyour account, het verificatietoken te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="e9643-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="e9643-155">Uw account-ID en verificatie token kunnen worden bekeken op Hallo [Twilio-accountpagina][twilio_account]in velden met het label Hallo **ACCOUNT-SID** en **AUTH TOKEN**respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="e9643-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="e9643-156"><a id="create_app"></a>Een PHP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="e9643-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="e9643-157">Een PHP-toepassing die gebruikmaakt van Hallo Twilio-service en wordt uitgevoerd in Azure gaat niet anders dan de andere PHP-toepassing die gebruikmaakt van Hallo Twilio-service.</span><span class="sxs-lookup"><span data-stu-id="e9643-157">A PHP application that uses hello Twilio service and is running in Azure is no different than any other PHP application that uses hello Twilio service.</span></span> <span data-ttu-id="e9643-158">Terwijl Twilio-services op basis van REST worden en op verschillende manieren kunnen worden aangeroepen vanuit PHP, in dit artikel wordt de nadruk gelegd op hoe toouse Twilio services met [Twilio-bibliotheek voor PHP vanuit GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="e9643-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how toouse Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="e9643-159">Zie voor meer informatie over het gebruik van Hallo Twilio-bibliotheek voor PHP [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="e9643-159">For more information about using hello Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="e9643-160">Gedetailleerde instructies voor het bouwen en implementeren van een toepassing Twilio/PHP tooAzure zijn beschikbaar op [hoe tooMake een telefonische oproep met behulp van Twilio in een PHP-toepassing in Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="e9643-160">Detailed instructions for building and deploying a Twilio/PHP application tooAzure are available at [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="e9643-161"><a id="configure_app"></a>Configureren van uw toepassing tooUse Twilio-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="e9643-161"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="e9643-162">U kunt uw toepassing toouse hello Twilio-bibliotheek configureren voor PHP op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="e9643-162">You can configure your application toouse hello Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="e9643-163">Hallo Twilio-bibliotheek voor PHP vanuit GitHub downloaden ([https://github.com/twilio/twilio-php][twilio_php]) en voeg Hallo **Services** directory tooyour-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e9643-163">Download hello Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add hello **Services** directory tooyour application.</span></span>
   
    <span data-ttu-id="e9643-164">OF</span><span class="sxs-lookup"><span data-stu-id="e9643-164">-OR-</span></span>
2. <span data-ttu-id="e9643-165">Hallo Twilio-bibliotheek voor PHP installeren als een PEER-pakket.</span><span class="sxs-lookup"><span data-stu-id="e9643-165">Install hello Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="e9643-166">Het kan worden geïnstalleerd met Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="e9643-166">It can be installed with hello following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="e9643-167">Zodra u Hallo Twilio-bibliotheek voor PHP hebt geïnstalleerd, kunt u vervolgens toevoegen een **require_once** instructie Hallo boven aan uw PHP-bestanden tooreference Hallo bibliotheek:</span><span class="sxs-lookup"><span data-stu-id="e9643-167">Once you have installed hello Twilio library for PHP, you can then add a **require_once** statement at hello top of your PHP files tooreference hello library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="e9643-168">Zie voor meer informatie [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="e9643-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="e9643-169"><a id="howto_make_call"></a>Procedure: een uitgaande aanroep</span><span class="sxs-lookup"><span data-stu-id="e9643-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="e9643-170">Hallo hieronder ziet u hoe een uitgaande toomake-gesprek Hallo **Services_Twilio** klasse.</span><span class="sxs-lookup"><span data-stu-id="e9643-170">hello following shows how toomake an outgoing call using hello **Services_Twilio** class.</span></span> <span data-ttu-id="e9643-171">Deze code wordt een Twilio-voorwaarde site tooreturn hello Twilio Markup Language (TwiML) antwoord.</span><span class="sxs-lookup"><span data-stu-id="e9643-171">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="e9643-172">Vervang uw waarden voor Hallo **van** en **naar** telefoonnummers, en zorg ervoor dat u controleert of Hallo **van** telefoonnummer voor uw Twilio-account voorafgaande toorunning Hallo code.</span><span class="sxs-lookup"><span data-stu-id="e9643-172">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="e9643-173">Zoals gezegd, gebruikt deze code een Twilio-voorwaarde site tooreturn hello TwiML antwoord.</span><span class="sxs-lookup"><span data-stu-id="e9643-173">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="e9643-174">U kunt in plaats hiervan uw eigen site tooprovide hello TwiML antwoord; Zie voor meer informatie [hoe tooProvide TwiML antwoorden vanaf uw eigen website](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="e9643-174">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="e9643-175">**Opmerking**: validatiefouten voor tootroubleshoot SSL-certificaat, Zie [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="e9643-175">**Note**: tootroubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="e9643-176"><a id="howto_send_sms"></a>Procedure: een SMS-bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="e9643-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="e9643-177">Hallo hieronder ziet u hoe een SMS-bericht met toosend Hallo **Services_Twilio** klasse.</span><span class="sxs-lookup"><span data-stu-id="e9643-177">hello following shows how toosend an SMS message using hello **Services_Twilio** class.</span></span> <span data-ttu-id="e9643-178">Hallo **van** nummer wordt geleverd door Twilio voor proefversie accounts toosend SMS-berichten.</span><span class="sxs-lookup"><span data-stu-id="e9643-178">hello **From** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="e9643-179">Hallo **naar** nummer om uw Twilio-account voorafgaande toorunning Hallo-code moet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="e9643-179">hello **To** number must be verified for your Twilio account prior toorunning hello code.</span></span>

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

## <span data-ttu-id="e9643-180"><a id="howto_provide_twiml_responses"></a>Hoe: TwiML reacties van uw eigen Website opgeven</span><span class="sxs-lookup"><span data-stu-id="e9643-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="e9643-181">Wanneer uw toepassing een aanroep van toohello Twilio-API initieert, stuurt Twilio uw aanvraag tooa-URL die wordt verwacht tooreturn TwiML antwoord.</span><span class="sxs-lookup"><span data-stu-id="e9643-181">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="e9643-182">Hallo in bovenstaand voorbeeld gebruikt Hallo Twilio-geleverde URL [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="e9643-182">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="e9643-183">(Hoewel TwiML is ontworpen voor gebruik door Twilio, vindt u het Hallo in uw browser.</span><span class="sxs-lookup"><span data-stu-id="e9643-183">(While TwiML is designed for use by Twilio, you can view hello it in your browser.</span></span> <span data-ttu-id="e9643-184">Bijvoorbeeld, klik op [http://twimlets.com/message] [ twimlet_message_url] toosee een lege `<Response>` element; Klik bijvoorbeeld op [http://twimlets.com/message? Bericht % 5B0 %5, D = Hallo % 20World] [ twimlet_message_url_hello_world] toosee een `<Response>` element met een `<Say>` element.)</span><span class="sxs-lookup"><span data-stu-id="e9643-184">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="e9643-185">In plaats van te vertrouwen op Hallo geleverde Twilio-URL, kunt u uw eigen website waarmee HTTP-antwoorden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e9643-185">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="e9643-186">U kunt Hallo-site maken in een andere taal die als resultaat geeft de XML-reacties; in dit onderwerp wordt ervan uitgegaan dat u PHP toocreate hello TwiML wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9643-186">You can create hello site in any language that returns XML responses; this topic assumes you'll be using PHP toocreate hello TwiML.</span></span>

<span data-ttu-id="e9643-187">Hallo PHP pagina resultaten in een antwoord TwiML waarin staat dat na **Hallo wereld** op Hallo-aanroep.</span><span class="sxs-lookup"><span data-stu-id="e9643-187">hello following PHP page results in a TwiML response that says **Hello World** on hello call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="e9643-188">Zoals u in de bovenstaande Hallo voorbeeld zien kunt, is het Hallo TwiML antwoord gewoon een XML-document.</span><span class="sxs-lookup"><span data-stu-id="e9643-188">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="e9643-189">Hallo Twilio-bibliotheek voor PHP bevat klassen die voor u TwiML genereren.</span><span class="sxs-lookup"><span data-stu-id="e9643-189">hello Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="e9643-190">Hallo onderstaand voorbeeld gelijkwaardige antwoord Hallo produceert, zoals hierboven, maar gebruikt Hallo **Services\_Twilio\_Twiml** klasse in Hallo Twilio-bibliotheek voor PHP:</span><span class="sxs-lookup"><span data-stu-id="e9643-190">hello example below produces hello equivalent response as shown above, but uses hello **Services\_Twilio\_Twiml** class in hello Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="e9643-191">Zie voor meer informatie over TwiML [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="e9643-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="e9643-192">Zodra u uw PHP-pagina tooprovide TwiML antwoorden instellen hebt, Hallo-URL van Hallo PHP-pagina gebruiken als de URL die wordt doorgegeven in Hallo Hallo `Services_Twilio->account->calls->create` methode.</span><span class="sxs-lookup"><span data-stu-id="e9643-192">Once you have your PHP page set up tooprovide TwiML responses, use hello URL of hello PHP page as hello URL passed into hello  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="e9643-193">Bijvoorbeeld, als u een webtoepassing met de naam hebt **MyTwiML** geïmplementeerde tooan Azure gehoste service en het Hallo-naam van de PHP-pagina Hallo is **mytwiml.php**, Hallo URL te kan worden doorgegeven **Services_ Twilio-account > -> aanroepen -> maken** zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9643-193">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, and hello name of hello PHP page is **mytwiml.php**, hello URL can be passed too **Services_Twilio->account->calls->create**  as shown in hello following example:</span></span>

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

<span data-ttu-id="e9643-194">Zie voor meer informatie over het gebruik van Twilio in Azure met PHP [hoe tooMake een telefonische oproep met behulp van Twilio in een PHP-toepassing in Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="e9643-194">For additional information about using Twilio in Azure with PHP, see [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="e9643-195"><a id="AdditionalServices"></a>How to: extra Twilio-Services gebruiken</span><span class="sxs-lookup"><span data-stu-id="e9643-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="e9643-196">Bovendien kunt toohello voorbeelden die hier worden weergegeven, dat twilio biedt op basis van een web-API's u tooleverage aanvullende Twilio-functionaliteit van uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e9643-196">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="e9643-197">Zie voor meer details Hallo [Twilio-API-documentatie][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="e9643-197">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="e9643-198"><a id="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9643-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="e9643-199">Nu u basisprincipes Hallo Hallo Twilio-service hebt geleerd, volgt u deze koppelingen toolearn meer:</span><span class="sxs-lookup"><span data-stu-id="e9643-199">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="e9643-200">[Richtlijnen voor Twilio-beveiliging][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="e9643-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="e9643-201">[Van de procedure Twilio en voorbeeldcode][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="e9643-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="e9643-202">[Twilio Quick Start-zelfstudie][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="e9643-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="e9643-203">[Twilio op GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="e9643-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="e9643-204">[Neem contact tooTwilio ondersteuning][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="e9643-204">[Talk tooTwilio Support][twilio_support]</span></span>

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
