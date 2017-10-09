---
title: "aaaDesign lijst efficiënt query's, Azure Batch | Microsoft Docs"
description: De prestaties verbeteren door het filteren van uw query's bij het aanvragen van informatie over Batch-resources zoals pools, jobs, taken en rekenknooppunten.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a><span data-ttu-id="7bae7-103">Query's efficiënt toolist Batch-resources maken</span><span class="sxs-lookup"><span data-stu-id="7bae7-103">Create queries toolist Batch resources efficiently</span></span>

<span data-ttu-id="7bae7-104">Hier leert u hoe tooincrease de prestaties van de Azure Batch-toepassing doordat Hallo hoeveelheid gegevens die door Hallo-service worden geretourneerd wanneer u een query uitvoert op taken, taken en rekenknooppunten Hello [Batch .NET] [ api_net] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7bae7-104">Here you'll learn how tooincrease your Azure Batch application's performance by reducing hello amount of data that is returned by hello service when you query jobs, tasks, and compute nodes with hello [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="7bae7-105">Bijna alle Batch-toepassingen moeten tooperform een soort bewaking of een andere bewerking Hallo Batch-service, vaak query met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-105">Nearly all Batch applications need tooperform some type of monitoring or other operation that queries hello Batch service, often at regular intervals.</span></span> <span data-ttu-id="7bae7-106">Bijvoorbeeld, toodetermine of er in een taak resterende taken in de wachtrij zijn, moet u gegevens ophalen voor elke taak in Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="7bae7-106">For example, toodetermine whether there are any queued tasks remaining in a job, you must get data on every task in hello job.</span></span> <span data-ttu-id="7bae7-107">toodetermine hello status van knooppunten in uw pool, moet u gegevens op elk knooppunt in de groep Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-107">toodetermine hello status of nodes in your pool, you must get data on every node in hello pool.</span></span> <span data-ttu-id="7bae7-108">Dit artikel wordt uitgelegd hoe tooexecute zoals query's in Hallo zo efficiënt mogelijk.</span><span class="sxs-lookup"><span data-stu-id="7bae7-108">This article explains how tooexecute such queries in hello most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="7bae7-109">Hallo Batch-service biedt speciale API-ondersteuning voor veelvoorkomende scenario Hallo van taken in een taak worden geteld.</span><span class="sxs-lookup"><span data-stu-id="7bae7-109">hello Batch service provides special API support for hello common scenario of counting tasks in a job.</span></span> <span data-ttu-id="7bae7-110">In plaats van een lijst met query om deze, kunt u Hallo aanroepen [ophalen taak telt] [ rest_get_task_counts] bewerking.</span><span class="sxs-lookup"><span data-stu-id="7bae7-110">Instead of using a list query for these, you can call hello [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="7bae7-111">Aantallen voor GET-taak geeft aan hoeveel taken in behandeling is, zijn uitgevoerd of voltooid en hoeveel taken hebt voltooid of mislukt.</span><span class="sxs-lookup"><span data-stu-id="7bae7-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="7bae7-112">Get-taak telt is efficiënter dan een lijst met query.</span><span class="sxs-lookup"><span data-stu-id="7bae7-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="7bae7-113">Zie voor meer informatie [aantal taken voor een taak op status (Preview)](batch-get-task-counts.md).</span><span class="sxs-lookup"><span data-stu-id="7bae7-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="7bae7-114">Hallo bewerking taak telt ophalen is niet beschikbaar in Batch-versies eerder dan 2017-06-01.5.1.</span><span class="sxs-lookup"><span data-stu-id="7bae7-114">hello Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="7bae7-115">Als u een oudere versie van het Hallo-service gebruikt, gebruikt u een lijst met query toocount taken in een taak in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="7bae7-115">If you are using an older version of hello service, then use a list query toocount tasks in a job instead.</span></span>
>
> 

## <a name="meet-hello-detaillevel"></a><span data-ttu-id="7bae7-116">Voldoen aan de Hallo DetailLevel</span><span class="sxs-lookup"><span data-stu-id="7bae7-116">Meet hello DetailLevel</span></span>
<span data-ttu-id="7bae7-117">In een productie-Batch-toepassing kunnen entiteiten, zoals jobs, taken en rekenknooppunten in Hallo duizendtallen nummeren.</span><span class="sxs-lookup"><span data-stu-id="7bae7-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in hello thousands.</span></span> <span data-ttu-id="7bae7-118">Wanneer u informatie over deze bronnen aanvraagt, moet een grote hoeveelheid gegevens 'afkomstig van Hallo kabel' hello Batch-servicetoepassing tooyour voor elke query.</span><span class="sxs-lookup"><span data-stu-id="7bae7-118">When you request information on these resources, a potentially large amount of data must "cross hello wire" from hello Batch service tooyour application on each query.</span></span> <span data-ttu-id="7bae7-119">U kunt door te beperken het aantal items Hallo en type informatie dat wordt geretourneerd door een query, verhogen Hallo snelheid van uw query's en daarom Hallo prestaties van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7bae7-119">By limiting hello number of items and type of information that is returned by a query, you can increase hello speed of your queries, and therefore hello performance of your application.</span></span>

