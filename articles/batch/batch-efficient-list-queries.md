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
# <a name="create-queries-toolist-batch-resources-efficiently"></a>Query's efficiënt toolist Batch-resources maken

Hier leert u hoe tooincrease de prestaties van de Azure Batch-toepassing doordat Hallo hoeveelheid gegevens die door Hallo-service worden geretourneerd wanneer u een query uitvoert op taken, taken en rekenknooppunten Hello [Batch .NET] [ api_net] bibliotheek.

Bijna alle Batch-toepassingen moeten tooperform een soort bewaking of een andere bewerking Hallo Batch-service, vaak query met regelmatige tussenpozen. Bijvoorbeeld, toodetermine of er in een taak resterende taken in de wachtrij zijn, moet u gegevens ophalen voor elke taak in Hallo-taak. toodetermine hello status van knooppunten in uw pool, moet u gegevens op elk knooppunt in de groep Hallo ophalen. Dit artikel wordt uitgelegd hoe tooexecute zoals query's in Hallo zo efficiënt mogelijk.

> [!NOTE]
> Hallo Batch-service biedt speciale API-ondersteuning voor veelvoorkomende scenario Hallo van taken in een taak worden geteld. In plaats van een lijst met query om deze, kunt u Hallo aanroepen [ophalen taak telt] [ rest_get_task_counts] bewerking. Aantallen voor GET-taak geeft aan hoeveel taken in behandeling is, zijn uitgevoerd of voltooid en hoeveel taken hebt voltooid of mislukt. Get-taak telt is efficiënter dan een lijst met query. Zie voor meer informatie [aantal taken voor een taak op status (Preview)](batch-get-task-counts.md). 
>
> Hallo bewerking taak telt ophalen is niet beschikbaar in Batch-versies eerder dan 2017-06-01.5.1. Als u een oudere versie van het Hallo-service gebruikt, gebruikt u een lijst met query toocount taken in een taak in plaats daarvan.
>
> 

## <a name="meet-hello-detaillevel"></a>Voldoen aan de Hallo DetailLevel
In een productie-Batch-toepassing kunnen entiteiten, zoals jobs, taken en rekenknooppunten in Hallo duizendtallen nummeren. Wanneer u informatie over deze bronnen aanvraagt, moet een grote hoeveelheid gegevens 'afkomstig van Hallo kabel' hello Batch-servicetoepassing tooyour voor elke query. U kunt door te beperken het aantal items Hallo en type informatie dat wordt geretourneerd door een query, verhogen Hallo snelheid van uw query's en daarom Hallo prestaties van uw toepassing.

Dit [Batch .NET] [ api_net] API code codefragment lijsten *elke* taak die is gekoppeld aan een taak, samen met *alle* van eigenschappen van elke Hallo taak:

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

U kunt echter een lijstquery veel efficiënter uitvoeren door het toepassen van een query tooyour 'detailniveau'. Dit doet u door het leveren van een [ODATADetailLevel] [ odata] object toohello [JobOperations.ListTasks] [ net_list_tasks] methode. In dit fragment retourneert alleen Hallo-ID, opdrachtregel en compute knooppunt informatie eigenschappen van de voltooide taken:

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

