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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="5c61a-104">Hoe toouse Twilio voor spraak- en SMS-mogelijkheden van Azure</span><span class="sxs-lookup"><span data-stu-id="5c61a-104">How toouse Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="5c61a-105">Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello Twilio-API-service op Azure.</span><span class="sxs-lookup"><span data-stu-id="5c61a-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="5c61a-106">Hallo scenario's worden behandeld omvatten te bellen en een kort bericht Service (SMS)-bericht te verzenden.</span><span class="sxs-lookup"><span data-stu-id="5c61a-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="5c61a-107">Zie voor meer informatie over Twilio en spraak en SMS gebruiken in uw toepassingen Hallo [Vervolgstappen](#NextSteps) sectie.</span><span class="sxs-lookup"><span data-stu-id="5c61a-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="5c61a-108"><a id="WhatIs"></a>Wat is Twilio?</span><span class="sxs-lookup"><span data-stu-id="5c61a-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="5c61a-109">Twilio is dat toekomstige Hallo zakelijke communicatie, ontwikkelaars tooembed spraak, VoIP, inschakelen en messaging in toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5c61a-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="5c61a-110">Ze virtualiseren alle infrastructuur die nodig is in een cloud-gebaseerde, globale-omgeving, beschikbaar te maken via Hallo Twilio communications API-platform.</span><span class="sxs-lookup"><span data-stu-id="5c61a-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="5c61a-111">Toepassingen zijn eenvoudige toobuild en schaalbare.</span><span class="sxs-lookup"><span data-stu-id="5c61a-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="5c61a-112">Profiteer van flexibiliteit met betalen naar gebruik prijzen en profiteren van de betrouwbaarheid van de cloud.</span><span class="sxs-lookup"><span data-stu-id="5c61a-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="5c61a-113">**Twilio stem** kunt u uw toepassingen toomake en gebeld.</span><span class="sxs-lookup"><span data-stu-id="5c61a-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="5c61a-114">**Twilio SMS** kunt u uw toepassingen toosend en SMS-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="5c61a-114">**Twilio SMS** enables your applications toosend and receive SMS messages.</span></span> <span data-ttu-id="5c61a-115">**Twilio Client** kunt u toomake VoIP-aanroepen vanuit een telefoon, tablet of een browser en WebRTC ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="5c61a-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="5c61a-116"><a id="Pricing"></a>Twilio-prijzen en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="5c61a-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="5c61a-117">Azure-klanten ontvangen een [speciale aanbieding](http://www.twilio.com/azure): gratis $10 Twilio tegoed wanneer u een upgrade uitvoert van uw Twilio-Account.</span><span class="sxs-lookup"><span data-stu-id="5c61a-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="5c61a-118">Deze Twilio-tegoed kan worden toegepast tooany Twilio-gebruik ($10 tegoed gelijkwaardige toosending maximaal 1000 SMS-berichten of ontvangst van too1000 inkomende stem minuten, afhankelijk van de locatie van uw telefoon en bericht- of aanroep bestemming Hallo).</span><span class="sxs-lookup"><span data-stu-id="5c61a-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="5c61a-119">Deze Twilio-tegoed inwisselen en aan de slag op [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="5c61a-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="5c61a-120">Twilio is een betalen naar gebruik service.</span><span class="sxs-lookup"><span data-stu-id="5c61a-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="5c61a-121">Er zijn geen kosten instellen en kunt u uw account op elk moment sluiten.</span><span class="sxs-lookup"><span data-stu-id="5c61a-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="5c61a-122">U vindt meer informatie op [Twilio prijzen](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="5c61a-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="5c61a-123"><a id="Concepts"></a>Concepten</span><span class="sxs-lookup"><span data-stu-id="5c61a-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="5c61a-124">Hallo Twilio-API is een RESTful-API met stem en SMS-functionaliteit voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5c61a-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="5c61a-125">Clientbibliotheken zijn beschikbaar in meerdere talen. Zie voor een lijst [Twilio-API-bibliotheken][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="5c61a-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="5c61a-126">Belangrijke aspecten van Hallo Twilio-API zijn Twilio-termen en Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="5c61a-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="5c61a-127"><a id="Verbs"></a>Twilio-termen</span><span class="sxs-lookup"><span data-stu-id="5c61a-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="5c61a-128">Hallo API wordt gebruikgemaakt van Twilio termen; bijvoorbeeld, Hallo  **&lt;zeg&gt;**  term Hiermee Twilio tooaudibly afleveren geeft een bericht op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="5c61a-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="5c61a-129">Hallo Hieronder volgt een lijst met Twilio-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5c61a-129">hello following is a list of Twilio verbs.</span></span>  <span data-ttu-id="5c61a-130">Meer informatie over Hallo andere termen en mogelijkheden via [Twilio Markup Language documentatie](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="5c61a-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="5c61a-131">**&lt;Externe&gt;**: Hallo aanroeper tooanother telefoon verbindt.</span><span class="sxs-lookup"><span data-stu-id="5c61a-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="5c61a-132">**&lt;Verzamel&gt;**: cijfers ingevoerd op het telefoonnummer Hallo verzamelt.</span><span class="sxs-lookup"><span data-stu-id="5c61a-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="5c61a-133">**&lt;Ophangen&gt;**: een aanroep wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="5c61a-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="5c61a-134">**&lt;Afspelen&gt;**: een geluidsbestand afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="5c61a-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="5c61a-135">**&lt;Onderbreken&gt;**: achtergrond wacht op een opgegeven aantal seconden.</span><span class="sxs-lookup"><span data-stu-id="5c61a-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="5c61a-136">**&lt;Record&gt;**: Hallo aanroeper stem registreert en retourneert een URL van een bestand dat Hallo opname bevat.</span><span class="sxs-lookup"><span data-stu-id="5c61a-136">**&lt;Record&gt;**: Records hello caller's voice and returns an URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="5c61a-137">**&lt;Omleiden&gt;**: draagt de controle van een telefoongesprek of SMS toohello TwiML op een andere URL.</span><span class="sxs-lookup"><span data-stu-id="5c61a-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="5c61a-138">**&lt;Afwijzen&gt;**: geweigerd een binnenkomende tooyour Twilio nummer bellen zonder u facturering</span><span class="sxs-lookup"><span data-stu-id="5c61a-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="5c61a-139">**&lt;Zeg&gt;**: zet tekst toospeech die wordt gemaakt op een aanroep.</span><span class="sxs-lookup"><span data-stu-id="5c61a-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="5c61a-140">**&lt;SMS&gt;**: een SMS-bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="5c61a-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="5c61a-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="5c61a-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="5c61a-142">TwiML is een reeks XML gebaseerde instructies op basis van Hallo Twilio-termen die Twilio van hoe u informeren over tooprocess een telefoongesprek of SMS.</span><span class="sxs-lookup"><span data-stu-id="5c61a-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="5c61a-143">Als u bijvoorbeeld Hallo TwiML na Hallo tekst wilt converteren **Hallo wereld** toospeech.</span><span class="sxs-lookup"><span data-stu-id="5c61a-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="5c61a-144">Bij het aanroepen van uw toepassing hello Twilio-API, is een van de API-parameters Hallo Hallo-URL die Hallo TwiML antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5c61a-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="5c61a-145">U kunt voor ontwikkelingsdoeleinden Twilio geleverde URL's tooprovide hello TwiML antwoorden die wordt gebruikt door uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5c61a-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="5c61a-146">U ook uw eigen URL's tooproduce hello TwiML reacties kan hosten en een andere optie is toouse hello **TwiMLResponse** object.</span><span class="sxs-lookup"><span data-stu-id="5c61a-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="5c61a-147">Zie voor meer informatie over Twilio-termen, hun kenmerken en TwiML [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="5c61a-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="5c61a-148">Zie voor meer informatie over Hallo Twilio-API, [Twilio-API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="5c61a-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="5c61a-149"><a id="CreateAccount"></a>Een Twilio-Account maken</span><span class="sxs-lookup"><span data-stu-id="5c61a-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="5c61a-150">Wanneer u klaar tooget een Twilio-account bent, aanmelden op [probeer Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="5c61a-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="5c61a-151">U kunt beginnen met een gratis account en upgrade van uw account later.</span><span class="sxs-lookup"><span data-stu-id="5c61a-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="5c61a-152">Wanneer u zich voor een Twilio-account aanmeldt, ontvangt u een account-ID en geen verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="5c61a-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="5c61a-153">Beide worden benodigde toomake Twilio-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="5c61a-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="5c61a-154">tooprevent onbevoegde toegang tot tooyour account, het verificatietoken te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="5c61a-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="5c61a-155">Uw account-ID en verificatie token kunnen worden bekeken op Hallo [Twilio-accountpagina][twilio_account]in velden met het label Hallo **ACCOUNT-SID** en **AUTH TOKEN**respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="5c61a-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="5c61a-156"><a id="create_app"></a>Een Azure-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="5c61a-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="5c61a-157">Een Azure-toepassing die als host fungeert voor een toepassing Twilio ingeschakeld is niet anders als elke andere Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5c61a-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="5c61a-158">U Hallo Twilio .NET-bibliotheek toevoegen en configureren van Hallo rol toouse hello Twilio .NET-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="5c61a-158">You add hello Twilio .NET library and configure hello role toouse hello Twilio .NET libraries.</span></span>
<span data-ttu-id="5c61a-159">Zie voor meer informatie over het maken van een eerste Azure-project [een Azure-project maken met Visual Studio][vs_project].</span><span class="sxs-lookup"><span data-stu-id="5c61a-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="5c61a-160"><a id="configure_app"></a>Configureren van uw toepassing toouse Twilio-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="5c61a-160"><a id="configure_app"></a>Configure Your Application toouse Twilio Libraries</span></span>
<span data-ttu-id="5c61a-161">Twilio biedt een reeks .NET helper-bibliotheken die verschillende aspecten van Twilio tooprovide eenvoudig en gemakkelijk manieren toointeract met Hallo Twilio REST-API en Twilio Client teruglopen toogenerate TwiML reacties.</span><span class="sxs-lookup"><span data-stu-id="5c61a-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio tooprovide simple and easy ways toointeract with hello Twilio REST API and Twilio Client toogenerate TwiML responses.</span></span>

<span data-ttu-id="5c61a-162">Twilio bevat vijf bibliotheken voor .NET-ontwikkelaars:</span><span class="sxs-lookup"><span data-stu-id="5c61a-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="5c61a-163">Bibliotheek</span><span class="sxs-lookup"><span data-stu-id="5c61a-163">Library</span></span>|<span data-ttu-id="5c61a-164">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5c61a-164">Description</span></span>
---|---
<span data-ttu-id="5c61a-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="5c61a-165">Twilio.API</span></span>|<span data-ttu-id="5c61a-166">Hallo core Twilio-bibliotheek die Hallo Twilio REST-API in een beschrijvende .NET-bibliotheek terugloopt.</span><span class="sxs-lookup"><span data-stu-id="5c61a-166">hello core Twilio library that wraps hello Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="5c61a-167">Deze bibliotheek is beschikbaar voor .NET, Silverlight en Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="5c61a-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="5c61a-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="5c61a-168">Twilio.TwiML</span></span>|<span data-ttu-id="5c61a-169">Biedt een .NET gebruiksvriendelijke manier toogenerate TwiML aantekeningen.</span><span class="sxs-lookup"><span data-stu-id="5c61a-169">Provides a .NET friendly way toogenerate TwiML markup.</span></span>
<span data-ttu-id="5c61a-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="5c61a-170">Twilio.MVC</span></span>|<span data-ttu-id="5c61a-171">Voor ontwikkelaars met ASP.NET MVC, bevat deze bibliotheek een TwilioController, TwiML ActionResult en aanvraag validatiekenmerk.</span><span class="sxs-lookup"><span data-stu-id="5c61a-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="5c61a-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="5c61a-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="5c61a-173">Deze bibliotheek bevat voor ontwikkelaars met ontwikkelsysteem van Microsoft gratis WebMatrix, Razor syntaxis van de hulpprogramma's voor verschillende Twilio-acties.</span><span class="sxs-lookup"><span data-stu-id="5c61a-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="5c61a-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="5c61a-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="5c61a-175">Hallo mogelijkheid token generator voor gebruik met Hallo Twilio Client JavaScript SDK bevat.</span><span class="sxs-lookup"><span data-stu-id="5c61a-175">Contains hello Capability token generator for use with hello Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="5c61a-176">Houd er rekening mee dat alle bibliotheken .NET 3.5, Silverlight 4 of Windows Phone 7 of hoger vereist.</span><span class="sxs-lookup"><span data-stu-id="5c61a-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="5c61a-177">Hallo voorbeelden in deze handleiding Hallo Twilio.API bibliotheek gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5c61a-177">hello samples provided in this guide use hello Twilio.API library.</span></span>

<span data-ttu-id="5c61a-178">Hallo-bibliotheken mag [geïnstalleerd met behulp van Hallo NuGet package manager extensie](http://www.twilio.com/docs/csharp/install) beschikbaar is voor Visual Studio 2010 up too2015.</span><span class="sxs-lookup"><span data-stu-id="5c61a-178">hello libraries can be [installed using hello NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up too2015.</span></span>  <span data-ttu-id="5c61a-179">Hallo broncode op wordt gehost [GitHub][twilio_github_repo], waaronder een Wiki met volledige documentatie voor het gebruik van Hallo-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="5c61a-179">hello source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using hello libraries.</span></span>

<span data-ttu-id="5c61a-180">Microsoft Visual Studio 2010 installeert standaard versie 1.2 van NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c61a-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="5c61a-181">Hallo Twilio-bibliotheken installeren vereist versie 1.6 van NuGet of hoger.</span><span class="sxs-lookup"><span data-stu-id="5c61a-181">Installing hello Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="5c61a-182">Zie voor meer informatie over het installeren of bijwerken van NuGet [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="5c61a-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="5c61a-183">tooinstall hello meest recente versie van NuGet, moet u eerst Hallo geladen versie met behulp van Visual Studio-extensie Manager Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5c61a-183">tooinstall hello latest version of NuGet, you must first uninstall hello loaded version using hello Visual Studio Extension Manager.</span></span> <span data-ttu-id="5c61a-184">toodo geval is, moet u Visual Studio uitvoeren als administrator.</span><span class="sxs-lookup"><span data-stu-id="5c61a-184">toodo so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="5c61a-185">Anders wordt is de knop verwijderen Hallo uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5c61a-185">Otherwise, hello Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="5c61a-186"><a id="use_nuget"></a>tooadd hello Twilio-bibliotheken tooyour Visual Studio-project:</span><span class="sxs-lookup"><span data-stu-id="5c61a-186"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour Visual Studio project:</span></span>
1. <span data-ttu-id="5c61a-187">Open uw oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c61a-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="5c61a-188">Met de rechtermuisknop op **verwijzingen**.</span><span class="sxs-lookup"><span data-stu-id="5c61a-188">Right-click **References**.</span></span>
3. <span data-ttu-id="5c61a-189">Klik op **NuGet-pakketten beheren...**</span><span class="sxs-lookup"><span data-stu-id="5c61a-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="5c61a-190">Klik op **Online**.</span><span class="sxs-lookup"><span data-stu-id="5c61a-190">Click **Online**.</span></span>
5. <span data-ttu-id="5c61a-191">Typ in de online zoekvak hello, *twilio*.</span><span class="sxs-lookup"><span data-stu-id="5c61a-191">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="5c61a-192">Klik op **installeren** op Hallo Twilio-pakket.</span><span class="sxs-lookup"><span data-stu-id="5c61a-192">Click **Install** on hello Twilio package.</span></span>

## <span data-ttu-id="5c61a-193"><a id="howto_make_call"></a>Procedure: een uitgaande aanroep</span><span class="sxs-lookup"><span data-stu-id="5c61a-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="5c61a-194">Hallo hieronder ziet u hoe een uitgaande toomake-gesprek Hallo **CallResource** klasse.</span><span class="sxs-lookup"><span data-stu-id="5c61a-194">hello following shows how toomake an outgoing call using hello **CallResource** class.</span></span> <span data-ttu-id="5c61a-195">Deze code wordt een Twilio-voorwaarde site tooreturn hello Twilio Markup Language (TwiML) antwoord.</span><span class="sxs-lookup"><span data-stu-id="5c61a-195">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="5c61a-196">Vervang uw waarden voor Hallo **naar** en **van** telefoonnummers, en zorg ervoor dat u controleert of Hallo **van** telefoonnummer voor uw Twilio-account voordat Hallo code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5c61a-196">Substitute your values for hello **to** and **from** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account before running hello code.</span></span>

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

<span data-ttu-id="5c61a-197">Voor meer informatie over Hallo parameters doorgegeven toohello **CallResource.Create** methode, Zie [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="5c61a-197">For more information about hello parameters passed in toohello **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="5c61a-198">Zoals gezegd, gebruikt deze code een Twilio-voorwaarde site tooreturn hello TwiML antwoord.</span><span class="sxs-lookup"><span data-stu-id="5c61a-198">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="5c61a-199">U kunt in plaats hiervan uw eigen site tooprovide hello TwiML antwoord.</span><span class="sxs-lookup"><span data-stu-id="5c61a-199">You could instead use your own site tooprovide hello TwiML response.</span></span> <span data-ttu-id="5c61a-200">Zie voor meer informatie [hoe: bieden TwiML reacties van uw eigen website](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="5c61a-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="5c61a-201"><a id="howto_send_sms"></a>Procedure: een SMS-bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="5c61a-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="5c61a-202">Hallo volgende schermafbeelding ziet u hoe een SMS-bericht met toosend Hallo **MessageResource** klasse.</span><span class="sxs-lookup"><span data-stu-id="5c61a-202">hello following screenshot shows how toosend an SMS message using hello **MessageResource**  class.</span></span> <span data-ttu-id="5c61a-203">Hallo **van** nummer wordt geleverd door Twilio voor proefversie accounts toosend SMS-berichten.</span><span class="sxs-lookup"><span data-stu-id="5c61a-203">hello **from** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="5c61a-204">Hallo **naar** nummer voor uw Twilio-account moet worden geverifieerd voordat u Hallo code uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5c61a-204">hello **to** number must be verified for your Twilio account before you run hello code.</span></span>

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

## <span data-ttu-id="5c61a-205"><a id="howto_provide_twiml_responses"></a>Hoe: TwiML reacties van uw eigen website opgeven</span><span class="sxs-lookup"><span data-stu-id="5c61a-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="5c61a-206">Wanneer uw toepassing initieert een aanroep van toohello Twilio-API - bijvoorbeeld via Hallo **CallResource.Create** methode - Twilio stuurt de aanvraag-URL voor tooan die verwachte tooreturn is een antwoord TwiML.</span><span class="sxs-lookup"><span data-stu-id="5c61a-206">When your application initiates a call toohello Twilio API - for example, via hello **CallResource.Create** method - Twilio sends your request tooan URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="5c61a-207">Hallo-voorbeeld in [hoe: geen uitgaande aanroep doen](#howto_make_call) gebruikt Hallo Twilio-geleverde URL [http://twimlets.com/message] [ twimlet_message_url] tooreturn Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="5c61a-207">hello example in [How to: Make an outgoing call](#howto_make_call) uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] tooreturn hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="5c61a-208">Hoewel TwiML is ontworpen voor gebruik door webservices, kunt u Hallo TwiML kunt weergeven in uw browser.</span><span class="sxs-lookup"><span data-stu-id="5c61a-208">While TwiML is designed for use by web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="5c61a-209">Bijvoorbeeld, klik op [http://twimlets.com/message] [ twimlet_message_url] toosee een lege &lt;antwoord&gt; element; Klik bijvoorbeeld op [http://twimlets.com/message ? Bericht % 5B0 %5, D = Hallo % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee een &lt;antwoord&gt; element met een &lt;zeg&gt; element.</span><span class="sxs-lookup"><span data-stu-id="5c61a-209">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="5c61a-210">In plaats van te vertrouwen op Hallo geleverde Twilio-URL, kunt u uw eigen website URL waarmee HTTP-antwoorden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5c61a-210">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="5c61a-211">U kunt Hallo site maken in een andere taal waarmee HTTP-antwoorden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5c61a-211">You can create hello site in any language that returns HTTP responses.</span></span> <span data-ttu-id="5c61a-212">In dit onderwerp wordt ervan uitgegaan dat u Hallo-URL van een algemene ASP.NET-handler moet worden gehost.</span><span class="sxs-lookup"><span data-stu-id="5c61a-212">This topic assumes you'll be hosting hello URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="5c61a-213">Hallo na ASP.NET-Handler een antwoord TwiML waarin staat dat crafts **Hallo wereld** op Hallo-aanroep.</span><span class="sxs-lookup"><span data-stu-id="5c61a-213">hello following ASP.NET Handler crafts a TwiML response that says **Hello World** on hello call.</span></span>

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
    
<span data-ttu-id="5c61a-214">Zoals u in de bovenstaande Hallo voorbeeld zien kunt, is het Hallo TwiML antwoord gewoon een XML-document.</span><span class="sxs-lookup"><span data-stu-id="5c61a-214">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="5c61a-215">Hallo Twilio.TwiML bibliotheek bevat de klassen die voor u TwiML genereren.</span><span class="sxs-lookup"><span data-stu-id="5c61a-215">hello Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="5c61a-216">Hallo onderstaand voorbeeld gelijkwaardige antwoord Hallo produceert, zoals hierboven beschreven, maar gebruikt Hallo **VoiceResponse** klasse.</span><span class="sxs-lookup"><span data-stu-id="5c61a-216">hello example below produces hello equivalent response as shown above, but uses hello **VoiceResponse** class.</span></span>

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

<span data-ttu-id="5c61a-217">Zie voor meer informatie over TwiML [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="5c61a-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="5c61a-218">Nadat u een manier tooprovide TwiML antwoorden hebt ingesteld, kunt u die URL toohello doorgeven **CallResource.Create** methode.</span><span class="sxs-lookup"><span data-stu-id="5c61a-218">Once you have set up a way tooprovide TwiML responses, you can pass that URL toohello **CallResource.Create** method.</span></span> <span data-ttu-id="5c61a-219">Bijvoorbeeld, als u een webtoepassing met de naam MyTwiML geïmplementeerd tooan Azure-cloudservice hebt en Hallo-naam van uw ASP.NET-Handler mytwiml.ashx is, Hallo-URL kan worden doorgegeven te**CallResource.Create** zoals weergegeven in de volgende code Hallo Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5c61a-219">For example, if you have a web application named MyTwiML deployed tooan Azure cloud service, and hello name of your ASP.NET Handler is mytwiml.ashx, hello URL can be passed too**CallResource.Create** as shown in hello following code sample:</span></span>

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="5c61a-220">Zie voor meer informatie over het gebruik van Twilio in Azure met ASP.NET [hoe toomake een telefoon aanroepen in een Webrol in Azure met behulp van Twilio][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="5c61a-220">For additional information about using Twilio on Azure with ASP.NET, see [How toomake a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

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
