---
title: Het gebruik van de Engagement API op Universal Windows
description: Het gebruik van de Engagement API op Universal Windows
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
ms.openlocfilehash: 75fc134a5535e6113331470cf61df9c06eb8e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-universal"></a><span data-ttu-id="be989-103">Het gebruik van de Engagement API op Universal Windows</span><span class="sxs-lookup"><span data-stu-id="be989-103">How to Use the Engagement API on Windows Universal</span></span>
<span data-ttu-id="be989-104">Dit document is een invoegtoepassing voor het document [hoe integreren Engagement voor universele Windows-](mobile-engagement-windows-store-integrate-engagement.md): biedt diepte meer informatie over het gebruik van de Engagement-API voor het rapporteren van de toepassingsstatistieken van uw.</span><span class="sxs-lookup"><span data-stu-id="be989-104">This document is an add-on to the document [How to Integrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="be989-105">Houd er rekening mee dat als u alleen Engagement voor het rapporteren van uw toepassing sessies, activiteiten, crashes en technische informatie wilt, klikt u vervolgens de eenvoudigste manier is om alle uw `Page` onderliggende klassen overnemen van de `EngagementPage` klasse.</span><span class="sxs-lookup"><span data-stu-id="be989-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Page` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="be989-106">Als u wilt meer doen, bijvoorbeeld als u wilt rapporteren toepassing specifieke gebeurtenissen, fouten en taken, of als u hebt voor het rapporteren van activiteiten van uw toepassing op een andere manier dan de geïmplementeerd in de `EngagementPage` klassen, moet u de Engagement-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="be989-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="be989-107">De Engagement-API wordt geleverd door de `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="be989-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="be989-108">U kunt toegang tot deze methoden via `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="be989-108">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="be989-109">Zelfs als de agent-module is niet geïnitialiseerd, wordt elke aanroep van de API wordt uitgesteld en weer worden uitgevoerd wanneer de agent beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="be989-109">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="be989-110">Engagement-concepten</span><span class="sxs-lookup"><span data-stu-id="be989-110">Engagement concepts</span></span>
<span data-ttu-id="be989-111">De volgende onderdelen verfijnen de algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md) voor het Universal Windows platform.</span><span class="sxs-lookup"><span data-stu-id="be989-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="be989-112">`Session` en `Activity`</span><span class="sxs-lookup"><span data-stu-id="be989-112">`Session` and `Activity`</span></span>
<span data-ttu-id="be989-113">Een *activiteit* wordt meestal gekoppeld aan één pagina van de toepassing, dat wil zeggen de *activiteit* wordt gestart wanneer de pagina wordt weergegeven en stopt wanneer de pagina is gesloten: dit is het geval wanneer de Engagement SDK is geïntegreerd met behulp van de `EngagementPage` klasse.</span><span class="sxs-lookup"><span data-stu-id="be989-113">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="be989-114">Maar *activiteiten* kunnen ook handmatig met behulp van de Engagement-API worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="be989-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="be989-115">Hiermee kunt u het scheiden van een bepaalde pagina in verschillende sub-onderdelen voor meer informatie over het gebruik van deze pagina (bijvoorbeeld weten hoe vaak en hoe lang dialoogvensters worden gebruikt binnen deze pagina).</span><span class="sxs-lookup"><span data-stu-id="be989-115">This allows you to split a given page in several sub parts to get more details about the usage of this page (for example to know how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="be989-116">Rapportage</span><span class="sxs-lookup"><span data-stu-id="be989-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="be989-117">Gebruiker start een nieuwe activiteit</span><span class="sxs-lookup"><span data-stu-id="be989-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-118">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="be989-119">U moet aan te roepen `StartActivity()` elke keer dat de wijzigingen van de gebruiker-activiteit.</span><span class="sxs-lookup"><span data-stu-id="be989-119">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="be989-120">De eerste aanroep van deze functie wordt een nieuwe gebruikerssessie gestart.</span><span class="sxs-lookup"><span data-stu-id="be989-120">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be989-121">De SDK worden automatisch de EndActivity-methode aangeroepen wanneer de toepassing wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="be989-121">The SDK automatically calls the EndActivity method when the application is closed.</span></span> <span data-ttu-id="be989-122">Dus is het raadzaam de StartActivity-methode niet aanroepen wanneer de activiteit van de wijzigingen van de gebruiker en op nooit de EndActivity-methode niet aanroepen omdat de huidige sessie moet worden beëindigd zorgt ervoor dat u deze methode aanroept.</span><span class="sxs-lookup"><span data-stu-id="be989-122">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user changes, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="be989-123">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="be989-124">Gebruiker eindigt zijn huidige activiteit</span><span class="sxs-lookup"><span data-stu-id="be989-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-125">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="be989-126">Hiermee wordt de activiteit en de sessie beëindigd.</span><span class="sxs-lookup"><span data-stu-id="be989-126">This ends the activity and the session.</span></span> <span data-ttu-id="be989-127">U moet deze methode niet aanroepen, tenzij u zeker weet wat u doet.</span><span class="sxs-lookup"><span data-stu-id="be989-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="be989-128">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="be989-129">Rapportage van taken</span><span class="sxs-lookup"><span data-stu-id="be989-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="be989-130">Een taak starten</span><span class="sxs-lookup"><span data-stu-id="be989-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-131">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="be989-132">De taak kunt u sommige taken gedurende een periode bijhouden.</span><span class="sxs-lookup"><span data-stu-id="be989-132">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="be989-133">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-133">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="be989-134">Een taak beëindigen</span><span class="sxs-lookup"><span data-stu-id="be989-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-135">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="be989-136">Zodra een taak die wordt gevolgd door een taak is beëindigd, moet u de methode EndJob aanroepen voor deze taak door de taaknaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="be989-136">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="be989-137">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-137">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="be989-138">Melden van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="be989-138">Reporting Events</span></span>
<span data-ttu-id="be989-139">Er is drie soorten gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="be989-139">There is three types of events :</span></span>