In dit voorbeeldscenario als er duizenden taken in Hallo-job Hallo resultaten van de tweede query hello wordt doorgaans veel sneller dan Hallo als eerste geretourneerd. Meer informatie over het gebruik van ODATADetailLevel wanneer u objecten Hello Batch .NET API is opgenomen [hieronder](#efficient-querying-in-batch-net).

> [!IMPORTANT]
> Ten zeerste aangeraden dat u *altijd* leveringen een lijst ODATADetailLevel object tooyour .NET API-aanroepen van maximale efficiëntie tooensure en prestaties van uw toepassing. Door te geven een detailniveau, kunt u toolower Batch-service, reactietijden, netwerkgebruik te verbeteren en geheugengebruik minimaliseren door clienttoepassingen.
> 
> 

## <a name="filter-select-and-expand"></a>Filteren, selecteert en vouw
Hallo [Batch .NET] [ api_net] en [Batch REST] [ api_rest] API's bieden Hallo mogelijkheid tooreduce beide Hallo aantal items dat wordt geretourneerd in een lijst evenals Hallo hoeveelheid informatie die wordt geretourneerd voor elke. U dit doen door op te geven **filter**, **Selecteer**, en **Vouw tekenreeksen** bij het uitvoeren van de lijst met query's.

### <a name="filter"></a>Filteren
Hallo filtertekenreeks is een expressie die het aantal items dat wordt geretourneerd Hallo vermindert. Bijvoorbeeld: lijst alleen hello taken voor een taak, of de lijst alleen rekenknooppunten die gereed toorun taken zijn uitgevoerd.

* Hallo filtertekenreeks bestaat uit een of meer expressies met een expressie die uit een eigenschapsnaam, een operator en een waarde bestaat. Hallo-eigenschappen die kunnen worden opgegeven zijn specifieke tooeach entiteitstype waarmee u een query uitvoeren, zoals zijn Hallo-operators die worden ondersteund voor elke eigenschap.
* Meerdere expressies kunnen worden gecombineerd met behulp van de logische operators Hallo `and` en `or`.
* In dit voorbeeld filteren tekenreekslijsten alleen Hallo uitgevoerd 'weergeven' taken: `(state eq 'running') and startswith(id, 'renderTask')`.

### <a name="select"></a>Selecteer
Selecteer tekenreeks Hallo beperkt Hallo eigenschapswaarden die voor elk item worden geretourneerd. U geeft een lijst met namen van eigenschappen en alleen de eigenschapswaarden van deze worden geretourneerd voor items in de queryresultaten Hallo Hallo.

* Selecteer tekenreeks Hallo bestaat uit een door komma's gescheiden lijst met namen van eigenschappen. U kunt opgeven dat Hallo-eigenschappen voor het entiteitstype Hallo die u een query wilt uitvoeren.
* In dit voorbeeld selecteert tekenreeks dat slechts drie eigenschapswaarden voor elke taak moeten worden geretourneerd: `id, state, stateTransitionTime`.

### <a name="expand"></a>Uitvouwen
Hallo Vouw tekenreeks vermindert het aantal API-aanroepen die vereist tooobtain zijn Hallo bepaalde gegevens. Wanneer u een tekenreeks uit te breiden, meer informatie over elk item kan worden verkregen met één API-aanroep. In plaats van de eerste verkrijgen Hallo-lijst van entiteiten en vervolgens de aanvragende informatie voor elk item in de lijst hello, die u gebruikt een tekenreeks uit te breiden tooobtain Hallo dezelfde gegevens in één API-aanroep. Minder API-aanroepen betekent betere prestaties.

* Vergelijkbare toohello Selecteer tekenreeks Hallo uitvouwen tekenreeks of bepaalde gegevens in de queryresultaten lijst is opgenomen.
* Hallo Vouw tekenreeks wordt alleen ondersteund wanneer het wordt gebruikt in de lijst taken, taakschema's, taken en groepen. Op dit moment wordt alleen ondersteund statistische gegevens.
* Wanneer alle eigenschappen zijn vereist en er is geen tekenreeks select is opgegeven, Hallo tekenreeks uitvouwen *moet* worden statistische informatie over gebruikte tooget. Als een select-tekenreeks tooobtain een subset van de eigenschappen van de gebruikte is `stats` kan worden opgegeven in de select tekenreeks Hallo en Hallo Vouw tekenreeks niet hoeft toobe opgegeven.
* In dit voorbeeld Vouw tekenreeks geeft aan dat statistische gegevens moet worden geretourneerd voor elk item in de lijst Hallo: `stats`.

> [!NOTE]
> Tijdens het construeren van Hallo drie querytypen tekenreeks (filteren, selecteert en vouw), moet u ervoor zorgen dat Hallo eigenschapnamen en case overeenkomen met die van hun collega's REST-API-element. Bijvoorbeeld, als u werkt met .NET Hallo [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) klasse, moet u **status** in plaats van **status**, ook al Hallo .NET-eigenschap is [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state). Zie Hallo tabellen hieronder voor de eigenschaptoewijzingen tussen Hallo .NET en REST-API's.
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a>Regels voor filteren, selecteert en breidt tekenreeksen
* Namen van eigenschappen in het filter, selecteert en breidt tekenreeksen moeten worden weergegeven als in Hallo [Batch REST] [ api_rest] API--zelfs wanneer u [Batch .NET] [ api_net] of een andere Batch-SDK Hallo.
* Alle namen van eigenschappen zijn hoofdlettergevoelig, maar eigenschapswaarden zijn niet hoofdlettergevoelig.
* Datum/tijd tekenreeksen kunnen twee verschillende indelingen, en moet worden voorafgegaan door `DateTime`.
  
  * Voorbeeld van W3C-DTF-indeling:`creationTime gt DateTime'2011-05-08T08:49:37Z'`
  * Voorbeeld van RFC 1123 indeling:`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`
* Booleaanse tekenreeksen zijn `true` of `false`.
* Als een eigenschap is ongeldig of de operator is opgegeven, een `400 (Bad Request)` fout resulteert.

## <a name="efficient-querying-in-batch-net"></a>Efficiënter uitvoeren van query's in Batch .NET
Binnen Hallo [Batch .NET] [ api_net] API, Hallo [ODATADetailLevel] [ odata] klasse wordt gebruikt voor het verstrekken van filter, selecteren en uitvouwen tekenreeksen toolist bewerkingen. Hallo ODataDetailLevel klasse heeft drie openbare string-eigenschappen die kunnen worden opgegeven in de constructor Hallo of rechtstreeks op Hallo object ingesteld. U geeft Hallo ODataDetailLevel object als een parameter toohello verschillende bewerkingen na opvragen, zoals [ListPools][net_list_pools], [ListJobs][net_list_jobs], en [ListTasks][net_list_tasks].

* [ODATADetailLevel][odata].[ FilterClause][odata_filter]: Hallo aantal items dat wordt geretourneerd beperken.
* [ODATADetailLevel][odata].[ SelectClause][odata_select]: Geef op welke eigenschapswaarden worden geretourneerd bij elk item.
* [ODATADetailLevel][odata].[ ExpandClause][odata_expand]: gegevens ophalen voor alle artikelen in één API-aanroep in plaats van afzonderlijke aanroepen voor elk item.

Hallo volgende codefragment Hallo Batch .NET API tooefficiently query Hallo Batch-service gebruikt voor Hallo statistieken van een specifieke set met groepen. In dit scenario heeft Hallo Batch gebruiker test- en productie-groepen. Hallo test groep id's worden voorafgegaan door 'test' en Hallo productie groep id's worden voorafgegaan door 'prod'. In het Hallo-fragment *myBatchClient* is een goed geïnitialiseerd exemplaar van Hallo [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) klasse.

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
> Een exemplaar van [ODATADetailLevel] [ odata] die is geconfigureerd met selecteren en uitvouwen componenten kunnen ook worden doorgegeven tooappropriate Get-methoden, zoals [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , toolimit Hallo hoeveelheid gegevens die wordt geretourneerd.
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a>Batch REST-API voor too.NET toewijzingen
Namen van eigenschappen in het filter, selecteert en breidt tekenreeksen *moet* overeenstemming met de REST-API collega's, zowel in de naam en het geval is. Hallo onderstaande tabellen bevatten toewijzingen tussen Hallo .NET en REST-API collega's.

### <a name="mappings-for-filter-strings"></a>Toewijzingen voor tekenreeksen
* **.NET-lijst methoden**: Hallo .NET API methoden in deze kolom accepteert een [ODATADetailLevel] [ odata] -object als parameter.
* **Aanvragen voor REST-lijst**: elke REST-API pagina gekoppelde tooin in deze kolom bevat een tabel waarin Hallo eigenschappen en bewerkingen die zijn toegestaan in *filter* tekenreeksen. U gebruikt deze eigenschapnamen en bewerkingen wanneer u samenstellen een [ODATADetailLevel.FilterClause] [ odata_filter] tekenreeks.

| Methoden voor .NET-lijst | Aanvragen voor REST-lijst |
| --- | --- |
| [CertificateOperations.ListCertificates][net_list_certs] |[Hallo certificaten weergeven in een account][rest_list_certs] |
| [CloudTask.ListNodeFiles][net_list_task_files] |[Hallo-bestanden weergeven die zijn gekoppeld aan een taak][rest_list_task_files] |
| [JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status] |[Status van de lijst Hallo van Hallo taakvoorbereidings- en jobvrijgevingstaken voor een taak][rest_list_jobprep_status] |
| [JobOperations.ListJobs][net_list_jobs] |[Hallo-taken weergeven in een account][rest_list_jobs] |
| [JobOperations.ListNodeFiles][net_list_nodefiles] |[Lijst Hallo bestanden op een knooppunt][rest_list_nodefiles] |
| [JobOperations.ListTasks][net_list_tasks] |[Hallo taken die zijn gekoppeld aan een taak][rest_list_tasks] |
| [JobScheduleOperations.ListJobSchedules][net_list_job_schedules] |[Lijst Hallo taakschema's in een account][rest_list_job_schedules] |
| [JobScheduleOperations.ListJobs][net_list_schedule_jobs] |[Hallo-taken weergeven die zijn gekoppeld aan een jobplanning][rest_list_schedule_jobs] |
| [PoolOperations.ListComputeNodes][net_list_compute_nodes] |[Lijst Hallo rekenknooppunten in een groep][rest_list_compute_nodes] |
| [PoolOperations.ListPools][net_list_pools] |[Lijst Hallo opslaggroepen in een account][rest_list_pools] |

### <a name="mappings-for-select-strings"></a>Toewijzingen voor Selecteer tekenreeksen
* **Batch .NET-typen**: typen Batch .NET API.
* **REST-API-entiteiten**: elke pagina in deze kolom bevat een of meer tabellen die Hallo REST-API-Eigenschapsnamen voor Hallo type lijst. De namen van deze eigenschappen worden gebruikt wanneer u samenstellen *Selecteer* tekenreeksen. U gebruikt deze dezelfde eigenschapnamen als u een [ODATADetailLevel.SelectClause] [ odata_select] tekenreeks.

| Batch .NET-typen | REST-API-entiteiten |
| --- | --- |
| [Certificaat][net_cert] |[Informatie ophalen over een certificaat][rest_get_cert] |
| [CloudJob][net_job] |[Informatie over een taak ophalen][rest_get_job] |
| [CloudJobSchedule][net_schedule] |[Informatie over het schema van een taak ophalen][rest_get_schedule] |
| [ComputeNode][net_node] |[Informatie ophalen over een knooppunt][rest_get_node] |
| [CloudPool][net_pool] |[Informatie ophalen over een groep][rest_get_pool] |
| [CloudTask][net_task] |[Informatie over een taak ophalen][rest_get_task] |

## <a name="example-construct-a-filter-string"></a>Voorbeeld: een filtertekenreeks maken
Wanneer u een filtertekenreeks voor samenstellen [ODATADetailLevel.FilterClause][odata_filter], raadpleegt u bovenstaande Hallo tabel onder '-toewijzingen voor filtertekenreeksen' toofind Hallo REST-API-documentatiepagina die overeenkomt met toohello lijstbewerking gewenste tooperform. Vindt u Hallo Filterbaar eigenschappen en hun ondersteunde operators in Hallo eerste multirow tabel op die pagina. Als u wenst dat tooretrieve alle taken waarvan afsluitcode niet nul was, bijvoorbeeld dit rij op [Hallo taken die zijn gekoppeld aan een taak] [ rest_list_tasks] Hallo toepasselijke eigenschap tekenreeks en de toegestane operators:

| Eigenschap | Bewerkingen die zijn toegestaan | Type |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

Hallo filtertekenreeks voor het weergeven van alle taken met een andere afsluitcode dan zou dus zijn:

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a>Voorbeeld: een select tekenreeks maken
tooconstruct [ODATADetailLevel.SelectClause][odata_select], raadpleegt u bovenstaande Hallo tabel onder '-toewijzingen voor Selecteer tekenreeksen' en navigeer toohello REST-API-pagina die overeenkomt met het type entiteit toohello die u hebt biedt. Vindt u Hallo selecteerbare eigenschappen en hun ondersteunde operators in Hallo eerste multirow tabel op die pagina. Als u wenst dat tooretrieve alleen Hallo-ID en vanaf de opdrachtregel voor elke taak in een lijst, bijvoorbeeld vindt u deze rijen in de toepasselijke tabel Hallo op [informatie ophalen over een taak][rest_get_task]:

| Eigenschap | Type | Opmerkingen |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

Hallo Selecteer string zou voor waaronder alleen Hallo-ID en -opdrachtregel met elke vermelde taak vervolgens zijn:

`id, commandLine`

## <a name="code-samples"></a>Codevoorbeelden
### <a name="efficient-list-queries-code-sample"></a>Voorbeeld van code voor efficiënte lijst met query 's
Bekijk Hallo [EfficientListQueries] [ efficient_query_sample] voorbeeldproject op GitHub toosee hoe efficiënt lijst uitvoeren van query's kan invloed hebben op prestaties in een toepassing. Deze C#-consoletoepassing maakt en een groot aantal taken tooa taak toegevoegd. Klik op deze manier meerdere aanroepen toohello [JobOperations.ListTasks] [ net_list_tasks] methode en geeft [ODATADetailLevel] [ odata] objecten die zijn geconfigureerd met een andere eigenschap waarden toovary Hallo hoeveelheid gegevens toobe geretourneerd. Het volgende voor vergelijkbare toohello uitvoer genereert:

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

Zoals u in Hallo verstreken keren, kunt u de reactietijden van de query aanzienlijk verlagen door te beperken Hallo eigenschappen en Hallo aantal items dat wordt geretourneerd. U vindt deze en andere voorbeeldprojecten in Hallo [azure-batch-samples] [ github_samples] opslagplaats op GitHub.

### <a name="batchmetrics-library-and-code-sample"></a>BatchMetrics-bibliotheek en code-voorbeeld
Bovendien toohello EfficientListQueries codevoorbeeld bovenstaande, kunt u vinden Hallo [BatchMetrics] [ batch_metrics] -project in Hallo [azure-batch-samples] [ github_samples] GitHub-opslagplaats. Hallo BatchMetrics voorbeeldproject laat zien hoe de Azure Batch-taak uitgevoerd met Hallo Batch-API voor het bewaken van tooefficiently.

Hallo [BatchMetrics] [ batch_metrics] voorbeeld bevat een bibliotheekproject voor .NET-klasse die u in uw eigen projecten en een eenvoudig opdrachtregelprogramma opnemen kunt tooexercise programma en gebruik Hallo Hallo demonstreren bibliotheek.

Hallo-voorbeeldtoepassing in Hallo project toont Hallo volgende bewerkingen:

1. Specifieke kenmerken in de volgorde toodownload alleen Hallo eigenschappen selecteren die u nodig hebt
2. Filteren op status overgang keer volgorde toodownload alleen wijzigingen sinds de laatste query waarvoor een Hallo

Bijvoorbeeld, weergegeven Hallo methode na in Hallo BatchMetrics-bibliotheek. Deze retourneert een ODATADetailLevel waarmee wordt aangegeven dat alleen Hallo `id` en `state` eigenschappen moeten worden opgehaald voor Hallo entiteiten die zijn opgevraagd. Ook wordt hiermee aangegeven dat alleen entiteiten waarvan de status is gewijzigd sinds de opgegeven Hallo `DateTime` parameter moet worden geretourneerd.

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a>Volgende stappen
### <a name="parallel-node-tasks"></a>Knooppunt parallelle taken
[Azure Batch compute Resourcegebruik met gelijktijdige knooppunt taken maximaliseren](batch-parallel-node-tasks.md) is een ander artikel betrekking tooBatch toepassingsprestaties. Bepaalde typen werkbelastingen kunnen profiteren van parallelle taken worden uitgevoerd op grotere-- maar minder--rekenknooppunten. Bekijk Hallo [voorbeeldscenario](batch-parallel-node-tasks.md#example-scenario) in Hallo-artikel voor meer informatie over dit scenario.

### <a name="batch-forum"></a>Batch-Forum
Hallo [Azure Batch-Forum] [ forum] is uitermate toodiscuss Batch plaats en vragen over Hallo-service op MSDN. Kop op via voor nuttige 'een tijdelijke' berichten, en stel uw vragen wanneer deze zich voordoen tijdens het bouwen van uw Batch-oplossingen.

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