<span data-ttu-id="7bae7-120">Dit [Batch .NET] [ api_net] API code codefragment lijsten *elke* taak die is gekoppeld aan een taak, samen met *alle* van eigenschappen van elke Hallo taak:</span><span class="sxs-lookup"><span data-stu-id="7bae7-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of hello properties of each task:</span></span>

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="7bae7-121">U kunt echter een lijstquery veel efficiënter uitvoeren door het toepassen van een query tooyour 'detailniveau'.</span><span class="sxs-lookup"><span data-stu-id="7bae7-121">You can perform a much more efficient list query, however, by applying a "detail level" tooyour query.</span></span> <span data-ttu-id="7bae7-122">Dit doet u door het leveren van een [ODATADetailLevel] [ odata] object toohello [JobOperations.ListTasks] [ net_list_tasks] methode.</span><span class="sxs-lookup"><span data-stu-id="7bae7-122">You do this by supplying an [ODATADetailLevel][odata] object toohello [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="7bae7-123">In dit fragment retourneert alleen Hallo-ID, opdrachtregel en compute knooppunt informatie eigenschappen van de voltooide taken:</span><span class="sxs-lookup"><span data-stu-id="7bae7-123">This snippet returns only hello ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="7bae7-124">In dit voorbeeldscenario als er duizenden taken in Hallo-job Hallo resultaten van de tweede query hello wordt doorgaans veel sneller dan Hallo als eerste geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7bae7-124">In this example scenario, if there are thousands of tasks in hello job, hello results from hello second query will typically be returned much quicker than hello first.</span></span> <span data-ttu-id="7bae7-125">Meer informatie over het gebruik van ODATADetailLevel wanneer u objecten Hello Batch .NET API is opgenomen [hieronder](#efficient-querying-in-batch-net).</span><span class="sxs-lookup"><span data-stu-id="7bae7-125">More information about using ODATADetailLevel when you list items with hello Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7bae7-126">Ten zeerste aangeraden dat u *altijd* leveringen een lijst ODATADetailLevel object tooyour .NET API-aanroepen van maximale efficiëntie tooensure en prestaties van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7bae7-126">We highly recommend that you *always* supply an ODATADetailLevel object tooyour .NET API list calls tooensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="7bae7-127">Door te geven een detailniveau, kunt u toolower Batch-service, reactietijden, netwerkgebruik te verbeteren en geheugengebruik minimaliseren door clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-127">By specifying a detail level, you can help toolower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="7bae7-128">Filteren, selecteert en vouw</span><span class="sxs-lookup"><span data-stu-id="7bae7-128">Filter, select, and expand</span></span>
<span data-ttu-id="7bae7-129">Hallo [Batch .NET] [ api_net] en [Batch REST] [ api_rest] API's bieden Hallo mogelijkheid tooreduce beide Hallo aantal items dat wordt geretourneerd in een lijst evenals Hallo hoeveelheid informatie die wordt geretourneerd voor elke.</span><span class="sxs-lookup"><span data-stu-id="7bae7-129">hello [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide hello ability tooreduce both hello number of items that are returned in a list, as well as hello amount of information that is returned for each.</span></span> <span data-ttu-id="7bae7-130">U dit doen door op te geven **filter**, **Selecteer**, en **Vouw tekenreeksen** bij het uitvoeren van de lijst met query's.</span><span class="sxs-lookup"><span data-stu-id="7bae7-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="7bae7-131">Filteren</span><span class="sxs-lookup"><span data-stu-id="7bae7-131">Filter</span></span>
<span data-ttu-id="7bae7-132">Hallo filtertekenreeks is een expressie die het aantal items dat wordt geretourneerd Hallo vermindert.</span><span class="sxs-lookup"><span data-stu-id="7bae7-132">hello filter string is an expression that reduces hello number of items that are returned.</span></span> <span data-ttu-id="7bae7-133">Bijvoorbeeld: lijst alleen hello taken voor een taak, of de lijst alleen rekenknooppunten die gereed toorun taken zijn uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7bae7-133">For example, list only hello running tasks for a job, or list only compute nodes that are ready toorun tasks.</span></span>

* <span data-ttu-id="7bae7-134">Hallo filtertekenreeks bestaat uit een of meer expressies met een expressie die uit een eigenschapsnaam, een operator en een waarde bestaat.</span><span class="sxs-lookup"><span data-stu-id="7bae7-134">hello filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="7bae7-135">Hallo-eigenschappen die kunnen worden opgegeven zijn specifieke tooeach entiteitstype waarmee u een query uitvoeren, zoals zijn Hallo-operators die worden ondersteund voor elke eigenschap.</span><span class="sxs-lookup"><span data-stu-id="7bae7-135">hello properties that can be specified are specific tooeach entity type that you query, as are hello operators that are supported for each property.</span></span>
* <span data-ttu-id="7bae7-136">Meerdere expressies kunnen worden gecombineerd met behulp van de logische operators Hallo `and` en `or`.</span><span class="sxs-lookup"><span data-stu-id="7bae7-136">Multiple expressions can be combined by using hello logical operators `and` and `or`.</span></span>
* <span data-ttu-id="7bae7-137">In dit voorbeeld filteren tekenreekslijsten alleen Hallo uitgevoerd 'weergeven' taken: `(state eq 'running') and startswith(id, 'renderTask')`.</span><span class="sxs-lookup"><span data-stu-id="7bae7-137">This example filter string lists only hello running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="7bae7-138">Selecteer</span><span class="sxs-lookup"><span data-stu-id="7bae7-138">Select</span></span>
<span data-ttu-id="7bae7-139">Selecteer tekenreeks Hallo beperkt Hallo eigenschapswaarden die voor elk item worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7bae7-139">hello select string limits hello property values that are returned for each item.</span></span> <span data-ttu-id="7bae7-140">U geeft een lijst met namen van eigenschappen en alleen de eigenschapswaarden van deze worden geretourneerd voor items in de queryresultaten Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bae7-140">You specify a list of property names, and only those property values are returned for hello items in hello query results.</span></span>

* <span data-ttu-id="7bae7-141">Selecteer tekenreeks Hallo bestaat uit een door komma's gescheiden lijst met namen van eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-141">hello select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="7bae7-142">U kunt opgeven dat Hallo-eigenschappen voor het entiteitstype Hallo die u een query wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7bae7-142">You can specify any of hello properties for hello entity type you are querying.</span></span>
* <span data-ttu-id="7bae7-143">In dit voorbeeld selecteert tekenreeks dat slechts drie eigenschapswaarden voor elke taak moeten worden geretourneerd: `id, state, stateTransitionTime`.</span><span class="sxs-lookup"><span data-stu-id="7bae7-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="7bae7-144">Uitvouwen</span><span class="sxs-lookup"><span data-stu-id="7bae7-144">Expand</span></span>
<span data-ttu-id="7bae7-145">Hallo Vouw tekenreeks vermindert het aantal API-aanroepen die vereist tooobtain zijn Hallo bepaalde gegevens.</span><span class="sxs-lookup"><span data-stu-id="7bae7-145">hello expand string reduces hello number of API calls that are required tooobtain certain information.</span></span> <span data-ttu-id="7bae7-146">Wanneer u een tekenreeks uit te breiden, meer informatie over elk item kan worden verkregen met één API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="7bae7-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="7bae7-147">In plaats van de eerste verkrijgen Hallo-lijst van entiteiten en vervolgens de aanvragende informatie voor elk item in de lijst hello, die u gebruikt een tekenreeks uit te breiden tooobtain Hallo dezelfde gegevens in één API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="7bae7-147">Rather than first obtaining hello list of entities, then requesting information for each item in hello list, you use an expand string tooobtain hello same information in a single API call.</span></span> <span data-ttu-id="7bae7-148">Minder API-aanroepen betekent betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="7bae7-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="7bae7-149">Vergelijkbare toohello Selecteer tekenreeks Hallo uitvouwen tekenreeks of bepaalde gegevens in de queryresultaten lijst is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-149">Similar toohello select string, hello expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="7bae7-150">Hallo Vouw tekenreeks wordt alleen ondersteund wanneer het wordt gebruikt in de lijst taken, taakschema's, taken en groepen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-150">hello expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="7bae7-151">Op dit moment wordt alleen ondersteund statistische gegevens.</span><span class="sxs-lookup"><span data-stu-id="7bae7-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="7bae7-152">Wanneer alle eigenschappen zijn vereist en er is geen tekenreeks select is opgegeven, Hallo tekenreeks uitvouwen *moet* worden statistische informatie over gebruikte tooget.</span><span class="sxs-lookup"><span data-stu-id="7bae7-152">When all properties are required and no select string is specified, hello expand string *must* be used tooget statistics information.</span></span> <span data-ttu-id="7bae7-153">Als een select-tekenreeks tooobtain een subset van de eigenschappen van de gebruikte is `stats` kan worden opgegeven in de select tekenreeks Hallo en Hallo Vouw tekenreeks niet hoeft toobe opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7bae7-153">If a select string is used tooobtain a subset of properties, then `stats` can be specified in hello select string, and hello expand string does not need toobe specified.</span></span>
* <span data-ttu-id="7bae7-154">In dit voorbeeld Vouw tekenreeks geeft aan dat statistische gegevens moet worden geretourneerd voor elk item in de lijst Hallo: `stats`.</span><span class="sxs-lookup"><span data-stu-id="7bae7-154">This example expand string specifies that statistics information should be returned for each item in hello list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="7bae7-155">Tijdens het construeren van Hallo drie querytypen tekenreeks (filteren, selecteert en vouw), moet u ervoor zorgen dat Hallo eigenschapnamen en case overeenkomen met die van hun collega's REST-API-element.</span><span class="sxs-lookup"><span data-stu-id="7bae7-155">When constructing any of hello three query string types (filter, select, and expand), you must ensure that hello property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="7bae7-156">Bijvoorbeeld, als u werkt met .NET Hallo [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) klasse, moet u **status** in plaats van **status**, ook al Hallo .NET-eigenschap is [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span><span class="sxs-lookup"><span data-stu-id="7bae7-156">For example, when working with hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though hello .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="7bae7-157">Zie Hallo tabellen hieronder voor de eigenschaptoewijzingen tussen Hallo .NET en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="7bae7-157">See hello tables below for property mappings between hello .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="7bae7-158">Regels voor filteren, selecteert en breidt tekenreeksen</span><span class="sxs-lookup"><span data-stu-id="7bae7-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="7bae7-159">Namen van eigenschappen in het filter, selecteert en breidt tekenreeksen moeten worden weergegeven als in Hallo [Batch REST] [ api_rest] API--zelfs wanneer u [Batch .NET] [ api_net] of een andere Batch-SDK Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bae7-159">Properties names in filter, select, and expand strings should appear as they do in hello [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of hello other Batch SDKs.</span></span>
* <span data-ttu-id="7bae7-160">Alle namen van eigenschappen zijn hoofdlettergevoelig, maar eigenschapswaarden zijn niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="7bae7-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="7bae7-161">Datum/tijd tekenreeksen kunnen twee verschillende indelingen, en moet worden voorafgegaan door `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="7bae7-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="7bae7-162">Voorbeeld van W3C-DTF-indeling:`creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="7bae7-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="7bae7-163">Voorbeeld van RFC 1123 indeling:`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="7bae7-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="7bae7-164">Booleaanse tekenreeksen zijn `true` of `false`.</span><span class="sxs-lookup"><span data-stu-id="7bae7-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="7bae7-165">Als een eigenschap is ongeldig of de operator is opgegeven, een `400 (Bad Request)` fout resulteert.</span><span class="sxs-lookup"><span data-stu-id="7bae7-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="7bae7-166">Efficiënter uitvoeren van query's in Batch .NET</span><span class="sxs-lookup"><span data-stu-id="7bae7-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="7bae7-167">Binnen Hallo [Batch .NET] [ api_net] API, Hallo [ODATADetailLevel] [ odata] klasse wordt gebruikt voor het verstrekken van filter, selecteren en uitvouwen tekenreeksen toolist bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-167">Within hello [Batch .NET][api_net] API, hello [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings toolist operations.</span></span> <span data-ttu-id="7bae7-168">Hallo ODataDetailLevel klasse heeft drie openbare string-eigenschappen die kunnen worden opgegeven in de constructor Hallo of rechtstreeks op Hallo object ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7bae7-168">hello ODataDetailLevel class has three public string properties that can be specified in hello constructor, or set directly on hello object.</span></span> <span data-ttu-id="7bae7-169">U geeft Hallo ODataDetailLevel object als een parameter toohello verschillende bewerkingen na opvragen, zoals [ListPools][net_list_pools], [ListJobs][net_list_jobs], en [ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="7bae7-169">You then pass hello ODataDetailLevel object as a parameter toohello various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="7bae7-170">[ODATADetailLevel][odata].[ FilterClause][odata_filter]: Hallo aantal items dat wordt geretourneerd beperken.</span><span class="sxs-lookup"><span data-stu-id="7bae7-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit hello number of items that are returned.</span></span>
* <span data-ttu-id="7bae7-171">[ODATADetailLevel][odata].[ SelectClause][odata_select]: Geef op welke eigenschapswaarden worden geretourneerd bij elk item.</span><span class="sxs-lookup"><span data-stu-id="7bae7-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="7bae7-172">[ODATADetailLevel][odata].[ ExpandClause][odata_expand]: gegevens ophalen voor alle artikelen in één API-aanroep in plaats van afzonderlijke aanroepen voor elk item.</span><span class="sxs-lookup"><span data-stu-id="7bae7-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="7bae7-173">Hallo volgende codefragment Hallo Batch .NET API tooefficiently query Hallo Batch-service gebruikt voor Hallo statistieken van een specifieke set met groepen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-173">hello following code snippet uses hello Batch .NET API tooefficiently query hello Batch service for hello statistics of a specific set of pools.</span></span> <span data-ttu-id="7bae7-174">In dit scenario heeft Hallo Batch gebruiker test- en productie-groepen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-174">In this scenario, hello Batch user has both test and production pools.</span></span> <span data-ttu-id="7bae7-175">Hallo test groep id's worden voorafgegaan door 'test' en Hallo productie groep id's worden voorafgegaan door 'prod'.</span><span class="sxs-lookup"><span data-stu-id="7bae7-175">hello test pool IDs are prefixed with "test", and hello production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="7bae7-176">In het Hallo-fragment *myBatchClient* is een goed geïnitialiseerd exemplaar van Hallo [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) klasse.</span><span class="sxs-lookup"><span data-stu-id="7bae7-176">In hello snippet, *myBatchClient* is a properly initialized instance of hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="7bae7-177">Een exemplaar van [ODATADetailLevel] [ odata] die is geconfigureerd met selecteren en uitvouwen componenten kunnen ook worden doorgegeven tooappropriate Get-methoden, zoals [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , toolimit Hallo hoeveelheid gegevens die wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7bae7-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed tooappropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), toolimit hello amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a><span data-ttu-id="7bae7-178">Batch REST-API voor too.NET toewijzingen</span><span class="sxs-lookup"><span data-stu-id="7bae7-178">Batch REST too.NET API mappings</span></span>
<span data-ttu-id="7bae7-179">Namen van eigenschappen in het filter, selecteert en breidt tekenreeksen *moet* overeenstemming met de REST-API collega's, zowel in de naam en het geval is.</span><span class="sxs-lookup"><span data-stu-id="7bae7-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="7bae7-180">Hallo onderstaande tabellen bevatten toewijzingen tussen Hallo .NET en REST-API collega's.</span><span class="sxs-lookup"><span data-stu-id="7bae7-180">hello tables below provide mappings between hello .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="7bae7-181">Toewijzingen voor tekenreeksen</span><span class="sxs-lookup"><span data-stu-id="7bae7-181">Mappings for filter strings</span></span>
* <span data-ttu-id="7bae7-182">**.NET-lijst methoden**: Hallo .NET API methoden in deze kolom accepteert een [ODATADetailLevel] [ odata] -object als parameter.</span><span class="sxs-lookup"><span data-stu-id="7bae7-182">**.NET list methods**: Each of hello .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="7bae7-183">**Aanvragen voor REST-lijst**: elke REST-API pagina gekoppelde tooin in deze kolom bevat een tabel waarin Hallo eigenschappen en bewerkingen die zijn toegestaan in *filter* tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-183">**REST list requests**: Each REST API page linked tooin this column contains a table that specifies hello properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="7bae7-184">U gebruikt deze eigenschapnamen en bewerkingen wanneer u samenstellen een [ODATADetailLevel.FilterClause] [ odata_filter] tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="7bae7-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="7bae7-185">Methoden voor .NET-lijst</span><span class="sxs-lookup"><span data-stu-id="7bae7-185">.NET list methods</span></span> | <span data-ttu-id="7bae7-186">Aanvragen voor REST-lijst</span><span class="sxs-lookup"><span data-stu-id="7bae7-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="7bae7-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="7bae7-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="7bae7-188">[Hallo certificaten weergeven in een account][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="7bae7-188">[List hello certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="7bae7-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="7bae7-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="7bae7-190">[Hallo-bestanden weergeven die zijn gekoppeld aan een taak][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="7bae7-190">[List hello files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="7bae7-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="7bae7-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="7bae7-192">[Status van de lijst Hallo van Hallo taakvoorbereidings- en jobvrijgevingstaken voor een taak][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="7bae7-192">[List hello status of hello job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="7bae7-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="7bae7-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="7bae7-194">[Hallo-taken weergeven in een account][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="7bae7-194">[List hello jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="7bae7-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="7bae7-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="7bae7-196">[Lijst Hallo bestanden op een knooppunt][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="7bae7-196">[List hello files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="7bae7-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="7bae7-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="7bae7-198">[Hallo taken die zijn gekoppeld aan een taak][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="7bae7-198">[List hello tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="7bae7-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="7bae7-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="7bae7-200">[Lijst Hallo taakschema's in een account][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="7bae7-200">[List hello job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="7bae7-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="7bae7-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="7bae7-202">[Hallo-taken weergeven die zijn gekoppeld aan een jobplanning][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="7bae7-202">[List hello jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="7bae7-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="7bae7-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="7bae7-204">[Lijst Hallo rekenknooppunten in een groep][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="7bae7-204">[List hello compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="7bae7-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="7bae7-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="7bae7-206">[Lijst Hallo opslaggroepen in een account][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="7bae7-206">[List hello pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="7bae7-207">Toewijzingen voor Selecteer tekenreeksen</span><span class="sxs-lookup"><span data-stu-id="7bae7-207">Mappings for select strings</span></span>
* <span data-ttu-id="7bae7-208">**Batch .NET-typen**: typen Batch .NET API.</span><span class="sxs-lookup"><span data-stu-id="7bae7-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="7bae7-209">**REST-API-entiteiten**: elke pagina in deze kolom bevat een of meer tabellen die Hallo REST-API-Eigenschapsnamen voor Hallo type lijst.</span><span class="sxs-lookup"><span data-stu-id="7bae7-209">**REST API entities**: Each page in this column contains one or more tables that list hello REST API property names for hello type.</span></span> <span data-ttu-id="7bae7-210">De namen van deze eigenschappen worden gebruikt wanneer u samenstellen *Selecteer* tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="7bae7-211">U gebruikt deze dezelfde eigenschapnamen als u een [ODATADetailLevel.SelectClause] [ odata_select] tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="7bae7-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="7bae7-212">Batch .NET-typen</span><span class="sxs-lookup"><span data-stu-id="7bae7-212">Batch .NET types</span></span> | <span data-ttu-id="7bae7-213">REST-API-entiteiten</span><span class="sxs-lookup"><span data-stu-id="7bae7-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="7bae7-214">[Certificaat][net_cert]</span><span class="sxs-lookup"><span data-stu-id="7bae7-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="7bae7-215">[Informatie ophalen over een certificaat][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="7bae7-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="7bae7-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="7bae7-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="7bae7-217">[Informatie over een taak ophalen][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="7bae7-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="7bae7-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="7bae7-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="7bae7-219">[Informatie over het schema van een taak ophalen][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="7bae7-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="7bae7-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="7bae7-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="7bae7-221">[Informatie ophalen over een knooppunt][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="7bae7-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="7bae7-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="7bae7-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="7bae7-223">[Informatie ophalen over een groep][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="7bae7-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="7bae7-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="7bae7-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="7bae7-225">[Informatie over een taak ophalen][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="7bae7-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="7bae7-226">Voorbeeld: een filtertekenreeks maken</span><span class="sxs-lookup"><span data-stu-id="7bae7-226">Example: construct a filter string</span></span>
<span data-ttu-id="7bae7-227">Wanneer u een filtertekenreeks voor samenstellen [ODATADetailLevel.FilterClause][odata_filter], raadpleegt u bovenstaande Hallo tabel onder '-toewijzingen voor filtertekenreeksen' toofind Hallo REST-API-documentatiepagina die overeenkomt met toohello lijstbewerking gewenste tooperform.</span><span class="sxs-lookup"><span data-stu-id="7bae7-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult hello table above under "Mappings for filter strings" toofind hello REST API documentation page that corresponds toohello list operation that you wish tooperform.</span></span> <span data-ttu-id="7bae7-228">Vindt u Hallo Filterbaar eigenschappen en hun ondersteunde operators in Hallo eerste multirow tabel op die pagina.</span><span class="sxs-lookup"><span data-stu-id="7bae7-228">You will find hello filterable properties and their supported operators in hello first multirow table on that page.</span></span> <span data-ttu-id="7bae7-229">Als u wenst dat tooretrieve alle taken waarvan afsluitcode niet nul was, bijvoorbeeld dit rij op [Hallo taken die zijn gekoppeld aan een taak] [ rest_list_tasks] Hallo toepasselijke eigenschap tekenreeks en de toegestane operators:</span><span class="sxs-lookup"><span data-stu-id="7bae7-229">If you wish tooretrieve all tasks whose exit code was nonzero, for example, this row on [List hello tasks associated with a job][rest_list_tasks] specifies hello applicable property string and allowable operators:</span></span>

| <span data-ttu-id="7bae7-230">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="7bae7-230">Property</span></span> | <span data-ttu-id="7bae7-231">Bewerkingen die zijn toegestaan</span><span class="sxs-lookup"><span data-stu-id="7bae7-231">Operations allowed</span></span> | <span data-ttu-id="7bae7-232">Type</span><span class="sxs-lookup"><span data-stu-id="7bae7-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="7bae7-233">Hallo filtertekenreeks voor het weergeven van alle taken met een andere afsluitcode dan zou dus zijn:</span><span class="sxs-lookup"><span data-stu-id="7bae7-233">Thus, hello filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="7bae7-234">Voorbeeld: een select tekenreeks maken</span><span class="sxs-lookup"><span data-stu-id="7bae7-234">Example: construct a select string</span></span>
<span data-ttu-id="7bae7-235">tooconstruct [ODATADetailLevel.SelectClause][odata_select], raadpleegt u bovenstaande Hallo tabel onder '-toewijzingen voor Selecteer tekenreeksen' en navigeer toohello REST-API-pagina die overeenkomt met het type entiteit toohello die u hebt biedt.</span><span class="sxs-lookup"><span data-stu-id="7bae7-235">tooconstruct [ODATADetailLevel.SelectClause][odata_select], consult hello table above under "Mappings for select strings" and navigate toohello REST API page that corresponds toohello type of entity that you are listing.</span></span> <span data-ttu-id="7bae7-236">Vindt u Hallo selecteerbare eigenschappen en hun ondersteunde operators in Hallo eerste multirow tabel op die pagina.</span><span class="sxs-lookup"><span data-stu-id="7bae7-236">You will find hello selectable properties and their supported operators in hello first multirow table on that page.</span></span> <span data-ttu-id="7bae7-237">Als u wenst dat tooretrieve alleen Hallo-ID en vanaf de opdrachtregel voor elke taak in een lijst, bijvoorbeeld vindt u deze rijen in de toepasselijke tabel Hallo op [informatie ophalen over een taak][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="7bae7-237">If you wish tooretrieve only hello ID and command line for each task in a list, for example, you will find these rows in hello applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="7bae7-238">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="7bae7-238">Property</span></span> | <span data-ttu-id="7bae7-239">Type</span><span class="sxs-lookup"><span data-stu-id="7bae7-239">Type</span></span> | <span data-ttu-id="7bae7-240">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="7bae7-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

<span data-ttu-id="7bae7-241">Hallo Selecteer string zou voor waaronder alleen Hallo-ID en -opdrachtregel met elke vermelde taak vervolgens zijn:</span><span class="sxs-lookup"><span data-stu-id="7bae7-241">hello select string for including only hello ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="7bae7-242">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="7bae7-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="7bae7-243">Voorbeeld van code voor efficiënte lijst met query 's</span><span class="sxs-lookup"><span data-stu-id="7bae7-243">Efficient list queries code sample</span></span>
<span data-ttu-id="7bae7-244">Bekijk Hallo [EfficientListQueries] [ efficient_query_sample] voorbeeldproject op GitHub toosee hoe efficiënt lijst uitvoeren van query's kan invloed hebben op prestaties in een toepassing.</span><span class="sxs-lookup"><span data-stu-id="7bae7-244">Check out hello [EfficientListQueries][efficient_query_sample] sample project on GitHub toosee how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="7bae7-245">Deze C#-consoletoepassing maakt en een groot aantal taken tooa taak toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7bae7-245">This C# console application creates and adds a large number of tasks tooa job.</span></span> <span data-ttu-id="7bae7-246">Klik op deze manier meerdere aanroepen toohello [JobOperations.ListTasks] [ net_list_tasks] methode en geeft [ODATADetailLevel] [ odata] objecten die zijn geconfigureerd met een andere eigenschap waarden toovary Hallo hoeveelheid gegevens toobe geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7bae7-246">Then, it makes multiple calls toohello [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values toovary hello amount of data toobe returned.</span></span> <span data-ttu-id="7bae7-247">Het volgende voor vergelijkbare toohello uitvoer genereert:</span><span class="sxs-lookup"><span data-stu-id="7bae7-247">It produces output similar toohello following:</span></span>

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

<span data-ttu-id="7bae7-248">Zoals u in Hallo verstreken keren, kunt u de reactietijden van de query aanzienlijk verlagen door te beperken Hallo eigenschappen en Hallo aantal items dat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7bae7-248">As shown in hello elapsed times, you can greatly lower query response times by limiting hello properties and hello number of items that are returned.</span></span> <span data-ttu-id="7bae7-249">U vindt deze en andere voorbeeldprojecten in Hallo [azure-batch-samples] [ github_samples] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="7bae7-249">You can find this and other sample projects in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="7bae7-250">BatchMetrics-bibliotheek en code-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="7bae7-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="7bae7-251">Bovendien toohello EfficientListQueries codevoorbeeld bovenstaande, kunt u vinden Hallo [BatchMetrics] [ batch_metrics] -project in Hallo [azure-batch-samples] [ github_samples] GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="7bae7-251">In addition toohello EfficientListQueries code sample above, you can find hello [BatchMetrics][batch_metrics] project in hello [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="7bae7-252">Hallo BatchMetrics voorbeeldproject laat zien hoe de Azure Batch-taak uitgevoerd met Hallo Batch-API voor het bewaken van tooefficiently.</span><span class="sxs-lookup"><span data-stu-id="7bae7-252">hello BatchMetrics sample project demonstrates how tooefficiently monitor Azure Batch job progress using hello Batch API.</span></span>

<span data-ttu-id="7bae7-253">Hallo [BatchMetrics] [ batch_metrics] voorbeeld bevat een bibliotheekproject voor .NET-klasse die u in uw eigen projecten en een eenvoudig opdrachtregelprogramma opnemen kunt tooexercise programma en gebruik Hallo Hallo demonstreren bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7bae7-253">hello [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program tooexercise and demonstrate hello use of hello library.</span></span>

<span data-ttu-id="7bae7-254">Hallo-voorbeeldtoepassing in Hallo project toont Hallo volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="7bae7-254">hello sample application within hello project demonstrates hello following operations:</span></span>

1. <span data-ttu-id="7bae7-255">Specifieke kenmerken in de volgorde toodownload alleen Hallo eigenschappen selecteren die u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="7bae7-255">Selecting specific attributes in order toodownload only hello properties you need</span></span>
2. <span data-ttu-id="7bae7-256">Filteren op status overgang keer volgorde toodownload alleen wijzigingen sinds de laatste query waarvoor een Hallo</span><span class="sxs-lookup"><span data-stu-id="7bae7-256">Filtering on state transition times in order toodownload only changes since hello last query</span></span>

<span data-ttu-id="7bae7-257">Bijvoorbeeld, weergegeven Hallo methode na in Hallo BatchMetrics-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7bae7-257">For example, hello following method appears in hello BatchMetrics library.</span></span> <span data-ttu-id="7bae7-258">Deze retourneert een ODATADetailLevel waarmee wordt aangegeven dat alleen Hallo `id` en `state` eigenschappen moeten worden opgehaald voor Hallo entiteiten die zijn opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="7bae7-258">It returns an ODATADetailLevel that specifies that only hello `id` and `state` properties should be obtained for hello entities that are queried.</span></span> <span data-ttu-id="7bae7-259">Ook wordt hiermee aangegeven dat alleen entiteiten waarvan de status is gewijzigd sinds de opgegeven Hallo `DateTime` parameter moet worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7bae7-259">It also specifies that only entities whose state has changed since hello specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="7bae7-260">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7bae7-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="7bae7-261">Knooppunt parallelle taken</span><span class="sxs-lookup"><span data-stu-id="7bae7-261">Parallel node tasks</span></span>
<span data-ttu-id="7bae7-262">[Azure Batch compute Resourcegebruik met gelijktijdige knooppunt taken maximaliseren](batch-parallel-node-tasks.md) is een ander artikel betrekking tooBatch toepassingsprestaties.</span><span class="sxs-lookup"><span data-stu-id="7bae7-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related tooBatch application performance.</span></span> <span data-ttu-id="7bae7-263">Bepaalde typen werkbelastingen kunnen profiteren van parallelle taken worden uitgevoerd op grotere-- maar minder--rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="7bae7-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="7bae7-264">Bekijk Hallo [voorbeeldscenario](batch-parallel-node-tasks.md#example-scenario) in Hallo-artikel voor meer informatie over dit scenario.</span><span class="sxs-lookup"><span data-stu-id="7bae7-264">Check out hello [example scenario](batch-parallel-node-tasks.md#example-scenario) in hello article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="7bae7-265">Batch-Forum</span><span class="sxs-lookup"><span data-stu-id="7bae7-265">Batch Forum</span></span>
<span data-ttu-id="7bae7-266">Hallo [Azure Batch-Forum] [ forum] is uitermate toodiscuss Batch plaats en vragen over Hallo-service op MSDN.</span><span class="sxs-lookup"><span data-stu-id="7bae7-266">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="7bae7-267">Kop op via voor nuttige 'een tijdelijke' berichten, en stel uw vragen wanneer deze zich voordoen tijdens het bouwen van uw Batch-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="7bae7-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job