* <span data-ttu-id="be989-140">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="be989-140">Standalone events</span></span>
* <span data-ttu-id="be989-141">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="be989-141">Session events</span></span>
* <span data-ttu-id="be989-142">Gebeurtenissen van de taak</span><span class="sxs-lookup"><span data-stu-id="be989-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="be989-143">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="be989-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-144">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="be989-145">Er kunnen zelfstandige gebeurtenissen plaatsvinden buiten de context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="be989-145">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="be989-146">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="be989-147">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="be989-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-148">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="be989-149">Sessiegebeurtenissen worden meestal gebruikt voor het rapporteren van de acties die worden uitgevoerd door een gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="be989-149">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="be989-150">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-150">Example</span></span>
<span data-ttu-id="be989-151">**Zonder gegevens:**</span><span class="sxs-lookup"><span data-stu-id="be989-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="be989-152">**Met gegevens:**</span><span class="sxs-lookup"><span data-stu-id="be989-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="be989-153">Taakgebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="be989-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-154">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="be989-155">Taakgebeurtenissen worden meestal gebruikt voor het rapporteren van de acties die door een gebruiker tijdens een taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="be989-155">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="be989-156">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="be989-157">Rapportage van fouten</span><span class="sxs-lookup"><span data-stu-id="be989-157">Reporting Errors</span></span>
<span data-ttu-id="be989-158">Er zijn drie soorten fouten:</span><span class="sxs-lookup"><span data-stu-id="be989-158">There are three types of errors :</span></span>

