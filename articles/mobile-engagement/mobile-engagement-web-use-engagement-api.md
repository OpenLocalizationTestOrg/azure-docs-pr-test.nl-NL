---
title: Azure Mobile Engagement Web SDK-API's | Microsoft Docs
description: De nieuwste updates en procedures voor de webservice-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="848f8-103">Gebruik de API van Azure Mobile Engagement in een webtoepassing</span><span class="sxs-lookup"><span data-stu-id="848f8-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="848f8-104">Dit document is een aanvulling op het document dat wordt bepaald hoe naar [Mobile Engagement integreren in een webtoepassing](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="848f8-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="848f8-105">Het biedt gedetailleerde informatie over het gebruik van de Azure Mobile Engagement-API voor het rapporteren van de toepassingsstatistieken van uw.</span><span class="sxs-lookup"><span data-stu-id="848f8-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="848f8-106">De Mobile Engagement-API wordt geleverd door de `engagement.agent` object.</span><span class="sxs-lookup"><span data-stu-id="848f8-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="848f8-107">De Azure Mobile Engagement Web SDK alias is standaard `engagement`.</span><span class="sxs-lookup"><span data-stu-id="848f8-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="848f8-108">U kunt deze alias van de SDK-configuratie opnieuw definiëren.</span><span class="sxs-lookup"><span data-stu-id="848f8-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="848f8-109">Mobile Engagement-concepten</span><span class="sxs-lookup"><span data-stu-id="848f8-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="848f8-110">De volgende onderdelen verfijnen algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md) voor de webplatform.</span><span class="sxs-lookup"><span data-stu-id="848f8-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="848f8-111">`Session` en `Activity`</span><span class="sxs-lookup"><span data-stu-id="848f8-111">`Session` and `Activity`</span></span>
<span data-ttu-id="848f8-112">Als de gebruiker blijft niet-actief is gedurende meer dan een paar seconden tussen twee activiteiten, wordt de volgorde van de gebruiker van activiteiten splitsen in twee verschillende sessies.</span><span class="sxs-lookup"><span data-stu-id="848f8-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="848f8-113">Deze enkele seconden worden de sessietime-out genoemd.</span><span class="sxs-lookup"><span data-stu-id="848f8-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="848f8-114">Als uw webtoepassing het einde van de activiteiten van de gebruiker niet zelfstandig declareren (door het aanroepen van de `engagement.agent.endActivity` functie), verloopt de Mobile Engagement-server automatisch de gebruikerssessie binnen drie minuten nadat de pagina van de toepassing is gesloten.</span><span class="sxs-lookup"><span data-stu-id="848f8-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="848f8-115">Dit wordt de sessietime-out van server genoemd.</span><span class="sxs-lookup"><span data-stu-id="848f8-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="848f8-116">Geautomatiseerde rapporten over niet-onderschepte JavaScript-uitzonderingen worden standaard niet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="848f8-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="848f8-117">U kunt echter crashes rapporteren handmatig met behulp van de `sendCrash` (Zie de sectie op reporting crashes).</span><span class="sxs-lookup"><span data-stu-id="848f8-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="848f8-118">Rapportage</span><span class="sxs-lookup"><span data-stu-id="848f8-118">Reporting activities</span></span>
<span data-ttu-id="848f8-119">Rapportage van gebruikersactiviteit omvat zodra een gebruiker een nieuwe activiteit en wanneer de gebruiker de huidige activiteit wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="848f8-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="848f8-120">Gebruiker start een nieuwe activiteit</span><span class="sxs-lookup"><span data-stu-id="848f8-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="848f8-121">U moet aan te roepen `startActivity()` elke gebruikersactiviteit tijd wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="848f8-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="848f8-122">De eerste aanroep van deze functie wordt een nieuwe gebruikerssessie gestart.</span><span class="sxs-lookup"><span data-stu-id="848f8-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="848f8-123">Gebruiker eindigt de huidige activiteit</span><span class="sxs-lookup"><span data-stu-id="848f8-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="848f8-124">U moet aan te roepen `endActivity()` ten minste eenmaal wanneer de gebruiker is voltooid, de laatste activiteit.</span><span class="sxs-lookup"><span data-stu-id="848f8-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="848f8-125">Dit informeert de Mobile Engagement Web SDK dat de gebruiker die momenteel niet actief is en dat de sessie van de gebruiker moet worden gesloten nadat de sessietime-out is verlopen.</span><span class="sxs-lookup"><span data-stu-id="848f8-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="848f8-126">Als u aanroept `startActivity()` voordat de sessietime-out is verlopen, wordt de sessie gewoon hervat.</span><span class="sxs-lookup"><span data-stu-id="848f8-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="848f8-127">Omdat er geen betrouwbare aanroep is voor wanneer de navigator-venster wordt gesloten, is het vaak moeilijk of onmogelijk om af te vangen het einde van de activiteiten van de gebruiker binnen een omgeving.</span><span class="sxs-lookup"><span data-stu-id="848f8-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="848f8-128">Daarom wordt de Mobile Engagement-server automatisch verloopt de sessie van de gebruiker binnen drie minuten nadat de pagina van de toepassing is gesloten.</span><span class="sxs-lookup"><span data-stu-id="848f8-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="848f8-129">Melden van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="848f8-129">Reporting events</span></span>
<span data-ttu-id="848f8-130">Rapportage over gebeurtenissen behandelt sessiegebeurtenissen en zelfstandige gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="848f8-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="848f8-131">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="848f8-131">Session events</span></span>
<span data-ttu-id="848f8-132">Sessiegebeurtenissen worden meestal gebruikt voor het rapporteren van de acties die worden uitgevoerd door een gebruiker tijdens de sessie van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="848f8-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="848f8-133">**Voorbeeld zonder extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="848f8-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="848f8-134">**Voorbeeld met extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="848f8-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="848f8-135">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="848f8-135">Standalone events</span></span>
<span data-ttu-id="848f8-136">In tegenstelling tot sessiegebeurtenissen, kunnen zelfstandige gebeurtenissen plaatsvinden buiten de context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="848f8-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="848f8-137">Gebruik voor die ``engagement.agent.sendEvent`` in plaats van ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="848f8-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="848f8-138">Rapportage van fouten</span><span class="sxs-lookup"><span data-stu-id="848f8-138">Reporting errors</span></span>
<span data-ttu-id="848f8-139">Rapportage van fouten bevat informatie over fouten in sessie en zelfstandige.</span><span class="sxs-lookup"><span data-stu-id="848f8-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="848f8-140">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="848f8-140">Session errors</span></span>
<span data-ttu-id="848f8-141">Sessie-fouten worden gewoonlijk gebruikt voor het rapporteren van de fouten die een invloed op de gebruiker tijdens de sessie van de gebruiker hebben.</span><span class="sxs-lookup"><span data-stu-id="848f8-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="848f8-142">**Voorbeeld zonder extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="848f8-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="848f8-143">**Voorbeeld met extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="848f8-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="848f8-144">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="848f8-144">Standalone errors</span></span>
<span data-ttu-id="848f8-145">In tegenstelling tot sessie fouten, kunnen zelfstandige fouten optreden buiten de context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="848f8-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="848f8-146">Gebruik voor die `engagement.agent.sendError` in plaats van `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="848f8-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="848f8-147">Rapportage van taken</span><span class="sxs-lookup"><span data-stu-id="848f8-147">Reporting jobs</span></span>
<span data-ttu-id="848f8-148">Rapportage van taken dekt rapportage van fouten en gebeurtenissen die zich tijdens een taak voordoen en de rapportage van crashes.</span><span class="sxs-lookup"><span data-stu-id="848f8-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="848f8-149">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="848f8-149">**Example:**</span></span>

