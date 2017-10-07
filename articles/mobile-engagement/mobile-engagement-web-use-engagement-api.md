---
title: Mobile Engagement Web SDK-API's aaaAzure | Microsoft Docs
description: meest recente updates en procedures voor het Hallo Web SDK voor Azure Mobile Engagement Hallo
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
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="24961-103">Hello Azure Mobile Engagement-API in een webtoepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="24961-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="24961-104">Dit document is een toevoeging toohello document dat hoe te aangeeft[Mobile Engagement integreren in een webtoepassing](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="24961-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="24961-105">Het biedt gedetailleerde informatie over hoe toouse API van Azure Mobile Engagement tooreport Hallo de toepassingsstatistieken van uw.</span><span class="sxs-lookup"><span data-stu-id="24961-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="24961-106">Hallo Mobile Engagement API geleverd door Hallo `engagement.agent` object.</span><span class="sxs-lookup"><span data-stu-id="24961-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="24961-107">Azure Mobile Engagement Web SDK alias wordt Hallo `engagement`.</span><span class="sxs-lookup"><span data-stu-id="24961-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="24961-108">U kunt deze alias uit Hallo SDK-configuratie opnieuw definiëren.</span><span class="sxs-lookup"><span data-stu-id="24961-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="24961-109">Mobile Engagement-concepten</span><span class="sxs-lookup"><span data-stu-id="24961-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="24961-110">Hallo volgende delen verfijnen algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md) voor Hallo webplatform.</span><span class="sxs-lookup"><span data-stu-id="24961-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="24961-111">`Session` en `Activity`</span><span class="sxs-lookup"><span data-stu-id="24961-111">`Session` and `Activity`</span></span>
<span data-ttu-id="24961-112">Als Hallo gebruiker actief gedurende meer dan een paar seconden tussen twee activiteiten blijft, is hello volgorde van activiteiten van de gebruiker opgesplitst in twee verschillende sessies.</span><span class="sxs-lookup"><span data-stu-id="24961-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="24961-113">Deze enkele seconden heten Hallo sessietime-out.</span><span class="sxs-lookup"><span data-stu-id="24961-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="24961-114">Als uw webtoepassing Hallo einde van de activiteiten van de gebruiker niet zelfstandig declareren (door de aanroepende Hallo `engagement.agent.endActivity` functie), Hallo Mobile Engagement server verloopt automatisch Hallo gebruikerssessie binnen drie minuten nadat de pagina van de toepassing hello is gesloten.</span><span class="sxs-lookup"><span data-stu-id="24961-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="24961-115">Dit wordt Hallo server sessietime-out genoemd.</span><span class="sxs-lookup"><span data-stu-id="24961-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="24961-116">Geautomatiseerde rapporten over niet-onderschepte JavaScript-uitzonderingen worden standaard niet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="24961-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="24961-117">U kunt echter crashes rapporteren handmatig met behulp van Hallo `sendCrash` (Zie de sectie Hallo op reporting crashes).</span><span class="sxs-lookup"><span data-stu-id="24961-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="24961-118">Rapportage</span><span class="sxs-lookup"><span data-stu-id="24961-118">Reporting activities</span></span>
<span data-ttu-id="24961-119">Rapportage van gebruikersactiviteit omvat zodra een gebruiker een nieuwe activiteit en wanneer gebruiker Hallo Hallo huidige activiteit wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="24961-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="24961-120">Gebruiker start een nieuwe activiteit</span><span class="sxs-lookup"><span data-stu-id="24961-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="24961-121">U moet toocall `startActivity()` elke gebruikersactiviteit tijd wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="24961-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="24961-122">Hallo eerste aanroep toothis functie wordt een nieuwe gebruikerssessie gestart.</span><span class="sxs-lookup"><span data-stu-id="24961-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="24961-123">Gebruiker eindigt Hallo huidige activiteit</span><span class="sxs-lookup"><span data-stu-id="24961-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="24961-124">U moet toocall `endActivity()` ten minste eenmaal wanneer Hallo gebruiker is voltooid, de laatste activiteit.</span><span class="sxs-lookup"><span data-stu-id="24961-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="24961-125">Dit informeert Hallo Mobile Engagement Web SDK dat Hallo gebruiker momenteel niet actief is en dat de gebruikerssessie Hallo toobe moet gesloten nadat Hallo sessietime-out is verlopen.</span><span class="sxs-lookup"><span data-stu-id="24961-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="24961-126">Als u aanroept `startActivity()` voordat Hallo sessietime-out is verlopen, Hallo sessie gewoon is hervat.</span><span class="sxs-lookup"><span data-stu-id="24961-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="24961-127">Omdat er geen betrouwbare aanroep is voor als Hallo navigator-venster is gesloten, is het vaak moeilijk of onmogelijk toocatch Hallo einde van de activiteiten van de gebruiker binnen een omgeving.</span><span class="sxs-lookup"><span data-stu-id="24961-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="24961-128">Dat is waarom Mobile Engagement server verloopt automatisch Hallo Hallo gebruikerssessie binnen drie minuten nadat de pagina van de toepassing hello is gesloten.</span><span class="sxs-lookup"><span data-stu-id="24961-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="24961-129">Melden van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="24961-129">Reporting events</span></span>
<span data-ttu-id="24961-130">Rapportage over gebeurtenissen behandelt sessiegebeurtenissen en zelfstandige gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="24961-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="24961-131">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="24961-131">Session events</span></span>
<span data-ttu-id="24961-132">Sessiegebeurtenissen zijn meestal gebruikte tooreport Hallo bewerkingen worden uitgevoerd door een gebruiker tijdens Hallo gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="24961-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="24961-133">**Voorbeeld zonder extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="24961-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="24961-134">**Voorbeeld met extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="24961-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="24961-135">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="24961-135">Standalone events</span></span>
<span data-ttu-id="24961-136">In tegenstelling tot sessiegebeurtenissen, kunnen zelfstandige gebeurtenissen plaatsvinden buiten Hallo context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="24961-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="24961-137">Gebruik voor die ``engagement.agent.sendEvent`` in plaats van ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="24961-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="24961-138">Rapportage van fouten</span><span class="sxs-lookup"><span data-stu-id="24961-138">Reporting errors</span></span>
<span data-ttu-id="24961-139">Rapportage van fouten bevat informatie over fouten in sessie en zelfstandige.</span><span class="sxs-lookup"><span data-stu-id="24961-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="24961-140">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="24961-140">Session errors</span></span>
<span data-ttu-id="24961-141">Sessie fouten worden gewoonlijk gebruikte tooreport Hallo fouten die een invloed op Hallo gebruiker tijdens Hallo gebruikerssessie hebben.</span><span class="sxs-lookup"><span data-stu-id="24961-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="24961-142">**Voorbeeld zonder extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="24961-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="24961-143">**Voorbeeld met extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="24961-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="24961-144">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="24961-144">Standalone errors</span></span>
<span data-ttu-id="24961-145">In tegenstelling tot sessie fouten, kunnen zelfstandige fouten optreden buiten Hallo context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="24961-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="24961-146">Gebruik voor die `engagement.agent.sendError` in plaats van `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="24961-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="24961-147">Rapportage van taken</span><span class="sxs-lookup"><span data-stu-id="24961-147">Reporting jobs</span></span>
<span data-ttu-id="24961-148">Rapportage van taken dekt rapportage van fouten en gebeurtenissen die zich tijdens een taak voordoen en de rapportage van crashes.</span><span class="sxs-lookup"><span data-stu-id="24961-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="24961-149">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="24961-149">**Example:**</span></span>