* <span data-ttu-id="be989-159">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="be989-159">Standalone errors</span></span>
* <span data-ttu-id="be989-160">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="be989-160">Session errors</span></span>
* <span data-ttu-id="be989-161">Taakfouten</span><span class="sxs-lookup"><span data-stu-id="be989-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="be989-162">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="be989-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-163">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="be989-164">Zelfstandige fouten kunnen strijd sessie-fouten optreden buiten de context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="be989-164">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="be989-165">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="be989-166">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="be989-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-167">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="be989-168">Sessie-fouten worden gewoonlijk gebruikt voor het rapporteren van de fouten die invloed hebben op de gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="be989-168">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="be989-169">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="be989-170">Taakfouten</span><span class="sxs-lookup"><span data-stu-id="be989-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-171">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="be989-172">Fouten kunnen zijn gerelateerd aan een actieve taak in plaats van te wijten aan de huidige gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="be989-172">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="be989-173">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="be989-174">Reporting Crashes</span><span class="sxs-lookup"><span data-stu-id="be989-174">Reporting Crashes</span></span>
<span data-ttu-id="be989-175">De agent biedt twee methoden om te gaan met crashes.</span><span class="sxs-lookup"><span data-stu-id="be989-175">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="be989-176">Een uitzondering verzenden</span><span class="sxs-lookup"><span data-stu-id="be989-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-177">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="be989-178">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-178">Example</span></span>
<span data-ttu-id="be989-179">U kunt een uitzondering op elk gewenst moment kunt verzenden door aan te roepen:</span><span class="sxs-lookup"><span data-stu-id="be989-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="be989-180">U kunt ook een optionele parameter gebruiken om de sessie engagement op hetzelfde moment dan het verzenden van de crash te beëindigen.</span><span class="sxs-lookup"><span data-stu-id="be989-180">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="be989-181">Bellen om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="be989-181">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="be989-182">Als u dat doet, wordt de sessie en taken worden gesloten na het verzenden van de crash.</span><span class="sxs-lookup"><span data-stu-id="be989-182">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="be989-183">Verzenden van een onverwerkte uitzondering</span><span class="sxs-lookup"><span data-stu-id="be989-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="be989-184">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="be989-185">Engagement biedt ook een methode voor het verzenden van niet-verwerkte uitzonderingen hebt u **UITGESCHAKELDE** Engagement automatisch **crash** reporting.</span><span class="sxs-lookup"><span data-stu-id="be989-185">Engagement also provides a method to send unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="be989-186">Dit is vooral nuttig wanneer gebruikt in de toepassing UnhandledException gebeurtenis-handler.</span><span class="sxs-lookup"><span data-stu-id="be989-186">This is especially useful when used inside the application UnhandledException event handler.</span></span>

<span data-ttu-id="be989-187">Deze methode wordt **altijd** de engagement-sessie en taken te beëindigen nadat deze is aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="be989-187">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="be989-188">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-188">Example</span></span>
<span data-ttu-id="be989-189">U kunt deze gebruiken voor het implementeren van uw eigen UnhandledExceptionEventArgs-handler.</span><span class="sxs-lookup"><span data-stu-id="be989-189">You can use it to implement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="be989-190">Bijvoorbeeld, voeg de `Current_UnhandledException` methode van de `App.xaml.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="be989-190">For example, add the `Current_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="be989-191">Voeg in App.xaml.cs in "Openbare App() {}" toe:</span><span class="sxs-lookup"><span data-stu-id="be989-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="be989-192">Apparaat-Id</span><span class="sxs-lookup"><span data-stu-id="be989-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="be989-193">U kunt de engagement apparaat-id ophalen door deze methode aanroept.</span><span class="sxs-lookup"><span data-stu-id="be989-193">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="be989-194">Parameters voor extra 's</span><span class="sxs-lookup"><span data-stu-id="be989-194">Extras parameters</span></span>
<span data-ttu-id="be989-195">Willekeurige gegevens kunnen worden gekoppeld aan een gebeurtenis, een fout, een activiteit of een taak.</span><span class="sxs-lookup"><span data-stu-id="be989-195">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="be989-196">Deze gegevens kunnen worden onderverdeeld met behulp van een woordenboek.</span><span class="sxs-lookup"><span data-stu-id="be989-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="be989-197">Sleutels en waarden kunnen van elk type zijn.</span><span class="sxs-lookup"><span data-stu-id="be989-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="be989-198">Extra gegevens worden geserialiseerd, dus als u wilt uw eigen type invoegen in extra's u moet een gegevenscontract voor dit type toevoegen.</span><span class="sxs-lookup"><span data-stu-id="be989-198">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="be989-199">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-199">Example</span></span>
<span data-ttu-id="be989-200">We maken een nieuwe klasse 'Persoon'.</span><span class="sxs-lookup"><span data-stu-id="be989-200">We create a new class "Person".</span></span>

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

