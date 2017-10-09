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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="e07d8-104">Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden in Python</span><span class="sxs-lookup"><span data-stu-id="e07d8-104">How tooUse Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="e07d8-105">Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello Twilio-API-service op Azure.</span><span class="sxs-lookup"><span data-stu-id="e07d8-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="e07d8-106">Hallo scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden.</span><span class="sxs-lookup"><span data-stu-id="e07d8-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="e07d8-107">Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen Hallo [Vervolgstappen](#NextSteps) sectie.</span><span class="sxs-lookup"><span data-stu-id="e07d8-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="e07d8-108"><a id="WhatIs"></a>Wat is Twilio?</span><span class="sxs-lookup"><span data-stu-id="e07d8-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="e07d8-109">Twilio is dat toekomstige Hallo zakelijke communicatie, ontwikkelaars tooembed spraak, VoIP, inschakelen en messaging in toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e07d8-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="e07d8-110">Ze virtualiseren alle infrastructuur die nodig is in een cloud-gebaseerde, globale-omgeving, beschikbaar te maken via Hallo Twilio communications API-platform.</span><span class="sxs-lookup"><span data-stu-id="e07d8-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="e07d8-111">Toepassingen zijn eenvoudige toobuild en schaalbare.</span><span class="sxs-lookup"><span data-stu-id="e07d8-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="e07d8-112">Profiteer van flexibiliteit met pay-as-you gaat prijzen en profiteren van de betrouwbaarheid van de cloud.</span><span class="sxs-lookup"><span data-stu-id="e07d8-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="e07d8-113">**Twilio stem** kunt u uw toepassingen toomake en gebeld.</span><span class="sxs-lookup"><span data-stu-id="e07d8-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span>
<span data-ttu-id="e07d8-114">**Twilio SMS** kunt u uw toepassing toosend tekstberichten en ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e07d8-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span>
<span data-ttu-id="e07d8-115">**Twilio Client** kunt u toomake VoIP-aanroepen vanuit een telefoon, tablet of een browser en WebRTC ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="e07d8-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="e07d8-116"><a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="e07d8-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="e07d8-117">Azure-klanten ontvangen een [speciale aanbieding] [ special_offer] $10 Twilio tegoed wanneer u een upgrade uitvoert van uw Twilio-Account.</span><span class="sxs-lookup"><span data-stu-id="e07d8-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="e07d8-118">Deze Twilio-tegoed kan worden toegepast tooany Twilio-gebruik ($10 tegoed gelijkwaardige toosending maximaal 1000 SMS-berichten of ontvangst van too1000 inkomende stem minuten, afhankelijk van de locatie van uw telefoon en bericht- of aanroep bestemming Hallo).</span><span class="sxs-lookup"><span data-stu-id="e07d8-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="e07d8-119">Dit inwisselen [Twilio tegoed] [ special_offer] en aan de slag.</span><span class="sxs-lookup"><span data-stu-id="e07d8-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="e07d8-120">Twilio is een betalen naar gebruik service.</span><span class="sxs-lookup"><span data-stu-id="e07d8-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="e07d8-121">Er zijn geen kosten instellen en kunt u uw account op elk moment sluiten.</span><span class="sxs-lookup"><span data-stu-id="e07d8-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="e07d8-122">U vindt meer informatie op [Twilio prijzen][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="e07d8-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="e07d8-123"><a id="Concepts"></a>Concepten</span><span class="sxs-lookup"><span data-stu-id="e07d8-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="e07d8-124">Hallo Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e07d8-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="e07d8-125">Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="e07d8-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="e07d8-126">Belangrijke aspecten van Hallo Twilio-API zijn Twilio-termen en Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="e07d8-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="e07d8-127"><a id="Verbs"></a>Twilio-termen</span><span class="sxs-lookup"><span data-stu-id="e07d8-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="e07d8-128">Hallo API wordt gebruikgemaakt van Twilio termen; bijvoorbeeld, Hallo  **&lt;zeg&gt;**  term Hiermee Twilio tooaudibly afleveren geeft een bericht op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="e07d8-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="e07d8-129">Hallo Hieronder volgt een lijst met Twilio-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="e07d8-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="e07d8-130">Meer informatie over Hallo andere termen en mogelijkheden via [Twilio Markup Language documentatie][twiml].</span><span class="sxs-lookup"><span data-stu-id="e07d8-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="e07d8-131">**&lt;Externe&gt;**: Hallo aanroeper tooanother telefoon verbindt.</span><span class="sxs-lookup"><span data-stu-id="e07d8-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="e07d8-132">**&lt;Verzamel&gt;**: cijfers ingevoerd op het telefoonnummer Hallo verzamelt.</span><span class="sxs-lookup"><span data-stu-id="e07d8-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="e07d8-133">**&lt;Ophangen&gt;**: een aanroep wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="e07d8-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="e07d8-134">**&lt;Onderbreken&gt;**: achtergrond wacht op een opgegeven aantal seconden.</span><span class="sxs-lookup"><span data-stu-id="e07d8-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="e07d8-135">**&lt;Afspelen&gt;**: een geluidsbestand afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="e07d8-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="e07d8-136">**&lt;Wachtrij&gt;**: Hallo tooa wachtrij van aanroepfuncties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e07d8-136">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="e07d8-137">**&lt;Record&gt;**: registreert Hallo stem van de aanroepfunctie Hallo en retourneert een URL van een bestand dat Hallo opname bevat.</span><span class="sxs-lookup"><span data-stu-id="e07d8-137">**&lt;Record&gt;**: Records hello voice of hello caller and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="e07d8-138">**&lt;Omleiden&gt;**: draagt de controle van een telefoongesprek of SMS toohello TwiML op een andere URL.</span><span class="sxs-lookup"><span data-stu-id="e07d8-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="e07d8-139">**&lt;Afwijzen&gt;**: geweigerd een binnenkomende tooyour Twilio nummer bellen zonder u facturering.</span><span class="sxs-lookup"><span data-stu-id="e07d8-139">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="e07d8-140">**&lt;Zeg&gt;**: zet tekst toospeech die wordt gemaakt op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="e07d8-140">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="e07d8-141">**&lt;SMS&gt;**: een SMS-bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="e07d8-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="e07d8-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="e07d8-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="e07d8-143">TwiML is een reeks XML gebaseerde instructies op basis van Hallo Twilio-termen die Twilio van hoe u informeren over tooprocess een telefoongesprek of SMS.</span><span class="sxs-lookup"><span data-stu-id="e07d8-143">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="e07d8-144">Als u bijvoorbeeld Hallo TwiML na Hallo tekst wilt converteren **Hallo wereld** toospeech.</span><span class="sxs-lookup"><span data-stu-id="e07d8-144">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="e07d8-145">Bij het aanroepen van uw toepassing hello Twilio-API, is een van de API-parameters Hallo Hallo-URL die Hallo TwiML antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e07d8-145">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="e07d8-146">U kunt voor ontwikkelingsdoeleinden Twilio geleverde URL's tooprovide hello TwiML antwoorden die wordt gebruikt door uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e07d8-146">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="e07d8-147">U ook uw eigen URL's tooproduce hello TwiML reacties kan hosten en een andere optie is toouse hello `TwiMLResponse` object.</span><span class="sxs-lookup"><span data-stu-id="e07d8-147">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello `TwiMLResponse` object.</span></span>

<span data-ttu-id="e07d8-148">Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="e07d8-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="e07d8-149">Zie voor meer informatie over Hallo Twilio-API, [Twilio-API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="e07d8-149">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="e07d8-150"><a id="CreateAccount"></a>Een Twilio-Account maken</span><span class="sxs-lookup"><span data-stu-id="e07d8-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="e07d8-151">Wanneer u klaar tooget een Twilio-account bent, aanmelden op [probeer Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="e07d8-151">When you are ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="e07d8-152">U kunt beginnen met een gratis account en upgrade van uw account later.</span><span class="sxs-lookup"><span data-stu-id="e07d8-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="e07d8-153">Wanneer u zich voor een Twilio-account aanmeldt, ontvangt u een account-SID en geen verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="e07d8-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="e07d8-154">Beide worden benodigde toomake Twilio-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e07d8-154">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="e07d8-155">tooprevent onbevoegde toegang tot tooyour account, het verificatietoken te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="e07d8-155">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="e07d8-156">Uw account-SID en de verificatietoken worden weergegeven in Hallo [Twilio Console][twilio_console]in velden met het label Hallo **ACCOUNT-SID** en **AUTH TOKEN**respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="e07d8-156">Your account SID and authentication token are viewable in hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="e07d8-157"><a id="create_app"></a>Een Python-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="e07d8-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="e07d8-158">Een Python-toepassing die gebruikmaakt van Hallo Twilio-service en wordt uitgevoerd in Azure gaat niet anders dan de andere Python-toepassing die gebruikmaakt van Hallo Twilio-service.</span><span class="sxs-lookup"><span data-stu-id="e07d8-158">A Python application that uses hello Twilio service and is running in Azure is no different than any other Python application that uses hello Twilio service.</span></span> <span data-ttu-id="e07d8-159">Terwijl Twilio-services op basis van REST worden en op verschillende manieren kunnen worden aangeroepen vanuit Python, in dit artikel wordt de nadruk gelegd op hoe toouse Twilio services met [Twilio-bibliotheek voor Python vanuit GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="e07d8-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how toouse Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="e07d8-160">Zie voor meer informatie over het gebruik van Hallo Twilio-bibliotheek voor Python [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="e07d8-160">For more information about using hello Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="e07d8-161">Eerste, [installatie een nieuwe Azure Linux VM] [azure_vm_setup] tooact als host voor de nieuwe Python-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="e07d8-161">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Python web application.</span></span> <span data-ttu-id="e07d8-162">Zodra hello virtuele Machine wordt uitgevoerd, moet u tooexpose uw toepassing op een openbare poort zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="e07d8-162">Once hello Virtual Machine is running, you will need tooexpose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="e07d8-163">Een inkomende regel toevoegen</span><span class="sxs-lookup"><span data-stu-id="e07d8-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="e07d8-164">Ga toohello [Netwerkbeveiligingsgroep] [azure_nsg] pagina.</span><span class="sxs-lookup"><span data-stu-id="e07d8-164">Go toohello [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="e07d8-165">Selecteer Hallo Netwerkbeveiligingsgroep dat correspondeert met de virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="e07d8-165">Select hello Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="e07d8-166">Toevoegen en **uitgaande regel** voor **poort 80**.</span><span class="sxs-lookup"><span data-stu-id="e07d8-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="e07d8-167">Ervoor tooallow binnenkomende van elk adres zijn.</span><span class="sxs-lookup"><span data-stu-id="e07d8-167">Be sure tooallow incoming from any address.</span></span>

### <a name="set-hello-dns-name-label"></a><span data-ttu-id="e07d8-168">Hallo Label DNS-naam instellen</span><span class="sxs-lookup"><span data-stu-id="e07d8-168">Set hello DNS Name Label</span></span>
  1. <span data-ttu-id="e07d8-169">Ga toohello [Hallo openbare IP-mailadressen] [azure_ips] pagina.</span><span class="sxs-lookup"><span data-stu-id="e07d8-169">Go toohello [hello Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="e07d8-170">Selecteer Hallo openbare IP-adres dat correspends met uw virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="e07d8-170">Select hello Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="e07d8-171">Set Hallo **Label DNS-naam** in Hallo **configuratie** sectie.</span><span class="sxs-lookup"><span data-stu-id="e07d8-171">Set hello **DNS Name Label** in hello **Configuration** section.</span></span> <span data-ttu-id="e07d8-172">In geval van Hallo van dit voorbeeld is het wordt als volgt uitzien *your domain-label*. centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="e07d8-172">In hello case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="e07d8-173">Zodra u zich kunt tooconnect via SSH toohello virtuele Machine die u kunt installeren Webframework van uw keuze Hallo (Hallo twee meest bekende in Python wordt [Flask](http://flask.pocoo.org/) en [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="e07d8-173">Once you are able tooconnect through SSH toohello Virtual Machine you can install hello Web Framework of your choice (hello two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="e07d8-174">U kunt een van beide installeren alleen door Hallo `pip install` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e07d8-174">You can install either of them just by running hello `pip install` command.</span></span>

<span data-ttu-id="e07d8-175">Houd er rekening mee dat we Hallo virtueel machineverkeer tooallow alleen geconfigureerd op poort 80.</span><span class="sxs-lookup"><span data-stu-id="e07d8-175">Keep in mind that we configured hello Virtual Machine tooallow traffic only on port 80.</span></span> <span data-ttu-id="e07d8-176">Dus zorg ervoor dat tooconfigure Hallo toepassing toouse deze poort.</span><span class="sxs-lookup"><span data-stu-id="e07d8-176">So make sure tooconfigure hello application toouse this port.</span></span>

## <span data-ttu-id="e07d8-177"><a id="configure_app"></a>Configureren van uw toepassing tooUse Twilio-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="e07d8-177"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="e07d8-178">U kunt uw toepassing toouse hello Twilio-bibliotheek voor Python configureren op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="e07d8-178">You can configure your application toouse hello Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="e07d8-179">Hallo Twilio-bibliotheek voor Python installeren als een Pip-pakket.</span><span class="sxs-lookup"><span data-stu-id="e07d8-179">Install hello Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="e07d8-180">Het kan worden geïnstalleerd met Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="e07d8-180">It can be installed with hello following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="e07d8-181">OF</span><span class="sxs-lookup"><span data-stu-id="e07d8-181">-OR-</span></span>

* <span data-ttu-id="e07d8-182">Hallo Twilio-bibliotheek voor Python vanuit GitHub downloaden ([https://github.com/twilio/twilio-python][twilio_python]) en installeer deze als volgt:</span><span class="sxs-lookup"><span data-stu-id="e07d8-182">Download hello Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="e07d8-183">Wanneer u Hallo Twilio-bibliotheek voor Python hebt geïnstalleerd, kunt u vervolgens `import` in uw Python-bestanden:</span><span class="sxs-lookup"><span data-stu-id="e07d8-183">Once you have installed hello Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="e07d8-184">Zie voor meer informatie [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="e07d8-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="e07d8-185"><a id="howto_make_call"></a>Procedure: een uitgaande aanroep</span><span class="sxs-lookup"><span data-stu-id="e07d8-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="e07d8-186">Hallo volgende ziet u hoe een uitgaande toomake aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e07d8-186">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="e07d8-187">Deze code wordt een Twilio-voorwaarde site tooreturn hello Twilio Markup Language (TwiML) antwoord.</span><span class="sxs-lookup"><span data-stu-id="e07d8-187">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="e07d8-188">Vervang uw waarden voor Hallo **from_number** en **to_number** telefoonnummers, en zorg ervoor dat u hebt geverifieerd dat Hallo **from_number** telefoonnummer voor uw Twilio-account voordat u de code van de Hallo is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e07d8-188">Substitute your values for hello **from_number** and **to_number** phone numbers, and ensure that you've verified hello **from_number** phone number for your Twilio account before running hello code.</span></span>

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

<span data-ttu-id="e07d8-189">Zoals gezegd, gebruikt deze code een Twilio-voorwaarde site tooreturn hello TwiML antwoord.</span><span class="sxs-lookup"><span data-stu-id="e07d8-189">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="e07d8-190">U kunt in plaats hiervan uw eigen site tooprovide hello TwiML antwoord; Zie voor meer informatie [hoe tooProvide TwiML antwoorden vanaf uw eigen website](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="e07d8-190">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="e07d8-191"><a id="howto_send_sms"></a>Procedure: een SMS-bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="e07d8-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="e07d8-192">Hallo hieronder ziet u hoe een SMS-bericht met toosend Hallo `TwilioRestClient` klasse.</span><span class="sxs-lookup"><span data-stu-id="e07d8-192">hello following shows how toosend an SMS message using hello `TwilioRestClient` class.</span></span> <span data-ttu-id="e07d8-193">Hallo **from_number** nummer wordt geleverd door Twilio voor proefversie accounts toosend SMS-berichten.</span><span class="sxs-lookup"><span data-stu-id="e07d8-193">hello **from_number** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="e07d8-194">Hallo **to_number** nummer voor uw Twilio-account moet worden gecontroleerd voordat Hallo code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e07d8-194">hello **to_number** number must be verified for your Twilio account before running hello code.</span></span>

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

## <span data-ttu-id="e07d8-195"><a id="howto_provide_twiml_responses"></a>Hoe: TwiML reacties van uw eigen Website opgeven</span><span class="sxs-lookup"><span data-stu-id="e07d8-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="e07d8-196">Wanneer uw toepassing een aanroep van toohello Twilio-API initieert, stuurt Twilio uw aanvraag tooa-URL die wordt verwacht tooreturn TwiML antwoord.</span><span class="sxs-lookup"><span data-stu-id="e07d8-196">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="e07d8-197">Hallo in bovenstaand voorbeeld gebruikt Hallo Twilio-geleverde URL [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="e07d8-197">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="e07d8-198">(Hoewel TwiML is ontworpen voor gebruik door Twilio, kunt u deze bekijken in uw browser.</span><span class="sxs-lookup"><span data-stu-id="e07d8-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="e07d8-199">Bijvoorbeeld, klik op [http://twimlets.com/message] [ twimlet_message_url] toosee een lege `<Response>` element; Klik bijvoorbeeld op [http://twimlets.com/message? Bericht % 5B0 %5, D = Hallo % 20World] [ twimlet_message_url_hello_world] toosee een `<Response>` element met een `<Say>` element.)</span><span class="sxs-lookup"><span data-stu-id="e07d8-199">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="e07d8-200">In plaats van te vertrouwen op Hallo geleverde Twilio-URL, kunt u uw eigen website waarmee HTTP-antwoorden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e07d8-200">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="e07d8-201">U kunt Hallo-site maken in een andere taal die als resultaat geeft de XML-reacties; in dit onderwerp wordt ervan uitgegaan dat u Python toocreate hello TwiML gaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e07d8-201">You can create hello site in any language that returns XML responses; this topic assumes you will be using Python toocreate hello TwiML.</span></span>

<span data-ttu-id="e07d8-202">Hallo volgende voorbeelden wordt de uitvoer een TwiML-antwoord dat **Hallo wereld** op Hallo-aanroep.</span><span class="sxs-lookup"><span data-stu-id="e07d8-202">hello following examples will output a TwiML response that says **Hello World** on hello call.</span></span>

<span data-ttu-id="e07d8-203">Met Flask:</span><span class="sxs-lookup"><span data-stu-id="e07d8-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="e07d8-204">Met Django:</span><span class="sxs-lookup"><span data-stu-id="e07d8-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="e07d8-205">Zoals u in de bovenstaande Hallo voorbeeld zien kunt, is het Hallo TwiML antwoord gewoon een XML-document.</span><span class="sxs-lookup"><span data-stu-id="e07d8-205">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="e07d8-206">Hallo Twilio-bibliotheek voor Python bevat klassen die voor u TwiML genereren.</span><span class="sxs-lookup"><span data-stu-id="e07d8-206">hello Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="e07d8-207">Hallo onderstaand voorbeeld gelijkwaardige antwoord Hallo produceert, zoals hierboven beschreven, maar gebruikt Hallo `twiml` module in Hallo Twilio-bibliotheek voor Python:</span><span class="sxs-lookup"><span data-stu-id="e07d8-207">hello example below produces hello equivalent response as shown above, but uses hello `twiml` module in hello Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="e07d8-208">Zie voor meer informatie over TwiML [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="e07d8-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="e07d8-209">Zodra u uw Python-toepassing instellen tooprovide TwiML antwoorden hebt, Hallo-URL van de toepassing hello gebruiken als de URL die wordt doorgegeven in Hallo Hallo `client.calls.create` methode.</span><span class="sxs-lookup"><span data-stu-id="e07d8-209">Once you have your Python application set up tooprovide TwiML responses, use hello URL of hello application as hello URL passed into hello `client.calls.create`  method.</span></span> <span data-ttu-id="e07d8-210">Bijvoorbeeld, als u een webtoepassing met de naam hebt **MyTwiML** geïmplementeerde tooan Azure gehoste service, kunt u de url als webhook gebruiken zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="e07d8-210">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, you can use its url as webhook as shown in hello following example:</span></span>

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

## <span data-ttu-id="e07d8-211"><a id="AdditionalServices"></a>How to: extra Twilio-Services gebruiken</span><span class="sxs-lookup"><span data-stu-id="e07d8-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="e07d8-212">Bovendien kunt toohello voorbeelden die hier worden weergegeven, dat twilio biedt op basis van een web-API's u tooleverage aanvullende Twilio-functionaliteit van uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e07d8-212">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="e07d8-213">Zie voor meer details Hallo [Twilio-API-documentatie][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="e07d8-213">For full details, see hello [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="e07d8-214"><a id="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e07d8-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="e07d8-215">Nu u basisprincipes Hallo Hallo Twilio-service hebt geleerd, volgt u deze koppelingen toolearn meer:</span><span class="sxs-lookup"><span data-stu-id="e07d8-215">Now that you have learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="e07d8-216">[Richtlijnen voor Twilio-beveiliging][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="e07d8-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="e07d8-217">[Twilio-procedure hulplijnen en voorbeeldcode][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="e07d8-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="e07d8-218">[Twilio Quick Start-zelfstudie][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="e07d8-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="e07d8-219">[Twilio op GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="e07d8-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="e07d8-220">[Neem contact tooTwilio ondersteuning][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="e07d8-220">[Talk tooTwilio Support][twilio_support]</span></span>

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