<span data-ttu-id="848f8-150">Als u bewaken van een AJAX-aanvraag wilt, gebruikt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="848f8-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="848f8-151">Rapportage van fouten tijdens een taak</span><span class="sxs-lookup"><span data-stu-id="848f8-151">Reporting errors during a job</span></span>
<span data-ttu-id="848f8-152">Fouten kunnen zijn gerelateerd aan een actieve taak in plaats van aan de huidige gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="848f8-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="848f8-153">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="848f8-153">**Example:**</span></span>

<span data-ttu-id="848f8-154">Als u een fout gemeld wilt als een AJAX-aanvraag is mislukt:</span><span class="sxs-lookup"><span data-stu-id="848f8-154">If you want to report an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="848f8-155">Melden van gebeurtenissen gedurende een project</span><span class="sxs-lookup"><span data-stu-id="848f8-155">Reporting events during a job</span></span>
<span data-ttu-id="848f8-156">Gebeurtenissen kunnen zijn gerelateerd aan een actieve taak in plaats van aan de huidige gebruikerssessie dank aan de `engagement.agent.sendJobEvent` functie.</span><span class="sxs-lookup"><span data-stu-id="848f8-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="848f8-157">Deze functie werkt precies hetzelfde als `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="848f8-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="848f8-158">Reporting crashes</span><span class="sxs-lookup"><span data-stu-id="848f8-158">Reporting crashes</span></span>
<span data-ttu-id="848f8-159">Gebruik de `sendCrash` functie voor het rapport handmatig is vastgelopen.</span><span class="sxs-lookup"><span data-stu-id="848f8-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="848f8-160">De `crashid` een tekenreeks die welk type crash aangeeft is.</span><span class="sxs-lookup"><span data-stu-id="848f8-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="848f8-161">De `crash` -argument is meestal de stacktracering van de crash als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="848f8-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="848f8-162">Extra parameters</span><span class="sxs-lookup"><span data-stu-id="848f8-162">Extra parameters</span></span>
<span data-ttu-id="848f8-163">U kunt willekeurige gegevens koppelen aan een gebeurtenis, fout, activiteit of taak.</span><span class="sxs-lookup"><span data-stu-id="848f8-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="848f8-164">De gegevens kan niet een JSON-object (maar niet een matrix of primitief type).</span><span class="sxs-lookup"><span data-stu-id="848f8-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="848f8-165">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="848f8-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="848f8-166">Limieten</span><span class="sxs-lookup"><span data-stu-id="848f8-166">Limits</span></span>
<span data-ttu-id="848f8-167">Grenzen die op extra parameters van toepassing zijn op het gebied van reguliere expressies voor sleutels, waardetypen en grootte.</span><span class="sxs-lookup"><span data-stu-id="848f8-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="848f8-168">Sleutels</span><span class="sxs-lookup"><span data-stu-id="848f8-168">Keys</span></span>
<span data-ttu-id="848f8-169">Elke sleutel in het object moet overeenkomen met de volgende reguliere expressie:</span><span class="sxs-lookup"><span data-stu-id="848f8-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="848f8-170">Dit betekent dat sleutels moeten beginnen met ten minste één letter gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="848f8-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="848f8-171">Waarden</span><span class="sxs-lookup"><span data-stu-id="848f8-171">Values</span></span>
<span data-ttu-id="848f8-172">Waarden zijn beperkt tot tekenreeks, het aantal en Booleaanse typen.</span><span class="sxs-lookup"><span data-stu-id="848f8-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="848f8-173">Grootte</span><span class="sxs-lookup"><span data-stu-id="848f8-173">Size</span></span>
<span data-ttu-id="848f8-174">Extra's zijn beperkt tot 1024 tekens per aanroep (nadat de Mobile Engagement Web SDK coderen van deze in JSON).</span><span class="sxs-lookup"><span data-stu-id="848f8-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="848f8-175">Rapportage-toepassingsinformatie</span><span class="sxs-lookup"><span data-stu-id="848f8-175">Reporting application information</span></span>
<span data-ttu-id="848f8-176">U kunt handmatig rapporteren voor het bijhouden van gegevens (of andere toepassingsspecifieke gegevens) met behulp van de `sendAppInfo()` functie.</span><span class="sxs-lookup"><span data-stu-id="848f8-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="848f8-177">Houd er rekening mee dat deze gegevens stapsgewijs kunnen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="848f8-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="848f8-178">Alleen de meest recente waarde voor een specifieke sleutel wordt bewaard voor een specifiek apparaat.</span><span class="sxs-lookup"><span data-stu-id="848f8-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="848f8-179">Als gebeurtenis extra's, kunt u een JSON-object om toepassingsinformatie.</span><span class="sxs-lookup"><span data-stu-id="848f8-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="848f8-180">Houd er rekening mee dat matrices of onderliggende objecten worden behandeld als platte tekenreeksen (met behulp van de JSON-serialisatie).</span><span class="sxs-lookup"><span data-stu-id="848f8-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="848f8-181">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="848f8-181">**Example:**</span></span>

