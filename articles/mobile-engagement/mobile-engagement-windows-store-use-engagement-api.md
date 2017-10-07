---
title: aaaHow tooUse Hallo Engagement API op universele Windows-
description: Hoe tooUse Engagement API op Universal Windows hello
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a><span data-ttu-id="c5254-103">Hoe tooUse Engagement API op Universal Windows hello</span><span class="sxs-lookup"><span data-stu-id="c5254-103">How tooUse hello Engagement API on Windows Universal</span></span>
<span data-ttu-id="c5254-104">Dit document is een invoegtoepassing toohello document [hoe tooIntegrate Engagement voor universele Windows-](mobile-engagement-windows-store-integrate-engagement.md): biedt diepte meer informatie over hoe toouse Hallo Engagement API tooreport de toepassingsstatistieken van uw.</span><span class="sxs-lookup"><span data-stu-id="c5254-104">This document is an add-on toohello document [How tooIntegrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="c5254-105">Houd er rekening mee dat als u Engagement tooreport van uw toepassing sessies, activiteiten, crashes en technische informatie wilt, hello eenvoudigste manier toomake alle is uw `Page` onderliggende klassen overnemen van Hallo `EngagementPage` klasse.</span><span class="sxs-lookup"><span data-stu-id="c5254-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Page` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="c5254-106">Als u wilt meer, bijvoorbeeld als u tooreport toepassing specifieke gebeurtenissen, fouten en taken moet toodo, of als er tooreport activiteiten van uw toepassing in een andere manier dan een geïmplementeerd in Hallo Hallo `EngagementPage` klassen, moet u toouse Hallo Engagement API.</span><span class="sxs-lookup"><span data-stu-id="c5254-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="c5254-107">Hallo Engagement API geleverd door Hallo `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="c5254-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="c5254-108">U hebt toegang tot methoden toothose via `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="c5254-108">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="c5254-109">Zelfs als Hallo agent-module is niet geïnitialiseerd, elke aanroep toohello API wordt uitgesteld en opnieuw worden uitgevoerd wanneer de Hallo agent beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="c5254-109">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="c5254-110">Engagement-concepten</span><span class="sxs-lookup"><span data-stu-id="c5254-110">Engagement concepts</span></span>
<span data-ttu-id="c5254-111">Hallo volgende delen verfijnen Hallo algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md) voor Hallo Universal Windows platform.</span><span class="sxs-lookup"><span data-stu-id="c5254-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="c5254-112">`Session` en `Activity`</span><span class="sxs-lookup"><span data-stu-id="c5254-112">`Session` and `Activity`</span></span>
<span data-ttu-id="c5254-113">Een *activiteit* wordt meestal veroorzaakt door één pagina van de toepassing hello, die toosay hello *activiteit* wordt gestart wanneer het Hallo-pagina wordt weergegeven en stopt wanneer Hallo pagina is gesloten: dit is Hallo geval wanneer hello Engagement SDK is geïntegreerd met behulp van Hallo `EngagementPage` klasse.</span><span class="sxs-lookup"><span data-stu-id="c5254-113">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="c5254-114">Maar *activiteiten* kunnen ook handmatig met behulp van Hallo Engagement API worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="c5254-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="c5254-115">Hiermee kunt u een bepaalde pagina in verschillende onderdelen tooget sub meer informatie over het gebruik van deze pagina (bijvoorbeeld hoe vaak tooknow en hoe lang dialoogvensters worden gebruikt binnen deze pagina) Hallo toosplit.</span><span class="sxs-lookup"><span data-stu-id="c5254-115">This allows you toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknow how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="c5254-116">Rapportage</span><span class="sxs-lookup"><span data-stu-id="c5254-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="c5254-117">Gebruiker start een nieuwe activiteit</span><span class="sxs-lookup"><span data-stu-id="c5254-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-118">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="c5254-119">U moet toocall `StartActivity()` elke activiteit tijd Hallo gebruiker wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c5254-119">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="c5254-120">Hallo eerste aanroep toothis functie wordt een nieuwe gebruikerssessie gestart.</span><span class="sxs-lookup"><span data-stu-id="c5254-120">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5254-121">Hallo EndActivity methode Hallo SDK automatisch aangeroepen wanneer de toepassing hello wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="c5254-121">hello SDK automatically calls hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="c5254-122">Dus is het raadzaam toocall hello StartActivity methode wanneer Hallo activiteit van de gebruiker hello wordt gewijzigd en tooNEVER oproep Hallo EndActivity-methode sinds het aanroepen van deze methode forceert toobe van Hallo huidige sessie is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="c5254-122">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user changes, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="c5254-123">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="c5254-124">Gebruiker eindigt zijn huidige activiteit</span><span class="sxs-lookup"><span data-stu-id="c5254-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-125">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="c5254-126">Dit Hallo-activiteit en Hallo-sessie wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="c5254-126">This ends hello activity and hello session.</span></span> <span data-ttu-id="c5254-127">U moet deze methode niet aanroepen, tenzij u zeker weet wat u doet.</span><span class="sxs-lookup"><span data-stu-id="c5254-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="c5254-128">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="c5254-129">Rapportage van taken</span><span class="sxs-lookup"><span data-stu-id="c5254-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="c5254-130">Een taak starten</span><span class="sxs-lookup"><span data-stu-id="c5254-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-131">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="c5254-132">U kunt Hallo tootrack sommige taken gebruiken gedurende een periode.</span><span class="sxs-lookup"><span data-stu-id="c5254-132">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="c5254-133">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-133">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="c5254-134">Een taak beëindigen</span><span class="sxs-lookup"><span data-stu-id="c5254-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-135">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="c5254-136">Zodra een taak die wordt gevolgd door een taak is beëindigd, moet u Hallo EndJob methode aanroepen voor deze taak door het Hallo-taaknaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="c5254-136">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="c5254-137">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-137">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="c5254-138">Melden van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c5254-138">Reporting Events</span></span>
<span data-ttu-id="c5254-139">Er is drie soorten gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="c5254-139">There is three types of events :</span></span>

