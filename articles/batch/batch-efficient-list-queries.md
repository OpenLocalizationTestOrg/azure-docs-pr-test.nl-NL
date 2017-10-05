---
title: "Lijst met efficiënt query's, Azure Batch ontwerpen | Microsoft Docs"
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
ms.openlocfilehash: a80b207f591bd888d4749287527013c5e554fb6e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-queries-to-list-batch-resources-efficiently"></a><span data-ttu-id="70838-103">Query's op de lijst met Batch-resources efficiënt maken</span><span class="sxs-lookup"><span data-stu-id="70838-103">Create queries to list Batch resources efficiently</span></span>

<span data-ttu-id="70838-104">Hier leert u hoe u de prestaties van uw Azure Batch-toepassingen door te verminderen de hoeveelheid gegevens die door de service worden geretourneerd wanneer u query jobs, taken en met rekenknooppunten verhoogt de [Batch .NET] [ api_net] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="70838-104">Here you'll learn how to increase your Azure Batch application's performance by reducing the amount of data that is returned by the service when you query jobs, tasks, and compute nodes with the [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="70838-105">Bijna alle Batch-toepassingen hoeft uit te voeren van een type controle of een andere bewerking vaak query van de Batch-service met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="70838-105">Nearly all Batch applications need to perform some type of monitoring or other operation that queries the Batch service, often at regular intervals.</span></span> <span data-ttu-id="70838-106">Om te bepalen of er in een taak resterende taken in de wachtrij zijn, kunt u gegevens moet ophalen voor elke taak in de taak.</span><span class="sxs-lookup"><span data-stu-id="70838-106">For example, to determine whether there are any queued tasks remaining in a job, you must get data on every task in the job.</span></span> <span data-ttu-id="70838-107">Om te bepalen van de status van knooppunten in uw pool, moet u gegevens ophalen op elk knooppunt in de groep.</span><span class="sxs-lookup"><span data-stu-id="70838-107">To determine the status of nodes in your pool, you must get data on every node in the pool.</span></span> <span data-ttu-id="70838-108">In dit artikel wordt uitgelegd hoe u dergelijke query's uitvoeren in de meest efficiënte manier.</span><span class="sxs-lookup"><span data-stu-id="70838-108">This article explains how to execute such queries in the most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="70838-109">De Batch-service biedt speciale API-ondersteuning voor de gangbare scenario van taken in een taak worden geteld.</span><span class="sxs-lookup"><span data-stu-id="70838-109">The Batch service provides special API support for the common scenario of counting tasks in a job.</span></span> <span data-ttu-id="70838-110">In plaats van een lijst met query om deze, roept u de [ophalen taak telt] [ rest_get_task_counts] bewerking.</span><span class="sxs-lookup"><span data-stu-id="70838-110">Instead of using a list query for these, you can call the [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="70838-111">Aantallen voor GET-taak geeft aan hoeveel taken in behandeling is, zijn uitgevoerd of voltooid en hoeveel taken hebt voltooid of mislukt.</span><span class="sxs-lookup"><span data-stu-id="70838-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="70838-112">Get-taak telt is efficiënter dan een lijst met query.</span><span class="sxs-lookup"><span data-stu-id="70838-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="70838-113">Zie voor meer informatie [aantal taken voor een taak op status (Preview)](batch-get-task-counts.md).</span><span class="sxs-lookup"><span data-stu-id="70838-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="70838-114">De bewerking taak telt ophalen is niet beschikbaar in Batch-versies eerder dan 2017-06-01.5.1.</span><span class="sxs-lookup"><span data-stu-id="70838-114">The Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="70838-115">Als u van een oudere versie van de service gebruikmaakt, gebruikt u een lijst met query voor het tellen van taken in een job in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="70838-115">If you are using an older version of the service, then use a list query to count tasks in a job instead.</span></span>
>
> 

## <a name="meet-the-detaillevel"></a><span data-ttu-id="70838-116">Voldoen aan de DetailLevel</span><span class="sxs-lookup"><span data-stu-id="70838-116">Meet the DetailLevel</span></span>
<span data-ttu-id="70838-117">In een productie-Batch-toepassing kunnen entiteiten, zoals jobs, taken en rekenknooppunten in duizendtallen nummeren.</span><span class="sxs-lookup"><span data-stu-id="70838-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in the thousands.</span></span> <span data-ttu-id="70838-118">Wanneer u informatie over deze bronnen aanvraagt, moet een grote hoeveelheid gegevens 'kruislingse de kabel' van de Batch-service voor uw toepassing op elke query.</span><span class="sxs-lookup"><span data-stu-id="70838-118">When you request information on these resources, a potentially large amount of data must "cross the wire" from the Batch service to your application on each query.</span></span> <span data-ttu-id="70838-119">Door te beperken het aantal items en type informatie dat wordt geretourneerd door een query, verhoogt u de snelheid van uw query's en daarom op de prestaties van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="70838-119">By limiting the number of items and type of information that is returned by a query, you can increase the speed of your queries, and therefore the performance of your application.</span></span>

<span data-ttu-id="70838-120">Dit [Batch .NET] [ api_net] API code codefragment lijsten *elke* taak die is gekoppeld aan een taak, samen met *alle* van de eigenschappen van elke taak:</span><span class="sxs-lookup"><span data-stu-id="70838-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of the properties of each task:</span></span>

```csharp
// Get a collection of all of the tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="70838-121">U kunt echter een veel efficiënter lijstquery uitvoeren door het toepassen van een 'detailniveau' aan de query.</span><span class="sxs-lookup"><span data-stu-id="70838-121">You can perform a much more efficient list query, however, by applying a "detail level" to your query.</span></span> <span data-ttu-id="70838-122">Dit doet u door het leveren van een [ODATADetailLevel] [ odata] object toe aan de [JobOperations.ListTasks] [ net_list_tasks] methode.</span><span class="sxs-lookup"><span data-stu-id="70838-122">You do this by supplying an [ODATADetailLevel][odata] object to the [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="70838-123">In dit fragment retourneert alleen de ID, de opdrachtregel en de compute knooppunt informatie eigenschappen van voltooide taken:</span><span class="sxs-lookup"><span data-stu-id="70838-123">This snippet returns only the ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties to return
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply the ODATADetailLevel to the ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="70838-124">In dit voorbeeldscenario als er duizenden taken in de taak, de resultaten van de tweede query wordt doorgaans geretourneerd veel sneller dan de eerste.</span><span class="sxs-lookup"><span data-stu-id="70838-124">In this example scenario, if there are thousands of tasks in the job, the results from the second query will typically be returned much quicker than the first.</span></span> <span data-ttu-id="70838-125">Meer informatie over het gebruik van ODATADetailLevel wanneer u objecten met de Batch .NET API is opgenomen [hieronder](#efficient-querying-in-batch-net).</span><span class="sxs-lookup"><span data-stu-id="70838-125">More information about using ODATADetailLevel when you list items with the Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70838-126">Ten zeerste aangeraden dat u *altijd* opgeven van een object ODATADetailLevel op uw lijst .NET API aanroepen van maximale efficiëntie en prestaties van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="70838-126">We highly recommend that you *always* supply an ODATADetailLevel object to your .NET API list calls to ensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="70838-127">Door te geven een detailniveau, kunt u helpen te verlagen reactietijden van de Batch-service, netwerkgebruik verbeteren en geheugengebruik minimaliseren door clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="70838-127">By specifying a detail level, you can help to lower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="70838-128">Filteren, selecteert en vouw</span><span class="sxs-lookup"><span data-stu-id="70838-128">Filter, select, and expand</span></span>
<span data-ttu-id="70838-129">De [Batch .NET] [ api_net] en [Batch REST] [ api_rest] API's bieden de mogelijkheid om te beperken van zowel het aantal items dat wordt geretourneerd in een lijst, evenals de hoeveelheid gegevens die voor elke wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="70838-129">The [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide the ability to reduce both the number of items that are returned in a list, as well as the amount of information that is returned for each.</span></span> <span data-ttu-id="70838-130">U dit doen door op te geven **filter**, **Selecteer**, en **Vouw tekenreeksen** bij het uitvoeren van de lijst met query's.</span><span class="sxs-lookup"><span data-stu-id="70838-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="70838-131">Filteren</span><span class="sxs-lookup"><span data-stu-id="70838-131">Filter</span></span>
<span data-ttu-id="70838-132">De filtertekenreeks is een expressie die vermindert het aantal items dat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="70838-132">The filter string is an expression that reduces the number of items that are returned.</span></span> <span data-ttu-id="70838-133">Bijvoorbeeld, lijst met actieve taken voor een taak of lijst alleen rekenknooppunten die gereed zijn om de taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="70838-133">For example, list only the running tasks for a job, or list only compute nodes that are ready to run tasks.</span></span>

* <span data-ttu-id="70838-134">De filtertekenreeks bestaat uit een of meer expressies met een expressie die uit een eigenschapsnaam, een operator en een waarde bestaat.</span><span class="sxs-lookup"><span data-stu-id="70838-134">The filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="70838-135">De eigenschappen die kunnen worden opgegeven zijn specifiek voor elk entiteitstype waarmee u een query uitvoeren, zoals de operators die worden ondersteund voor elke eigenschap zijn.</span><span class="sxs-lookup"><span data-stu-id="70838-135">The properties that can be specified are specific to each entity type that you query, as are the operators that are supported for each property.</span></span>
* <span data-ttu-id="70838-136">Meerdere expressies kunnen worden gecombineerd met behulp van de logische operators `and` en `or`.</span><span class="sxs-lookup"><span data-stu-id="70838-136">Multiple expressions can be combined by using the logical operators `and` and `or`.</span></span>
* <span data-ttu-id="70838-137">In dit voorbeeld filteren tekenreekslijsten alleen de wordt uitgevoerd 'weergeven' taken: `(state eq 'running') and startswith(id, 'renderTask')`.</span><span class="sxs-lookup"><span data-stu-id="70838-137">This example filter string lists only the running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="70838-138">Selecteer</span><span class="sxs-lookup"><span data-stu-id="70838-138">Select</span></span>
<span data-ttu-id="70838-139">De select-tekenreeks beperkt de waarden van de eigenschappen die worden geretourneerd voor elk item.</span><span class="sxs-lookup"><span data-stu-id="70838-139">The select string limits the property values that are returned for each item.</span></span> <span data-ttu-id="70838-140">U geeft een lijst met namen van eigenschappen en alleen de eigenschapswaarden van deze voor de items in de queryresultaten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="70838-140">You specify a list of property names, and only those property values are returned for the items in the query results.</span></span>

* <span data-ttu-id="70838-141">De select-tekenreeks bestaat uit een door komma's gescheiden lijst met namen van eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="70838-141">The select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="70838-142">U kunt opgeven dat geen van de eigenschappen voor het entiteitstype die u wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="70838-142">You can specify any of the properties for the entity type you are querying.</span></span>
* <span data-ttu-id="70838-143">In dit voorbeeld selecteert tekenreeks dat slechts drie eigenschapswaarden voor elke taak moeten worden geretourneerd: `id, state, stateTransitionTime`.</span><span class="sxs-lookup"><span data-stu-id="70838-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="70838-144">Uitvouwen</span><span class="sxs-lookup"><span data-stu-id="70838-144">Expand</span></span>
<span data-ttu-id="70838-145">De tekenreeks uit te breiden vermindert het aantal API-aanroepen die nodig zijn om bepaalde informatie te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="70838-145">The expand string reduces the number of API calls that are required to obtain certain information.</span></span> <span data-ttu-id="70838-146">Wanneer u een tekenreeks uit te breiden, meer informatie over elk item kan worden verkregen met één API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="70838-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="70838-147">In plaats van de eerste verkrijgen van de lijst met entiteiten, die vervolgens vraagt informatie voor elk item in de lijst met een tekenreeks uit te breiden kunt u dezelfde gegevens in één API-aanroep verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="70838-147">Rather than first obtaining the list of entities, then requesting information for each item in the list, you use an expand string to obtain the same information in a single API call.</span></span> <span data-ttu-id="70838-148">Minder API-aanroepen betekent betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="70838-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="70838-149">Net als bij de optie tekenreeks, de expand-reeks bepaalt of bepaalde gegevens worden opgenomen in de lijst met queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="70838-149">Similar to the select string, the expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="70838-150">De tekenreeks uit te breiden wordt alleen ondersteund wanneer het wordt gebruikt in de lijst taken, taakschema's, taken en groepen.</span><span class="sxs-lookup"><span data-stu-id="70838-150">The expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="70838-151">Op dit moment wordt alleen ondersteund statistische gegevens.</span><span class="sxs-lookup"><span data-stu-id="70838-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="70838-152">Wanneer alle eigenschappen vereist zijn en er is geen tekenreeks select is opgegeven, de tekenreeks uit te breiden *moet* worden gebruikt voor statistische gegevens ophalen.</span><span class="sxs-lookup"><span data-stu-id="70838-152">When all properties are required and no select string is specified, the expand string *must* be used to get statistics information.</span></span> <span data-ttu-id="70838-153">Als een select-tekenreeks is gebruikt voor het verkrijgen van een subset van eigenschappen, klikt u vervolgens `stats` kunnen worden opgegeven in de select-tekenreeks en de tekenreeks uit te breiden niet hoeft te worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="70838-153">If a select string is used to obtain a subset of properties, then `stats` can be specified in the select string, and the expand string does not need to be specified.</span></span>
* <span data-ttu-id="70838-154">In dit voorbeeld Vouw tekenreeks geeft aan dat statistische gegevens voor elk item in de lijst moet worden geretourneerd: `stats`.</span><span class="sxs-lookup"><span data-stu-id="70838-154">This example expand string specifies that statistics information should be returned for each item in the list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="70838-155">Bij het maken van een van de drie querytypen tekenreeks (filteren, selecteert en vouw), moet u ervoor zorgen dat de namen van eigenschappen en de aanvraag overeenkomen met die van hun collega's REST-API-element.</span><span class="sxs-lookup"><span data-stu-id="70838-155">When constructing any of the three query string types (filter, select, and expand), you must ensure that the property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="70838-156">Bijvoorbeeld, als u werkt met de .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) klasse, moet u **status** in plaats van **status**, zelfs als de eigenschap .NET [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span><span class="sxs-lookup"><span data-stu-id="70838-156">For example, when working with the .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though the .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="70838-157">Zie de tabellen hieronder voor de eigenschaptoewijzingen tussen .NET en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="70838-157">See the tables below for property mappings between the .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="70838-158">Regels voor filteren, selecteert en breidt tekenreeksen</span><span class="sxs-lookup"><span data-stu-id="70838-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="70838-159">Namen van eigenschappen in het filter, selecteert en breidt tekenreeksen moeten worden weergegeven als in de [Batch REST] [ api_rest] API--zelfs wanneer u [Batch .NET] [ api_net] of een van de andere Batch-SDK's.</span><span class="sxs-lookup"><span data-stu-id="70838-159">Properties names in filter, select, and expand strings should appear as they do in the [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of the other Batch SDKs.</span></span>
* <span data-ttu-id="70838-160">Alle namen van eigenschappen zijn hoofdlettergevoelig, maar eigenschapswaarden zijn niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="70838-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="70838-161">Datum/tijd tekenreeksen kunnen twee verschillende indelingen, en moet worden voorafgegaan door `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="70838-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="70838-162">Voorbeeld van W3C-DTF-indeling:`creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="70838-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="70838-163">Voorbeeld van RFC 1123 indeling:`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="70838-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="70838-164">Booleaanse tekenreeksen zijn `true` of `false`.</span><span class="sxs-lookup"><span data-stu-id="70838-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="70838-165">Als een eigenschap is ongeldig of de operator is opgegeven, een `400 (Bad Request)` fout resulteert.</span><span class="sxs-lookup"><span data-stu-id="70838-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="70838-166">Efficiënter uitvoeren van query's in Batch .NET</span><span class="sxs-lookup"><span data-stu-id="70838-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="70838-167">Binnen de [Batch .NET] [ api_net] API, de [ODATADetailLevel] [ odata] klasse wordt gebruikt voor het verstrekken van filter, en selecteer tekenreeksen worden uitgebreid tot bewerkingen na opvragen.</span><span class="sxs-lookup"><span data-stu-id="70838-167">Within the [Batch .NET][api_net] API, the [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings to list operations.</span></span> <span data-ttu-id="70838-168">De klasse ODataDetailLevel heeft drie openbare eigenschappen die kunnen worden opgegeven in de constructor of rechtstreeks op het object is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="70838-168">The ODataDetailLevel class has three public string properties that can be specified in the constructor, or set directly on the object.</span></span> <span data-ttu-id="70838-169">U geeft het ODataDetailLevel-object als parameter voor de verschillende bewerkingen na opvragen, zoals [ListPools][net_list_pools], [ListJobs][net_list_jobs], en [ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="70838-169">You then pass the ODataDetailLevel object as a parameter to the various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="70838-170">[ODATADetailLevel][odata].[ FilterClause][odata_filter]: Beperk het aantal items dat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="70838-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit the number of items that are returned.</span></span>
* <span data-ttu-id="70838-171">[ODATADetailLevel][odata].[ SelectClause][odata_select]: Geef op welke eigenschapswaarden worden geretourneerd bij elk item.</span><span class="sxs-lookup"><span data-stu-id="70838-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="70838-172">[ODATADetailLevel][odata].[ ExpandClause][odata_expand]: gegevens ophalen voor alle artikelen in één API-aanroep in plaats van afzonderlijke aanroepen voor elk item.</span><span class="sxs-lookup"><span data-stu-id="70838-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="70838-173">Het volgende codefragment gebruikt de Batch .NET API om efficiënt query de Batch-service voor de statistieken van een specifieke set met groepen.</span><span class="sxs-lookup"><span data-stu-id="70838-173">The following code snippet uses the Batch .NET API to efficiently query the Batch service for the statistics of a specific set of pools.</span></span> <span data-ttu-id="70838-174">In dit scenario heeft de gebruiker Batch pools test- en productie.</span><span class="sxs-lookup"><span data-stu-id="70838-174">In this scenario, the Batch user has both test and production pools.</span></span> <span data-ttu-id="70838-175">De id's van de test-toepassingen worden voorafgegaan door 'test' en de productiepool-id's worden voorafgegaan door 'prod'.</span><span class="sxs-lookup"><span data-stu-id="70838-175">The test pool IDs are prefixed with "test", and the production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="70838-176">In het codefragment *myBatchClient* is een goed geïnitialiseerd exemplaar van de [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) klasse.</span><span class="sxs-lookup"><span data-stu-id="70838-176">In the snippet, *myBatchClient* is a properly initialized instance of the [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which to set the filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want to pull only the "test" pools, so we limit the number of items returned
// by using a FilterClause and specifying that the pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// To further limit the data that crosses the wire, configure the SelectClause to
// limit the properties that are returned on each CloudPool object to only
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify the ExpandClause so that the .NET API pulls the statistics for the
// CloudPools in a single underlying REST API call. Note that we use the pool's
// REST API element name "stats" here as opposed to "Statistics" as it appears in
// the .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing the amount of data that is returned
// by specifying the detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="70838-177">Een exemplaar van [ODATADetailLevel] [ odata] die is geconfigureerd met selecteren en uitvouwen componenten kunnen ook worden doorgegeven aan de juiste Get-methoden, zoals [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), te beperken van de hoeveelheid gegevens die wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="70838-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed to appropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), to limit the amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-to-net-api-mappings"></a><span data-ttu-id="70838-178">Batch REST in .NET API toewijzingen</span><span class="sxs-lookup"><span data-stu-id="70838-178">Batch REST to .NET API mappings</span></span>
<span data-ttu-id="70838-179">Namen van eigenschappen in het filter, selecteert en breidt tekenreeksen *moet* overeenstemming met de REST-API collega's, zowel in de naam en het geval is.</span><span class="sxs-lookup"><span data-stu-id="70838-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="70838-180">De onderstaande tabellen bevatten toewijzingen tussen de collega .NET en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="70838-180">The tables below provide mappings between the .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="70838-181">Toewijzingen voor tekenreeksen</span><span class="sxs-lookup"><span data-stu-id="70838-181">Mappings for filter strings</span></span>
* <span data-ttu-id="70838-182">**.NET-lijst methoden**: elk van de .NET API-methoden in deze kolom accepteert een [ODATADetailLevel] [ odata] -object als parameter.</span><span class="sxs-lookup"><span data-stu-id="70838-182">**.NET list methods**: Each of the .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="70838-183">**Aanvragen voor REST-lijst**: elke REST-API-pagina is gekoppeld aan in deze kolom bevat een tabel waarin de eigenschappen en bewerkingen die zijn toegestaan in *filter* tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="70838-183">**REST list requests**: Each REST API page linked to in this column contains a table that specifies the properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="70838-184">U gebruikt deze eigenschapnamen en bewerkingen wanneer u samenstellen een [ODATADetailLevel.FilterClause] [ odata_filter] tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="70838-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="70838-185">Methoden voor .NET-lijst</span><span class="sxs-lookup"><span data-stu-id="70838-185">.NET list methods</span></span> | <span data-ttu-id="70838-186">Aanvragen voor REST-lijst</span><span class="sxs-lookup"><span data-stu-id="70838-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="70838-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="70838-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="70838-188">[Lijst van de certificaten in een account][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="70838-188">[List the certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="70838-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="70838-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="70838-190">[De bestanden die zijn gekoppeld aan een taak weergeven][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="70838-190">[List the files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="70838-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="70838-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="70838-192">[De status van de taakvoorbereidingstaak en jobvrijgevingstaken voor een taak weergeven][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="70838-192">[List the status of the job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="70838-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="70838-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="70838-194">[Lijst van de taken in een account][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="70838-194">[List the jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="70838-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="70838-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="70838-196">[Lijst van de bestanden op een knooppunt][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="70838-196">[List the files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="70838-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="70838-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="70838-198">[Lijst van de taken die zijn gekoppeld aan een taak][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="70838-198">[List the tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="70838-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="70838-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="70838-200">[Lijst van de taakschema's in een account][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="70838-200">[List the job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="70838-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="70838-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="70838-202">[Lijst van de taken die zijn gekoppeld aan een jobplanning][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="70838-202">[List the jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="70838-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="70838-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="70838-204">[Lijst van de rekenknooppunten in een groep][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="70838-204">[List the compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="70838-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="70838-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="70838-206">[De toepassingen in een account weergeven][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="70838-206">[List the pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="70838-207">Toewijzingen voor Selecteer tekenreeksen</span><span class="sxs-lookup"><span data-stu-id="70838-207">Mappings for select strings</span></span>
* <span data-ttu-id="70838-208">**Batch .NET-typen**: typen Batch .NET API.</span><span class="sxs-lookup"><span data-stu-id="70838-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="70838-209">**REST-API-entiteiten**: elke pagina in deze kolom bevat een of meer tabellen met de namen van de REST-API-eigenschappen voor het type.</span><span class="sxs-lookup"><span data-stu-id="70838-209">**REST API entities**: Each page in this column contains one or more tables that list the REST API property names for the type.</span></span> <span data-ttu-id="70838-210">De namen van deze eigenschappen worden gebruikt wanneer u samenstellen *Selecteer* tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="70838-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="70838-211">U gebruikt deze dezelfde eigenschapnamen als u een [ODATADetailLevel.SelectClause] [ odata_select] tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="70838-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="70838-212">Batch .NET-typen</span><span class="sxs-lookup"><span data-stu-id="70838-212">Batch .NET types</span></span> | <span data-ttu-id="70838-213">REST-API-entiteiten</span><span class="sxs-lookup"><span data-stu-id="70838-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="70838-214">[Certificaat][net_cert]</span><span class="sxs-lookup"><span data-stu-id="70838-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="70838-215">[Informatie ophalen over een certificaat][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="70838-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="70838-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="70838-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="70838-217">[Informatie over een taak ophalen][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="70838-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="70838-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="70838-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="70838-219">[Informatie over het schema van een taak ophalen][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="70838-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="70838-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="70838-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="70838-221">[Informatie ophalen over een knooppunt][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="70838-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="70838-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="70838-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="70838-223">[Informatie ophalen over een groep][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="70838-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="70838-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="70838-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="70838-225">[Informatie over een taak ophalen][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="70838-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="70838-226">Voorbeeld: een filtertekenreeks maken</span><span class="sxs-lookup"><span data-stu-id="70838-226">Example: construct a filter string</span></span>
<span data-ttu-id="70838-227">Wanneer u een filtertekenreeks voor samenstellen [ODATADetailLevel.FilterClause][odata_filter], raadpleegt u de bovenstaande tabel onder '-toewijzingen voor filtertekenreeksen' om te zoeken naar de REST-API-documentatiepagina die overeenkomt met de lijstbewerking die u wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="70838-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult the table above under "Mappings for filter strings" to find the REST API documentation page that corresponds to the list operation that you wish to perform.</span></span> <span data-ttu-id="70838-228">U vindt de Filterbaar eigenschappen en hun ondersteunde operators in de eerste multirow tabel op die pagina.</span><span class="sxs-lookup"><span data-stu-id="70838-228">You will find the filterable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="70838-229">Als u wilt ophalen van alle taken waarvan afsluitcode niet nul was, bijvoorbeeld dit rij op [lijst van de taken die zijn gekoppeld aan een taak] [ rest_list_tasks] stelt de toepasselijke eigenschap tekenreeks en de toegestane operators:</span><span class="sxs-lookup"><span data-stu-id="70838-229">If you wish to retrieve all tasks whose exit code was nonzero, for example, this row on [List the tasks associated with a job][rest_list_tasks] specifies the applicable property string and allowable operators:</span></span>

| <span data-ttu-id="70838-230">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="70838-230">Property</span></span> | <span data-ttu-id="70838-231">Bewerkingen die zijn toegestaan</span><span class="sxs-lookup"><span data-stu-id="70838-231">Operations allowed</span></span> | <span data-ttu-id="70838-232">Type</span><span class="sxs-lookup"><span data-stu-id="70838-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="70838-233">Daarom zou de filtertekenreeks voor het weergeven van alle taken met een andere waarde dan nul afsluitcode:</span><span class="sxs-lookup"><span data-stu-id="70838-233">Thus, the filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="70838-234">Voorbeeld: een select tekenreeks maken</span><span class="sxs-lookup"><span data-stu-id="70838-234">Example: construct a select string</span></span>
<span data-ttu-id="70838-235">Om samen te stellen [ODATADetailLevel.SelectClause][odata_select], raadpleegt u de bovenstaande tabel onder '-toewijzingen voor Selecteer tekenreeksen' en navigeer naar de pagina REST-API die overeenkomt met het type entiteit die u weergeeft.</span><span class="sxs-lookup"><span data-stu-id="70838-235">To construct [ODATADetailLevel.SelectClause][odata_select], consult the table above under "Mappings for select strings" and navigate to the REST API page that corresponds to the type of entity that you are listing.</span></span> <span data-ttu-id="70838-236">U vindt de selecteerbare eigenschappen en hun ondersteunde operators in de eerste multirow tabel op die pagina.</span><span class="sxs-lookup"><span data-stu-id="70838-236">You will find the selectable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="70838-237">Als u wilt dat alleen de ID en de opdrachtregel voor elke taak in een lijst ophalen, bijvoorbeeld, vindt u deze rijen in de tabel van toepassing op [informatie ophalen over een taak][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="70838-237">If you wish to retrieve only the ID and command line for each task in a list, for example, you will find these rows in the applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="70838-238">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="70838-238">Property</span></span> | <span data-ttu-id="70838-239">Type</span><span class="sxs-lookup"><span data-stu-id="70838-239">Type</span></span> | <span data-ttu-id="70838-240">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="70838-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`The ID of the task.` |
| `commandLine` |`String` |`The command line of the task.` |

<span data-ttu-id="70838-241">Selecteer de string voor het opnemen van alleen de ID en de opdrachtregel voor elke vermelde taak zou vervolgens zijn:</span><span class="sxs-lookup"><span data-stu-id="70838-241">The select string for including only the ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="70838-242">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="70838-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="70838-243">Voorbeeld van code voor efficiënte lijst met query 's</span><span class="sxs-lookup"><span data-stu-id="70838-243">Efficient list queries code sample</span></span>
<span data-ttu-id="70838-244">Bekijk de [EfficientListQueries] [ efficient_query_sample] voorbeeldproject op GitHub om te zien hoe efficiënt lijst uitvoeren van query's kan invloed hebben op prestaties in een toepassing.</span><span class="sxs-lookup"><span data-stu-id="70838-244">Check out the [EfficientListQueries][efficient_query_sample] sample project on GitHub to see how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="70838-245">Deze C#-consoletoepassing maakt en voegt u een groot aantal taken toe aan een job.</span><span class="sxs-lookup"><span data-stu-id="70838-245">This C# console application creates and adds a large number of tasks to a job.</span></span> <span data-ttu-id="70838-246">Klik op deze manier meerdere aanroepen naar de [JobOperations.ListTasks] [ net_list_tasks] methode en geeft [ODATADetailLevel] [ odata] objecten die zijn geconfigureerd met verschillende eigenschapwaarden variëren van de hoeveelheid gegevens moeten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="70838-246">Then, it makes multiple calls to the [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values to vary the amount of data to be returned.</span></span> <span data-ttu-id="70838-247">Het wordt ongeveer de volgende uitvoer gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="70838-247">It produces output similar to the following:</span></span>

```
Adding 5000 tasks to job jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER to query tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER to continue...
```

<span data-ttu-id="70838-248">Zoals u in de verstreken tijd, kunt u de reactietijden van de query aanzienlijk verlagen door het beperken van de eigenschappen en het aantal items dat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="70838-248">As shown in the elapsed times, you can greatly lower query response times by limiting the properties and the number of items that are returned.</span></span> <span data-ttu-id="70838-249">U vindt deze en andere voorbeeldprojecten in de [azure-batch-samples] [ github_samples] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="70838-249">You can find this and other sample projects in the [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="70838-250">BatchMetrics-bibliotheek en code-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="70838-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="70838-251">Naast het codevoorbeeld EfficientListQueries bovenstaande vindt u de [BatchMetrics] [ batch_metrics] project in de [azure-batch-samples] [ github_samples] GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="70838-251">In addition to the EfficientListQueries code sample above, you can find the [BatchMetrics][batch_metrics] project in the [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="70838-252">Het voorbeeldproject BatchMetrics laat zien hoe efficiënt voortgang Azure Batch-taak met de Batch-API.</span><span class="sxs-lookup"><span data-stu-id="70838-252">The BatchMetrics sample project demonstrates how to efficiently monitor Azure Batch job progress using the Batch API.</span></span>

<span data-ttu-id="70838-253">De [BatchMetrics] [ batch_metrics] voorbeeld bevat een bibliotheekproject voor .NET-klasse die u kunt opnemen in uw eigen projecten en een eenvoudig opdrachtregelprogramma uitoefenen en demonstreren van het gebruik van de bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="70838-253">The [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program to exercise and demonstrate the use of the library.</span></span>

<span data-ttu-id="70838-254">De voorbeeldtoepassing in het project ziet u de volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="70838-254">The sample application within the project demonstrates the following operations:</span></span>

1. <span data-ttu-id="70838-255">Specifieke kenmerken selecteren om te downloaden van alleen de eigenschappen die u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="70838-255">Selecting specific attributes in order to download only the properties you need</span></span>
2. <span data-ttu-id="70838-256">Filteren op status overgang keren om te kunnen downloaden van alleen wijzigingen sinds de laatste query</span><span class="sxs-lookup"><span data-stu-id="70838-256">Filtering on state transition times in order to download only changes since the last query</span></span>

<span data-ttu-id="70838-257">Bijvoorbeeld, verschijnt de volgende methode in de bibliotheek BatchMetrics.</span><span class="sxs-lookup"><span data-stu-id="70838-257">For example, the following method appears in the BatchMetrics library.</span></span> <span data-ttu-id="70838-258">Deze retourneert een ODATADetailLevel die geeft aan dat alleen de `id` en `state` eigenschappen moeten worden opgehaald voor de entiteiten die zijn opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="70838-258">It returns an ODATADetailLevel that specifies that only the `id` and `state` properties should be obtained for the entities that are queried.</span></span> <span data-ttu-id="70838-259">Ook wordt hiermee aangegeven dat alleen entiteiten waarvan de status is gewijzigd sinds de opgegeven `DateTime` parameter moet worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="70838-259">It also specifies that only entities whose state has changed since the specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="70838-260">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70838-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="70838-261">Knooppunt parallelle taken</span><span class="sxs-lookup"><span data-stu-id="70838-261">Parallel node tasks</span></span>
<span data-ttu-id="70838-262">[Azure Batch compute Resourcegebruik met gelijktijdige knooppunt taken maximaliseren](batch-parallel-node-tasks.md) een ander artikel betrekking heeft op de prestaties van de Batch-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="70838-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related to Batch application performance.</span></span> <span data-ttu-id="70838-263">Bepaalde typen werkbelastingen kunnen profiteren van parallelle taken worden uitgevoerd op grotere-- maar minder--rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="70838-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="70838-264">Bekijk de [voorbeeldscenario](batch-parallel-node-tasks.md#example-scenario) in het artikel voor meer informatie over dit scenario.</span><span class="sxs-lookup"><span data-stu-id="70838-264">Check out the [example scenario](batch-parallel-node-tasks.md#example-scenario) in the article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="70838-265">Batch-Forum</span><span class="sxs-lookup"><span data-stu-id="70838-265">Batch Forum</span></span>
<span data-ttu-id="70838-266">De [Azure Batch-Forum] [ forum] is een goede plaats om te bespreken Batch en vragen over de service op MSDN.</span><span class="sxs-lookup"><span data-stu-id="70838-266">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="70838-267">Kop op via voor nuttige 'een tijdelijke' berichten, en stel uw vragen wanneer deze zich voordoen tijdens het bouwen van uw Batch-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="70838-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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