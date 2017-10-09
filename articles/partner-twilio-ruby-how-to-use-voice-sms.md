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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="c017c-104">Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden in Ruby</span><span class="sxs-lookup"><span data-stu-id="c017c-104">How tooUse Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="c017c-105">Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello Twilio-API-service op Azure.</span><span class="sxs-lookup"><span data-stu-id="c017c-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="c017c-106">Hallo scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden.</span><span class="sxs-lookup"><span data-stu-id="c017c-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="c017c-107">Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen Hallo [Vervolgstappen](#NextSteps) sectie.</span><span class="sxs-lookup"><span data-stu-id="c017c-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="c017c-108"><a id="WhatIs"></a>Wat is Twilio?</span><span class="sxs-lookup"><span data-stu-id="c017c-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="c017c-109">Twilio is een telephony-webservice-API waarmee u uw bestaande web talen en de vaardigheden toobuild stem en de SMS-toepassingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c017c-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="c017c-110">Twilio is een service van derden (niet een functie van Azure en niet in een Microsoft-product).</span><span class="sxs-lookup"><span data-stu-id="c017c-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="c017c-111">**Twilio stem** kunt u uw toepassingen toomake en gebeld.</span><span class="sxs-lookup"><span data-stu-id="c017c-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="c017c-112">**Twilio SMS** kunt u uw toepassingen toomake en SMS-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="c017c-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="c017c-113">**Twilio Client** zorgt ervoor dat uw toepassingen tooenable gesproken communicatie met bestaande Internet-verbindingen, inclusief mobiele verbindingen.</span><span class="sxs-lookup"><span data-stu-id="c017c-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="c017c-114"><a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="c017c-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="c017c-115">Informatie over prijzen voor Twilio is beschikbaar op [Twilio prijzen][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="c017c-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="c017c-116">Azure-klanten ontvangen een [speciale aanbieding][special_offer]: een gratis tegoed van 1000 teksten of 1000 inkomende minuten.</span><span class="sxs-lookup"><span data-stu-id="c017c-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="c017c-117">toosign voor dit bieden of meer informatie, gaat u naar [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="c017c-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="c017c-118"><a id="Concepts"></a>Concepten</span><span class="sxs-lookup"><span data-stu-id="c017c-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="c017c-119">Hallo Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c017c-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="c017c-120">Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="c017c-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="c017c-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="c017c-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="c017c-122">TwiML is een reeks XML-instructies die Twilio van hoe u informeren tooprocess een telefoongesprek of SMS.</span><span class="sxs-lookup"><span data-stu-id="c017c-122">TwiML is a set of XML-based instructions that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="c017c-123">Als u bijvoorbeeld Hallo TwiML na Hallo tekst wilt converteren **Hallo wereld** toospeech.</span><span class="sxs-lookup"><span data-stu-id="c017c-123">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="c017c-124">Alle TwiML documenten hebben `<Response>` als hun hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="c017c-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="c017c-125">Van daaruit u Twilio-termen toodefine Hallo gedrag van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="c017c-125">From there, you use Twilio Verbs toodefine hello behavior of your application.</span></span>

### <span data-ttu-id="c017c-126"><a id="Verbs"></a>TwiML termen</span><span class="sxs-lookup"><span data-stu-id="c017c-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="c017c-127">Twilio-bewerkingen zijn XML-labels die Twilio wat te vertellen**doen**.</span><span class="sxs-lookup"><span data-stu-id="c017c-127">Twilio Verbs are XML tags that tell Twilio what too**do**.</span></span> <span data-ttu-id="c017c-128">Bijvoorbeeld, Hallo  **&lt;zeg&gt;**  term Hiermee Twilio tooaudibly afleveren geeft een bericht op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="c017c-128">For example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span> 

<span data-ttu-id="c017c-129">Hallo Hieronder volgt een lijst met Twilio-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c017c-129">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="c017c-130">**&lt;Externe&gt;**: Hallo aanroeper tooanother telefoon verbindt.</span><span class="sxs-lookup"><span data-stu-id="c017c-130">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="c017c-131">**&lt;Verzamel&gt;**: cijfers ingevoerd op het telefoonnummer Hallo verzamelt.</span><span class="sxs-lookup"><span data-stu-id="c017c-131">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="c017c-132">**&lt;Ophangen&gt;**: een aanroep wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="c017c-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="c017c-133">**&lt;Afspelen&gt;**: een geluidsbestand afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="c017c-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="c017c-134">**&lt;Onderbreken&gt;**: achtergrond wacht op een opgegeven aantal seconden.</span><span class="sxs-lookup"><span data-stu-id="c017c-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="c017c-135">**&lt;Record&gt;**: Hallo aanroeper stem registreert en retourneert een URL van een bestand dat Hallo opname bevat.</span><span class="sxs-lookup"><span data-stu-id="c017c-135">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="c017c-136">**&lt;Omleiden&gt;**: draagt de controle van een telefoongesprek of SMS toohello TwiML op een andere URL.</span><span class="sxs-lookup"><span data-stu-id="c017c-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="c017c-137">**&lt;Afwijzen&gt;**: geweigerd een binnenkomende tooyour Twilio nummer bellen zonder u facturering</span><span class="sxs-lookup"><span data-stu-id="c017c-137">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="c017c-138">**&lt;Zeg&gt;**: zet tekst toospeech die wordt gemaakt op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="c017c-138">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="c017c-139">**&lt;SMS&gt;**: een SMS-bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="c017c-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="c017c-140">Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="c017c-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="c017c-141">Zie voor meer informatie over Hallo Twilio-API, [Twilio-API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="c017c-141">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="c017c-142"><a id="CreateAccount"></a>Een Twilio-Account maken</span><span class="sxs-lookup"><span data-stu-id="c017c-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="c017c-143">Wanneer u klaar tooget een Twilio-account bent, aanmelden op [probeer Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="c017c-143">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="c017c-144">U kunt beginnen met een gratis account en upgrade van uw account later.</span><span class="sxs-lookup"><span data-stu-id="c017c-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="c017c-145">Wanneer u zich voor een Twilio-account aanmeldt, krijgt u een gratis telefoonnummer voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="c017c-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="c017c-146">U ontvangt ook een SID-account en een auth-token.</span><span class="sxs-lookup"><span data-stu-id="c017c-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="c017c-147">Beide worden benodigde toomake Twilio-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c017c-147">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="c017c-148">tooprevent onbevoegde toegang tot tooyour account, het verificatietoken te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="c017c-148">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="c017c-149">Uw account-SID en auth token kunnen worden bekeken op Hallo [Twilio-accountpagina][twilio_account]in velden met het label Hallo **ACCOUNT-SID** en **AUTH TOKEN** , respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="c017c-149">Your account SID and auth token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="c017c-150"><a id="VerifyPhoneNumbers"></a>Controleer of de telefoonnummers</span><span class="sxs-lookup"><span data-stu-id="c017c-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="c017c-151">Toevoeging toohello aantal u door Twilio krijgt, kunt u ook cijfers (dat wil zeggen uw mobiele telefoon of home telefoonnummer) te beheren voor gebruik in uw toepassingen controleren.</span><span class="sxs-lookup"><span data-stu-id="c017c-151">In addition toohello number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="c017c-152">Voor meer informatie over een telefoonnummer tooverify Zie [beheren cijfers][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="c017c-152">For information on how tooverify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="c017c-153"><a id="create_app"></a>Een Ruby-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="c017c-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="c017c-154">Een Ruby-toepassing die gebruikmaakt van Hallo Twilio-service en wordt uitgevoerd in Azure gaat niet anders dan andere Ruby toepassing die gebruikmaakt van Hallo Twilio-service.</span><span class="sxs-lookup"><span data-stu-id="c017c-154">A Ruby application that uses hello Twilio service and is running in Azure is no different than any other Ruby application that uses hello Twilio service.</span></span> <span data-ttu-id="c017c-155">Terwijl Twilio-services RESTful worden en op verschillende manieren kunnen worden aangeroepen vanuit Ruby, in dit artikel wordt de nadruk gelegd op hoe toouse Twilio services met [Twilio hulpbibliotheek voor Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="c017c-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how toouse Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="c017c-156">Eerst [installatie een nieuwe Azure Linux VM] [ azure_vm_setup] tooact als host voor de nieuwe Ruby-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="c017c-156">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Ruby web application.</span></span> <span data-ttu-id="c017c-157">Hallo stappen met betrekking tot Hallo maken van een app Rails, net set-up Hallo VM overslaan.</span><span class="sxs-lookup"><span data-stu-id="c017c-157">Ignore hello steps involving hello creation of a Rails app, just set-up hello VM.</span></span> <span data-ttu-id="c017c-158">Zorg ervoor dat u maakt een eindpunt met een externe poort 80 en een interne 5000-poort.</span><span class="sxs-lookup"><span data-stu-id="c017c-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="c017c-159">In onderstaande Hallo voorbeelden, we gebruiken [Sinatra][sinatra], een zeer eenvoudige web-framework voor Ruby.</span><span class="sxs-lookup"><span data-stu-id="c017c-159">In hello examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="c017c-160">Maar u kunt gewoon Hallo Twilio-hulpbibliotheek voor Ruby gebruiken met een andere webframework, met inbegrip van Ruby op Rails.</span><span class="sxs-lookup"><span data-stu-id="c017c-160">But you can certainly use hello Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="c017c-161">SSH in uw nieuwe virtuele machine en maak een map voor uw nieuwe app.</span><span class="sxs-lookup"><span data-stu-id="c017c-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="c017c-162">Maak een bestand met de naam Gemfile en kopieer Hallo code in het volgende in die map:</span><span class="sxs-lookup"><span data-stu-id="c017c-162">Inside that directory, create a file called Gemfile and copy hello following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="c017c-163">Op Hallo opdrachtregel uitvoeren `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="c017c-163">On hello command line run `bundle install`.</span></span> <span data-ttu-id="c017c-164">Hiermee installeert u bovenstaande Hallo-afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="c017c-164">This will install hello dependencies above.</span></span> <span data-ttu-id="c017c-165">Maak vervolgens een bestand met de naam `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="c017c-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="c017c-166">Dit is waar Hallo-code voor uw web-app woont.</span><span class="sxs-lookup"><span data-stu-id="c017c-166">This will be where hello code for your web app lives.</span></span> <span data-ttu-id="c017c-167">Plak Hallo code in het volgende:</span><span class="sxs-lookup"><span data-stu-id="c017c-167">Paste hello following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="c017c-168">Op dit moment moet u kunnen Hallo uitvoeren Hallo opdracht `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="c017c-168">At this point you should be able hello run hello command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="c017c-169">Dit wordt spin-up een kleine webserver op poort 5000.</span><span class="sxs-lookup"><span data-stu-id="c017c-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="c017c-170">U moet kunnen toobrowse toothis app in uw browser via Hallo URL instellen voor uw Azure VM.</span><span class="sxs-lookup"><span data-stu-id="c017c-170">You should be able toobrowse toothis app in your browser by visiting hello URL you set-up for your Azure VM.</span></span> <span data-ttu-id="c017c-171">Nadat u uw web-app in de browser Hallo bereiken kunt, bent u klaar toostart bouwen van een Twilio-app.</span><span class="sxs-lookup"><span data-stu-id="c017c-171">Once you can reach your web app in hello browser, you're ready toostart building a Twilio app.</span></span>

## <span data-ttu-id="c017c-172"><a id="configure_app"></a>Uw toepassing tooUse Twilio configureren</span><span class="sxs-lookup"><span data-stu-id="c017c-172"><a id="configure_app"></a>Configure Your Application tooUse Twilio</span></span>
<span data-ttu-id="c017c-173">U kunt uw web-app toouse hello Twilio-bibliotheek configureren met het bijwerken van uw `Gemfile` tooinclude deze regel:</span><span class="sxs-lookup"><span data-stu-id="c017c-173">You can configure your web app toouse hello Twilio library by updating your `Gemfile` tooinclude this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="c017c-174">Voer op de opdrachtregel hello, `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="c017c-174">On hello command line, run `bundle install`.</span></span> <span data-ttu-id="c017c-175">Open nu `web.rb` en deze regel boven hello, inclusief:</span><span class="sxs-lookup"><span data-stu-id="c017c-175">Now open `web.rb` and including this line at hello top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="c017c-176">U bent nu klaar voor toouse hello Twilio-hulpbibliotheek voor Ruby in uw web-app.</span><span class="sxs-lookup"><span data-stu-id="c017c-176">You're now all set toouse hello Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="c017c-177"><a id="howto_make_call"></a>Procedure: een uitgaande aanroep</span><span class="sxs-lookup"><span data-stu-id="c017c-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="c017c-178">Hallo volgende ziet u hoe een uitgaande toomake aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c017c-178">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="c017c-179">Belangrijkste concepten bevatten voor Ruby toomake die rest-API aanroept met behulp van Hallo Twilio-hulpbibliotheek en TwiML rendering.</span><span class="sxs-lookup"><span data-stu-id="c017c-179">Key concepts include using hello Twilio helper library for Ruby toomake REST API calls and rendering TwiML.</span></span> <span data-ttu-id="c017c-180">Vervang uw waarden voor Hallo **van** en **naar** telefoonnummers, en zorg ervoor dat u controleert of Hallo **van** telefoonnummer voor uw Twilio-account voorafgaande toorunning Hallo code.</span><span class="sxs-lookup"><span data-stu-id="c017c-180">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

<span data-ttu-id="c017c-181">Deze functie te toevoegen`web.md`:</span><span class="sxs-lookup"><span data-stu-id="c017c-181">Add this function too`web.md`:</span></span>

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

<span data-ttu-id="c017c-182">Als de open-up `http://yourdomain.cloudapp.net/make_call` in een browser die Hallo aanroep toohello Twilio-API toomake Hallo telefonische oproep wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="c017c-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger hello call toohello Twilio API toomake hello phone call.</span></span> <span data-ttu-id="c017c-183">Hallo eerst twee parameters in `client.account.calls.create` redelijk spreken voor zich: Hallo nummer Hallo-aanroep is `from` en Hallo nummer Hallo-aanroep is `to`.</span><span class="sxs-lookup"><span data-stu-id="c017c-183">hello first two parameters in `client.account.calls.create` are fairly self-explanatory: hello number hello call is `from` and hello number hello call is `to`.</span></span> 

<span data-ttu-id="c017c-184">Hallo derde parameter (`url`) Hallo URL dat Twilio tooget instructies over welke toodo aanvragen zodra het Hallo-aanroep is verbonden.</span><span class="sxs-lookup"><span data-stu-id="c017c-184">hello third parameter (`url`) is hello URL that Twilio requests tooget instructions on what toodo once hello call is connected.</span></span> <span data-ttu-id="c017c-185">In dit geval wordt de installatie een URL (`http://yourdomain.cloudapp.net`) die een eenvoudig TwiML document retourneert en maakt gebruik van Hallo `<Say>` term toodo sommige spraak en spreek 'Hello Monkey' toohello ontvanger Hallo aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c017c-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses hello `<Say>` verb toodo some text-to-speech and say "Hello Monkey" toohello person recieving hello call.</span></span>

## <span data-ttu-id="c017c-186"><a id="howto_recieve_sms"></a>Procedure: een SMS-bericht ontvangen</span><span class="sxs-lookup"><span data-stu-id="c017c-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="c017c-187">In het vorige voorbeeld Hallo geïnitieerd we een **uitgaande** telefoongesprek.</span><span class="sxs-lookup"><span data-stu-id="c017c-187">In hello previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="c017c-188">Deze tijd, Hallo telefoonnummer op dat Twilio doorgegeven tijdens registratie tooprocess hebt we gebruiken een **binnenkomende** SMS-bericht.</span><span class="sxs-lookup"><span data-stu-id="c017c-188">This time, let's use hello phone number that Twilio gave us during sign-up tooprocess an **incoming** SMS message.</span></span>

<span data-ttu-id="c017c-189">Eerste, aanmelden tooyour [Twilio-dashboard][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="c017c-189">First, log-in tooyour [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="c017c-190">Klik op 'Cijfers' in de bovenste nav Hallo en klik vervolgens op Hallo Twilio-nummer die u zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c017c-190">Click on "Numbers" in hello top nav and then click on hello Twilio number you were provided.</span></span> <span data-ttu-id="c017c-191">Hier ziet u twee URL's die u kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="c017c-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="c017c-192">Een stem aanvraag-URL en een SMS-bericht aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="c017c-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="c017c-193">Dit zijn Hallo-URL's die is gemaakt met Twilio-aanroepen wanneer een telefonische oproep of een SMS-bericht tooyour nummer wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="c017c-193">These are hello URLs that Twilio calls whenever a phone call is made or an SMS is sent tooyour number.</span></span> <span data-ttu-id="c017c-194">Hallo-URL's worden ook wel bekend als 'web hooks'.</span><span class="sxs-lookup"><span data-stu-id="c017c-194">hello URLs are also known as "web hooks".</span></span>

<span data-ttu-id="c017c-195">Willen we graag tooprocess binnenkomende SMS-berichten, dus we Hallo URL bijwerken`http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="c017c-195">We would like tooprocess incoming SMS messages, so let's update hello URL too`http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="c017c-196">Opwekken en klikt u op wijzigingen opslaan onder Hallo van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="c017c-196">Go ahead and click Save Changes at hello bottom of hello page.</span></span> <span data-ttu-id="c017c-197">Nu weer `web.rb` onze toepassing toohandle we programma dit:</span><span class="sxs-lookup"><span data-stu-id="c017c-197">Now, back in `web.rb` let's program our application toohandle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="c017c-198">Hallo nadat wijziging hebt aangebracht, moet u ervoor dat toore-begin uw web-app.</span><span class="sxs-lookup"><span data-stu-id="c017c-198">After making hello change, make sure toore-start your web app.</span></span> <span data-ttu-id="c017c-199">Nu uw telefoon Elimineer en verzenden van een SMS-tooyour Twilio-nummer.</span><span class="sxs-lookup"><span data-stu-id="c017c-199">Now, take out your phone and send an SMS tooyour Twilio number.</span></span> <span data-ttu-id="c017c-200">U krijgt onmiddellijk een SMS-antwoord met de tekst "artikel van Hey, Hartelijk dank voor het Hallo-ping!</span><span class="sxs-lookup"><span data-stu-id="c017c-200">You should promptly get an SMS response that says "Hey, thanks for hello ping!</span></span> <span data-ttu-id="c017c-201">Twilio en Azure steen! '.</span><span class="sxs-lookup"><span data-stu-id="c017c-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="c017c-202"><a id="additional_services"></a>How to: extra Twilio-Services gebruiken</span><span class="sxs-lookup"><span data-stu-id="c017c-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="c017c-203">Bovendien kunt toohello voorbeelden die hier worden weergegeven, dat twilio biedt op basis van een web-API's u tooleverage aanvullende Twilio-functionaliteit van uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c017c-203">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="c017c-204">Zie voor meer details Hallo [Twilio-API-documentatie][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="c017c-204">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="c017c-205"><a id="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c017c-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="c017c-206">Nu u basisprincipes Hallo Hallo Twilio-service hebt geleerd, volgt u deze koppelingen toolearn meer:</span><span class="sxs-lookup"><span data-stu-id="c017c-206">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="c017c-207">[Richtlijnen voor Twilio-beveiliging][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="c017c-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="c017c-208">[Twilio HowTos en voorbeeldcode][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="c017c-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="c017c-209">[Twilio Quick Start-zelfstudie][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="c017c-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="c017c-210">[Twilio op GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="c017c-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="c017c-211">[Neem contact tooTwilio ondersteuning][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="c017c-211">[Talk tooTwilio Support][twilio_support]</span></span>

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
