---
title: Het gebruik van Twilio voor spraak- en SMS (Ruby) | Microsoft Docs
description: Informatie over het maken van een telefonische oproep en verzenden van een SMS-bericht met de Twilio-API-service op Azure. Codevoorbeelden geschreven in Ruby.
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
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="0bd18-104">Het gebruik van Twilio voor spraak- en SMS-mogelijkheden in Ruby</span><span class="sxs-lookup"><span data-stu-id="0bd18-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="0bd18-105">Deze handleiding wordt uitgelegd hoe algemene programmeertaken met de Twilio-API-service uitvoeren op Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd18-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="0bd18-106">De scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden.</span><span class="sxs-lookup"><span data-stu-id="0bd18-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="0bd18-107">Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen de [Vervolgstappen](#NextSteps) sectie.</span><span class="sxs-lookup"><span data-stu-id="0bd18-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="0bd18-108"><a id="WhatIs"></a>Wat is Twilio?</span><span class="sxs-lookup"><span data-stu-id="0bd18-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="0bd18-109">Twilio is een telephony-webservice-API waarmee u uw bestaande web talen en vaardigheden gebruiken om voice en SMS-toepassingen te ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="0bd18-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="0bd18-110">Twilio is een service van derden (niet een functie van Azure en niet in een Microsoft-product).</span><span class="sxs-lookup"><span data-stu-id="0bd18-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="0bd18-111">**Twilio stem** zorgt ervoor dat uw toepassingen en telefoongesprekken ontvangen.</span><span class="sxs-lookup"><span data-stu-id="0bd18-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="0bd18-112">**Twilio SMS** zorgt ervoor dat uw toepassingen en SMS-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="0bd18-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="0bd18-113">**Twilio Client** zorgt ervoor dat uw toepassingen voice-communicatie met bestaande Internet-verbindingen, inclusief mobiele verbindingen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0bd18-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="0bd18-114"><a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="0bd18-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="0bd18-115">Informatie over prijzen voor Twilio is beschikbaar op [Twilio prijzen][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="0bd18-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="0bd18-116">Azure-klanten ontvangen een [speciale aanbieding][special_offer]: een gratis tegoed van 1000 teksten of 1000 inkomende minuten.</span><span class="sxs-lookup"><span data-stu-id="0bd18-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="0bd18-117">Als u zich aanmelden voor deze aanbieding of meer informatie, gaat u naar [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="0bd18-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="0bd18-118"><a id="Concepts"></a>Concepten</span><span class="sxs-lookup"><span data-stu-id="0bd18-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="0bd18-119">De Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0bd18-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="0bd18-120">Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="0bd18-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="0bd18-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="0bd18-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="0bd18-122">TwiML is een set XML-instructies die informeren Twilio van het verwerken van een aanroep of SMS-bericht.</span><span class="sxs-lookup"><span data-stu-id="0bd18-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="0bd18-123">Als u bijvoorbeeld de volgende TwiML tekst wilt converteren **Hallo wereld** spraak.</span><span class="sxs-lookup"><span data-stu-id="0bd18-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="0bd18-124">Alle TwiML documenten hebben `<Response>` als hun hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="0bd18-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="0bd18-125">Daar kunt u Twilio-woorden gebruiken om te bepalen het gedrag van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0bd18-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <span data-ttu-id="0bd18-126"><a id="Verbs"></a>TwiML termen</span><span class="sxs-lookup"><span data-stu-id="0bd18-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="0bd18-127">Twilio-bewerkingen zijn XML-labels die Twilio wat ze kunnen vertellen **doen**.</span><span class="sxs-lookup"><span data-stu-id="0bd18-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="0bd18-128">Bijvoorbeeld, de  **&lt;zeg&gt;**  term geeft Twilio hoorbaar een bericht te bezorgen in een aanroep van de opdracht.</span><span class="sxs-lookup"><span data-stu-id="0bd18-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="0bd18-129">Hier volgt een lijst met Twilio-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0bd18-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="0bd18-130">**&lt;Externe&gt;**: de aanroeper verbindt met een andere telefoon.</span><span class="sxs-lookup"><span data-stu-id="0bd18-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="0bd18-131">**&lt;Verzamel&gt;**: verzamelt cijfers ingevoerd op de toetsenblok van de telefoon.</span><span class="sxs-lookup"><span data-stu-id="0bd18-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="0bd18-132">**&lt;Ophangen&gt;**: een aanroep wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="0bd18-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="0bd18-133">**&lt;Afspelen&gt;**: een geluidsbestand afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="0bd18-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="0bd18-134">**&lt;Onderbreken&gt;**: achtergrond wacht op een opgegeven aantal seconden.</span><span class="sxs-lookup"><span data-stu-id="0bd18-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="0bd18-135">**&lt;Record&gt;**: van de aanroeper stem registreert en retourneert een URL van een bestand dat de opname bevat.</span><span class="sxs-lookup"><span data-stu-id="0bd18-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="0bd18-136">**&lt;Omleiden&gt;**: beheer van een telefoongesprek of SMS overgebracht naar de TwiML op een andere URL.</span><span class="sxs-lookup"><span data-stu-id="0bd18-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="0bd18-137">**&lt;Afwijzen&gt;**: een inkomend gesprek naar het nummer van uw Twilio verwerpt zonder u facturering</span><span class="sxs-lookup"><span data-stu-id="0bd18-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="0bd18-138">**&lt;Zeg&gt;**: zet tekst-naar-spraak die wordt gemaakt op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="0bd18-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="0bd18-139">**&lt;SMS&gt;**: een SMS-bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="0bd18-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="0bd18-140">Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="0bd18-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="0bd18-141">Zie voor meer informatie over de API Twilio [Twilio-API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="0bd18-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="0bd18-142"><a id="CreateAccount"></a>Een Twilio-Account maken</span><span class="sxs-lookup"><span data-stu-id="0bd18-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="0bd18-143">Wanneer u klaar bent om op te halen van een Twilio-account, aanmelden op [probeer Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="0bd18-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="0bd18-144">U kunt beginnen met een gratis account en upgrade van uw account later.</span><span class="sxs-lookup"><span data-stu-id="0bd18-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="0bd18-145">Wanneer u zich voor een Twilio-account aanmeldt, krijgt u een gratis telefoonnummer voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0bd18-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="0bd18-146">U ontvangt ook een SID-account en een auth-token.</span><span class="sxs-lookup"><span data-stu-id="0bd18-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="0bd18-147">Beide moest u Twilio-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="0bd18-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="0bd18-148">Om te voorkomen dat onbevoegde toegang tot je account, uw verificatietoken veilig houden.</span><span class="sxs-lookup"><span data-stu-id="0bd18-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="0bd18-149">Uw account-SID en auth token kunnen worden bekeken op de [Twilio-accountpagina][twilio_account], in de velden met het label **ACCOUNT-SID** en **AUTH TOKEN**respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="0bd18-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="0bd18-150"><a id="VerifyPhoneNumbers"></a>Controleer of de telefoonnummers</span><span class="sxs-lookup"><span data-stu-id="0bd18-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="0bd18-151">Naast het aantal krijgt u door Twilio, kunt u ook controleren of cijfers die u beheert (dat wil zeggen uw mobiele telefoon of home telefoonnummer) voor gebruik in uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0bd18-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="0bd18-152">Zie voor meer informatie over het controleren van een telefoonnummer [beheren cijfers][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="0bd18-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="0bd18-153"><a id="create_app"></a>Een Ruby-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="0bd18-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="0bd18-154">Een Ruby-toepassing die gebruikmaakt van de Twilio-service en wordt uitgevoerd in Azure gaat niet anders dan andere Ruby toepassing die gebruikmaakt van de Twilio-service.</span><span class="sxs-lookup"><span data-stu-id="0bd18-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="0bd18-155">Terwijl Twilio-services RESTful worden en op verschillende manieren kunnen worden aangeroepen vanuit Ruby, in dit artikel wordt de nadruk gelegd op het gebruik van services met Twilio [Twilio hulpbibliotheek voor Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="0bd18-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="0bd18-156">Eerst [installatie een nieuwe Azure Linux VM] [ azure_vm_setup] om te fungeren als host voor de nieuwe Ruby-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="0bd18-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="0bd18-157">De stappen met betrekking tot het maken van een app Rails, alleen installatie van de virtuele machine negeren.</span><span class="sxs-lookup"><span data-stu-id="0bd18-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="0bd18-158">Zorg ervoor dat u maakt een eindpunt met een externe poort 80 en een interne 5000-poort.</span><span class="sxs-lookup"><span data-stu-id="0bd18-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="0bd18-159">In de onderstaande voorbeelden we gebruiken [Sinatra][sinatra], een zeer eenvoudige web-framework voor Ruby.</span><span class="sxs-lookup"><span data-stu-id="0bd18-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="0bd18-160">Maar u kunt gewoon de Twilio helper-bibliotheek voor Ruby gebruiken met een andere webframework, met inbegrip van Ruby op Rails.</span><span class="sxs-lookup"><span data-stu-id="0bd18-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="0bd18-161">SSH in uw nieuwe virtuele machine en maak een map voor uw nieuwe app.</span><span class="sxs-lookup"><span data-stu-id="0bd18-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="0bd18-162">Maken van een bestand met de naam Gemfile binnen die map en kopieer de volgende code in de App:</span><span class="sxs-lookup"><span data-stu-id="0bd18-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="0bd18-163">Op de opdrachtregel uitvoeren `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="0bd18-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="0bd18-164">Hiermee installeert u de bovenstaande afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="0bd18-164">This will install the dependencies above.</span></span> <span data-ttu-id="0bd18-165">Maak vervolgens een bestand met de naam `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="0bd18-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="0bd18-166">Dit is waar de code voor uw web-app woont.</span><span class="sxs-lookup"><span data-stu-id="0bd18-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="0bd18-167">Plak de volgende code in het:</span><span class="sxs-lookup"><span data-stu-id="0bd18-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="0bd18-168">Op dit moment kunt u mogelijk de Voer de opdracht `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="0bd18-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="0bd18-169">Dit wordt spin-up een kleine webserver op poort 5000.</span><span class="sxs-lookup"><span data-stu-id="0bd18-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="0bd18-170">U moet mogelijk zijn om te bladeren naar deze app in uw browser via de URL u installeren voor uw Azure VM.</span><span class="sxs-lookup"><span data-stu-id="0bd18-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="0bd18-171">Nadat u uw web-app in de browser bereiken kunt, bent u klaar om te beginnen met het bouwen van een Twilio-app.</span><span class="sxs-lookup"><span data-stu-id="0bd18-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <span data-ttu-id="0bd18-172"><a id="configure_app"></a>Uw toepassing configureren voor gebruik Twilio</span><span class="sxs-lookup"><span data-stu-id="0bd18-172"><a id="configure_app"></a>Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="0bd18-173">U kunt uw web-app voor het gebruik van de bibliotheek Twilio door bij te werken uw `Gemfile` deze regel wilt opnemen:</span><span class="sxs-lookup"><span data-stu-id="0bd18-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="0bd18-174">Voer op de opdrachtregel `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="0bd18-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="0bd18-175">Open nu `web.rb` en deze regel boven, inclusief:</span><span class="sxs-lookup"><span data-stu-id="0bd18-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="0bd18-176">U bent nu klaar voor gebruik van de hulpbibliotheek Twilio voor Ruby in uw web-app.</span><span class="sxs-lookup"><span data-stu-id="0bd18-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="0bd18-177"><a id="howto_make_call"></a>Procedure: een uitgaande aanroep</span><span class="sxs-lookup"><span data-stu-id="0bd18-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="0bd18-178">Hieronder ziet u hoe u een uitgaande aanroep.</span><span class="sxs-lookup"><span data-stu-id="0bd18-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="0bd18-179">Belangrijkste concepten zijn met behulp van de bibliotheek Twilio helper voor Ruby REST-API-aanroepen en TwiML rendering.</span><span class="sxs-lookup"><span data-stu-id="0bd18-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="0bd18-180">Vervang uw waarden voor de **van** en **naar** telefoonnummers, en zorg ervoor dat u controleert of de **van** telefoonnummer voor uw Twilio-account voordat u de code uitvoert.</span><span class="sxs-lookup"><span data-stu-id="0bd18-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="0bd18-181">Deze functie toevoegen `web.md`:</span><span class="sxs-lookup"><span data-stu-id="0bd18-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="0bd18-182">Als de open-up `http://yourdomain.cloudapp.net/make_call` in een browser die de aanroep naar de Twilio-API van de oproep wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="0bd18-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="0bd18-183">De eerste twee parameters in `client.account.calls.create` redelijk spreken voor zich: het aantal de aanroep is `from` en het nummer van de aanroep is `to`.</span><span class="sxs-lookup"><span data-stu-id="0bd18-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="0bd18-184">De derde parameter (`url`) is de URL die Twilio-aanvragen voor instructies over wat u moet doen nadat de oproep is verbonden.</span><span class="sxs-lookup"><span data-stu-id="0bd18-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="0bd18-185">In dit geval wordt de installatie een URL (`http://yourdomain.cloudapp.net`) die een eenvoudig TwiML-document geretourneerd en gebruikt de `<Say>` term sommige spraak doen en spreek 'Hello Monkey' aan de persoon die de oproep ontvangt.</span><span class="sxs-lookup"><span data-stu-id="0bd18-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <span data-ttu-id="0bd18-186"><a id="howto_recieve_sms"></a>Procedure: een SMS-bericht ontvangen</span><span class="sxs-lookup"><span data-stu-id="0bd18-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="0bd18-187">In het vorige voorbeeld geïnitieerd we een **uitgaande** telefoongesprek.</span><span class="sxs-lookup"><span data-stu-id="0bd18-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="0bd18-188">Deze tijd, gebruiken we het telefoonnummer dat Twilio doorgegeven tijdens hebt registratie verwerken een **binnenkomende** SMS-bericht.</span><span class="sxs-lookup"><span data-stu-id="0bd18-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="0bd18-189">Eerste, aanmelding bij uw [Twilio-dashboard][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="0bd18-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="0bd18-190">Klik op 'Cijfers' in de bovenste nav en klik vervolgens op het Twilio-nummer dat u hebt opgegeven zijn.</span><span class="sxs-lookup"><span data-stu-id="0bd18-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="0bd18-191">Hier ziet u twee URL's die u kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="0bd18-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="0bd18-192">Een stem aanvraag-URL en een SMS-bericht aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="0bd18-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="0bd18-193">Dit zijn de URL's die telkens wanneer een telefonische oproep wordt gedaan of een SMS-bericht naar het nummer van uw verzonden Twilio-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="0bd18-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="0bd18-194">De URL's worden ook wel bekend als 'web hooks'.</span><span class="sxs-lookup"><span data-stu-id="0bd18-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="0bd18-195">Wij willen graag binnenkomende SMS-berichten verwerken, dus laten we werken de URL van `http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="0bd18-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="0bd18-196">Opwekken en klikt u op opslaan wijzigingen aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="0bd18-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="0bd18-197">Nu weer `web.rb` we onze toepassing voor het afhandelen van dit programma:</span><span class="sxs-lookup"><span data-stu-id="0bd18-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="0bd18-198">Zorg dat u uw web-app opnieuw te starten nadat u de wijziging.</span><span class="sxs-lookup"><span data-stu-id="0bd18-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="0bd18-199">Nu uw telefoon Elimineer en een SMS-bericht verzenden naar uw Twilio-nummer.</span><span class="sxs-lookup"><span data-stu-id="0bd18-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="0bd18-200">U krijgt onmiddellijk een SMS-antwoord met de tekst "artikel van Hey, Bedankt voor het pingen!</span><span class="sxs-lookup"><span data-stu-id="0bd18-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="0bd18-201">Twilio en Azure steen! '.</span><span class="sxs-lookup"><span data-stu-id="0bd18-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="0bd18-202"><a id="additional_services"></a>How to: extra Twilio-Services gebruiken</span><span class="sxs-lookup"><span data-stu-id="0bd18-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="0bd18-203">Naast de voorbeelden die hier worden weergegeven, biedt Twilio web-API's waarmee u kunt gebruikmaken van aanvullende Twilio-functionaliteit van uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0bd18-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="0bd18-204">Zie voor meer informatie de [Twilio-API-documentatie][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="0bd18-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="0bd18-205"><a id="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0bd18-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="0bd18-206">Nu u de basisprincipes van de Twilio-service hebt geleerd, volgt u deze koppelingen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="0bd18-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="0bd18-207">[Richtlijnen voor Twilio-beveiliging][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="0bd18-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="0bd18-208">[Twilio HowTos en voorbeeldcode][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="0bd18-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="0bd18-209">[Twilio Quick Start-zelfstudie][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="0bd18-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="0bd18-210">[Twilio op GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="0bd18-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="0bd18-211">[Neem contact op met Twilio-ondersteuning][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="0bd18-211">[Talk to Twilio Support][twilio_support]</span></span>

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
