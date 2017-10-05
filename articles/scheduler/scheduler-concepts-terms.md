---
title: Scheduler-concepten, -termen en -entiteiten | Microsoft Docs
description: "Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie, inclusief jobs en jobverzamelingen.  Toont een uitgebreid voorbeeld van een geplande job."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 0f035b58ccd140a5481703df7e184206da2ed651
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="57dc8-104">Schedulerconcepten, -terminologie en -entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="57dc8-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="57dc8-105">Scheduler-entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="57dc8-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="57dc8-106">In de volgende tabel worden de belangrijkste resources beschreven die door de Scheduler-API beschikbaar worden gemaakt of worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="57dc8-106">The following table describes the main resources exposed or used by the Scheduler API:</span></span>

| <span data-ttu-id="57dc8-107">Resource</span><span class="sxs-lookup"><span data-stu-id="57dc8-107">Resource</span></span> | <span data-ttu-id="57dc8-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="57dc8-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57dc8-109">**Jobverzameling**</span><span class="sxs-lookup"><span data-stu-id="57dc8-109">**Job collection**</span></span> |<span data-ttu-id="57dc8-110">Een jobverzameling bevat een aantal jobs en onderhoudt instellingen, quota en vertragingen die worden gedeeld door jobs binnen de verzameling.</span><span class="sxs-lookup"><span data-stu-id="57dc8-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within the collection.</span></span> <span data-ttu-id="57dc8-111">Een jobverzameling wordt gemaakt door de eigenaar van een abonnement en groepeert jobs op basis van gebruiks- of toepassingsgrenzen.</span><span class="sxs-lookup"><span data-stu-id="57dc8-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="57dc8-112">Een jobverzameling is beperkt tot één regio.</span><span class="sxs-lookup"><span data-stu-id="57dc8-112">It’s constrained to one region.</span></span> <span data-ttu-id="57dc8-113">U kunt er ook quota mee afdwingen om het gebruik van alle jobs in die verzameling te beperken.</span><span class="sxs-lookup"><span data-stu-id="57dc8-113">It also allows the enforcement of quotas to constrain the usage of all jobs in that collection.</span></span> <span data-ttu-id="57dc8-114">De quota omvatten MaxJobs en MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="57dc8-114">The quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="57dc8-115">**Job**</span><span class="sxs-lookup"><span data-stu-id="57dc8-115">**Job**</span></span> |<span data-ttu-id="57dc8-116">Een job definieert één terugkerende actie, met eenvoudige of complexe strategieën, die moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="57dc8-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="57dc8-117">Acties omvatten mogelijk HTTP-, opslagwachtrij-, Service Bus-wachtrij- of Service Bus-onderwerpaanvragen.</span><span class="sxs-lookup"><span data-stu-id="57dc8-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="57dc8-118">**Jobgeschiedenis**</span><span class="sxs-lookup"><span data-stu-id="57dc8-118">**Job history**</span></span> |<span data-ttu-id="57dc8-119">Een jobgeschiedenis bevat de details van de uitvoering van een job.</span><span class="sxs-lookup"><span data-stu-id="57dc8-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="57dc8-120">Hierin wordt aangegeven of de job is geslaagd of mislukt. U vindt hierin ook alle responsdetails.</span><span class="sxs-lookup"><span data-stu-id="57dc8-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="57dc8-121">Scheduler-entiteitsbeheer</span><span class="sxs-lookup"><span data-stu-id="57dc8-121">Scheduler entity management</span></span>
<span data-ttu-id="57dc8-122">Op een hoog niveau maken de Scheduler-API en de Service Management-API de volgende bewerkingen beschikbaar op de resources:</span><span class="sxs-lookup"><span data-stu-id="57dc8-122">At a high level, the scheduler and the service management API expose the following operations on the resources:</span></span>

