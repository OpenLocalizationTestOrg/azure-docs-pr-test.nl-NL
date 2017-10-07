---
title: aaaHow tooUse Hallo Engagement API op Windows Phone Silverlight
description: Hoe tooUse Hallo Engagement API op Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="2ea32-103">Hoe tooUse Hallo Engagement API op Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="2ea32-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="2ea32-104">Dit document is een invoegtoepassing toohello document [hoe toointegrate Mobile Engagement in uw Windows Phone Silverlight-app](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="2ea32-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="2ea32-105">Het biedt diepte meer informatie over hoe toouse Hallo Engagement API tooreport de toepassingsstatistieken van uw.</span><span class="sxs-lookup"><span data-stu-id="2ea32-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="2ea32-106">Als u wilt dat alleen Engagement tooreport van uw toepassing sessies, activiteiten, crashes en technische informatie, is Hallo eenvoudigste manier toomake alle uw `PhoneApplicationPage` onderliggende klassen overnemen van Hallo `EngagementPage` klasse.</span><span class="sxs-lookup"><span data-stu-id="2ea32-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="2ea32-107">Als u wilt meer, bijvoorbeeld als u tooreport toepassing specifieke gebeurtenissen, fouten en taken moet toodo, of als er tooreport activiteiten van uw toepassing in een andere manier dan een geïmplementeerd in Hallo Hallo `EngagementPage` klassen, moet u toouse Hallo Engagement API.</span><span class="sxs-lookup"><span data-stu-id="2ea32-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="2ea32-108">Hallo Engagement API geleverd door Hallo `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="2ea32-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="2ea32-109">U hebt toegang tot methoden toothose via `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="2ea32-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="2ea32-110">Zelfs als Hallo agent-module is niet geïnitialiseerd, elke aanroep toohello API wordt uitgesteld en opnieuw worden uitgevoerd wanneer de Hallo agent beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2ea32-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="2ea32-111">Engagement-concepten</span><span class="sxs-lookup"><span data-stu-id="2ea32-111">Engagement concepts</span></span>
<span data-ttu-id="2ea32-112">Hallo volgende onderdelen verfijnen Hallo Mobile Engagement-concepten voor Hallo Windows Phone-platform.</span><span class="sxs-lookup"><span data-stu-id="2ea32-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="2ea32-113">`Session` en `Activity`</span><span class="sxs-lookup"><span data-stu-id="2ea32-113">`Session` and `Activity`</span></span>
<span data-ttu-id="2ea32-114">Een *activiteit* wordt meestal veroorzaakt door één pagina van de toepassing hello, die toosay hello *activiteit* wordt gestart wanneer het Hallo-pagina wordt weergegeven en stopt wanneer Hallo pagina is gesloten: dit is Hallo geval wanneer hello Engagement SDK is geïntegreerd met behulp van Hallo `EngagementPage` klasse.</span><span class="sxs-lookup"><span data-stu-id="2ea32-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="2ea32-115">Maar *activiteiten* kunnen ook handmatig met behulp van Hallo Engagement API worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="2ea32-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="2ea32-116">Hierdoor kunnen een bepaalde pagina toosplit in verschillende sub delen tooget meer informatie over Hallo gebruik van deze pagina (bijvoorbeeld hoe vaak tooknown en hoe lang dialoogvensters worden gebruikt binnen deze pagina).</span><span class="sxs-lookup"><span data-stu-id="2ea32-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="2ea32-117">Rapportage</span><span class="sxs-lookup"><span data-stu-id="2ea32-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="2ea32-118">Gebruiker start een nieuwe activiteit</span><span class="sxs-lookup"><span data-stu-id="2ea32-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-119">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="2ea32-120">U moet toocall `StartActivity()` elke activiteit tijd Hallo gebruiker wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="2ea32-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="2ea32-121">Hallo eerste aanroep toothis functie wordt een nieuwe gebruikerssessie gestart.</span><span class="sxs-lookup"><span data-stu-id="2ea32-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ea32-122">Hallo SDK automatisch Hallo EndActivity methode aanroepen wanneer de toepassing hello wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="2ea32-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="2ea32-123">Dus is het raadzaam toocall hello StartActivity methode wanneer het Hallo-activiteit van Hallo gebruiker wijzigings- en tooNEVER aanroep Hallo EndActivity-methode sinds het aanroepen van deze methode forceert Hallo huidige sessie toobe beëindigd.</span><span class="sxs-lookup"><span data-stu-id="2ea32-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="2ea32-124">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="2ea32-125">Gebruiker eindigt zijn huidige activiteit</span><span class="sxs-lookup"><span data-stu-id="2ea32-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-126">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="2ea32-127">U moet toocall `EndActivity()` ten minste eenmaal wanneer de gebruiker Hallo is voltooid, de laatste activiteit.</span><span class="sxs-lookup"><span data-stu-id="2ea32-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="2ea32-128">Dit Hallo Engagement SDK dat Hallo gebruiker momenteel niet actief is en dat de gebruikerssessie Hallo toobe moeten eenmaal Hallo sessietime-out gesloten verloopt informeert (als u aanroept `StartActivity()` voordat Hallo sessietime-out is verlopen, Hallo sessie gewoon wordt voortgezet).</span><span class="sxs-lookup"><span data-stu-id="2ea32-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="2ea32-129">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="2ea32-130">Rapportage van taken</span><span class="sxs-lookup"><span data-stu-id="2ea32-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="2ea32-131">Een taak starten</span><span class="sxs-lookup"><span data-stu-id="2ea32-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-132">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="2ea32-133">U kunt Hallo tootrack sommige taken gebruiken gedurende een periode.</span><span class="sxs-lookup"><span data-stu-id="2ea32-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="2ea32-134">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="2ea32-135">Een taak beëindigen</span><span class="sxs-lookup"><span data-stu-id="2ea32-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-136">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="2ea32-137">Zodra een taak die wordt gevolgd door een taak is beëindigd, moet u Hallo EndJob methode aanroepen voor deze taak door het Hallo-taaknaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="2ea32-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="2ea32-138">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="2ea32-139">Melden van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="2ea32-139">Reporting Events</span></span>
<span data-ttu-id="2ea32-140">Er is drie soorten gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="2ea32-140">There is three types of events :</span></span>

* <span data-ttu-id="2ea32-141">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="2ea32-141">Standalone events</span></span>
* <span data-ttu-id="2ea32-142">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="2ea32-142">Session events</span></span>
* <span data-ttu-id="2ea32-143">Gebeurtenissen van de taak</span><span class="sxs-lookup"><span data-stu-id="2ea32-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="2ea32-144">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="2ea32-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-145">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="2ea32-146">Er kunnen zelfstandige gebeurtenissen plaatsvinden buiten de context van een sessie Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ea32-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="2ea32-147">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="2ea32-148">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="2ea32-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-149">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="2ea32-150">Sessiegebeurtenissen zijn meestal gebruikte tooreport Hallo bewerkingen worden uitgevoerd door een gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="2ea32-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="2ea32-151">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-151">Example</span></span>
<span data-ttu-id="2ea32-152">**Zonder gegevens:**</span><span class="sxs-lookup"><span data-stu-id="2ea32-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="2ea32-153">**Met gegevens:**</span><span class="sxs-lookup"><span data-stu-id="2ea32-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="2ea32-154">Taakgebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="2ea32-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-155">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="2ea32-156">Gebeurtenissen van de taak zijn meestal gebruikte tooreport Hallo acties die door een gebruiker wordt uitgevoerd tijdens een taak.</span><span class="sxs-lookup"><span data-stu-id="2ea32-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="2ea32-157">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="2ea32-158">Rapportage van fouten</span><span class="sxs-lookup"><span data-stu-id="2ea32-158">Reporting Errors</span></span>
<span data-ttu-id="2ea32-159">Er is drie soorten fouten:</span><span class="sxs-lookup"><span data-stu-id="2ea32-159">There is three types of errors :</span></span>

* <span data-ttu-id="2ea32-160">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="2ea32-160">Standalone errors</span></span>
* <span data-ttu-id="2ea32-161">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="2ea32-161">Session errors</span></span>
* <span data-ttu-id="2ea32-162">Taakfouten</span><span class="sxs-lookup"><span data-stu-id="2ea32-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="2ea32-163">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="2ea32-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-164">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="2ea32-165">Strijdig toosession fouten, zelfstandige fouten kunnen optreden buiten Hallo context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="2ea32-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="2ea32-166">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="2ea32-167">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="2ea32-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-168">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="2ea32-169">Sessie-fouten worden gewoonlijk gebruikte tooreport Hallo fouten die invloed hebben op Hallo gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="2ea32-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="2ea32-170">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="2ea32-171">Taakfouten</span><span class="sxs-lookup"><span data-stu-id="2ea32-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-172">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="2ea32-173">Fouten kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="2ea32-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="2ea32-174">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="2ea32-175">Reporting Crashes</span><span class="sxs-lookup"><span data-stu-id="2ea32-175">Reporting Crashes</span></span>
<span data-ttu-id="2ea32-176">Hallo agent biedt twee methoden toodeal crashes.</span><span class="sxs-lookup"><span data-stu-id="2ea32-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="2ea32-177">Een uitzondering verzenden</span><span class="sxs-lookup"><span data-stu-id="2ea32-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-178">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="2ea32-179">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-179">Example</span></span>
<span data-ttu-id="2ea32-180">U kunt een uitzondering op elk gewenst moment kunt verzenden door aan te roepen:</span><span class="sxs-lookup"><span data-stu-id="2ea32-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="2ea32-181">U kunt ook een optionele parameter tooterminate Hallo engagement sessie op Hallo hetzelfde moment dan het Hallo-crash verzenden.</span><span class="sxs-lookup"><span data-stu-id="2ea32-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="2ea32-182">toodo dus aanroepen:</span><span class="sxs-lookup"><span data-stu-id="2ea32-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="2ea32-183">Als u dat doet, worden Hallo-sessie en taken gesloten na de Hallo crash verzenden.</span><span class="sxs-lookup"><span data-stu-id="2ea32-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="2ea32-184">Verzenden van een onverwerkte uitzondering</span><span class="sxs-lookup"><span data-stu-id="2ea32-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="2ea32-185">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="2ea32-186">Engagement biedt ook een methode toosend onverwerkte uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="2ea32-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="2ea32-187">Dit is vooral nuttig wanneer gebruikt in Hallo silverlight UnhandledException gebeurtenis-handler.</span><span class="sxs-lookup"><span data-stu-id="2ea32-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="2ea32-188">Deze methode wordt **altijd** Hallo engagement sessie en taken te beëindigen nadat deze is aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2ea32-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="2ea32-189">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-189">Example</span></span>
<span data-ttu-id="2ea32-190">U kunt deze tooimplement uw eigen handler UnhandledException (met name als u de automatische crash Hallo rapportagefunctie van Engagement hebt uitgeschakeld).</span><span class="sxs-lookup"><span data-stu-id="2ea32-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="2ea32-191">Bijvoorbeeld in Hallo `Application_UnhandledException` methode Hallo `App.xaml.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="2ea32-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="2ea32-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="2ea32-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="2ea32-193">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="2ea32-194">Als u Hallo gebruiker navigeert doorsturen, weg van een toepassing nadat Hallo gedeactiveerd gebeurtenis wordt gegenereerd, probeert Hallo besturingssysteem tooput Hallo toepassing in een niet-actieve status.</span><span class="sxs-lookup"><span data-stu-id="2ea32-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="2ea32-195">Hallo-toepassing is tombstones.</span><span class="sxs-lookup"><span data-stu-id="2ea32-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="2ea32-196">In dit proces een aanvraag wordt beëindigd, maar sommige gegevens over Hallo status van de toepassing hello en Hallo afzonderlijke pagina's in de toepassing hello behouden blijven.</span><span class="sxs-lookup"><span data-stu-id="2ea32-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="2ea32-197">U hebt tooinsert `EngagementAgent.Instance.OnActivated(e)` in Hallo `Application_Activated` methode van Hallo App.xaml.cs bestand tooreset Hallo Engagement Agent wanneer de toepassing hello Tombstoned is geweest.</span><span class="sxs-lookup"><span data-stu-id="2ea32-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="2ea32-198">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="2ea32-199">Apparaat-Id</span><span class="sxs-lookup"><span data-stu-id="2ea32-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="2ea32-200">U kunt Hallo engagement apparaat-id ophalen door deze methode aanroept.</span><span class="sxs-lookup"><span data-stu-id="2ea32-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="2ea32-201">Parameters voor extra 's</span><span class="sxs-lookup"><span data-stu-id="2ea32-201">Extras parameters</span></span>
<span data-ttu-id="2ea32-202">Willekeurige gegevens kunnen worden aangesloten tooan gebeurtenis, een fout, een activiteit of een taak.</span><span class="sxs-lookup"><span data-stu-id="2ea32-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="2ea32-203">Deze gegevens kunnen worden onderverdeeld met behulp van een woordenboek.</span><span class="sxs-lookup"><span data-stu-id="2ea32-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="2ea32-204">Sleutels en waarden kunnen van elk type zijn.</span><span class="sxs-lookup"><span data-stu-id="2ea32-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="2ea32-205">Extra gegevens worden geserialiseerd als u uw eigen type in extra's tooinsert wilt u moet daarom tooadd een gegevenscontract voor dit type.</span><span class="sxs-lookup"><span data-stu-id="2ea32-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="2ea32-206">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-206">Example</span></span>
<span data-ttu-id="2ea32-207">We maken een nieuwe klasse 'Persoon'.</span><span class="sxs-lookup"><span data-stu-id="2ea32-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="2ea32-208">Vervolgens voegen we toe een `Person` exemplaar tooan extra.</span><span class="sxs-lookup"><span data-stu-id="2ea32-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="2ea32-209">Als u andere typen objecten plaatst, zorg ervoor dat de methode ToString() geïmplementeerde tooreturn menselijke leesbare string.</span><span class="sxs-lookup"><span data-stu-id="2ea32-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="2ea32-210">Limieten</span><span class="sxs-lookup"><span data-stu-id="2ea32-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="2ea32-211">Sleutels</span><span class="sxs-lookup"><span data-stu-id="2ea32-211">Keys</span></span>
<span data-ttu-id="2ea32-212">Elke sleutel in het Hallo-object moet overeenkomen met de volgende reguliere expressie Hallo:</span><span class="sxs-lookup"><span data-stu-id="2ea32-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="2ea32-213">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="2ea32-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="2ea32-214">Grootte</span><span class="sxs-lookup"><span data-stu-id="2ea32-214">Size</span></span>
<span data-ttu-id="2ea32-215">Extra's zijn beperkt te**1024** tekens per aanroep.</span><span class="sxs-lookup"><span data-stu-id="2ea32-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="2ea32-216">Rapportage-toepassingsinformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="2ea32-217">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="2ea32-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="2ea32-218">U kunt handmatig rapporteert informatie (of andere toepassing specifieke gegevens) met de functie SendAppInfo() Hallo bijhouden.</span><span class="sxs-lookup"><span data-stu-id="2ea32-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="2ea32-219">Merk op dat deze gegevens stapsgewijs kunnen worden verzonden: alleen Hallo meest recente waarde voor een bepaalde sleutel worden behouden voor een bepaald apparaat.</span><span class="sxs-lookup"><span data-stu-id="2ea32-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="2ea32-220">Als gebeurtenis extra's, een woordenlijst gebruiken\<-object, object\> tooattach gegevens.</span><span class="sxs-lookup"><span data-stu-id="2ea32-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="2ea32-221">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2ea32-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="2ea32-222">Limieten</span><span class="sxs-lookup"><span data-stu-id="2ea32-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="2ea32-223">Sleutels</span><span class="sxs-lookup"><span data-stu-id="2ea32-223">Keys</span></span>
<span data-ttu-id="2ea32-224">Elke sleutel in het Hallo-object moet overeenkomen met de volgende reguliere expressie Hallo:</span><span class="sxs-lookup"><span data-stu-id="2ea32-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="2ea32-225">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="2ea32-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="2ea32-226">Grootte</span><span class="sxs-lookup"><span data-stu-id="2ea32-226">Size</span></span>
<span data-ttu-id="2ea32-227">Toepassingsgegevens zijn beperkt te**1024** tekens per aanroep.</span><span class="sxs-lookup"><span data-stu-id="2ea32-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="2ea32-228">In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 44 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="2ea32-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="2ea32-229">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="2ea32-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="2ea32-230">Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="2ea32-230">Enable Logging</span></span>
<span data-ttu-id="2ea32-231">Hallo SDK kan worden geconfigureerd tooproduce test Logboeken in Hallo IDE-console.</span><span class="sxs-lookup"><span data-stu-id="2ea32-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="2ea32-232">Deze logboeken worden niet standaard geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="2ea32-232">These logs are not activated by default.</span></span> <span data-ttu-id="2ea32-233">toocustomize deze, update Hallo eigenschap `EngagementAgent.Instance.TestLogEnabled` tooone van Hallo waarde in Hallo `EngagementTestLogLevel` opsomming, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2ea32-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
