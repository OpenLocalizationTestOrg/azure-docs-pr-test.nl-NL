---
title: Het gebruik van Twilio voor spraak- en SMS (PHP) | Microsoft Docs
description: Informatie over het maken van een telefonische oproep en verzenden van een SMS-bericht met de Twilio-API-service op Azure. Codevoorbeelden geschreven in PHP.
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
ms.openlocfilehash: bd50eac7390e8639f77894689388e6926cdb619c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="6bdb1-104">Het gebruik van Twilio voor spraak- en SMS-mogelijkheden van PHP</span><span class="sxs-lookup"><span data-stu-id="6bdb1-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="6bdb1-105">Deze handleiding wordt uitgelegd hoe algemene programmeertaken met de Twilio-API-service uitvoeren op Azure.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="6bdb1-106">De scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="6bdb1-107">Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen de [Vervolgstappen](#NextSteps) sectie.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="6bdb1-108"><a id="WhatIs"></a>Wat is Twilio?</span><span class="sxs-lookup"><span data-stu-id="6bdb1-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="6bdb1-109">Twilio is dat de toekomstige zakelijke communicatie, waarmee ontwikkelaars voor het insluiten van spraak, VoIP en messaging in toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="6bdb1-110">Ze virtualiseren alle infrastructuur die nodig is in een cloud-gebaseerde, globale-omgeving, beschikbaar te maken via de Twilio-communicatieplatform API.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="6bdb1-111">Toepassingen zijn eenvoudig te maken en schaalbare.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="6bdb1-112">Profiteer van flexibiliteit met pay-as-you gaat prijzen en profiteren van de betrouwbaarheid van de cloud.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="6bdb1-113">**Twilio stem** zorgt ervoor dat uw toepassingen en telefoongesprekken ontvangen.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="6bdb1-114">**Twilio SMS** kan uw toepassing te verzenden en ontvangen van de SMS-berichten.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-114">**Twilio SMS** enables your application to send and receive text messages.</span></span> <span data-ttu-id="6bdb1-115">**Twilio Client** kunt u VoIP-aanroepen van elke telefoon, tablet of browser en WebRTC ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="6bdb1-116"><a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="6bdb1-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="6bdb1-117">Azure-klanten ontvangen een [speciale aanbieding](http://www.twilio.com/azure): gratis $10 Twilio tegoed wanneer u een upgrade uitvoert van uw Twilio-Account.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="6bdb1-118">Deze Twilio-tegoed kan worden toegepast op alle Twilio-gebruik ($10 credit gelijk is aan maximaal 1000 SMS-berichten verzenden of ontvangen van maximaal 1000 inkomende Voice-minuten, afhankelijk van de locatie van uw telefoon en bericht- of aanroep doel).</span><span class="sxs-lookup"><span data-stu-id="6bdb1-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="6bdb1-119">Deze Twilio-tegoed inwisselen en aan de slag op: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="6bdb1-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="6bdb1-120">Twilio is een betalen naar gebruik service.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="6bdb1-121">Er zijn geen kosten instellen en kunt u uw account op elk moment sluiten.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="6bdb1-122">U vindt meer informatie op [Twilio prijzen][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="6bdb1-123"><a id="Concepts"></a>Concepten</span><span class="sxs-lookup"><span data-stu-id="6bdb1-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="6bdb1-124">De Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="6bdb1-125">Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="6bdb1-126">Belangrijke aspecten van de API Twilio zijn Twilio-termen en Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="6bdb1-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="6bdb1-127"><a id="Verbs"></a>Twilio-termen</span><span class="sxs-lookup"><span data-stu-id="6bdb1-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="6bdb1-128">De API wordt gebruikgemaakt van Twilio termen; bijvoorbeeld, de  **&lt;zeg&gt;**  term geeft Twilio hoorbaar een bericht te bezorgen in een aanroep van de opdracht.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="6bdb1-129">Hier volgt een lijst met Twilio-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="6bdb1-130">Meer informatie over de andere termen en mogelijkheden via [Twilio Markup Language documentatie](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="6bdb1-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="6bdb1-131">**&lt;Externe&gt;**: de aanroeper verbindt met een andere telefoon.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="6bdb1-132">**&lt;Verzamel&gt;**: verzamelt cijfers ingevoerd op de toetsenblok van de telefoon.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="6bdb1-133">**&lt;Ophangen&gt;**: een aanroep wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="6bdb1-134">**&lt;Afspelen&gt;**: een geluidsbestand afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="6bdb1-135">**&lt;Onderbreken&gt;**: achtergrond wacht op een opgegeven aantal seconden.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="6bdb1-136">**&lt;Record&gt;**: van de aanroeper stem registreert en retourneert een URL van een bestand dat de opname bevat.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="6bdb1-137">**&lt;Omleiden&gt;**: beheer van een telefoongesprek of SMS overgebracht naar de TwiML op een andere URL.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="6bdb1-138">**&lt;Afwijzen&gt;**: een inkomend gesprek naar het nummer van uw Twilio verwerpt zonder u facturering</span><span class="sxs-lookup"><span data-stu-id="6bdb1-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="6bdb1-139">**&lt;Zeg&gt;**: zet tekst-naar-spraak die wordt gemaakt op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="6bdb1-140">**&lt;SMS&gt;**: een SMS-bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="6bdb1-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="6bdb1-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="6bdb1-142">TwiML is een set op basis van de Twilio-termen die informeren Twilio van het verwerken van een aanroep of SMS op basis van een XML-instructies.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="6bdb1-143">Als u bijvoorbeeld de volgende TwiML tekst wilt converteren **Hallo wereld** spraak.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="6bdb1-144">Wanneer uw toepassing de Twilio-API aanroept, is een van de API-parameters de URL die de TwiML-antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="6bdb1-145">Voor ontwikkelingsdoeleinden, kunt u geleverde Twilio-URL's voor de TwiML-antwoorden die wordt gebruikt door uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="6bdb1-146">U ook uw eigen URL's om te produceren de antwoorden TwiML kan hosten en een andere optie is met de **TwiMLResponse** object.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="6bdb1-147">Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="6bdb1-148">Zie voor meer informatie over de API Twilio [Twilio-API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="6bdb1-149"><a id="CreateAccount"></a>Een Twilio-Account maken</span><span class="sxs-lookup"><span data-stu-id="6bdb1-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="6bdb1-150">Wanneer u klaar bent om op te halen van een Twilio-account, aanmelden op [probeer Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="6bdb1-151">U kunt beginnen met een gratis account en upgrade van uw account later.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="6bdb1-152">Wanneer u zich voor een Twilio-account aanmeldt, ontvangt u een account-ID en geen verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="6bdb1-153">Beide moest u Twilio-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="6bdb1-154">Om te voorkomen dat onbevoegde toegang tot je account, uw verificatietoken veilig houden.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="6bdb1-155">Uw account-ID en verificatie token kunnen worden bekeken op de [Twilio-accountpagina][twilio_account], in de velden met het label **ACCOUNT-SID** en **AUTH TOKEN**respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="6bdb1-156"><a id="create_app"></a>Een PHP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="6bdb1-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="6bdb1-157">Een PHP-toepassing die gebruikmaakt van de Twilio-service en wordt uitgevoerd in Azure gaat niet anders dan de andere PHP-toepassing die gebruikmaakt van de Twilio-service.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span></span> <span data-ttu-id="6bdb1-158">Terwijl Twilio-services op basis van REST worden en op verschillende manieren kunnen worden aangeroepen vanuit PHP, in dit artikel wordt de nadruk gelegd op het gebruik van services met Twilio [Twilio-bibliotheek voor PHP vanuit GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="6bdb1-159">Zie voor meer informatie over het gebruik van de Twilio-bibliotheek voor PHP [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="6bdb1-160">Gedetailleerde instructies voor het bouwen en implementeren van een Twilio/PHP-toepassing naar Azure zijn beschikbaar op [een telefonische oproep met behulp van Twilio in een PHP-toepassing in Azure maken][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="6bdb1-161"><a id="configure_app"></a>Uw toepassing configureren voor gebruik Twilio-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="6bdb1-161"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="6bdb1-162">U kunt uw toepassing configureren voor gebruik van de Twilio-bibliotheek voor PHP op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="6bdb1-162">You can configure your application to use the Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="6bdb1-163">De Twilio-bibliotheek voor PHP vanuit GitHub downloaden ([https://github.com/twilio/twilio-php][twilio_php]) en voeg de **Services** map voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span></span>
   
    <span data-ttu-id="6bdb1-164">OF</span><span class="sxs-lookup"><span data-stu-id="6bdb1-164">-OR-</span></span>
2. <span data-ttu-id="6bdb1-165">De Twilio-bibliotheek voor PHP installeren als een PEER-pakket.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-165">Install the Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="6bdb1-166">Het kan worden geïnstalleerd met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="6bdb1-166">It can be installed with the following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="6bdb1-167">Nadat u de Twilio-bibliotheek voor PHP hebt geïnstalleerd, kunt u vervolgens toevoegen een **require_once** instructie aan de bovenkant van uw PHP-bestanden om te verwijzen naar de bibliotheek:</span><span class="sxs-lookup"><span data-stu-id="6bdb1-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="6bdb1-168">Zie voor meer informatie [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="6bdb1-169"><a id="howto_make_call"></a>Procedure: een uitgaande aanroep</span><span class="sxs-lookup"><span data-stu-id="6bdb1-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="6bdb1-170">De volgende laat zien hoe u een uitgaande aanroepen met behulp van de **Services_Twilio** klasse.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span></span> <span data-ttu-id="6bdb1-171">Deze code gebruikt ook een Twilio-voorwaarde site om de Twilio Markup Language (TwiML) antwoord retourneren.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="6bdb1-172">Vervang uw waarden voor de **van** en **naar** telefoonnummers, en zorg ervoor dat u controleert of de **van** telefoonnummer voor uw Twilio-account voordat u de code uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // The number of the phone initiating the the call.
    $from_number = "NNNNNNNNNNN";

    // The number of the phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use the Twilio-provided site for the TwiML response.
    $url = "http://twimlets.com/message";

    // The phone message text.
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make the call.
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

<span data-ttu-id="6bdb1-173">Zoals gezegd, gebruikt deze code een geleverde Twilio-site om te retourneren van het antwoord TwiML.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="6bdb1-174">U kunt uw eigen website in plaats daarvan voor het antwoord TwiML; Zie voor meer informatie [hoe bieden TwiML antwoorden vanaf uw eigen website](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="6bdb1-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="6bdb1-175">**Opmerking**: om op te lossen validatiefouten voor SSL-certificaat, Zie [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="6bdb1-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="6bdb1-176"><a id="howto_send_sms"></a>Procedure: een SMS-bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="6bdb1-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="6bdb1-177">Hieronder vindt u het verzenden van een SMS-bericht met de **Services_Twilio** klasse.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span></span> <span data-ttu-id="6bdb1-178">De **van** nummer wordt geleverd door Twilio voor proefaccounts SMS-berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="6bdb1-179">De **naar** nummer moet worden geverifieerd voor uw Twilio-account voordat u de code uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-179">The **To** number must be verified for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send the SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="6bdb1-180"><a id="howto_provide_twiml_responses"></a>Hoe: TwiML reacties van uw eigen Website opgeven</span><span class="sxs-lookup"><span data-stu-id="6bdb1-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="6bdb1-181">Wanneer uw toepassing een aanroep van de Twilio-API initieert, stuurt Twilio uw aanvraag voor een URL die wordt verwacht dat een antwoord TwiML retourneren.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="6bdb1-182">Het bovenstaande voorbeeld gebruikt de URL opgegeven Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="6bdb1-183">(Hoewel TwiML is ontworpen voor gebruik door Twilio, ziet u de it in uw browser.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span></span> <span data-ttu-id="6bdb1-184">Bijvoorbeeld, klik op [http://twimlets.com/message] [ twimlet_message_url] om te zien van een lege `<Response>` element; Klik bijvoorbeeld op [http://twimlets.com/message? Bericht % 5B0 %5, D = Hallo % 20World] [ twimlet_message_url_hello_world] om te zien een `<Response>` element met een `<Say>` element.)</span><span class="sxs-lookup"><span data-stu-id="6bdb1-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="6bdb1-185">In plaats van te vertrouwen op de opgegeven Twilio-URL, kunt u uw eigen website waarmee HTTP-antwoorden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="6bdb1-186">U kunt de site maken in een andere taal die als resultaat geeft de XML-reacties; in dit onderwerp wordt ervan uitgegaan dat u PHP wilt gebruiken voor het maken van de TwiML.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span></span>

<span data-ttu-id="6bdb1-187">De volgende pagina van de PHP resulteert in een antwoord TwiML waarin staat dat **Hallo wereld** bij het aanroepen van.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="6bdb1-188">Zoals u in het bovenstaande voorbeeld zien kunt, is het antwoord TwiML gewoon een XML-document.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-188">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="6bdb1-189">De Twilio-bibliotheek voor PHP bevat klassen die voor u TwiML genereren.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="6bdb1-190">Het onderstaande voorbeeld de equivalente reactie produceert, zoals hierboven, maar gebruikt de **Services\_Twilio\_Twiml** klasse in de bibliotheek Twilio voor PHP:</span><span class="sxs-lookup"><span data-stu-id="6bdb1-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="6bdb1-191">Zie voor meer informatie over TwiML [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="6bdb1-192">Zodra u uw PHP-pagina instellen op TwiML geven hebt, gebruikt u de URL van de PHP-pagina als de URL die wordt doorgegeven in de `Services_Twilio->account->calls->create` methode.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="6bdb1-193">Bijvoorbeeld, als u een webtoepassing met de naam hebt **MyTwiML** geïmplementeerd voor een Azure gehoste service en de naam van de PHP-pagina is **mytwiml.php**, de URL kan worden doorgegeven aan **Services_Twilio -> account-aanroepen > -> maken** zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6bdb1-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // The phone message text.
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

<span data-ttu-id="6bdb1-194">Zie voor meer informatie over het gebruik van Twilio in Azure met PHP [een telefonische oproep met behulp van Twilio in een PHP-toepassing in Azure maken][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="6bdb1-195"><a id="AdditionalServices"></a>How to: extra Twilio-Services gebruiken</span><span class="sxs-lookup"><span data-stu-id="6bdb1-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="6bdb1-196">Naast de voorbeelden die hier worden weergegeven, biedt Twilio web-API's waarmee u kunt gebruikmaken van aanvullende Twilio-functionaliteit van uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6bdb1-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="6bdb1-197">Zie voor meer informatie de [Twilio-API-documentatie][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="6bdb1-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="6bdb1-198"><a id="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bdb1-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="6bdb1-199">Nu u de basisprincipes van de Twilio-service hebt geleerd, volgt u deze koppelingen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="6bdb1-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="6bdb1-200">[Richtlijnen voor Twilio-beveiliging][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="6bdb1-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="6bdb1-201">[Van de procedure Twilio en voorbeeldcode][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="6bdb1-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="6bdb1-202">[Twilio Quick Start-zelfstudie][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="6bdb1-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="6bdb1-203">[Twilio op GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="6bdb1-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="6bdb1-204">[Neem contact op met Twilio-ondersteuning][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="6bdb1-204">[Talk to Twilio Support][twilio_support]</span></span>

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