| <span data-ttu-id="57dc8-123">Mogelijkheid</span><span class="sxs-lookup"><span data-stu-id="57dc8-123">Capability</span></span> | <span data-ttu-id="57dc8-124">Beschrijving en URI-adres</span><span class="sxs-lookup"><span data-stu-id="57dc8-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="57dc8-125">**Beheer van jobverzameling**</span><span class="sxs-lookup"><span data-stu-id="57dc8-125">**Job collection management**</span></span> |<span data-ttu-id="57dc8-126">GET-, PUT- en DELETE-ondersteuning voor het maken en wijzigen van jobverzamelingen en de daarin opgenomen jobs.</span><span class="sxs-lookup"><span data-stu-id="57dc8-126">GET, PUT, and DELETE support for creating and modifying job collections and the jobs contained therein.</span></span> <span data-ttu-id="57dc8-127">Een jobverzameling is een container voor jobs en is toegewezen aan quota en gedeelde instellingen.</span><span class="sxs-lookup"><span data-stu-id="57dc8-127">A job collection is a container for jobs and maps to quotas and shared settings.</span></span> <span data-ttu-id="57dc8-128">Voorbeelden van quota, die verderop worden beschreven, zijn maximum aantal jobs en kleinste terugkeerpatroon.</span><span class="sxs-lookup"><span data-stu-id="57dc8-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="57dc8-129">PUT en DELETE:`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="57dc8-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="57dc8-130">GET:`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="57dc8-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="57dc8-131">**Jobbeheer**</span><span class="sxs-lookup"><span data-stu-id="57dc8-131">**Job management**</span></span> |<span data-ttu-id="57dc8-132">Ondersteuning voor GET, PUT, POST, PATCH en DELETE voor het maken en wijzigen van jobs.</span><span class="sxs-lookup"><span data-stu-id="57dc8-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="57dc8-133">Alle jobs moeten behoren tot een jobverzameling die al bestaat. Er wordt dus niet impliciet een gemaakt.</span><span class="sxs-lookup"><span data-stu-id="57dc8-133">All jobs must belong to a job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="57dc8-134">**Beheer van jobgeschiedenis**</span><span class="sxs-lookup"><span data-stu-id="57dc8-134">**Job history management**</span></span> |<span data-ttu-id="57dc8-135">Ondersteuning voor GET voor het ophalen van een geschiedenis van 60 dagen van uitgevoerde jobs, zoals de verstreken tijd van jobs en de resultaten van het uitvoeren van jobs.</span><span class="sxs-lookup"><span data-stu-id="57dc8-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="57dc8-136">Voegt ondersteuning toe voor querytekenreeksparameters om te filteren op basis van toestand en status.</span><span class="sxs-lookup"><span data-stu-id="57dc8-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="57dc8-137">Jobtypen</span><span class="sxs-lookup"><span data-stu-id="57dc8-137">Job types</span></span>
<span data-ttu-id="57dc8-138">Er zijn meerdere typen jobs: HTTP-jobs (inclusief HTTPS-jobs die ondersteuning bieden voor SSL), opslagwachtrijjobs Service Bus-wachtrijjobs en Service Bus-onderwerpjobs.</span><span class="sxs-lookup"><span data-stu-id="57dc8-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="57dc8-139">HTTP-jobs zijn ideaal als u een eindpunt van een bestaande workload of service hebt.</span><span class="sxs-lookup"><span data-stu-id="57dc8-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="57dc8-140">U kunt opslagwachtrijjobs gebruiken om berichten te posten naar opslagwachtrijen, zodat die jobs ideaal zijn voor workloads die gebruikmaken van opslagwachtrijen.</span><span class="sxs-lookup"><span data-stu-id="57dc8-140">You can use storage queue jobs to post messages to storage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="57dc8-141">Zo zijn Service Bus-jobs ook ideaal voor workloads die gebruikmaken van Service Bus-wachtrijen en -onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="57dc8-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="the-job-entity-in-detail"></a><span data-ttu-id="57dc8-142">De entiteit "job" in detail</span><span class="sxs-lookup"><span data-stu-id="57dc8-142">The "job" entity in detail</span></span>
<span data-ttu-id="57dc8-143">Op basisniveau bevat een geplande job verschillende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="57dc8-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="57dc8-144">De actie die moet worden uitgevoerd wanneer de timer van de job wordt gestart</span><span class="sxs-lookup"><span data-stu-id="57dc8-144">The action to perform when the job timer fires</span></span>  
* <span data-ttu-id="57dc8-145">(Optioneel) De tijd voor het uitvoeren van de job</span><span class="sxs-lookup"><span data-stu-id="57dc8-145">(Optional) The time to run the job</span></span>  
* <span data-ttu-id="57dc8-146">(Optioneel) Wanneer en hoe vaak de job moet worden herhaald</span><span class="sxs-lookup"><span data-stu-id="57dc8-146">(Optional) When and how often to repeat the job</span></span>  
* <span data-ttu-id="57dc8-147">(Optioneel) Een actie die moet worden gestart als de primaire actie mislukt</span><span class="sxs-lookup"><span data-stu-id="57dc8-147">(Optional) An action to fire if the primary action fails</span></span>  

<span data-ttu-id="57dc8-148">Intern bevat een geplande job ook door het systeem geleverde gegevens, zoals de volgende geplande uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="57dc8-148">Internally, a scheduled job also contains system-provided data such as the next scheduled execution time.</span></span>