<span data-ttu-id="be989-201">Vervolgens voegen we toe een `Person` een extra exemplaar.</span><span class="sxs-lookup"><span data-stu-id="be989-201">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="be989-202">Als u andere typen objecten plaatst, zorg er dan voor dat hun methode ToString() wordt geïmplementeerd om een menselijke leesbare tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="be989-202">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="be989-203">Limieten</span><span class="sxs-lookup"><span data-stu-id="be989-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="be989-204">Sleutels</span><span class="sxs-lookup"><span data-stu-id="be989-204">Keys</span></span>
<span data-ttu-id="be989-205">Elke sleutel in het object moet overeenkomen met de volgende reguliere expressie:</span><span class="sxs-lookup"><span data-stu-id="be989-205">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="be989-206">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="be989-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="be989-207">Grootte</span><span class="sxs-lookup"><span data-stu-id="be989-207">Size</span></span>
<span data-ttu-id="be989-208">Extra's zijn beperkt tot **1024** tekens per aanroep.</span><span class="sxs-lookup"><span data-stu-id="be989-208">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="be989-209">Rapportage-toepassingsinformatie</span><span class="sxs-lookup"><span data-stu-id="be989-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="be989-210">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="be989-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="be989-211">U kunt handmatig bijhouden informatie (of andere toepassing specifieke gegevens) met behulp van de SendAppInfo() functie rapporteren.</span><span class="sxs-lookup"><span data-stu-id="be989-211">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="be989-212">Merk op dat deze gegevens stapsgewijs kunnen worden verzonden: alleen de meest recente waarde voor een opgegeven sleutel worden behouden voor een bepaald apparaat.</span><span class="sxs-lookup"><span data-stu-id="be989-212">Note that this data can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="be989-213">Als gebeurtenis extra's, een woordenlijst gebruiken\<-object, object\> gegevens koppelen.</span><span class="sxs-lookup"><span data-stu-id="be989-213">Like event extras, use a Dictionary\<object, object\> to attach data.</span></span>

### <a name="example"></a><span data-ttu-id="be989-214">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="be989-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="be989-215">Limieten</span><span class="sxs-lookup"><span data-stu-id="be989-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="be989-216">Sleutels</span><span class="sxs-lookup"><span data-stu-id="be989-216">Keys</span></span>
<span data-ttu-id="be989-217">Elke sleutel in het object moet overeenkomen met de volgende reguliere expressie:</span><span class="sxs-lookup"><span data-stu-id="be989-217">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="be989-218">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="be989-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="be989-219">Grootte</span><span class="sxs-lookup"><span data-stu-id="be989-219">Size</span></span>
<span data-ttu-id="be989-220">Toepassingsinformatie is beperkt tot **1024** tekens per aanroep.</span><span class="sxs-lookup"><span data-stu-id="be989-220">Application information is limited to **1024** characters per call.</span></span>

<span data-ttu-id="be989-221">In het vorige voorbeeld is de JSON naar de server verzonden 44 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="be989-221">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="be989-222">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="be989-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="be989-223">Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="be989-223">Enable Logging</span></span>
<span data-ttu-id="be989-224">De SDK kan worden geconfigureerd voor het produceren van Logboeken van de test in de IDE-console.</span><span class="sxs-lookup"><span data-stu-id="be989-224">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="be989-225">Deze logboeken worden niet standaard geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="be989-225">These logs are not activated by default.</span></span> <span data-ttu-id="be989-226">Werk de eigenschap voor het aanpassen van dit `EngagementAgent.Instance.TestLogEnabled` op een van de waarde in de `EngagementTestLogLevel` opsomming, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="be989-226">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

