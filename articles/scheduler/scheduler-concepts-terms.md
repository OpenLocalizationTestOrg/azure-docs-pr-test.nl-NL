---
title: aaaScheduler concepten, termen en entiteiten | Microsoft Docs
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
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="2aa4c-104">Schedulerconcepten, -terminologie en -entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="2aa4c-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="2aa4c-105">Scheduler-entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="2aa4c-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="2aa4c-106">Hallo beschrijft volgende tabel de belangrijkste resources Hallo beschikbaar worden gemaakt of gebruikt door Hallo Scheduler API:</span><span class="sxs-lookup"><span data-stu-id="2aa4c-106">hello following table describes hello main resources exposed or used by hello Scheduler API:</span></span>

| <span data-ttu-id="2aa4c-107">Resource</span><span class="sxs-lookup"><span data-stu-id="2aa4c-107">Resource</span></span> | <span data-ttu-id="2aa4c-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2aa4c-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2aa4c-109">**Jobverzameling**</span><span class="sxs-lookup"><span data-stu-id="2aa4c-109">**Job collection**</span></span> |<span data-ttu-id="2aa4c-110">Een jobverzameling bevat een aantal jobs en onderhoudt instellingen, quota en vertragingen die worden gedeeld door jobs binnen Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within hello collection.</span></span> <span data-ttu-id="2aa4c-111">Een jobverzameling wordt gemaakt door de eigenaar van een abonnement en groepeert jobs op basis van gebruiks- of toepassingsgrenzen.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="2aa4c-112">Er is beperkte tooone regio.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-112">It’s constrained tooone region.</span></span> <span data-ttu-id="2aa4c-113">Kunt u ook quota mee afdwingen Hallo tooconstrain Hallo gebruik van alle jobs in die verzameling.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-113">It also allows hello enforcement of quotas tooconstrain hello usage of all jobs in that collection.</span></span> <span data-ttu-id="2aa4c-114">Hallo quota omvatten MaxJobs en MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-114">hello quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="2aa4c-115">**Job**</span><span class="sxs-lookup"><span data-stu-id="2aa4c-115">**Job**</span></span> |<span data-ttu-id="2aa4c-116">Een job definieert één terugkerende actie, met eenvoudige of complexe strategieën, die moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="2aa4c-117">Acties omvatten mogelijk HTTP-, opslagwachtrij-, Service Bus-wachtrij- of Service Bus-onderwerpaanvragen.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="2aa4c-118">**Jobgeschiedenis**</span><span class="sxs-lookup"><span data-stu-id="2aa4c-118">**Job history**</span></span> |<span data-ttu-id="2aa4c-119">Een jobgeschiedenis bevat de details van de uitvoering van een job.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="2aa4c-120">Hierin wordt aangegeven of de job is geslaagd of mislukt. U vindt hierin ook alle responsdetails.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="2aa4c-121">Scheduler-entiteitsbeheer</span><span class="sxs-lookup"><span data-stu-id="2aa4c-121">Scheduler entity management</span></span>
<span data-ttu-id="2aa4c-122">Op een hoog niveau weergeven Hallo scheduler en Hallo servicebeheer-API Hallo bewerkingen op Hallo-resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="2aa4c-122">At a high level, hello scheduler and hello service management API expose hello following operations on hello resources:</span></span>