* <span data-ttu-id="c5254-140">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c5254-140">Standalone events</span></span>
* <span data-ttu-id="c5254-141">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c5254-141">Session events</span></span>
* <span data-ttu-id="c5254-142">Gebeurtenissen van de taak</span><span class="sxs-lookup"><span data-stu-id="c5254-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="c5254-143">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c5254-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-144">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="c5254-145">Er kunnen zelfstandige gebeurtenissen plaatsvinden buiten de context van een sessie Hallo.</span><span class="sxs-lookup"><span data-stu-id="c5254-145">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="c5254-146">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="c5254-147">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c5254-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-148">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="c5254-149">Sessiegebeurtenissen zijn meestal gebruikte tooreport Hallo bewerkingen worden uitgevoerd door een gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="c5254-149">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="c5254-150">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-150">Example</span></span>
<span data-ttu-id="c5254-151">**Zonder gegevens:**</span><span class="sxs-lookup"><span data-stu-id="c5254-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="c5254-152">**Met gegevens:**</span><span class="sxs-lookup"><span data-stu-id="c5254-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="c5254-153">Taakgebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c5254-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-154">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="c5254-155">Gebeurtenissen van de taak zijn meestal gebruikte tooreport Hallo acties die door een gebruiker wordt uitgevoerd tijdens een taak.</span><span class="sxs-lookup"><span data-stu-id="c5254-155">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="c5254-156">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="c5254-157">Rapportage van fouten</span><span class="sxs-lookup"><span data-stu-id="c5254-157">Reporting Errors</span></span>
<span data-ttu-id="c5254-158">Er zijn drie soorten fouten:</span><span class="sxs-lookup"><span data-stu-id="c5254-158">There are three types of errors :</span></span>