<span data-ttu-id="24961-150">Als u toomonitor een AJAX-aanvraag wilt, gebruikt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="24961-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

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

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="24961-151">Rapportage van fouten tijdens een taak</span><span class="sxs-lookup"><span data-stu-id="24961-151">Reporting errors during a job</span></span>
<span data-ttu-id="24961-152">Fouten kunnen gerelateerde tooa taak in plaats van de huidige gebruikerssessie toohello uitgevoerd worden.</span><span class="sxs-lookup"><span data-stu-id="24961-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="24961-153">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="24961-153">**Example:**</span></span>

<span data-ttu-id="24961-154">Als u wilt dat tooreport een fout als een AJAX-aanvraag is mislukt:</span><span class="sxs-lookup"><span data-stu-id="24961-154">If you want tooreport an error if an AJAX request fails:</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="24961-155">Melden van gebeurtenissen gedurende een project</span><span class="sxs-lookup"><span data-stu-id="24961-155">Reporting events during a job</span></span>
<span data-ttu-id="24961-156">Gebeurtenissen kunnen worden gerelateerde tooa die u uitvoert in plaats van de huidige gebruikerssessie toohello, dankzij toohello `engagement.agent.sendJobEvent` functie.</span><span class="sxs-lookup"><span data-stu-id="24961-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="24961-157">Deze functie werkt precies hetzelfde als `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="24961-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="24961-158">Reporting crashes</span><span class="sxs-lookup"><span data-stu-id="24961-158">Reporting crashes</span></span>
<span data-ttu-id="24961-159">Gebruik Hallo `sendCrash` functie tooreport handmatig is vastgelopen.</span><span class="sxs-lookup"><span data-stu-id="24961-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="24961-160">Hallo `crashid` een tekenreeks waarmee Hallo type crash is.</span><span class="sxs-lookup"><span data-stu-id="24961-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="24961-161">Hallo `crash` argument is meestal de stacktracering Hallo Hallo crash als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="24961-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="24961-162">Extra parameters</span><span class="sxs-lookup"><span data-stu-id="24961-162">Extra parameters</span></span>
<span data-ttu-id="24961-163">U kunt willekeurige gegevens tooan gebeurtenis, fout, activiteit of taak koppelen.</span><span class="sxs-lookup"><span data-stu-id="24961-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="24961-164">Hallo-gegevens kunnen worden een JSON-object (maar niet een matrix of primitief type).</span><span class="sxs-lookup"><span data-stu-id="24961-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="24961-165">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="24961-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="24961-166">Limieten</span><span class="sxs-lookup"><span data-stu-id="24961-166">Limits</span></span>
<span data-ttu-id="24961-167">Limieten die tooextra parameters van toepassing zijn op Hallo gebieden van reguliere expressies voor sleutels, waardetypen en grootte.</span><span class="sxs-lookup"><span data-stu-id="24961-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="24961-168">Sleutels</span><span class="sxs-lookup"><span data-stu-id="24961-168">Keys</span></span>
<span data-ttu-id="24961-169">Elke sleutel in het Hallo-object moet overeenkomen met de volgende reguliere expressie Hallo:</span><span class="sxs-lookup"><span data-stu-id="24961-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="24961-170">Dit betekent dat sleutels moeten beginnen met ten minste één letter gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="24961-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="24961-171">Waarden</span><span class="sxs-lookup"><span data-stu-id="24961-171">Values</span></span>
<span data-ttu-id="24961-172">Waarden zijn beperkt toostring, het aantal en Booleaanse typen.</span><span class="sxs-lookup"><span data-stu-id="24961-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="24961-173">Grootte</span><span class="sxs-lookup"><span data-stu-id="24961-173">Size</span></span>
<span data-ttu-id="24961-174">Extra's zijn beperkt too1, 024 tekens per aanroep (nadat Hallo Mobile Engagement Web SDK coderen van deze in JSON).</span><span class="sxs-lookup"><span data-stu-id="24961-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="24961-175">Rapportage-toepassingsinformatie</span><span class="sxs-lookup"><span data-stu-id="24961-175">Reporting application information</span></span>
<span data-ttu-id="24961-176">U kunt handmatig rapporteren voor het bijhouden van gegevens (of andere toepassingsspecifieke gegevens) met behulp van Hallo `sendAppInfo()` functie.</span><span class="sxs-lookup"><span data-stu-id="24961-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="24961-177">Houd er rekening mee dat deze gegevens stapsgewijs kunnen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="24961-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="24961-178">Laatste waarde alleen Hallo voor een specifieke sleutel wordt bewaard voor een specifiek apparaat.</span><span class="sxs-lookup"><span data-stu-id="24961-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="24961-179">Als gebeurtenis extra's, kunt u een JSON-object tooabstract toepassingsinformatie.</span><span class="sxs-lookup"><span data-stu-id="24961-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="24961-180">Houd er rekening mee dat matrices of onderliggende objecten worden behandeld als platte tekenreeksen (met behulp van de JSON-serialisatie).</span><span class="sxs-lookup"><span data-stu-id="24961-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="24961-181">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="24961-181">**Example:**</span></span>