<span data-ttu-id="848f8-182">Hier volgt een voorbeeld van code voor het verzenden van de gebruiker geslacht en Geboortedatum:</span><span class="sxs-lookup"><span data-stu-id="848f8-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="848f8-183">Limieten</span><span class="sxs-lookup"><span data-stu-id="848f8-183">Limits</span></span>
<span data-ttu-id="848f8-184">Limieten die van toepassing op toepassingsgegevens zijn op het gebied van reguliere expressies voor sleutels en grootte.</span><span class="sxs-lookup"><span data-stu-id="848f8-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="848f8-185">Sleutels</span><span class="sxs-lookup"><span data-stu-id="848f8-185">Keys</span></span>
<span data-ttu-id="848f8-186">Elke sleutel in het object moet overeenkomen met de volgende reguliere expressie:</span><span class="sxs-lookup"><span data-stu-id="848f8-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="848f8-187">Dit betekent dat sleutels moeten beginnen met ten minste één letter gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="848f8-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="848f8-188">Grootte</span><span class="sxs-lookup"><span data-stu-id="848f8-188">Size</span></span>
<span data-ttu-id="848f8-189">Toepassingsinformatie is beperkt tot 1024 tekens per aanroep (nadat de Mobile Engagement Web SDK coderen van deze in JSON).</span><span class="sxs-lookup"><span data-stu-id="848f8-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="848f8-190">In het voorgaande voorbeeld is de JSON naar de server verzonden 44 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="848f8-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