* <span data-ttu-id="c5254-159">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="c5254-159">Standalone errors</span></span>
* <span data-ttu-id="c5254-160">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="c5254-160">Session errors</span></span>
* <span data-ttu-id="c5254-161">Taakfouten</span><span class="sxs-lookup"><span data-stu-id="c5254-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="c5254-162">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="c5254-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-163">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="c5254-164">Strijdig toosession fouten, zelfstandige fouten kunnen optreden buiten Hallo context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="c5254-164">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="c5254-165">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="c5254-166">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="c5254-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-167">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="c5254-168">Sessie-fouten worden gewoonlijk gebruikte tooreport Hallo fouten die invloed hebben op Hallo gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="c5254-168">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="c5254-169">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="c5254-170">Taakfouten</span><span class="sxs-lookup"><span data-stu-id="c5254-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-171">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="c5254-172">Fouten kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="c5254-172">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="c5254-173">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="c5254-174">Reporting Crashes</span><span class="sxs-lookup"><span data-stu-id="c5254-174">Reporting Crashes</span></span>
<span data-ttu-id="c5254-175">Hallo agent biedt twee methoden toodeal crashes.</span><span class="sxs-lookup"><span data-stu-id="c5254-175">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="c5254-176">Een uitzondering verzenden</span><span class="sxs-lookup"><span data-stu-id="c5254-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-177">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="c5254-178">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-178">Example</span></span>
<span data-ttu-id="c5254-179">U kunt een uitzondering op elk gewenst moment kunt verzenden door aan te roepen:</span><span class="sxs-lookup"><span data-stu-id="c5254-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="c5254-180">U kunt ook een optionele parameter tooterminate Hallo engagement sessie op Hallo hetzelfde moment dan het Hallo-crash verzenden.</span><span class="sxs-lookup"><span data-stu-id="c5254-180">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="c5254-181">toodo dus aanroepen:</span><span class="sxs-lookup"><span data-stu-id="c5254-181">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="c5254-182">Als u dat doet, worden Hallo-sessie en taken gesloten na de Hallo crash verzenden.</span><span class="sxs-lookup"><span data-stu-id="c5254-182">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="c5254-183">Verzenden van een onverwerkte uitzondering</span><span class="sxs-lookup"><span data-stu-id="c5254-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="c5254-184">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="c5254-185">Engagement biedt ook een methode toosend niet-verwerkte uitzonderingen hebt u **UITGESCHAKELDE** Engagement automatisch **crash** reporting.</span><span class="sxs-lookup"><span data-stu-id="c5254-185">Engagement also provides a method toosend unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="c5254-186">Dit is vooral nuttig wanneer gebruikt in Hallo toepassing UnhandledException gebeurtenis-handler.</span><span class="sxs-lookup"><span data-stu-id="c5254-186">This is especially useful when used inside hello application UnhandledException event handler.</span></span>