<span data-ttu-id="24961-182">Hier volgt een voorbeeld van code voor de verzendende Hallo-gebruiker geslacht en Geboortedatum:</span><span class="sxs-lookup"><span data-stu-id="24961-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="24961-183">Limieten</span><span class="sxs-lookup"><span data-stu-id="24961-183">Limits</span></span>
<span data-ttu-id="24961-184">Limieten die van toepassing zijn tooapplication informatie hebben Hallo gebieden van reguliere expressies voor sleutels en grootte.</span><span class="sxs-lookup"><span data-stu-id="24961-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="24961-185">Sleutels</span><span class="sxs-lookup"><span data-stu-id="24961-185">Keys</span></span>
<span data-ttu-id="24961-186">Elke sleutel in het Hallo-object moet overeenkomen met de volgende reguliere expressie Hallo:</span><span class="sxs-lookup"><span data-stu-id="24961-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="24961-187">Dit betekent dat sleutels moeten beginnen met ten minste één letter gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="24961-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="24961-188">Grootte</span><span class="sxs-lookup"><span data-stu-id="24961-188">Size</span></span>
<span data-ttu-id="24961-189">Toepassingsinformatie is beperkt too1, 024 tekens per aanroep (nadat Hallo Mobile Engagement Web SDK coderen van deze in JSON).</span><span class="sxs-lookup"><span data-stu-id="24961-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="24961-190">In de Hallo voorgaande voorbeeld, verzonden hello JSON toohello server 44 tekens lang is:</span><span class="sxs-lookup"><span data-stu-id="24961-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