<span data-ttu-id="57dc8-149">De volgende code geeft een uitgebreid voorbeeld van een geplande job.</span><span class="sxs-lookup"><span data-stu-id="57dc8-149">The following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="57dc8-150">Details hierover vindt u in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="57dc8-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often to fire (default to 1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default to recur infinitely)
            "endTime": "2012-11-04",                     // optional (default to recur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="57dc8-151">Zoals u in het voorbeeld van een geplande job hierboven ziet, heeft een jobdefinitie verschillende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="57dc8-151">As seen in the sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="57dc8-152">Begintijd ("startTime")</span><span class="sxs-lookup"><span data-stu-id="57dc8-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="57dc8-153">Actie ("action"), die een foutactie ("errorAction") bevat</span><span class="sxs-lookup"><span data-stu-id="57dc8-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="57dc8-154">Terugkeerpatroon ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="57dc8-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="57dc8-155">Toestand ("state")</span><span class="sxs-lookup"><span data-stu-id="57dc8-155">State (“state”)</span></span>  
* <span data-ttu-id="57dc8-156">Status ("status"</span><span class="sxs-lookup"><span data-stu-id="57dc8-156">Status (“status”)</span></span>  
* <span data-ttu-id="57dc8-157">Beleid voor opnieuw proberen ("retryPolicy")</span><span class="sxs-lookup"><span data-stu-id="57dc8-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="57dc8-158">Hieronder vindt u een toelichting van elk van deze onderdelen:</span><span class="sxs-lookup"><span data-stu-id="57dc8-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="57dc8-159">startTime</span><span class="sxs-lookup"><span data-stu-id="57dc8-159">startTime</span></span>
<span data-ttu-id="57dc8-160">De "startTime" is de starttijd. Hiermee kan de aanroeper bij de verbinding een tijdzoneverschil opgeven in [ISO 8601-notatie](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="57dc8-160">The "startTime” is the start time and allows the caller to specify a time zone offset on the wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="57dc8-161">action en errorAction</span><span class="sxs-lookup"><span data-stu-id="57dc8-161">action and errorAction</span></span>
<span data-ttu-id="57dc8-162">De "action" is de actie die bij elke herhaling wordt aangeroepen en beschrijft een type serviceaanroep.</span><span class="sxs-lookup"><span data-stu-id="57dc8-162">The “action” is the action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="57dc8-163">De actie is datgene wat wordt uitgevoerd volgens de opgegeven planning.</span><span class="sxs-lookup"><span data-stu-id="57dc8-163">The action is what will be executed on the provided schedule.</span></span> <span data-ttu-id="57dc8-164">Scheduler biedt ondersteuning voor HTTP-, opslagwachtrij-, Service Bus-onderwerp- en Service Bus-wachtrijacties.</span><span class="sxs-lookup"><span data-stu-id="57dc8-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="57dc8-165">De actie in het bovenstaande voorbeeld is een HTTP-actie.</span><span class="sxs-lookup"><span data-stu-id="57dc8-165">The action in the example above is an HTTP action.</span></span> <span data-ttu-id="57dc8-166">Hieronder volgt een voorbeeld van een opslagwachtrijactie:</span><span class="sxs-lookup"><span data-stu-id="57dc8-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="57dc8-167">Hieronder volgt een voorbeeld van een Service Bus-onderwerpactie.</span><span class="sxs-lookup"><span data-stu-id="57dc8-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="57dc8-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="57dc8-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="57dc8-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="57dc8-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="57dc8-170">Hieronder volgt een voorbeeld van een Service Bus-wachtrijactie:</span><span class="sxs-lookup"><span data-stu-id="57dc8-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="57dc8-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="57dc8-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="57dc8-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Kan netMessaging of AMQP zijn "authentication": {</span><span class="sxs-lookup"><span data-stu-id="57dc8-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="57dc8-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Een bericht",</span><span class="sxs-lookup"><span data-stu-id="57dc8-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="57dc8-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="57dc8-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="57dc8-175">De "errorAction" is de foutafhandeling, de actie die wordt aangeroepen wanneer de primaire actie mislukt.</span><span class="sxs-lookup"><span data-stu-id="57dc8-175">The “errorAction” is the error handler, the action invoked when the primary action fails.</span></span> <span data-ttu-id="57dc8-176">U kunt deze variabele gebruiken om een eindpunt voor foutafhandeling aan te roepen of een gebruikersmelding te verzenden.</span><span class="sxs-lookup"><span data-stu-id="57dc8-176">You can use this variable to call an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="57dc8-177">Dit kan worden gebruikt om een secundair eindpunt te bereiken in het geval dat het primaire eindpunt niet beschikbaar is (bijvoorbeeld in het geval van een noodgeval op de site van het eindpunt). Het kan ook worden gebruikt voor de kennisgeving van een eindpunt voor foutafhandeling.</span><span class="sxs-lookup"><span data-stu-id="57dc8-177">This can be used for reaching a secondary endpoint in the case that the primary is not available (e.g., in the case of a disaster at the endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="57dc8-178">Net als de primaire actie kan ook de foutactie een eenvoudige of samengestelde logica zijn op basis van andere acties.</span><span class="sxs-lookup"><span data-stu-id="57dc8-178">Just like the primary action, the error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="57dc8-179">Zie [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx) (Een Shared Access Signature maken en gebruiken) voor meer informatie over het maken van een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="57dc8-179">To learn how to create a SAS token, refer to [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="57dc8-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="57dc8-180">recurrence</span></span>
<span data-ttu-id="57dc8-181">Recurrence heeft meerdere onderdelen:</span><span class="sxs-lookup"><span data-stu-id="57dc8-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="57dc8-182">Frequentie ("frequency"): minuut, uur, dag, week, maand of jaar</span><span class="sxs-lookup"><span data-stu-id="57dc8-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="57dc8-183">Interval ("interval"): interval voor de opgegeven herhaling</span><span class="sxs-lookup"><span data-stu-id="57dc8-183">Interval: Interval at the given frequency for the recurrence</span></span>  
* <span data-ttu-id="57dc8-184">Voorgeschreven planning ("schedule"): geef de minuten, uren, weekdagen, maanden en maanddagen op van het terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="57dc8-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of the recurrence</span></span>  
* <span data-ttu-id="57dc8-185">Aantal ("count"): het aantal herhalingen</span><span class="sxs-lookup"><span data-stu-id="57dc8-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="57dc8-186">Eindtijd ("endTime"): na de opgegeven eindtijd worden geen jobs uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="57dc8-186">End time: No jobs will execute after the specified end time</span></span>  

<span data-ttu-id="57dc8-187">Een job wordt herhaald als hiervoor in de JSON-definitie van de job een terugkerend object is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="57dc8-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="57dc8-188">Als zowel "count" als "endTime" worden opgegeven, wordt de voltooiingsregel die het eerst is vermeld, uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="57dc8-188">If both count and endTime are specified, the completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="57dc8-189">state</span><span class="sxs-lookup"><span data-stu-id="57dc8-189">state</span></span>
<span data-ttu-id="57dc8-190">De toestand (state) van de job is een van deze vier waarden: enabled, disabled, completed, or faulted (ingeschakeld, uitgeschakeld, voltooid of mislukt).</span><span class="sxs-lookup"><span data-stu-id="57dc8-190">The state of the job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="57dc8-191">U kunt voor jobs een PUT of PATCH uitvoeren om ze bij te werken met de status enabled (ingeschakeld) of disabled (uitgeschakeld).</span><span class="sxs-lookup"><span data-stu-id="57dc8-191">You can PUT or PATCH jobs so as to update them to the enabled or disabled state.</span></span> <span data-ttu-id="57dc8-192">Als een job is voltooid of mislukt, is dat een eindtoestand die niet kan worden bijgewerkt (hoewel de job nog steeds kan worden verwijderd met DELETE).</span><span class="sxs-lookup"><span data-stu-id="57dc8-192">If a job has been completed or faulted, that is a final state that cannot be updated (though the job can still be DELETED).</span></span> <span data-ttu-id="57dc8-193">De eigenschap state kan er bijvoorbeeld als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="57dc8-193">An example of the state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="57dc8-194">Voltooide en mislukte jobs worden na 60 dagen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="57dc8-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="57dc8-195">status</span><span class="sxs-lookup"><span data-stu-id="57dc8-195">status</span></span>
<span data-ttu-id="57dc8-196">Nadat een Scheduler-job is gestart, wordt informatie over de huidige status van de job geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="57dc8-196">Once a Scheduler job has started, information will be returned about the current status of the job.</span></span> <span data-ttu-id="57dc8-197">Dit object kan niet worden ingesteld door de gebruiker, maar wordt door het systeem ingesteld.</span><span class="sxs-lookup"><span data-stu-id="57dc8-197">This object is not settable by the user—it’s set by the system.</span></span> <span data-ttu-id="57dc8-198">Het is echter opgenomen in het jobobject (in plaats van een afzonderlijke gekoppelde resource) zodat de status van een job eenvoudig kan worden verkregen.</span><span class="sxs-lookup"><span data-stu-id="57dc8-198">However, it is included in the job object (rather than a separate linked resource) so that one can obtain the status of a job easily.</span></span>

<span data-ttu-id="57dc8-199">De jobstatus bevat de tijd van de vorige uitvoering (indien van toepassing), het tijdstip van de volgende geplande uitvoering (voor jobs die in uitvoering zijn) en het aantal keer dat de job is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="57dc8-199">Job status includes the time of the previous execution (if any), the time of the next scheduled execution (for in-progress jobs), and the execution count of the job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="57dc8-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="57dc8-200">retryPolicy</span></span>
<span data-ttu-id="57dc8-201">Als een Scheduler-job is mislukt, is het mogelijk om een beleid voor opnieuw proberen op te geven, om te bepalen of en hoe wordt geprobeerd om de actie opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="57dc8-201">If a Scheduler job fails, it is possible to specify a retry policy to determine whether and how the action is retried.</span></span> <span data-ttu-id="57dc8-202">Dit wordt bepaald door het object **retryType**: dat is ingesteld op **none** (geen) als er geen beleid voor opnieuw proberen is opgegeven, zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="57dc8-202">This is determined by the **retryType** object—it is set to **none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="57dc8-203">Het is ingesteld op **fixed** (vast) als er wel een beleid voor opnieuw proberen is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="57dc8-203">Set it to **fixed** if there is a retry policy.</span></span>

<span data-ttu-id="57dc8-204">Om een beleid voor opnieuw proberen in te stellen, kunnen twee extra instellingen worden opgegeven: een interval voor nieuwe poging (**retryInterval**) en het aantal nieuwe pogingen (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="57dc8-204">To set a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and the number of retries (**retryCount**).</span></span>

<span data-ttu-id="57dc8-205">Het interval voor een nieuwe poging, dat met het object **retryInterval** wordt opgegeven, is het interval tussen nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="57dc8-205">The retry interval, specified with the **retryInterval** object, is the interval between retries.</span></span> <span data-ttu-id="57dc8-206">De standaardwaarde is 30 seconden, de configureerbare minimumwaarde is 15 seconden en de maximumwaarde is 18 maanden.</span><span class="sxs-lookup"><span data-stu-id="57dc8-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="57dc8-207">Jobs in gratis jobverzamelingen hebben een configureerbare minimumwaarde van 1 uur.</span><span class="sxs-lookup"><span data-stu-id="57dc8-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="57dc8-208">Dit interval wordt gedefinieerd in de ISO 8601-notatie.</span><span class="sxs-lookup"><span data-stu-id="57dc8-208">It is defined in the ISO 8601 format.</span></span> <span data-ttu-id="57dc8-209">Op dezelfde manier wordt de waarde van het aantal nieuwe pogingen opgegeven met het object **retryCount**; dit is het aantal keren dat een nieuwe poging wordt gedaan.</span><span class="sxs-lookup"><span data-stu-id="57dc8-209">Similarly, the value of the number of retries is specified with the **retryCount** object; it is the number of times a retry is attempted.</span></span> <span data-ttu-id="57dc8-210">De standaardwaarde is 4 en de maximumwaarde is 20\.</span><span class="sxs-lookup"><span data-stu-id="57dc8-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="57dc8-211">Beide **retryInterval** en **retryCount** zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="57dc8-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="57dc8-212">Ze hebben hun standaardwaarden als **retryType** is ingesteld op **fixed** en er niet expliciet waarden zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="57dc8-212">They are given their default values if **retryType** is set to **fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="57dc8-213">Zie ook</span><span class="sxs-lookup"><span data-stu-id="57dc8-213">See also</span></span>
 [<span data-ttu-id="57dc8-214">Wat is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="57dc8-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="57dc8-215">Aan de slag met behulp van Scheduler in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="57dc8-215">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="57dc8-216">Plannen en facturering in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="57dc8-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="57dc8-217">Complexe schema's en geavanceerde terugkeerpatronen bouwen met Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="57dc8-217">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="57dc8-218">Naslaginformatie over REST API van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="57dc8-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="57dc8-219">Naslaginformatie over Azure Scheduler PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="57dc8-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="57dc8-220">Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="57dc8-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="57dc8-221">Azure Scheduler-limieten, standaardwaarden en foutcodes</span><span class="sxs-lookup"><span data-stu-id="57dc8-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="57dc8-222">Azure Scheduler uitgaande verificatie</span><span class="sxs-lookup"><span data-stu-id="57dc8-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