<span data-ttu-id="c5254-187">Deze methode wordt **altijd** Hallo engagement sessie en taken te beëindigen nadat deze is aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c5254-187">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="c5254-188">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-188">Example</span></span>
<span data-ttu-id="c5254-189">U kunt deze tooimplement uw eigen UnhandledExceptionEventArgs-handler.</span><span class="sxs-lookup"><span data-stu-id="c5254-189">You can use it tooimplement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="c5254-190">Bijvoorbeeld, voeg Hallo `Current_UnhandledException` methode Hallo `App.xaml.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="c5254-190">For example, add hello `Current_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="c5254-191">Voeg in App.xaml.cs in "Openbare App() {}" toe:</span><span class="sxs-lookup"><span data-stu-id="c5254-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="c5254-192">Apparaat-Id</span><span class="sxs-lookup"><span data-stu-id="c5254-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="c5254-193">U kunt Hallo engagement apparaat-id ophalen door deze methode aanroept.</span><span class="sxs-lookup"><span data-stu-id="c5254-193">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="c5254-194">Parameters voor extra 's</span><span class="sxs-lookup"><span data-stu-id="c5254-194">Extras parameters</span></span>
<span data-ttu-id="c5254-195">Willekeurige gegevens kunnen worden aangesloten tooan gebeurtenis, een fout, een activiteit of een taak.</span><span class="sxs-lookup"><span data-stu-id="c5254-195">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="c5254-196">Deze gegevens kunnen worden onderverdeeld met behulp van een woordenboek.</span><span class="sxs-lookup"><span data-stu-id="c5254-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="c5254-197">Sleutels en waarden kunnen van elk type zijn.</span><span class="sxs-lookup"><span data-stu-id="c5254-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="c5254-198">Extra gegevens worden geserialiseerd als u uw eigen type in extra's tooinsert wilt u moet daarom tooadd een gegevenscontract voor dit type.</span><span class="sxs-lookup"><span data-stu-id="c5254-198">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="c5254-199">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-199">Example</span></span>
<span data-ttu-id="c5254-200">We maken een nieuwe klasse 'Persoon'.</span><span class="sxs-lookup"><span data-stu-id="c5254-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="c5254-201">Vervolgens voegen we toe een `Person` exemplaar tooan extra.</span><span class="sxs-lookup"><span data-stu-id="c5254-201">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="c5254-202">Als u andere typen objecten plaatst, zorg ervoor dat de methode ToString() geïmplementeerde tooreturn menselijke leesbare string.</span><span class="sxs-lookup"><span data-stu-id="c5254-202">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="c5254-203">Limieten</span><span class="sxs-lookup"><span data-stu-id="c5254-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="c5254-204">Sleutels</span><span class="sxs-lookup"><span data-stu-id="c5254-204">Keys</span></span>
<span data-ttu-id="c5254-205">Elke sleutel in het Hallo-object moet overeenkomen met de volgende reguliere expressie Hallo:</span><span class="sxs-lookup"><span data-stu-id="c5254-205">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="c5254-206">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="c5254-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="c5254-207">Grootte</span><span class="sxs-lookup"><span data-stu-id="c5254-207">Size</span></span>
<span data-ttu-id="c5254-208">Extra's zijn beperkt te**1024** tekens per aanroep.</span><span class="sxs-lookup"><span data-stu-id="c5254-208">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="c5254-209">Rapportage-toepassingsinformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="c5254-210">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c5254-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="c5254-211">U kunt handmatig rapporteert informatie (of andere toepassing specifieke gegevens) met de functie SendAppInfo() Hallo bijhouden.</span><span class="sxs-lookup"><span data-stu-id="c5254-211">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="c5254-212">Merk op dat deze gegevens stapsgewijs kunnen worden verzonden: alleen Hallo meest recente waarde voor een bepaalde sleutel worden behouden voor een bepaald apparaat.</span><span class="sxs-lookup"><span data-stu-id="c5254-212">Note that this data can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="c5254-213">Als gebeurtenis extra's, een woordenlijst gebruiken\<-object, object\> tooattach gegevens.</span><span class="sxs-lookup"><span data-stu-id="c5254-213">Like event extras, use a Dictionary\<object, object\> tooattach data.</span></span>

### <a name="example"></a><span data-ttu-id="c5254-214">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c5254-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="c5254-215">Limieten</span><span class="sxs-lookup"><span data-stu-id="c5254-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="c5254-216">Sleutels</span><span class="sxs-lookup"><span data-stu-id="c5254-216">Keys</span></span>
<span data-ttu-id="c5254-217">Elke sleutel in het Hallo-object moet overeenkomen met de volgende reguliere expressie Hallo:</span><span class="sxs-lookup"><span data-stu-id="c5254-217">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="c5254-218">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="c5254-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="c5254-219">Grootte</span><span class="sxs-lookup"><span data-stu-id="c5254-219">Size</span></span>
<span data-ttu-id="c5254-220">Toepassingsinformatie is beperkt te**1024** tekens per aanroep.</span><span class="sxs-lookup"><span data-stu-id="c5254-220">Application information is limited too**1024** characters per call.</span></span>

<span data-ttu-id="c5254-221">In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 44 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="c5254-221">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="c5254-222">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="c5254-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="c5254-223">Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="c5254-223">Enable Logging</span></span>
<span data-ttu-id="c5254-224">Hallo SDK kan worden geconfigureerd tooproduce test Logboeken in Hallo IDE-console.</span><span class="sxs-lookup"><span data-stu-id="c5254-224">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="c5254-225">Deze logboeken worden niet standaard geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="c5254-225">These logs are not activated by default.</span></span> <span data-ttu-id="c5254-226">toocustomize deze, update Hallo eigenschap `EngagementAgent.Instance.TestLogEnabled` tooone van Hallo waarde in Hallo `EngagementTestLogLevel` opsomming, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c5254-226">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