| <span data-ttu-id="2aa4c-123">Mogelijkheid</span><span class="sxs-lookup"><span data-stu-id="2aa4c-123">Capability</span></span> | <span data-ttu-id="2aa4c-124">Beschrijving en URI-adres</span><span class="sxs-lookup"><span data-stu-id="2aa4c-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="2aa4c-125">**Beheer van jobverzameling**</span><span class="sxs-lookup"><span data-stu-id="2aa4c-125">**Job collection management**</span></span> |<span data-ttu-id="2aa4c-126">GET, PUT en DELETE-ondersteuning voor het maken en wijzigen van jobverzamelingen en Hallo taken daarin.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-126">GET, PUT, and DELETE support for creating and modifying job collections and hello jobs contained therein.</span></span> <span data-ttu-id="2aa4c-127">Een jobverzameling is een container voor jobs en tooquotas en gedeelde instellingen worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-127">A job collection is a container for jobs and maps tooquotas and shared settings.</span></span> <span data-ttu-id="2aa4c-128">Voorbeelden van quota, die verderop worden beschreven, zijn maximum aantal jobs en kleinste terugkeerpatroon.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="2aa4c-129">PUT en DELETE:`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="2aa4c-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="2aa4c-130">GET:`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="2aa4c-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="2aa4c-131">**Jobbeheer**</span><span class="sxs-lookup"><span data-stu-id="2aa4c-131">**Job management**</span></span> |<span data-ttu-id="2aa4c-132">Ondersteuning voor GET, PUT, POST, PATCH en DELETE voor het maken en wijzigen van jobs.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="2aa4c-133">Alle taken behoren tooa jobverzameling die al bestaat, zodat er niet impliciet een gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-133">All jobs must belong tooa job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="2aa4c-134">**Beheer van jobgeschiedenis**</span><span class="sxs-lookup"><span data-stu-id="2aa4c-134">**Job history management**</span></span> |<span data-ttu-id="2aa4c-135">Ondersteuning voor GET voor het ophalen van een geschiedenis van 60 dagen van uitgevoerde jobs, zoals de verstreken tijd van jobs en de resultaten van het uitvoeren van jobs.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="2aa4c-136">Voegt ondersteuning toe voor querytekenreeksparameters om te filteren op basis van toestand en status.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="2aa4c-137">Jobtypen</span><span class="sxs-lookup"><span data-stu-id="2aa4c-137">Job types</span></span>
<span data-ttu-id="2aa4c-138">Er zijn meerdere typen jobs: HTTP-jobs (inclusief HTTPS-jobs die ondersteuning bieden voor SSL), opslagwachtrijjobs Service Bus-wachtrijjobs en Service Bus-onderwerpjobs.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="2aa4c-139">HTTP-jobs zijn ideaal als u een eindpunt van een bestaande workload of service hebt.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="2aa4c-140">U kunt wachtrij taken toopost berichten toostorage opslagwachtrijen, zodat die jobs zijn ideaal voor workloads die gebruikmaken van opslagwachtrijen.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-140">You can use storage queue jobs toopost messages toostorage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="2aa4c-141">Zo zijn Service Bus-jobs ook ideaal voor workloads die gebruikmaken van Service Bus-wachtrijen en -onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="hello-job-entity-in-detail"></a><span data-ttu-id="2aa4c-142">entiteit van Hallo "job" in detail</span><span class="sxs-lookup"><span data-stu-id="2aa4c-142">hello "job" entity in detail</span></span>
<span data-ttu-id="2aa4c-143">Op basisniveau bevat een geplande job verschillende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="2aa4c-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="2aa4c-144">Hallo actie tooperform wanneer Hallo taak timer wordt geactiveerd</span><span class="sxs-lookup"><span data-stu-id="2aa4c-144">hello action tooperform when hello job timer fires</span></span>  
* <span data-ttu-id="2aa4c-145">(Optioneel) Hallo tijd toorun Hallo taak</span><span class="sxs-lookup"><span data-stu-id="2aa4c-145">(Optional) hello time toorun hello job</span></span>  
* <span data-ttu-id="2aa4c-146">(Optioneel) Wanneer en hoe vaak toorepeat Hallo taak</span><span class="sxs-lookup"><span data-stu-id="2aa4c-146">(Optional) When and how often toorepeat hello job</span></span>  
* <span data-ttu-id="2aa4c-147">(Optioneel) Een actie toofire als Hallo primaire actie mislukt</span><span class="sxs-lookup"><span data-stu-id="2aa4c-147">(Optional) An action toofire if hello primary action fails</span></span>  

<span data-ttu-id="2aa4c-148">Intern bevat een geplande taak ook systeem geleverde gegevens, zoals Hallo volgende geplande uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-148">Internally, a scheduled job also contains system-provided data such as hello next scheduled execution time.</span></span>

<span data-ttu-id="2aa4c-149">Hallo volgende code geeft een uitgebreid voorbeeld van een geplande taak.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-149">hello following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="2aa4c-150">Details hierover vindt u in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-150">Details are provided in subsequent sections.</span></span>

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
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
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

<span data-ttu-id="2aa4c-151">Zoals u in Hallo voorbeeld een geplande job hierboven, heeft een jobdefinitie verschillende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="2aa4c-151">As seen in hello sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="2aa4c-152">Begintijd ("startTime")</span><span class="sxs-lookup"><span data-stu-id="2aa4c-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="2aa4c-153">Actie ("action"), die een foutactie ("errorAction") bevat</span><span class="sxs-lookup"><span data-stu-id="2aa4c-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="2aa4c-154">Terugkeerpatroon ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="2aa4c-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="2aa4c-155">Toestand ("state")</span><span class="sxs-lookup"><span data-stu-id="2aa4c-155">State (“state”)</span></span>  
* <span data-ttu-id="2aa4c-156">Status ("status"</span><span class="sxs-lookup"><span data-stu-id="2aa4c-156">Status (“status”)</span></span>  
* <span data-ttu-id="2aa4c-157">Beleid voor opnieuw proberen ("retryPolicy")</span><span class="sxs-lookup"><span data-stu-id="2aa4c-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="2aa4c-158">Hieronder vindt u een toelichting van elk van deze onderdelen:</span><span class="sxs-lookup"><span data-stu-id="2aa4c-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="2aa4c-159">startTime</span><span class="sxs-lookup"><span data-stu-id="2aa4c-159">startTime</span></span>
<span data-ttu-id="2aa4c-160">Hallo "startTime" is de begintijd Hallo waardoor Hallo aanroeper toospecify een tijdzone offset op Hallo-kabel in [ISO 8601-notatie](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="2aa4c-160">hello "startTime” is hello start time and allows hello caller toospecify a time zone offset on hello wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="2aa4c-161">action en errorAction</span><span class="sxs-lookup"><span data-stu-id="2aa4c-161">action and errorAction</span></span>
<span data-ttu-id="2aa4c-162">Hallo "action" hello actie die wordt gestart bij elk exemplaar is, en beschrijft een type Serviceaanroep.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-162">hello “action” is hello action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="2aa4c-163">Hallo-actie is wat op Hallo opgegeven planning wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-163">hello action is what will be executed on hello provided schedule.</span></span> <span data-ttu-id="2aa4c-164">Scheduler biedt ondersteuning voor HTTP-, opslagwachtrij-, Service Bus-onderwerp- en Service Bus-wachtrijacties.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="2aa4c-165">Hallo is Hallo bovenstaande voorbeeld een HTTP-actie.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-165">hello action in hello example above is an HTTP action.</span></span> <span data-ttu-id="2aa4c-166">Hieronder volgt een voorbeeld van een opslagwachtrijactie:</span><span class="sxs-lookup"><span data-stu-id="2aa4c-166">Below is an example of a storage queue action:</span></span>

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

<span data-ttu-id="2aa4c-167">Hieronder volgt een voorbeeld van een Service Bus-onderwerpactie.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="2aa4c-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="2aa4c-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="2aa4c-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="2aa4c-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="2aa4c-170">Hieronder volgt een voorbeeld van een Service Bus-wachtrijactie:</span><span class="sxs-lookup"><span data-stu-id="2aa4c-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="2aa4c-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="2aa4c-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="2aa4c-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Kan netMessaging of AMQP zijn "authentication": {</span><span class="sxs-lookup"><span data-stu-id="2aa4c-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="2aa4c-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Een bericht",</span><span class="sxs-lookup"><span data-stu-id="2aa4c-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="2aa4c-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="2aa4c-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="2aa4c-175">Hallo "errorAction" is hello foutafhandeling, Hallo actie die wordt aangeroepen wanneer de primaire actie Hallo mislukt.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-175">hello “errorAction” is hello error handler, hello action invoked when hello primary action fails.</span></span> <span data-ttu-id="2aa4c-176">U kunt deze variabele toocall een eindpunt voor foutafhandeling gebruiken of een gebruikersmelding te verzenden.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-176">You can use this variable toocall an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="2aa4c-177">Dit kan worden gebruikt voor het bereiken van een secundair eindpunt in geval van Hallo die Hallo primaire is niet beschikbaar (bijvoorbeeld in Hallo geval van een noodgeval op de site van het eindpunt Hallo) of kunnen worden gebruikt voor het verwittigen van een eindpunt voor foutafhandeling.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-177">This can be used for reaching a secondary endpoint in hello case that hello primary is not available (e.g., in hello case of a disaster at hello endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="2aa4c-178">Net als de primaire actie hello mag Hallo foutbewerking zijn eenvoudige of samengestelde logica op basis van andere acties.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-178">Just like hello primary action, hello error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="2aa4c-179">hoe toocreate een SAS-token te verwijzen toolearn[maken en gebruiken van een Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="2aa4c-179">toolearn how toocreate a SAS token, refer too[Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="2aa4c-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="2aa4c-180">recurrence</span></span>
<span data-ttu-id="2aa4c-181">Recurrence heeft meerdere onderdelen:</span><span class="sxs-lookup"><span data-stu-id="2aa4c-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="2aa4c-182">Frequentie ("frequency"): minuut, uur, dag, week, maand of jaar</span><span class="sxs-lookup"><span data-stu-id="2aa4c-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="2aa4c-183">Interval: Het tijdsinterval Hallo opgegeven frequentie voor Hallo terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="2aa4c-183">Interval: Interval at hello given frequency for hello recurrence</span></span>  
* <span data-ttu-id="2aa4c-184">Voorgeschreven planning: minuten, uren, weekdagen, maanden en maanddagen op van Hallo terugkeerpatroon opgeven</span><span class="sxs-lookup"><span data-stu-id="2aa4c-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of hello recurrence</span></span>  
* <span data-ttu-id="2aa4c-185">Aantal ("count"): het aantal herhalingen</span><span class="sxs-lookup"><span data-stu-id="2aa4c-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="2aa4c-186">Eindtijd: geen jobs uitgevoerd nadat Hallo eindtijd opgegeven</span><span class="sxs-lookup"><span data-stu-id="2aa4c-186">End time: No jobs will execute after hello specified end time</span></span>  

<span data-ttu-id="2aa4c-187">Een job wordt herhaald als hiervoor in de JSON-definitie van de job een terugkerend object is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="2aa4c-188">Als zowel count en endTime zijn opgegeven, wordt de voltooiingsregel Hallo die eerst gehonoreerd.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-188">If both count and endTime are specified, hello completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="2aa4c-189">state</span><span class="sxs-lookup"><span data-stu-id="2aa4c-189">state</span></span>
<span data-ttu-id="2aa4c-190">status van taak Hallo Hallo is een van de vier waarden: ingeschakeld, uitgeschakeld, voltooid of mislukt.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-190">hello state of hello job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="2aa4c-191">U kunt plaatsen of PATCH zodat taken als tooupdate ze toohello ingeschakeld of uitgeschakeld staat.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-191">You can PUT or PATCH jobs so as tooupdate them toohello enabled or disabled state.</span></span> <span data-ttu-id="2aa4c-192">Als een taak is voltooid of mislukt, is dat een eindtoestand die kan niet worden bijgewerkt (Hoewel Hallo taak kan nog steeds worden verwijderd).</span><span class="sxs-lookup"><span data-stu-id="2aa4c-192">If a job has been completed or faulted, that is a final state that cannot be updated (though hello job can still be DELETED).</span></span> <span data-ttu-id="2aa4c-193">Een voorbeeld van de eigenschap state Hallo is als volgt:</span><span class="sxs-lookup"><span data-stu-id="2aa4c-193">An example of hello state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="2aa4c-194">Voltooide en mislukte jobs worden na 60 dagen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="2aa4c-195">status</span><span class="sxs-lookup"><span data-stu-id="2aa4c-195">status</span></span>
<span data-ttu-id="2aa4c-196">Nadat een Scheduler-job is gestart, wordt informatie geretourneerd over de huidige status van taak Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-196">Once a Scheduler job has started, information will be returned about hello current status of hello job.</span></span> <span data-ttu-id="2aa4c-197">Dit object kan niet worden ingesteld door de gebruiker Hallo — ingesteld door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-197">This object is not settable by hello user—it’s set by hello system.</span></span> <span data-ttu-id="2aa4c-198">Het is echter opgenomen in Hallo taakobject (eerder dan een afzonderlijke gekoppelde resource) zodat Hallo status van een job eenvoudig kan worden verkregen.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-198">However, it is included in hello job object (rather than a separate linked resource) so that one can obtain hello status of a job easily.</span></span>

<span data-ttu-id="2aa4c-199">Taakstatus omvat Hallo-tijd van Hallo vorige uitvoering (indien aanwezig), Hallo tijdstip van Hallo volgende geplande uitvoering (voor taken wordt uitgevoerd) en Hallo uitvoering aantal Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-199">Job status includes hello time of hello previous execution (if any), hello time of hello next scheduled execution (for in-progress jobs), and hello execution count of hello job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="2aa4c-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="2aa4c-200">retryPolicy</span></span>
<span data-ttu-id="2aa4c-201">Als een Scheduler-job is mislukt, is het mogelijk toospecify een nieuwe poging beleid toodetermine of en hoe Hallo actie opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-201">If a Scheduler job fails, it is possible toospecify a retry policy toodetermine whether and how hello action is retried.</span></span> <span data-ttu-id="2aa4c-202">Dit wordt bepaald door Hallo **retryType** object — te is ingesteld**geen** als er geen beleid voor opnieuw proberen, zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-202">This is determined by hello **retryType** object—it is set too**none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="2aa4c-203">Stel deze in te**vaste** als er een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-203">Set it too**fixed** if there is a retry policy.</span></span>

<span data-ttu-id="2aa4c-204">een beleid voor opnieuw proberen tooset twee extra instellingen kunnen worden opgegeven: interval voor opnieuw proberen (**retryInterval**) en het aantal nieuwe pogingen hello (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="2aa4c-204">tooset a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and hello number of retries (**retryCount**).</span></span>

<span data-ttu-id="2aa4c-205">interval voor Hallo opnieuw proberen, opgegeven met de Hallo **retryInterval** object, hello-interval tussen nieuwe pogingen is.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-205">hello retry interval, specified with hello **retryInterval** object, is hello interval between retries.</span></span> <span data-ttu-id="2aa4c-206">De standaardwaarde is 30 seconden, de configureerbare minimumwaarde is 15 seconden en de maximumwaarde is 18 maanden.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="2aa4c-207">Jobs in gratis jobverzamelingen hebben een configureerbare minimumwaarde van 1 uur.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="2aa4c-208">Dit is gedefinieerd in Hallo ISO 8601-notatie.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-208">It is defined in hello ISO 8601 format.</span></span> <span data-ttu-id="2aa4c-209">Op deze manier Hallo-waarde van aantal nieuwe pogingen hello wordt opgegeven met de Hallo **retryCount** object; dit is het aantal keren dat een nieuwe poging wordt gedaan Hallo.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-209">Similarly, hello value of hello number of retries is specified with hello **retryCount** object; it is hello number of times a retry is attempted.</span></span> <span data-ttu-id="2aa4c-210">De standaardwaarde is 4 en de maximumwaarde is 20\.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="2aa4c-211">Beide **retryInterval** en **retryCount** zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="2aa4c-212">De standaardwaarden wordt verstrekt als **retryType** te is ingesteld,**vaste** en geen waarden expliciet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2aa4c-212">They are given their default values if **retryType** is set too**fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="2aa4c-213">Zie ook</span><span class="sxs-lookup"><span data-stu-id="2aa4c-213">See also</span></span>
 [<span data-ttu-id="2aa4c-214">Wat is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="2aa4c-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="2aa4c-215">Aan de slag met behulp van Scheduler in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2aa4c-215">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="2aa4c-216">Plannen en facturering in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="2aa4c-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="2aa4c-217">Hoe plant u toobuild complexe en geavanceerde terugkeerpatronen met Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="2aa4c-217">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="2aa4c-218">Naslaginformatie over REST API van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="2aa4c-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="2aa4c-219">Naslaginformatie over Azure Scheduler PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="2aa4c-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="2aa4c-220">Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="2aa4c-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="2aa4c-221">Azure Scheduler-limieten, standaardwaarden en foutcodes</span><span class="sxs-lookup"><span data-stu-id="2aa4c-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="2aa4c-222">Azure Scheduler uitgaande verificatie</span><span class="sxs-lookup"><span data-stu-id="2aa4c-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

